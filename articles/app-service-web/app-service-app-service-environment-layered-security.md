---
title: "Architektura zabezpieczeń warstwowych ze środowiska usługi aplikacji"
description: "Implementacja architektury zabezpieczeń warstwowych, ze środowiska usługi App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="79b7d-103">Implementacja architektury zabezpieczeń warstwowych, ze środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="79b7d-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="79b7d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="79b7d-104">Overview</span></span>
<span data-ttu-id="79b7d-105">Ponieważ środowiska usługi App Service udostępniają odizolowanym środowisku uruchomieniowym wdrożony w sieci wirtualnej, deweloperzy mogą tworzyć architektury zabezpieczeń warstwowych, zapewniając różne poziomy dostępu do sieci dla każdej warstwy aplikacji fizycznych.</span><span class="sxs-lookup"><span data-stu-id="79b7d-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="79b7d-106">Wspólne dążenie jest Ukryj zapleczy interfejsu API z dostępem do Internetu ogólne i Zezwalaj tylko na interfejsy API do wywołania przez aplikacje sieci web nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="79b7d-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="79b7d-107">[Sieciowe grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] pozwala na podsieci zawierający środowiska usługi App Service ograniczenia publiczny dostęp do aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="79b7d-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="79b7d-108">Na poniższym diagramie przedstawiono architekturę przykład z aplikacją WebAPI na podstawie wdrożony w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79b7d-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="79b7d-109">Trzy wystąpienia aplikacji sieci web w osobnych, wdrożone na trzy osobne środowiska usługi aplikacji wywołań zaplecza w tej samej aplikacji WebAPI.</span><span class="sxs-lookup"><span data-stu-id="79b7d-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Architektura koncepcyjna][ConceptualArchitecture] 

