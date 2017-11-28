---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: Portal | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Te kroki pomoże utworzyć przy użyciu portalu hello połączenie bramy sieci VPN typu lokacja-lokacja między lokalizacjami."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="4546f-104">Utwórz połączenie lokacja-lokacja w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4546f-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="4546f-105">W tym artykule opisano, jak toouse hello Azure toocreate portalu połączenie bramy sieci VPN lokacja-lokacja z toohello sieci Twojej lokalnej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="4546f-106">Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="4546f-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="4546f-107">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="4546f-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4546f-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4546f-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="4546f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4546f-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="4546f-110">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4546f-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="4546f-111">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="4546f-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="4546f-112">Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2).</span><span class="sxs-lookup"><span data-stu-id="4546f-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="4546f-113">Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP.</span><span class="sxs-lookup"><span data-stu-id="4546f-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="4546f-114">Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="4546f-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4546f-116">Before you begin</span></span>

<span data-ttu-id="4546f-117">Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="4546f-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="4546f-118">Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go.</span><span class="sxs-lookup"><span data-stu-id="4546f-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="4546f-119">Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="4546f-120">Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="4546f-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="4546f-121">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="4546f-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="4546f-122">Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy.</span><span class="sxs-lookup"><span data-stu-id="4546f-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="4546f-123">Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="4546f-124">Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="4546f-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="4546f-125"><a name="values"></a>Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="4546f-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="4546f-126">Przykłady Hello w tym artykule Użyj hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="4546f-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="4546f-127">Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="4546f-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="4546f-128">**Nazwa sieci wirtualnej:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4546f-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="4546f-129">**Przestrzeń adresowa:**</span><span class="sxs-lookup"><span data-stu-id="4546f-129">**Address Space:**</span></span> 
  * <span data-ttu-id="4546f-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4546f-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="4546f-131">10.12.0.0/16 (opcjonalnie na potrzeby tego ćwiczenia)</span><span class="sxs-lookup"><span data-stu-id="4546f-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="4546f-132">**Podsieci:**</span><span class="sxs-lookup"><span data-stu-id="4546f-132">**Subnets:**</span></span>
  * <span data-ttu-id="4546f-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4546f-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="4546f-134">BackEnd: 10.12.0.0/24 (opcjonalnie na potrzeby tego ćwiczenia)</span><span class="sxs-lookup"><span data-stu-id="4546f-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="4546f-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4546f-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="4546f-136">**Grupa zasobów:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="4546f-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="4546f-137">**Lokalizacja:** Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="4546f-137">**Location:** East US</span></span>
