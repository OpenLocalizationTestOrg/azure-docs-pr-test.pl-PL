---
title: "Skonfigurować wymuszanie tunelowania dla połączenia usługi Azure Site to Site: klasycznym | Dokumentacja firmy Microsoft"
description: "Jak tooredirect lub \"force\" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalizacji lokalnej."
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
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="94df8-103">Konfigurowanie przy użyciu tunelowania wymuszonego hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="94df8-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="94df8-104">Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="94df8-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="94df8-105">Jest to wymagane krytycznych dla większości organizacji IT zasad.</span><span class="sxs-lookup"><span data-stu-id="94df8-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="94df8-106">Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure będzie zawsze przechodzenie od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji.</span><span class="sxs-lookup"><span data-stu-id="94df8-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="94df8-107">Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="94df8-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="94df8-108">W tym artykule przedstawiono konfigurowanie wymuszonego tunelowania dla sieci wirtualnych utworzonych przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="94df8-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="94df8-109">Tunelowanie wymuszone można skonfigurować przy użyciu programu PowerShell, nie za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="94df8-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="94df8-110">Tooconfigure wymuszonego tunelowania dla modelu wdrażania usługi Resource Manager hello, zaznacz klasycznego artykułu z następującej listy rozwijanej hello:</span><span class="sxs-lookup"><span data-stu-id="94df8-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="94df8-111">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="94df8-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="94df8-112">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="94df8-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="94df8-113">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="94df8-113">Requirements and considerations</span></span>
<span data-ttu-id="94df8-114">Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika (przez).</span><span class="sxs-lookup"><span data-stu-id="94df8-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="94df8-115">Przekierowywanie ruchu tooan w lokalnym witryny jest wyrażona jako brama sieci VPN platformy Azure toohello trasy domyślnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="94df8-116">Witaj poniższej sekcji przedstawiono hello obecne ograniczenie hello tabeli routingu i tras dla sieci wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="94df8-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="94df8-117">Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu.</span><span class="sxs-lookup"><span data-stu-id="94df8-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="94df8-118">Tabela routingu Hello system ma hello następujące trzy grupy tras:</span><span class="sxs-lookup"><span data-stu-id="94df8-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="94df8-119">**Tras lokalnych sieci wirtualnej:** bezpośrednio toohello docelowego maszyny wirtualne w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="94df8-120">**Trasy lokalnymi:** toohello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94df8-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="94df8-121">**Trasa domyślna:** bezpośrednio toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="94df8-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="94df8-122">Pakiety przeznaczone toohello prywatnych adresów IP nie pasuje do żadnego hello dwoma poprzednimi trasy zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="94df8-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="94df8-123">Hello wersji z tras zdefiniowanych przez użytkownika można utworzyć routingu tooadd tabeli trasy domyślnej i następnie skojarzyć hello routingu tabeli tooyour sieci wirtualnej adresy podsieci używane tooenable wymuszone tunelowanie korzysta z tych podsieci.</span><span class="sxs-lookup"><span data-stu-id="94df8-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="94df8-124">Należy tooset "domyślnej witryny" między sieci wirtualnej podłączonej toohello hello między lokalizacjami lokalnych witryn.</span><span class="sxs-lookup"><span data-stu-id="94df8-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="94df8-125">Wymuszanie tunelowania musi być skojarzony z sieć wirtualną, która ma dynamiczne routingu bramy sieci VPN (nie bramy statyczne).</span><span class="sxs-lookup"><span data-stu-id="94df8-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="94df8-126">ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="94df8-127">Zobacz hello [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="94df8-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="94df8-128">Przegląd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="94df8-128">Configuration overview</span></span>
<span data-ttu-id="94df8-129">W hello poniższy przykład tunelowane hello nie wymusza podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="94df8-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="94df8-130">Witaj obciążeń w podsieci frontonu hello można kontynuować tooaccept i odpowiada na żądania toocustomer z hello Internet bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="94df8-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="94df8-131">Witaj podsieci w warstwie pośredniej i wewnętrznej bazy danych zostało wymuszone tunelowane.</span><span class="sxs-lookup"><span data-stu-id="94df8-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="94df8-132">Wszystkie połączenia wychodzące z tymi dwiema podsieciami toohello Internet będzie tooan wymuszonym lub ponownie przekierowanego lokacji lokalnej za pośrednictwem jednego powitalne tuneli S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="94df8-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="94df8-133">Pozwala toorestrict i inspekcję dostępu do Internetu na maszynach wirtualnych lub w chmurze usługi na platformie Azure, pozostawiając tooenable architektury usługa wielowarstwowa wymagane.</span><span class="sxs-lookup"><span data-stu-id="94df8-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="94df8-134">Możesz również zastosować wymuszonego tunelowania toohello całe sieci wirtualne Jeśli w sieci wirtualne nie żadne obciążenia skierowane do Internetu.</span><span class="sxs-lookup"><span data-stu-id="94df8-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Wymuszone tunelowanie](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="94df8-136">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="94df8-136">Before you begin</span></span>
<span data-ttu-id="94df8-137">Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="94df8-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="94df8-138">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94df8-138">An Azure subscription.</span></span> <span data-ttu-id="94df8-139">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94df8-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="94df8-140">Skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-140">A configured virtual network.</span></span> 
* <span data-ttu-id="94df8-141">Witaj najnowszą wersję hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94df8-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="94df8-142">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94df8-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="94df8-143">Konfigurowanie wymuszonego tunelowania</span><span class="sxs-lookup"><span data-stu-id="94df8-143">Configure forced tunneling</span></span>
<span data-ttu-id="94df8-144">Hello procedury pomoże określić wymuszanie tunelowania do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="94df8-145">kroki konfiguracji Hello odpowiada pliku konfiguracji sieci toohello w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

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

<span data-ttu-id="94df8-146">W tym przykładzie hello sieci wirtualnej "Sieci wirtualnej MultiTier" zawiera trzy podsieci: podsieci "Frontend", "Midtier" i "Zaplecze", w przypadku połączeń między różnymi lokalizacjami cztery: "DefaultSiteHQ" i trzy gałęzie.</span><span class="sxs-lookup"><span data-stu-id="94df8-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="94df8-147">kroki Hello będzie hello "DefaultSiteHQ" jako hello domyślne lokacji połączenie tunelowania wymuszonego i konfigurowanie hello Midtier i wewnętrznej bazy danych podsieci toouse wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="94df8-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="94df8-148">Tworzy tabelę routingu.</span><span class="sxs-lookup"><span data-stu-id="94df8-148">Create a routing table.</span></span> <span data-ttu-id="94df8-149">Użyj następującego polecenia cmdlet toocreate hello tabeli routingu.</span><span class="sxs-lookup"><span data-stu-id="94df8-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="94df8-150">Dodaj tabelę routingu toohello trasy domyślnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="94df8-151">Witaj poniższy przykład umożliwia dodanie domyślną trasę toohello tabelę routingu utworzone w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="94df8-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="94df8-152">Należy pamiętać, że hello tylko trasy obsługiwane jest prefiks docelowy hello toohello "0.0.0.0/0" następnego skoku "Właściwość VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="94df8-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="94df8-153">Kojarzenie hello routingu tabeli toohello podsieci.</span><span class="sxs-lookup"><span data-stu-id="94df8-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="94df8-154">Po utworzeniu tabeli routingu i dodać trasy, użyj następującego przykładu tooadd hello lub skojarzyć podsieci tooa tabeli hello trasy w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="94df8-155">przykład Witaj dodaje hello trasy tabeli "MyRouteTable" toohello Midtier i podsieci wewnętrznej bazy danych z MultiTier wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="94df8-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="94df8-156">Przypisz domyślnej witryny dla wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="94df8-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="94df8-157">W hello poprzedzających krok hello przykładowe polecenia cmdlet skrypty utworzone hello tabeli routingu i skojarzone tootwo tabeli tras hello hello podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94df8-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="94df8-158">pozostały krok Hello jest tooselect lokalnej lokacji między hello połączeń obejmujący wiele lokacji sieci wirtualnej hello jako hello domyślnej witryny lub tunelu.</span><span class="sxs-lookup"><span data-stu-id="94df8-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="94df8-159">Dodatkowe polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="94df8-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="94df8-160">toodelete tabelę tras</span><span class="sxs-lookup"><span data-stu-id="94df8-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="94df8-161">toolist tabelę tras</span><span class="sxs-lookup"><span data-stu-id="94df8-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="94df8-162">toodelete tras z tabeli tras</span><span class="sxs-lookup"><span data-stu-id="94df8-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="94df8-163">tooremove tras z podsiecią</span><span class="sxs-lookup"><span data-stu-id="94df8-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="94df8-164">Tabela tras hello toolist skojarzony z podsiecią</span><span class="sxs-lookup"><span data-stu-id="94df8-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="94df8-165">tooremove domyślnej witryny z bramy sieci VPN w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="94df8-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```