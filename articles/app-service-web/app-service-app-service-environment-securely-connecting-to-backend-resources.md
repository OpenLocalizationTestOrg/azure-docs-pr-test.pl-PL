---
title: "Bezpieczne łączenie z zasobami zaplecza ze środowiska usługi aplikacji"
description: "Dowiedz się więcej o tym, jak bezpiecznie łączyć się z zasobami zaplecza ze środowiska usługi aplikacji."
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="ea0eb-103">Bezpieczne łączenie z zasobami zaplecza ze środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="ea0eb-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="ea0eb-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ea0eb-104">Overview</span></span>
<span data-ttu-id="ea0eb-105">Od chwili utworzenia środowiska usługi aplikacji jest zawsze w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** klasycznego modelu wdrażania [sieci wirtualnej] [ virtualnetwork], połączenia wychodzące z środowiska usługi aplikacji do innych zasobów w wewnętrznej bazie danych może przepływać wyłącznie za pośrednictwem sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="ea0eb-106">Z ostatnie zmiany wprowadzone w czerwca 2016 ASEs można także wdrożyć w sieci wirtualnych korzystających z zakresów adresów publicznych lub przestrzenie adresowe RFC1918 (tj.)</span><span class="sxs-lookup"><span data-stu-id="ea0eb-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="ea0eb-107">adresy prywatne).</span><span class="sxs-lookup"><span data-stu-id="ea0eb-107">private addresses).</span></span>  

<span data-ttu-id="ea0eb-108">Na przykład może być programu SQL Server w klastrze maszyn wirtualnych z portu 1433 zablokowana.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="ea0eb-109">Punkt końcowy może być ACLd tylko umożliwiających dostęp do innych zasobów w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="ea0eb-110">Inny przykład poufnych punkty końcowe mogą uruchomić lokalnie i być podłączona do platformy Azure przez albo [lokacja-lokacja] [ SiteToSite] lub [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="ea0eb-111">W związku z tym tylko zasoby w sieciach wirtualnych połączony lokacja-lokacja lub ExpressRoute tunele będą możliwość dostępu z lokalnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="ea0eb-112">Wszystkie te scenariusze aplikacje działające w środowisku usługi aplikacji będzie można bezpiecznie łączyć się z różnych serwerów i zasobów z.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="ea0eb-113">Ruch wychodzący z aplikacji działających w środowisku usługi aplikacji do prywatnego punktów końcowych w tej samej sieci wirtualnej (lub podłączone do tej samej sieci wirtualnej), zostanie tylko przepływ za pośrednictwem sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="ea0eb-114">Ruch wychodzący do punktów końcowych prywatnych nie będą przepływać za pośrednictwem publicznej sieci Internet.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="ea0eb-115">Jedno zastrzeżenie: dotyczy ruchu wychodzącego ze środowiska usługi aplikacji do punktów końcowych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="ea0eb-116">Środowiska usługi App Service można nawiązać połączenia z punktami końcowymi maszyn wirtualnych znajdujących się w **tego samego** podsieci co środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="ea0eb-117">To zwykle nie powinna być problem tak długo, jak środowiska usługi App Service są wdrażane w podsieci zarezerwowane do wyłącznego użytku przez środowisko usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="ea0eb-118">Łączność wychodząca i wymagania dotyczące systemu DNS</span><span class="sxs-lookup"><span data-stu-id="ea0eb-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="ea0eb-119">Dla środowiska usługi aplikacji do poprawnego wymaga wychodzący dostęp do różnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="ea0eb-120">Pełna lista zewnętrznych punktów końcowych używanych przez ASE znajduje się w sekcji "Wymagana łączność sieciową" [konfiguracji sieci ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="ea0eb-121">Środowiska usługi aplikacji wymaga prawidłowy infrastruktury DNS skonfigurowane dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="ea0eb-122">Jeśli z jakiegokolwiek powodu konfiguracji DNS zostaną zmienione po utworzeniu środowiska usługi aplikacji, deweloperzy można wymusić środowiska usługi aplikacji do pobrania dla nowej konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="ea0eb-123">Wyzwolenie stopniowego ponowny rozruch środowiska przy użyciu ikony "Restart" znajduje się w górnej części bloku zarządzania środowiska usługi aplikacji w portalu spowoduje, że środowisko do pobrania dla nowej konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="ea0eb-124">Zalecane jest również, że żadnych niestandardowych serwerów DNS w sieci wirtualnej, należy skonfigurować wcześniejsze przed utworzeniem środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="ea0eb-125">Konfiguracja DNS sieci wirtualnej zostanie zmieniona, podczas tworzenia środowiska usługi aplikacji, która spowoduje niepowodzenie procesu tworzenia środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="ea0eb-126">W podobny szyjnej Jeśli istnieje niestandardowy serwer DNS na drugim końcu bramy sieci VPN, a serwer DNS jest nieosiągalny lub jest niedostępny, proces tworzenia środowiska usługi aplikacji również powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="ea0eb-127">Łączenie z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="ea0eb-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="ea0eb-128">Typowe konfiguracje programu SQL Server ma punktu końcowego nasłuchiwania na porcie 1433:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Punkt końcowy serwera SQL][SqlServerEndpoint]

