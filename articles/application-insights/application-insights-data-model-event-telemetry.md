---
title: Model danych Telemetrii aplikacji Azure Insights - dane telemetryczne zdarzenia | Dokumentacja firmy Microsoft
description: "Model danych usługi Insights aplikacji dla dane telemetryczne zdarzenia"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 422e193ae10938954602a6ef8c49fd47f473bc01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="aa1ab-103">Dane telemetryczne zdarzenia: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa1ab-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="aa1ab-104">Można utworzyć zdarzenia telemetrii elementów (w [usługi Application Insights](app-insights-overview.md)) do reprezentowania zdarzenie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="aa1ab-105">Zwykle jest on interakcji z użytkownikiem, takich jak przycisk kliknij lub kolejność wyewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="aa1ab-106">Można także zdarzeń cyklu życia aplikacji, takich jak inicjowanie lub konfiguracji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="aa1ab-107">Semantycznie zdarzenia może lub nie może zostać skorelowane z żądania.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="aa1ab-108">Jednak jeśli prawidłowo używana, dane telemetryczne zdarzenia jest ważniejsze niż żądań i śladów.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="aa1ab-109">Zdarzenia należy tematu, aby rozdzielić od siebie, mniej aktywnego i reprezentują firm telemetrii [próbkowania](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="aa1ab-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="aa1ab-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="aa1ab-110">Name</span></span>

<span data-ttu-id="aa1ab-111">Nazwa zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-111">Event name.</span></span> <span data-ttu-id="aa1ab-112">Umożliwia grupowanie prawidłowego i przydatne metryki, należy ograniczyć aplikacji, tak aby generuje niewielką liczbę nazw oddzielne zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="aa1ab-113">Na przykład nie używaj osobnej nazwy dla każdego wystąpienia wygenerowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="aa1ab-114">Maksymalna długość: 512 znaków</span><span class="sxs-lookup"><span data-stu-id="aa1ab-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="aa1ab-115">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="aa1ab-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="aa1ab-116">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="aa1ab-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="aa1ab-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa1ab-117">Next steps</span></span>

- <span data-ttu-id="aa1ab-118">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="aa1ab-119">Pisanie niestandardowych zdarzeń telemetrii</span><span class="sxs-lookup"><span data-stu-id="aa1ab-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="aa1ab-120">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa1ab-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
