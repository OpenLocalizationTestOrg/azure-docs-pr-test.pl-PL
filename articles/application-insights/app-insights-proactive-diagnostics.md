---
title: "Inteligentne wykrywania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Usługa Application Insights odbywa się szczegółowa analiza automatycznego dotyczących telemetrii aplikacji i ostrzega o potencjalnych problemach."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="5d108-103">Inteligentne wykrywanie w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="5d108-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="5d108-104">Inteligentne wykrywanie automatycznie ostrzega o potencjalnych problemów z wydajnością w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5d108-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="5d108-105">Wykonuje aktywnego analizy telemetrii, wysyłanej przez aplikację do [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d108-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5d108-106">Jeśli istnieje nagły wzrost awariami lub nietypowe wzorce wydajności serwera lub klienta, zostanie wyświetlony alert.</span><span class="sxs-lookup"><span data-stu-id="5d108-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="5d108-107">Ta funkcja wymaga żadnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5d108-107">This feature needs no configuration.</span></span> <span data-ttu-id="5d108-108">Działa on tak, jeśli aplikacja wyśle za mało danych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="5d108-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="5d108-109">Alerty o wykryciu inteligentne są dostępne zarówno z wiadomości e-mail, który pojawi się, jak i z bloku inteligentne wykrywania.</span><span class="sxs-lookup"><span data-stu-id="5d108-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="5d108-110">Zapoznaj się z zagrożeń wykrywanych przez usługę inteligentnego</span><span class="sxs-lookup"><span data-stu-id="5d108-110">Review your Smart Detections</span></span>
<span data-ttu-id="5d108-111">Może odnajdować wykryć na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="5d108-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="5d108-112">**Otrzymasz wiadomość e-mail** z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5d108-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="5d108-113">Oto typowy przykład:</span><span class="sxs-lookup"><span data-stu-id="5d108-113">Here's a typical example:</span></span>
  
    ![Alerty e-mail](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="5d108-115">Kliknij przycisk duży, aby otworzyć bardziej szczegółowo w portalu.</span><span class="sxs-lookup"><span data-stu-id="5d108-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="5d108-116">**Na kafelku inteligentne wykrywanie** na Omówienie aplikacji bloku pokazuje liczbę ostatnich alertów.</span><span class="sxs-lookup"><span data-stu-id="5d108-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="5d108-117">Kliknij Kafelek, aby wyświetlić listę ostatnich alertów.</span><span class="sxs-lookup"><span data-stu-id="5d108-117">Click the tile to see a list of recent alerts.</span></span>

![Wyświetl ostatnie wykryć](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="5d108-119">Wybierz alert, aby wyświetlić jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="5d108-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="5d108-120">Jakie problemy zostaną wykryte?</span><span class="sxs-lookup"><span data-stu-id="5d108-120">What problems are detected?</span></span>
<span data-ttu-id="5d108-121">Istnieją trzy typy wykrywania:</span><span class="sxs-lookup"><span data-stu-id="5d108-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="5d108-122">[Inteligentne wykrywania — błąd anomalii](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5d108-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="5d108-123">Używamy oczekiwana liczba nieudanych żądań dla aplikacji, ustaw uczenia maszynowego dopasowywanie obciążenia i innych czynników.</span><span class="sxs-lookup"><span data-stu-id="5d108-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="5d108-124">Jeśli współczynnik awaryjności odbędzie się poza oczekiwanym koperty, możemy wysyłać alert.</span><span class="sxs-lookup"><span data-stu-id="5d108-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="5d108-125">[Inteligentne wykrywania - anomalii wydajności](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5d108-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="5d108-126">Otrzymywać powiadomień, jeśli odpowiedź czas trwania operacji lub zależności jest spowolnieniem w porównaniu do linii bazowej historyczne lub nazywamy nietypowych wzorca w czasie odpowiedzi lub czas ładowania strony.</span><span class="sxs-lookup"><span data-stu-id="5d108-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="5d108-127">[Inteligentne wykrywania — problemy z usługą w chmurze Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="5d108-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="5d108-128">Uzyskiwanie alertów, jeśli aplikacja jest hostowana w usług Azure Cloud Services i wystąpienia roli ma uruchamianiem, często odtwarzania lub awarie środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="5d108-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="5d108-129">(Łącza pomocy Każde powiadomienie prowadzą do odpowiednich artykułów.)</span><span class="sxs-lookup"><span data-stu-id="5d108-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="5d108-130">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="5d108-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="5d108-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d108-131">Next steps</span></span>
<span data-ttu-id="5d108-132">Te narzędzia diagnostyczne pomóc sprawdzić dane telemetryczne z aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5d108-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="5d108-133">Eksplorator metryk</span><span class="sxs-lookup"><span data-stu-id="5d108-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="5d108-134">Eksplorator wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="5d108-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="5d108-135">Analiza - język zaawansowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="5d108-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="5d108-136">Wykrywanie inteligentne jest całkowicie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="5d108-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="5d108-137">A może chcesz skonfigurować niektóre alerty więcej?</span><span class="sxs-lookup"><span data-stu-id="5d108-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="5d108-138">Ręcznie skonfigurowanej metryki alertów</span><span class="sxs-lookup"><span data-stu-id="5d108-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="5d108-139">Dostępność testy sieci web</span><span class="sxs-lookup"><span data-stu-id="5d108-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

