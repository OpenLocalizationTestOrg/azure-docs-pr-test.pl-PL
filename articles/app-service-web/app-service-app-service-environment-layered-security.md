---
title: "aaaLayered Architektura zabezpieczeń ze środowiska usługi App Service"
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
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="b1dc9-103">Implementacja architektury zabezpieczeń warstwowych, ze środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1dc9-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="b1dc9-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b1dc9-104">Overview</span></span>
<span data-ttu-id="b1dc9-105">Ponieważ środowiska usługi App Service udostępniają odizolowanym środowisku uruchomieniowym wdrożony w sieci wirtualnej, deweloperzy mogą tworzyć architektury zabezpieczeń warstwowych, zapewniając różne poziomy dostępu do sieci dla każdej warstwy aplikacji fizycznych.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="b1dc9-106">Wspólne dążenie jest toohide interfejsu API zapleczy z dostępem do Internetu ogólne i Zezwalaj tylko na interfejsy API toobe wywoływany przez aplikacje sieci web nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="b1dc9-107">[Sieciowe grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] mogą być używane w podsieci zawierający aplikacje tooAPI dostępu publicznego toorestrict środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="b1dc9-108">Hello Poniższy diagram przedstawia architekturę przykład z aplikacją WebAPI na podstawie wdrożony w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="b1dc9-109">Trzy wystąpienia aplikacji sieci web w osobnych, wdrożone na trzy osobne środowiska usługi aplikacji należy toohello zaplecza wywołania tej samej aplikacji WebAPI.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Architektura koncepcyjna][ConceptualArchitecture] 

