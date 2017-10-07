---
title: "aaaTelemetry próbkowania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Jak tookeep hello ilość danych telemetrycznych pod kontrolą."
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="9baba-103">Próbkowanie w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="9baba-103">Sampling in Application Insights</span></span>


<span data-ttu-id="9baba-104">Próbkowanie to funkcja [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9baba-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="9baba-105">Jest to hello zalecany sposób tooreduce telemetrii ruchu i magazynu, przy zachowaniu statystycznie prawidłową analizy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9baba-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="9baba-106">Filtr Hello wybiera elementy, które są powiązane, dzięki czemu można przechodzić między elementami podczas wykonywania badań diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="9baba-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="9baba-107">Gdy metryki liczby są przedstawiane tooyou w portalu hello, są renormalized tootake konto hello próbkowania toominimize żadnego wpływu na powitania statystyk.</span><span class="sxs-lookup"><span data-stu-id="9baba-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="9baba-108">Próbkowania powoduje zmniejszenie kosztów ruchu i dane i pomaga uniknąć ograniczania.</span><span class="sxs-lookup"><span data-stu-id="9baba-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="9baba-109">Krótko mówiąc:</span><span class="sxs-lookup"><span data-stu-id="9baba-109">In brief:</span></span>
* <span data-ttu-id="9baba-110">Próbkowanie zachowuje 1 w  *n*  rejestruje i odrzuca hello rest.</span><span class="sxs-lookup"><span data-stu-id="9baba-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="9baba-111">Na przykład mogą go zachować zdarzenia 1 do 5, częstotliwość próbkowania, 20%.</span><span class="sxs-lookup"><span data-stu-id="9baba-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="9baba-112">Próbkowanie odbywa się automatycznie, jeśli aplikacja wyśle dużej ilości danych telemetrii, w aplikacji serwera sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9baba-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="9baba-113">Można również ustawić próbkowania ręcznie, albo hello w portalu na powitania cennikiem; lub w hello zestawu SDK platformy ASP.NET w pliku .config hello tooalso zmniejszenie ruchu w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="9baba-114">Jeśli dziennika zdarzeń niestandardowych, i chcesz toomake się, że zestaw zdarzeń jest zachowywana lub odrzucone ze sobą, upewnij się, że zostały one hello tę samą wartość OperationId.</span><span class="sxs-lookup"><span data-stu-id="9baba-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="9baba-115">dzielnik próbkowania Hello  *n*  jest zgłaszany we wszystkich rekordach we właściwości hello `itemCount`, w wyszukiwaniu widocznego w obszarze hello przyjazna nazwa "liczbę żądań" lub "liczba zdarzeń".</span><span class="sxs-lookup"><span data-stu-id="9baba-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="9baba-116">Podczas pobierania próbek nie jest w operacji `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="9baba-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="9baba-117">Jeśli piszesz zapytania analityczne, [uwzględnienia próbkowania](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="9baba-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="9baba-118">W szczególności, zamiast po prostu zliczanie rekordów, należy użyć `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9baba-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="9baba-119">Typy pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="9baba-119">Types of sampling</span></span>
<span data-ttu-id="9baba-120">Istnieją trzy metody alternatywne próbkowania:</span><span class="sxs-lookup"><span data-stu-id="9baba-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="9baba-121">**Próbkowanie adaptacyjną** automatycznie dostosowuje hello ilość danych telemetrycznych wysłanych z hello zestawu SDK w aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9baba-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="9baba-122">Domyślnie z 2.0.0-beta3 v zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9baba-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="9baba-123">Obecnie dostępne dla platformy ASP.NET tylko telemetrii po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="9baba-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="9baba-124">**Próbkowanie stałej stawki** zmniejsza hello ilość danych telemetrycznych wysłanych z serwera programu ASP.NET oraz z przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9baba-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="9baba-125">Możesz ustawić częstotliwość hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-125">You set hello rate.</span></span> <span data-ttu-id="9baba-126">powitania klienta i serwera będzie synchronizować ich próbkowania tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.</span><span class="sxs-lookup"><span data-stu-id="9baba-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="9baba-127">**Wprowadzanie próbkowania** działa w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9baba-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="9baba-128">Odrzuca niektóre dane telemetryczne hello dociera z aplikacji, z szybkością ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="9baba-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="9baba-129">Nie zmniejszenie ruchu telemetrii, ale pomaga zachować w wykorzystaniu całego przydziału miesięcznego.</span><span class="sxs-lookup"><span data-stu-id="9baba-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="9baba-130">Witaj dużą zaletą próbkowania wprowadzanie jest bez ponownego wdrażania aplikacji można ją ustawić, czy działa on jednakowo do wszystkich serwerów i klientów.</span><span class="sxs-lookup"><span data-stu-id="9baba-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="9baba-131">W przypadku adaptacyjną lub stała częstotliwość próbkowania w operacji, wprowadzanie próbek jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="9baba-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="9baba-132">Wprowadzanie próbkowania</span><span class="sxs-lookup"><span data-stu-id="9baba-132">Ingestion sampling</span></span>
<span data-ttu-id="9baba-133">Ta forma pobierania próbek działa w momencie hello gdzie telemetrii hello z serwera sieci web, przeglądarki i urządzenia osiąga punkt końcowy usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="9baba-134">Chociaż nie redukują hello telemetrii wysyłania danych z aplikacji, Zmniejsz ilość hello przetwarzane i przechowywane (i naliczona opłata za) przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9baba-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="9baba-135">Użyj tego typu próbkowania, jeśli aplikacja często przechodzi przez jego przydział miesięczny i nie ma możliwości hello przy użyciu jednego z typów na podstawie zestawu SDK hello pobierania próbek.</span><span class="sxs-lookup"><span data-stu-id="9baba-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="9baba-136">Ustaw częstotliwość próbkowania hello w hello przydziałów i cennik bloku:</span><span class="sxs-lookup"><span data-stu-id="9baba-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![W bloku Omówienie aplikacji hello kliknij ustawienia, przydziału, próbek, a następnie wybierz częstotliwość próbkowania, a następnie kliknij przycisk Aktualizuj.](./media/app-insights-sampling/04.png)

<span data-ttu-id="9baba-138">Podobnie jak inne rodzaje próbkowania algorytm hello zachowuje elementy powiązane dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9baba-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="9baba-139">Na przykład, gdy jest sprawdzanie hello telemetrii w wyszukiwania, będzie możliwe toofind hello powiązana tooa określonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="9baba-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="9baba-140">Metryka liczby takich jak liczby żądań i szybkość wyjątek poprawnie zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="9baba-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="9baba-141">Punkty danych, które są odrzucane przez pobieranie próbek nie są dostępne w dowolnej funkcji usługi Application Insights, takich jak [eksportu ciągłego](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="9baba-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="9baba-142">Wprowadzanie próbkowania nie działa podczas operacji SDK próbkowania adaptacyjną lub stałej stawki.</span><span class="sxs-lookup"><span data-stu-id="9baba-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="9baba-143">Częstotliwość próbkowania hello na powitania zestawu SDK jest mniejsza niż 100%, następnie hello wprowadzanie próbkowania ustawione jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="9baba-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="9baba-144">Witaj wartości wyświetlane na kafelku hello wskazuje wartość hello, dla wprowadzanie próbkowania.</span><span class="sxs-lookup"><span data-stu-id="9baba-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="9baba-145">Jeśli jest używany w operacji pobierania zestawu SDK nie reprezentuje hello rzeczywiste próbkowania.</span><span class="sxs-lookup"><span data-stu-id="9baba-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="9baba-146">Adaptacyjną próbkowania na serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="9baba-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="9baba-147">Adaptacyjną próbkowania jest dostępna dla hello zestaw SDK usługi Application Insights dla platformy ASP.NET v 2.0.0-beta3 i nowszych i jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="9baba-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="9baba-148">Próbkowanie adaptacyjną ma wpływ na powitania ilość danych telemetrycznych wysłanych z Twojej toohello aplikacji serwera sieci web usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9baba-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="9baba-149">Witaj woluminu jest automatycznie korygowane tookeep w ramach określonej maksymalna szybkość ruchu.</span><span class="sxs-lookup"><span data-stu-id="9baba-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="9baba-150">Go nie działa niewielki dane telemetryczne, więc w debugowaniu aplikacji lub witryny sieci Web z użyciem niski nie będzie to mieć wpływ na.</span><span class="sxs-lookup"><span data-stu-id="9baba-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="9baba-151">wolumin docelowy hello tooachieve, niektóre dane telemetryczne hello generowane są usuwane.</span><span class="sxs-lookup"><span data-stu-id="9baba-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="9baba-152">Zachowując podobnie jak inne rodzaje próbkowania algorytm hello elementy powiązane dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9baba-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="9baba-153">Na przykład, gdy jest sprawdzanie hello telemetrii w wyszukiwania, będzie możliwe toofind hello powiązana tooa określonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="9baba-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="9baba-154">Metryka zlicza, takich jak liczby żądań i szybkość wyjątek są skorygowaną toocompensate dla hello próbkowania szybkości, tak aby pokazywały około poprawne wartości w Eksploratorze metryki.</span><span class="sxs-lookup"><span data-stu-id="9baba-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="9baba-155">**Aktualizacja projektu NuGet** najnowsza wersja pakietów toohello *wersji wstępnej* wersji usługi Application Insights: kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Include wstępna** i wyszukaj Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="9baba-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="9baba-156">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), można dostosować kilku parametrów w hello `AdaptiveSamplingTelemetryProcessor` węzła.</span><span class="sxs-lookup"><span data-stu-id="9baba-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="9baba-157">rysunki Hello wyświetlane są wartościami domyślnymi hello:</span><span class="sxs-lookup"><span data-stu-id="9baba-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="9baba-158">Witaj docelowej szybkość, z której hello adaptacyjną algorytm ma dla **na każdym hoście serwera**.</span><span class="sxs-lookup"><span data-stu-id="9baba-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="9baba-159">Jeśli aplikacja sieci web jest uruchomiony na wielu hostach, tak tooremain w szybkość docelowy ruchu w portalu usługi Application Insights hello Zmniejsz tę wartość.</span><span class="sxs-lookup"><span data-stu-id="9baba-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="9baba-160">Interwał powitania, w których hello jest ponownie oceniane bieżącej szybkości telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9baba-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="9baba-161">Ocena jest wykonywane średniej ruchomej.</span><span class="sxs-lookup"><span data-stu-id="9baba-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="9baba-162">Możesz tooshorten ten interwał Jeśli seria odpowiedzialności za toosudden telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9baba-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="9baba-163">W przypadku zmiany wartości wartości procentowej pobierania próbek, jak najszybciej po firma Microsoft może toolower ponownie próbkowania procent toocapture mniejsza ilość danych.</span><span class="sxs-lookup"><span data-stu-id="9baba-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="9baba-164">W przypadku zmiany wartości wartości procentowej pobierania próbek, jak najszybciej po firma Microsoft może tooincrease ponownie próbkowania procent toocapture większej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="9baba-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="9baba-165">Jako wartość procentowa próbek różni się to minimalny hello jest firma Microsoft może tooset.</span><span class="sxs-lookup"><span data-stu-id="9baba-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="9baba-166">Jako wartość procentowa próbek różni się to maksymalna wartość hello jest firma Microsoft może tooset.</span><span class="sxs-lookup"><span data-stu-id="9baba-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="9baba-167">Hello obliczania średniej ruchomej hello waga hello przypisaną wartość najnowszych toohello.</span><span class="sxs-lookup"><span data-stu-id="9baba-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="9baba-168">Użyj tooor równy wartość mniejszą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9baba-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="9baba-169">Mniejsze wartości zmiany algorytm hello mniej reaktywne toosudden.</span><span class="sxs-lookup"><span data-stu-id="9baba-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="9baba-170">wartość Hello przypisany podczas aplikacji hello właśnie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="9baba-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="9baba-171">Nie zmniejsza to podczas debugowania kodu.</span><span class="sxs-lookup"><span data-stu-id="9baba-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="9baba-172">Lista typów, które nie mają toobe próbkowany rozdzielany średnikami.</span><span class="sxs-lookup"><span data-stu-id="9baba-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="9baba-173">Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9baba-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="9baba-174">Wszystkie wystąpienia hello określone typy są przesyłane; próbkowanych Hello typy, które nie zostały określone.</span><span class="sxs-lookup"><span data-stu-id="9baba-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="9baba-175">Lista typów, które mają toobe próbkowany rozdzielany średnikami.</span><span class="sxs-lookup"><span data-stu-id="9baba-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="9baba-176">Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9baba-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="9baba-177">Witaj określone typy są próbkowane; wszystkie wystąpienia elementu hello będą zawsze przesyłane innych typów.</span><span class="sxs-lookup"><span data-stu-id="9baba-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="9baba-178">**tooswitch poza** adaptacyjną próbkowania, Usuń hello AdaptiveSamplingTelemetryProcessor węzła z applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="9baba-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="9baba-179">Alternatywa: Konfigurowanie adaptacyjną próbkowania w kodzie</span><span class="sxs-lookup"><span data-stu-id="9baba-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="9baba-180">Zamiast dostosowywania próbkowania w pliku .config hello, możesz użyć kodu.</span><span class="sxs-lookup"><span data-stu-id="9baba-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="9baba-181">Dzięki temu toospecify funkcję wywołania zwrotnego, które jest wywoływane zawsze, gdy częstotliwość próbkowania hello jest ponownie oceniane.</span><span class="sxs-lookup"><span data-stu-id="9baba-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="9baba-182">Można go użyć, na przykład toofind się, jakie częstotliwość próbkowania jest używany.</span><span class="sxs-lookup"><span data-stu-id="9baba-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="9baba-183">Usuń hello `AdaptiveSamplingTelemetryProcessor` węzeł z pliku .config hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="9baba-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="9baba-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="9baba-185">([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="9baba-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="9baba-186">Próbkowania dla stron sieci web w języku JavaScript</span><span class="sxs-lookup"><span data-stu-id="9baba-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="9baba-187">Można skonfigurować stron sieci web do pobierania próbek stałej stawki z dowolnego serwera.</span><span class="sxs-lookup"><span data-stu-id="9baba-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="9baba-188">Gdy możesz [skonfigurować hello stron sieci web dla usługi Application Insights](app-insights-javascript.md), zmodyfikować fragment hello, który można pobrać z portalu Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="9baba-189">(W aplikacjach ASP.NET, fragment hello zazwyczaj znajduje się w _Layout.cshtml.)  Wstaw wiersz, takich jak `samplingPercentage: 10,` przed klucza Instrumentacji hello:</span><span class="sxs-lookup"><span data-stu-id="9baba-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="9baba-190">W przypadku wartości procentowej pobierania próbek hello wybierz wartość procentową, która jest Zamknij too100/N, gdzie N to liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="9baba-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="9baba-191">Próbkowanie aktualnie nie obsługuje innych wartości.</span><span class="sxs-lookup"><span data-stu-id="9baba-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="9baba-192">Włączenie próbkowania stałej stawki na powitania serwera, hello klientami a serwerem będzie synchronizować tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.</span><span class="sxs-lookup"><span data-stu-id="9baba-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="9baba-193">Stałej częstotliwość próbkowania dla witryn sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9baba-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="9baba-194">Stały częstotliwość próbkowania zmniejsza ruch hello wysłanych z serwera sieci web i przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="9baba-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="9baba-195">W przeciwieństwie do próbkowania adaptacyjną zmniejsza telemetrii według stałej stawki ustalanej określone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9baba-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="9baba-196">Również synchronizacji powitania klienta i serwera próbkowania, tak aby elementy powiązane są zachowywane — na przykład, jeśli przyjrzymy widoku strony w wyszukiwaniu mogły zostać odnalezione jego powiązanego żądania.</span><span class="sxs-lookup"><span data-stu-id="9baba-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="9baba-197">Algorytm próbkowania Hello zachowuje elementy powiązane.</span><span class="sxs-lookup"><span data-stu-id="9baba-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="9baba-198">Dla każdego żądania HTTP zdarzeń, go i jego zdarzenia powiązane są odrzucane albo przesyłane.</span><span class="sxs-lookup"><span data-stu-id="9baba-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="9baba-199">W Eksploratorze metryk stawki, takich jak liczby żądań i wyjątków są pomnożona przez współczynnik toocompensate dla hello próbkowania, dzięki czemu są one poprawne około.</span><span class="sxs-lookup"><span data-stu-id="9baba-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="9baba-200">**Aktualizację pakietów NuGet projektu** toohello najnowszych *wstępną* wersji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9baba-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="9baba-201">Kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Uwzględnij wersję wstępną** i wyszukaj Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="9baba-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="9baba-202">**Wyłącz adaptacyjną próbkowania**: W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), usunąć lub komentarz hello `AdaptiveSamplingTelemetryProcessor` węzła.</span><span class="sxs-lookup"><span data-stu-id="9baba-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="9baba-203">**Włącz moduł próbkowania stałej stawki hello.**</span><span class="sxs-lookup"><span data-stu-id="9baba-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="9baba-204">Dodaj ten fragment zbyt[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="9baba-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="9baba-205">W przypadku wartości procentowej pobierania próbek hello wybierz wartość procentową, która jest Zamknij too100/N, gdzie N to liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="9baba-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="9baba-206">Próbkowanie aktualnie nie obsługuje innych wartości.</span><span class="sxs-lookup"><span data-stu-id="9baba-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="9baba-207">Alternatywa: Włącz stałej częstotliwość próbkowania w kodzie serwera</span><span class="sxs-lookup"><span data-stu-id="9baba-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="9baba-208">Zamiast ustawienie parametru próbkowania hello w pliku .config hello, możesz użyć kodu.</span><span class="sxs-lookup"><span data-stu-id="9baba-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="9baba-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="9baba-209">*C#*</span></span>

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

<span data-ttu-id="9baba-210">([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="9baba-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="9baba-211">Podczas pobierania próbek toouse?</span><span class="sxs-lookup"><span data-stu-id="9baba-211">When toouse sampling?</span></span>
<span data-ttu-id="9baba-212">Jeśli używasz hello 2.0.0-beta3 wersji zestawu SDK platformy ASP.NET jest automatycznie włączone adaptacyjną próbkowania lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="9baba-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="9baba-213">Niezależnie od tego, jakiego używasz wersja zestawu SDK można użyć próbkowania wprowadzanie (w naszym serwera).</span><span class="sxs-lookup"><span data-stu-id="9baba-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="9baba-214">Nie trzeba próbkowania dla większości aplikacji małych i średnich.</span><span class="sxs-lookup"><span data-stu-id="9baba-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="9baba-215">najbardziej przydatne informacje diagnostyczne Hello i najbardziej dokładna statystyki są pobierane przez zbierania danych dotyczących wszystkich działań użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9baba-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="9baba-216">główne zalety próbkowania Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="9baba-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="9baba-217">Aplikacja Insights usługi porzucania ("ogranicza") danych punktów aplikacji wysyła bardzo wysoki współczynnik dane telemetryczne w skrócie czasu interwału.</span><span class="sxs-lookup"><span data-stu-id="9baba-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="9baba-218">tookeep w hello [przydziału](app-insights-pricing.md) punktów danych dla warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="9baba-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="9baba-219">ruch sieciowy tooreduce z kolekcji hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9baba-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="9baba-220">Jakiego typu próbkowania należy używać?</span><span class="sxs-lookup"><span data-stu-id="9baba-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="9baba-221">**Użyj wprowadzanie próbkowania, jeśli:**</span><span class="sxs-lookup"><span data-stu-id="9baba-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="9baba-222">Często przejść przez wykorzystaniu całego przydziału miesięcznego dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9baba-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="9baba-223">Używasz wersji hello zestawu SDK, który nie obsługuje pobierania próbek — na przykład, hello zestawu Java SDK lub wersji platformy ASP.NET starszych niż 2.</span><span class="sxs-lookup"><span data-stu-id="9baba-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="9baba-224">Otrzymujesz dużej ilości danych telemetrycznych z przeglądarki sieci web użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9baba-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="9baba-225">**Użyj stałej stawki próbkowania, jeśli:**</span><span class="sxs-lookup"><span data-stu-id="9baba-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="9baba-226">Używasz hello zestaw SDK usługi Application Insights dla usług sieci web ASP.NET w wersji 2.0.0 lub nowszej, a</span><span class="sxs-lookup"><span data-stu-id="9baba-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="9baba-227">Ma próbkowania synchronizowane między klientem a serwerem, dzięki czemu możesz podczas analizowania zdarzenia w [wyszukiwania](app-insights-diagnostic-search.md), można przechodzić między powiązanych zdarzeń na powitania klienta i serwera, takie jak liczba wyświetleń strony i żądań http.</span><span class="sxs-lookup"><span data-stu-id="9baba-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="9baba-228">Upewnieniu się wartości procentowej pobierania próbek hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9baba-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="9baba-229">Powinien być wystarczająco duża tooget dokładnych metryk, ale poniżej hello szybkość, z której przekracza przydział cenową i hello ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="9baba-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="9baba-230">**Użyj adaptacyjną próbkowania:**</span><span class="sxs-lookup"><span data-stu-id="9baba-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="9baba-231">W przeciwnym razie zalecamy adaptacyjną próbkowania.</span><span class="sxs-lookup"><span data-stu-id="9baba-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="9baba-232">Ta opcja jest włączona domyślnie w hello ASP.NET server SDK w wersji 2.0.0-beta3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9baba-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="9baba-233">Do niektórych minimalna częstotliwość nie redukują ruchu, nie będzie to miało wpływ na lokacji niskiego użycia.</span><span class="sxs-lookup"><span data-stu-id="9baba-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="9baba-234">Jak sprawdzić, czy w operacji pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="9baba-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="9baba-235">rzeczywiste hello toodiscover próbkowania szybkość niezależnie od tego, gdzie ma zastosowane, użyj [Analytics query](app-insights-analytics.md) takich jak ta:</span><span class="sxs-lookup"><span data-stu-id="9baba-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="9baba-236">W każdym zachowane rekordu, `itemCount` wskazuje liczbę hello oryginalnego rekordów, które reprezentuje on równy too1 + hello liczbę poprzednich odrzuconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="9baba-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="9baba-237">Jak działa pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="9baba-237">How does sampling work?</span></span>
<span data-ttu-id="9baba-238">Stałej stawki i adaptacyjną próbkowania są funkcją hello zestawu SDK w wersji platformy ASP.NET z 2.0.0 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="9baba-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="9baba-239">Wprowadzanie próbkowania jest funkcją hello usługa Application Insights i można w operacji hello zestawu SDK nie wykonuje próbkowania.</span><span class="sxs-lookup"><span data-stu-id="9baba-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="9baba-240">Algorytm próbkowania Hello decyduje o tym, które toodrop elementów telemetrii i które tych tookeep (czy jest hello zestawu SDK lub usługa Application Insights hello).</span><span class="sxs-lookup"><span data-stu-id="9baba-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="9baba-241">decyzja próbkowania Hello opiera się na kilka reguł, które mają toopreserve wszystkie punkty danych powiązane ze sobą nienaruszone, obsługa diagnostycznych doświadczenie w usłudze Application Insights jest efektywna i niezawodne nawet w przypadku ograniczonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9baba-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="9baba-242">Na przykład jeśli niepomyślnych żądań aplikacji są wysyłane dodatkowe dane telemetryczne elementy (takie jak wyjątku i ślady zarejestrowane z tym żądaniem), pobierania próbek nie zostaną podzielone tego żądania i inne dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9baba-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="9baba-243">Ją zachowuje lub porzuca je wszystkie razem.</span><span class="sxs-lookup"><span data-stu-id="9baba-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="9baba-244">W związku z tym sprawdzając szczegóły żądania hello w usłudze Application Insights, należy zawsze widzieć żądania hello wraz z jego elementy skojarzone dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9baba-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="9baba-245">Dla aplikacji, które definiują "użytkownika" (czyli najbardziej typowych aplikacji sieci web), decyzja próbkowania hello jest oparta na skrót hello hello identyfikator użytkownika, co oznacza, że wszystkie dane telemetryczne dla każdego konkretnego użytkownika jest zachowywana lub porzucony.</span><span class="sxs-lookup"><span data-stu-id="9baba-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="9baba-246">Dla hello typów aplikacji, które nie określają użytkowników (np. usługi sieci web) decyzja próbkowania hello jest oparta na identyfikator operacji hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="9baba-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="9baba-247">Na koniec hello telemetrii elementów, które nie ma identyfikatora użytkownika ani operacji Ustaw (na przykład elementów dane telemetryczne zgłoszone asynchronicznych wątków nie kontekst http) próbkowania po prostu przechwytuje procent elementów telemetrii każdego typu.</span><span class="sxs-lookup"><span data-stu-id="9baba-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="9baba-248">Prezentując tooyou wstecz telemetrii usługi Application Insights hello usługi można dostosować metryki hello przez hello tej samej wartości procentowej pobierania próbek użytej w czasie hello kolekcji, toocompensate dla hello brakujących punktów danych.</span><span class="sxs-lookup"><span data-stu-id="9baba-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="9baba-249">W związku z tym podczas przeglądania hello telemetrii w usłudze Application Insights, użytkownicy hello jest wyświetlany statystycznie prawidłową przybliżenia, które są bardzo Zamknij toohello liczb rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9baba-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="9baba-250">dokładność Hello zbliżenia hello zależy przede wszystkim wartości procentowej pobierania próbek hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="9baba-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="9baba-251">Dokładność hello zwiększa się również, dla aplikacji, które obsługi dużej liczby zazwyczaj podobne żądania z partii użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9baba-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="9baba-252">Na hello drugiej strony, aplikacji, które nie działają z znaczne obciążenie, próbkowanie nie jest potrzebna, jak te aplikacje zazwyczaj można wysłać ich dane telemetryczne pozostając w ramach limitu przydziału hello, nie powodując utraty danych z przepustowości.</span><span class="sxs-lookup"><span data-stu-id="9baba-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="9baba-253">Należy pamiętać, że usługi Application Insights nie przykładowe typy telemetrii metryki i sesji od dla tych typów zmniejszenie precyzji hello można zdecydowanie niepożądane.</span><span class="sxs-lookup"><span data-stu-id="9baba-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="9baba-254">Adaptacyjną pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="9baba-254">Adaptive sampling</span></span>
<span data-ttu-id="9baba-255">Adaptacyjną próbkowania dodaje składnik tego monitorów hello bieżąca szybkość transmisji z hello zestawu SDK i dostosowuje hello próbkowania procent tootry toostay w hello docelowy maksymalna szybkość.</span><span class="sxs-lookup"><span data-stu-id="9baba-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="9baba-256">dostosowanie Hello są przeliczane w regularnych odstępach czasu i opierają się na to ruchoma średnia hello szybkość transmisji wychodzących.</span><span class="sxs-lookup"><span data-stu-id="9baba-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="9baba-257">Pobieranie próbek i hello JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="9baba-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="9baba-258">powitania klienta (JavaScript) zestawu SDK uczestniczy w stałej częstotliwość próbkowania w połączeniu z powitania po stronie serwera zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9baba-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="9baba-259">Hello Instrumentacji stron wysyła dane telemetryczne po stronie klienta z hello tych samych użytkowników, których powitania po stronie serwera wprowadzono decyzji zbyt "sample w."</span><span class="sxs-lookup"><span data-stu-id="9baba-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="9baba-260">Tę logikę jest zaprojektowana toomaintain integralność sesji użytkownika na stronach klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="9baba-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="9baba-261">W związku z tym z dowolnym elemencie określonego telemetrii usługi Application Insights, można znaleźć wszystkie pozostałe elementy danych telemetrycznych dla tego użytkownika lub sesję.</span><span class="sxs-lookup"><span data-stu-id="9baba-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="9baba-262">*Moje klienta i dane telemetryczne po stronie serwera nie pokazuj przykłady skoordynowany sposób, jak opisano powyżej.*</span><span class="sxs-lookup"><span data-stu-id="9baba-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="9baba-263">Sprawdź czy jest włączony próbkowania stałej stawki zarówno na serwerze i kliencie.</span><span class="sxs-lookup"><span data-stu-id="9baba-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="9baba-264">Upewnij się, że ta wersja zestawu SDK hello jest 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9baba-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="9baba-265">Sprawdź, czy możesz ustawić hello samej próbkowania wartość procentowa w powitania klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="9baba-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="9baba-266">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="9baba-266">Frequently Asked Questions</span></span>
<span data-ttu-id="9baba-267">*Dlaczego nie jest próbkowania proste "zbieranie X procent każdego typu danych telemetrycznych"?*</span><span class="sxs-lookup"><span data-stu-id="9baba-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="9baba-268">Gdy ta metoda pobierania próbek będzie dostarczać bardzo wysokiej precyzji w przybliżenia metryki, go spowoduje przerwanie możliwości toocorrelate danych diagnostycznych na użytkowników, sesji i żądań, co jest szczególnie ważne dla diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="9baba-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="9baba-269">W związku z tym pobierania próbek działa lepiej "Zbieraj wszystkie dane telemetryczne elementy X procent użytkowników aplikacji" lub "Zbieraj wszystkie dane telemetryczne dotyczące X Procent żądań aplikacji" logiki.</span><span class="sxs-lookup"><span data-stu-id="9baba-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="9baba-270">Dla elementów telemetrii hello nie są skojarzone z żądaniami hello (na przykład asynchronicznego przetwarzania w tle) spadek hello jest zbyt "zbieranie X procent wszystkie elementy dla każdego typu danych telemetrycznych."</span><span class="sxs-lookup"><span data-stu-id="9baba-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="9baba-271">*Mogą ulec zmianie wartości procentowej pobierania próbek hello?*</span><span class="sxs-lookup"><span data-stu-id="9baba-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="9baba-272">Tak, adaptacyjną próbkowania stopniowo zmienia wartości procentowej pobierania próbek hello, oparte na powitania obecnie obserwowanych ilość danych telemetrycznych hello.</span><span class="sxs-lookup"><span data-stu-id="9baba-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="9baba-273">*Użycie stałej stawki próbkowania, jak sprawdzić, które próbkowania procent działa hello najlepsze w przypadku mojej aplikacji?*</span><span class="sxs-lookup"><span data-stu-id="9baba-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="9baba-274">Jednym ze sposobów jest toostart z adaptacyjną próbkowania, sprawdź, co Oceń to reguluje na (zobacz hello powyżej pytanie), a następnie przełącznika toofixed częstotliwość próbkowania przy użyciu tego kursu.</span><span class="sxs-lookup"><span data-stu-id="9baba-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="9baba-275">W przeciwnym razie należy tooguess.</span><span class="sxs-lookup"><span data-stu-id="9baba-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="9baba-276">Analizowanie bieżącego użycia telemetrii w AI, obserwować żadnego ograniczania przepustowości, czyli występujących i szacowania hello ilość danych telemetrycznych hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="9baba-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="9baba-277">Te trzy wejść, wraz z wybranej warstwy cenowej, sugerują, jaka może być tooreduce hello ilość danych telemetrycznych hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="9baba-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="9baba-278">Jednak wzrost liczby hello użytkowników lub niektóre shift, w hello ilość danych telemetrycznych może unieważnić oszacować.</span><span class="sxs-lookup"><span data-stu-id="9baba-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="9baba-279">*Co się stanie, jeśli można skonfigurować wartości procentowej pobierania próbek zbyt niska?*</span><span class="sxs-lookup"><span data-stu-id="9baba-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="9baba-280">Procent próbkowania zbyt niski (próbkowanie over-aggressive) zmniejsza hello dokładność przybliżenia hello toocompensate hello wizualizacji danych hello hello danych woluminu redukcji próbujący usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9baba-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="9baba-281">Ponadto czynności diagnostycznych może być obniżona, jako część hello rzadko niepowodzeniem lub powolne żądań próbkować można się.</span><span class="sxs-lookup"><span data-stu-id="9baba-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="9baba-282">*Co się stanie, jeśli można skonfigurować zbyt wysokiej wartości procentowej pobierania próbek?*</span><span class="sxs-lookup"><span data-stu-id="9baba-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="9baba-283">Konfigurowanie próbkowania zbyt wysoki procent (nie agresywne wystarczająco) powoduje niewystarczające redukcję ilości hello hello zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="9baba-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="9baba-284">Nadal może się okazać dane telemetryczne utraty danych związane z toothrottling i koszt hello przy użyciu usługi Application Insights mogą być wyższe niż planowana powodu toooverage opłat.</span><span class="sxs-lookup"><span data-stu-id="9baba-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="9baba-285">*Na platformach, które mogą używać próbkowania?*</span><span class="sxs-lookup"><span data-stu-id="9baba-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="9baba-286">Wprowadzanie próbkowanie może być spowodowany automatycznie dla dowolnego telemetrii powyżej woluminu hello zestawu SDK nie wykonuje próbkowanie.</span><span class="sxs-lookup"><span data-stu-id="9baba-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="9baba-287">To będzie działać, na przykład, jeśli aplikacja korzysta z serwera Java lub jeśli używasz starszej wersji hello zestawu SDK platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9baba-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="9baba-288">Jeśli używasz zestawu SDK platformy ASP.NET w wersji 2.0.0 lub nowszym (hostowanego na platformie Azure lub na danym serwerze), możesz uzyskać adaptacyjną próbkowania domyślnie, ale szybkość toofixed można przełączać się zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="9baba-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="9baba-289">Z włączonym próbkowaniem stałej stawki, hello przeglądarkę zestawu SDK automatycznie synchronizuje toosample zdarzenia związane z.</span><span class="sxs-lookup"><span data-stu-id="9baba-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="9baba-290">*Brak niektórych zdarzeń rzadkich zawsze ma toosee. Jak można je poza próbkowania hello modułu?*</span><span class="sxs-lookup"><span data-stu-id="9baba-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="9baba-291">Inicjowanie oddzielnego wystąpienia TelemetryClient z nowego TelemetryConfiguration (nie hello domyślnie aktywny).</span><span class="sxs-lookup"><span data-stu-id="9baba-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="9baba-292">Użyj tego toosend rzadkich zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9baba-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9baba-293">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9baba-293">Next steps</span></span>
* <span data-ttu-id="9baba-294">[Filtrowanie](app-insights-api-filtering-sampling.md) zapewniają więcej ścisłej kontroli wysyła zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9baba-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

