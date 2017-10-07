---
title: aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne zdarzenia | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="902fc-103">Dane telemetryczne zdarzenia: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="902fc-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="902fc-104">Można utworzyć zdarzenia telemetrii elementów (w [usługi Application Insights](app-insights-overview.md)) toorepresent zdarzenie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="902fc-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="902fc-105">Zwykle jest on interakcji z użytkownikiem, takich jak przycisk kliknij lub kolejność wyewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="902fc-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="902fc-106">Można także zdarzeń cyklu życia aplikacji, takich jak inicjowanie lub konfiguracji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="902fc-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="902fc-107">Semantycznie zdarzenia może lub nie może być skorelowane toorequests.</span><span class="sxs-lookup"><span data-stu-id="902fc-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="902fc-108">Jednak jeśli prawidłowo używana, dane telemetryczne zdarzenia jest ważniejsze niż żądań i śladów.</span><span class="sxs-lookup"><span data-stu-id="902fc-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="902fc-109">Zdarzenia reprezentują telemetrii biznesowych i powinna być tooseparate podmiotu, mniej aktywnego [próbkowania](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="902fc-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="902fc-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="902fc-110">Name</span></span>

<span data-ttu-id="902fc-111">Nazwa zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="902fc-111">Event name.</span></span> <span data-ttu-id="902fc-112">Grupowanie prawidłowego tooallow i przydatne metryki, należy ograniczyć aplikacji tak, aby generuje niewielką liczbę nazw oddzielne zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="902fc-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="902fc-113">Na przykład nie używaj osobnej nazwy dla każdego wystąpienia wygenerowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="902fc-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="902fc-114">Maksymalna długość: 512 znaków</span><span class="sxs-lookup"><span data-stu-id="902fc-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="902fc-115">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="902fc-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="902fc-116">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="902fc-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="902fc-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="902fc-117">Next steps</span></span>

- <span data-ttu-id="902fc-118">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="902fc-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="902fc-119">Pisanie niestandardowych zdarzeń telemetrii</span><span class="sxs-lookup"><span data-stu-id="902fc-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="902fc-120">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="902fc-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
