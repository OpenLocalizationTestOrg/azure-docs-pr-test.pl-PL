---
title: "Ustawianie alertów w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Bądź na bieżąco o wydłużają czas odpowiedzi, wyjątków i innych wydajności lub zmiany użycia w aplikacji sieci web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: c8386ffc5d68260eeb75edf7efb77db1163dcef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="set-alerts-in-application-insights"></a><span data-ttu-id="911c6-103">Ustawianie alertów w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="911c6-103">Set Alerts in Application Insights</span></span>
<span data-ttu-id="911c6-104">[Azure Application Insights] [ start] alertów na zmiany w metryki wydajności i użycia w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="911c6-104">[Azure Application Insights][start] can alert you to changes in performance or usage metrics in your web app.</span></span> 

<span data-ttu-id="911c6-105">Usługa Application Insights monitoruje aplikację na żywo na [różnymi platformami] [ platforms] ułatwiających diagnozowanie problemów z wydajnością i poznania wzorców użycia.</span><span class="sxs-lookup"><span data-stu-id="911c6-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] to help you diagnose performance issues and understand usage patterns.</span></span>

<span data-ttu-id="911c6-106">Istnieją trzy typy alertów:</span><span class="sxs-lookup"><span data-stu-id="911c6-106">There are three kinds of alerts:</span></span>

* <span data-ttu-id="911c6-107">**Alerty metryki** informujące o tym, kiedy metrykę przecina wartość progową dla niektórych okres — takie jak czas reakcji, liczby wyjątków, użycie procesora CPU lub wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="911c6-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span></span> 
* <span data-ttu-id="911c6-108">[**Testów sieci Web** ] [ availability] informujące o tym, kiedy ta lokacja jest niedostępny w Internecie lub odpowiada powoli.</span><span class="sxs-lookup"><span data-stu-id="911c6-108">[**Web tests**][availability] tell you when your site is unavailable on the internet, or responding slowly.</span></span> <span data-ttu-id="911c6-109">[Dowiedz się więcej][availability].</span><span class="sxs-lookup"><span data-stu-id="911c6-109">[Learn more][availability].</span></span>
* <span data-ttu-id="911c6-110">[**Proaktywna Diagnostyka** ](app-insights-proactive-diagnostics.md) zostaną skonfigurowane automatycznie Pragniemy poinformować Cię o wydajności nietypowe wzorce.</span><span class="sxs-lookup"><span data-stu-id="911c6-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically to notify you about unusual performance patterns.</span></span>

<span data-ttu-id="911c6-111">Możemy skupić się na metryki alertów w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="911c6-111">We focus on metric alerts in this article.</span></span>

## <a name="set-a-metric-alert"></a><span data-ttu-id="911c6-112">Ustaw metryki alertu</span><span class="sxs-lookup"><span data-stu-id="911c6-112">Set a Metric alert</span></span>
<span data-ttu-id="911c6-113">Otwarcie bloku reguły alertów, a następnie za pomocą przycisku Dodaj.</span><span class="sxs-lookup"><span data-stu-id="911c6-113">Open the Alert rules blade, and then use the add button.</span></span> 

![W bloku reguły alertów wybierz opcję Dodaj alertu.](./media/app-insights-alerts/01-set-metric.png)