* <span data-ttu-id="4546f-138">**Serwer DNS:** opcjonalnie.</span><span class="sxs-lookup"><span data-stu-id="4546f-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="4546f-139">Witaj adres IP serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="4546f-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="4546f-140">**Nazwa bramy sieci wirtualnej:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="4546f-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="4546f-141">**Publiczny adres IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="4546f-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="4546f-142">**Typ sieci VPN:** oparta na trasach</span><span class="sxs-lookup"><span data-stu-id="4546f-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="4546f-143">**Typ połączenia:** lokacja-lokacja (IPsec)</span><span class="sxs-lookup"><span data-stu-id="4546f-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="4546f-144">**Typ bramy:** VPN</span><span class="sxs-lookup"><span data-stu-id="4546f-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="4546f-145">**Nazwa bramy sieci lokalnej:** Site2</span><span class="sxs-lookup"><span data-stu-id="4546f-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="4546f-146">**Nazwa połączenia:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="4546f-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="4546f-147"><a name="CreatVNet"></a>1. Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4546f-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="4546f-148"><a name="dns"></a>2. Określanie serwera DNS</span><span class="sxs-lookup"><span data-stu-id="4546f-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="4546f-149">DNS nie jest wymagane toocreate Site-to-Site połączenia.</span><span class="sxs-lookup"><span data-stu-id="4546f-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="4546f-150">Jednak jeśli chcesz toohave rozpoznawania nazw zasobów, które są wdrożone tooyour sieci wirtualnej, należy określić serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="4546f-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="4546f-151">To ustawienie umożliwia określenie serwera DNS hello mają toouse do rozpoznawania nazw dla tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="4546f-152">Nie powoduje ono jednak utworzenia serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="4546f-152">It does not create a DNS server.</span></span> <span data-ttu-id="4546f-153">Aby uzyskać więcej informacji na temat rozpoznawania nazw, zobacz artykuł [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Rozpoznawanie nazw dla maszyn wirtualnych i wystąpień roli)</span><span class="sxs-lookup"><span data-stu-id="4546f-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="4546f-154"><a name="gatewaysubnet"></a>3. Utwórz podsieć bramy hello</span><span class="sxs-lookup"><span data-stu-id="4546f-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="4546f-155"><a name="VNetGateway"></a>4. Tworzenie bramy sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="4546f-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="4546f-156"><a name="LocalNetworkGateway"></a>5. Utwórz bramę sieci lokalnej hello</span><span class="sxs-lookup"><span data-stu-id="4546f-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="4546f-157">Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="4546f-158">Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie.</span><span class="sxs-lookup"><span data-stu-id="4546f-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="4546f-159">Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy.</span><span class="sxs-lookup"><span data-stu-id="4546f-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="4546f-160">Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="4546f-161">Jeśli zmiany sieci lokalnej lub publicznego adresu IP toochange hello hello urządzenia sieci VPN, należy można łatwo aktualizować wartości hello później.</span><span class="sxs-lookup"><span data-stu-id="4546f-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="4546f-162"><a name="VPNDevice"></a>6. Konfiguracja urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="4546f-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="4546f-163">Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="4546f-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="4546f-164">W tym kroku konfigurowane jest urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="4546f-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="4546f-165">Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4546f-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="4546f-166">Klucz współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="4546f-166">A shared key.</span></span> <span data-ttu-id="4546f-167">Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="4546f-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="4546f-168">W naszych przykładach używamy podstawowego klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="4546f-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="4546f-169">Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.</span><span class="sxs-lookup"><span data-stu-id="4546f-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="4546f-170">Witaj publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4546f-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="4546f-171">Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4546f-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="4546f-172">toofind hello publiczny adres IP bramy sieci VPN przy użyciu hello portalu Azure Przejdź zbyt**bramy sieci wirtualnej**, następnie kliknij nazwę hello bramy.</span><span class="sxs-lookup"><span data-stu-id="4546f-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="4546f-173"><a name="CreateConnection"></a>7. Utwórz połączenie sieci VPN hello</span><span class="sxs-lookup"><span data-stu-id="4546f-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="4546f-174">Utwórz połączenie sieci VPN hello lokacja-lokacja między bramą sieci wirtualnej i lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="4546f-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="4546f-175"><a name="VerifyConnection"></a>8. Sprawdź hello połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="4546f-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="4546f-176"><a name="connectVM"></a>Maszyna wirtualna tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="4546f-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="4546f-177"><a name="reset"></a>Jak tooreset bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="4546f-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="4546f-178">Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="4546f-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="4546f-179">W takiej sytuacji lokalnego urządzenia sieci VPN są wszystkie działa poprawnie, ale są nie jest w stanie tooestablish tuneli protokołu IPsec o hello bram sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4546f-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="4546f-180">Aby uzyskać instrukcje, zobacz [Resetowanie bramy VPN Gateway](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="4546f-181"><a name="resize"></a>Jak toochange bramy jednostki SKU (zmiany rozmiaru bramy)</span><span class="sxs-lookup"><span data-stu-id="4546f-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="4546f-182">Aby hello kroki toochange jednostka SKU bramy, zobacz [jednostki SKU bramy](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="4546f-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4546f-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4546f-183">Next steps</span></span>

* <span data-ttu-id="4546f-184">Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="4546f-185">Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="4546f-186">Aby uzyskać informacje o połączeniach o wysokiej dostępności typu aktywne-aktywne, zobacz [Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="4546f-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
