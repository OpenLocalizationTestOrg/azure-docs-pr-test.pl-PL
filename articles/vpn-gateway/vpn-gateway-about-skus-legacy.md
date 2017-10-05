---
title: Brama starszej wersji sieci wirtualnej platformy Azure jednostki SKU | Dokumentacja firmy Microsoft
description: Stary wirtualnych sieci jednostki SKU bramy.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="8002d-103">Praca z bramy sieci wirtualnej jednostki SKU (starszej wersji jednostki SKU)</span><span class="sxs-lookup"><span data-stu-id="8002d-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="8002d-104">Ten artykuł zawiera informacje dotyczące starszych bramy sieci wirtualnej (stare) jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="8002d-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="8002d-105">Starszego jednostki SKU nadal działa w obu modelach wdrażania dla bram sieci VPN, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="8002d-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="8002d-106">Klasycznego bramy sieci VPN w dalszym ciągu używać starszej wersji jednostki SKU, zarówno dla bramy istniejących i nowych bram.</span><span class="sxs-lookup"><span data-stu-id="8002d-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="8002d-107">Podczas tworzenia nowego Menedżera zasobów sieci VPN bramy, użyj nowej jednostki SKU bramy.</span><span class="sxs-lookup"><span data-stu-id="8002d-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="8002d-108">Informacje o nowej wersji produktu, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8002d-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="8002d-109"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="8002d-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="8002d-110"><a name="agg"></a>Szacowany łącznej przepływności przez jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="8002d-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="8002d-111"><a name="config"></a>Obsługiwane konfiguracje według typu jednostki SKU i sieci VPN</span><span class="sxs-lookup"><span data-stu-id="8002d-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="8002d-112"><a name="resize"></a>Zmień rozmiar bramy (zmienianie jednostka SKU bramy)</span><span class="sxs-lookup"><span data-stu-id="8002d-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="8002d-113">Można zmienić rozmiar jednostka SKU bramy w ramach tej samej rodziny SKU.</span><span class="sxs-lookup"><span data-stu-id="8002d-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="8002d-114">Na przykład jeśli masz wersji Standard, możesz zmienić rozmiar do SKU wysokowydajnej.</span><span class="sxs-lookup"><span data-stu-id="8002d-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="8002d-115">Nie można zmienić rozmiaru z bramy sieci VPN między starym jednostki SKU i nowe rodziny SKU.</span><span class="sxs-lookup"><span data-stu-id="8002d-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="8002d-116">Nie można na przykład przejść z wersji Standard, do wersji VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="8002d-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="8002d-117">Aby zmienić rozmiar jednostki SKU bramy dla klasycznym modelu wdrożenia, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8002d-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="8002d-118">Aby zmienić rozmiar jednostki SKU bramy dla modelu wdrażania usługi Resource Manager, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8002d-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="8002d-119"><a name="migrate"></a>Migracja do nowej bramy jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="8002d-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="8002d-120">Jeśli pracujesz z modelu wdrażania usługi Resource Manager, można migrować do nowej bramy jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="8002d-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="8002d-121">Jeśli pracujesz z klasycznym modelu wdrożenia, nie można migrować do nowej jednostki SKU i zamiast tego należy nadal używać starszej wersji jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="8002d-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8002d-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8002d-122">Next steps</span></span>

<span data-ttu-id="8002d-123">Aby uzyskać więcej informacji o nowej jednostki SKU bramy, zobacz [jednostki SKU bramy](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="8002d-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="8002d-124">Aby uzyskać więcej informacji na temat ustawień konfiguracji, zobacz [o bramy sieci VPN, ustawienia konfiguracji](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="8002d-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>