<span data-ttu-id="b1dc9-111">Witaj zielony znak plus wskazać, że hello sieciowej grupy zabezpieczeń w podsieci hello zawierający "apiase" umożliwia wywołania z hello aplikacji sieci web nadrzędnego jako dobrze wywołania po sobie samym.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="b1dc9-112">Jednak hello tej samej grupy zabezpieczeń sieci jawnie nie zezwala na dostęp do toogeneral ruchu przychodzącego ruchu z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="b1dc9-113">Witaj pozostałej części tego tematu przeprowadzi Cię przez hello kroki potrzebne tooconfigure hello sieciowej grupy zabezpieczeń w podsieci hello zawierający "apiase".</span><span class="sxs-lookup"><span data-stu-id="b1dc9-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="b1dc9-114">Określanie hello zachowanie sieci</span><span class="sxs-lookup"><span data-stu-id="b1dc9-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="b1dc9-115">W kolejności tooknow zabezpieczenia sieci, jakie potrzebne są zasady, konieczne toodetermine klientów sieci, które mogą być tooreach hello środowiska usługi aplikacji zawierającego hello aplikacji interfejsu API i których klienci będą blokowane.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="b1dc9-116">Ponieważ [sieciowej grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] są stosowane toosubnets i środowiska usługi App Service są wdrażane na podsieci, hello reguły zawarte w grupy NSG stosuje się zbyt**wszystkie** aplikacje działające w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="b1dc9-117">Przy użyciu hello przykładowa architektura tego artykułu, grupy zabezpieczeń sieci po podsieci zastosowane toohello zawierającej "apiase", wszystkie aplikacje uruchomione na powitania "apiase" środowiska usługi aplikacji, które będą chronione za pomocą hello sam zestaw reguł zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="b1dc9-118">**Określić hello wychodzący adres IP nadrzędnego obiektów wywołujących:** co to jest hello adres lub adresy IP z wywołań nadrzędnego hello?</span><span class="sxs-lookup"><span data-stu-id="b1dc9-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="b1dc9-119">Te adresy muszą toobe jawnie dozwolone w hello NSG dostępu.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="b1dc9-120">Ponieważ wywołań między środowiska usługi App Service są traktowane jako wywołania "Internet", oznacza to hello wychodzącego IP przypisany adres tooeach z hello trzy nadrzędnego środowiska usługi App Service musi toobe zezwolenie na dostęp w hello NSG dla podsieci "apiase" hello.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="b1dc9-121">Aby uzyskać więcej informacji na temat określania hello wychodzący adres IP, aplikacje działające w środowisku usługi aplikacji można znaleźć hello [architektury sieci] [ NetworkArchitecture] artykuł z omówieniem.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="b1dc9-122">**Aplikacja interfejsu API zaplecza hello należy toocall się?**</span><span class="sxs-lookup"><span data-stu-id="b1dc9-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="b1dc9-123">Czasami ich i niewielkie punkt jest scenariusz hello których hello zaplecza aplikacji wymaga toocall samej siebie.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="b1dc9-124">Jeśli w aplikacji interfejsu API zaplecza w środowisku usługi aplikacji wymaga toocall samego, to także traktowane jako wywołanie "Internet".</span><span class="sxs-lookup"><span data-stu-id="b1dc9-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="b1dc9-125">W architekturze próbki hello wymaga zezwalania na dostęp z hello wychodzący adres IP hello "apiase" środowiska usługi aplikacji oraz.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="b1dc9-126">Konfigurowanie hello grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="b1dc9-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="b1dc9-127">Po ustawieniu hello z wychodzących adresów IP są znane, hello następnym krokiem jest tooconstruct grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="b1dc9-128">Można utworzyć grupy zabezpieczeń sieci dla obu Menedżera zasobów opartych na sieci wirtualnych, a także klasycznych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="b1dc9-129">Poniższe przykłady Hello Pokaż tworzenia i konfigurowania grupy NSG w klasycznym sieci wirtualnej przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="b1dc9-130">Dla architektury próbki hello środowisk hello znajdują się w południowo-środkowe stany, więc pusta grupa NSG jest tworzona w tym regionie:</span><span class="sxs-lookup"><span data-stu-id="b1dc9-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="b1dc9-131">Najpierw jawnie zezwolić na reguła jest dodawana hello infrastruktury zarządzania platformy Azure, zgodnie z opisem w artykule hello na [ruch przychodzący] [ InboundTraffic] dla środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="b1dc9-132">Następnie dwie reguły są dodawane tooallow HTTP i HTTPS wywołania z hello pierwszy nadrzędnego środowiska usługi aplikacji ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="b1dc9-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="b1dc9-133">Płukania i powtórz te czynności dla hello drugiego i trzeciego nadrzędnego środowiska usługi App Service ("fe2ase" i "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="b1dc9-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="b1dc9-134">Ponadto należy udzielić dostępu toohello wychodzący adres IP środowiska usługi aplikacji hello zaplecza interfejsu API, dzięki czemu można wywołania zwrotnego do samej siebie.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="b1dc9-135">Nie inne reguły zabezpieczeń sieciowych muszą toobe skonfigurowany, ponieważ co grupa NSG zawiera zestaw reguł domyślnych, które blokują dostęp przychodzące z Internetu hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="b1dc9-136">Poniżej przedstawiono pełną listę reguł w grupie zabezpieczeń sieci hello Hello.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="b1dc9-137">Należy zwrócić uwagę, jak reguły ostatniego hello, który zostanie wyróżniona, blokuje przychodzące dostęp z wszystkich wywołań innych niż te, które jawnie przyznano dostęp.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Konfiguracja grupy NSG][NSGConfiguration] 

<span data-ttu-id="b1dc9-139">Ostatnim krokiem Hello jest tooapply hello NSG toohello podsieci, która zawiera hello "apiase" środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="b1dc9-140">Z podsiecią toohello grupa NSG stosowana hello hello trzy nadrzędnego środowiska usługi App Service i hello środowiska usługi aplikacji hello zawierającego zaplecza interfejsu API, dozwolone są tylko toocall do środowiska "apiase" hello.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="b1dc9-141">Linki do dodatkowych i informacji</span><span class="sxs-lookup"><span data-stu-id="b1dc9-141">Additional Links and Information</span></span>
<span data-ttu-id="b1dc9-142">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="b1dc9-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="b1dc9-143">Informacje o [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="b1dc9-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="b1dc9-144">Opis [wychodzących adresów IP] [ NetworkArchitecture] i środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="b1dc9-145">[Porty sieciowe] [ InboundTraffic] używane przez środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b1dc9-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
