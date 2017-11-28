---
title: "aaaHow wykonać... w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania w usłudze Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="32ac8-103">Jak mogę (...) w usłudze Application Insights?</span><span class="sxs-lookup"><span data-stu-id="32ac8-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="32ac8-104">Otrzymasz wiadomość e-mail, gdy...</span><span class="sxs-lookup"><span data-stu-id="32ac8-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="32ac8-105">Wiadomość e-mail, jeśli Moja witryna jest wyłączona</span><span class="sxs-lookup"><span data-stu-id="32ac8-105">Email if my site goes down</span></span>
<span data-ttu-id="32ac8-106">Ustaw [dostępności testu sieci web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="32ac8-107">Wyślij wiadomość e-mail, jeśli Moja witryna jest przeciążony</span><span class="sxs-lookup"><span data-stu-id="32ac8-107">Email if my site is overloaded</span></span>
<span data-ttu-id="32ac8-108">Ustaw [alert](app-insights-alerts.md) na **czas odpowiedzi serwera**.</span><span class="sxs-lookup"><span data-stu-id="32ac8-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="32ac8-109">Próg między 1 i 2 sekundy powinny działać.</span><span class="sxs-lookup"><span data-stu-id="32ac8-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="32ac8-110">Aplikacji mogą być również wyświetlane znaki obciążenie zwracając kod błędu.</span><span class="sxs-lookup"><span data-stu-id="32ac8-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="32ac8-111">Ustaw alert na **żądań zakończonych niepowodzeniem**.</span><span class="sxs-lookup"><span data-stu-id="32ac8-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="32ac8-112">Jeśli chcesz tooset alert na **wyjątki serwera**, może być toodo [niektóre dodatkowe ustawienia](app-insights-asp-net-exceptions.md) w kolejności toosee danych.</span><span class="sxs-lookup"><span data-stu-id="32ac8-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="32ac8-113">Wyślij wiadomość e-mail na wyjątki</span><span class="sxs-lookup"><span data-stu-id="32ac8-113">Email on exceptions</span></span>
1. [<span data-ttu-id="32ac8-114">Konfigurowanie monitorowania wyjątków</span><span class="sxs-lookup"><span data-stu-id="32ac8-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="32ac8-115">[Ustawić alert](app-insights-alerts.md) na powitania wyjątek liczba metryki</span><span class="sxs-lookup"><span data-stu-id="32ac8-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="32ac8-116">Wyślij wiadomość e-mail na zdarzenia w mojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="32ac8-116">Email on an event in my app</span></span>
<span data-ttu-id="32ac8-117">Załóżmy, że chcesz tooget wiadomość e-mail, gdy wystąpi określone zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="32ac8-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="32ac8-118">Usługi Application Insights nie obsługuje tej funkcji bezpośrednio, ale może [Wyślij alert, gdy metryki przekracza próg](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="32ac8-119">Alerty można ustawić na [metryki niestandardowe](app-insights-api-custom-events-metrics.md#trackmetric), ale nie niestandardowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="32ac8-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="32ac8-120">Metryka po wystąpieniu zdarzenia hello zapisu niektórych tooincrease kodu:</span><span class="sxs-lookup"><span data-stu-id="32ac8-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="32ac8-121">Lub:</span><span class="sxs-lookup"><span data-stu-id="32ac8-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="32ac8-122">Ponieważ alerty mają dwa stany, dostępne są toosend niskiej wartości należy wziąć pod uwagę alert hello toohave zakończone:</span><span class="sxs-lookup"><span data-stu-id="32ac8-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="32ac8-123">Tworzenie wykresu w [Eksploratora metryk](app-insights-metrics-explorer.md) toosee Twojego alarmu:</span><span class="sxs-lookup"><span data-stu-id="32ac8-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="32ac8-124">Teraz ustawić toofire alertu, gdy metryki hello wykraczają poza wartość mid przez krótki czas:</span><span class="sxs-lookup"><span data-stu-id="32ac8-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="32ac8-125">Ustaw hello uśrednianie minimum toohello okresu.</span><span class="sxs-lookup"><span data-stu-id="32ac8-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="32ac8-126">Zarówno Metryka hello systemowi powyżej i poniżej progu hello będziesz otrzymywać wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="32ac8-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="32ac8-127">Niektóre punkty tooconsider:</span><span class="sxs-lookup"><span data-stu-id="32ac8-127">Some points tooconsider:</span></span>

* <span data-ttu-id="32ac8-128">Alert ma dwa stany ("alertu" i "dobrej kondycji").</span><span class="sxs-lookup"><span data-stu-id="32ac8-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="32ac8-129">Stan Hello jest obliczane tylko wtedy, gdy otrzyma metryki.</span><span class="sxs-lookup"><span data-stu-id="32ac8-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="32ac8-130">Tylko wtedy, gdy zmieni się stan hello zostanie wysłana wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="32ac8-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="32ac8-131">Dlatego należy toosend wysoka i niska wartość metryki.</span><span class="sxs-lookup"><span data-stu-id="32ac8-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="32ac8-132">tooevaluate hello alertu, średnia hello jest zajęta wartości hello odebranych za pośrednictwem hello poprzedzający okres.</span><span class="sxs-lookup"><span data-stu-id="32ac8-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="32ac8-133">Występuje za każdym razem, gdy Metryka zostanie odebrana, więc częściej niż ustawiony okres hello można wysłać wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="32ac8-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="32ac8-134">Ponieważ wiadomości e-mail są wysyłane zarówno w "alertu" i "dobrej kondycji", można ponownie myśląc jednorazowej wydarzenia jako warunek dwustanowy tooconsider.</span><span class="sxs-lookup"><span data-stu-id="32ac8-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="32ac8-135">Na przykład zamiast zdarzenia "zadanie zostało ukończone", ma warunek "zadanie w toku", gdzie otrzymywać wiadomości e-mail na powitania rozpoczęcia i zakończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="32ac8-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="32ac8-136">Automatyczne konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="32ac8-136">Set up alerts automatically</span></span>
[<span data-ttu-id="32ac8-137">Użyj programu PowerShell toocreate nowe alerty</span><span class="sxs-lookup"><span data-stu-id="32ac8-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="32ac8-138">Użyj programu PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="32ac8-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="32ac8-139">Tworzenie nowych zasobów</span><span class="sxs-lookup"><span data-stu-id="32ac8-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="32ac8-140">Utwórz nowe alerty</span><span class="sxs-lookup"><span data-stu-id="32ac8-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="32ac8-141">Oddzielne dane telemetryczne z różnych wersji</span><span class="sxs-lookup"><span data-stu-id="32ac8-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="32ac8-142">Wiele ról w aplikacji: Użyj pojedynczego zasobu usługi Application Insights i odfiltrować cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="32ac8-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="32ac8-143">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="32ac8-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="32ac8-144">Oddzielanie programowanie, badanie i wersje: Korzystanie z różnych zasobów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="32ac8-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="32ac8-145">Wybierz klucze Instrumentacji hello z pliku web.config. [Dowiedz się więcej](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="32ac8-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="32ac8-146">Raportowanie kompilacji wersji: Dodawanie właściwości przy użyciu inicjatora telemetrii.</span><span class="sxs-lookup"><span data-stu-id="32ac8-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="32ac8-147">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="32ac8-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="32ac8-148">Monitorowanie serwerów wewnętrznej bazy danych i aplikacji klasycznych</span><span class="sxs-lookup"><span data-stu-id="32ac8-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="32ac8-149">[Moduł zestawu SDK serwera Windows hello użyj](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="32ac8-150">Wizualizuj dane</span><span class="sxs-lookup"><span data-stu-id="32ac8-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="32ac8-151">Pulpit nawigacyjny z metryki z wielu aplikacji</span><span class="sxs-lookup"><span data-stu-id="32ac8-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="32ac8-152">W [Explorer Metryka](app-insights-metrics-explorer.md)należy dostosować wykres i zapisać ją jako ulubioną.</span><span class="sxs-lookup"><span data-stu-id="32ac8-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="32ac8-153">Przypnij toohello pulpitu nawigacyjnego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="32ac8-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="32ac8-154">Pulpit nawigacyjny z danymi z innych źródeł i usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="32ac8-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="32ac8-155">[Eksportuj dane telemetryczne tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="32ac8-156">Lub</span><span class="sxs-lookup"><span data-stu-id="32ac8-156">Or</span></span>

* <span data-ttu-id="32ac8-157">Użyj programu SharePoint jako pulpitu nawigacyjnego, wyświetlanie danych w części sieci web programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="32ac8-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="32ac8-158">[Eksport ciągły i analiza strumienia tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="32ac8-159">Użyj bazy danych hello tooexamine PowerView i tworzenie składnika web part programu SharePoint dla PowerView.</span><span class="sxs-lookup"><span data-stu-id="32ac8-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="32ac8-160">Filtrowanie anonimowe lub uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="32ac8-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="32ac8-161">Jeśli użytkownicy logują się, możesz ustawić hello [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users). (Go nie jest realizowane automatycznie.)</span><span class="sxs-lookup"><span data-stu-id="32ac8-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="32ac8-162">Następnie możesz:</span><span class="sxs-lookup"><span data-stu-id="32ac8-162">You can then:</span></span>

* <span data-ttu-id="32ac8-163">Wyszukaj identyfikatorów określonego użytkownika</span><span class="sxs-lookup"><span data-stu-id="32ac8-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="32ac8-164">Filtruj metryki tooeither anonimowe lub uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="32ac8-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="32ac8-165">Modyfikowanie nazwy właściwości lub wartości</span><span class="sxs-lookup"><span data-stu-id="32ac8-165">Modify property names or values</span></span>
<span data-ttu-id="32ac8-166">Utwórz [filtru](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="32ac8-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="32ac8-167">Dzięki temu można zmodyfikować lub będzie filtrować dane telemetryczne przed wysłaniem z Twojej aplikacji tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="32ac8-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="32ac8-168">Listy poszczególnych użytkowników i ich użycia</span><span class="sxs-lookup"><span data-stu-id="32ac8-168">List specific users and their usage</span></span>
<span data-ttu-id="32ac8-169">Jeśli chcesz zbyt[wyszukiwanie określonych użytkowników](#search-specific-users), można ustawić hello [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="32ac8-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="32ac8-170">Jeśli chcesz listę użytkowników z danymi, takich jak strony przeglądania lub częstotliwość logowania, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="32ac8-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="32ac8-171">[Identyfikator użytkownika uwierzytelnionego zestawu](app-insights-api-custom-events-metrics.md#authenticated-users), [eksportu tooa bazy danych](app-insights-code-sample-export-sql-stream-analytics.md) i użyj odpowiednich narzędzi tooanalyze Brak danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32ac8-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="32ac8-172">Jeśli masz niewielką liczbę użytkowników, wysyłanie zdarzeń niestandardowych lub metryki, przy użyciu danych hello zainteresowania hello wartość metryki lub nazwa zdarzenia i identyfikator użytkownika hello ustawienie jako właściwość.</span><span class="sxs-lookup"><span data-stu-id="32ac8-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="32ac8-173">tooanalyze wyświetleń strony, Zastąp hello standardowe JavaScript trackPageView wywołania.</span><span class="sxs-lookup"><span data-stu-id="32ac8-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="32ac8-174">tooanalyze telemetrii po stronie serwera, użyj telemetrii inicjatora tooadd hello użytkownika identyfikator tooall serwera telemetrii.</span><span class="sxs-lookup"><span data-stu-id="32ac8-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="32ac8-175">Następnie można filtru i segmentu metryki i wyszukiwania na powitania identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32ac8-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="32ac8-176">Zmniejszenie ruchu z mojej tooApplication app Insights</span><span class="sxs-lookup"><span data-stu-id="32ac8-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="32ac8-177">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), wyłącz wszystkie moduły nie jest konieczne, takie zbierających dane licznika wydajności hello.</span><span class="sxs-lookup"><span data-stu-id="32ac8-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="32ac8-178">Użyj [próbkowania i filtrowanie](app-insights-api-filtering-sampling.md) na powitania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="32ac8-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="32ac8-179">Na stronach sieci web Ogranicz liczbę hello zgłoszone dla każdego widoku strony wywołania Ajax.</span><span class="sxs-lookup"><span data-stu-id="32ac8-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="32ac8-180">We fragmencie skryptu powitania po `instrumentationKey:...` , Wstaw: `,maxAjaxCallsPerView:3` (lub odpowiednią ilość).</span><span class="sxs-lookup"><span data-stu-id="32ac8-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="32ac8-181">Jeśli używasz [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), obliczeniowe agregacji hello partii wartości metryki przed wysłaniem hello wynik.</span><span class="sxs-lookup"><span data-stu-id="32ac8-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="32ac8-182">Brak przeciążenia TrackMetric() udostępniający tego.</span><span class="sxs-lookup"><span data-stu-id="32ac8-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="32ac8-183">Dowiedz się więcej o [ceny i przydziały](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="32ac8-184">Wyłączanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="32ac8-184">Disable telemetry</span></span>
<span data-ttu-id="32ac8-185">zbyt**dynamicznie zatrzymywania i uruchamiania** hello zbierania i przekazywania danych telemetrycznych z powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="32ac8-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="32ac8-186">zbyt**wyłączyć wybranego standardowe moduły zbierające** — na przykład liczniki wydajności, żądań HTTP lub zależności - Usuń lub komentarz hello odpowiednich wierszy w [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Można to zrobisz, na przykład, jeśli chcesz toosend danych TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="32ac8-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="32ac8-187">Przeglądanie liczników wydajności systemu</span><span class="sxs-lookup"><span data-stu-id="32ac8-187">View system performance counters</span></span>
<span data-ttu-id="32ac8-188">Wśród hello metryk, które można wyświetlić w Eksploratorze metryk to zbiór liczników wydajności systemu.</span><span class="sxs-lookup"><span data-stu-id="32ac8-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="32ac8-189">Jest wstępnie zdefiniowanych bloku zatytułowany **serwerów** wyświetlający kilka z nich.</span><span class="sxs-lookup"><span data-stu-id="32ac8-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Otwórz zasobu usługi Application Insights i kliknij pozycję serwery](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="32ac8-191">Jeśli zostanie wyświetlony nie danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="32ac8-191">If you see no performance counter data</span></span>
* <span data-ttu-id="32ac8-192">**Serwer usług IIS** na własnym komputerze lub na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32ac8-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="32ac8-193">[Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="32ac8-194">**Witryny sieci web Azure** — nie obsługujemy jeszcze liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="32ac8-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="32ac8-195">Istnieje kilka miar, który można uzyskać w ramach standardowego hello Azure witryny sieci web w Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="32ac8-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="32ac8-196">**Serwer UNIX** - [zainstalować collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="32ac8-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="32ac8-197">toodisplay większej liczby liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="32ac8-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="32ac8-198">Najpierw [Dodaj nowy wykres](app-insights-metrics-explorer.md) i zobacz, jeśli licznik hello w hello podstawowe ustawiono firma Microsoft oferuje.</span><span class="sxs-lookup"><span data-stu-id="32ac8-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="32ac8-199">Jeśli nie, [dodać zestaw toohello liczników hello zebrane przez moduł licznika wydajności hello](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="32ac8-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
