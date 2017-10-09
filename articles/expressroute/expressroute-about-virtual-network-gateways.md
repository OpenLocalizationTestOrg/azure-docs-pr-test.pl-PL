---
title: bramy sieci wirtualnej ExpressRoute aaaAbout | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="ef27a-103">Informacje o bramach sieci wirtualnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ef27a-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="ef27a-104">Brama sieci wirtualnej służy toosend ruchu sieciowego między sieciami wirtualnymi platformy Azure i lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ef27a-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="ef27a-105">Po skonfigurowaniu połączenia ExpressRoute, należy utworzyć i skonfigurować bramę sieci wirtualnej i połączenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef27a-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="ef27a-106">Podczas tworzenia bramy sieci wirtualnej należy określić kilka ustawień.</span><span class="sxs-lookup"><span data-stu-id="ef27a-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="ef27a-107">Jedno z ustawień wymaganych hello Określa, czy brama hello będzie używana dla ruchu ExpressRoute i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ef27a-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="ef27a-108">W modelu wdrażania usługi Resource Manager hello jest hello ustawienie "-elementu GatewayType".</span><span class="sxs-lookup"><span data-stu-id="ef27a-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="ef27a-109">Po ruch sieciowy będzie przesyłany w połączeniu sieci prywatnej, należy użyć typu bramy hello "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="ef27a-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="ef27a-110">Dotyczy to również określonego tooas bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef27a-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="ef27a-111">Gdy ruch sieciowy będzie przesyłany zaszyfrowanych przez hello publicznej sieci Internet, użyj typu bramy hello "Vpn".</span><span class="sxs-lookup"><span data-stu-id="ef27a-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="ef27a-112">Jest to tooas określonej bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ef27a-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="ef27a-113">Wszystkie połączenia typu lokacja-lokacja, punkt-lokacja i połączenia między sieciami wirtualnymi używają bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ef27a-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="ef27a-114">Każda sieć wirtualna może mieć tylko jedną bramę sieci wirtualnej na typ bramy.</span><span class="sxs-lookup"><span data-stu-id="ef27a-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="ef27a-115">Na przykład można mieć jedną bramę sieci wirtualnej, która używa klasy -GatewayType Vpn, oraz jednej, która używa klasy -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef27a-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="ef27a-116">Ten artykuł skupia się na bramę sieci wirtualnej hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef27a-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="ef27a-117"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="ef27a-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="ef27a-118">Jeśli chcesz tooupgrade Twojego tooa bramy bardziej zaawansowanych bramy jednostka SKU, w większości przypadków, w których można używać hello polecenia cmdlet programu PowerShell "Zmiany rozmiaru AzureRmVirtualNetworkGateway".</span><span class="sxs-lookup"><span data-stu-id="ef27a-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="ef27a-119">To będzie działać dla uaktualnienia tooStandard i wysokowydajnej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="ef27a-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="ef27a-120">Jednak toohello tooupgrade UltraPerformance SKU, konieczne będzie toorecreate hello bramy.</span><span class="sxs-lookup"><span data-stu-id="ef27a-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="ef27a-121"><a name="aggthroughput"></a>Szacowany łącznej przepływności według jednostka SKU bramy</span><span class="sxs-lookup"><span data-stu-id="ef27a-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="ef27a-122">Witaj poniższej tabeli przedstawiono typy bramy hello i hello szacowany łącznej przepływności.</span><span class="sxs-lookup"><span data-stu-id="ef27a-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="ef27a-123">Ta tabela odnosi się hello tooboth Resource Manager i klasycznych modeli wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ef27a-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ef27a-124">Przepływność aplikacji zależy od wielu czynników, takich jak czas oczekiwania na trasie hello, i hello liczba ruch przepływa zostanie otwarta aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="ef27a-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="ef27a-125">numery Hello hello tabeli reprezentują hello górny limit aplikacji hello mogących theorectically osiągnięcia w środowisku idealne.</span><span class="sxs-lookup"><span data-stu-id="ef27a-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="ef27a-126"><a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="ef27a-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="ef27a-127">Aby uzyskać dodatkowe zasoby techniczne i wymagania określonej składni, korzystając z polecenia cmdlet programu PowerShell i interfejsów API REST konfiguracji bramy sieci wirtualnej Zobacz hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="ef27a-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="ef27a-128">**Wdrożenie klasyczne**</span><span class="sxs-lookup"><span data-stu-id="ef27a-128">**Classic**</span></span> | <span data-ttu-id="ef27a-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ef27a-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="ef27a-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef27a-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="ef27a-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef27a-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="ef27a-132">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="ef27a-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="ef27a-133">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="ef27a-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="ef27a-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef27a-134">Next steps</span></span>
<span data-ttu-id="ef27a-135">Zobacz [omówienie ExpressRoute](expressroute-introduction.md) Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="ef27a-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