<span data-ttu-id="79b7d-111">Zielony znak plus wskazują, że grupy zabezpieczeń sieci w podsieci zawierający "apiase" umożliwia wywołania z aplikacji sieci web nadrzędnego jako dobrze wywołania po sobie samym.</span><span class="sxs-lookup"><span data-stu-id="79b7d-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="79b7d-112">Jednak tej samej grupy zabezpieczeń sieci jawnie nie zezwala na dostęp do ogólnego ruch przychodzący z Internetu.</span><span class="sxs-lookup"><span data-stu-id="79b7d-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="79b7d-113">W pozostałej części w tym temacie przedstawiono kroki potrzebne do skonfigurowania sieciowej grupy zabezpieczeń w podsieci zawierający "apiase".</span><span class="sxs-lookup"><span data-stu-id="79b7d-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="79b7d-114">Określanie zachowania sieci</span><span class="sxs-lookup"><span data-stu-id="79b7d-114">Determining the Network Behavior</span></span>
<span data-ttu-id="79b7d-115">Aby dowiedzieć się, jakie reguły zabezpieczeń sieciowych są potrzebne, musisz określić klientów sieci będzie mogło nawiązać środowiska usługi aplikacji zawierającej aplikację interfejsu API i których klienci będą blokowane.</span><span class="sxs-lookup"><span data-stu-id="79b7d-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="79b7d-116">Ponieważ [sieciowej grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] są stosowane do podsieci i środowiska usługi App Service są wdrażane na podsieci, zasad zawartych w grupie NSG są stosowane do **wszystkie** aplikacje działające w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79b7d-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="79b7d-117">Przy użyciu architektury próbki tego artykułu, po zastosowaniu sieciową grupę zabezpieczeń do podsieci, zawierający "apiase", wszystkie aplikacje uruchomione na "apiase" środowiska usługi aplikacji będą chronione za pomocą tego samego zestawu reguł zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="79b7d-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="79b7d-118">**Określić wychodzący adres IP nadrzędne obiekty wywołujące:** co to jest adres IP lub adresy nadrzędne obiekty wywołujące?</span><span class="sxs-lookup"><span data-stu-id="79b7d-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="79b7d-119">Te adresy musi być jawnie dozwolone dostępu w grupie NSG.</span><span class="sxs-lookup"><span data-stu-id="79b7d-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="79b7d-120">Ponieważ wywołań między środowiska usługi App Service są traktowane jako wywołania "Internet", oznacza to, że wychodzący adres IP przypisany do każdego z trzech nadrzędnego środowiska usługi aplikacji musi mieć dostęp w grupie NSG dla podsieci "apiase".</span><span class="sxs-lookup"><span data-stu-id="79b7d-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="79b7d-121">Aby uzyskać więcej informacji na temat określania wychodzący adres IP, aby aplikacje działające w środowisku usługi aplikacji, zobacz [architektury sieci] [ NetworkArchitecture] artykuł z omówieniem.</span><span class="sxs-lookup"><span data-stu-id="79b7d-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="79b7d-122">**W aplikacji interfejsu API zaplecza trzeba wywołać się?**</span><span class="sxs-lookup"><span data-stu-id="79b7d-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="79b7d-123">Czasami ich i niewielkie punkt jest scenariusz, w którym aplikacja zaplecza musi wywołać się.</span><span class="sxs-lookup"><span data-stu-id="79b7d-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="79b7d-124">Jeśli aplikacji interfejsu API zaplecza w środowisku usługi aplikacji musi wywołać się, to także traktowane jako wywołanie "Internet".</span><span class="sxs-lookup"><span data-stu-id="79b7d-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="79b7d-125">W architekturze próbki wymaga zezwalania na dostęp z wychodzący adres IP "apiase" środowiska usługi aplikacji oraz.</span><span class="sxs-lookup"><span data-stu-id="79b7d-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="79b7d-126">Konfigurowanie grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="79b7d-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="79b7d-127">Zestaw wychodzących adresów IP są znane, następnym krokiem po do utworzenia grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="79b7d-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="79b7d-128">Można utworzyć grupy zabezpieczeń sieci dla obu Menedżera zasobów opartych na sieci wirtualnych, a także klasycznych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="79b7d-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="79b7d-129">Poniższe przykłady Pokaż tworzenia i konfigurowania grupy NSG w klasycznym sieci wirtualnej przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="79b7d-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="79b7d-130">Dla architektury próbki tych środowisk znajdują się w południowo-środkowe stany, więc pusta grupa NSG jest tworzona w tym regionie:</span><span class="sxs-lookup"><span data-stu-id="79b7d-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="79b7d-131">Najpierw jawnie zezwolić na reguły jest dodawany do infrastruktury zarządzania platformy Azure, zgodnie z opisem w artykule na [ruch przychodzący] [ InboundTraffic] dla środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="79b7d-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="79b7d-132">Następnie dwie reguły są dodawane do zezwala na wywołania HTTP i HTTPS z pierwszego środowiska usługi aplikacji nadrzędnego ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="79b7d-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b7d-133">Przepłukać i powtórz dla drugiego i trzeciego nadrzędnego środowiska usługi App Service ("fe2ase" i "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="79b7d-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b7d-134">Ponadto należy udzielić dostępu do środowiska usługi aplikacji interfejsu API zaplecza wychodzących adres IP, dzięki czemu można wywołania zwrotnego do tego samego.</span><span class="sxs-lookup"><span data-stu-id="79b7d-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b7d-135">Żadne inne reguły zabezpieczeń sieci należy skonfigurować co grupa NSG ma zestaw reguł domyślnych, które blokują dostęp przychodzące z Internetu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="79b7d-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="79b7d-136">Poniżej przedstawiono pełną listę reguł w grupie zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="79b7d-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="79b7d-137">Należy zwrócić uwagę, jak ostatni reguły, która zostanie wyróżniona, blokuje dostęp dla ruchu przychodzącego z wszystkich wywołań innych niż te, które jawnie przyznano dostęp.</span><span class="sxs-lookup"><span data-stu-id="79b7d-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Konfiguracja grupy NSG][NSGConfiguration] 

<span data-ttu-id="79b7d-139">Ostatnim krokiem jest aby zastosować grupy NSG do podsieci, która zawiera "apiase" środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79b7d-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="79b7d-140">Grupa NSG stosowana do podsieci tylko trzy nadrzędnego środowiska usługi App Service i środowiska usługi aplikacji zawierające zaplecza interfejsu API, są dozwolone do wywołania w środowisku "apiase".</span><span class="sxs-lookup"><span data-stu-id="79b7d-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="79b7d-141">Linki do dodatkowych i informacji</span><span class="sxs-lookup"><span data-stu-id="79b7d-141">Additional Links and Information</span></span>
<span data-ttu-id="79b7d-142">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="79b7d-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="79b7d-143">Informacje o [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="79b7d-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="79b7d-144">Opis [wychodzących adresów IP] [ NetworkArchitecture] i środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="79b7d-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="79b7d-145">[Porty sieciowe] [ InboundTraffic] używane przez środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="79b7d-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
