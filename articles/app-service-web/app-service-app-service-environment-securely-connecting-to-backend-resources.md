---
title: "aaaSecurely tooBackEnd łączenie zasobów z środowiska usługi aplikacji"
description: "Więcej informacji na temat sposobu toosecurely łączenie zasobów toobackend ze środowiska usługi aplikacji."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="b30c9-103">Bezpieczne łączenie tooBackend zasobów ze środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b30c9-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="b30c9-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b30c9-104">Overview</span></span>
<span data-ttu-id="b30c9-105">Od chwili utworzenia środowiska usługi aplikacji jest zawsze w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** klasycznego modelu wdrażania [sieci wirtualnej] [ virtualnetwork], przepływ wyłącznie za pośrednictwem sieci wirtualnej hello połączenia wychodzące z zasobami zaplecza tooother środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b30c9-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="b30c9-106">Z ostatnie zmiany wprowadzone w czerwca 2016 ASEs można także wdrożyć w sieci wirtualnych, które używają zakresy publicznych adresów lub RFC1918 przestrzeni adresów (czyli adresy prywatne).</span><span class="sxs-lookup"><span data-stu-id="b30c9-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="b30c9-107">Na przykład może być programu SQL Server w klastrze maszyn wirtualnych z portu 1433 zablokowana.</span><span class="sxs-lookup"><span data-stu-id="b30c9-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="b30c9-108">punkt końcowy Hello może być ACLd tooonly zezwolić na dostęp z innych zasobów na hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b30c9-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="b30c9-109">Inny przykład poufnych punkty końcowe może uruchomić lokalnie i być tooAzure połączonych za pośrednictwem albo [lokacja-lokacja] [ SiteToSite] lub [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="b30c9-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="b30c9-110">W związku z tym zasobów tylko w sieciach wirtualnych połączona toohello lokacja-lokacja lub ExpressRoute tunele będą punkty końcowe lokalnymi tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="b30c9-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="b30c9-111">Dla wszystkich tych scenariuszach aplikacje działające w środowisku usługi aplikacji będzie można toosecurely stanie łączyć toohello różnych serwerów i zasobów.</span><span class="sxs-lookup"><span data-stu-id="b30c9-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="b30c9-112">Ruch wychodzący z aplikacji działających w punktów końcowych tooprivate środowiska usługi aplikacji w hello tej samej sieci wirtualnej (lub podłączone toohello tej samej sieci wirtualnej), zostanie tylko przepływ hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b30c9-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="b30c9-113">Tooprivate ruchu wychodzącego, które punkty końcowe nie będzie przepływać przez hello publicznej sieci Internet.</span><span class="sxs-lookup"><span data-stu-id="b30c9-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="b30c9-114">Jedno zastrzeżenie: dotyczy ruchu toooutbound z tooendpoints środowiska usługi aplikacji w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b30c9-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="b30c9-115">Środowiska usługi App Service można nawiązać połączenia z punktami końcowymi maszyn wirtualnych znajdujących się w hello **tego samego** podsieci jako hello środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b30c9-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="b30c9-116">To zwykle nie powinna być problem tak długo, jak środowiska usługi App Service są wdrażane w podsieci zarezerwowane do wyłącznego użytku przez hello środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b30c9-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="b30c9-117">Łączność wychodząca i wymagania dotyczące systemu DNS</span><span class="sxs-lookup"><span data-stu-id="b30c9-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="b30c9-118">Dla środowiska usługi aplikacji toofunction poprawnie, wymaga punkty końcowe toovarious wychodzący dostęp.</span><span class="sxs-lookup"><span data-stu-id="b30c9-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="b30c9-119">Pełną listę zewnętrzne punkty końcowe hello używane przez ASE jest hello sekcji "Wymagana łączność sieciową" hello [konfiguracji sieci ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b30c9-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="b30c9-120">Środowiska usługi aplikacji wymagają skonfigurowanej dla sieci wirtualnej hello prawidłowy infrastruktury DNS.</span><span class="sxs-lookup"><span data-stu-id="b30c9-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="b30c9-121">Jeśli dla dowolnego hello Przyczyna konfiguracji DNS została zmieniona po utworzeniu środowiska usługi aplikacji, deweloperzy można wymusić toopick środowiska usługi aplikacji hello nowej konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="b30c9-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="b30c9-122">Wyzwolenie stopniowego ponowny rozruch środowiska za pomocą ikony "Restart" hello, znajdujący się u góry hello hello środowiska usługi aplikacji blok zarządzania w portalu hello spowoduje toopick środowiska hello hello nowej konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="b30c9-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="b30c9-123">Zalecane jest również, że żadnych niestandardowych serwerów DNS w sieci wirtualnej hello należy skonfigurować przed toocreating wcześniejsze czasu środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b30c9-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="b30c9-124">Konfiguracja DNS sieci wirtualnej zostanie zmieniona, podczas tworzenia środowiska usługi aplikacji, która spowoduje niepowodzenie procesu tworzenia środowiska usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b30c9-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="b30c9-125">W podobny szyjnej Jeśli istnieje niestandardowy serwer DNS na powitania drugiej bramy sieci VPN, a serwer DNS hello jest hello jest nieosiągalny lub jest niedostępny, również zakończą się proces tworzenia środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b30c9-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="b30c9-126">Łączenie tooa programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="b30c9-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="b30c9-127">Typowe konfiguracje programu SQL Server ma punktu końcowego nasłuchiwania na porcie 1433:</span><span class="sxs-lookup"><span data-stu-id="b30c9-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Punkt końcowy serwera SQL][SqlServerEndpoint]

<span data-ttu-id="b30c9-129">Istnieją dwa podejścia do ograniczania ruchu toothis końcowego:</span><span class="sxs-lookup"><span data-stu-id="b30c9-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="b30c9-130">[Listy kontroli dostępu do sieci] [ NetworkAccessControlLists] (listy ACL sieci)</span><span class="sxs-lookup"><span data-stu-id="b30c9-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="b30c9-131">[Grupy zabezpieczeń sieci][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="b30c9-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="b30c9-132">Ograniczanie dostępu do sieci listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="b30c9-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="b30c9-133">Port 1433 mogą być chronione przy użyciu listy kontroli dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="b30c9-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="b30c9-134">przykład Witaj poniżej klienta whitelists adresów pochodzące z wewnątrz sieci wirtualnej i zablokuje dostęp tooall innych klientów.</span><span class="sxs-lookup"><span data-stu-id="b30c9-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Przykład listy kontroli dostępu do sieci][NetworkAccessControlListExample]

<span data-ttu-id="b30c9-136">Wszystkie aplikacje uruchomione w środowisku usługi aplikacji w tej samej sieci wirtualnej Witaj, ponieważ hello programu SQL Server będzie wystąpienia programu SQL Server toohello tooconnect możliwe przy użyciu hello **wewnętrznej sieci wirtualnej** adres IP dla maszyny wirtualnej hello programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b30c9-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="b30c9-137">Parametry połączenia przykład Hello poniżej odwołania hello SQL Server przy użyciu prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="b30c9-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="b30c9-138">Mimo że hello maszyna wirtualna ma publiczny punkt końcowy również, próby nawiązania połączenia z użyciem hello publiczny adres IP zostanie odrzucone z powodu sieci hello listy ACL.</span><span class="sxs-lookup"><span data-stu-id="b30c9-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="b30c9-139">Ograniczanie dostępu z sieciową grupą zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b30c9-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="b30c9-140">Informacje o innym podejściu do zabezpieczania dostępu jest z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b30c9-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="b30c9-141">Grupy zabezpieczeń sieci może być zastosowane tooindividual maszyn wirtualnych lub podsieci tooa zawierających maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="b30c9-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="b30c9-142">Grupa zabezpieczeń sieci musi najpierw toobe utworzone:</span><span class="sxs-lookup"><span data-stu-id="b30c9-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="b30c9-143">Ograniczanie dostępu tooonly ruchu w sieci wewnętrznej jest bardzo prosty z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b30c9-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="b30c9-144">reguły domyślne Hello w grupie zabezpieczeń sieci tylko zezwalają na dostęp z innych klientów sieci w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b30c9-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="b30c9-145">W związku z tym blokowania dostępu tooSQL serwer jest tak proste, jak stosowanie sieciową grupę zabezpieczeń z jego domyślne zasady tooeither hello maszynami wirtualnymi programu SQL Server lub podsieci hello zawierającej hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b30c9-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="b30c9-146">Poniższy przykład Hello stosuje zabezpieczeń grupy toohello zawierający podsieci:</span><span class="sxs-lookup"><span data-stu-id="b30c9-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="b30c9-147">wynik końcowy Hello jest zestaw reguł zabezpieczeń, które blokują dostęp zewnętrznych, umożliwiając dostęp do sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b30c9-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Reguły zabezpieczeń sieciowych domyślne][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="b30c9-149">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b30c9-149">Getting started</span></span>
<span data-ttu-id="b30c9-150">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="b30c9-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="b30c9-151">tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="b30c9-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="b30c9-152">Szczegółowe wokół kontrolowanie ruchu przychodzącego tooyour środowiska usługi aplikacji, zobacz [kontrolowanie ruchu przychodzącego tooan środowiska usługi aplikacji][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="b30c9-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="b30c9-153">Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="b30c9-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
