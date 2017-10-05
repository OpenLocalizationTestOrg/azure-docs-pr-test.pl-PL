---
title: "Analiza użycia aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Dowiedz się, użytkownicy i ich działania z aplikacji sieci web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="28969-103">Analiza użycia aplikacji sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="28969-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="28969-104">Funkcje aplikacji sieci web są najbardziej popularnych?</span><span class="sxs-lookup"><span data-stu-id="28969-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="28969-105">Czy użytkownicy osiągnąć cele związane z aplikacją?</span><span class="sxs-lookup"><span data-stu-id="28969-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="28969-106">Czy one usunąć w szczególności, i zwracają później?</span><span class="sxs-lookup"><span data-stu-id="28969-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="28969-107">[Azure Application Insights](app-insights-overview.md) pomaga uzyskać zaawansowane wgląd w jaki sposób użytkownicy korzystają z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="28969-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="28969-108">Za każdym razem, gdy aktualizacji aplikacji, można ocenić, jak działa dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28969-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="28969-109">Z tym wiedzy możesz wprowadzić decyzje dotyczące Twojej dalej programistycznych opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="28969-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="28969-110">Wysłać dane telemetryczne z aplikacji</span><span class="sxs-lookup"><span data-stu-id="28969-110">Send telemetry from your app</span></span>

