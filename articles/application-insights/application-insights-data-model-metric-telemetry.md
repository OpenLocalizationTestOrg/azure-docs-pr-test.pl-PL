---
title: "Model danych Telemetrii Insights aplikacji Azure — dane telemetryczne metryki | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne metryki"
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="e43ac-103">Dane telemetryczne metryki: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e43ac-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="e43ac-104">Istnieją dwa typy dane telemetryczne metryki obsługiwane przez [usługi Application Insights](app-insights-overview.md): pojedyncze pomiaru i wstępnie zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="e43ac-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="e43ac-105">Pojedynczego pomiaru jest po prostu nazw i wartości.</span><span class="sxs-lookup"><span data-stu-id="e43ac-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="e43ac-106">Metryka wstępnie zagregowane określa minimalną i maksymalną wartość metryki interwał agregacji i odchylenie standardowe go.</span><span class="sxs-lookup"><span data-stu-id="e43ac-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="e43ac-107">Wstępnie zagregowane dane telemetryczne metryki zakłada tego okresu agregacji został jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="e43ac-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="e43ac-108">Istnieje kilka dobrze znane nazwy metryki obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e43ac-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="e43ac-109">Metryka reprezentujący liczniki systemu i procesu:</span><span class="sxs-lookup"><span data-stu-id="e43ac-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="e43ac-110">**Nazwa platformy .NET**</span><span class="sxs-lookup"><span data-stu-id="e43ac-110">**.NET name**</span></span>             | <span data-ttu-id="e43ac-111">**Nazwa o niesprecyzowanym platformy**</span><span class="sxs-lookup"><span data-stu-id="e43ac-111">**Platform agnostic name**</span></span> | <span data-ttu-id="e43ac-112">**Nazwa interfejsu API REST**</span><span class="sxs-lookup"><span data-stu-id="e43ac-112">**REST API name**</span></span> | <span data-ttu-id="e43ac-113">**Opis**</span><span class="sxs-lookup"><span data-stu-id="e43ac-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="e43ac-114">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-114">Work in progress...</span></span> | [<span data-ttu-id="e43ac-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="e43ac-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="e43ac-116">Łączna liczba procesorów maszyny</span><span class="sxs-lookup"><span data-stu-id="e43ac-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="e43ac-117">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-117">Work in progress...</span></span> | [<span data-ttu-id="e43ac-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="e43ac-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="e43ac-119">ilość pamięci dostępnej na dysku</span><span class="sxs-lookup"><span data-stu-id="e43ac-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="e43ac-120">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-120">Work in progress...</span></span> | [<span data-ttu-id="e43ac-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="e43ac-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="e43ac-122">Procesor CPU procesu hostingu aplikacji</span><span class="sxs-lookup"><span data-stu-id="e43ac-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="e43ac-123">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-123">Work in progress...</span></span> | [<span data-ttu-id="e43ac-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="e43ac-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="e43ac-125">pamięci używanej przez proces obsługujący aplikacji</span><span class="sxs-lookup"><span data-stu-id="e43ac-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="e43ac-126">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-126">Work in progress...</span></span> | [<span data-ttu-id="e43ac-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e43ac-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="e43ac-128">Liczba operacji We/Wy jest uruchamiana za procesu hostingu aplikacji</span><span class="sxs-lookup"><span data-stu-id="e43ac-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="e43ac-129">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-129">Work in progress...</span></span> | [<span data-ttu-id="e43ac-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="e43ac-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="e43ac-131">Liczba żądań przetworzonych przez aplikację</span><span class="sxs-lookup"><span data-stu-id="e43ac-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="e43ac-132">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-132">Work in progress...</span></span> | [<span data-ttu-id="e43ac-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="e43ac-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="e43ac-134">Liczba wyjątków zgłoszonych przez aplikację</span><span class="sxs-lookup"><span data-stu-id="e43ac-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="e43ac-135">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-135">Work in progress...</span></span> | [<span data-ttu-id="e43ac-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="e43ac-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="e43ac-137">Średnia liczba żądań czasu wykonywania</span><span class="sxs-lookup"><span data-stu-id="e43ac-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="e43ac-138">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="e43ac-138">Work in progress...</span></span> | [<span data-ttu-id="e43ac-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="e43ac-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="e43ac-140">Liczba żądań oczekujących do przetworzenia w kolejce</span><span class="sxs-lookup"><span data-stu-id="e43ac-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="e43ac-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e43ac-141">Name</span></span>

<span data-ttu-id="e43ac-142">Nazwa metryki, które chcesz zobaczyć w portalu usługi Application Insights i interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e43ac-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="e43ac-143">Wartość</span><span class="sxs-lookup"><span data-stu-id="e43ac-143">Value</span></span>

<span data-ttu-id="e43ac-144">Pojedynczej wartości miary.</span><span class="sxs-lookup"><span data-stu-id="e43ac-144">Single value for measurement.</span></span> <span data-ttu-id="e43ac-145">Suma poszczególnych pomiarów podczas agregacji.</span><span class="sxs-lookup"><span data-stu-id="e43ac-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="e43ac-146">Licznik</span><span class="sxs-lookup"><span data-stu-id="e43ac-146">Count</span></span>

<span data-ttu-id="e43ac-147">Waga metryki zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="e43ac-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="e43ac-148">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="e43ac-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="e43ac-149">Min</span><span class="sxs-lookup"><span data-stu-id="e43ac-149">Min</span></span>

<span data-ttu-id="e43ac-150">Minimalna wartość zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="e43ac-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="e43ac-151">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="e43ac-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="e43ac-152">Maks.</span><span class="sxs-lookup"><span data-stu-id="e43ac-152">Max</span></span>

<span data-ttu-id="e43ac-153">Maksymalna wartość zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="e43ac-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="e43ac-154">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="e43ac-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="e43ac-155">Odchylenie standardowe</span><span class="sxs-lookup"><span data-stu-id="e43ac-155">Standard deviation</span></span>

<span data-ttu-id="e43ac-156">Odchylenie standardowe zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="e43ac-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="e43ac-157">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="e43ac-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="e43ac-158">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="e43ac-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="e43ac-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e43ac-159">Next steps</span></span>

- <span data-ttu-id="e43ac-160">Dowiedz się, jak używać [aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="e43ac-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="e43ac-161">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e43ac-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="e43ac-162">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e43ac-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
