---
title: "Diagnozowanie błędów i wyjątków w aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="930c5-103">Diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="930c5-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="930c5-104">Wyjątki w aplikacji sieci web na żywo są zgłaszane przez [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="930c5-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="930c5-105">Żądań zakończonych niepowodzeniem może być zgodne z wyjątków i innych zdarzeń klienta i serwera, dzięki czemu można szybko diagnozowania przyczyn.</span><span class="sxs-lookup"><span data-stu-id="930c5-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="930c5-106">Konfigurowanie zgłoszenie wyjątku</span><span class="sxs-lookup"><span data-stu-id="930c5-106">Set up exception reporting</span></span>
* <span data-ttu-id="930c5-107">Istnieć wyjątki zgłoszone z aplikacji serwera:</span><span class="sxs-lookup"><span data-stu-id="930c5-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="930c5-108">Zainstaluj [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w kodzie aplikacji lub</span><span class="sxs-lookup"><span data-stu-id="930c5-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="930c5-109">Serwery sieci web usług IIS: Uruchom [agenta Application Insights](app-insights-monitor-performance-live-website-now.md); lub</span><span class="sxs-lookup"><span data-stu-id="930c5-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="930c5-110">Aplikacje sieci web platformy Azure: Dodaj [rozszerzenie usługi Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="930c5-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="930c5-111">Aplikacje sieci web Java: Zainstaluj [agenta Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="930c5-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="930c5-112">Zainstaluj [fragment kodu JavaScript](app-insights-javascript.md) na stronach sieci web, aby przechwytywać wyjątki przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="930c5-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="930c5-113">W niektórych struktur aplikacji lub z niektórych ustawień należy wykonać kilka dodatkowych czynności, aby przechwytywać wyjątki więcej:</span><span class="sxs-lookup"><span data-stu-id="930c5-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="930c5-114">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="930c5-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="930c5-115">MVC</span><span class="sxs-lookup"><span data-stu-id="930c5-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="930c5-116">1.* interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="930c5-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="930c5-117">2.* interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="930c5-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="930c5-118">WCF</span><span class="sxs-lookup"><span data-stu-id="930c5-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="930c5-119">Diagnozowanie wyjątków przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="930c5-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="930c5-120">Otwórz rozwiązanie aplikacji w programie Visual Studio, aby pomóc w debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="930c5-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="930c5-121">Uruchom aplikację, na serwerze lub na komputerze deweloperskim za pomocą F5.</span><span class="sxs-lookup"><span data-stu-id="930c5-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="930c5-122">Otwórz okno wyszukiwania usługi Application Insights w programie Visual Studio i ustawić go, aby wyświetlić zdarzenia z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="930c5-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="930c5-123">Podczas debugowania kodu, możesz to zrobić, klikając przycisk Application Insights.</span><span class="sxs-lookup"><span data-stu-id="930c5-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Kliknij prawym przyciskiem myszy projekt i wybierz polecenie usługi Application Insights, Otwórz.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="930c5-125">Zwróć uwagę, czy raport ma zawierać tylko wyjątki można filtrować.</span><span class="sxs-lookup"><span data-stu-id="930c5-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="930c5-126">*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="930c5-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="930c5-127">Kliknij raport do wyświetlenia jego ślad stosu.</span><span class="sxs-lookup"><span data-stu-id="930c5-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="930c5-128">Kliknij przycisk informacje w wierszu w ślad stosu, aby otworzyć plik odpowiedni kod.</span><span class="sxs-lookup"><span data-stu-id="930c5-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="930c5-129">W kodzie Zwróć uwagę, że CodeLens zawiera dane dotyczące wyjątków:</span><span class="sxs-lookup"><span data-stu-id="930c5-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Powiadomienie CodeLens wyjątków.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="930c5-131">Diagnozowanie błędów przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="930c5-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="930c5-132">Na stronie przeglądu usługi Application Insights aplikacji kafelka błędów Wyświetla wykresy wyjątków i nieudane żądania HTTP, wraz z listy żądania adresów URL, które powodują najczęstsze błędy.</span><span class="sxs-lookup"><span data-stu-id="930c5-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Wybierz ustawienia, błędów](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="930c5-134">Kliknij przycisk za pomocą jednego z typów wyjątku nie powiodło się na liście, aby uzyskać dostęp do poszczególnych wystąpień tego wyjątku, której można wyświetlić szczegóły i ślad stosu:</span><span class="sxs-lookup"><span data-stu-id="930c5-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Wybierz wystąpienie nieudanych żądań, a w obszarze szczegółów wyjątku, uzyskać dostęp do wystąpienia wyjątku.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="930c5-136">**Alternatywnie** można uruchomić z listy żądań i znaleźć wyjątki z nim związane.</span><span class="sxs-lookup"><span data-stu-id="930c5-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="930c5-137">*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="930c5-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="930c5-138">I śledzenie niestandardowe dane dziennika</span><span class="sxs-lookup"><span data-stu-id="930c5-138">Custom tracing and log data</span></span>
<span data-ttu-id="930c5-139">Aby uzyskać dane diagnostyczne specyficzne dla aplikacji, można wstawić kod, aby wysłać dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="930c5-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="930c5-140">To wyświetlane w diagnostycznych wyszukiwania obok żądania, widok strony i inne dane zbierane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="930c5-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="930c5-141">Istnieje kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="930c5-141">You have several options:</span></span>

* <span data-ttu-id="930c5-142">[Funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) jest zwykle używana do monitorowania wzorce użycia, ale dane wysyła również są wyświetlane w obszarze niestandardowych zdarzeń diagnostycznych wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="930c5-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="930c5-143">Zdarzenia są nazywane i mogą przenosić właściwości ciągu lub liczbowego metryki, w których można [filtru wyszukiwania diagnostycznych](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="930c5-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="930c5-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) pozwala wysyłać dane dłużej, takie jak informacje POST.</span><span class="sxs-lookup"><span data-stu-id="930c5-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="930c5-145">[Funkcji TrackException()](#exceptions) wysyła stos danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="930c5-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="930c5-146">[Więcej informacji na temat wyjątki](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="930c5-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="930c5-147">Jeśli używasz już struktury rejestrowania, takich jak Log4Net lub NLog, możesz [przechwytywania tych dzienników](app-insights-asp-net-trace-logs.md) i wyświetlać je w diagnostycznych wyszukiwania obok danych żądania i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="930c5-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="930c5-148">Aby wyświetlić te zdarzenia, otwórz [wyszukiwania](app-insights-diagnostic-search.md), otwórz filtru, a następnie wybierz Custom Event śledzenia i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="930c5-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="930c5-150">Jeśli aplikacja generuje wiele danych telemetrycznych, moduł próbkowania adaptacyjnego będzie automatycznie redukować ilość danych wysyłanych do portalu, wysyłając tylko ich reprezentatywną część.</span><span class="sxs-lookup"><span data-stu-id="930c5-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="930c5-151">Zdarzenia, które są częścią tej samej operacji zostanie wybrana lub zostanie usunięte zaznaczenie jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="930c5-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="930c5-152">Więcej informacji na temat pobierania próbek.</span><span class="sxs-lookup"><span data-stu-id="930c5-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="930c5-153">Jak wyświetlić dane POST na żądanie</span><span class="sxs-lookup"><span data-stu-id="930c5-153">How to see request POST data</span></span>
<span data-ttu-id="930c5-154">Szczegóły żądania nie zawierają danych wysłanych do aplikacji w wywołaniu POST.</span><span class="sxs-lookup"><span data-stu-id="930c5-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="930c5-155">Te dane są raportowane:</span><span class="sxs-lookup"><span data-stu-id="930c5-155">To have this data reported:</span></span>

* <span data-ttu-id="930c5-156">[Zainstaluj zestaw SDK](app-insights-asp-net.md) w projekcie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="930c5-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="930c5-157">Wstawianie kodu w aplikacji do wywołania [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="930c5-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="930c5-158">Wyślij dane POST w parametrze wiadomości.</span><span class="sxs-lookup"><span data-stu-id="930c5-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="930c5-159">Istnieje limit dozwolony rozmiar, dlatego powinna próbować wysłać tylko istotne dane.</span><span class="sxs-lookup"><span data-stu-id="930c5-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="930c5-160">Podczas badania, żądanie nie powiodło się, Znajdź skojarzone dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="930c5-160">When you investigate a failed request, find the associated traces.</span></span>  

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="930c5-162"><a name="exceptions"></a>Przechwytywanie wyjątków i powiązane dane diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="930c5-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="930c5-163">Na początku nie będą widzieć w portalu wszystkie wyjątki, które spowodować awarię aplikacji.</span><span class="sxs-lookup"><span data-stu-id="930c5-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="930c5-164">Zobaczysz wszystkie wyjątki przeglądarki (Jeśli używasz [JavaScript SDK](app-insights-javascript.md) na stronach sieci web).</span><span class="sxs-lookup"><span data-stu-id="930c5-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="930c5-165">Jednak większość serwera wyjątki są przechwytywane przez usługi IIS i trzeba napisać z bitowego kodu w celu zapoznania się z nimi.</span><span class="sxs-lookup"><span data-stu-id="930c5-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="930c5-166">Możesz:</span><span class="sxs-lookup"><span data-stu-id="930c5-166">You can:</span></span>

* <span data-ttu-id="930c5-167">**Wyjątki rejestru jawnie** przez wstawianie kodu do obsługi wyjątków, aby zgłosić wyjątki.</span><span class="sxs-lookup"><span data-stu-id="930c5-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="930c5-168">**Przechwytywanie wyjątków automatycznie** przez skonfigurowanie struktury programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="930c5-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="930c5-169">Dodatki niezbędne są różne dla różnych typów framework.</span><span class="sxs-lookup"><span data-stu-id="930c5-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="930c5-170">Raportowanie jawnie wyjątków</span><span class="sxs-lookup"><span data-stu-id="930c5-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="930c5-171">Najprostszym sposobem jest aby wstawić wywołań funkcji trackexception() obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="930c5-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="930c5-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="930c5-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="930c5-173">C#</span><span class="sxs-lookup"><span data-stu-id="930c5-173">C#</span></span>

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

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="930c5-174">VB</span><span class="sxs-lookup"><span data-stu-id="930c5-174">VB</span></span>

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

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="930c5-175">Właściwości i pomiarów parametry są opcjonalne, ale są przydatne w przypadku [filtrowanie i dodawanie](app-insights-diagnostic-search.md) dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="930c5-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="930c5-176">Na przykład jeśli aplikację można uruchomić kilka gier, można znaleźć wszystkie raporty wyjątek związane z określonym gier.</span><span class="sxs-lookup"><span data-stu-id="930c5-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="930c5-177">Możesz dodać dowolną liczbę elementów jak do każdego słownika.</span><span class="sxs-lookup"><span data-stu-id="930c5-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="930c5-178">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="930c5-178">Browser exceptions</span></span>
<span data-ttu-id="930c5-179">Większość przeglądarki wyjątki są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="930c5-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="930c5-180">Jeśli strony sieci web zawiera pliki skryptów z sieci dostarczania zawartości lub inne domeny, upewnij się, Twoje tag skryptu ma atrybut ```crossorigin="anonymous"```, oraz że serwer wysyła [nagłówki CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="930c5-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="930c5-181">Pozwoli to uzyskać ślad stosu i szczegóły dla nieobsłużonych wyjątków JavaScript z tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="930c5-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="930c5-182">Formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="930c5-182">Web forms</span></span>
<span data-ttu-id="930c5-183">W przypadku formularzy sieci web modułu HTTP będzie można zebrać wyjątki, kiedy nie ma żadnych przekierowuje skonfigurowano CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="930c5-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="930c5-184">Ale jeśli masz active przekierowania, Dodaj następujące wiersze do funkcji Application_Error w Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="930c5-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="930c5-185">(Dodaj plik Global.asax, jeśli nie został wcześniej).</span><span class="sxs-lookup"><span data-stu-id="930c5-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="930c5-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="930c5-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="930c5-187">MVC</span><span class="sxs-lookup"><span data-stu-id="930c5-187">MVC</span></span>
<span data-ttu-id="930c5-188">Jeśli [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) konfiguracja jest `Off`, a następnie wyjątki będą dostępne dla [moduł HTTP](https://msdn.microsoft.com/library/ms178468.aspx) do zbierania.</span><span class="sxs-lookup"><span data-stu-id="930c5-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="930c5-189">Jednak jeśli jest `RemoteOnly` (ustawienie domyślne) lub `On`, a następnie wyjątek zostanie wyczyszczony i nie są dostępne dla usługi Application Insights w celu automatycznego zbierania.</span><span class="sxs-lookup"><span data-stu-id="930c5-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="930c5-190">Możesz rozwiązać ten problem, zastępowanie [klasy System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)i stosowanie przesłoniętych klasy, jak pokazano poniżej różnych wersji MVC ([źródła github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="930c5-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report the exception
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

#### <a name="mvc-2"></a><span data-ttu-id="930c5-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="930c5-191">MVC 2</span></span>
<span data-ttu-id="930c5-192">Zastąp atrybutu HandleError Twojego nowy atrybut w kontrolerach.</span><span class="sxs-lookup"><span data-stu-id="930c5-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="930c5-193">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="930c5-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="930c5-194">MVC 3</span></span>
<span data-ttu-id="930c5-195">Zarejestruj `AiHandleErrorAttribute` jako filtr globalny w Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="930c5-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="930c5-196">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="930c5-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="930c5-197">MVC 4, MVC5</span></span>
<span data-ttu-id="930c5-198">AiHandleErrorAttribute rejestru jako filtr globalny w FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="930c5-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="930c5-199">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="930c5-200">Interfejs API sieci Web 1.x</span><span class="sxs-lookup"><span data-stu-id="930c5-200">Web API 1.x</span></span>
<span data-ttu-id="930c5-201">Zastąp System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="930c5-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="930c5-202">Możesz dodać ten atrybut przesłoniętej do określonych kontrolerów lub dodać je do konfiguracji filtrów globalnych klasy WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="930c5-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

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

[<span data-ttu-id="930c5-203">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="930c5-204">Istnieje wiele przypadków, które nie obsługują filtry wyjątków.</span><span class="sxs-lookup"><span data-stu-id="930c5-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="930c5-205">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="930c5-205">For example:</span></span>

* <span data-ttu-id="930c5-206">Wyjątki generowane z konstruktorami kontrolera.</span><span class="sxs-lookup"><span data-stu-id="930c5-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="930c5-207">Wyjątków zgłaszanych przez programy obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="930c5-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="930c5-208">Wyjątki generowane podczas routingu.</span><span class="sxs-lookup"><span data-stu-id="930c5-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="930c5-209">Wyjątki generowane podczas serializacji treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="930c5-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="930c5-210">Interfejs API sieci Web 2.x</span><span class="sxs-lookup"><span data-stu-id="930c5-210">Web API 2.x</span></span>
<span data-ttu-id="930c5-211">Dodaj implementacji interfejsu IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="930c5-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="930c5-212">Dodaj ją do usług w WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="930c5-212">Add this to the services in WebApiConfig:</span></span>

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
  <span data-ttu-id="930c5-213">}</span><span class="sxs-lookup"><span data-stu-id="930c5-213">}</span></span>

[<span data-ttu-id="930c5-214">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="930c5-215">Opis rozwiązań alternatywnych można:</span><span class="sxs-lookup"><span data-stu-id="930c5-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="930c5-216">Zamień tylko ExceptionHandler niestandardowej implementacji IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="930c5-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="930c5-217">Jest to nazywane tylko, gdy platformę jest nadal mogli wybrać które komunikat odpowiedzi do odesłania, (nie gdy połączenie zostało przerwane dla wystąpienia)</span><span class="sxs-lookup"><span data-stu-id="930c5-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="930c5-218">Filtry wyjątków (zgodnie z opisem w sekcji kontrolery 1.x interfejsu API sieci Web powyżej) — nie jest wywoływana we wszystkich przypadkach.</span><span class="sxs-lookup"><span data-stu-id="930c5-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="930c5-219">WCF</span><span class="sxs-lookup"><span data-stu-id="930c5-219">WCF</span></span>
<span data-ttu-id="930c5-220">Dodaj klasę Attribute i implementującą interfejsy IErrorHandler i IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="930c5-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="930c5-221">Dodaj atrybut do implementacji usługi:</span><span class="sxs-lookup"><span data-stu-id="930c5-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="930c5-222">Próbki</span><span class="sxs-lookup"><span data-stu-id="930c5-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="930c5-223">Liczniki wydajności wyjątku</span><span class="sxs-lookup"><span data-stu-id="930c5-223">Exception performance counters</span></span>
<span data-ttu-id="930c5-224">Jeśli masz [zainstalować agenta programu Application Insights](app-insights-monitor-performance-live-website-now.md) na serwerze, można uzyskać wykres wyjątki szybkości, mierząc .NET.</span><span class="sxs-lookup"><span data-stu-id="930c5-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="930c5-225">Dotyczy to zarówno obsłużonych i nieobsłużonych wyjątków .NET.</span><span class="sxs-lookup"><span data-stu-id="930c5-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="930c5-226">Otwiera blok Explorer metryki, Dodaj nowy wykres i wybierz **szybkość wyjątek**, to wymienione w obszarze liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="930c5-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="930c5-227">.NET framework oblicza stopę przez liczenie wyjątków w interwale i podzielenie przez długość interwału.</span><span class="sxs-lookup"><span data-stu-id="930c5-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="930c5-228">Należy pamiętać, że będzie się różnił od liczby "Wyjątków" obliczana na podstawie raportów TrackException przez portal usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="930c5-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="930c5-229">Interwałami próbkowania są różne, a zestaw SDK nie wysyła raporty TrackException wszystkie obsługiwane i nieobsługiwane wyjątki.</span><span class="sxs-lookup"><span data-stu-id="930c5-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="930c5-230">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="930c5-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="930c5-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="930c5-231">Next steps</span></span>
* [<span data-ttu-id="930c5-232">Monitorowanie REST, SQL i innych wywołania zależności</span><span class="sxs-lookup"><span data-stu-id="930c5-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="930c5-233">Czas ładowania strony monitora, wyjątki przeglądarki i wywołania AJAX</span><span class="sxs-lookup"><span data-stu-id="930c5-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="930c5-234">Liczniki Monitora wydajności</span><span class="sxs-lookup"><span data-stu-id="930c5-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
