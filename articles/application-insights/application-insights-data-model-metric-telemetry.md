---
title: aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne metryki | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="ce169-103">Dane telemetryczne metryki: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ce169-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="ce169-104">Istnieją dwa typy dane telemetryczne metryki obsługiwane przez [usługi Application Insights](app-insights-overview.md): pojedyncze pomiaru i wstępnie zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="ce169-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="ce169-105">Pojedynczego pomiaru jest po prostu nazw i wartości.</span><span class="sxs-lookup"><span data-stu-id="ce169-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="ce169-106">Metryka wstępnie zagregowane określa minimalną i maksymalną wartość metryki hello w interwał agregacji hello i odchylenie standardowe go.</span><span class="sxs-lookup"><span data-stu-id="ce169-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="ce169-107">Wstępnie zagregowane dane telemetryczne metryki zakłada tego okresu agregacji został jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="ce169-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="ce169-108">Istnieje kilka dobrze znane nazwy metryki obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce169-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="ce169-109">Metryka reprezentujący liczniki systemu i procesu:</span><span class="sxs-lookup"><span data-stu-id="ce169-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="ce169-110">**Nazwa platformy .NET**</span><span class="sxs-lookup"><span data-stu-id="ce169-110">**.NET name**</span></span>             | <span data-ttu-id="ce169-111">**Nazwa o niesprecyzowanym platformy**</span><span class="sxs-lookup"><span data-stu-id="ce169-111">**Platform agnostic name**</span></span> | <span data-ttu-id="ce169-112">**Nazwa interfejsu API REST**</span><span class="sxs-lookup"><span data-stu-id="ce169-112">**REST API name**</span></span> | <span data-ttu-id="ce169-113">**Opis**</span><span class="sxs-lookup"><span data-stu-id="ce169-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="ce169-114">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-114">Work in progress...</span></span> | [<span data-ttu-id="ce169-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="ce169-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="ce169-116">Łączna liczba procesorów maszyny</span><span class="sxs-lookup"><span data-stu-id="ce169-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="ce169-117">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-117">Work in progress...</span></span> | [<span data-ttu-id="ce169-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="ce169-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="ce169-119">ilość pamięci dostępnej na dysku</span><span class="sxs-lookup"><span data-stu-id="ce169-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="ce169-120">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-120">Work in progress...</span></span> | [<span data-ttu-id="ce169-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="ce169-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="ce169-122">Procesor CPU hello procesu hostingu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="ce169-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="ce169-123">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-123">Work in progress...</span></span> | [<span data-ttu-id="ce169-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="ce169-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="ce169-125">Pamięć używana przez proces hello hosting aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="ce169-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="ce169-126">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-126">Work in progress...</span></span> | [<span data-ttu-id="ce169-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="ce169-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="ce169-128">Liczba operacji We/Wy jest uruchamiana za procesu hostingu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="ce169-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="ce169-129">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-129">Work in progress...</span></span> | [<span data-ttu-id="ce169-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="ce169-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="ce169-131">Liczba żądań przetworzonych przez aplikację</span><span class="sxs-lookup"><span data-stu-id="ce169-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="ce169-132">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-132">Work in progress...</span></span> | [<span data-ttu-id="ce169-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="ce169-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="ce169-134">Liczba wyjątków zgłoszonych przez aplikację</span><span class="sxs-lookup"><span data-stu-id="ce169-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="ce169-135">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-135">Work in progress...</span></span> | [<span data-ttu-id="ce169-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="ce169-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="ce169-137">Średnia liczba żądań czasu wykonywania</span><span class="sxs-lookup"><span data-stu-id="ce169-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="ce169-138">Praca w toku...</span><span class="sxs-lookup"><span data-stu-id="ce169-138">Work in progress...</span></span> | [<span data-ttu-id="ce169-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="ce169-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="ce169-140">Liczba żądań oczekujących na powitania przetwarzania w kolejce</span><span class="sxs-lookup"><span data-stu-id="ce169-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="ce169-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ce169-141">Name</span></span>

<span data-ttu-id="ce169-142">Nazwa metryki hello chcesz toosee w portalu usługi Application Insights i interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce169-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="ce169-143">Wartość</span><span class="sxs-lookup"><span data-stu-id="ce169-143">Value</span></span>

<span data-ttu-id="ce169-144">Pojedynczej wartości miary.</span><span class="sxs-lookup"><span data-stu-id="ce169-144">Single value for measurement.</span></span> <span data-ttu-id="ce169-145">Suma poszczególnych pomiarów hello agregacji.</span><span class="sxs-lookup"><span data-stu-id="ce169-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="ce169-146">Licznik</span><span class="sxs-lookup"><span data-stu-id="ce169-146">Count</span></span>

<span data-ttu-id="ce169-147">Waga metryki hello zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="ce169-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="ce169-148">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="ce169-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="ce169-149">Min</span><span class="sxs-lookup"><span data-stu-id="ce169-149">Min</span></span>

<span data-ttu-id="ce169-150">Minimalna wartość metryki hello agregowane.</span><span class="sxs-lookup"><span data-stu-id="ce169-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="ce169-151">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="ce169-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="ce169-152">Maks.</span><span class="sxs-lookup"><span data-stu-id="ce169-152">Max</span></span>

<span data-ttu-id="ce169-153">Maksymalna wartość metryki hello agregowane.</span><span class="sxs-lookup"><span data-stu-id="ce169-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="ce169-154">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="ce169-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="ce169-155">Odchylenie standardowe</span><span class="sxs-lookup"><span data-stu-id="ce169-155">Standard deviation</span></span>

<span data-ttu-id="ce169-156">Odchylenie standardowe hello zagregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="ce169-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="ce169-157">Nie powinien mieć ustawionej dla miary.</span><span class="sxs-lookup"><span data-stu-id="ce169-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="ce169-158">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="ce169-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="ce169-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce169-159">Next steps</span></span>

- <span data-ttu-id="ce169-160">Dowiedz się, jak toouse [aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="ce169-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="ce169-161">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce169-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="ce169-162">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce169-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
