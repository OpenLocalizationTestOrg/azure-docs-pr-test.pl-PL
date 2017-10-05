---
title: "Skonfigurować wymuszanie tunelowania dla połączenia usługi Azure Site to Site: klasycznym | Dokumentacja firmy Microsoft"
description: "Jak przekierować lub \"force\" cały ruch do Internetu powiązane z powrotem do lokalizacji lokalnej."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 79bf6892c823da282c3e763921e830f986419854
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-classic-deployment-model"></a><span data-ttu-id="4018a-103">Konfigurowanie wymuszonego tunelowania przy użyciu klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="4018a-103">Configure forced tunneling using the classic deployment model</span></span>

<span data-ttu-id="4018a-104">Wymuszanie tunelowania umożliwia przekierowanie lub "force" cały ruch do Internetu z powrotem do lokalizacji lokalnej za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="4018a-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="4018a-105">Jest to wymagane krytycznych dla większości organizacji IT zasad.</span><span class="sxs-lookup"><span data-stu-id="4018a-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="4018a-106">Bez tunelowania wymuszonego, ruch do Internetu z maszyn wirtualnych na platformie Azure będzie zawsze przechodzenie od infrastruktury sieci platformy Azure bezpośrednio się z Internetem, bez opcji pozwala sprawdzać lub kontrolować ruch.</span><span class="sxs-lookup"><span data-stu-id="4018a-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="4018a-107">Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie informacji lub inne rodzaje naruszeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4018a-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="4018a-108">W tym artykule przedstawiono konfigurowanie wymuszonego tunelowania dla sieci wirtualnych utworzonych przy użyciu klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4018a-108">This article walks you through configuring forced tunneling for virtual networks created using the classic deployment model.</span></span> <span data-ttu-id="4018a-109">Tunelowanie wymuszone można skonfigurować przy użyciu programu PowerShell, nie za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="4018a-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="4018a-110">Jeśli chcesz skonfigurować wymuszanie tunelowania dla modelu wdrażania usługi Resource Manager, wybierz klasycznego artykułu z poniższej listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="4018a-110">If you want to configure forced tunneling for the Resource Manager deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4018a-111">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="4018a-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="4018a-112">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4018a-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="4018a-113">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="4018a-113">Requirements and considerations</span></span>
<span data-ttu-id="4018a-114">Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika (przez).</span><span class="sxs-lookup"><span data-stu-id="4018a-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="4018a-115">Ruch jest przekierowywany do lokacji lokalnej jest wyrażona jako domyślną trasę do bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4018a-115">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="4018a-116">W poniższej sekcji przedstawiono bieżące ograniczenia tabeli routingu i tras dla sieci wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4018a-116">The following section lists the current limitation of the routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="4018a-117">Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu.</span><span class="sxs-lookup"><span data-stu-id="4018a-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="4018a-118">W tabeli routingu system ma następujące trzy grupy tras:</span><span class="sxs-lookup"><span data-stu-id="4018a-118">The system routing table has the following three groups of routes:</span></span>

  * <span data-ttu-id="4018a-119">**Tras lokalnych sieci wirtualnej:** bezpośrednio do miejsca docelowego maszyny wirtualne w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-119">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="4018a-120">**Trasy lokalnymi:** bramy do sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4018a-120">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="4018a-121">**Trasa domyślna:** bezpośrednio do Internetu.</span><span class="sxs-lookup"><span data-stu-id="4018a-121">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="4018a-122">Pakiety przeznaczone do prywatnych adresów IP nie jest objęty przez poprzednie dwie trasy zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="4018a-122">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span></span>
