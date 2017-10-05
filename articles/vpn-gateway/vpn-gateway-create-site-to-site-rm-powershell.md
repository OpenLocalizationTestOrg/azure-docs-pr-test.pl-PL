---
title: "Łączenie sieci lokalnej sieci z siecią wirtualną platformy Azure: sieci VPN typu lokacja-lokacja: PowerShell | Microsoft Docs"
description: "Kroki tworzenia połączenia IPsec z sieci lokalnej do sieci wirtualnej platformy Azure za pośrednictwem publicznego Internetu. Ta procedura jest pomocna podczas tworzenia połączenia usługi VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą programu PowerShell."
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
ms.openlocfilehash: 27f4a8fb9a83b98e99df635bf4c80f6048ce348c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="5f40c-104">Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN typu lokacja-lokacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f40c-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="5f40c-105">Ten artykuł pokazuje, jak używać programu PowerShell do tworzenia połączenia bramy sieci VPN lokacja-lokacja z Twojej sieci lokalnej do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-105">This article shows you how to use PowerShell to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="5f40c-106">Kroki podane w tym artykule mają zastosowanie do modelu wdrażania przy użyciu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f40c-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="5f40c-107">Tę konfigurację możesz również utworzyć przy użyciu innego narzędzia wdrażania lub modelu wdrażania, wybierając inną opcję z następującej listy:</span><span class="sxs-lookup"><span data-stu-id="5f40c-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f40c-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f40c-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="5f40c-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f40c-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="5f40c-110">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5f40c-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="5f40c-111">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="5f40c-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="5f40c-112">Portal klasyczny (model klasyczny)</span><span class="sxs-lookup"><span data-stu-id="5f40c-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="5f40c-113">Połączenie bramy sieci VPN typu lokacja-lokacja umożliwia łączenie sieci lokalnej z siecią wirtualną platformy Azure za pośrednictwem tunelu sieci VPN IPsec/IKE (IKEv1 lub IKEv2).</span><span class="sxs-lookup"><span data-stu-id="5f40c-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="5f40c-114">Ten typ połączenia wymaga lokalnego urządzenia sieci VPN z przypisanym publicznym adresem IP dostępnym z zewnątrz.</span><span class="sxs-lookup"><span data-stu-id="5f40c-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="5f40c-115">Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="5f40c-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="5f40c-117"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5f40c-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="5f40c-118">Przed rozpoczęciem konfiguracji sprawdź, czy są spełnione następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="5f40c-118">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="5f40c-119">Upewnij się, że masz zgodne urządzenie sieci VPN i dostępna jest osoba, która umie je skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="5f40c-119">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="5f40c-120">Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="5f40c-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="5f40c-121">Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="5f40c-122">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="5f40c-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="5f40c-123">Jeśli nie znasz zakresów adresów IP w konfiguracji swojej sieci lokalnej, skontaktuj się z osobą, która może podać Ci te dane.</span><span class="sxs-lookup"><span data-stu-id="5f40c-123">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="5f40c-124">Tworząc tę konfigurację, musisz określić prefiksy zakresu adresów IP, które platforma Azure będzie kierować do Twojej lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-124">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="5f40c-125">Żadna z podsieci sieci lokalnej nie może się nakładać na podsieci sieci wirtualnej, z którymi chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="5f40c-125">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="5f40c-126">Zainstaluj najnowszą wersję poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f40c-126">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5f40c-127">Polecenia cmdlet programu PowerShell są często aktualizowane. Ich zaktualizowanie jest zazwyczaj konieczne w celu uzyskania najnowszych wersji funkcji.</span><span class="sxs-lookup"><span data-stu-id="5f40c-127">PowerShell cmdlets are updated frequently and you will typically need to update your PowerShell cmdlets to get the latest feature functionality.</span></span> <span data-ttu-id="5f40c-128">Jeśli nie zaktualizujesz poleceń cmdlet programu PowerShell, mogą wystąpić błędy określonych wartości.</span><span class="sxs-lookup"><span data-stu-id="5f40c-128">If you don't update your PowerShell cmdlets, the values specified may fail.</span></span> <span data-ttu-id="5f40c-129">Aby uzyskać więcej informacji na temat pobierania i instalowania poleceń cmdlet programu PowerShell, zobacz artykuł [How to install and configure Azure PowerShell (Jak zainstalować i skonfigurować program Azure PowerShell)](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f40c-129">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="5f40c-130"><a name="example"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="5f40c-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="5f40c-131">W przykładach w tym artykule są stosowane następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="5f40c-131">The examples in this article use the following values.</span></span> <span data-ttu-id="5f40c-132">Tych wartości możesz użyć do tworzenia środowiska testowego lub odwoływać się do nich, aby lepiej zrozumieć przykłady w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="5f40c-132">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

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