* <span data-ttu-id="911c6-116">Ustaw zasób przed inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="911c6-116">Set the resource before the other properties.</span></span> <span data-ttu-id="911c6-117">**Wybierz zasób "(składniki)"** Aby ustawić alertów dla metryki wydajności i użycia.</span><span class="sxs-lookup"><span data-stu-id="911c6-117">**Choose the "(components)" resource** if you want to set alerts on performance or usage metrics.</span></span>
* <span data-ttu-id="911c6-118">Nazwa nadana alert musi być unikatowa w obrębie grupy zasobów (nie tylko aplikacji).</span><span class="sxs-lookup"><span data-stu-id="911c6-118">The name that you give to the alert must be unique within the resource group (not just your application).</span></span>
* <span data-ttu-id="911c6-119">Należy zachować ostrożność, należy pamiętać, jednostki, w których użytkownik jest proszony o wprowadź wartość progu.</span><span class="sxs-lookup"><span data-stu-id="911c6-119">Be careful to note the units in which you're asked to enter the threshold value.</span></span>
* <span data-ttu-id="911c6-120">Po zaznaczeniu pola "E-mail właścicieli...", alerty są wysyłane pocztą e-mail do każdego, kto ma dostęp do tej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="911c6-120">If you check the box "Email owners...", alerts are sent by email to everyone who has access to this resource group.</span></span> <span data-ttu-id="911c6-121">Aby rozszerzyć ten zestaw osoby, dodaj je do [grupy zasobów lub subskrypcji](app-insights-resources-roles-access-control.md) (nie zasób).</span><span class="sxs-lookup"><span data-stu-id="911c6-121">To expand this set of people, add them to the [resource group or subscription](app-insights-resources-roles-access-control.md) (not the resource).</span></span>
* <span data-ttu-id="911c6-122">Jeśli określisz "Dodatkowe wiadomości e-mail" alerty są wysyłane do tych osób lub grup (czy zaznaczono pole "wiadomości e-mail właścicieli...").</span><span class="sxs-lookup"><span data-stu-id="911c6-122">If you specify "Additional emails", alerts are sent to those individuals or groups (whether or not you checked the "email owners..." box).</span></span> 
* <span data-ttu-id="911c6-123">Ustaw [adresu elementu webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) Jeśli zdefiniowano aplikacji sieci web, która odpowiada na alerty.</span><span class="sxs-lookup"><span data-stu-id="911c6-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds to alerts.</span></span> <span data-ttu-id="911c6-124">Jest to zarówno gdy alert jest aktywny, jak i po jej usunięciu.</span><span class="sxs-lookup"><span data-stu-id="911c6-124">It is called both when the alert is Activated and when it is Resolved.</span></span> <span data-ttu-id="911c6-125">(Ale należy pamiętać, że w chwili obecnej, parametry zapytania nie są przekazywane jako właściwości elementu webhook).</span><span class="sxs-lookup"><span data-stu-id="911c6-125">(But note that at present, query parameters are not passed through as webhook properties.)</span></span>
* <span data-ttu-id="911c6-126">Można wyłączyć lub włączyć alert: wyświetlanie przycisków w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="911c6-126">You can Disable or Enable the alert: see the buttons at the top of the blade.</span></span>

<span data-ttu-id="911c6-127">*Przycisk Dodaj alertu nie jest widoczny.*</span><span class="sxs-lookup"><span data-stu-id="911c6-127">*I don't see the Add Alert button.*</span></span> 

* <span data-ttu-id="911c6-128">Używasz konta organizacyjnego?</span><span class="sxs-lookup"><span data-stu-id="911c6-128">Are you using an organizational account?</span></span> <span data-ttu-id="911c6-129">Można ustawić alerty, jeśli masz właścicielem lub współautorem dostęp do tego zasobu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="911c6-129">You can set alerts if you have owner or contributor access to this application resource.</span></span> <span data-ttu-id="911c6-130">Spójrz na blok kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="911c6-130">Take a look at the Access Control blade.</span></span> <span data-ttu-id="911c6-131">[Więcej informacji na temat kontroli dostępu][roles].</span><span class="sxs-lookup"><span data-stu-id="911c6-131">[Learn about access control][roles].</span></span>

