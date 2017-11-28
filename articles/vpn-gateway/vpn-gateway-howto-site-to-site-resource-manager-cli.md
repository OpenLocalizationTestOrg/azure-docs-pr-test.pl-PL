---
title: "Łączenie sieci lokalnej sieci z siecią wirtualną platformy Azure: sieć VPN typu lokacja-lokacja: interfejs wiersza polecenia | Microsoft Docs"
description: "Kroki tworzenia połączenia IPsec z sieci lokalnej do sieci wirtualnej platformy Azure za pośrednictwem publicznego Internetu. Ta procedura jest pomocna podczas tworzenia połączenia bramy sieci VPN typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą interfejsu wiersza polecenia."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="c2397-104">Tworzenie sieci wirtualnej z wykorzystaniem połączenia sieci VPN typu lokacja-lokacja przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c2397-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="c2397-105">Ten artykuł pokazuje, jak używać interfejsu wiersza polecenia platformy Azure do tworzenia połączenia bramy sieci VPN lokacja-lokacja z Twojej sieci lokalnej do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="c2397-106">Kroki podane w tym artykule mają zastosowanie do modelu wdrażania przy użyciu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c2397-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="c2397-107">Tę konfigurację możesz również utworzyć przy użyciu innego narzędzia wdrażania lub modelu wdrażania, wybierając inną opcję z następującej listy:</span><span class="sxs-lookup"><span data-stu-id="c2397-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2397-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c2397-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c2397-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2397-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c2397-110">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c2397-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c2397-111">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="c2397-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="c2397-113">Połączenie bramy sieci VPN typu lokacja-lokacja umożliwia łączenie sieci lokalnej z siecią wirtualną platformy Azure za pośrednictwem tunelu sieci VPN IPsec/IKE (IKEv1 lub IKEv2).</span><span class="sxs-lookup"><span data-stu-id="c2397-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c2397-114">Ten typ połączenia wymaga lokalnego urządzenia sieci VPN z przypisanym publicznym adresem IP dostępnym z zewnątrz.</span><span class="sxs-lookup"><span data-stu-id="c2397-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="c2397-115">Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c2397-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2397-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c2397-116">Before you begin</span></span>

<span data-ttu-id="c2397-117">Przed rozpoczęciem konfiguracji sprawdź, czy są spełnione następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="c2397-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="c2397-118">Upewnij się, że masz zgodne urządzenie sieci VPN i dostępna jest osoba, która umie je skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="c2397-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="c2397-119">Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c2397-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c2397-120">Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c2397-121">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c2397-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c2397-122">Jeśli nie znasz zakresów adresów IP w konfiguracji swojej sieci lokalnej, skontaktuj się z osobą, która może podać Ci te dane.</span><span class="sxs-lookup"><span data-stu-id="c2397-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c2397-123">Tworząc tę konfigurację, musisz określić prefiksy zakresu adresów IP, które platforma Azure będzie kierować do Twojej lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="c2397-124">Żadna z podsieci sieci lokalnej nie może się nakładać na podsieci sieci wirtualnej, z którymi chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="c2397-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="c2397-125">Sprawdź, czy masz zainstalowaną najnowszą wersję poleceń interfejsu wiersza polecenia (2.0 lub nowszą).</span><span class="sxs-lookup"><span data-stu-id="c2397-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="c2397-126">Aby uzyskać informacje o instalowaniu poleceń interfejsu wiersza polecenia, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0](/cli/azure/install-azure-cli) i [Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2397-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="c2397-127"><a name="example"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="c2397-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c2397-128">Następujących wartości możesz użyć do tworzenia środowiska testowego lub odwoływać się do tych wartości, aby lepiej zrozumieć przykłady w niniejszym artykule:</span><span class="sxs-lookup"><span data-stu-id="c2397-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="c2397-129"><a name="Login"></a>1. Nawiązywanie połączenia z subskrypcją</span><span class="sxs-lookup"><span data-stu-id="c2397-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="c2397-130"><a name="rg"></a>2. Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c2397-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="c2397-131">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie „TestRG1” w lokalizacji „eastus”.</span><span class="sxs-lookup"><span data-stu-id="c2397-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="c2397-132">Jeśli masz już grupę zasobów w regionie, w którym chcesz utworzyć swoją sieć wirtualną, możesz jej użyć zamiast tej.</span><span class="sxs-lookup"><span data-stu-id="c2397-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="c2397-133"><a name="VNet"></a>3. Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c2397-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="c2397-134">Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją przy użyciu polecenia [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="c2397-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="c2397-135">Podczas tworzenia sieci wirtualnej upewnij się, że określone przestrzenie adresowe nie nakładają się na żadne inne przestrzenie adresowe w obrębie sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="c2397-136">Poniższy przykład obejmuje tworzenie sieci wirtualnej o nazwie „TestVNet1” i podsieci „Subnet1”.</span><span class="sxs-lookup"><span data-stu-id="c2397-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="c2397-137">4. <a name="gwsub"></a>Tworzenie podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="c2397-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="c2397-138">Dla tej konfiguracji potrzebna jest również podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="c2397-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="c2397-139">Brama sieci wirtualnej korzysta z podsieci bramy, która zawiera adresy IP używane przez usługi bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="c2397-140">Podczas tworzenia podsieci bramy musi ona otrzymać nazwę „GatewaySubnet”.</span><span class="sxs-lookup"><span data-stu-id="c2397-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="c2397-141">Jeśli zostanie nadana inna nazwa, podsieć zostanie utworzona, ale platforma Azure nie będzie jej traktowała jako podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="c2397-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="c2397-142">Rozmiar określanej podsieci bramy zależy od konfiguracji bramy sieci VPN, którą chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c2397-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="c2397-143">Chociaż możliwe jest utworzenie podsieci bramy tak małej, jak /29, zaleca się wybranie większej podsieci /27 lub /28, aby zawierała więcej adresów.</span><span class="sxs-lookup"><span data-stu-id="c2397-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="c2397-144">Zastosowanie większej podsieci bramy daje wystarczającą liczbę adresów IP, aby uwzględnić możliwe przyszłe konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="c2397-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="c2397-145">Użyj polecenia [az network vnet subnet create](/cli/azure/network/vnet/subnet#create), aby utworzyć podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="c2397-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="c2397-146"><a name="localnet"></a>5. Tworzenie bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="c2397-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="c2397-147">Brama sieci lokalnej zazwyczaj odwołuje się do lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="c2397-148">Nadaj lokacji nazwę, za pomocą której platforma Azure może odwołać się do niej, a następnie określ adres IP lokalnego urządzenia sieci VPN, z którym będzie tworzone połączenie.</span><span class="sxs-lookup"><span data-stu-id="c2397-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="c2397-149">Określ również prefiksy adresów IP, które będą kierowane za pośrednictwem bramy sieci VPN do urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="c2397-150">Określone prefiksy adresów są prefiksami znajdującymi się w Twojej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="c2397-151">W przypadku zmian w sieci lokalnej prefiksy można łatwo zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="c2397-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="c2397-152">Wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c2397-152">Use the following values:</span></span>

