---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Ta procedura jest pomocna podczas tworzenia połączenia usługi VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="c84b9-104">Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN typu lokacja-lokacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c84b9-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="c84b9-105">W tym artykule opisano, jak toouse połączenie bramy sieci VPN toocreate lokacja do lokacji programu PowerShell z lokalnej sieci toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="c84b9-106">Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c84b9-107">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="c84b9-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c84b9-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c84b9-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c84b9-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c84b9-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c84b9-110">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c84b9-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c84b9-111">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="c84b9-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="c84b9-112">Portal klasyczny (model klasyczny)</span><span class="sxs-lookup"><span data-stu-id="c84b9-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="c84b9-113">Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2).</span><span class="sxs-lookup"><span data-stu-id="c84b9-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c84b9-114">Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP.</span><span class="sxs-lookup"><span data-stu-id="c84b9-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="c84b9-115">Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c84b9-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="c84b9-117"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c84b9-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c84b9-118">Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="c84b9-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="c84b9-119">Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go.</span><span class="sxs-lookup"><span data-stu-id="c84b9-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c84b9-120">Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c84b9-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c84b9-121">Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c84b9-122">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c84b9-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c84b9-123">Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy.</span><span class="sxs-lookup"><span data-stu-id="c84b9-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c84b9-124">Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="c84b9-125">Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="c84b9-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="c84b9-126">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c84b9-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c84b9-127">Polecenia cmdlet programu PowerShell są często aktualizowane i zazwyczaj konieczne będzie tooupdate Twojego środowiska PowerShell poleceń cmdlet tooget hello najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="c84b9-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="c84b9-128">Jeśli nie zaktualizujesz poleceń cmdlet programu PowerShell hello wartości określonych może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c84b9-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="c84b9-129">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać więcej informacji o pobieraniu i instalowaniu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c84b9-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="c84b9-130"><a name="example"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="c84b9-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c84b9-131">Przykłady Hello w tym artykule Użyj hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c84b9-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="c84b9-132">Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c84b9-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="c84b9-133"><a name="Login"></a>1. Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c84b9-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="c84b9-134"><a name="VNet"></a>2. Tworzenie sieci wirtualnej i podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="c84b9-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c84b9-135">Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją.</span><span class="sxs-lookup"><span data-stu-id="c84b9-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="c84b9-136">Podczas tworzenia sieci wirtualnej, upewnij się, że przestrzenie adresowe hello, które określisz nie nakłada przestrzeni adresowych hello wyposażonych w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="c84b9-137"><a name="vnet"></a>toocreate sieć wirtualną i podsieć bramy</span><span class="sxs-lookup"><span data-stu-id="c84b9-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c84b9-138">Ten przykład tworzy sieć wirtualną i podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="c84b9-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="c84b9-139">Jeśli masz już sieć wirtualną, wymagającym tooadd podsieć bramy, aby wyświetlić [tooadd bramy podsieci tooa sieć wirtualną utworzono już](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="c84b9-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="c84b9-140">Utwórz grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="c84b9-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="c84b9-141">Utwórz swoją sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c84b9-141">Create your virtual network.</span></span>

1. <span data-ttu-id="c84b9-142">Ustaw zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="c84b9-143">Utwórz hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="c84b9-144"><a name="gatewaysubnet"></a>tooadd bramy sieci wirtualnej tooa podsieci utworzono już</span><span class="sxs-lookup"><span data-stu-id="c84b9-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="c84b9-145">Ustaw zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="c84b9-146">Utwórz podsieć bramy hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="c84b9-147">Ustaw konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="c84b9-148">3. <a name="localnet"></a>Utwórz bramę sieci lokalnej hello</span><span class="sxs-lookup"><span data-stu-id="c84b9-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="c84b9-149">Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="c84b9-150">Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie.</span><span class="sxs-lookup"><span data-stu-id="c84b9-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="c84b9-151">Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy.</span><span class="sxs-lookup"><span data-stu-id="c84b9-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="c84b9-152">Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="c84b9-153">W przypadku zmiany sieci lokalnej, można łatwo aktualizować hello prefiksy.</span><span class="sxs-lookup"><span data-stu-id="c84b9-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="c84b9-154">Użyj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c84b9-154">Use hello following values:</span></span>

