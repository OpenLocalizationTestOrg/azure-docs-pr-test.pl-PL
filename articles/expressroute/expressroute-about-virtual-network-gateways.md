---
title: Temat bram sieci wirtualnej ExpressRoute | Dokumentacja firmy Microsoft
description: "Informacje na temat bram sieci wirtualnej dla usługi ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="54b88-103">Informacje o bramach sieci wirtualnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="54b88-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="54b88-104">Brama sieci wirtualnej służy do wysyłania ruchu sieciowego między sieciami wirtualnymi platformy Azure i lokalnymi lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="54b88-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="54b88-105">Po skonfigurowaniu połączenia ExpressRoute, należy utworzyć i skonfigurować bramę sieci wirtualnej i połączenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54b88-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="54b88-106">Podczas tworzenia bramy sieci wirtualnej należy określić kilka ustawień.</span><span class="sxs-lookup"><span data-stu-id="54b88-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="54b88-107">Jeden z wymaganych ustawień Określa, czy brama będzie używana dla ruchu ExpressRoute i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="54b88-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="54b88-108">W modelu wdrażania usługi Resource Manager, jest ustawienie "-elementu GatewayType".</span><span class="sxs-lookup"><span data-stu-id="54b88-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="54b88-109">Gdy ruch sieciowy będzie przesyłany w połączeniu sieci prywatnej, używając typu bramy "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="54b88-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="54b88-110">Ten typ bramy jest również określany jako brama usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="54b88-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="54b88-111">Gdy ruch sieciowy będzie przesyłany zaszyfrowane w publicznej sieci Internet, używając typu bramy "Vpn".</span><span class="sxs-lookup"><span data-stu-id="54b88-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="54b88-112">Ten typ bramy jest określany jako brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="54b88-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="54b88-113">Wszystkie połączenia typu lokacja-lokacja, punkt-lokacja i połączenia między sieciami wirtualnymi używają bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="54b88-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="54b88-114">Każda sieć wirtualna może mieć tylko jedną bramę sieci wirtualnej na typ bramy.</span><span class="sxs-lookup"><span data-stu-id="54b88-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="54b88-115">Na przykład można mieć jedną bramę sieci wirtualnej, która używa klasy -GatewayType Vpn, oraz jednej, która używa klasy -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="54b88-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="54b88-116">Ten artykuł skupia się na bramę sieci wirtualnej usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="54b88-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="54b88-117"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="54b88-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="54b88-118">Jeśli chcesz uaktualnić bramę do bardziej zaawansowanych jednostka SKU bramy, w większości przypadków służy polecenie cmdlet programu PowerShell "Zmiany rozmiaru AzureRmVirtualNetworkGateway".</span><span class="sxs-lookup"><span data-stu-id="54b88-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="54b88-119">Będzie działać, dotyczy uaktualnień do standardowej i wysokowydajnej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="54b88-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="54b88-120">Jednak aby uaktualnić do wersji UltraPerformance, należy ponownie utworzyć bramę.</span><span class="sxs-lookup"><span data-stu-id="54b88-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="54b88-121"><a name="aggthroughput"></a>Szacowany łącznej przepływności według jednostka SKU bramy</span><span class="sxs-lookup"><span data-stu-id="54b88-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="54b88-122">W poniższej tabeli przedstawiono typy bram i szacowaną agregowaną przepływność.</span><span class="sxs-lookup"><span data-stu-id="54b88-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="54b88-123">Ta tabela ma zastosowanie w obu modelach wdrażania — przy użyciu usługi Resource Manager i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="54b88-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="54b88-124">Przepływność aplikacji zależy od wielu czynników, takich jak czas oczekiwania na trasie, a liczba przepływów ruchu sieciowego, który otwiera aplikację.</span><span class="sxs-lookup"><span data-stu-id="54b88-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="54b88-125">Numery w tabeli reprezentuje górny limit, który theorectically może aplikacji są dostępne w środowisku idealne.</span><span class="sxs-lookup"><span data-stu-id="54b88-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="54b88-126"><a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="54b88-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="54b88-127">Aby uzyskać dodatkowe zasoby techniczne i wymagania określonej składni, korzystając z polecenia cmdlet programu PowerShell i interfejsów API REST konfiguracji bramy sieci wirtualnej zobacz następujące strony:</span><span class="sxs-lookup"><span data-stu-id="54b88-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="54b88-128">**Wdrożenie klasyczne**</span><span class="sxs-lookup"><span data-stu-id="54b88-128">**Classic**</span></span> | <span data-ttu-id="54b88-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="54b88-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="54b88-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54b88-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="54b88-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54b88-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="54b88-132">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="54b88-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="54b88-133">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="54b88-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="54b88-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54b88-134">Next steps</span></span>
<span data-ttu-id="54b88-135">Zobacz [omówienie ExpressRoute](expressroute-introduction.md) Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="54b88-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

