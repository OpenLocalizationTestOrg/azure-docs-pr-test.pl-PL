---
title: "aaaDebug aplikacji za pomocą usługi Azure Application Insights w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Analiza wydajności i diagnostyka aplikacji sieci Web podczas debugowania oraz w środowisku produkcyjnym."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="f549a-103">Debugowanie aplikacji przy użyciu usługi Azure Application Insights w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f549a-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="f549a-104">W programie Visual Studio (w wersji 2015 i nowszych) można analizować wydajność i diagnozować problemy w aplikacji sieci Web platformy ASP.NET zarówno podczas debugowania, jak i w środowisku produkcyjnym, przy użyciu telemetrii z usługi [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f549a-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="f549a-105">Jeśli utworzono aplikację sieci web ASP.NET przy użyciu programu Visual Studio 2017 lub później, jest już hello zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f549a-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="f549a-106">W przeciwnym razie, jeśli użytkownik jeszcze tego nie zrobiono, [dodać usługi Application Insights tooyour aplikację](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f549a-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="f549a-107">toomonitor aplikacji po jej w środowisku produkcyjnym na żywo, zwykle wyświetlić hello telemetrii usługi Application Insights w hello [portalu Azure](https://portal.azure.com), gdzie można ustawić alertów i zastosować zaawansowanych narzędzi monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f549a-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="f549a-108">Jednak do debugowania, możesz również wyszukiwania i analizować dane telemetryczne hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f549a-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="f549a-109">Używając telemetrii tooanalyze programu Visual Studio zarówno z lokacji produkcyjnych i debugowanie działa na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="f549a-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="f549a-110">W drugim przypadku hello można analizować debugowania działa nawet, jeśli jeszcze nie skonfigurowano hello SDK toosend telemetrii toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f549a-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="f549a-111"><a name="run"></a> Debugowanie projektu</span><span class="sxs-lookup"><span data-stu-id="f549a-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="f549a-112">Uruchom aplikację sieci Web w trybie debugowania lokalnego, naciskając klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="f549a-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="f549a-113">Otwórz niektóre dane telemetryczne toogenerate różnych stron.</span><span class="sxs-lookup"><span data-stu-id="f549a-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="f549a-114">W programie Visual Studio zobacz temat liczbę hello zdarzenia, które zostały zarejestrowane przez moduł usługi Application Insights hello w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f549a-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![W programie Visual Studio przycisk Application Insights hello pokazuje podczas debugowania.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="f549a-116">Kliknij ten przycisk toosearch telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f549a-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="f549a-117">Wyszukiwanie usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f549a-117">Application Insights search</span></span>
<span data-ttu-id="f549a-118">Okno wyszukiwania usługi Application Insights Hello zawiera zdarzenia, które zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="f549a-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="f549a-119">(Jeśli zalogowano tooAzure podczas konfigurowania usługi Application Insights, możesz wyszukać hello tego samego zdarzenia w portalu Azure hello.)</span><span class="sxs-lookup"><span data-stu-id="f549a-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Kliknij prawym przyciskiem myszy projekt hello i wybierz usługę Application Insights wyszukiwania](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="f549a-121">Po zaznaczeniu lub Anuluj wybór filtrów, kliknij przycisk wyszukiwania hello na końcu hello hello pole wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f549a-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="f549a-122">na wszystkie pola w zdarzeniach hello działa Hello dowolny tekst wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f549a-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="f549a-123">Na przykład wyszukać część hello adres URL strony; lub hello wartość właściwości, takie jak klient Miasto; lub słów w dzienniku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="f549a-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="f549a-124">Kliknij przycisk Właściwości szczegółowe toosee żadnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f549a-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="f549a-125">Dla żądania tooyour aplikacji sieci web możesz kliknąć za pośrednictwem toohello kodu.</span><span class="sxs-lookup"><span data-stu-id="f549a-125">For requests tooyour web app, you can click through toohello code.</span></span>

![W obszarze szczegółów żądania kliknij go, toohello kodu](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="f549a-127">Elementy pokrewne można również otworzyć toohelp diagnozowanie żądań zakończonych niepowodzeniem lub wyjątki.</span><span class="sxs-lookup"><span data-stu-id="f549a-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![W obszarze szczegółów żądania przewiń w dół toorelated elementów](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="f549a-129">Wyświetl wyjątki oraz nieudanych żądań.</span><span class="sxs-lookup"><span data-stu-id="f549a-129">View exceptions and failed requests</span></span>
<span data-ttu-id="f549a-130">Pokaż raporty wyjątek hello wyszukiwania okna.</span><span class="sxs-lookup"><span data-stu-id="f549a-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="f549a-131">(W niektórych starszych typów aplikacji sieci Web ASP.NET, należy za[monitorowania wyjątków](app-insights-asp-net-exceptions.md) toosee wyjątki, które są obsługiwane przez platformę hello.)</span><span class="sxs-lookup"><span data-stu-id="f549a-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="f549a-132">Kliknij przycisk tooget wyjątku, ślad stosu.</span><span class="sxs-lookup"><span data-stu-id="f549a-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="f549a-133">Jeśli kod aplikacji hello hello jest otwarty w programie Visual Studio, możesz kliknąć za pośrednictwem z hello stosu śledzenia toohello odpowiedni wiersz kodu hello.</span><span class="sxs-lookup"><span data-stu-id="f549a-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Ślad stosu wyjątków](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="f549a-135">Wyświetlanie podsumowań żądania i wyjątków w kodzie hello</span><span class="sxs-lookup"><span data-stu-id="f549a-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="f549a-136">W hello obiektyw kodu wiersz powyżej każdej metody obsługi można zobaczyć liczbę żądań hello i wyjątki zarejestrowane przez usługę Application Insights w ciągu ostatnich 24 godzin hello.</span><span class="sxs-lookup"><span data-stu-id="f549a-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Ślad stosu wyjątków](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="f549a-138">Obiektyw kod przedstawia tylko dane usługi Application Insights, jeśli masz [skonfigurowane portalem usługi Application Insights aplikacji toosend telemetrii toohello](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f549a-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="f549a-139">Więcej informacji o usłudze Application Insights w wierszach Code Lens</span><span class="sxs-lookup"><span data-stu-id="f549a-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="f549a-140">Trends</span><span class="sxs-lookup"><span data-stu-id="f549a-140">Trends</span></span>
<span data-ttu-id="f549a-141">Trends to narzędzie do wizualizacji zachowania aplikacji wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="f549a-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="f549a-142">Wybierz **Eksploruj trendy Telemetrii** z przycisku paska narzędzi Application Insights hello lub okno wyszukiwania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f549a-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="f549a-143">Wybierz jeden z pięciu tooget zapytania wspólnej pracy.</span><span class="sxs-lookup"><span data-stu-id="f549a-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="f549a-144">W zależności od typów telemetrii, zakresów czasu i innych właściwości możesz analizować różne zestawy danych .</span><span class="sxs-lookup"><span data-stu-id="f549a-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="f549a-145">anomalie toofind danych, wybierz jedną z opcji anomalii hello w obszarze rozwijanym "Typ widoku" hello.</span><span class="sxs-lookup"><span data-stu-id="f549a-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="f549a-146">Opcje filtrowania Hello u dołu okna hello hello był łatwo toohone w na konkretne podzestawy telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f549a-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="f549a-148">[Więcej informacji na temat narzędzia Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="f549a-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="f549a-149">Monitorowanie lokalne</span><span class="sxs-lookup"><span data-stu-id="f549a-149">Local monitoring</span></span>
<span data-ttu-id="f549a-150">(Z programu Visual Studio 2015 Update 2) Jeśli nie skonfigurowano portalu Application Insights toohello telemetrii toosend hello SDK (tak, aby klucz nie istnieje Instrumentacji w ApplicationInsights.config) okna diagnostyki hello wyświetla dane telemetryczne z sesji debugowania najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="f549a-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="f549a-151">Jest to pożądane, jeśli poprzednia wersji aplikacji została już opublikowana.</span><span class="sxs-lookup"><span data-stu-id="f549a-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="f549a-152">Nie chcesz telemetrii hello z Twojej debugowania toobe sesji łączyć z telemetrii hello na powitania portalu Application Insights z opublikowanych aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f549a-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="f549a-153">Jest również przydatne w przypadku niektórych [telemetria niestandardowa](app-insights-api-custom-events-metrics.md) mają toodebug przed wysłaniem danych telemetrycznych toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="f549a-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="f549a-154">*Na początku I w pełni skonfigurowane usługi Application Insights toosend telemetrii toohello portalu. A teraz chcesz I dane telemetryczne hello toosee tylko w programie Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="f549a-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="f549a-155">W ustawieniach okna wyszukiwania hello jest opcja toosearch lokalnego diagnostyki nawet wtedy, gdy aplikacja wysyła dane telemetryczne toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="f549a-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="f549a-156">dane telemetryczne toostop wysyłane toohello portalu komentarz linii hello `<instrumentationkey>...` z ApplicationInsights.config. Jeśli wszystko jest gotowe toosend telemetrii toohello portal Usuń komentarz.</span><span class="sxs-lookup"><span data-stu-id="f549a-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f549a-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f549a-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="f549a-158">**[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="f549a-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="f549a-159">Monitorowanie użycia, dostępności, zależności i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="f549a-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="f549a-160">Integrowanie śladów ze struktur rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="f549a-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="f549a-161">Zapisywanie niestandardowych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="f549a-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="f549a-163">**[Praca z portalu Application Insights hello](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="f549a-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="f549a-164">Wyświetlanie pulpitów nawigacyjnych, zaawansowanych narzędzi diagnostycznych i danych analitycznych, alerty, mapa na żywo zależności aplikacji i danych telemetrycznych wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="f549a-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

