---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne zależności | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne zależności"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="67e36-103">Dane telemetryczne zależności: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="67e36-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="67e36-104">Dane telemetryczne zależności (w [usługi Application Insights](app-insights-overview.md)) reprezentuje interakcji składnika hello monitorować za pomocą składnika zdalnego, takich jak SQL lub punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="67e36-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="67e36-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="67e36-105">Name</span></span>

<span data-ttu-id="67e36-106">Nazwa polecenia hello inicjowane z tego wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="67e36-107">Wartość Kardynalność niski.</span><span class="sxs-lookup"><span data-stu-id="67e36-107">Low cardinality value.</span></span> <span data-ttu-id="67e36-108">Przykłady są nazwa procedury składowanej i szablon ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="67e36-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="67e36-109">ID</span><span class="sxs-lookup"><span data-stu-id="67e36-109">ID</span></span>

<span data-ttu-id="67e36-110">Identyfikator wystąpienia wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="67e36-111">Używane na potrzeby korelacji z elementem dane telemetryczne żądania hello odpowiadającego toothis wywołanie zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="67e36-112">Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.</span><span class="sxs-lookup"><span data-stu-id="67e36-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="67e36-113">Dane</span><span class="sxs-lookup"><span data-stu-id="67e36-113">Data</span></span>

<span data-ttu-id="67e36-114">Polecenia inicjowane przez wywołanie zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="67e36-115">Przykłady są instrukcji SQL i adres URL protokołu HTTP z wszystkie parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="67e36-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="67e36-116">Typ</span><span class="sxs-lookup"><span data-stu-id="67e36-116">Type</span></span>

<span data-ttu-id="67e36-117">Nazwa typu zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-117">Dependency type name.</span></span> <span data-ttu-id="67e36-118">Kardynalność niskiej wartości logiczne grupowanie zależności i interpretacji innych pól, takich jak commandName i resultCode.</span><span class="sxs-lookup"><span data-stu-id="67e36-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="67e36-119">Przykłady są SQL, tabeli platformy Azure i HTTP.</span><span class="sxs-lookup"><span data-stu-id="67e36-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="67e36-120">docelowy</span><span class="sxs-lookup"><span data-stu-id="67e36-120">Target</span></span>

<span data-ttu-id="67e36-121">Lokacji docelowej wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-121">Target site of a dependency call.</span></span> <span data-ttu-id="67e36-122">Przykłady to nazwa serwera, adres hosta.</span><span class="sxs-lookup"><span data-stu-id="67e36-122">Examples are server name, host address.</span></span> <span data-ttu-id="67e36-123">Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.</span><span class="sxs-lookup"><span data-stu-id="67e36-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="67e36-124">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="67e36-124">Duration</span></span>

<span data-ttu-id="67e36-125">Żądaj czasu trwania w formacie: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="67e36-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="67e36-126">Musi być mniejsza niż `1000` dni.</span><span class="sxs-lookup"><span data-stu-id="67e36-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="67e36-127">Kod wyniku</span><span class="sxs-lookup"><span data-stu-id="67e36-127">Result code</span></span>

<span data-ttu-id="67e36-128">Kod wyniku wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="67e36-128">Result code of a dependency call.</span></span> <span data-ttu-id="67e36-129">Przykłady to kod błędu SQL oraz kod stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="67e36-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="67e36-130">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="67e36-130">Success</span></span>

<span data-ttu-id="67e36-131">Oznaczenia wywołanie powiodła się czy nie.</span><span class="sxs-lookup"><span data-stu-id="67e36-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="67e36-132">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="67e36-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="67e36-133">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="67e36-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="67e36-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67e36-134">Next steps</span></span>

- <span data-ttu-id="67e36-135">Konfigurowanie śledzenia dla zależności [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="67e36-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="67e36-136">Konfigurowanie śledzenia dla zależności [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="67e36-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="67e36-137">Zapisać dane telemetryczne zależności niestandardowych</span><span class="sxs-lookup"><span data-stu-id="67e36-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="67e36-138">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="67e36-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="67e36-139">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="67e36-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