<span data-ttu-id="ea0eb-130">Istnieją dwa podejścia do ograniczania ruchu do tego punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="ea0eb-131">[Listy kontroli dostępu do sieci] [ NetworkAccessControlLists] (listy ACL sieci)</span><span class="sxs-lookup"><span data-stu-id="ea0eb-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="ea0eb-132">[Grupy zabezpieczeń sieci][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="ea0eb-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="ea0eb-133">Ograniczanie dostępu do sieci listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="ea0eb-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="ea0eb-134">Port 1433 mogą być chronione przy użyciu listy kontroli dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="ea0eb-135">Przykład poniżej klienta whitelists adresów, pochodzących z wewnątrz sieci wirtualnej i blokuje dostęp do wszystkich innych klientów.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Przykład listy kontroli dostępu do sieci][NetworkAccessControlListExample]

<span data-ttu-id="ea0eb-137">Wszystkie aplikacje uruchomione w środowisku usługi aplikacji w tej samej sieci wirtualnej, ponieważ program SQL Server będzie mogła nawiązać połączenia przy użyciu wystąpienia programu SQL Server **wewnętrznej sieci wirtualnej** adres IP dla maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="ea0eb-138">Przykład parametry połączenia poniżej odwołuje się do serwera SQL przy użyciu prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="ea0eb-139">Mimo że maszyna wirtualna ma publiczny punkt końcowy również, próby nawiązania połączenia z użyciem publiczny adres IP zostanie odrzucone z powodu listy ACL sieci.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="ea0eb-140">Ograniczanie dostępu z sieciową grupą zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ea0eb-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="ea0eb-141">Informacje o innym podejściu do zabezpieczania dostępu jest z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="ea0eb-142">Grupy zabezpieczeń sieci może odnosić się do poszczególnych maszyn wirtualnych lub w podsieci zawierającej maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="ea0eb-143">Najpierw musi zostać utworzona grupa zabezpieczeń sieci:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="ea0eb-144">Ograniczanie dostępu do tylko ruchu w wewnętrznej sieci wirtualnej jest bardzo prosty z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="ea0eb-145">Reguły domyślne w grupie zabezpieczeń sieci tylko zezwalają na dostęp z innych klientów sieci w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="ea0eb-146">W związku z tym zablokowanie dostępu do programu SQL Server jest tak proste, jak stosowanie sieciową grupę zabezpieczeń z jej domyślnych reguł albo programem SQL Server lub podsieci zawierających maszyny wirtualne z maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="ea0eb-147">Poniższy przykład dotyczy sieciowej grupy zabezpieczeń zawierające podsieci:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="ea0eb-148">W rezultacie jest zestaw reguł zabezpieczeń, które blokują dostęp zewnętrznych, umożliwiając dostęp do sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Reguły zabezpieczeń sieciowych domyślne][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="ea0eb-150">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ea0eb-150">Getting started</span></span>
<span data-ttu-id="ea0eb-151">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="ea0eb-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="ea0eb-152">Wprowadzenie do środowiska usługi App Service, zobacz [wprowadzenie do środowiska usługi aplikacji][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="ea0eb-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="ea0eb-153">Aby uzyskać szczegółowe informacje związane sterowanie ruch przychodzący do środowiska usługi aplikacji, zobacz [kontrolowanie ruch przychodzący do środowiska usługi aplikacji][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="ea0eb-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="ea0eb-154">Aby uzyskać więcej informacji o platformie usługi Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="ea0eb-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
