---
title: "aaaHow tooscale środowiska Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "W tym samouczku przedstawiono sposób tooscale środowiska Azure czas serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="0d4cb-103">Jak tooscale środowisku Insights serii czasu</span><span class="sxs-lookup"><span data-stu-id="0d4cb-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="0d4cb-104">W tym samouczku przedstawiono sposób tooscale środowisku Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="0d4cb-105">Skalowania w górę różnych typów jednostki sku nie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="0d4cb-106">Nie można przekonwertować w środowisku zawierającym S1 Sku środowisku S2.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="0d4cb-107">Szybkość wejściowych S1 SKU i pojemności</span><span class="sxs-lookup"><span data-stu-id="0d4cb-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="0d4cb-108">S1 Pojemność jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="0d4cb-108">S1 SKU Capacity</span></span> | <span data-ttu-id="0d4cb-109">Szybkość transferu</span><span class="sxs-lookup"><span data-stu-id="0d4cb-109">Ingress Rate</span></span> | <span data-ttu-id="0d4cb-110">Maksymalna pojemność magazynu</span><span class="sxs-lookup"><span data-stu-id="0d4cb-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="0d4cb-111">1</span><span class="sxs-lookup"><span data-stu-id="0d4cb-111">1</span></span> | <span data-ttu-id="0d4cb-112">1 GB (1 mln zdarzeń)</span><span class="sxs-lookup"><span data-stu-id="0d4cb-112">1 GB (1 million events)</span></span> | <span data-ttu-id="0d4cb-113">30 GB (30 milionów zdarzeń) na miesiąc</span><span class="sxs-lookup"><span data-stu-id="0d4cb-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="0d4cb-114">10</span><span class="sxs-lookup"><span data-stu-id="0d4cb-114">10</span></span> | <span data-ttu-id="0d4cb-115">10 GB (10 milionów zdarzeń)</span><span class="sxs-lookup"><span data-stu-id="0d4cb-115">10 GB (10 million events)</span></span> | <span data-ttu-id="0d4cb-116">300 GB (300 milionów zdarzeń) na miesiąc</span><span class="sxs-lookup"><span data-stu-id="0d4cb-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="0d4cb-117">Szybkość wejściowych s2 jednostki SKU i pojemności</span><span class="sxs-lookup"><span data-stu-id="0d4cb-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="0d4cb-118">S2 Pojemność jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="0d4cb-118">S2 SKU Capacity</span></span> | <span data-ttu-id="0d4cb-119">Szybkość transferu</span><span class="sxs-lookup"><span data-stu-id="0d4cb-119">Ingress Rate</span></span> | <span data-ttu-id="0d4cb-120">Maksymalna pojemność magazynu</span><span class="sxs-lookup"><span data-stu-id="0d4cb-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="0d4cb-121">1</span><span class="sxs-lookup"><span data-stu-id="0d4cb-121">1</span></span> | <span data-ttu-id="0d4cb-122">10 GB (10 milionów zdarzeń)</span><span class="sxs-lookup"><span data-stu-id="0d4cb-122">10 GB (10 million events)</span></span> | <span data-ttu-id="0d4cb-123">300 GB (300 milionów zdarzeń) na miesiąc</span><span class="sxs-lookup"><span data-stu-id="0d4cb-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="0d4cb-124">10</span><span class="sxs-lookup"><span data-stu-id="0d4cb-124">10</span></span> | <span data-ttu-id="0d4cb-125">100 GB (100 milionów zdarzeń)</span><span class="sxs-lookup"><span data-stu-id="0d4cb-125">100 GB (100 million events)</span></span> | <span data-ttu-id="0d4cb-126">3 TB (zdarzenia miliard 3) na miesiąc</span><span class="sxs-lookup"><span data-stu-id="0d4cb-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="0d4cb-127">Możliwości skalowania liniowo, więc sku S1, o pojemności 2 obsługuje 2 GB (2 milionów) zdarzeń według dnia służąca szybkość i 60 GB (60 miliona zdarzeń) w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="0d4cb-128">Zmiana pojemności hello środowiska</span><span class="sxs-lookup"><span data-stu-id="0d4cb-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="0d4cb-129">W hello portalu Azure, wybierz hello środowiska której pojemność chcesz toochange.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="0d4cb-130">W obszarze Ustawienia kliknij przycisk Konfiguruj.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="0d4cb-131">Użyj systemu hello pojemności suwaka tooselect hello wydajności spełniający wymagania hello ceny wejściowych i pojemności magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d4cb-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d4cb-132">Next steps</span></span>

* <span data-ttu-id="0d4cb-133">Sprawdź, czy hello nowego miejsca jest wystarczająca tooprevent ograniczania.</span><span class="sxs-lookup"><span data-stu-id="0d4cb-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="0d4cb-134">Aby uzyskać więcej informacji, zobacz hello *środowisku może być pobieranie ograniczany* sekcji [tutaj](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cb-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
