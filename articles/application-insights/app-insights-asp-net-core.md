---
title: Application Insights dla platformy ASP.NET Core aaaAzure | Dokumentacja firmy Microsoft
description: "Monitorowanie aplikacji sieci web dla dostępności, wydajności i użycia."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="d0bd5-103">Usługa Application Insights dla aplikacji ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d0bd5-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="d0bd5-104">[Usługa Application Insights](app-insights-overview.md) umożliwia monitorowanie aplikacji sieci web, dostępności, wydajności i użycia.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="d0bd5-105">Opinii hello Ci o hello wydajność i skuteczność aplikacji w hello wild można wybrać opcje informowane o kierunku hello hello projektu w każdym cyklu programistycznym.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Przykład](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="d0bd5-107">Będziesz potrzebować subskrypcji z [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0bd5-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="d0bd5-108">Zaloguj się przy użyciu konta Microsoft, które możesz mieć dla systemu Windows, usługi XBox Live lub innych usług w chmurze firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="d0bd5-109">Zespół może mieć tooAzure organizacyjnej subskrypcji: hello właściciela tooadd poprosić tooit przy użyciu konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d0bd5-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d0bd5-110">Getting started</span></span>

* <span data-ttu-id="d0bd5-111">W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Konfiguruj usługę Application Insights**, lub **Dodaj > usługi Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="d0bd5-112">[Dowiedz się więcej](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="d0bd5-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="d0bd5-113">Jeśli nie widzisz tych poleceń menu, wykonaj hello [ręcznego pobierania Przewodnik wprowadzający](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="d0bd5-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="d0bd5-114">Może być konieczne toodo to jeżeli projekt został utworzony przy użyciu wersji programu Visual Studio przed 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="d0bd5-115">Korzystanie z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d0bd5-115">Using Application Insights</span></span>
<span data-ttu-id="d0bd5-116">Zaloguj się na powitania [portalu Microsoft Azure](https://portal.azure.com), wybierz pozycję **wszystkie zasoby** lub **usługi Application Insights**, a następnie wybierz zasób hello utworzenia toomonitor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="d0bd5-117">W osobnym oknie przeglądarki należy użyć aplikacji przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="d0bd5-118">Zostanie wyświetlone dane znajdujące się na wykresach usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="d0bd5-119">(Może być tooclick odświeżania). Będzie niewielką ilość danych podczas projektujesz, ale te wykresy naprawdę pochodzić aktywności podczas publikowania aplikacji i wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="d0bd5-120">Strona omówienia Hello zawiera wykresy wydajności: czas odpowiedzi serwera, czas ładowania strony i liczby żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="d0bd5-121">Kliknij przycisk toosee dowolnego wykresu, więcej wykresów i danych.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="d0bd5-122">Widoki w portalu hello dzielą się na trzy główne kategorie:</span><span class="sxs-lookup"><span data-stu-id="d0bd5-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="d0bd5-123">[Eksploratora metryk](app-insights-metrics-explorer.md) przedstawia wykres i tabelę metryki i liczby, takie jak czas reakcji, awariami lub metryki samodzielnie utworzony z hello [interfejsu API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d0bd5-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="d0bd5-124">Filtr segmentu hello dane i przez tooget wartości właściwości lepiej zrozumieć aplikacji i jej użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="d0bd5-125">[Eksplorator wyszukiwania](app-insights-diagnostic-search.md) zawiera listę poszczególnych zdarzeń, takich jak określone żądania, wyjątki, ślady dziennika lub zdarzenia utworzone samodzielnie z hello [interfejsu API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d0bd5-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="d0bd5-126">Filtrowanie wyszukiwania w zdarzeniach hello i nawigowanie między problemów tooinvestigate powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="d0bd5-127">[Analiza](app-insights-analytics.md) pozwala uruchamiać zapytania SQL przypominającej za pośrednictwem telemetrii i jest zaawansowanym narzędziem analityczne i diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="d0bd5-128">Alerty</span><span class="sxs-lookup"><span data-stu-id="d0bd5-128">Alerts</span></span>
* <span data-ttu-id="d0bd5-129">Automatycznie Pobierz [aktywne alerty diagnostycznych](app-insights-proactive-diagnostics.md) który informujące o nietypowych zmian awariami i innych metryk.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="d0bd5-130">Konfigurowanie [testów dostępności](app-insights-monitor-web-app-availability.md) tootest witryny sieci Web stale z lokalizacji na całym świecie i get wiadomości e-mail, gdy tylko jedną testowania kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="d0bd5-131">Konfigurowanie [metryki alerty](app-insights-monitor-web-app-availability.md) tooknow w przypadku metryk, takich jak czas odpowiedzi lub stawki wyjątek poza akceptowalnych limitów.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="d0bd5-132">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="d0bd5-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="d0bd5-133">Oprogramowanie typu „open source”</span><span class="sxs-lookup"><span data-stu-id="d0bd5-133">Open source</span></span>
[<span data-ttu-id="d0bd5-134">Przeczytaj i współtworzenia toohello kodu</span><span class="sxs-lookup"><span data-stu-id="d0bd5-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="d0bd5-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0bd5-135">Next steps</span></span>
* <span data-ttu-id="d0bd5-136">[Dodawanie stron sieci web tooyour telemetrii](app-insights-javascript.md) toomonitor strony użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="d0bd5-137">[Monitor zależności](app-insights-asp-net-dependencies.md) toosee gdy REST, SQL lub innych zasobów zewnętrznych powoduje spowolnienie użytkownik.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="d0bd5-138">[Za pomocą interfejsu API hello](app-insights-api-custom-events-metrics.md) toosend własne zdarzenia i metryki dla bardziej szczegółowy widok wydajności i użycia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="d0bd5-139">[Badania dostępności](app-insights-monitor-web-app-availability.md) Sprawdź aplikację stale z wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="d0bd5-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

