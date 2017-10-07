---
title: Brama sieci wirtualnej platformy Azure aaaLegacy jednostki SKU | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="f457e-103">Praca z bramy sieci wirtualnej jednostki SKU (starszej wersji jednostki SKU)</span><span class="sxs-lookup"><span data-stu-id="f457e-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="f457e-104">Ten artykuł zawiera informacje o hello starszej wersji (stare) bramy sieci wirtualnej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="f457e-105">starsza wersja Hello jednostki SKU nadal działa w obu modelach wdrażania dla bram sieci VPN, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="f457e-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="f457e-106">Klasycznego bramy sieci VPN kontynuować toouse hello starszej wersji jednostki SKU, zarówno dla bramy istniejących i nowych bram.</span><span class="sxs-lookup"><span data-stu-id="f457e-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="f457e-107">Podczas tworzenia nowego Menedżera zasobów sieci VPN bramy, użyj nowej bramy hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="f457e-108">Informacji o hello nowej wersji produktu, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f457e-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="f457e-109"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="f457e-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="f457e-110"><a name="agg"></a>Szacowany łącznej przepływności przez jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f457e-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="f457e-111"><a name="config"></a>Obsługiwane konfiguracje według typu jednostki SKU i sieci VPN</span><span class="sxs-lookup"><span data-stu-id="f457e-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="f457e-112"><a name="resize"></a>Zmień rozmiar bramy (zmienianie jednostka SKU bramy)</span><span class="sxs-lookup"><span data-stu-id="f457e-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="f457e-113">Możesz zmienić rozmiar jednostka SKU bramy w ramach hello tej samej rodziny SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="f457e-114">Na przykład jeśli masz wersji Standard, można zmienić rozmiar tooa wysokowydajnej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="f457e-115">Nie można zmienić rozmiaru sieć VPN bramy między hello starego jednostki SKU i hello nowe rodziny SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="f457e-116">Na przykład nie można przejść z wersji Standard tooa VpnGw2 jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="f457e-117">tooresize brama jednostki SKU dla hello klasycznego modelu wdrażania, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f457e-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="f457e-118">tooresize brama jednostki SKU dla hello modelu wdrażania usługi Resource Manager, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f457e-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="f457e-119"><a name="migrate"></a>Migrowanie toohello nową bramę jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f457e-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="f457e-120">Jeśli pracujesz z modelu wdrażania usługi Resource Manager hello, można migrować toohello nową bramę jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="f457e-121">Jeśli pracujesz z hello klasycznego modelu wdrażania, nie można migrować toohello nowe jednostki SKU i zamiast tego należy kontynuować toouse hello starszej wersji jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f457e-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f457e-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f457e-122">Next steps</span></span>

<span data-ttu-id="f457e-123">Aby uzyskać więcej informacji na temat hello nowe jednostki SKU bramy, zobacz [jednostki SKU bramy](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="f457e-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="f457e-124">Aby uzyskać więcej informacji na temat ustawień konfiguracji, zobacz [o bramy sieci VPN, ustawienia konfiguracji](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f457e-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>