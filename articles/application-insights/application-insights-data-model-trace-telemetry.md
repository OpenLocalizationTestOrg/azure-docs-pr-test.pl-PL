---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne śledzenia | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne śledzenia"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="98759-103">Dane telemetryczne śledzenia: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="98759-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="98759-104">Dane telemetryczne śledzenia (w [usługi Application Insights](app-insights-overview.md)) reprezentuje `printf` styl instrukcji śledzenia, które są przeszukiwane tekstu.</span><span class="sxs-lookup"><span data-stu-id="98759-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="98759-105">`Log4Net`, `NLog`, i inne wpisy w pliku tekstowym dziennika są przetłumaczyć wystąpień tego typu.</span><span class="sxs-lookup"><span data-stu-id="98759-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="98759-106">Witaj śledzenia nie ma pomiarów jako rozszerzalności.</span><span class="sxs-lookup"><span data-stu-id="98759-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="98759-107">Komunikat</span><span class="sxs-lookup"><span data-stu-id="98759-107">Message</span></span>

<span data-ttu-id="98759-108">Komunikat śledzenia.</span><span class="sxs-lookup"><span data-stu-id="98759-108">Trace message.</span></span>

<span data-ttu-id="98759-109">Maksymalna długość: 32768 znaków</span><span class="sxs-lookup"><span data-stu-id="98759-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="98759-110">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="98759-110">Severity level</span></span>

<span data-ttu-id="98759-111">Poziom ważności śledzenia.</span><span class="sxs-lookup"><span data-stu-id="98759-111">Trace severity level.</span></span> <span data-ttu-id="98759-112">Wartość może być `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="98759-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="98759-113">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="98759-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="98759-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98759-114">Next steps</span></span>

- <span data-ttu-id="98759-115">[Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="98759-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="98759-116">[Eksploruj dzienniki śledzenia w usłudze Application Insights Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="98759-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="98759-117">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="98759-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="98759-118">Zapisać dane telemetryczne śledzenia niestandardowych</span><span class="sxs-lookup"><span data-stu-id="98759-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="98759-119">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="98759-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
