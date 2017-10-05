---
title: "Debugowanie aplikacji z usługą Azure Application Insights w programie Visual Studio | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="f65c1-103">Debugowanie aplikacji przy użyciu usługi Azure Application Insights w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f65c1-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="f65c1-104">W programie Visual Studio (w wersji 2015 i nowszych) można analizować wydajność i diagnozować problemy w aplikacji sieci Web platformy ASP.NET zarówno podczas debugowania, jak i w środowisku produkcyjnym, przy użyciu telemetrii z usługi [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f65c1-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="f65c1-105">Jeśli aplikację sieci Web platformy ASP.NET utworzono przy użyciu programu Visual Studio 2017 lub nowszego, zawiera już ona zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f65c1-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="f65c1-106">W przeciwnym razie, jeśli jeszcze tego nie zrobiono, należy [dodać usługę Application Insights do aplikacji](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f65c1-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="f65c1-107">Monitorowanie aplikacji w środowisku produkcyjnym zwykle polega na przeglądaniu danych telemetrycznych z usługi Application Insights w witrynie [Azure Portal](https://portal.azure.com), w której można ustawiać alerty i stosować zaawansowane narzędzia do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f65c1-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="f65c1-108">Jednak na potrzeby debugowania można również wyszukiwać i analizować dane telemetryczne w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f65c1-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="f65c1-109">Visual Studio umożliwia analizowanie danych telemetrycznych zarówno z lokacji produkcyjnych i debugowanie działa na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="f65c1-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="f65c1-110">W tym ostatnim przypadku można analizować przebiegi debugowania, nawet jeśli nie skonfigurowano jeszcze zestawu SDK na potrzeby wysyłania danych telemetrycznych do witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f65c1-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="f65c1-111"><a name="run"></a> Debugowanie projektu</span><span class="sxs-lookup"><span data-stu-id="f65c1-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="f65c1-112">Uruchom aplikację sieci Web w trybie debugowania lokalnego, naciskając klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="f65c1-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="f65c1-113">Otwórz różne strony w celu wygenerowania telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f65c1-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="f65c1-114">W programie Visual Studio zobacz temat liczbę zdarzeń, które zostały zarejestrowane przez moduł usługi Application Insights w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f65c1-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![Przycisk usługi Application Insights jest widoczny w programie Visual Studio podczas debugowania.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="f65c1-116">Kliknij ten przycisk, aby wyszukać dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="f65c1-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="f65c1-117">Wyszukiwanie usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f65c1-117">Application Insights search</span></span>
<span data-ttu-id="f65c1-118">Okno wyszukiwania usługi Application Insights pokazuje zarejestrowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f65c1-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="f65c1-119">(Jeśli użytkownik zarejestrowany w usłudze Azure podczas konfigurowania usługi Application Insights, można wyszukiwać tego samego zdarzenia w portalu Azure.)</span><span class="sxs-lookup"><span data-stu-id="f65c1-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Kliknij prawym przyciskiem myszy projekt i wybierz kolejno opcje Application Insights, Wyszukiwanie](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="f65c1-121">Po wybraniu lub anulowaniu wyboru filtrów kliknij przycisk wyszukiwania na końcu tekstowego pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f65c1-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="f65c1-122">Wyszukiwanie dowolnego tekstu działa we wszystkich polach zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f65c1-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="f65c1-123">Można wyszukać na przykład część adresu URL strony, wartość właściwości (taką jak miasto klienta) lub określone słowa w dzienniku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="f65c1-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="f65c1-124">Kliknij dowolne zdarzenie, aby wyświetlić jego szczegółowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="f65c1-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="f65c1-125">W celu wyświetlenia żądań wysyłanych do aplikacji sieci Web można kliknąć w obrębie kodu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-125">For requests to your web app, you can click through to the code.</span></span>

![W obszarze Szczegóły żądania kliknij w obrębie kodu](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="f65c1-127">Można również otworzyć elementy pokrewne, aby łatwiej diagnozować niepowodzenia żądań lub wyjątki.</span><span class="sxs-lookup"><span data-stu-id="f65c1-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![W obszarze Szczegóły żądania przewiń w dół do elementów pokrewnych](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="f65c1-129">Wyświetl wyjątki oraz nieudanych żądań.</span><span class="sxs-lookup"><span data-stu-id="f65c1-129">View exceptions and failed requests</span></span>
<span data-ttu-id="f65c1-130">Raporty dotyczące wyjątków są wyświetlane w oknie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f65c1-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="f65c1-131">W niektórych starszych typach aplikacji sieci Web platformy ASP.NET trzeba [skonfigurować monitorowanie wyjątków](app-insights-asp-net-exceptions.md), aby zobaczyć wyjątki, które są obsługiwane przez architekturę.</span><span class="sxs-lookup"><span data-stu-id="f65c1-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="f65c1-132">Kliknij wyjątek, aby uzyskać ślad stosu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="f65c1-133">Jeśli kod aplikacji jest otwarty w programie Visual Studio, można przejść przez ślad stosu do odpowiedniego wiersza kodu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Ślad stosu wyjątków](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="f65c1-135">Wyświetlanie podsumowań żądania i wyjątków w kodzie</span><span class="sxs-lookup"><span data-stu-id="f65c1-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="f65c1-136">W wierszu kodu obiektyw powyżej każdej metody obsługi można zobaczyć liczbę żądań i wyjątki zarejestrowane przez usługę Application Insights w ciągu ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="f65c1-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Ślad stosu wyjątków](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="f65c1-138">Dane usługi Application Insights są wyświetlane w wierszach Code Lens tylko wtedy, gdy [skonfigurowano aplikację na potrzeby wysyłania danych telemetrycznych do portalu usługi Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f65c1-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="f65c1-139">Więcej informacji o usłudze Application Insights w wierszach Code Lens</span><span class="sxs-lookup"><span data-stu-id="f65c1-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="f65c1-140">Trends</span><span class="sxs-lookup"><span data-stu-id="f65c1-140">Trends</span></span>
<span data-ttu-id="f65c1-141">Trends to narzędzie do wizualizacji zachowania aplikacji wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="f65c1-142">Na przycisku paska narzędzi Application Insights lub w oknie Application Insights Search wybierz pozycję **Eksploruj trendy telemetryczne**.</span><span class="sxs-lookup"><span data-stu-id="f65c1-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="f65c1-143">Wybierz jedno z pięciu typowych zapytań, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="f65c1-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="f65c1-144">W zależności od typów telemetrii, zakresów czasu i innych właściwości możesz analizować różne zestawy danych .</span><span class="sxs-lookup"><span data-stu-id="f65c1-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="f65c1-145">Aby znaleźć anomalie w danych, wybierz jedną z opcji anomalii w menu rozwijanym „Typ widoku”.</span><span class="sxs-lookup"><span data-stu-id="f65c1-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="f65c1-146">Opcje filtrowania u dołu okna ułatwiają sprecyzowanie konkretnych podzestawów w telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f65c1-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="f65c1-148">[Więcej informacji na temat narzędzia Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="f65c1-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="f65c1-149">Monitorowanie lokalne</span><span class="sxs-lookup"><span data-stu-id="f65c1-149">Local monitoring</span></span>
<span data-ttu-id="f65c1-150">(Z programu Visual Studio 2015 Update 2) Jeśli nie skonfigurowano zestaw SDK, aby wysłać dane telemetryczne do portalu usługi Application Insights (tak, aby klucz nie istnieje Instrumentacji w ApplicationInsights.config) oknie diagnostyki wyświetla dane telemetryczne z sesji debugowania najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="f65c1-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="f65c1-151">Jest to pożądane, jeśli poprzednia wersji aplikacji została już opublikowana.</span><span class="sxs-lookup"><span data-stu-id="f65c1-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="f65c1-152">Lepiej, aby telemetria z sesji debugowania nie była mieszana z telemetrią z opublikowanej aplikacji w portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f65c1-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="f65c1-153">Jest to również przydatne, jeśli masz trochę [niestandardowej telemetrii](app-insights-api-custom-events-metrics.md), którą chcesz debugować przed wysłaniem telemetrii do portalu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="f65c1-154">*Na początku usługa Application Insights została skonfigurowana do wysyłania telemetrii do portalu, ale teraz chcę widzieć telemetrię tylko w programie Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="f65c1-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="f65c1-155">W ustawieniach okna wyszukiwania istnieje możliwość wyszukiwania lokalnych danych diagnostycznych, nawet jeśli aplikacja wysyła telemetrię do portalu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="f65c1-156">Aby zatrzymać przesyłanie telemetrii do portalu, zakomentuj wiersz `<instrumentationkey>...` w pliku ApplicationInsights.config. Gdy wszystko będzie gotowe, odkomentuj wiersz, aby wznowić wysyłanie telemetrii do portalu.</span><span class="sxs-lookup"><span data-stu-id="f65c1-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f65c1-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f65c1-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="f65c1-158">**[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="f65c1-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="f65c1-159">Monitorowanie użycia, dostępności, zależności i wyjątków.</span><span class="sxs-lookup"><span data-stu-id="f65c1-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="f65c1-160">Integrowanie śladów ze struktur rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="f65c1-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="f65c1-161">Zapisywanie niestandardowych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="f65c1-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="f65c1-163">**[Praca z portalem usługi Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="f65c1-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="f65c1-164">Wyświetlanie pulpitów nawigacyjnych, zaawansowanych narzędzi diagnostycznych i danych analitycznych, alerty, mapa na żywo zależności aplikacji i danych telemetrycznych wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="f65c1-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

