---
title: "aaaSmart wykrywania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="a139b-103">Inteligentne wykrywanie w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="a139b-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="a139b-104">Inteligentne wykrywanie automatycznie ostrzega o potencjalnych problemów z wydajnością w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a139b-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="a139b-105">Wykonuje aktywnego analizy aplikacji zbyt wysyła dane telemetryczne hello[usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a139b-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a139b-106">Jeśli istnieje nagły wzrost awariami lub nietypowe wzorce wydajności serwera lub klienta, zostanie wyświetlony alert.</span><span class="sxs-lookup"><span data-stu-id="a139b-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="a139b-107">Ta funkcja wymaga żadnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a139b-107">This feature needs no configuration.</span></span> <span data-ttu-id="a139b-108">Działa on tak, jeśli aplikacja wyśle za mało danych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="a139b-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="a139b-109">Alerty o wykryciu inteligentne mogą dostęp zarówno z hello wiadomości e-mail, które otrzymujesz i za pomocą bloku inteligentne wykrywanie hello.</span><span class="sxs-lookup"><span data-stu-id="a139b-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="a139b-110">Zapoznaj się z zagrożeń wykrywanych przez usługę inteligentnego</span><span class="sxs-lookup"><span data-stu-id="a139b-110">Review your Smart Detections</span></span>
<span data-ttu-id="a139b-111">Może odnajdować wykryć na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="a139b-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="a139b-112">**Otrzymasz wiadomość e-mail** z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a139b-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="a139b-113">Oto typowy przykład:</span><span class="sxs-lookup"><span data-stu-id="a139b-113">Here's a typical example:</span></span>
  
    ![Alerty e-mail](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="a139b-115">Kliknij przycisk tooopen duży przycisk hello bardziej szczegółowo w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a139b-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="a139b-116">**Kafelek inteligentne wykrywanie Hello** na Omówienie aplikacji bloku pokazuje liczbę ostatnich alertów.</span><span class="sxs-lookup"><span data-stu-id="a139b-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="a139b-117">Kliknij przycisk toosee kafelka hello listę ostatnich alertów.</span><span class="sxs-lookup"><span data-stu-id="a139b-117">Click hello tile toosee a list of recent alerts.</span></span>

![Wyświetl ostatnie wykryć](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="a139b-119">Wybierz alert toosee jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="a139b-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="a139b-120">Jakie problemy zostaną wykryte?</span><span class="sxs-lookup"><span data-stu-id="a139b-120">What problems are detected?</span></span>
<span data-ttu-id="a139b-121">Istnieją trzy typy wykrywania:</span><span class="sxs-lookup"><span data-stu-id="a139b-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="a139b-122">[Inteligentne wykrywania — błąd anomalii](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a139b-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="a139b-123">Używamy uczenia maszynowego tooset hello oczekiwano liczba nieudanych żądań dla aplikacji, dopasowywanie obciążenia i innych czynników.</span><span class="sxs-lookup"><span data-stu-id="a139b-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="a139b-124">Jeśli częstość niepowodzeń hello odbędzie się poza oczekiwanym koperty hello, możemy wysyłać alert.</span><span class="sxs-lookup"><span data-stu-id="a139b-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="a139b-125">[Inteligentne wykrywania - anomalii wydajności](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a139b-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="a139b-126">Otrzymywać powiadomień, jeśli odpowiedź czas trwania operacji lub zależności jest spowolnieniem porównaniu toohistorical linii bazowej lub nazywamy nietypowych wzorca w czasie odpowiedzi lub czas ładowania strony.</span><span class="sxs-lookup"><span data-stu-id="a139b-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="a139b-127">[Inteligentne wykrywania — problemy z usługą w chmurze Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="a139b-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="a139b-128">Uzyskiwanie alertów, jeśli aplikacja jest hostowana w usług Azure Cloud Services i wystąpienia roli ma uruchamianiem, często odtwarzania lub awarie środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="a139b-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="a139b-129">(łącza pomocy hello Każde powiadomienie przejście odpowiednich artykułów toohello.)</span><span class="sxs-lookup"><span data-stu-id="a139b-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="a139b-130">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="a139b-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="a139b-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a139b-131">Next steps</span></span>
<span data-ttu-id="a139b-132">Te narzędzia diagnostyczne pomóc sprawdzić telemetrii hello z aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a139b-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="a139b-133">Eksplorator metryk</span><span class="sxs-lookup"><span data-stu-id="a139b-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="a139b-134">Eksplorator wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="a139b-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a139b-135">Analiza - język zaawansowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="a139b-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="a139b-136">Wykrywanie inteligentne jest całkowicie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="a139b-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="a139b-137">A może chcesz tooset niektóre alerty więcej?</span><span class="sxs-lookup"><span data-stu-id="a139b-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="a139b-138">Ręcznie skonfigurowanej metryki alertów</span><span class="sxs-lookup"><span data-stu-id="a139b-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="a139b-139">Dostępność testy sieci web</span><span class="sxs-lookup"><span data-stu-id="a139b-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

