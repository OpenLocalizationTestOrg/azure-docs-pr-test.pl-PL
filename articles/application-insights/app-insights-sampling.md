---
title: "Próbkowanie danych telemetrii w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Jak zapewnić ilość danych telemetrycznych pod kontrolą."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="be939-103">Próbkowanie w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="be939-103">Sampling in Application Insights</span></span>


<span data-ttu-id="be939-104">Próbkowanie to funkcja [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be939-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="be939-105">Jest zalecanym sposobem ograniczenia ruchu danych telemetrycznych i magazynu, zachowując statystycznie prawidłową analizy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be939-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="be939-106">Filtr wybiera elementy, które są powiązane, dzięki czemu można przechodzić między elementami podczas wykonywania badań diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="be939-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="be939-107">Gdy metryki liczby są prezentowane w portalu, są one renormalized w celu uwzględnienia pobierania próbek, aby zminimalizować wpływ na statystyki.</span><span class="sxs-lookup"><span data-stu-id="be939-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="be939-108">Próbkowania powoduje zmniejszenie kosztów ruchu i dane i pomaga uniknąć ograniczania.</span><span class="sxs-lookup"><span data-stu-id="be939-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="be939-109">Krótko mówiąc:</span><span class="sxs-lookup"><span data-stu-id="be939-109">In brief:</span></span>
* <span data-ttu-id="be939-110">Próbkowanie zachowuje 1 w  *n*  rejestruje i odrzuca wszystkie pozostałe.</span><span class="sxs-lookup"><span data-stu-id="be939-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="be939-111">Na przykład mogą go zachować zdarzenia 1 do 5, częstotliwość próbkowania, 20%.</span><span class="sxs-lookup"><span data-stu-id="be939-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="be939-112">Próbkowanie odbywa się automatycznie, jeśli aplikacja wyśle dużej ilości danych telemetrii, w aplikacji serwera sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be939-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="be939-113">Można również ustawić próbkowania ręcznie, albo w portalu na stronie cen; lub w zestawie SDK platformy ASP.NET w pliku .config, aby również zmniejszenie ruchu w sieci.</span><span class="sxs-lookup"><span data-stu-id="be939-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="be939-114">Jeśli dziennika zdarzeń niestandardowych, należy się upewnić, że zestaw zdarzeń jest zatrzymany lub odrzucone razem upewnij się, że mają one taką samą wartość OperationId.</span><span class="sxs-lookup"><span data-stu-id="be939-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="be939-115">Dzielnik próbkowania  *n*  jest zgłaszany we wszystkich rekordach we właściwości `itemCount`, w wyszukiwaniu widocznego pod przyjazną nazwą "liczbę żądań" lub "liczba zdarzeń".</span><span class="sxs-lookup"><span data-stu-id="be939-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="be939-116">Podczas pobierania próbek nie jest w operacji `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="be939-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="be939-117">Jeśli piszesz zapytania analityczne, [uwzględnienia próbkowania](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="be939-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="be939-118">W szczególności, zamiast po prostu zliczanie rekordów, należy użyć `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="be939-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="be939-119">Typy pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="be939-119">Types of sampling</span></span>
<span data-ttu-id="be939-120">Istnieją trzy metody alternatywne próbkowania:</span><span class="sxs-lookup"><span data-stu-id="be939-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="be939-121">**Próbkowanie adaptacyjną** automatycznie dostosowuje ilość danych telemetrycznych wysłanych z zestawu SDK w aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be939-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="be939-122">Domyślnie z 2.0.0-beta3 v zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="be939-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="be939-123">Obecnie dostępne dla platformy ASP.NET tylko telemetrii po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="be939-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="be939-124">**Próbkowanie stałej stawki** zmniejsza ilość danych telemetrycznych wysłanych z serwera programu ASP.NET oraz z przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be939-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="be939-125">Możesz ustawić częstotliwość.</span><span class="sxs-lookup"><span data-stu-id="be939-125">You set the rate.</span></span> <span data-ttu-id="be939-126">Klient i serwer będzie synchronizować ich próbkowania tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.</span><span class="sxs-lookup"><span data-stu-id="be939-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="be939-127">**Wprowadzanie próbkowania** działa w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="be939-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="be939-128">Odrzuca niektóre dane telemetryczne, przychodzący z aplikacji, z szybkością ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="be939-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="be939-129">Nie zmniejszenie ruchu telemetrii, ale pomaga zachować w wykorzystaniu całego przydziału miesięcznego.</span><span class="sxs-lookup"><span data-stu-id="be939-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="be939-130">Duży zaletą wprowadzanie próbkowania jest bez ponownego wdrażania aplikacji można ją ustawić, czy działa on jednakowo do wszystkich serwerów i klientów.</span><span class="sxs-lookup"><span data-stu-id="be939-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="be939-131">W przypadku adaptacyjną lub stała częstotliwość próbkowania w operacji, wprowadzanie próbek jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="be939-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="be939-132">Wprowadzanie próbkowania</span><span class="sxs-lookup"><span data-stu-id="be939-132">Ingestion sampling</span></span>
<span data-ttu-id="be939-133">Ta forma pobierania próbek działa w momencie, gdy dane telemetryczne z serwera sieci web, przeglądarki i urządzenia osiąga punkt końcowy usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="be939-134">Chociaż nie redukują ruchu danych telemetrycznych wysłanych z aplikacji, Zmniejsz rozmiar przetwarzane i przechowywane (i naliczona opłata za) przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="be939-135">Użyj tego typu próbkowania, jeśli aplikacja często przechodzi przez jego przydział miesięczny, a nie ma możliwości użycia jednej z tego zestawu SDK typu próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="be939-136">Ustaw częstotliwość próbkowania w przydziały i cenach bloku:</span><span class="sxs-lookup"><span data-stu-id="be939-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![W bloku Omówienie aplikacji kliknij ustawienia, przydział, próbek, a następnie wybierz częstotliwość próbkowania, a następnie kliknij przycisk Aktualizuj.](./media/app-insights-sampling/04.png)

<span data-ttu-id="be939-138">Podobnie jak inne rodzaje próbkowania algorytm zachowuje elementy powiązane dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="be939-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="be939-139">Na przykład gdy jest sprawdzanie telemetrii w wyszukiwania, będziesz mieć możliwość odnaleźć żądania dotyczące określonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="be939-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="be939-140">Metryka liczby takich jak liczby żądań i szybkość wyjątek poprawnie zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="be939-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="be939-141">Punkty danych, które są odrzucane przez pobieranie próbek nie są dostępne w dowolnej funkcji usługi Application Insights, takich jak [eksportu ciągłego](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="be939-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="be939-142">Wprowadzanie próbkowania nie działa podczas operacji SDK próbkowania adaptacyjną lub stałej stawki.</span><span class="sxs-lookup"><span data-stu-id="be939-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="be939-143">Jeśli częstotliwość próbkowania w zestawie SDK jest mniejsza niż 100%, częstotliwość próbkowania wprowadzanie ustawiona jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="be939-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="be939-144">Wartości wyświetlane na kafelku określa wartość, która zostanie ustawiona wprowadzanie próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="be939-145">Jeśli jest używany w operacji pobierania zestawu SDK nie reprezentuje rzeczywistego próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="be939-146">Adaptacyjną próbkowania na serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="be939-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="be939-147">Adaptacyjną próbkowania jest dostępna dla aplikacji Insights zestawu SDK dla platformy ASP.NET v 2.0.0-beta3 i nowszych i jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="be939-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="be939-148">Próbkowanie adaptacyjną wpływa na ilość danych telemetrycznych wysłanych z aplikacji serwera sieci web usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="be939-149">Wolumin zostanie automatycznie dopasowana do pozostać w określonym maksymalna szybkość ruchu.</span><span class="sxs-lookup"><span data-stu-id="be939-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="be939-150">Go nie działa niewielki dane telemetryczne, więc w debugowaniu aplikacji lub witryny sieci Web z użyciem niski nie będzie to mieć wpływ na.</span><span class="sxs-lookup"><span data-stu-id="be939-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="be939-151">Uzyskanie wolumin docelowy, niektóre dane telemetryczne, generowane jest pomijany.</span><span class="sxs-lookup"><span data-stu-id="be939-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="be939-152">Zachowując podobnie jak inne rodzaje próbkowania algorytm elementy powiązane dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="be939-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="be939-153">Na przykład gdy jest sprawdzanie telemetrii w wyszukiwania, będziesz mieć możliwość odnaleźć żądania dotyczące określonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="be939-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="be939-154">Metryka liczby takich jak liczby żądań i szybkość wyjątek są dostosowane do kompensacji próbkowania, tak aby pokazywały około poprawne wartości w Eksploratorze metryki.</span><span class="sxs-lookup"><span data-stu-id="be939-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="be939-155">**Aktualizacja projektu NuGet** pakietów do najnowszej wersji *wersji wstępnej* wersji usługi Application Insights: kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Include wstępna** i wyszukaj Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="be939-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="be939-156">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), można dostosować kilku parametrów w `AdaptiveSamplingTelemetryProcessor` węzła.</span><span class="sxs-lookup"><span data-stu-id="be939-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="be939-157">Dane pokazywane są wartościami domyślnymi:</span><span class="sxs-lookup"><span data-stu-id="be939-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="be939-158">Docelowy szybkość, z której ma adaptacyjną algorytmu dla **na każdym hoście serwera**.</span><span class="sxs-lookup"><span data-stu-id="be939-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="be939-159">Jeśli aplikacja sieci web jest uruchomiony na wielu hostach, zmniejsz tę wartość tak, aby pozostają w szybkość docelowy ruchu w portalu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="be939-160">Interwał, jaką jest ponownie oceniane bieżącej szybkości telemetrii.</span><span class="sxs-lookup"><span data-stu-id="be939-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="be939-161">Ocena jest wykonywane średniej ruchomej.</span><span class="sxs-lookup"><span data-stu-id="be939-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="be939-162">Możesz skrócić ten interwał, jeśli seria nagłym odpowiada telemetrii.</span><span class="sxs-lookup"><span data-stu-id="be939-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="be939-163">Podczas pobierania próbek zmiany wartość procentową, jak najszybciej po firma Microsoft mogą obniżyć wartości procentowej pobierania próbek ponownie, aby przechwycić mniejszej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="be939-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="be939-164">Podczas pobierania próbek zmiany wartości procent, jak najszybciej po firma Microsoft mogą zwiększyć wartości procentowej pobierania próbek ponownie, aby przechwycić większej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="be939-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="be939-165">Jako wartość procentowa próbek różni się co to jest minimalny, które firma Microsoft mogła ustawić.</span><span class="sxs-lookup"><span data-stu-id="be939-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="be939-166">Jako wartość procentowa próbek różni się co to jest wartość maksymalna, które firma Microsoft mogła ustawić.</span><span class="sxs-lookup"><span data-stu-id="be939-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="be939-167">Podczas obliczania średniej ruchomej wagi przypisane do najbardziej aktualną wartość.</span><span class="sxs-lookup"><span data-stu-id="be939-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="be939-168">Użyj wartości równa lub mniejsza niż 1.</span><span class="sxs-lookup"><span data-stu-id="be939-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="be939-169">Mniejsze wartości zmiany algorytm mniej reaguje na gwałtowny.</span><span class="sxs-lookup"><span data-stu-id="be939-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="be939-170">Wartość przypisana, gdy aplikacja właśnie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="be939-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="be939-171">Nie zmniejsza to podczas debugowania kodu.</span><span class="sxs-lookup"><span data-stu-id="be939-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="be939-172">Rozdzielany średnikami lista typów, które mają być pobrane.</span><span class="sxs-lookup"><span data-stu-id="be939-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="be939-173">Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia.</span><span class="sxs-lookup"><span data-stu-id="be939-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="be939-174">Wszystkie wystąpienia określonych typów są przesyłane; typy, które nie są określone są próbkowane.</span><span class="sxs-lookup"><span data-stu-id="be939-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="be939-175">Rozdzielany średnikami lista typów, które mają być pobrane.</span><span class="sxs-lookup"><span data-stu-id="be939-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="be939-176">Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia.</span><span class="sxs-lookup"><span data-stu-id="be939-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="be939-177">Próbkowanych określonych typów; wszystkie wystąpienia innych typów zawsze będą przesyłane.</span><span class="sxs-lookup"><span data-stu-id="be939-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="be939-178">**Aby wyłączyć** adaptacyjną próbkowania, Usuń węzeł AdaptiveSamplingTelemetryProcessor z applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="be939-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="be939-179">Alternatywa: Konfigurowanie adaptacyjną próbkowania w kodzie</span><span class="sxs-lookup"><span data-stu-id="be939-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="be939-180">Zamiast dostosowywania próbkowania w pliku .config, możesz użyć kodu.</span><span class="sxs-lookup"><span data-stu-id="be939-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="be939-181">Dzięki temu można określić funkcję wywołania zwrotnego, które jest wywoływane zawsze, gdy następuje także ponowna ocena próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="be939-182">Można to, na przykład, aby dowiedzieć się, jakie częstotliwość próbkowania jest używany.</span><span class="sxs-lookup"><span data-stu-id="be939-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="be939-183">Usuń `AdaptiveSamplingTelemetryProcessor` węzeł z pliku .config.</span><span class="sxs-lookup"><span data-stu-id="be939-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="be939-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="be939-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="be939-185">([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="be939-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="be939-186">Próbkowania dla stron sieci web w języku JavaScript</span><span class="sxs-lookup"><span data-stu-id="be939-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="be939-187">Można skonfigurować stron sieci web do pobierania próbek stałej stawki z dowolnego serwera.</span><span class="sxs-lookup"><span data-stu-id="be939-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="be939-188">Gdy użytkownik [skonfigurować stron sieci web dla usługi Application Insights](app-insights-javascript.md), zmodyfikować fragment kodu, który można pobrać z portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="be939-189">(W aplikacjach ASP.NET, fragment zazwyczaj znajduje się w _Layout.cshtml.)  Wstaw wiersz, takich jak `samplingPercentage: 10,` przed klucza Instrumentacji:</span><span class="sxs-lookup"><span data-stu-id="be939-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="be939-190">W przypadku wartości procentowej pobierania próbek wybierz wartość procentową, która jest bliski 100/N, gdzie N to liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="be939-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="be939-191">Próbkowanie aktualnie nie obsługuje innych wartości.</span><span class="sxs-lookup"><span data-stu-id="be939-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="be939-192">Włączenie próbkowania stałej stawki na serwerze, klientami a serwerem będzie synchronizować tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.</span><span class="sxs-lookup"><span data-stu-id="be939-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="be939-193">Stałej częstotliwość próbkowania dla witryn sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be939-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="be939-194">Stały częstotliwość próbkowania zmniejsza ruch wysyłany z serwera sieci web i przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="be939-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="be939-195">W przeciwieństwie do próbkowania adaptacyjną zmniejsza telemetrii według stałej stawki ustalanej określone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be939-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="be939-196">Również synchronizacji klienta i serwera próbkowania, tak aby elementy powiązane są zachowywane — na przykład, jeśli przyjrzymy widoku strony w wyszukiwaniu mogły zostać odnalezione jego powiązanego żądania.</span><span class="sxs-lookup"><span data-stu-id="be939-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="be939-197">Algorytm próbkowania zachowuje elementy powiązane.</span><span class="sxs-lookup"><span data-stu-id="be939-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="be939-198">Dla każdego żądania HTTP zdarzeń, go i jego zdarzenia powiązane są odrzucane albo przesyłane.</span><span class="sxs-lookup"><span data-stu-id="be939-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="be939-199">W Eksploratorze metryk stawki, takich jak liczby żądań i wyjątków są pomnożona przez współczynnik kompensacji próbkowania, dzięki czemu są one poprawne około.</span><span class="sxs-lookup"><span data-stu-id="be939-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="be939-200">**Aktualizację pakietów NuGet projektu** do najnowszej wersji *wstępną* wersji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="be939-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="be939-201">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Uwzględnij wersję wstępną** i wyszukaj Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="be939-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="be939-202">**Wyłącz adaptacyjną próbkowania**: W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), usunąć lub komentarz `AdaptiveSamplingTelemetryProcessor` węzła.</span><span class="sxs-lookup"><span data-stu-id="be939-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="be939-203">**Włącz moduł próbkowania stałej stawki.**</span><span class="sxs-lookup"><span data-stu-id="be939-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="be939-204">Dodaj ten fragment kodu dotyczący [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="be939-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="be939-205">W przypadku wartości procentowej pobierania próbek wybierz wartość procentową, która jest bliski 100/N, gdzie N to liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="be939-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="be939-206">Próbkowanie aktualnie nie obsługuje innych wartości.</span><span class="sxs-lookup"><span data-stu-id="be939-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="be939-207">Alternatywa: Włącz stałej częstotliwość próbkowania w kodzie serwera</span><span class="sxs-lookup"><span data-stu-id="be939-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="be939-208">Zamiast ustawienie parametru próbkowania w pliku .config, możesz użyć kodu.</span><span class="sxs-lookup"><span data-stu-id="be939-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="be939-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="be939-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="be939-210">([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="be939-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="be939-211">Kiedy należy używać próbkowania?</span><span class="sxs-lookup"><span data-stu-id="be939-211">When to use sampling?</span></span>
<span data-ttu-id="be939-212">Adaptacyjną próbkowania jest włączane automatycznie, jeśli używasz 2.0.0-beta3 wersji zestawu SDK platformy ASP.NET lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="be939-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="be939-213">Niezależnie od tego, jakiego używasz wersja zestawu SDK można użyć próbkowania wprowadzanie (w naszym serwera).</span><span class="sxs-lookup"><span data-stu-id="be939-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="be939-214">Nie trzeba próbkowania dla większości aplikacji małych i średnich.</span><span class="sxs-lookup"><span data-stu-id="be939-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="be939-215">Najbardziej przydatne informacje diagnostyczne i najbardziej dokładna statystyki są pobierane przez zbierania danych dotyczących wszystkich działań użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be939-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="be939-216">Główne zalety próbkowania są następujące:</span><span class="sxs-lookup"><span data-stu-id="be939-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="be939-217">Aplikacja Insights usługi porzucania ("ogranicza") danych punktów aplikacji wysyła bardzo wysoki współczynnik dane telemetryczne w skrócie czasu interwału.</span><span class="sxs-lookup"><span data-stu-id="be939-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="be939-218">Aby zachować w [przydziału](app-insights-pricing.md) punktów danych dla warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="be939-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="be939-219">Aby zmniejszyć ruch sieciowy z kolekcji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="be939-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="be939-220">Jakiego typu próbkowania należy używać?</span><span class="sxs-lookup"><span data-stu-id="be939-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="be939-221">**Użyj wprowadzanie próbkowania, jeśli:**</span><span class="sxs-lookup"><span data-stu-id="be939-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="be939-222">Często przejść przez wykorzystaniu całego przydziału miesięcznego dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="be939-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="be939-223">Używasz wersji zestawu SDK, który nie obsługuje pobierania próbek — na przykład, zestaw SDK Java lub wersji platformy ASP.NET starszych niż 2.</span><span class="sxs-lookup"><span data-stu-id="be939-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="be939-224">Otrzymujesz dużej ilości danych telemetrycznych z przeglądarki sieci web użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be939-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="be939-225">**Użyj stałej stawki próbkowania, jeśli:**</span><span class="sxs-lookup"><span data-stu-id="be939-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="be939-226">Używany jest zestaw SDK usługi Application Insights dla usług sieci web ASP.NET w wersji 2.0.0 lub nowszej, a</span><span class="sxs-lookup"><span data-stu-id="be939-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="be939-227">Ma próbkowania synchronizowane między klientem a serwerem, dzięki czemu możesz podczas analizowania zdarzenia w [wyszukiwania](app-insights-diagnostic-search.md), można przechodzić między powiązanych zdarzeń na kliencie i serwerze, na przykład wyświetleń strony i żądań http.</span><span class="sxs-lookup"><span data-stu-id="be939-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="be939-228">Upewnieniu się wartości procentowej pobierania próbek dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be939-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="be939-229">Powinien być wystarczająco duża, aby uzyskać dokładne metryki, ale poniżej poziomu przekraczający limitu przydziału cenową i limity ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="be939-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="be939-230">**Użyj adaptacyjną próbkowania:**</span><span class="sxs-lookup"><span data-stu-id="be939-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="be939-231">W przeciwnym razie zalecamy adaptacyjną próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="be939-232">Ta opcja jest włączona domyślnie w ASP.NET server SDK, 2.0.0-beta3 wersji lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="be939-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="be939-233">Do niektórych minimalna częstotliwość nie redukują ruchu, nie będzie to miało wpływ na lokacji niskiego użycia.</span><span class="sxs-lookup"><span data-stu-id="be939-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="be939-234">Jak sprawdzić, czy w operacji pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="be939-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="be939-235">Aby odnaleźć rzeczywiste próbkowania niezależnie od tego, gdzie zostały zastosowane, należy użyć [Analytics query](app-insights-analytics.md) takich jak ta:</span><span class="sxs-lookup"><span data-stu-id="be939-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="be939-236">W każdym zachowane rekordu, `itemCount` wskazuje liczbę oryginalnego rekordów, które reprezentuje on równą 1 + Liczba poprzednich odrzuconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="be939-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="be939-237">Jak działa pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="be939-237">How does sampling work?</span></span>
<span data-ttu-id="be939-238">Stałej stawki i adaptacyjną próbkowania są funkcji zestawu SDK w wersji platformy ASP.NET z 2.0.0 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="be939-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="be939-239">Wprowadzanie próbkowania to funkcja usługi Application Insights i można w operacji, jeśli zestaw SDK nie wykonuje próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="be939-240">Algorytm próbkowania decyduje elementy dane telemetryczne, które można usunąć, a które zachować (zarówno w zestawie SDK i w usłudze Application Insights).</span><span class="sxs-lookup"><span data-stu-id="be939-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="be939-241">Decyzja próbkowania opiera się na kilka reguł, które Staraj się zachować wszystkie punkty danych powiązane ze sobą bez zmian, obsługa diagnostycznych doświadczenie w usłudze Application Insights jest efektywna i niezawodne nawet w przypadku ograniczonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="be939-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="be939-242">Na przykład jeśli niepomyślnych żądań aplikacji są wysyłane dodatkowe dane telemetryczne elementy (takie jak wyjątku i ślady zarejestrowane z tym żądaniem), pobierania próbek nie zostaną podzielone tego żądania i inne dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="be939-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="be939-243">Ją zachowuje lub porzuca je wszystkie razem.</span><span class="sxs-lookup"><span data-stu-id="be939-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="be939-244">W związku z tym sprawdzając szczegóły żądania w usłudze Application Insights, należy zawsze widzieć wraz z jego elementy skojarzone dane telemetryczne żądania.</span><span class="sxs-lookup"><span data-stu-id="be939-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="be939-245">Dla aplikacji, które definiują "użytkownika" (czyli najbardziej typowych aplikacji sieci web), decyzja próbkowania jest oparta na skrót identyfikator użytkownika, co oznacza, że wszystkie dane telemetryczne dla każdego konkretnego użytkownika jest zachowywana lub porzucony.</span><span class="sxs-lookup"><span data-stu-id="be939-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="be939-246">Dla typów aplikacji, które nie określają użytkowników (np. usługi sieci web) decyzja próbkowania jest oparta na identyfikator operacji żądania.</span><span class="sxs-lookup"><span data-stu-id="be939-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="be939-247">Na koniec elementów dane telemetryczne, które nie ma identyfikatora użytkownika ani operacji Ustaw (na przykład elementów dane telemetryczne zgłoszone asynchronicznych wątków nie kontekst http) próbkowania po prostu przechwytuje procent elementów telemetrii każdego typu.</span><span class="sxs-lookup"><span data-stu-id="be939-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="be939-248">Przedstawiając telemetrii powrót do usługi Application Insights dostosowywaniu metryk taką samą wartość procentową próbkowania użytej w czasie kolekcji, do kompensacji brakujących punktów danych.</span><span class="sxs-lookup"><span data-stu-id="be939-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="be939-249">W związku z tym podczas przeglądania danych telemetrii w usłudze Application Insights, użytkownicy wyświetlanego statystycznie prawidłową przybliżenia, które są bardzo bliski liczb rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="be939-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="be939-250">Dokładność zbliżenia zależy przede wszystkim procent skonfigurowanych próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="be939-251">Dokładność zwiększa się również, dla aplikacji, które obsługi dużej liczby zazwyczaj podobne żądania z partii użytkowników.</span><span class="sxs-lookup"><span data-stu-id="be939-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="be939-252">Z drugiej strony dla aplikacji, które nie działają z znaczne obciążenie, próbkowania nie jest potrzebna jak te aplikacje zazwyczaj można wysłać ich dane telemetryczne pozostając w ramach limitu przydziału, nie powodując utraty danych z przepustowości.</span><span class="sxs-lookup"><span data-stu-id="be939-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="be939-253">Należy pamiętać, że usługi Application Insights nie przykładowe typy telemetrii metryki i sesji od dla tych typów zmniejszenie dokładność można zdecydowanie niepożądane.</span><span class="sxs-lookup"><span data-stu-id="be939-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="be939-254">Adaptacyjną pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="be939-254">Adaptive sampling</span></span>
<span data-ttu-id="be939-255">Próbkowanie adaptacyjną dodaje składnik, który monitoruje bieżąca szybkość transmisji z zestawu SDK i dopasowuje wartości procentowej pobierania próbek, aby spróbować pozostać w docelowym maksymalna szybkość.</span><span class="sxs-lookup"><span data-stu-id="be939-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="be939-256">Dostosowania są przeliczane w regularnych odstępach czasu i opierają się na to ruchoma średnia szybkość transmisji wychodzących.</span><span class="sxs-lookup"><span data-stu-id="be939-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="be939-257">Pobieranie próbek i zestawu SDK języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="be939-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="be939-258">Po stronie klienta (JavaScript) zestawu SDK uczestniczy w stałej częstotliwość próbkowania w połączeniu z zestawem SDK po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="be939-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="be939-259">Instrumentacją stron wysyła dane telemetryczne po stronie klienta z tych samych użytkowników, dla których po stronie serwera wprowadzone decyzję "próbki w".</span><span class="sxs-lookup"><span data-stu-id="be939-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="be939-260">Istotą takiej logiki zaprojektowano w celu zachowania integralności sesji użytkownika dla strony klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="be939-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="be939-261">W związku z tym z dowolnym elemencie określonego telemetrii usługi Application Insights, można znaleźć wszystkie pozostałe elementy danych telemetrycznych dla tego użytkownika lub sesję.</span><span class="sxs-lookup"><span data-stu-id="be939-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="be939-262">*Moje klienta i dane telemetryczne po stronie serwera nie pokazuj przykłady skoordynowany sposób, jak opisano powyżej.*</span><span class="sxs-lookup"><span data-stu-id="be939-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="be939-263">Sprawdź czy jest włączony próbkowania stałej stawki zarówno na serwerze i kliencie.</span><span class="sxs-lookup"><span data-stu-id="be939-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="be939-264">Upewnij się, że zestawu SDK w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="be939-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="be939-265">Sprawdź, ustawić tej samej wartości procentowej pobierania próbek w klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="be939-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="be939-266">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="be939-266">Frequently Asked Questions</span></span>
<span data-ttu-id="be939-267">*Dlaczego nie jest próbkowania proste "zbieranie X procent każdego typu danych telemetrycznych"?*</span><span class="sxs-lookup"><span data-stu-id="be939-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="be939-268">Gdy ta metoda pobierania próbek będzie dostarczać bardzo wysokiej precyzji w przybliżenia metryki, go spowoduje przerwanie możliwość powiązania danych diagnostycznych na użytkowników, sesji i żądań, co jest szczególnie ważne dla diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be939-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="be939-269">W związku z tym pobierania próbek działa lepiej "Zbieraj wszystkie dane telemetryczne elementy X procent użytkowników aplikacji" lub "Zbieraj wszystkie dane telemetryczne dotyczące X Procent żądań aplikacji" logiki.</span><span class="sxs-lookup"><span data-stu-id="be939-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="be939-270">Dla elementów telemetrii nie są skojarzone z żądaniami (na przykład asynchronicznego przetwarzania w tle), jest bazowy "zbieranie X procent wszystkie elementy dla każdego typu danych telemetrycznych."</span><span class="sxs-lookup"><span data-stu-id="be939-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="be939-271">*Mogą ulec zmianie wartości procentowej pobierania próbek?*</span><span class="sxs-lookup"><span data-stu-id="be939-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="be939-272">Tak, adaptacyjną próbkowania stopniowo zmienia wartości procentowej pobierania próbek, oparte na aktualnie obserwowanych ilość danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="be939-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="be939-273">*Użycie stałej stawki próbkowania, jak sprawdzić, które próbkowania procent będzie najlepsza dla mojej aplikacji?*</span><span class="sxs-lookup"><span data-stu-id="be939-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="be939-274">Jednym ze sposobów jest próbkowania do uruchomienia z adaptacyjną, sprawdź, co Oceń to rozliczy na (zobacz powyżej pytanie), a następnie przejdź do stałej stawki próbkowania przy użyciu tego kursu.</span><span class="sxs-lookup"><span data-stu-id="be939-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="be939-275">W przeciwnym razie trzeba odgadnąć.</span><span class="sxs-lookup"><span data-stu-id="be939-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="be939-276">Analizowanie bieżącego użycia telemetrii w AI, przestrzegać wszelkich ograniczania przepustowości występuje i oszacowania ilości zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="be939-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="be939-277">Te trzy wejść, wraz z wybranej warstwy cenowej, sugerują, ile można zmniejszyć ilość zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="be939-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="be939-278">Jednak wzrost liczby użytkowników lub inne przesunięcia w woluminie danych telemetrycznych może unieważnić oszacować.</span><span class="sxs-lookup"><span data-stu-id="be939-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="be939-279">*Co się stanie, jeśli można skonfigurować wartości procentowej pobierania próbek zbyt niska?*</span><span class="sxs-lookup"><span data-stu-id="be939-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="be939-280">Procent próbkowania zbyt niski (próbkowanie over-aggressive) zmniejsza dokładność przybliżenia, gdy usługi Application Insights próbuje kompensacji wizualizację danych redukcji woluminów danych.</span><span class="sxs-lookup"><span data-stu-id="be939-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="be939-281">Ponadto czynności diagnostycznych może być obniżona, jako część żądania rzadko awarie lub powolne próbkować można się.</span><span class="sxs-lookup"><span data-stu-id="be939-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="be939-282">*Co się stanie, jeśli można skonfigurować zbyt wysokiej wartości procentowej pobierania próbek?*</span><span class="sxs-lookup"><span data-stu-id="be939-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="be939-283">Konfigurowanie próbkowania zbyt wysoki procent (nie agresywne wystarczająco) powoduje niewystarczające zmniejszenia ilości zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="be939-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="be939-284">Nadal może wystąpić utrata danych telemetrii dotyczące ograniczania przepustowości i kosztów przy użyciu usługi Application Insights może być większa niż zostanie zaplanowane z powodu nadwyżkowe opłat.</span><span class="sxs-lookup"><span data-stu-id="be939-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="be939-285">*Na platformach, które mogą używać próbkowania?*</span><span class="sxs-lookup"><span data-stu-id="be939-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="be939-286">Wprowadzanie próbkowanie może być spowodowany automatycznie dla dowolnego telemetrii powyżej woluminu zestawu SDK nie wykonuje próbkowania.</span><span class="sxs-lookup"><span data-stu-id="be939-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="be939-287">To będzie działać, na przykład, jeśli aplikacja korzysta z serwera Java lub jeśli używasz starszej wersji zestawu SDK platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be939-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="be939-288">Jeśli używasz zestawu SDK platformy ASP.NET w wersji 2.0.0 lub nowszym (hostowanego na platformie Azure lub na danym serwerze), możesz uzyskać adaptacyjną próbkowania domyślnie, ale możesz przełączyć się do stałej stawki, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="be939-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="be939-289">Z włączonym próbkowaniem stałej stawki, przeglądarkę zestawu SDK automatycznie synchronizuje do próbkowania powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="be939-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="be939-290">*Brak niektórych rzadkich zdarzeń, które można zawsze były wyświetlane. Jak można je poza modułu próbkowania?*</span><span class="sxs-lookup"><span data-stu-id="be939-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="be939-291">Inicjowanie oddzielnego wystąpienia TelemetryClient z nowego TelemetryConfiguration (nie domyślnie aktywny).</span><span class="sxs-lookup"><span data-stu-id="be939-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="be939-292">Użyj do wysyłania zdarzeń rzadko.</span><span class="sxs-lookup"><span data-stu-id="be939-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be939-293">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be939-293">Next steps</span></span>
* <span data-ttu-id="be939-294">[Filtrowanie](app-insights-api-filtering-sampling.md) zapewniają więcej ścisłej kontroli wysyła zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="be939-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