* <span data-ttu-id="4018a-123">Wraz z wydaniem trasy zdefiniowane przez użytkownika można utworzyć tabeli routingu, aby dodać trasy domyślnej i późniejszym skojarzeniu tabeli routingu do adresy podsieci Twojej sieci wirtualnej mogą być używane w taki sposób, aby włączyć tunelowanie wymuszone korzysta z tych podsieci.</span><span class="sxs-lookup"><span data-stu-id="4018a-123">With the release of user-defined routes, you can create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="4018a-124">Należy określić "domyślnej witryny" między lokacjami lokalnego między lokalizacjami podłączony do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-124">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span>
* <span data-ttu-id="4018a-125">Wymuszanie tunelowania musi być skojarzony z sieć wirtualną, która ma dynamiczne routingu bramy sieci VPN (nie bramy statyczne).</span><span class="sxs-lookup"><span data-stu-id="4018a-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="4018a-126">ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem sesje komunikacji równorzędnej BGP usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4018a-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="4018a-127">Zobacz [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4018a-127">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="4018a-128">Przegląd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4018a-128">Configuration overview</span></span>
<span data-ttu-id="4018a-129">W poniższym przykładzie tunelowane frontonu nie wymusza podsieci.</span><span class="sxs-lookup"><span data-stu-id="4018a-129">In the following example, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="4018a-130">Obciążeń w podsieci frontonu mogą nadal akceptować i odpowiadać na żądania klientów i z Internetu.</span><span class="sxs-lookup"><span data-stu-id="4018a-130">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="4018a-131">Podsieci warstwie pośredniej i wewnętrznej bazy danych zostało wymuszone tunelowane.</span><span class="sxs-lookup"><span data-stu-id="4018a-131">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="4018a-132">Wszystkie połączenia wychodzące z tymi dwoma podsieciami z Internetem zostanie wymuszone lub przekierowany z powrotem do lokacji lokalnej za pośrednictwem jeden tunel S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="4018a-132">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="4018a-133">Dzięki temu można ograniczyć i inspekcję dostępu do Internetu na maszynach wirtualnych lub w chmurze usługi na platformie Azure, pozostawiając włączyć architektury usługa wielowarstwowa wymagane.</span><span class="sxs-lookup"><span data-stu-id="4018a-133">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="4018a-134">Możesz również zastosować wymuszanie tunelowania do całej sieci wirtualnych, jeśli w sieci wirtualne nie żadne obciążenia skierowane do Internetu.</span><span class="sxs-lookup"><span data-stu-id="4018a-134">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Wymuszone tunelowanie](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="4018a-136">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4018a-136">Before you begin</span></span>
<span data-ttu-id="4018a-137">Przed rozpoczęciem konfiguracji sprawdź, czy dysponujesz następującymi elementami.</span><span class="sxs-lookup"><span data-stu-id="4018a-137">Verify that you have the following items before beginning configuration.</span></span>

* <span data-ttu-id="4018a-138">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4018a-138">An Azure subscription.</span></span> <span data-ttu-id="4018a-139">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4018a-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4018a-140">Skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-140">A configured virtual network.</span></span> 
* <span data-ttu-id="4018a-141">Najnowsza wersja poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4018a-141">The latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4018a-142">Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet programu Azure PowerShell, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4018a-142">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="4018a-143">Konfigurowanie wymuszonego tunelowania</span><span class="sxs-lookup"><span data-stu-id="4018a-143">Configure forced tunneling</span></span>
<span data-ttu-id="4018a-144">Poniższa procedura umożliwia określenie, wymuszanie tunelowania do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-144">The following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="4018a-145">Odpowiada kroków konfiguracji do pliku konfiguracji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-145">The configuration steps correspond to the VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="4018a-146">W tym przykładzie sieci wirtualnej "Sieci wirtualnej MultiTier" zawiera trzy podsieci: podsieci "Frontend", "Midtier" i "Zaplecze", w przypadku połączeń między różnymi lokalizacjami cztery: "DefaultSiteHQ" i trzy gałęzie.</span><span class="sxs-lookup"><span data-stu-id="4018a-146">In this example, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="4018a-147">Kroki będą DefaultSiteHQ jako domyślnego połączenia lokacji dla wymuszone tunelowanie i skonfigurować Midtier i wymusić podsieci wewnętrznej bazy danych do użycia tunelowania.</span><span class="sxs-lookup"><span data-stu-id="4018a-147">The steps will set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span></span>

1. <span data-ttu-id="4018a-148">Tworzy tabelę routingu.</span><span class="sxs-lookup"><span data-stu-id="4018a-148">Create a routing table.</span></span> <span data-ttu-id="4018a-149">Użyj następującego polecenia cmdlet do utworzenia tabeli tras.</span><span class="sxs-lookup"><span data-stu-id="4018a-149">Use the following cmdlet to create your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="4018a-150">Dodaj domyślną trasę do tabeli routingu.</span><span class="sxs-lookup"><span data-stu-id="4018a-150">Add a default route to the routing table.</span></span> 

  <span data-ttu-id="4018a-151">Poniższy przykład dodaje domyślną trasę do tabeli routingu utworzone w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="4018a-151">The following example adds a default route to the routing table created in Step 1.</span></span> <span data-ttu-id="4018a-152">Należy pamiętać, że obsługiwane tylko trasy jest prefiks docelowy "0.0.0.0/0" do następnego skoku "Właściwość VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="4018a-152">Note that the only route supported is the destination prefix of "0.0.0.0/0" to the "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="4018a-153">Kojarzenie tabeli routingu do podsieci.</span><span class="sxs-lookup"><span data-stu-id="4018a-153">Associate the routing table to the subnets.</span></span> 

  <span data-ttu-id="4018a-154">Po utworzeniu tabeli routingu i dodać trasy, skorzystaj z następującego przykładu, aby dodać lub skojarzyć tabeli tras z podsiecią sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-154">After a routing table is created and a route added, use the following example to add or associate the route table to a VNet subnet.</span></span> <span data-ttu-id="4018a-155">W przykładzie dodano tabeli tras "MyRouteTable" z podsieciami z MultiTier wirtualnymi Midtier i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4018a-155">The example adds the route table "MyRouteTable" to the Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="4018a-156">Przypisz domyślnej witryny dla wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="4018a-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="4018a-157">W poprzednim kroku przykładowe skrypty polecenia cmdlet utworzono tabelę routingu i skojarzona tabela tras do dwóch podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4018a-157">In the preceding step, the sample cmdlet scripts created the routing table and associated the route table to two of the VNet subnets.</span></span> <span data-ttu-id="4018a-158">Pozostały krok polega na wybraniu lokalnej lokacji między połączeń obejmujący wiele lokacji sieci wirtualnej jako domyślnej witryny lub tunelu.</span><span class="sxs-lookup"><span data-stu-id="4018a-158">The remaining step is to select a local site among the multi-site connections of the virtual network as the default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="4018a-159">Dodatkowe polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4018a-159">Additional PowerShell cmdlets</span></span>
### <a name="to-delete-a-route-table"></a><span data-ttu-id="4018a-160">Można usunąć tabeli tras</span><span class="sxs-lookup"><span data-stu-id="4018a-160">To delete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="to-list-a-route-table"></a><span data-ttu-id="4018a-161">Aby wyświetlić tabelę tras</span><span class="sxs-lookup"><span data-stu-id="4018a-161">To list a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="to-delete-a-route-from-a-route-table"></a><span data-ttu-id="4018a-162">Aby usunąć trasy z tabeli tras</span><span class="sxs-lookup"><span data-stu-id="4018a-162">To delete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="to-remove-a-route-from-a-subnet"></a><span data-ttu-id="4018a-163">Aby usunąć trasy z podsiecią</span><span class="sxs-lookup"><span data-stu-id="4018a-163">To remove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-list-the-route-table-associated-with-a-subnet"></a><span data-ttu-id="4018a-164">Aby wyświetlić listę tabeli tras skojarzony z podsiecią</span><span class="sxs-lookup"><span data-stu-id="4018a-164">To list the route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-remove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="4018a-165">Aby usunąć domyślną witrynę z bramy sieci VPN w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4018a-165">To remove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```