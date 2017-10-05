---
title: "Jak... w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="156f6-103">Jak mogę (...) w usłudze Application Insights?</span><span class="sxs-lookup"><span data-stu-id="156f6-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="156f6-104">Otrzymasz wiadomość e-mail, gdy...</span><span class="sxs-lookup"><span data-stu-id="156f6-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="156f6-105">Wiadomość e-mail, jeśli Moja witryna jest wyłączona</span><span class="sxs-lookup"><span data-stu-id="156f6-105">Email if my site goes down</span></span>
<span data-ttu-id="156f6-106">Ustaw [dostępności testu sieci web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="156f6-107">Wyślij wiadomość e-mail, jeśli Moja witryna jest przeciążony</span><span class="sxs-lookup"><span data-stu-id="156f6-107">Email if my site is overloaded</span></span>
<span data-ttu-id="156f6-108">Ustaw [alert](app-insights-alerts.md) na **czas odpowiedzi serwera**.</span><span class="sxs-lookup"><span data-stu-id="156f6-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="156f6-109">Próg między 1 i 2 sekundy powinny działać.</span><span class="sxs-lookup"><span data-stu-id="156f6-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="156f6-110">Aplikacji mogą być również wyświetlane znaki obciążenie zwracając kod błędu.</span><span class="sxs-lookup"><span data-stu-id="156f6-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="156f6-111">Ustaw alert na **żądań zakończonych niepowodzeniem**.</span><span class="sxs-lookup"><span data-stu-id="156f6-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="156f6-112">Jeśli chcesz ustawić alert na **wyjątki serwera**, może być konieczne przeprowadzenie [niektóre dodatkowe ustawienia](app-insights-asp-net-exceptions.md) Aby wyświetlić dane.</span><span class="sxs-lookup"><span data-stu-id="156f6-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="156f6-113">Wyślij wiadomość e-mail na wyjątki</span><span class="sxs-lookup"><span data-stu-id="156f6-113">Email on exceptions</span></span>
1. [<span data-ttu-id="156f6-114">Konfigurowanie monitorowania wyjątków</span><span class="sxs-lookup"><span data-stu-id="156f6-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="156f6-115">[Ustawić alert](app-insights-alerts.md) na wyjątku liczba metryki</span><span class="sxs-lookup"><span data-stu-id="156f6-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="156f6-116">Wyślij wiadomość e-mail na zdarzenia w mojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="156f6-116">Email on an event in my app</span></span>
<span data-ttu-id="156f6-117">Załóżmy, że chcesz otrzymasz wiadomość e-mail, gdy wystąpi określone zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="156f6-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="156f6-118">Usługi Application Insights nie obsługuje tej funkcji bezpośrednio, ale może [Wyślij alert, gdy metryki przekracza próg](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="156f6-119">Alerty można ustawić na [metryki niestandardowe](app-insights-api-custom-events-metrics.md#trackmetric), ale nie niestandardowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="156f6-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="156f6-120">Napisanie kodu, aby zwiększyć metrykę, gdy wystąpi zdarzenie:</span><span class="sxs-lookup"><span data-stu-id="156f6-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="156f6-121">Lub:</span><span class="sxs-lookup"><span data-stu-id="156f6-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="156f6-122">Ponieważ alerty mają dwa stany, konieczne będzie wysyłać niską wartość, gdy należy wziąć pod uwagę w alercie, aby zostać zakończone:</span><span class="sxs-lookup"><span data-stu-id="156f6-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="156f6-123">Tworzenie wykresu w [Eksploratora metryk](app-insights-metrics-explorer.md) wyświetlić Twojej alarmu:</span><span class="sxs-lookup"><span data-stu-id="156f6-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="156f6-124">Teraz ustawić alert, aby zostać wywołane podczas Metryka wykraczają poza wartość mid przez krótki czas:</span><span class="sxs-lookup"><span data-stu-id="156f6-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="156f6-125">Ustaw okres uśredniania do minimum.</span><span class="sxs-lookup"><span data-stu-id="156f6-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="156f6-126">Będziesz otrzymywać wiadomości e-mail, zarówno Metryka systemowi powyżej i poniżej progu.</span><span class="sxs-lookup"><span data-stu-id="156f6-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="156f6-127">Niektóre kwestie do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="156f6-127">Some points to consider:</span></span>

* <span data-ttu-id="156f6-128">Alert ma dwa stany ("alertu" i "dobrej kondycji").</span><span class="sxs-lookup"><span data-stu-id="156f6-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="156f6-129">Stan jest oceniane tylko wtedy, gdy otrzyma metryki.</span><span class="sxs-lookup"><span data-stu-id="156f6-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="156f6-130">Wiadomości e-mail są wysyłane tylko wtedy, gdy stan zmieni się.</span><span class="sxs-lookup"><span data-stu-id="156f6-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="156f6-131">Jest to Dlaczego należy wysyłać wysokiej i niskiej wartości metryki.</span><span class="sxs-lookup"><span data-stu-id="156f6-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="156f6-132">Aby ocenić ten alert, średnia jest pobierana odebranej wartości w poprzednim okresie.</span><span class="sxs-lookup"><span data-stu-id="156f6-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="156f6-133">Występuje za każdym razem, gdy Metryka zostanie odebrana, więc częściej niż okres, w którym można ustawić można wysłać wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="156f6-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="156f6-134">Ponieważ wiadomości e-mail są wysyłane zarówno w "alertu" i "dobrej kondycji", można rozważyć ponowne myśląc jednorazowej wydarzenia jako warunek dwustanowy.</span><span class="sxs-lookup"><span data-stu-id="156f6-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="156f6-135">Na przykład zamiast "zadanie ukończone" zdarzenia, mieć warunek "zadanie w toku", gdzie otrzymywać wiadomości e-mail na początku i na końcu zadania.</span><span class="sxs-lookup"><span data-stu-id="156f6-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="156f6-136">Automatyczne konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="156f6-136">Set up alerts automatically</span></span>
[<span data-ttu-id="156f6-137">Użyj programu PowerShell, aby utworzyć nowe alerty</span><span class="sxs-lookup"><span data-stu-id="156f6-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="156f6-138">Za pomocą programu PowerShell do zarządzania usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="156f6-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="156f6-139">Tworzenie nowych zasobów</span><span class="sxs-lookup"><span data-stu-id="156f6-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="156f6-140">Utwórz nowe alerty</span><span class="sxs-lookup"><span data-stu-id="156f6-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="156f6-141">Oddzielne dane telemetryczne z różnych wersji</span><span class="sxs-lookup"><span data-stu-id="156f6-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="156f6-142">Wiele ról w aplikacji: Użyj pojedynczego zasobu usługi Application Insights i odfiltrować cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="156f6-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="156f6-143">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="156f6-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="156f6-144">Oddzielanie programowanie, badanie i wersje: Korzystanie z różnych zasobów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="156f6-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="156f6-145">Wybierz klucze Instrumentacji z pliku web.config. [Dowiedz się więcej](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="156f6-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="156f6-146">Raportowanie kompilacji wersji: Dodawanie właściwości przy użyciu inicjatora telemetrii.</span><span class="sxs-lookup"><span data-stu-id="156f6-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="156f6-147">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="156f6-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="156f6-148">Monitorowanie serwerów wewnętrznej bazy danych i aplikacji klasycznych</span><span class="sxs-lookup"><span data-stu-id="156f6-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="156f6-149">[Użyć modułu programu Windows Server SDK](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="156f6-150">Wizualizuj dane</span><span class="sxs-lookup"><span data-stu-id="156f6-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="156f6-151">Pulpit nawigacyjny z metryki z wielu aplikacji</span><span class="sxs-lookup"><span data-stu-id="156f6-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="156f6-152">W [Explorer Metryka](app-insights-metrics-explorer.md)należy dostosować wykres i zapisać ją jako ulubioną.</span><span class="sxs-lookup"><span data-stu-id="156f6-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="156f6-153">Przypiąć go do pulpitu nawigacyjnego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="156f6-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="156f6-154">Pulpit nawigacyjny z danymi z innych źródeł i usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="156f6-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="156f6-155">[Eksportuj dane telemetryczne do usługi Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="156f6-156">Lub</span><span class="sxs-lookup"><span data-stu-id="156f6-156">Or</span></span>

* <span data-ttu-id="156f6-157">Użyj programu SharePoint jako pulpitu nawigacyjnego, wyświetlanie danych w części sieci web programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="156f6-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="156f6-158">[Za pomocą Eksport ciągły i Stream Analytics można wyeksportować do bazy danych SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="156f6-159">Użyj PowerView Sprawdź bazy danych i tworzenie składnika web part programu SharePoint dla PowerView.</span><span class="sxs-lookup"><span data-stu-id="156f6-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="156f6-160">Filtrowanie anonimowe lub uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="156f6-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="156f6-161">Jeśli użytkownicy logują się, możesz ustawić [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users). (Go nie jest realizowane automatycznie.)</span><span class="sxs-lookup"><span data-stu-id="156f6-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="156f6-162">Następnie możesz:</span><span class="sxs-lookup"><span data-stu-id="156f6-162">You can then:</span></span>

* <span data-ttu-id="156f6-163">Wyszukaj identyfikatorów określonego użytkownika</span><span class="sxs-lookup"><span data-stu-id="156f6-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="156f6-164">Metryki filtr do anonimowych lub uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="156f6-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="156f6-165">Modyfikowanie nazwy właściwości lub wartości</span><span class="sxs-lookup"><span data-stu-id="156f6-165">Modify property names or values</span></span>
<span data-ttu-id="156f6-166">Utwórz [filtru](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="156f6-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="156f6-167">Dzięki temu można zmodyfikować lub będzie filtrować dane telemetryczne przed wysłaniem go z aplikacji do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="156f6-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="156f6-168">Listy poszczególnych użytkowników i ich użycia</span><span class="sxs-lookup"><span data-stu-id="156f6-168">List specific users and their usage</span></span>
<span data-ttu-id="156f6-169">Jeśli chcesz, aby [wyszukiwanie określonych użytkowników](#search-specific-users), można ustawić [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="156f6-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="156f6-170">Jeśli chcesz listę użytkowników z danymi, takich jak strony przeglądania lub częstotliwość logowania, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="156f6-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="156f6-171">[Identyfikator użytkownika uwierzytelnionego zestawu](app-insights-api-custom-events-metrics.md#authenticated-users), [wyeksportować do bazy danych](app-insights-code-sample-export-sql-stream-analytics.md) i użyć odpowiedniego narzędzia do analizowania danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="156f6-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="156f6-172">Jeśli masz niewielką liczbę użytkowników, wysyłanie zdarzeń niestandardowych lub metryki, przy użyciu potrzebne dane jako nazwa metryki wartość lub zdarzenie, a ustawienie użytkownika jako właściwość.</span><span class="sxs-lookup"><span data-stu-id="156f6-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="156f6-173">Do analizowania wyświetleń strony, Zastąp standardowe wywołanie trackPageView JavaScript.</span><span class="sxs-lookup"><span data-stu-id="156f6-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="156f6-174">Do analizowania telemetrii po stronie serwera, użyj inicjatora telemetrii, aby dodać identyfikator użytkownika do wszystkie dane telemetryczne serwera.</span><span class="sxs-lookup"><span data-stu-id="156f6-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="156f6-175">Następnie można filtru i segmentu metryki i wyszukiwania identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="156f6-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="156f6-176">Zmniejszenie ruchu z mojej aplikacji do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="156f6-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="156f6-177">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), wyłącz wszystkie moduły nie jest konieczne, takie zbierającym licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="156f6-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="156f6-178">Użyj [próbkowania i filtrowanie](app-insights-api-filtering-sampling.md) w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="156f6-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="156f6-179">Na stronach sieci web limitu liczby wywołań Ajax zgłoszone dla każdego widoku strony.</span><span class="sxs-lookup"><span data-stu-id="156f6-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="156f6-180">We fragmencie kodu skryptu po `instrumentationKey:...` , Wstaw: `,maxAjaxCallsPerView:3` (lub odpowiednią ilość).</span><span class="sxs-lookup"><span data-stu-id="156f6-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="156f6-181">Jeśli używasz [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), obliczeniowe agregacji partie wartości metryki przed wysłaniem wynik.</span><span class="sxs-lookup"><span data-stu-id="156f6-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="156f6-182">Brak przeciążenia TrackMetric() udostępniający tego.</span><span class="sxs-lookup"><span data-stu-id="156f6-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="156f6-183">Dowiedz się więcej o [ceny i przydziały](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="156f6-184">Wyłączanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="156f6-184">Disable telemetry</span></span>
<span data-ttu-id="156f6-185">Aby **dynamicznie zatrzymywania i uruchamiania** zbierania i przekazywania danych telemetrycznych z serwera:</span><span class="sxs-lookup"><span data-stu-id="156f6-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="156f6-186">Aby **wyłączyć wybranego standardowe moduły zbierające** — na przykład liczniki wydajności, żądań HTTP lub zależności - Usuń lub komentarz w odpowiednich wierszach [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Można to zrobisz, na przykład, jeśli chcesz wysyłać dane TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="156f6-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="156f6-187">Przeglądanie liczników wydajności systemu</span><span class="sxs-lookup"><span data-stu-id="156f6-187">View system performance counters</span></span>
<span data-ttu-id="156f6-188">Wśród metryk, które można wyświetlić w Eksploratorze metryk są zestawem systemu liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="156f6-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="156f6-189">Jest wstępnie zdefiniowanych bloku zatytułowany **serwerów** wyświetlający kilka z nich.</span><span class="sxs-lookup"><span data-stu-id="156f6-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Otwórz zasobu usługi Application Insights i kliknij pozycję serwery](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="156f6-191">Jeśli zostanie wyświetlony nie danych licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="156f6-191">If you see no performance counter data</span></span>
* <span data-ttu-id="156f6-192">**Serwer usług IIS** na własnym komputerze lub na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="156f6-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="156f6-193">[Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="156f6-194">**Witryny sieci web Azure** — nie obsługujemy jeszcze liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="156f6-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="156f6-195">Istnieje kilka miar, który można uzyskać w ramach standardowego witryny sieci web platformy Azure w Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="156f6-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="156f6-196">**Serwer UNIX** - [zainstalować collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="156f6-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="156f6-197">Aby wyświetlić więcej liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="156f6-197">To display more performance counters</span></span>
* <span data-ttu-id="156f6-198">Najpierw [Dodaj nowy wykres](app-insights-metrics-explorer.md) i zobacz, czy licznik jest podstawowego zestawu, które są oferowane.</span><span class="sxs-lookup"><span data-stu-id="156f6-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="156f6-199">Jeśli nie, [dodać licznik do zestawu zebrane przez modułu licznika wydajności](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="156f6-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
