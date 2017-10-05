---
title: "Model danych Telemetrii Insights aplikacji Azure — dane telemetryczne zależności | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="61fd8-103">Dane telemetryczne zależności: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="61fd8-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="61fd8-104">Dane telemetryczne zależności (w [usługi Application Insights](app-insights-overview.md)) reprezentuje interakcji monitorowanego składnika zdalnego składnika, takiego jak SQL lub punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="61fd8-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="61fd8-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61fd8-105">Name</span></span>

<span data-ttu-id="61fd8-106">Nazwa polecenia inicjowane z tego wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="61fd8-107">Wartość Kardynalność niski.</span><span class="sxs-lookup"><span data-stu-id="61fd8-107">Low cardinality value.</span></span> <span data-ttu-id="61fd8-108">Przykłady są nazwa procedury składowanej i szablon ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="61fd8-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="61fd8-109">ID</span><span class="sxs-lookup"><span data-stu-id="61fd8-109">ID</span></span>

<span data-ttu-id="61fd8-110">Identyfikator wystąpienia wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="61fd8-111">Używane na potrzeby korelacji z elementem dane telemetryczne żądania odpowiadające wywołanie zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="61fd8-112">Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.</span><span class="sxs-lookup"><span data-stu-id="61fd8-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="61fd8-113">Dane</span><span class="sxs-lookup"><span data-stu-id="61fd8-113">Data</span></span>

<span data-ttu-id="61fd8-114">Polecenia inicjowane przez wywołanie zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="61fd8-115">Przykłady są instrukcji SQL i adres URL protokołu HTTP z wszystkie parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="61fd8-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="61fd8-116">Typ</span><span class="sxs-lookup"><span data-stu-id="61fd8-116">Type</span></span>

<span data-ttu-id="61fd8-117">Nazwa typu zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-117">Dependency type name.</span></span> <span data-ttu-id="61fd8-118">Kardynalność niskiej wartości logiczne grupowanie zależności i interpretacji innych pól, takich jak commandName i resultCode.</span><span class="sxs-lookup"><span data-stu-id="61fd8-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="61fd8-119">Przykłady są SQL, tabeli platformy Azure i HTTP.</span><span class="sxs-lookup"><span data-stu-id="61fd8-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="61fd8-120">docelowy</span><span class="sxs-lookup"><span data-stu-id="61fd8-120">Target</span></span>

<span data-ttu-id="61fd8-121">Lokacji docelowej wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-121">Target site of a dependency call.</span></span> <span data-ttu-id="61fd8-122">Przykłady to nazwa serwera, adres hosta.</span><span class="sxs-lookup"><span data-stu-id="61fd8-122">Examples are server name, host address.</span></span> <span data-ttu-id="61fd8-123">Aby uzyskać więcej informacji, zobacz [korelacji](application-insights-correlation.md) strony.</span><span class="sxs-lookup"><span data-stu-id="61fd8-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="61fd8-124">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="61fd8-124">Duration</span></span>

<span data-ttu-id="61fd8-125">Żądaj czasu trwania w formacie: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="61fd8-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="61fd8-126">Musi być mniejsza niż `1000` dni.</span><span class="sxs-lookup"><span data-stu-id="61fd8-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="61fd8-127">Kod wyniku</span><span class="sxs-lookup"><span data-stu-id="61fd8-127">Result code</span></span>

<span data-ttu-id="61fd8-128">Kod wyniku wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="61fd8-128">Result code of a dependency call.</span></span> <span data-ttu-id="61fd8-129">Przykłady to kod błędu SQL oraz kod stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="61fd8-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="61fd8-130">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="61fd8-130">Success</span></span>

<span data-ttu-id="61fd8-131">Oznaczenia wywołanie powiodła się czy nie.</span><span class="sxs-lookup"><span data-stu-id="61fd8-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="61fd8-132">Właściwości niestandardowe</span><span class="sxs-lookup"><span data-stu-id="61fd8-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="61fd8-133">Miar niestandardowych</span><span class="sxs-lookup"><span data-stu-id="61fd8-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="61fd8-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61fd8-134">Next steps</span></span>

- <span data-ttu-id="61fd8-135">Konfigurowanie śledzenia dla zależności [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="61fd8-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="61fd8-136">Konfigurowanie śledzenia dla zależności [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="61fd8-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="61fd8-137">Zapisać dane telemetryczne zależności niestandardowych</span><span class="sxs-lookup"><span data-stu-id="61fd8-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="61fd8-138">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61fd8-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="61fd8-139">Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61fd8-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
