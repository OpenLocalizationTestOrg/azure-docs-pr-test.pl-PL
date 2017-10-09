---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Ta procedura jest pomocna podczas tworzenia połączenia bramy sieci VPN typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą interfejsu wiersza polecenia."
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
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="88f1e-104">Tworzenie sieci wirtualnej z wykorzystaniem połączenia sieci VPN typu lokacja-lokacja przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="88f1e-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="88f1e-105">W tym artykule opisano, jak toouse hello Azure CLI toocreate połączenie bramy sieci VPN lokacja-lokacja z toohello sieci Twojej lokalnej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="88f1e-106">Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="88f1e-107">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="88f1e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="88f1e-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="88f1e-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="88f1e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88f1e-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="88f1e-110">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="88f1e-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="88f1e-111">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="88f1e-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="88f1e-113">Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2).</span><span class="sxs-lookup"><span data-stu-id="88f1e-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="88f1e-114">Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="88f1e-115">Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="88f1e-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="88f1e-116">Before you begin</span></span>

<span data-ttu-id="88f1e-117">Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="88f1e-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="88f1e-118">Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go.</span><span class="sxs-lookup"><span data-stu-id="88f1e-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="88f1e-119">Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="88f1e-120">Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="88f1e-121">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="88f1e-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="88f1e-122">Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="88f1e-123">Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="88f1e-124">Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="88f1e-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="88f1e-125">Sprawdź, że zainstalowano najnowszą wersję hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="88f1e-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="88f1e-126">Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli) i [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88f1e-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="88f1e-127"><a name="example"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="88f1e-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="88f1e-128">Można użyć hello następujące wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="88f1e-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

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

## <span data-ttu-id="88f1e-129"><a name="Login"></a>1. Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="88f1e-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="88f1e-130"><a name="rg"></a>2. Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="88f1e-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="88f1e-131">Witaj poniższy przykład tworzy grupę zasobów o nazwie "TestRG1" w lokalizacji "eastus" hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="88f1e-132">Jeśli masz już grupę zasobów w regionie hello mają toocreate sieci wirtualnej, można użyć niż jeden.</span><span class="sxs-lookup"><span data-stu-id="88f1e-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="88f1e-133"><a name="VNet"></a>3. Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="88f1e-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="88f1e-134">Jeśli nie masz już sieć wirtualną, utwórz ją za pomocą hello [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="88f1e-135">Podczas tworzenia sieci wirtualnej, upewnij się, że przestrzenie adresowe hello, które określisz nie nakłada przestrzeni adresowych hello wyposażonych w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="88f1e-136">Witaj poniższy przykład tworzy sieć wirtualną o nazwie "TestVNet1" i podsieć, "Podsieć1".</span><span class="sxs-lookup"><span data-stu-id="88f1e-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="88f1e-137">4. <a name="gwsub"></a>Utwórz podsieć bramy hello</span><span class="sxs-lookup"><span data-stu-id="88f1e-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="88f1e-138">Dla tej konfiguracji potrzebna jest również podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="88f1e-139">Brama sieci wirtualnej Hello używa podsieć bramy, która zawiera hello adresy IP, które są używane przez usługi bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="88f1e-140">Podczas tworzenia podsieci bramy musi ona otrzymać nazwę „GatewaySubnet”.</span><span class="sxs-lookup"><span data-stu-id="88f1e-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="88f1e-141">Jeśli zostanie nadana inna nazwa, podsieć zostanie utworzona, ale platforma Azure nie będzie jej traktowała jako podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="88f1e-142">rozmiar Hello hello podsieć bramy, który określisz jest zależna od konfiguracji bramy sieci VPN hello, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="88f1e-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="88f1e-143">Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając /27 lub /28.</span><span class="sxs-lookup"><span data-stu-id="88f1e-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="88f1e-144">Przy użyciu większych podsieci bramy umożliwia za mało adresów tooaccommodate możliwe przyszłych konfiguracją IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="88f1e-145">Użyj hello [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create) podsieci bramy hello toocreate polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="88f1e-146"><a name="localnet"></a>5. Utwórz bramę sieci lokalnej hello</span><span class="sxs-lookup"><span data-stu-id="88f1e-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="88f1e-147">Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="88f1e-148">Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie.</span><span class="sxs-lookup"><span data-stu-id="88f1e-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="88f1e-149">Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="88f1e-150">Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="88f1e-151">W przypadku zmiany sieci lokalnej, można łatwo aktualizować hello prefiksy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="88f1e-152">Użyj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="88f1e-152">Use hello following values:</span></span>

* <span data-ttu-id="88f1e-153">Witaj *— adres ip bramy* hello adres IP urządzenia sieci VPN użytkownika lokalnego.</span><span class="sxs-lookup"><span data-stu-id="88f1e-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="88f1e-154">Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="88f1e-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="88f1e-155">Witaj *--prefiksy w przypadku adresów lokalnych* są lokalnej przestrzeni adresowych.</span><span class="sxs-lookup"><span data-stu-id="88f1e-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="88f1e-156">Użyj hello [Tworzenie bramy lokalnej sieci az](/cli/azure/network/local-gateway#create) tooadd polecenia bramy sieci lokalnej przy użyciu wielu prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="88f1e-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="88f1e-157"><a name="PublicIP"></a>6. Żądanie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="88f1e-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="88f1e-158">Brama sieci VPN musi mieć publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="88f1e-159">Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="88f1e-160">adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="88f1e-161">Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="88f1e-162">Nie można zażądać przypisania statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="88f1e-163">Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="88f1e-164">Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie.</span><span class="sxs-lookup"><span data-stu-id="88f1e-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="88f1e-165">Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="88f1e-166">Użyj hello [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create) toorequest polecenia dynamicznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="88f1e-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="88f1e-167"><a name="CreateGateway"></a>7. Tworzenie bramy sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="88f1e-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="88f1e-168">Tworzenie bramy sieci VPN hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="88f1e-169">Tworzenie bramy sieci VPN może potrwać too45 minut lub więcej toocomplete.</span><span class="sxs-lookup"><span data-stu-id="88f1e-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="88f1e-170">Użyj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="88f1e-170">Use hello following values:</span></span>