## <span data-ttu-id="5f40c-133"><a name="Login"></a>1. Nawiązywanie połączenia z subskrypcją</span><span class="sxs-lookup"><span data-stu-id="5f40c-133"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="5f40c-134"><a name="VNet"></a>2. Tworzenie sieci wirtualnej i podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="5f40c-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="5f40c-135">Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją.</span><span class="sxs-lookup"><span data-stu-id="5f40c-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="5f40c-136">Podczas tworzenia sieci wirtualnej upewnij się, że określone przestrzenie adresowe nie nakładają się na żadne inne przestrzenie adresowe w obrębie sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-136">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="5f40c-137"><a name="vnet"></a>Aby utworzyć sieć wirtualną i podsieć bramy</span><span class="sxs-lookup"><span data-stu-id="5f40c-137"><a name="vnet"></a>To create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="5f40c-138">Ten przykład tworzy sieć wirtualną i podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="5f40c-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="5f40c-139">Jeśli masz już sieć wirtualną, do której potrzebujesz dodać podsieć bramy, zobacz [Aby dodać podsieć bramy do utworzonej wcześniej sieci wirtualnej](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="5f40c-139">If you already have a virtual network that you need to add a gateway subnet to, see [To add a gateway subnet to a virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="5f40c-140">Utwórz grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="5f40c-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="5f40c-141">Utwórz swoją sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5f40c-141">Create your virtual network.</span></span>

1. <span data-ttu-id="5f40c-142">Ustaw zmienne.</span><span class="sxs-lookup"><span data-stu-id="5f40c-142">Set the variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="5f40c-143">Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5f40c-143">Create the VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="5f40c-144"><a name="gatewaysubnet"></a>Aby dodać podsieć bramy do utworzonej wcześniej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5f40c-144"><a name="gatewaysubnet"></a>To add a gateway subnet to a virtual network you have already created</span></span>

1. <span data-ttu-id="5f40c-145">Ustaw zmienne.</span><span class="sxs-lookup"><span data-stu-id="5f40c-145">Set the variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="5f40c-146">Utwórz podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="5f40c-146">Create the gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="5f40c-147">Ustaw konfigurację.</span><span class="sxs-lookup"><span data-stu-id="5f40c-147">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="5f40c-148">3. <a name="localnet"></a>Tworzenie bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5f40c-148">3. <a name="localnet"></a>Create the local network gateway</span></span>

<span data-ttu-id="5f40c-149">Brama sieci lokalnej zazwyczaj odwołuje się do lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-149">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="5f40c-150">Nadaj lokacji nazwę, za pomocą której platforma Azure może odwołać się do niej, a następnie określ adres IP lokalnego urządzenia sieci VPN, z którym będzie tworzone połączenie.</span><span class="sxs-lookup"><span data-stu-id="5f40c-150">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="5f40c-151">Określ również prefiksy adresów IP, które będą kierowane za pośrednictwem bramy sieci VPN do urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-151">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="5f40c-152">Określone prefiksy adresów są prefiksami znajdującymi się w Twojej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-152">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="5f40c-153">W przypadku zmian w sieci lokalnej prefiksy można łatwo zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="5f40c-153">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="5f40c-154">Wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="5f40c-154">Use the following values:</span></span>

