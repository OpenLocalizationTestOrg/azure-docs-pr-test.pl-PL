---
title: "Planowanie i projektowanie pod kątem połączeń między lokalizacjami: Brama sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat bramy sieci VPN planowania i projektowania dla między różnymi lokalizacjami, hybrydowej i połączeń do wirtualnymi"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="b1039-103">Planowanie i projektowanie dla usługi VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b1039-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="b1039-104">Planowanie i projektowanie sieci między lokalizacjami i konfiguracje sieci wirtualnej do sieci wirtualnej może być proste i złożone, w zależności od potrzeb sieci.</span><span class="sxs-lookup"><span data-stu-id="b1039-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="b1039-105">W tym artykule przedstawiono podstawowe zagadnienia dotyczące planowania i projektowania.</span><span class="sxs-lookup"><span data-stu-id="b1039-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="b1039-106"><a name="planning"></a>Planowanie</span><span class="sxs-lookup"><span data-stu-id="b1039-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="b1039-107"><a name="compare"></a>Opcje łączności między lokalizacjami</span><span class="sxs-lookup"><span data-stu-id="b1039-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="b1039-108">Jeśli chcesz tooconnect lokalnej bezpiecznie Lokacje sieci wirtualnej tooa, więc ma trzy różne sposoby toodo: lokacja-lokacja, punkt-lokacja i ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b1039-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="b1039-109">Porównaj hello różnych między lokalizacjami połączeń, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b1039-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="b1039-110">wybrana opcja Hello może zależeć od różnych zagadnienia, takie jak:</span><span class="sxs-lookup"><span data-stu-id="b1039-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="b1039-111">Jakiego rodzaju przepływności wymaga rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="b1039-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="b1039-112">Czy chcesz toocommunicate za pośrednictwem hello publicznej sieci Internet za pośrednictwem bezpiecznej sieci VPN lub za pośrednictwem prywatnego połączenia?</span><span class="sxs-lookup"><span data-stu-id="b1039-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="b1039-113">Masz publicznego toouse dostępny adres IP?</span><span class="sxs-lookup"><span data-stu-id="b1039-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="b1039-114">Czy planujesz toouse urządzenia sieci VPN?</span><span class="sxs-lookup"><span data-stu-id="b1039-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="b1039-115">Jeśli tak, to czy jest ono zgodne?</span><span class="sxs-lookup"><span data-stu-id="b1039-115">If so, is it compatible?</span></span>
* <span data-ttu-id="b1039-116">Czy zamierzasz połączyć tylko kilka komputerów, czy też chcesz utworzyć trwałe połączenie dla witryny?</span><span class="sxs-lookup"><span data-stu-id="b1039-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="b1039-117">Jaki typ bramy sieci VPN jest wymagany dla rozwiązania hello ma toocreate?</span><span class="sxs-lookup"><span data-stu-id="b1039-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="b1039-118">Które jednostka SKU bramy należy używać?</span><span class="sxs-lookup"><span data-stu-id="b1039-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="b1039-119"><a name="planningtable"></a>Tabela planowania</span><span class="sxs-lookup"><span data-stu-id="b1039-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="b1039-120">Witaj w poniższej tabeli ułatwią podjęcie decyzji hello najlepszej opcji łączności dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b1039-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="b1039-121"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="b1039-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="b1039-122"><a name="wf"></a>Przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="b1039-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="b1039-123">Witaj następujące przedstawiono listę hello wspólnego przepływu pracy dla łączności chmury:</span><span class="sxs-lookup"><span data-stu-id="b1039-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="b1039-124">Projekt i plan, który łączności topologii i listy hello adres miejsca do wszystkich sieci mają tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b1039-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="b1039-125">Tworzenie sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1039-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="b1039-126">Tworzenie bramy sieci VPN dla hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1039-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="b1039-127">Tworzenie i konfigurowanie połączenia lokalnego tooon sieci lub innych sieci wirtualnych (w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="b1039-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="b1039-128">Utwórz i skonfiguruj połączenie punkt-lokacja dla bramy sieci VPN platformy Azure (w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="b1039-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="b1039-129"><a name="design"></a>Projekt</span><span class="sxs-lookup"><span data-stu-id="b1039-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="b1039-130"><a name="topologies"></a>Topologie połączenia</span><span class="sxs-lookup"><span data-stu-id="b1039-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="b1039-131">Przyjrzeć hello diagramów w hello [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b1039-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="b1039-132">Artykuł Hello zawiera podstawowe diagramy, hello modele wdrażania dla każdej topologii i narzędzia wdrażania dostępne hello toodeploy można użyć w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b1039-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="b1039-133"><a name="designbasics"></a>Podstawowe informacje o projekcie</span><span class="sxs-lookup"><span data-stu-id="b1039-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="b1039-134">Hello w następujących sekcjach omówiono w nim podstawowe bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b1039-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="b1039-135"><a name="servicelimits"></a>Limity usług sieci</span><span class="sxs-lookup"><span data-stu-id="b1039-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="b1039-136">Przewijanie hello tabel tooview [sieci usług limity](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b1039-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="b1039-137">limity Hello na liście mogą mieć wpływ na projekt.</span><span class="sxs-lookup"><span data-stu-id="b1039-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="b1039-138"><a name="subnets"></a>Temat podsieci</span><span class="sxs-lookup"><span data-stu-id="b1039-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="b1039-139">Podczas tworzenia połączenia, należy wziąć pod uwagę zakresy podsieci.</span><span class="sxs-lookup"><span data-stu-id="b1039-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="b1039-140">Nie można umieścić nakładające się zakresy adresów w podsieci.</span><span class="sxs-lookup"><span data-stu-id="b1039-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="b1039-141">Nakładające się podsieci jest po jednej wirtualnej sieci lub lokalnymi lokalizacji zawiera hello, który zawiera tą samą przestrzenią adresów, która hello z innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b1039-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="b1039-142">Oznacza to, należy inżynierów Twojej sieci dla Twojego toocarve sieci lokalnej lokalnymi zakresu dla toouse możesz dla Azure IP adresowania miejsca/podsieci.</span><span class="sxs-lookup"><span data-stu-id="b1039-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="b1039-143">Należy przestrzeń adresów, która nie jest używany w sieci lokalnej lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="b1039-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="b1039-144">Unikanie nakładające się podsieci ważne jest również podczas pracy z połączeniami sieci wirtualnej do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1039-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="b1039-145">Jeśli nakłada się na podsieci i adres IP istnieje zarówno wysyłania hello, jak i docelowy sieci wirtualnych, połączeń do wirtualnymi zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="b1039-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="b1039-146">Azure nie może przekierować z toohello danych hello innych sieci wirtualnej ponieważ hello adres docelowy jest częścią hello wysyłania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1039-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="b1039-147">Bramy sieci VPN wymaga określonej podsieci o nazwie podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="b1039-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="b1039-148">Wszystkie podsieci bramy muszą nosić nazwy GatewaySubnet toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="b1039-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="b1039-149">Upewnij się, nie tooname podsieć bramy innej nazwy i nie wdrażać maszyny wirtualne lub podsieci bramy toohello cokolwiek innego.</span><span class="sxs-lookup"><span data-stu-id="b1039-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="b1039-150">Zobacz [podsieci bramy](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="b1039-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="b1039-151"><a name="local"></a>Temat bram sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="b1039-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="b1039-152">Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b1039-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="b1039-153">W hello klasycznego modelu wdrażania hello bramy sieci lokalnej jest określony tooas lokalnej lokacji sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b1039-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="b1039-154">Podczas konfigurowania bramy sieci lokalnej, nadaj mu nazwę, określ hello publiczny adres IP urządzenia sieci VPN lokalne powitania i określ hello prefiksy adresów, które znajdują się w lokalizacji lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="b1039-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="b1039-155">Azure analizuje hello prefiksy adresów docelowy dla ruchu sieciowego, sprawdza hello konfiguracji, które zostały określone dla bramy sieci lokalnej hello i odpowiednio kieruje pakiety.</span><span class="sxs-lookup"><span data-stu-id="b1039-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="b1039-156">W razie potrzeby można zmodyfikować hello prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="b1039-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="b1039-157">Aby uzyskać więcej informacji, zobacz [bramy sieci lokalnej](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="b1039-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="b1039-158"><a name="gwtype"></a>Typy bramy — informacje</span><span class="sxs-lookup"><span data-stu-id="b1039-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="b1039-159">Bardzo ważne jest wybranie hello typu bramy poprawne dla danej topologii.</span><span class="sxs-lookup"><span data-stu-id="b1039-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="b1039-160">W przypadku wybrania niewłaściwego typu hello brama nie będzie działać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="b1039-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="b1039-161">Typ bramy Hello Określa jak brama hello łączy i jest wymaganego ustawienia konfiguracji dla modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b1039-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="b1039-162">dostępne są następujące typy bramy Hello:</span><span class="sxs-lookup"><span data-stu-id="b1039-162">hello gateway types are:</span></span>

* <span data-ttu-id="b1039-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="b1039-163">Vpn</span></span>
* <span data-ttu-id="b1039-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b1039-164">ExpressRoute</span></span>

#### <span data-ttu-id="b1039-165"><a name="connectiontype"></a>Typy połączenia — informacje</span><span class="sxs-lookup"><span data-stu-id="b1039-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="b1039-166">Każda konfiguracja wymaga określonego typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="b1039-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="b1039-167">typy połączeń Hello są:</span><span class="sxs-lookup"><span data-stu-id="b1039-167">hello connection types are:</span></span>

* <span data-ttu-id="b1039-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="b1039-168">IPsec</span></span>
* <span data-ttu-id="b1039-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="b1039-169">Vnet2Vnet</span></span>
* <span data-ttu-id="b1039-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b1039-170">ExpressRoute</span></span>
* <span data-ttu-id="b1039-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="b1039-171">VPNClient</span></span>

#### <span data-ttu-id="b1039-172"><a name="vpntype"></a>Typy sieci VPN — informacje</span><span class="sxs-lookup"><span data-stu-id="b1039-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="b1039-173">Każdej konfiguracji wymaga określonego typu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b1039-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="b1039-174">Jeśli są łączenie dwóch konfiguracji, takich jak tworzenie połączenia lokacja-lokacja i toohello połączenie punkt-lokacja tej samej sieci wirtualnej, należy użyć typu sieci VPN, który spełnia wymagania zarówno połączenia.</span><span class="sxs-lookup"><span data-stu-id="b1039-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="b1039-175">Witaj w poniższych tabelach hello sieci VPN typu ponieważ mapuje on tooeach Konfiguracja połączenia.</span><span class="sxs-lookup"><span data-stu-id="b1039-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="b1039-176">Upewnij się, że hello typ sieci VPN dla bramy konfiguracji hello dopasowań, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="b1039-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="b1039-177"><a name="devices"></a>Urządzenia sieci VPN w przypadku połączeń lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="b1039-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="b1039-178">połączenie tooconfigure Site-to-Site, niezależnie od tego modelu wdrażania należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b1039-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="b1039-179">Urządzenia sieci VPN, który jest zgodny z bram sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b1039-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="b1039-180">Adres IPv4 publicznych, który nie znajduje się za translatorem adresów Sieciowych</span><span class="sxs-lookup"><span data-stu-id="b1039-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="b1039-181">Należy środowisko toohave skonfigurowanie urządzenia sieci VPN lub ktoś, który może skonfigurować hello urządzenia dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b1039-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="b1039-182"><a name="forcedtunnel"></a>Należy wziąć pod uwagę routingu tunelowania wymuszonego</span><span class="sxs-lookup"><span data-stu-id="b1039-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="b1039-183">W przypadku większości konfiguracji można skonfigurować wymuszanie tunelowania.</span><span class="sxs-lookup"><span data-stu-id="b1039-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="b1039-184">Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b1039-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="b1039-185">Jest to wymagane krytycznych dla większości organizacji IT zasad.</span><span class="sxs-lookup"><span data-stu-id="b1039-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="b1039-186">Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure będzie zawsze przechodzenie od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b1039-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="b1039-187">Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b1039-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="b1039-188">W obu modeli wdrażania i za pomocą różnych narzędzi można skonfigurować połączenie tunelowania wymuszonego.</span><span class="sxs-lookup"><span data-stu-id="b1039-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="b1039-189">Aby uzyskać więcej informacji, zobacz [Konfiguracja wymuszonego tunelowania](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="b1039-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="b1039-190">**Diagram tunelowania wymuszonego**</span><span class="sxs-lookup"><span data-stu-id="b1039-190">**Forced tunneling diagram**</span></span>

![Diagram tunelowania wymuszonego Brama sieci VPN](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="b1039-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1039-192">Next steps</span></span>

<span data-ttu-id="b1039-193">Zobacz hello [bramy sieci VPN — często zadawane pytania](vpn-gateway-vpn-faq.md) i [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykuły Aby uzyskać więcej informacji o toohelp możesz z projektu.</span><span class="sxs-lookup"><span data-stu-id="b1039-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="b1039-194">Aby uzyskać więcej informacji o ustawieniach bramy, zobacz [o ustawienia bramy sieci VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b1039-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>