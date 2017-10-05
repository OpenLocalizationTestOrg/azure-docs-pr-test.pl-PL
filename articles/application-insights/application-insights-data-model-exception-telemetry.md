---
title: "Model danych Telemetrii aplikacji Azure Insights — dane telemetryczne dotyczące wyjątków | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="d1ab4-103">Dane telemetryczne wyjątku: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1ab4-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="d1ab4-104">W [usługi Application Insights](app-insights-overview.md), wystąpienie wyjątku reprezentuje obsłużonych i nieobsłużonych wyjątków, który wystąpił podczas wykonywania monitorowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="d1ab4-105">Identyfikator problemu</span><span class="sxs-lookup"><span data-stu-id="d1ab4-105">Problem Id</span></span>

<span data-ttu-id="d1ab4-106">Identyfikator, gdy wyjątek został zgłoszony w kodzie.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="d1ab4-107">Używane do grupowania wyjątków.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-107">Used for exceptions grouping.</span></span> <span data-ttu-id="d1ab4-108">Zwykle połączenie typ wyjątku i funkcję ze stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="d1ab4-109">Maksymalna długość: 1024 znaki</span><span class="sxs-lookup"><span data-stu-id="d1ab4-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="d1ab4-110">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="d1ab4-110">Severity level</span></span>

<span data-ttu-id="d1ab4-111">Poziom ważności śledzenia.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-111">Trace severity level.</span></span> <span data-ttu-id="d1ab4-112">Wartość może być `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="d1ab4-113">Szczegóły wyjątku</span><span class="sxs-lookup"><span data-stu-id="d1ab4-113">Exception details</span></span>

<span data-ttu-id="d1ab4-114">(Aby rozszerzony)</span><span class="sxs-lookup"><span data-stu-id="d1ab4-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="d1ab4-115">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="d1ab4-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="d1ab4-116">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="d1ab4-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="d1ab4-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1ab4-117">Next steps</span></span>

- <span data-ttu-id="d1ab4-118">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="d1ab4-119">Dowiedz się, jak [diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="d1ab4-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="d1ab4-120">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d1ab4-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