* <span data-ttu-id="5f40c-155">*GatewayIPAddress* to adres IP lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-155">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="5f40c-156">Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="5f40c-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="5f40c-157">*AddressPrefix* oznacza lokalną przestrzeń adresową.</span><span class="sxs-lookup"><span data-stu-id="5f40c-157">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="5f40c-158">Aby dodać bramę sieci lokalnej z pojedynczym prefiksem adresu:</span><span class="sxs-lookup"><span data-stu-id="5f40c-158">To add a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="5f40c-159">Aby dodać bramę sieci lokalnej z wieloma prefiksami adresów:</span><span class="sxs-lookup"><span data-stu-id="5f40c-159">To add a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="5f40c-160">Aby zmodyfikować prefiksy adresów IP bramy sieci lokalnej:</span><span class="sxs-lookup"><span data-stu-id="5f40c-160">To modify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="5f40c-161">Zdarza się, że prefiksy bramy sieci lokalnej są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="5f40c-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="5f40c-162">Kroki, które należy wykonać w celu zmodyfikowania prefiksów adresów IP, zależą od tego, czy utworzono połączenie bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-162">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="5f40c-163">Zapoznaj się z sekcją [Modyfikowanie prefiksów adresów IP bramy sieci lokalnej](#modify) tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="5f40c-163">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="5f40c-164"><a name="PublicIP"></a>4. Żądanie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="5f40c-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="5f40c-165">Brama sieci VPN musi mieć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5f40c-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="5f40c-166">Najpierw żąda się zasobu adresu IP, a następnie odwołuje do niego podczas tworzenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-166">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="5f40c-167">Adres IP jest dynamicznie przypisywany do zasobu podczas tworzenia bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-167">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="5f40c-168">Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5f40c-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="5f40c-169">Nie można zażądać przypisania statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5f40c-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="5f40c-170">Nie oznacza to jednak, że adres IP zmienia się po przypisaniu go do bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-170">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="5f40c-171">Jedyną sytuacją, w której ma miejsce zmiana publicznego adresu IP, jest usunięcie bramy i jej ponowne utworzenie.</span><span class="sxs-lookup"><span data-stu-id="5f40c-171">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="5f40c-172">Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="5f40c-173">Prześlij żądanie przydzielenia publicznego adresu IP, który zostanie przypisany do Twojej bramy sieci VPN sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-173">Request a Public IP address that will be assigned to your virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="5f40c-174"><a name="GatewayIPConfig"></a>5. Tworzenie konfiguracji adresowania IP bramy</span><span class="sxs-lookup"><span data-stu-id="5f40c-174"><a name="GatewayIPConfig"></a>5. Create the gateway IP addressing configuration</span></span>

<span data-ttu-id="5f40c-175">W ramach konfiguracji bramy zostaje zdefiniowana podsieć i publiczny adres IP do użycia.</span><span class="sxs-lookup"><span data-stu-id="5f40c-175">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="5f40c-176">Poniższy przykład umożliwia utworzenie własnej konfiguracji bramy:</span><span class="sxs-lookup"><span data-stu-id="5f40c-176">Use the following example to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="5f40c-177"><a name="CreateGateway"></a>6. Tworzenie bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5f40c-177"><a name="CreateGateway"></a>6. Create the VPN gateway</span></span>

<span data-ttu-id="5f40c-178">Utwórz bramę sieci VPN sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-178">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="5f40c-179">Tworzenie bramy sieci VPN może potrwać 45 minut lub więcej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-179">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="5f40c-180">Wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="5f40c-180">Use the following values:</span></span>

* <span data-ttu-id="5f40c-181">Wartość *-GatewayType* dla konfiguracji lokacja-lokacja to *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="5f40c-181">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="5f40c-182">Typ bramy zawsze zależy od wdrażanej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5f40c-182">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="5f40c-183">Na przykład inne konfiguracje bramy mogą wymagać zastosowania wartości -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f40c-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="5f40c-184">Dla pozycji *-VpnType* określającej typ sieci VPN można wybrać opcję *RouteBased* (oparta na trasach; w dokumentacji używa się czasem określenia „brama dynamiczna”) lub *PolicyBased* (oparta na zasadach; w dokumentacji używa się czasem określenia „brama statyczna”).</span><span class="sxs-lookup"><span data-stu-id="5f40c-184">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="5f40c-185">Więcej informacji o typach bram sieci VPN można znaleźć w artykule [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="5f40c-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="5f40c-186">Wybierz jednostkę SKU bramy, która ma być używana.</span><span class="sxs-lookup"><span data-stu-id="5f40c-186">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="5f40c-187">Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5f40c-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="5f40c-188">Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).</span><span class="sxs-lookup"><span data-stu-id="5f40c-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="5f40c-189">Jeśli podczas tworzenia bramy sieci VPN wystąpi błąd dotyczący opcji -GatewaySku, sprawdź, czy zainstalowano najnowszą wersję poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f40c-189">If you get an error when creating the VPN gateway regarding the -GatewaySku, verify that you have installed the latest version of the PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="5f40c-190"><a name="ConfigureVPNDevice"></a>7. Konfiguracja urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5f40c-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="5f40c-191">Połączenia typu lokacja-lokacja z siecią lokalną wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-191">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="5f40c-192">W tym kroku konfigurowane jest urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="5f40c-193">Podczas konfigurowania urządzenia sieci VPN potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="5f40c-193">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="5f40c-194">Klucz współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="5f40c-194">A shared key.</span></span> <span data-ttu-id="5f40c-195">To ten sam klucz współużytkowany, który jest określany podczas tworzenia połączenia sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="5f40c-195">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="5f40c-196">W naszych przykładach używamy podstawowego klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="5f40c-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="5f40c-197">Zalecamy, aby do użycia wygenerować bardziej złożony klucz.</span><span class="sxs-lookup"><span data-stu-id="5f40c-197">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="5f40c-198">Publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-198">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="5f40c-199">Publiczny adres IP można wyświetlić za pomocą witryny Azure Portal, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f40c-199">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="5f40c-200">Aby znaleźć publiczny adres IP bramy sieci wirtualnej przy użyciu programu PowerShell, skorzystaj z poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="5f40c-200">To find the Public IP address of your virtual network gateway using PowerShell, use the following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="5f40c-201"><a name="CreateConnection"></a>8. Tworzenie połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5f40c-201"><a name="CreateConnection"></a>8. Create the VPN connection</span></span>