> [!NOTE]
> <span data-ttu-id="911c6-132">W bloku alerty widać, że istnieje już zestaw alertu: [proaktywna Diagnostyka](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="911c6-132">In the alerts blade, you see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="911c6-133">Alert automatycznego monitoruje jednego określonego metryki, częstość niepowodzeń.</span><span class="sxs-lookup"><span data-stu-id="911c6-133">The automatic alert monitors one particular metric, request failure rate.</span></span> <span data-ttu-id="911c6-134">Jeśli zdecydujesz się Wyłącz alert aktywny, nie trzeba ustawiać własne alert częstość niepowodzeń żądań.</span><span class="sxs-lookup"><span data-stu-id="911c6-134">Unless you decide to disable the proactive alert, you don't need to set your own alert on request failure rate.</span></span> 
> 
> 

## <a name="see-your-alerts"></a><span data-ttu-id="911c6-135">Zobacz alerty</span><span class="sxs-lookup"><span data-stu-id="911c6-135">See your alerts</span></span>
<span data-ttu-id="911c6-136">Otrzymasz wiadomość e-mail, gdy stan alertu zmiany między stanem nieaktywnym i aktywnym.</span><span class="sxs-lookup"><span data-stu-id="911c6-136">You get an email when an alert changes state between inactive and active.</span></span> 

<span data-ttu-id="911c6-137">Bieżący stan poszczególnych alertów jest wyświetlany w bloku reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="911c6-137">The current state of each alert is shown in the Alert rules blade.</span></span>

<span data-ttu-id="911c6-138">Brak podsumowanie ostatnią aktywność w alertach listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="911c6-138">There's a summary of recent activity in the alerts drop-down:</span></span>

![Alerty z listy rozwijanej](./media/app-insights-alerts/010-alert-drop.png)

<span data-ttu-id="911c6-140">Historię zmian stanu znajduje się w dzienniku aktywności:</span><span class="sxs-lookup"><span data-stu-id="911c6-140">The history of state changes is in the Activity Log:</span></span>

![W bloku Przegląd kliknij pozycję Ustawienia, dzienniki inspekcji](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a><span data-ttu-id="911c6-142">Jak działają alerty</span><span class="sxs-lookup"><span data-stu-id="911c6-142">How alerts work</span></span>
* <span data-ttu-id="911c6-143">Alert ma trzy stany: "Nigdy aktywowany", "Aktywny" i "Rozwiązany".</span><span class="sxs-lookup"><span data-stu-id="911c6-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span></span> <span data-ttu-id="911c6-144">Aktywowany oznacza, że określony warunek był ma wartość true, ostatniej oceny.</span><span class="sxs-lookup"><span data-stu-id="911c6-144">Activated means the condition you specified was true, when it was last evaluated.</span></span>
* <span data-ttu-id="911c6-145">Powiadomienie jest generowany, gdy alert zmieni stan.</span><span class="sxs-lookup"><span data-stu-id="911c6-145">A notification is generated when an alert changes state.</span></span> <span data-ttu-id="911c6-146">(Jeśli stan alertu został już wartość true, podczas tworzenia alertu, można otrzymać powiadomienie do momentu warunek przechodzi false.)</span><span class="sxs-lookup"><span data-stu-id="911c6-146">(If the alert condition was already true when you created the alert, you might not get a notification until the condition goes false.)</span></span>
* <span data-ttu-id="911c6-147">Każde powiadomienie generuje wiadomość e-mail, jeśli zaznaczono pole wiadomości e-mail lub podane adresy e-mail.</span><span class="sxs-lookup"><span data-stu-id="911c6-147">Each notification generates an email if you checked the emails box, or provided email addresses.</span></span> <span data-ttu-id="911c6-148">Można też przyjrzeć się na liście rozwijanej powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="911c6-148">You can also look at the Notifications drop-down list.</span></span>
* <span data-ttu-id="911c6-149">Alert jest obliczane zawsze, gdy dociera metrykę, ale nie w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="911c6-149">An alert is evaluated each time a metric arrives, but not otherwise.</span></span>
* <span data-ttu-id="911c6-150">Obliczanie agreguje Metryka w poprzednim okresie i porównywany do progu, aby określić nowy stan.</span><span class="sxs-lookup"><span data-stu-id="911c6-150">The evaluation aggregates the metric over the preceding period, and then compares it to the threshold to determine the new state.</span></span>
* <span data-ttu-id="911c6-151">Okresu, w którym możesz wybrać Określa interwał, w którym są agregowane metryki.</span><span class="sxs-lookup"><span data-stu-id="911c6-151">The period that you choose specifies the interval over which metrics are aggregated.</span></span> <span data-ttu-id="911c6-152">Nie wpływa na częstotliwość oceny alertu: to zależy od częstotliwości odbioru metryki.</span><span class="sxs-lookup"><span data-stu-id="911c6-152">It doesn't affect how often the alert is evaluated: that depends on the frequency of arrival of metrics.</span></span>
* <span data-ttu-id="911c6-153">Jeśli żadne dane dla określonej metryki przez pewien czas, przerwa ma efekty różnych na ocenę alertów i na wykresach w Eksploratorze metryk.</span><span class="sxs-lookup"><span data-stu-id="911c6-153">If no data arrives for a particular metric for some time, the gap has different effects on alert evaluation and on the charts in metric explorer.</span></span> <span data-ttu-id="911c6-154">W Eksploratorze metryk Jeśli występuje bez danych przez czas dłuższy niż interwał próbkowania wykresu, wykres zawiera wartość 0.</span><span class="sxs-lookup"><span data-stu-id="911c6-154">In metric explorer, if no data is seen for longer than the chart's sampling interval, the chart shows a value of 0.</span></span> <span data-ttu-id="911c6-155">Ale alertu opartego na tej samej Metryka nie jest ponownie oceniane, i stan alertów pozostaje niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="911c6-155">But an alert based on the same metric is not be reevaluated, and the alert's state remains unchanged.</span></span> 
  
    <span data-ttu-id="911c6-156">Po odebraniu ostatecznie danych, wykres Przechodzi wstecz na wartość inną niż zero.</span><span class="sxs-lookup"><span data-stu-id="911c6-156">When data eventually arrives, the chart jumps back to a non-zero value.</span></span> <span data-ttu-id="911c6-157">Oblicza alertu na podstawie danych dostępnych w okresie określona.</span><span class="sxs-lookup"><span data-stu-id="911c6-157">The alert evaluates based on the data available for the period you specified.</span></span> <span data-ttu-id="911c6-158">Jeśli nowy punkt danych jest tylko jeden dostępny w okresie, agregacji jest oparty tylko na punktu danych.</span><span class="sxs-lookup"><span data-stu-id="911c6-158">If the new data point is the only one available in the period, the aggregate is based just on that data point.</span></span>
* <span data-ttu-id="911c6-159">Alert można często migotać między Stanami alertów i działa prawidłowo, nawet w przypadku ustawienia długiego okresu.</span><span class="sxs-lookup"><span data-stu-id="911c6-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span></span> <span data-ttu-id="911c6-160">Może to nastąpić, jeśli wartość metryki znajduje się wokół wartość progową.</span><span class="sxs-lookup"><span data-stu-id="911c6-160">This can happen if the metric value hovers around the threshold.</span></span> <span data-ttu-id="911c6-161">Brak nie histerezy przez wartość progową: przejście do alertu odbywa się na taką samą wartość jak przejście do dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="911c6-161">There is no hysteresis in the threshold: the transition to alert happens at the same value as the transition to healthy.</span></span>

## <a name="what-are-good-alerts-to-set"></a><span data-ttu-id="911c6-162">Co to są dobrym alerty można ustawić?</span><span class="sxs-lookup"><span data-stu-id="911c6-162">What are good alerts to set?</span></span>
<span data-ttu-id="911c6-163">To zależy od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="911c6-163">It depends on your application.</span></span> <span data-ttu-id="911c6-164">Do uruchomienia z najlepiej nie ustawiono zbyt wiele miar.</span><span class="sxs-lookup"><span data-stu-id="911c6-164">To start with, it's best not to set too many metrics.</span></span> <span data-ttu-id="911c6-165">Należy poświęcić trochę czasu spojrzenie na wykresach metryki uruchomionej aplikacji, aby uzyskać pewne pojęcie o jak działa normalnie.</span><span class="sxs-lookup"><span data-stu-id="911c6-165">Spend some time looking at your metric charts while your app is running, to get a feel for how it behaves normally.</span></span> <span data-ttu-id="911c6-166">Takie rozwiązanie pomaga znaleźć sposób, aby zwiększyć jej wydajność.</span><span class="sxs-lookup"><span data-stu-id="911c6-166">This practice helps you find ways to improve its performance.</span></span> <span data-ttu-id="911c6-167">Następnie skonfiguruj alerty informujące o tym, kiedy metryki wykraczać poza normalne strefy.</span><span class="sxs-lookup"><span data-stu-id="911c6-167">Then set up alerts to tell you when the metrics go outside the normal zone.</span></span> 

<span data-ttu-id="911c6-168">Alerty popularnych obejmują:</span><span class="sxs-lookup"><span data-stu-id="911c6-168">Popular alerts include:</span></span>

* <span data-ttu-id="911c6-169">[Metryki przeglądarki][client], szczególnie przeglądarki **czas ładowania strony**, są odpowiednie dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="911c6-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span></span> <span data-ttu-id="911c6-170">Jeśli Twoja strona zawiera wiele skryptów, należy szukać **wyjątki przeglądarki**.</span><span class="sxs-lookup"><span data-stu-id="911c6-170">If your page has many scripts, you should look for **browser exceptions**.</span></span> <span data-ttu-id="911c6-171">Aby uzyskać te metryki i alerty, musisz skonfigurować [monitorowania strony sieci web][client].</span><span class="sxs-lookup"><span data-stu-id="911c6-171">In order to get these metrics and alerts, you have to set up [web page monitoring][client].</span></span>
* <span data-ttu-id="911c6-172">**Czas odpowiedzi serwera** dla aplikacji sieci web po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="911c6-172">**Server response time** for the server side of web applications.</span></span> <span data-ttu-id="911c6-173">A także Konfigurowanie alertów, śledzić tej metryki, aby zobaczyć, czy nieproporcjonalnie zależy szybkości przetwarzania żądań wysokiej: odmiany może wskazywać, że aplikacja działa poza zasobów.</span><span class="sxs-lookup"><span data-stu-id="911c6-173">As well as setting up alerts, keep an eye on this metric to see if it varies disproportionately with high request rates: variation might indicate that your app is running out of resources.</span></span> 
* <span data-ttu-id="911c6-174">**Wyjątki serwera** — do zapoznania się z nimi, musisz wykonać niektóre [dodatkowe ustawienia](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="911c6-174">**Server exceptions** - to see them, you have to do some [additional setup](app-insights-asp-net-exceptions.md).</span></span>

<span data-ttu-id="911c6-175">Pamiętaj, że [diagnostyki szybkość niepowodzenia aktywnego](app-insights-proactive-failure-diagnostics.md) automatycznie monitorowanie szybkości, jaką aplikacji odpowiada na żądania z kodami awarii.</span><span class="sxs-lookup"><span data-stu-id="911c6-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor the rate at which your app responds to requests with failure codes.</span></span> 

## <a name="automation"></a><span data-ttu-id="911c6-176">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="911c6-176">Automation</span></span>
* [<span data-ttu-id="911c6-177">Za pomocą programu PowerShell można zautomatyzować konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="911c6-177">Use PowerShell to automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="911c6-178">Można zautomatyzować, reagowanie na alerty za pomocą elementów webhook</span><span class="sxs-lookup"><span data-stu-id="911c6-178">Use webhooks to automate responding to alerts</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a><span data-ttu-id="911c6-179">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="911c6-179">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a><span data-ttu-id="911c6-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="911c6-180">See also</span></span>
* [<span data-ttu-id="911c6-181">Dostępność testy sieci web</span><span class="sxs-lookup"><span data-stu-id="911c6-181">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="911c6-182">Zautomatyzować konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="911c6-182">Automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="911c6-183">Proaktywna Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="911c6-183">Proactive diagnostics</span></span>](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