* <span data-ttu-id="c2397-153">*--gateway-ip-address* to adres IP lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c2397-154">Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c2397-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c2397-155">*--local-address-prefixes* to Twoje lokalne przestrzenie adresowe.</span><span class="sxs-lookup"><span data-stu-id="c2397-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="c2397-156">Użyj polecenia [az network local-gateway create](/cli/azure/network/local-gateway#create), aby dodać bramę sieci lokalnej z wieloma prefiksami adresów:</span><span class="sxs-lookup"><span data-stu-id="c2397-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="c2397-157"><a name="PublicIP"></a>6. Żądanie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="c2397-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="c2397-158">Brama sieci VPN musi mieć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="c2397-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c2397-159">Najpierw żąda się zasobu adresu IP, a następnie odwołuje do niego podczas tworzenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="c2397-160">Adres IP jest dynamicznie przypisywany do zasobu podczas tworzenia bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="c2397-161">Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c2397-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c2397-162">Nie można zażądać przypisania statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c2397-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c2397-163">Nie oznacza to jednak, że adres IP zmienia się po przypisaniu go do bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="c2397-164">Jedyną sytuacją, w której ma miejsce zmiana publicznego adresu IP, jest usunięcie bramy i jej ponowne utworzenie.</span><span class="sxs-lookup"><span data-stu-id="c2397-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="c2397-165">Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c2397-166">Użyj polecenia [az network public-ip create](/cli/azure/network/public-ip#create), aby zażądać dynamicznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c2397-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="c2397-167"><a name="CreateGateway"></a>7. Tworzenie bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c2397-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="c2397-168">Utwórz bramę sieci VPN sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="c2397-169">Tworzenie bramy sieci VPN może potrwać 45 minut lub więcej.</span><span class="sxs-lookup"><span data-stu-id="c2397-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="c2397-170">Wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c2397-170">Use the following values:</span></span>