<span data-ttu-id="5f40c-202">Następnie należy utworzyć połączenie sieci VPN typu lokacja-lokacja między bramą sieci wirtualnej i urządzeniem sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-202">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="5f40c-203">Przedstawione wartości należy zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="5f40c-203">Be sure to replace the values with your own.</span></span> <span data-ttu-id="5f40c-204">Klucz współużytkowany musi odpowiadać wartości użytej podczas konfiguracji urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-204">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="5f40c-205">Należy pamiętać, że dla połączenia typu lokacja-lokacja wartość parametru „-ConnectionType” to *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="5f40c-205">Notice that the '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="5f40c-206">Ustaw zmienne.</span><span class="sxs-lookup"><span data-stu-id="5f40c-206">Set the variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="5f40c-207">Utwórz połączenie.</span><span class="sxs-lookup"><span data-stu-id="5f40c-207">Create the connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="5f40c-208">Po chwili zostanie nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="5f40c-208">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="5f40c-209"><a name="toverify"></a>9. Sprawdzenie połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5f40c-209"><a name="toverify"></a>9. Verify the VPN connection</span></span>

<span data-ttu-id="5f40c-210">Istnieje kilka różnych sposobów sprawdzenia połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-210">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="5f40c-211"><a name="connectVM"></a>Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="5f40c-211"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="5f40c-212"><a name="modify"></a>Modyfikowanie prefiksów adresów IP bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5f40c-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="5f40c-213">Jeśli prefiksy adresów IP, które mają być kierowane do lokalizacji lokalnej, ulegną zmianie, można zmodyfikować bramę sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5f40c-213">If the IP address prefixes that you want routed to your on-premises location change, you can modify the local network gateway.</span></span> <span data-ttu-id="5f40c-214">Poniżej przedstawiono dwa zestawy instrukcji.</span><span class="sxs-lookup"><span data-stu-id="5f40c-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="5f40c-215">Należy wybrać odpowiednie instrukcje w zależności od tego, czy utworzono już połączenie bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5f40c-215">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="5f40c-216"><a name="modifygwipaddress"></a>Modyfikowanie adresu IP bramy dla bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5f40c-216"><a name="modifygwipaddress"></a>Modify the gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f40c-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f40c-217">Next steps</span></span>

*  <span data-ttu-id="5f40c-218">Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="5f40c-218">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="5f40c-219">Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="5f40c-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="5f40c-220">Informacje na temat protokołu BGP można znaleźć w artykułach [BGP Overview](vpn-gateway-bgp-overview.md) (Omówienie protokołu BGP) i [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md) (Konfigurowanie protokołu BGP).</span><span class="sxs-lookup"><span data-stu-id="5f40c-220">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