* <span data-ttu-id="88f1e-171">Witaj *— typ bramy* Site-to-Site konfiguracja jest *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="88f1e-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="88f1e-172">Typ bramy Hello jest zawsze toohello określonej konfiguracji w przypadku wdrażania.</span><span class="sxs-lookup"><span data-stu-id="88f1e-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="88f1e-173">Aby uzyskać więcej informacji, zobacz [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype) (Typy bram).</span><span class="sxs-lookup"><span data-stu-id="88f1e-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="88f1e-174">Witaj *— sieci vpn typu* może być *RouteBased* (określony tooas dynamiczne bramy w części dokumentacji), lub *PolicyBased* (określony tooas statycznych bramy w niektórych dokumentacja).</span><span class="sxs-lookup"><span data-stu-id="88f1e-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="88f1e-175">Ustawienie Hello jest określonych toorequirements hello urządzenia, które są nawiązywane.</span><span class="sxs-lookup"><span data-stu-id="88f1e-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="88f1e-176">Aby uzyskać więcej informacji o typach bram sieci VPN, zobacz [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype) (Informacje o ustawieniach konfiguracji bramy sieci VPN).</span><span class="sxs-lookup"><span data-stu-id="88f1e-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="88f1e-177">Wybierz hello jednostka SKU bramy, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="88f1e-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="88f1e-178">Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="88f1e-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="88f1e-179">Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).</span><span class="sxs-lookup"><span data-stu-id="88f1e-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="88f1e-180">Tworzenie bramy sieci VPN hello przy użyciu hello [Tworzenie bramy sieci wirtualnej sieci az](/cli/azure/network/vnet-gateway#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="88f1e-181">Po uruchomieniu tego polecenia, używając hello parametr — nie - oczekiwania nie widać żadnych opinie i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="88f1e-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="88f1e-182">Ten parametr umożliwia toocreate bramy hello w tle hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="88f1e-183">Trwa około 45 minut toocreate bramy.</span><span class="sxs-lookup"><span data-stu-id="88f1e-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="88f1e-184"><a name="VPNDevice"></a>8. Konfiguracja urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="88f1e-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="88f1e-185">Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="88f1e-186">W tym kroku konfigurowane jest urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="88f1e-187">Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="88f1e-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="88f1e-188">Klucz współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="88f1e-188">A shared key.</span></span> <span data-ttu-id="88f1e-189">Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="88f1e-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="88f1e-190">W naszych przykładach używamy podstawowego klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="88f1e-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="88f1e-191">Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.</span><span class="sxs-lookup"><span data-stu-id="88f1e-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="88f1e-192">Witaj publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88f1e-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="88f1e-193">Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="88f1e-194">toofind hello publicznego adresu IP bramy sieci wirtualnej, użyj hello [az sieci ip publicznego listy](/cli/azure/network/public-ip#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="88f1e-195">Czytelnej, dane wyjściowe hello jest sformatowany toodisplay hello lista publicznych adresów IP w formacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="88f1e-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="88f1e-196"><a name="CreateConnection"></a>9. Utwórz połączenie sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="88f1e-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="88f1e-197">Utwórz połączenie sieci VPN hello lokacja-lokacja między bramą sieci wirtualnej i lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="88f1e-198">Płatności szczególną uwagę toohello udostępnionego klucza wartość, która musi być zgodna z hello skonfigurowane udostępnionych wartości klucza dla urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="88f1e-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="88f1e-199">Utwórz połączenie hello przy użyciu hello [Tworzenie połączenia sieci vpn az sieci](/cli/azure/network/vpn-connection#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="88f1e-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="88f1e-200">Automatycznie podczas hello zostanie nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="88f1e-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="88f1e-201"><a name="toverify"></a>10. Sprawdź hello połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="88f1e-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="88f1e-202">Jeśli chcesz toouse innego tooverify metody połączenia, zobacz [sprawdzić połączenie bramy sieci VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="88f1e-203"><a name="connectVM"></a>Maszyna wirtualna tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="88f1e-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="88f1e-204"><a name="tasks"></a>Typowe zadania</span><span class="sxs-lookup"><span data-stu-id="88f1e-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="88f1e-205">Ta sekcja zawiera typowe polecenia, które są przydatne przy pracy z konfiguracjami lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="88f1e-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="88f1e-206">Witaj pełną listę poleceń interfejsu wiersza polecenia sieci, zobacz [wiersza polecenia platformy Azure — sieci](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="88f1e-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="88f1e-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88f1e-207">Next steps</span></span>

* <span data-ttu-id="88f1e-208">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88f1e-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="88f1e-209">Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="88f1e-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="88f1e-210">Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="88f1e-211">Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="88f1e-212">Aby uzyskać informacje o połączeniach o wysokiej dostępności typu aktywne-aktywne, zobacz [Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="88f1e-213">Aby zapoznać się z listą poleceń interfejsu wiersza polecenia platformy Azure dotyczących sieci, zobacz [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="88f1e-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>