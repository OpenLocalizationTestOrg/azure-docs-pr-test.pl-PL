---
title: "Wymagania dotyczące usługi ExpressRoute aaaQoS | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera szczegółowe wymagania dotyczące konfigurowania technologii QoS oraz zarządzania nią na potrzeby obwodów usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="f8e08-103">Wymagania dotyczące technologii QoS w usłudze ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f8e08-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="f8e08-104">Program Skype dla firm obejmuje różne obciążenia, które wymagają zróżnicowanej obsługi w technologii QoS.</span><span class="sxs-lookup"><span data-stu-id="f8e08-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="f8e08-105">Jeśli planujesz tooconsume głosu usługi ExpressRoute, należy przestrzegać toohello wymagania opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="f8e08-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="f8e08-106">Mają zastosowanie wymagania QoS toohello komunikacji równorzędnej firmy Microsoft tylko.</span><span class="sxs-lookup"><span data-stu-id="f8e08-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="f8e08-107">Witaj wartości DSCP w ruchu sieciowego w komunikacji równorzędnej publicznej platformy Azure i Azure prywatnej komunikacji równorzędnej otrzymano będzie too0 resetowania.</span><span class="sxs-lookup"><span data-stu-id="f8e08-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="f8e08-108">Witaj Poniższa tabela zawiera listę oznaczenia wartościami DSCP używane przez usługi Skype dla firm.</span><span class="sxs-lookup"><span data-stu-id="f8e08-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="f8e08-109">Odwołuje się zbyt[Zarządzanie QoS dla usługi Skype dla firm](https://technet.microsoft.com/library/gg405409.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f8e08-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="f8e08-110">**Klasa ruchu**</span><span class="sxs-lookup"><span data-stu-id="f8e08-110">**Traffic Class**</span></span> | <span data-ttu-id="f8e08-111">**Obsługa (oznaczanie DSCP)**</span><span class="sxs-lookup"><span data-stu-id="f8e08-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="f8e08-112">**Obciążenia programu Skype dla firm**</span><span class="sxs-lookup"><span data-stu-id="f8e08-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8e08-113">**Połączenia głosowe**</span><span class="sxs-lookup"><span data-stu-id="f8e08-113">**Voice**</span></span> |<span data-ttu-id="f8e08-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="f8e08-114">EF (46)</span></span> |<span data-ttu-id="f8e08-115">Połączenia głosowe Skype/Lync</span><span class="sxs-lookup"><span data-stu-id="f8e08-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="f8e08-116">**Interaktywne**</span><span class="sxs-lookup"><span data-stu-id="f8e08-116">**Interactive**</span></span> |<span data-ttu-id="f8e08-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="f8e08-117">AF41 (34)</span></span> |<span data-ttu-id="f8e08-118">Wideo, VBSS</span><span class="sxs-lookup"><span data-stu-id="f8e08-118">Video, VBSS</span></span> |
| <span data-ttu-id="f8e08-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="f8e08-119">AF21 (18)</span></span> |<span data-ttu-id="f8e08-120">Współdzielenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8e08-120">App sharing</span></span> | |
| <span data-ttu-id="f8e08-121">**Domyślne**</span><span class="sxs-lookup"><span data-stu-id="f8e08-121">**Default**</span></span> |<span data-ttu-id="f8e08-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="f8e08-122">AF11 (10)</span></span> |<span data-ttu-id="f8e08-123">Transfer plików</span><span class="sxs-lookup"><span data-stu-id="f8e08-123">File transfer</span></span> |
| <span data-ttu-id="f8e08-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="f8e08-124">CS0 (0)</span></span> |<span data-ttu-id="f8e08-125">Inne</span><span class="sxs-lookup"><span data-stu-id="f8e08-125">Anything else</span></span> | |

* <span data-ttu-id="f8e08-126">Należy sklasyfikować hello obciążeń i oznaczenia wartościami DSCP prawo hello.</span><span class="sxs-lookup"><span data-stu-id="f8e08-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="f8e08-127">Wykonaj hello wskazówki [tutaj](https://technet.microsoft.com/library/gg405409.aspx) na temat oznaczenia wartościami DSCP tooset w sieci.</span><span class="sxs-lookup"><span data-stu-id="f8e08-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="f8e08-128">Skonfiguruj i obsługuj wiele kolejek w technologii QoS w sieci.</span><span class="sxs-lookup"><span data-stu-id="f8e08-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="f8e08-129">Głosu musi być klasą autonomicznej i traktowane EF hello określone w dokumencie RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="f8e08-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="f8e08-130">Można określić hello kolejkowania mechanizm, zasady wykrywania przeciążenia oraz możliwości przydziału przepustowości dla klasy ruchu.</span><span class="sxs-lookup"><span data-stu-id="f8e08-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="f8e08-131">Jednak hello DSCP oznaczenie dla usługi Skype dla firm obciążeń muszą zostać zachowane.</span><span class="sxs-lookup"><span data-stu-id="f8e08-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="f8e08-132">Jeśli używasz oznaczenia wartościami DSCP nie są wymienione powyżej, np. AF31 (26), muszą zmodyfikować tego too0 wartości DSCP przed wysłaniem tooMicrosoft pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="f8e08-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="f8e08-133">Firma Microsoft wysyła tylko pakietów oznaczonych hello wartości DSCP pokazano hello powyżej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f8e08-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f8e08-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8e08-134">Next steps</span></span>
* <span data-ttu-id="f8e08-135">Zobacz wymagania toohello [Routing](expressroute-routing.md) i [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="f8e08-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="f8e08-136">Zobacz następujące hello łączy tooconfigure połączenie ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f8e08-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="f8e08-137">Tworzenie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f8e08-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="f8e08-138">Configure routing (Konfigurowanie routingu)</span><span class="sxs-lookup"><span data-stu-id="f8e08-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="f8e08-139">Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="f8e08-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