* <span data-ttu-id="c84b9-155">Witaj *GatewayIPAddress* jest adresem IP hello lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c84b9-156">Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c84b9-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c84b9-157">Witaj *prefiks adresu* jest lokalnej przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="c84b9-158">tooadd bramy sieci lokalnej z prefiksem pojedynczy adres:</span><span class="sxs-lookup"><span data-stu-id="c84b9-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="c84b9-159">tooadd bramy sieci lokalnej przy użyciu wielu prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="c84b9-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="c84b9-160">toomodify prefiksów adresów IP dla bramy sieci lokalnej:</span><span class="sxs-lookup"><span data-stu-id="c84b9-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="c84b9-161">Zdarza się, że prefiksy bramy sieci lokalnej są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="c84b9-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="c84b9-162">kroki Hello podejmiesz toomodify Twojego adresu IP, który prefiksy zależą od tego, czy utworzono połączenia bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="c84b9-163">Zobacz hello [prefiksów adresów IP zmodyfikować dla bramy sieci lokalnej](#modify) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c84b9-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="c84b9-164"><a name="PublicIP"></a>4. Żądanie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="c84b9-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="c84b9-165">Brama sieci VPN musi mieć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="c84b9-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c84b9-166">Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="c84b9-167">adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="c84b9-168">Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c84b9-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c84b9-169">Nie można zażądać przypisania statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c84b9-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c84b9-170">Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="c84b9-171">Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie.</span><span class="sxs-lookup"><span data-stu-id="c84b9-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="c84b9-172">Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c84b9-173">Żądanie do publicznego adresu IP przypisanego tooyour sieci wirtualnej bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="c84b9-174"><a name="GatewayIPConfig"></a>5. Tworzenie konfiguracji adresów IP bramy hello</span><span class="sxs-lookup"><span data-stu-id="c84b9-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="c84b9-175">Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c84b9-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="c84b9-176">Użyj następującego przykładu toocreate hello konfigurację bramy:</span><span class="sxs-lookup"><span data-stu-id="c84b9-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="c84b9-177"><a name="CreateGateway"></a>6. Tworzenie bramy sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="c84b9-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="c84b9-178">Tworzenie bramy sieci VPN hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="c84b9-179">Tworzenie bramy sieci VPN może potrwać too45 minut lub więcej toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c84b9-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="c84b9-180">Użyj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c84b9-180">Use hello following values:</span></span>

* <span data-ttu-id="c84b9-181">Witaj *elementu GatewayType -* Site-to-Site konfiguracja jest *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c84b9-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c84b9-182">Typ bramy Hello jest zawsze toohello określonej konfiguracji w przypadku wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c84b9-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="c84b9-183">Na przykład inne konfiguracje bramy mogą wymagać zastosowania wartości -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c84b9-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="c84b9-184">Witaj *- VpnType* może być *RouteBased* (określony tooas dynamiczne bramy w części dokumentacji), lub *PolicyBased* (określony tooas statycznych bramy w części dokumentacji ).</span><span class="sxs-lookup"><span data-stu-id="c84b9-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="c84b9-185">Więcej informacji o typach bram sieci VPN można znaleźć w artykule [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c84b9-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="c84b9-186">Wybierz hello jednostka SKU bramy, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="c84b9-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="c84b9-187">Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c84b9-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c84b9-188">Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).</span><span class="sxs-lookup"><span data-stu-id="c84b9-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="c84b9-189">Jeśli wystąpi błąd podczas tworzenia bramy sieci VPN hello dotyczące hello - GatewaySku, sprawdź, że zainstalowano najnowszą wersję hello hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c84b9-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="c84b9-190"><a name="ConfigureVPNDevice"></a>7. Konfiguracja urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c84b9-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="c84b9-191">Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="c84b9-192">W tym kroku konfigurowane jest urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c84b9-193">Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c84b9-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="c84b9-194">Klucz współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="c84b9-194">A shared key.</span></span> <span data-ttu-id="c84b9-195">Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="c84b9-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c84b9-196">W naszych przykładach używamy podstawowego klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c84b9-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c84b9-197">Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.</span><span class="sxs-lookup"><span data-stu-id="c84b9-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="c84b9-198">Witaj publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c84b9-199">Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c84b9-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c84b9-200">Witaj toofind publiczny adres IP bramy sieci wirtualnej przy użyciu programu PowerShell, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c84b9-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c84b9-201"><a name="CreateConnection"></a>8. Utwórz połączenie sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="c84b9-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="c84b9-202">Następnie należy utworzyć połączenie VPN lokacja-lokacja hello między bramą sieci wirtualnej i urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="c84b9-203">Należy się, że wartości hello tooreplace własnymi.</span><span class="sxs-lookup"><span data-stu-id="c84b9-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="c84b9-204">klucz współużytkowany Hello musi odpowiadać wartości hello, używanego do konfiguracji urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="c84b9-205">Zwróć uwagę, że hello "-ConnectionType" lokacja-lokacja jest *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="c84b9-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="c84b9-206">Ustaw zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="c84b9-207">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="c84b9-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="c84b9-208">Automatycznie podczas hello zostanie nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="c84b9-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="c84b9-209"><a name="toverify"></a>9. Sprawdź hello połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c84b9-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="c84b9-210">Istnieje kilka różnych sposobów tooverify połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c84b9-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="c84b9-211"><a name="connectVM"></a>Maszyna wirtualna tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="c84b9-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="c84b9-212"><a name="modify"></a>Modyfikowanie prefiksów adresów IP bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="c84b9-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="c84b9-213">Zmiana hello prefiksów adresów IP, które mają być kierowane tooyour lokalnej lokalizacji można zmodyfikować hello bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c84b9-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="c84b9-214">Poniżej przedstawiono dwa zestawy instrukcji.</span><span class="sxs-lookup"><span data-stu-id="c84b9-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="c84b9-215">instrukcje Hello, musisz wybrać zależą od tego, czy zostały już utworzone połączenie bramy.</span><span class="sxs-lookup"><span data-stu-id="c84b9-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="c84b9-216"><a name="modifygwipaddress"></a>Modyfikowanie hello adres IP bramy dla bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="c84b9-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c84b9-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c84b9-217">Next steps</span></span>

*  <span data-ttu-id="c84b9-218">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c84b9-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c84b9-219">Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="c84b9-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c84b9-220">Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c84b9-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