<span data-ttu-id="28969-111">Najlepsze środowisko są uzyskiwane przez zainstalowanie usługi Application Insights, zarówno w kodzie serwera aplikacji, jak i na stronach sieci web.</span><span class="sxs-lookup"><span data-stu-id="28969-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="28969-112">Składniki klienta i serwera aplikacji wysłać dane telemetryczne, wróć do portalu Azure do analizy.</span><span class="sxs-lookup"><span data-stu-id="28969-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="28969-113">**Kod serwera:** zainstalować moduł odpowiednie dla Twojej [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), lub [innych](app-insights-platforms.md) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28969-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="28969-114">*Nie chcesz zainstalować kod serwera? Po prostu [tworzenie zasobów Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="28969-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="28969-115">**Kod strony sieci Web:** Otwórz [portalu Azure](https://portal.azure.com), otwórz zasobu usługi Application Insights dla aplikacji, a następnie **wprowadzenie > Monitorowanie i diagnozowanie po stronie klienta**.</span><span class="sxs-lookup"><span data-stu-id="28969-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Skopiuj skrypt do Nagłówek strony wzorcowej sieci web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="28969-117">**Pobierz dane telemetryczne:** uruchomić projekt w trybie debugowania na kilka minut, a następnie sprawdź wyniki w bloku omówienie w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="28969-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="28969-118">Publikowanie aplikacji w celu monitorowania wydajności aplikacji i dowiedzieć się, co robią użytkownicy z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="28969-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="28969-119">Uwzględnia Identyfikatora użytkownika i sesji w obrębie telemetrii</span><span class="sxs-lookup"><span data-stu-id="28969-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="28969-120">Aby śledzić użytkowników w czasie, usługi Application Insights wymaga do ich identyfikowania.</span><span class="sxs-lookup"><span data-stu-id="28969-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="28969-121">Narzędzie zdarzenia jest tylko narzędzie użycia, które nie wymagają Identyfikatora użytkownika lub identyfikator sesji.</span><span class="sxs-lookup"><span data-stu-id="28969-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="28969-122">Rozpocznij wysyłanie tych identyfikatorów [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="28969-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="28969-123">Eksploruj demograficznych użycia oraz statystyki</span><span class="sxs-lookup"><span data-stu-id="28969-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="28969-124">Dowiedz się, gdy użytkownicy korzystają z aplikacji, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają.</span><span class="sxs-lookup"><span data-stu-id="28969-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="28969-125">Raporty użytkowników i sesji filtrować dane według stron lub zdarzeń niestandardowych, a segment je za pomocą właściwości, takie jak lokalizacja, środowisko i strony.</span><span class="sxs-lookup"><span data-stu-id="28969-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="28969-126">Można także dodać własne filtry.</span><span class="sxs-lookup"><span data-stu-id="28969-126">You can also add your own filters.</span></span>

![Użytkownicy](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="28969-128">Szczegółowe informacje, z prawej strony punktu interesujących wzorców w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="28969-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="28969-129">**Użytkowników** raport liczby unikatowych użytkowników, które uzyskują dostęp do stron w ramach Twojej wybranych okresów.</span><span class="sxs-lookup"><span data-stu-id="28969-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="28969-130">(Użytkownicy są liczone przy użyciu plików cookie.</span><span class="sxs-lookup"><span data-stu-id="28969-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="28969-131">Jeśli ktoś uzyskuje dostęp do witryny za pomocą różnych przeglądarkach lub komputerów klienckich, lub czyści ich plików cookie, a następnie będzie można zliczane więcej niż raz.)</span><span class="sxs-lookup"><span data-stu-id="28969-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="28969-132">**Sesji** raport zlicza sesje użytkowników, które uzyskują dostęp do witryny.</span><span class="sxs-lookup"><span data-stu-id="28969-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="28969-133">Sesja jest okres aktywności przez użytkownika, został przerwany przez okres aktywności ponad pół godziny.</span><span class="sxs-lookup"><span data-stu-id="28969-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="28969-134">Więcej informacji na temat narzędzia użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="28969-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="28969-135">Liczba wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="28969-135">Page views</span></span>

<span data-ttu-id="28969-136">W bloku użycia kliknij za pośrednictwem kafelkiem wyświetleń strony, aby uzyskać podział najpopularniejszych stron:</span><span class="sxs-lookup"><span data-stu-id="28969-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![W bloku Przegląd kliknij wykres widoków strony](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="28969-138">W powyższym przykładzie jest gry witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="28969-138">The example above is from a games web site.</span></span> <span data-ttu-id="28969-139">Wykresy firma Microsoft może natychmiast zobacz:</span><span class="sxs-lookup"><span data-stu-id="28969-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="28969-140">Użycie nie ulepszona w zeszłym tygodniu.</span><span class="sxs-lookup"><span data-stu-id="28969-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="28969-141">Może być powinniśmy pomyśleć o optymalizacji dla aparatów wyszukiwania?</span><span class="sxs-lookup"><span data-stu-id="28969-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="28969-142">Tenisa jest najbardziej popularnym strona gier.</span><span class="sxs-lookup"><span data-stu-id="28969-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="28969-143">Ta funkcja pozwala skupić się na dalszych poprawek do tej strony.</span><span class="sxs-lookup"><span data-stu-id="28969-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="28969-144">Średnio odwiedzin strony tenisa około trzy razy w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="28969-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="28969-145">(Istnieją sesje około trzy razy więcej niż użytkowników.)</span><span class="sxs-lookup"><span data-stu-id="28969-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="28969-146">Większość użytkowników w witrynie w tygodniu pracy USA, a w godzinach pracy.</span><span class="sxs-lookup"><span data-stu-id="28969-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="28969-147">Być może należy udostępniamy przycisk "szybkie Ukryj" na stronie sieci web.</span><span class="sxs-lookup"><span data-stu-id="28969-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="28969-148">[Adnotacje](app-insights-annotations.md) na wykresie Pokaż, gdy nowe wersje witryny sieci Web zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="28969-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="28969-149">Brak najnowszych wdrożeń ma zauważalnego wpływu na sposób użycia.</span><span class="sxs-lookup"><span data-stu-id="28969-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="28969-150">Co zrobić, jeśli chcesz zbadać ruch do witryny bardziej szczegółowo, takich jak dzielenie według właściwości niestandardowej, wysyłanych w jego dane telemetryczne wyświetleń strony witryny?</span><span class="sxs-lookup"><span data-stu-id="28969-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="28969-151">Otwórz **zdarzenia** narzędzia w menu zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="28969-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="28969-152">To narzędzie umożliwia analizowanie, ile strony widoków i zdarzeń niestandardowych, które zostały wysłane z aplikacji, w oparciu o różne opcje filtrowania, cohorting i segmentacji.</span><span class="sxs-lookup"><span data-stu-id="28969-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="28969-153">Na liście rozwijanej "Kto używane" Wybierz "Dowolny widok strony".</span><span class="sxs-lookup"><span data-stu-id="28969-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="28969-154">Na liście rozwijanej "Podział według" Wybierz właściwość, według której będzie dzielony Twoje dane telemetryczne wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="28969-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="28969-155">Przechowywania - wróć ilu użytkowników?</span><span class="sxs-lookup"><span data-stu-id="28969-155">Retention - how many users come back?</span></span>

<span data-ttu-id="28969-156">Przechowywania pomaga zrozumieć, jak często użytkownicy powrócić do używać aplikacji w oparciu stado użytkowników, którzy wykonać akcję biznesowych w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="28969-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="28969-157">Zrozumienie, jakie określone funkcje, że użytkownicy przejdzie ponownie więcej niż inne</span><span class="sxs-lookup"><span data-stu-id="28969-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="28969-158">Na podstawie danych użytkownika rzeczywistych hipotez formularza</span><span class="sxs-lookup"><span data-stu-id="28969-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="28969-159">Określić, czy przechowywania jest problem w programie</span><span class="sxs-lookup"><span data-stu-id="28969-159">Determine whether retention is a problem in your product</span></span> 

![Przechowywanie](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="28969-161">Formanty przechowywania u góry, umożliwiają definiowanie określonych zdarzeń i zakres czasu, aby obliczyć przechowywania.</span><span class="sxs-lookup"><span data-stu-id="28969-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="28969-162">Wykres w środku zapewnia wizualną reprezentację ogólny procent przechowywania przez podany zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="28969-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="28969-163">Wykres w dolnej reprezentuje indywidualne przechowywania w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="28969-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="28969-164">Taki poziom szczegółowości pozwala zrozumieć, co robią użytkownicy i co może mieć wpływ na użytkowników zwracająca na bardziej szczegółowy poziom szczegółowości.</span><span class="sxs-lookup"><span data-stu-id="28969-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="28969-165">Więcej informacji na temat narzędzia przechowywania</span><span class="sxs-lookup"><span data-stu-id="28969-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="28969-166">Zdarzenia niestandardowe biznesowe</span><span class="sxs-lookup"><span data-stu-id="28969-166">Custom business events</span></span>

<span data-ttu-id="28969-167">Aby uzyskać przejrzysty użytkowników czy z aplikacji sieci web, jest przydatne do wstawiania wierszy kodu do dziennika zdarzeń niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="28969-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="28969-168">Zdarzenia te można śledzić żadnych czynności użytkownika szczegółowe akcje, takie jak kliknięcie określonego przycisków, aby bardziej znaczących zdarzenia biznesowe, takie jak dokonywania zakupu lub zastosowanie gier.</span><span class="sxs-lookup"><span data-stu-id="28969-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="28969-169">Chociaż w niektórych przypadkach wyświetleń strony może reprezentować przydatne zdarzeń, nie jest PRAWDA ogólnie.</span><span class="sxs-lookup"><span data-stu-id="28969-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="28969-170">Użytkownik może otworzyć stronę produktu bez zakupu produktu.</span><span class="sxs-lookup"><span data-stu-id="28969-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="28969-171">Zdarzenia firmy można wykresu postępu użytkowników za pośrednictwem witryny.</span><span class="sxs-lookup"><span data-stu-id="28969-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="28969-172">Można sprawdzić ich preferencje dotyczące różnych opcjach i gdzie one usunąć out lub ma trudności.</span><span class="sxs-lookup"><span data-stu-id="28969-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="28969-173">Z tej wiedzy można podejmowania świadomych decyzji o priorytetów w rozwoju listę prac.</span><span class="sxs-lookup"><span data-stu-id="28969-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="28969-174">Na stronie sieci web mogą być rejestrowane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="28969-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="28969-175">Lub w aplikacji sieci web po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="28969-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="28969-176">Wartości właściwości można dołączyć do tych zdarzeń, dzięki czemu można filtrować lub podzielić zdarzenia inspekcji w portalu.</span><span class="sxs-lookup"><span data-stu-id="28969-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="28969-177">Ponadto standardowy zestaw właściwości jest dołączany do każdego zdarzenia, takie jak identyfikator użytkownika anonimowego, co pozwala na śledzenie sekwencję działań użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28969-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="28969-178">Dowiedz się więcej o [zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent) i [właściwości](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="28969-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="28969-179">Zdarzenia metod selekcji i projekcji</span><span class="sxs-lookup"><span data-stu-id="28969-179">Slice and dice events</span></span>

<span data-ttu-id="28969-180">W menu Narzędzia użytkownikami, sesjami i zdarzenia możesz można kątami zdarzeń niestandardowych przez użytkownika, nazwę zdarzenia i właściwości.</span><span class="sxs-lookup"><span data-stu-id="28969-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="28969-181">![Użytkownicy](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="28969-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="28969-182">Projekt telemetrii w aplikacji</span><span class="sxs-lookup"><span data-stu-id="28969-182">Design the telemetry with the app</span></span>

<span data-ttu-id="28969-183">Podczas projektowania każdej funkcji aplikacji, należy wziąć pod uwagę, jak zamierzasz oceny sukcesu jej z użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="28969-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="28969-184">Zdecyduj, jakie zdarzenia biznesowe, które trzeba zarejestrować i kod wywołuje śledzenia dla tych zdarzeń w swojej aplikacji od początku.</span><span class="sxs-lookup"><span data-stu-id="28969-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="28969-185">A | Testowanie B</span><span class="sxs-lookup"><span data-stu-id="28969-185">A | B Testing</span></span>
<span data-ttu-id="28969-186">Jeśli nie wiesz, który wariant funkcji więcej powiedzie się, zwolnij ich wprowadzania każdego dostępne dla różnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28969-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="28969-187">Mierzony sukces każdego z nich, a następnie przesuń do ujednoliconego wersji.</span><span class="sxs-lookup"><span data-stu-id="28969-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="28969-188">Dla tej metody możesz dołączyć wartości różnych właściwości wszystkie dane telemetryczne wysyłany przez poszczególnych wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28969-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="28969-189">Możesz to zrobić przez definiowanie właściwości w active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="28969-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="28969-190">Te właściwości domyślne są dodawane do każdej telemetrii komunikat, który wysyła aplikacji — nie tylko komunikaty niestandardowe, ale także standardowe telemetrii.</span><span class="sxs-lookup"><span data-stu-id="28969-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="28969-191">W portalu usługi Application Insights filtrowania i podziału danych w wartości właściwości w taki sposób, aby porównać różne wersje.</span><span class="sxs-lookup"><span data-stu-id="28969-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="28969-192">Aby to zrobić, [Konfigurowanie inicjatora telemetrii](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="28969-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="28969-193">W inicjatorze aplikacji sieci web, takich jak Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="28969-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="28969-194">Wszystkie nowe TelemetryClients automatycznie dodają podaną wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="28969-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="28969-195">Zdarzenia telemetrii poszczególnych można zastąpić wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="28969-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28969-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28969-196">Next steps</span></span>
   - [<span data-ttu-id="28969-197">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="28969-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="28969-198">Lejki</span><span class="sxs-lookup"><span data-stu-id="28969-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="28969-199">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="28969-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="28969-200">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="28969-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="28969-201">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="28969-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="28969-202">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="28969-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