* <span data-ttu-id="c2397-171">Wartość *-gateway-type* dla konfiguracji lokacja-lokacja to *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c2397-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c2397-172">Typ bramy zawsze zależy od wdrażanej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c2397-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="c2397-173">Aby uzyskać więcej informacji, zobacz [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype) (Typy bram).</span><span class="sxs-lookup"><span data-stu-id="c2397-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="c2397-174">Dla pozycji *-vpn-type* określającej typ sieci VPN można wybrać opcję *RouteBased* (oparta na trasach; w dokumentacji używa się czasem określenia „brama dynamiczna”) lub *PolicyBased* (oparta na zasadach; w dokumentacji używa się czasem określenia „brama statyczna”).</span><span class="sxs-lookup"><span data-stu-id="c2397-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="c2397-175">To ustawienie zależy od wymagań urządzenia, z którym nawiązujesz połączenie.</span><span class="sxs-lookup"><span data-stu-id="c2397-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="c2397-176">Aby uzyskać więcej informacji o typach bram sieci VPN, zobacz [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype) (Informacje o ustawieniach konfiguracji bramy sieci VPN).</span><span class="sxs-lookup"><span data-stu-id="c2397-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="c2397-177">Wybierz jednostkę SKU bramy, która ma być używana.</span><span class="sxs-lookup"><span data-stu-id="c2397-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="c2397-178">Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c2397-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c2397-179">Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).</span><span class="sxs-lookup"><span data-stu-id="c2397-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="c2397-180">Utwórz bramę sieci VPN za pomocą polecenia [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create).</span><span class="sxs-lookup"><span data-stu-id="c2397-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="c2397-181">Jeśli to polecenie zostanie uruchomione z parametrem „--no-wait”, nie będą widoczne żadne informacje zwrotne ani dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c2397-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="c2397-182">Ten parametr umożliwia utworzenie bramy w tle.</span><span class="sxs-lookup"><span data-stu-id="c2397-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="c2397-183">Utworzenie bramy trwa około 45 minut.</span><span class="sxs-lookup"><span data-stu-id="c2397-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="c2397-184"><a name="VPNDevice"></a>8. Konfiguracja urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c2397-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="c2397-185">Połączenia typu lokacja-lokacja z siecią lokalną wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="c2397-186">W tym kroku konfigurowane jest urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c2397-187">Podczas konfigurowania urządzenia sieci VPN potrzebne będą:</span><span class="sxs-lookup"><span data-stu-id="c2397-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="c2397-188">Klucz współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="c2397-188">A shared key.</span></span> <span data-ttu-id="c2397-189">To ten sam klucz współużytkowany, który jest określany podczas tworzenia połączenia sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="c2397-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c2397-190">W naszych przykładach używamy podstawowego klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c2397-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c2397-191">Zalecamy, aby do użycia wygenerować bardziej złożony klucz.</span><span class="sxs-lookup"><span data-stu-id="c2397-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="c2397-192">Publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c2397-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c2397-193">Publiczny adres IP można wyświetlić za pomocą witryny Azure Portal, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c2397-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c2397-194">Aby znaleźć publiczny adres IP swojej bramy sieci wirtualnej, użyj polecenia [az network public-ip list](/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="c2397-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="c2397-195">W celu poprawienia czytelności dane wyjściowe są sformatowane do wyświetlania listy publicznych adresów IP w formacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="c2397-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c2397-196"><a name="CreateConnection"></a>9. Tworzenie połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c2397-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="c2397-197">Utwórz połączenie sieci VPN typu lokacja-lokacja między bramą sieci wirtualnej a lokalnym urządzeniem sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="c2397-198">Zwróć szczególną uwagę na wartość udostępnionego klucza, która musi być zgodna ze skonfigurowaną wartością klucza współużytkowanego dla Twojego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c2397-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="c2397-199">Utwórz połączenie za pomocą polecenia [az network vpn-connection create](/cli/azure/network/vpn-connection#create).</span><span class="sxs-lookup"><span data-stu-id="c2397-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="c2397-200">Po chwili zostanie nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="c2397-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="c2397-201"><a name="toverify"></a>10. Sprawdzenie połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c2397-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="c2397-202">Jeśli chcesz użyć innej metody, aby sprawdzić swoje połączenie, zobacz [Weryfikowanie połączenia bramy sieci VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c2397-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="c2397-203"><a name="connectVM"></a>Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="c2397-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="c2397-204"><a name="tasks"></a>Typowe zadania</span><span class="sxs-lookup"><span data-stu-id="c2397-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="c2397-205">Ta sekcja zawiera typowe polecenia, które są przydatne przy pracy z konfiguracjami lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="c2397-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="c2397-206">Aby uzyskać pełną listę poleceń sieciowych interfejsu wiersza polecenia, zobacz [Interfejs wiersza polecenia platformy Azure — sieć](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="c2397-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c2397-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2397-207">Next steps</span></span>

* <span data-ttu-id="c2397-208">Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c2397-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c2397-209">Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="c2397-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c2397-210">Informacje na temat protokołu BGP można znaleźć w artykułach [BGP Overview](vpn-gateway-bgp-overview.md) (Omówienie protokołu BGP) i [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md) (Konfigurowanie protokołu BGP).</span><span class="sxs-lookup"><span data-stu-id="c2397-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="c2397-211">Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="c2397-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="c2397-212">Aby uzyskać informacje o połączeniach o wysokiej dostępności typu aktywne-aktywne, zobacz [Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="c2397-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="c2397-213">Aby zapoznać się z listą poleceń interfejsu wiersza polecenia platformy Azure dotyczących sieci, zobacz [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="c2397-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>