---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne dotyczące wyjątków | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne dotyczące wyjątków"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="eb0ad-103">Dane telemetryczne wyjątku: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="eb0ad-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="eb0ad-104">W [usługi Application Insights](app-insights-overview.md), obsługiwany lub nieobsługiwany wyjątek, który wystąpił podczas wykonywania aplikacji hello monitorowane reprezentuje wystąpienie wyjątku.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="eb0ad-105">Identyfikator problemu</span><span class="sxs-lookup"><span data-stu-id="eb0ad-105">Problem Id</span></span>

<span data-ttu-id="eb0ad-106">Identyfikator której hello Wystąpił wyjątek w kodzie.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="eb0ad-107">Używane do grupowania wyjątków.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-107">Used for exceptions grouping.</span></span> <span data-ttu-id="eb0ad-108">Zwykle połączenie typ wyjątku i funkcję hello stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="eb0ad-109">Maksymalna długość: 1024 znaki</span><span class="sxs-lookup"><span data-stu-id="eb0ad-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="eb0ad-110">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="eb0ad-110">Severity level</span></span>

<span data-ttu-id="eb0ad-111">Poziom ważności śledzenia.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-111">Trace severity level.</span></span> <span data-ttu-id="eb0ad-112">Wartość może być `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="eb0ad-113">Szczegóły wyjątku</span><span class="sxs-lookup"><span data-stu-id="eb0ad-113">Exception details</span></span>

<span data-ttu-id="eb0ad-114">(toobe rozszerzony)</span><span class="sxs-lookup"><span data-stu-id="eb0ad-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="eb0ad-115">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="eb0ad-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="eb0ad-116">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="eb0ad-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="eb0ad-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb0ad-117">Next steps</span></span>

- <span data-ttu-id="eb0ad-118">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="eb0ad-119">Dowiedz się, jak za[diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="eb0ad-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="eb0ad-120">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eb0ad-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
