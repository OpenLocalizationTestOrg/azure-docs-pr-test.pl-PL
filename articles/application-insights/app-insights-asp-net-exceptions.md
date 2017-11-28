---
title: "aaaDiagnose błędów i wyjątków w sieci web aplikacji za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przechwytywanie wyjątków w aplikacji ASP.NET oraz dane telemetryczne żądania."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="79e74-103">Diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="79e74-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="79e74-104">Wyjątki w aplikacji sieci web na żywo są zgłaszane przez [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79e74-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="79e74-105">Żądań zakończonych niepowodzeniem może być zgodne z wyjątków oraz inne zdarzenia na powitania klienta i serwera, dzięki czemu można szybko diagnozowania przyczyn hello.</span><span class="sxs-lookup"><span data-stu-id="79e74-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="79e74-106">Konfigurowanie zgłoszenie wyjątku</span><span class="sxs-lookup"><span data-stu-id="79e74-106">Set up exception reporting</span></span>
* <span data-ttu-id="79e74-107">toohave wyjątki zgłaszane przez aplikację serwera:</span><span class="sxs-lookup"><span data-stu-id="79e74-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="79e74-108">Zainstaluj [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w kodzie aplikacji lub</span><span class="sxs-lookup"><span data-stu-id="79e74-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="79e74-109">Serwery sieci web usług IIS: Uruchom [agenta Application Insights](app-insights-monitor-performance-live-website-now.md); lub</span><span class="sxs-lookup"><span data-stu-id="79e74-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="79e74-110">Aplikacje sieci web platformy Azure: Dodaj hello [rozszerzenie usługi Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="79e74-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="79e74-111">Aplikacje sieci web Java: hello instalacji [agenta Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="79e74-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="79e74-112">Zainstaluj hello [fragment kodu JavaScript](app-insights-javascript.md) w listy wyjątków przeglądarki toocatch stron sieci web.</span><span class="sxs-lookup"><span data-stu-id="79e74-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="79e74-113">W niektórych struktur aplikacji lub z niektórymi ustawieniami, potrzebujesz tootake toocatch pewnych dodatkowych czynności więcej wyjątków:</span><span class="sxs-lookup"><span data-stu-id="79e74-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="79e74-114">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="79e74-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="79e74-115">MVC</span><span class="sxs-lookup"><span data-stu-id="79e74-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="79e74-116">1.* interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="79e74-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="79e74-117">2.* interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="79e74-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="79e74-118">WCF</span><span class="sxs-lookup"><span data-stu-id="79e74-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="79e74-119">Diagnozowanie wyjątków przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79e74-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="79e74-120">Otwórz rozwiązanie aplikacji hello w Visual Studio toohelp z debugowaniem.</span><span class="sxs-lookup"><span data-stu-id="79e74-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="79e74-121">Uruchamianie aplikacji hello na serwerze lub na komputerze deweloperskim za pomocą F5.</span><span class="sxs-lookup"><span data-stu-id="79e74-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="79e74-122">Otwórz okno wyszukiwania usługi Application Insights hello w programie Visual Studio i skonfigurować go toodisplay zdarzeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79e74-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="79e74-123">Podczas debugowania kodu, możesz to zrobić, klikając przycisk Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="79e74-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Kliknij prawym przyciskiem myszy projekt hello i wybierz polecenie usługi Application Insights, Otwórz.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="79e74-125">Zwróć uwagę, filtrować hello raport tooshow tylko wyjątki.</span><span class="sxs-lookup"><span data-stu-id="79e74-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="79e74-126">*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="79e74-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="79e74-127">Kliknij jego ślad stosu wyjątku tooshow raportu.</span><span class="sxs-lookup"><span data-stu-id="79e74-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="79e74-128">Kliknij przycisk informacje w wierszu w hello ślad stosu, tooopen hello odpowiedni kod pliku.</span><span class="sxs-lookup"><span data-stu-id="79e74-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="79e74-129">W kodzie hello Zwróć uwagę, że CodeLens zawiera dane dotyczące wyjątków hello:</span><span class="sxs-lookup"><span data-stu-id="79e74-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Powiadomienie CodeLens wyjątków.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="79e74-131">Diagnozowanie błędów przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="79e74-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="79e74-132">Z przeglądu usługi Application Insights hello aplikacji, hello błędów kafelka zawiera wykresy wyjątków i nieudanych żądań HTTP, wraz z listą hello adresów URL żądań powodujących hello najczęstsze błędy.</span><span class="sxs-lookup"><span data-stu-id="79e74-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Wybierz ustawienia, błędów](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="79e74-134">Kliknij przycisk za pomocą jednego z hello nie typów wyjątków w hello listy tooget tooindividual wystąpień hello wyjątku, której można wyświetlić szczegóły hello i ślad stosu:</span><span class="sxs-lookup"><span data-stu-id="79e74-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Wybierz wystąpienie nieudanych żądań, a w obszarze szczegółów wyjątku, komunikat tooinstances hello wyjątek.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="79e74-136">**Alternatywnie** można uruchomić z listy hello żądań i Znajdź tooit powiązanych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="79e74-137">*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="79e74-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="79e74-138">I śledzenie niestandardowe dane dziennika</span><span class="sxs-lookup"><span data-stu-id="79e74-138">Custom tracing and log data</span></span>
<span data-ttu-id="79e74-139">tooget danych diagnostycznych tooyour określonych aplikacji, można wstawić kodu toosend danych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="79e74-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="79e74-140">To wyświetlane w diagnostycznych wyszukiwania obok hello żądania, widok strony i inne dane zbierane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="79e74-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="79e74-141">Istnieje kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="79e74-141">You have several options:</span></span>

* <span data-ttu-id="79e74-142">[Funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) jest zwykle używana do monitorowania wzorce użycia, ale hello dane wysyła również są wyświetlane w obszarze niestandardowe zdarzenia diagnostyczne wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="79e74-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="79e74-143">Zdarzenia są nazywane i mogą przenosić właściwości ciągu lub liczbowego metryki, w których można [filtru wyszukiwania diagnostycznych](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="79e74-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="79e74-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) pozwala wysyłać dane dłużej, takie jak informacje POST.</span><span class="sxs-lookup"><span data-stu-id="79e74-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="79e74-145">[Funkcji TrackException()](#exceptions) wysyła stos danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="79e74-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="79e74-146">[Więcej informacji na temat wyjątki](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="79e74-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="79e74-147">Jeśli używasz już struktury rejestrowania, takich jak Log4Net lub NLog, możesz [przechwytywania tych dzienników](app-insights-asp-net-trace-logs.md) i wyświetlać je w diagnostycznych wyszukiwania obok danych żądania i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="79e74-148">Otwórz te zdarzenia toosee [wyszukiwania](app-insights-diagnostic-search.md), otwórz filtru, a następnie wybierz Custom Event śledzenia i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="79e74-150">Jeśli aplikacja generuje wiele telemetrii, hello adaptacyjną próbkowania modułu automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="79e74-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="79e74-151">Zdarzenia, które są częścią hello tej samej operacji będzie być zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="79e74-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="79e74-152">Więcej informacji na temat pobierania próbek.</span><span class="sxs-lookup"><span data-stu-id="79e74-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="79e74-153">Jak toosee żądania POST danych</span><span class="sxs-lookup"><span data-stu-id="79e74-153">How toosee request POST data</span></span>
<span data-ttu-id="79e74-154">Szczegóły żądania nie zawierają danych hello wysyłane tooyour aplikacji w wywołaniu POST.</span><span class="sxs-lookup"><span data-stu-id="79e74-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="79e74-155">toohave zgłoszone dane:</span><span class="sxs-lookup"><span data-stu-id="79e74-155">toohave this data reported:</span></span>

* <span data-ttu-id="79e74-156">[Zainstaluj zestaw SDK hello](app-insights-asp-net.md) w projekcie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79e74-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="79e74-157">Wstawianie kodu w Twojej aplikacji toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="79e74-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="79e74-158">Wysyłanie danych POST hello w parametrze wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="79e74-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="79e74-159">Brak Ogranicz rozmiar toohello dozwolone, należy spróbować toosend hello tylko istotne dane.</span><span class="sxs-lookup"><span data-stu-id="79e74-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="79e74-160">Podczas badania, żądanie nie powiodło się, Znajdź hello skojarzone dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="79e74-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="79e74-162"><a name="exceptions"></a>Przechwytywanie wyjątków i powiązane dane diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="79e74-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="79e74-163">Na początku nie będą widzieć w portalu hello wszystkie wyjątki hello, których przyczyną błędów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79e74-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="79e74-164">Zobaczysz wszystkie wyjątki przeglądarki (Jeśli używasz hello [JavaScript SDK](app-insights-javascript.md) na stronach sieci web).</span><span class="sxs-lookup"><span data-stu-id="79e74-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="79e74-165">Jednak większość serwera wyjątki są przechwytywane przez usługi IIS i masz toowrite nieco toosee kodu je.</span><span class="sxs-lookup"><span data-stu-id="79e74-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="79e74-166">Możesz:</span><span class="sxs-lookup"><span data-stu-id="79e74-166">You can:</span></span>

* <span data-ttu-id="79e74-167">**Wyjątki rejestru jawnie** przez wstawienie kodu w wyjątkach hello tooreport programy obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="79e74-168">**Przechwytywanie wyjątków automatycznie** przez skonfigurowanie struktury programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="79e74-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="79e74-169">dodatki niezbędne Hello są różne dla różnych typów framework.</span><span class="sxs-lookup"><span data-stu-id="79e74-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="79e74-170">Raportowanie jawnie wyjątków</span><span class="sxs-lookup"><span data-stu-id="79e74-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="79e74-171">Witaj Najprostszym sposobem jest tooinsert tooTrackException() wywołania programu obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="79e74-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="79e74-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="79e74-173">C#</span><span class="sxs-lookup"><span data-stu-id="79e74-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="79e74-174">VB</span><span class="sxs-lookup"><span data-stu-id="79e74-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="79e74-175">Witaj właściwości i pomiarów parametry są opcjonalne, ale są przydatne w przypadku [filtrowanie i dodawanie](app-insights-diagnostic-search.md) dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="79e74-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="79e74-176">Na przykład jeśli aplikację można uruchomić kilka gier, można znaleźć wszystkie hello wyjątek raportów powiązanych tooa określonego gier.</span><span class="sxs-lookup"><span data-stu-id="79e74-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="79e74-177">Możesz dodać dowolną liczbę elementów podczas jak tooeach słownika.</span><span class="sxs-lookup"><span data-stu-id="79e74-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="79e74-178">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="79e74-178">Browser exceptions</span></span>
<span data-ttu-id="79e74-179">Większość przeglądarki wyjątki są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="79e74-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="79e74-180">Jeśli strony sieci web zawiera pliki skryptów z sieci dostarczania zawartości lub inne domeny, upewnij się, Twoje tag skryptu ma atrybut hello ```crossorigin="anonymous"```, i wysyła ten serwer hello [nagłówki CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="79e74-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="79e74-181">Dzięki temu będzie można tooget ślad stosu i szczegóły dla nieobsłużonych wyjątków JavaScript z tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="79e74-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="79e74-182">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="79e74-182">Web forms</span></span>
<span data-ttu-id="79e74-183">W formularzach sieci web hello moduł HTTP będą mogli toocollect hello wyjątki podczas nie ma żadnych przekierowuje skonfigurowano CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="79e74-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="79e74-184">Ale jeśli masz active przekierowuje dodać powitania po funkcji Application_Error toohello wiersze w Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="79e74-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="79e74-185">(Dodaj plik Global.asax, jeśli nie został wcześniej).</span><span class="sxs-lookup"><span data-stu-id="79e74-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="79e74-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="79e74-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="79e74-187">MVC</span><span class="sxs-lookup"><span data-stu-id="79e74-187">MVC</span></span>
<span data-ttu-id="79e74-188">Jeśli hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) konfiguracja jest `Off`, a następnie wyjątki będą dostępne dla hello [moduł HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="79e74-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="79e74-189">Jednak jeśli jest `RemoteOnly` (ustawienie domyślne) lub `On`, hello wyjątek zostanie wyczyszczony i zbierać tooautomatically nie są dostępne dla usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="79e74-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="79e74-190">Możesz rozwiązać ten problem, zastępowanie hello [klasy System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)i stosowanie hello przesłonięcia klasy, jak pokazano na powitania MVC wersje poniżej ([źródła github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="79e74-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="79e74-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="79e74-191">MVC 2</span></span>
<span data-ttu-id="79e74-192">Zastąp atrybutu HandleError hello nowy atrybut w kontrolerach.</span><span class="sxs-lookup"><span data-stu-id="79e74-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="79e74-193">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="79e74-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="79e74-194">MVC 3</span></span>
<span data-ttu-id="79e74-195">Zarejestruj `AiHandleErrorAttribute` jako filtr globalny w Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="79e74-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="79e74-196">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="79e74-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="79e74-197">MVC 4, MVC5</span></span>
<span data-ttu-id="79e74-198">AiHandleErrorAttribute rejestru jako filtr globalny w FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="79e74-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="79e74-199">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="79e74-200">Interfejs API sieci Web 1.x</span><span class="sxs-lookup"><span data-stu-id="79e74-200">Web API 1.x</span></span>
<span data-ttu-id="79e74-201">Zastąp System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="79e74-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="79e74-202">Możesz dodawania kontrolerów toospecific tego atrybutu przesłoniętej lub dodać toohello filtrów globalnych konfiguracji w klasa WebApiConfig hello:</span><span class="sxs-lookup"><span data-stu-id="79e74-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="79e74-203">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="79e74-204">Brak liczbę przypadków mogących hello filtry wyjątków nie może obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="79e74-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="79e74-205">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="79e74-205">For example:</span></span>

* <span data-ttu-id="79e74-206">Wyjątki generowane z konstruktorami kontrolera.</span><span class="sxs-lookup"><span data-stu-id="79e74-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="79e74-207">Wyjątków zgłaszanych przez programy obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="79e74-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="79e74-208">Wyjątki generowane podczas routingu.</span><span class="sxs-lookup"><span data-stu-id="79e74-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="79e74-209">Wyjątki generowane podczas serializacji treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="79e74-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="79e74-210">Interfejs API sieci Web 2.x</span><span class="sxs-lookup"><span data-stu-id="79e74-210">Web API 2.x</span></span>
<span data-ttu-id="79e74-211">Dodaj implementacji interfejsu IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="79e74-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="79e74-212">Dodaj ten usług toohello WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="79e74-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="79e74-213">}</span><span class="sxs-lookup"><span data-stu-id="79e74-213">}</span></span>

[<span data-ttu-id="79e74-214">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="79e74-215">Opis rozwiązań alternatywnych można:</span><span class="sxs-lookup"><span data-stu-id="79e74-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="79e74-216">Zastąp hello tylko ExceptionHandler niestandardowych implementacji IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="79e74-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="79e74-217">Jest to nazywane tylko, gdy hello framework jest nadal toochoose toosend (nie po hello połączenie zostało przerwane dla wystąpienia) komunikatu odpowiedzi, które</span><span class="sxs-lookup"><span data-stu-id="79e74-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="79e74-218">Filtry wyjątków (zgodnie z opisem w sekcji hello na kontrolerach 1.x interfejsu API sieci Web powyżej) — nie jest wywoływana we wszystkich przypadkach.</span><span class="sxs-lookup"><span data-stu-id="79e74-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="79e74-219">WCF</span><span class="sxs-lookup"><span data-stu-id="79e74-219">WCF</span></span>
<span data-ttu-id="79e74-220">Dodaj klasę Attribute i implementującą interfejsy IErrorHandler i IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="79e74-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="79e74-221">Dodaj implementacji usługi toohello atrybutu hello:</span><span class="sxs-lookup"><span data-stu-id="79e74-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="79e74-222">Próbki</span><span class="sxs-lookup"><span data-stu-id="79e74-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="79e74-223">Liczniki wydajności wyjątku</span><span class="sxs-lookup"><span data-stu-id="79e74-223">Exception performance counters</span></span>
<span data-ttu-id="79e74-224">Jeśli masz [zainstalowany Agent Insights aplikacji hello](app-insights-monitor-performance-live-website-now.md) na serwerze, można uzyskać wykresu hello wyjątki szybkości, mierząc .NET.</span><span class="sxs-lookup"><span data-stu-id="79e74-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="79e74-225">Dotyczy to zarówno obsłużonych i nieobsłużonych wyjątków .NET.</span><span class="sxs-lookup"><span data-stu-id="79e74-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="79e74-226">Otwiera blok Explorer metryki, Dodaj nowy wykres i wybierz **szybkość wyjątek**, to wymienione w obszarze liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="79e74-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="79e74-227">Hello .NET framework szybkość hello jest obliczana przez zliczanie hello liczba wyjątków w interwale i podzielenie przez długość interwału powitania hello.</span><span class="sxs-lookup"><span data-stu-id="79e74-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="79e74-228">Należy pamiętać, że będzie się różnił od obliczana przez portal usługi Application Insights hello na podstawie raportów TrackException liczba wyjątków"hello".</span><span class="sxs-lookup"><span data-stu-id="79e74-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="79e74-229">interwałami próbkowania Hello są różne, a hello zestawu SDK nie wysyłaj raportów TrackException wszystkich obsłużonych i nieobsłużonych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="79e74-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="79e74-230">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="79e74-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="79e74-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79e74-231">Next steps</span></span>
* [<span data-ttu-id="79e74-232">Monitorowanie REST, SQL i innych toodependencies wywołania</span><span class="sxs-lookup"><span data-stu-id="79e74-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="79e74-233">Czas ładowania strony monitora, wyjątki przeglądarki i wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="79e74-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="79e74-234">Liczniki Monitora wydajności</span><span class="sxs-lookup"><span data-stu-id="79e74-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
