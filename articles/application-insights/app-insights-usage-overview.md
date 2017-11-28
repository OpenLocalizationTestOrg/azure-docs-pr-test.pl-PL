---
title: "Analiza aaaUsage dla aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="6c92e-103">Analiza użycia aplikacji sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="6c92e-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="6c92e-104">Funkcje aplikacji sieci web są najbardziej popularnych?</span><span class="sxs-lookup"><span data-stu-id="6c92e-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="6c92e-105">Czy użytkownicy osiągnąć cele związane z aplikacją?</span><span class="sxs-lookup"><span data-stu-id="6c92e-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="6c92e-106">Czy one usunąć w szczególności, i zwracają później?</span><span class="sxs-lookup"><span data-stu-id="6c92e-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="6c92e-107">[Azure Application Insights](app-insights-overview.md) pomaga uzyskać zaawansowane wgląd w jaki sposób użytkownicy korzystają z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6c92e-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="6c92e-108">Za każdym razem, gdy aktualizacji aplikacji, można ocenić, jak działa dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6c92e-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="6c92e-109">Z tym wiedzy możesz wprowadzić decyzje dotyczące Twojej dalej programistycznych opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="6c92e-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="6c92e-110">Wysłać dane telemetryczne z aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c92e-110">Send telemetry from your app</span></span>

<span data-ttu-id="6c92e-111">najlepsze środowisko Hello są uzyskiwane przez zainstalowanie usługi Application Insights, zarówno w kodzie serwera aplikacji, jak i na stronach sieci web.</span><span class="sxs-lookup"><span data-stu-id="6c92e-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="6c92e-112">składniki klienta i serwera aplikacji Hello wysłać dane telemetryczne wstecz toohello portalu Azure do analizy.</span><span class="sxs-lookup"><span data-stu-id="6c92e-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="6c92e-113">**Kod serwera:** instalacji hello moduł odpowiednie dla Twojej [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), lub [innych](app-insights-platforms.md) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c92e-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="6c92e-114">*Nie chcesz tooinstall kod serwera? Po prostu [tworzenie zasobów Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="6c92e-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="6c92e-115">**Kod strony sieci Web:** Otwórz hello [portalu Azure](https://portal.azure.com), otwórz hello zasobu usługi Application Insights dla aplikacji, a następnie **wprowadzenie > Monitorowanie i diagnozowanie po stronie klienta**.</span><span class="sxs-lookup"><span data-stu-id="6c92e-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Skopiuj skrypt hello do head hello głównej strony sieci web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="6c92e-117">**Pobierz dane telemetryczne:** uruchomić projekt w trybie debugowania na kilka minut, a następnie sprawdź wyniki w bloku omówienie hello w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c92e-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="6c92e-118">Publikowanie z toomonitor aplikacji wydajność aplikacji i dowiedzieć się, co robią użytkownicy z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="6c92e-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="6c92e-119">Uwzględnia Identyfikatora użytkownika i sesji w obrębie telemetrii</span><span class="sxs-lookup"><span data-stu-id="6c92e-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="6c92e-120">Użytkownicy tootrack wraz z upływem czasu, usługa Application Insights wymaga tooidentify sposób ich.</span><span class="sxs-lookup"><span data-stu-id="6c92e-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="6c92e-121">Zdarzenia Hello jest narzędzie hello jedynym narzędziem użycia, które nie wymagają Identyfikatora użytkownika lub identyfikator sesji.</span><span class="sxs-lookup"><span data-stu-id="6c92e-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="6c92e-122">Rozpocznij wysyłanie tych identyfikatorów [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="6c92e-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="6c92e-123">Eksploruj demograficznych użycia oraz statystyki</span><span class="sxs-lookup"><span data-stu-id="6c92e-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="6c92e-124">Dowiedz się, gdy użytkownicy korzystają z aplikacji, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają.</span><span class="sxs-lookup"><span data-stu-id="6c92e-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="6c92e-125">Raporty Hello użytkowników i sesji filtrować dane według stron lub zdarzeń niestandardowych i segmentację je przez właściwości, takie jak lokalizacja, środowiska i strony.</span><span class="sxs-lookup"><span data-stu-id="6c92e-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="6c92e-126">Można także dodać własne filtry.</span><span class="sxs-lookup"><span data-stu-id="6c92e-126">You can also add your own filters.</span></span>

![Użytkownicy](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="6c92e-128">Szczegółowe informacje na powitania prawym punktu interesujących wzorców w hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="6c92e-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="6c92e-129">Witaj **użytkowników** raport liczby hello liczby unikatowych użytkowników, które uzyskują dostęp do stron w ramach Twojej wybranych okresów.</span><span class="sxs-lookup"><span data-stu-id="6c92e-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="6c92e-130">(Użytkownicy są liczone przy użyciu plików cookie.</span><span class="sxs-lookup"><span data-stu-id="6c92e-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="6c92e-131">Jeśli ktoś uzyskuje dostęp do witryny za pomocą różnych przeglądarkach lub komputerów klienckich, lub czyści ich plików cookie, a następnie będzie można zliczane więcej niż raz.)</span><span class="sxs-lookup"><span data-stu-id="6c92e-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="6c92e-132">Witaj **sesji** raport zlicza hello sesje użytkowników, które uzyskują dostęp do witryny.</span><span class="sxs-lookup"><span data-stu-id="6c92e-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="6c92e-133">Sesja jest okres aktywności przez użytkownika, został przerwany przez okres aktywności ponad pół godziny.</span><span class="sxs-lookup"><span data-stu-id="6c92e-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="6c92e-134">Więcej informacji na temat narzędzia hello użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="6c92e-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="6c92e-135">Liczba wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="6c92e-135">Page views</span></span>

<span data-ttu-id="6c92e-136">W bloku użycia hello kliknij za pośrednictwem hello wyświetleń strony kafelka tooget podział najpopularniejszych stron:</span><span class="sxs-lookup"><span data-stu-id="6c92e-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![W bloku omówienie hello kliknij hello strony widoki wykresu](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="6c92e-138">w powyższym przykładzie Hello jest gry witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="6c92e-138">hello example above is from a games web site.</span></span> <span data-ttu-id="6c92e-139">Z wykresów hello natychmiast widać:</span><span class="sxs-lookup"><span data-stu-id="6c92e-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="6c92e-140">Użycie nie zwiększona hello zeszłym tygodniu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="6c92e-141">Może być powinniśmy pomyśleć o optymalizacji dla aparatów wyszukiwania?</span><span class="sxs-lookup"><span data-stu-id="6c92e-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="6c92e-142">Tenisa jest najbardziej popularnym strona gier hello.</span><span class="sxs-lookup"><span data-stu-id="6c92e-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="6c92e-143">Ta funkcja pozwala skupić się na dodatkowe ulepszenia toothis strony.</span><span class="sxs-lookup"><span data-stu-id="6c92e-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="6c92e-144">Średnio użytkowników stronie powitania tenisa około trzy razy w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="6c92e-145">(Istnieją sesje około trzy razy więcej niż użytkowników.)</span><span class="sxs-lookup"><span data-stu-id="6c92e-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="6c92e-146">Większość użytkowników w witrynie hello hello USA pracy tygodniu i w godzinach pracy.</span><span class="sxs-lookup"><span data-stu-id="6c92e-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="6c92e-147">Być może należy udostępniamy przycisk "szybkie Ukryj" na stronie sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="6c92e-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="6c92e-148">Witaj [adnotacje](app-insights-annotations.md) na wykresie hello Pokaż, gdy nowe wersje hello witryny sieci Web zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6c92e-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="6c92e-149">Brak hello ostatnie wdrożeń ma zauważalnego wpływu na sposób użycia.</span><span class="sxs-lookup"><span data-stu-id="6c92e-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="6c92e-150">Co zrobić, jeśli chcesz tooinvestigate hello ruchu tooyour lokacji bardziej szczegółowo, takich jak dzielenie według właściwości niestandardowej, wysyłanych w jego dane telemetryczne wyświetleń strony witryny?</span><span class="sxs-lookup"><span data-stu-id="6c92e-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="6c92e-151">Otwórz hello **zdarzenia** narzędzia w menu zasobu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="6c92e-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="6c92e-152">To narzędzie umożliwia analizowanie, ile strony widoków i zdarzeń niestandardowych, które zostały wysłane z aplikacji, w oparciu o różne opcje filtrowania, cohorting i segmentacji.</span><span class="sxs-lookup"><span data-stu-id="6c92e-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="6c92e-153">W hello "Kto używane" z listy rozwijanej wybierz "Dowolny widok strony".</span><span class="sxs-lookup"><span data-stu-id="6c92e-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="6c92e-154">W polu listy rozwijanej "Podziału przez" hello wybierz właściwości, według których toosplit ze strony wyświetlić dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="6c92e-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="6c92e-155">Przechowywania - wróć ilu użytkowników?</span><span class="sxs-lookup"><span data-stu-id="6c92e-155">Retention - how many users come back?</span></span>

<span data-ttu-id="6c92e-156">Przechowywania pomaga zrozumieć, jak często użytkownicy zwracać toouse aplikacji w oparciu stado użytkowników, którzy wykonać akcję biznesowych w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="6c92e-157">Zrozumienie, jakie określone funkcje, że użytkownicy wstecz toocome więcej niż inne</span><span class="sxs-lookup"><span data-stu-id="6c92e-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="6c92e-158">Na podstawie danych użytkownika rzeczywistych hipotez formularza</span><span class="sxs-lookup"><span data-stu-id="6c92e-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="6c92e-159">Określić, czy przechowywania jest problem w programie</span><span class="sxs-lookup"><span data-stu-id="6c92e-159">Determine whether retention is a problem in your product</span></span> 

![Przechowywanie](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="6c92e-161">Formanty przechowywania Hello na górze umożliwiają, możesz toodefine określonych zdarzeń i przechowywania toocalculate zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="6c92e-162">Witaj wykresu w środku hello daje wizualną reprezentację hello ogólną procent przechowywania hello zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="6c92e-163">Wykres Hello na dole hello reprezentuje indywidualne przechowywania w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="6c92e-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="6c92e-164">Taki poziom szczegółowości pozwala toounderstand, jakie użytkownicy wirtualni i co może mieć wpływ na użytkowników zwracająca na bardziej szczegółowy poziom szczegółowości.</span><span class="sxs-lookup"><span data-stu-id="6c92e-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="6c92e-165">Więcej informacji na temat narzędzia przechowywania hello</span><span class="sxs-lookup"><span data-stu-id="6c92e-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="6c92e-166">Zdarzenia niestandardowe biznesowe</span><span class="sxs-lookup"><span data-stu-id="6c92e-166">Custom business events</span></span>

<span data-ttu-id="6c92e-167">tooget przejrzysty co użytkownicy nie z aplikacji sieci web, jest przydatne tooinsert wierszy kodu toolog niestandardowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="6c92e-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="6c92e-168">Zdarzenia te można śledzić żadnych czynności użytkownika szczegółowe akcje, takie jak kliknięcie określonego przycisków, toomore firma zdarzenia, takie jak dokonywania zakupu lub zastosowanie gier.</span><span class="sxs-lookup"><span data-stu-id="6c92e-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="6c92e-169">Chociaż w niektórych przypadkach wyświetleń strony może reprezentować przydatne zdarzeń, nie jest PRAWDA ogólnie.</span><span class="sxs-lookup"><span data-stu-id="6c92e-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="6c92e-170">Użytkownik może otworzyć stronę produktu bez kupowanie hello produktu.</span><span class="sxs-lookup"><span data-stu-id="6c92e-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="6c92e-171">Zdarzenia firmy można wykresu postępu użytkowników za pośrednictwem witryny.</span><span class="sxs-lookup"><span data-stu-id="6c92e-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="6c92e-172">Można sprawdzić ich preferencje dotyczące różnych opcjach i gdzie one usunąć out lub ma trudności.</span><span class="sxs-lookup"><span data-stu-id="6c92e-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="6c92e-173">Z tej wiedzy można podejmowania świadomych decyzji o hello priorytetów w rozwoju listę prac.</span><span class="sxs-lookup"><span data-stu-id="6c92e-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="6c92e-174">Na stronie sieci web hello mogą być rejestrowane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="6c92e-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="6c92e-175">Lub po stronie serwera na powitania hello aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="6c92e-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="6c92e-176">Zdarzenia toothese wartości właściwości, można dołączyć, aby mogą filtrować lub podziału hello zdarzeń inspekcji w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6c92e-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="6c92e-177">Ponadto standardowy zestaw właściwości jest dołączone tooeach zdarzeń, takich jak identyfikator użytkownika anonimowego, co pozwala tootrace hello sekwencji działań użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c92e-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="6c92e-178">Dowiedz się więcej o [zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent) i [właściwości](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="6c92e-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="6c92e-179">Zdarzenia metod selekcji i projekcji</span><span class="sxs-lookup"><span data-stu-id="6c92e-179">Slice and dice events</span></span>

<span data-ttu-id="6c92e-180">W narzędziach użytkownikami, sesjami i zdarzenia hello użytkownik może kątami zdarzeń niestandardowych przez użytkownika, nazwę zdarzenia i właściwości.</span><span class="sxs-lookup"><span data-stu-id="6c92e-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="6c92e-181">![Użytkownicy](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="6c92e-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="6c92e-182">Dane telemetryczne hello projekt aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6c92e-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="6c92e-183">Podczas projektowania każdej funkcji aplikacji, należy wziąć pod uwagę, jak ma toomeasure jego powodzenia z użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="6c92e-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="6c92e-184">Zdecyduj, zdarzenia biznesowe muszą toorecord, a kodem hello śledzenia wywołań dla tych zdarzeń w aplikacji z hello start.</span><span class="sxs-lookup"><span data-stu-id="6c92e-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="6c92e-185">A | Testowanie B</span><span class="sxs-lookup"><span data-stu-id="6c92e-185">A | B Testing</span></span>
<span data-ttu-id="6c92e-186">Jeśli nie wiesz, który wariant funkcji więcej powiedzie się, zwolnij ich wprowadzania poszczególnych użytkowników toodifferent dostępny.</span><span class="sxs-lookup"><span data-stu-id="6c92e-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="6c92e-187">Mierzony sukces hello każdego z nich, a następnie przesuń tooa ujednoliconego wersji.</span><span class="sxs-lookup"><span data-stu-id="6c92e-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="6c92e-188">Dla tej metody można dołączyć właściwości różne wartości tooall hello telemetrii, wysyłany przez poszczególnych wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c92e-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="6c92e-189">Możesz to zrobić przez definiowanie właściwości w hello active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="6c92e-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="6c92e-190">Te właściwości domyślne są dodawane wysyła tooevery telemetrii wiadomość hello aplikacji — nie tylko z niestandardowych wiadomości, ale hello także standardowe telemetrii.</span><span class="sxs-lookup"><span data-stu-id="6c92e-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="6c92e-191">W portalu usługi Application Insights hello filtrowania i podziału danych w wartości właściwości hello, tak jak toocompare hello różne wersje.</span><span class="sxs-lookup"><span data-stu-id="6c92e-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="6c92e-192">toodo, [Konfigurowanie inicjatora telemetrii](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="6c92e-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="6c92e-193">W inicjatorze aplikacji sieci web hello takich jak Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="6c92e-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="6c92e-194">Wszystkie nowe TelemetryClients automatycznie dodają hello wartości właściwości, które określisz.</span><span class="sxs-lookup"><span data-stu-id="6c92e-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="6c92e-195">Zdarzenia telemetrii poszczególnych można zastąpić wartości domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="6c92e-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c92e-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c92e-196">Next steps</span></span>
   - [<span data-ttu-id="6c92e-197">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="6c92e-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="6c92e-198">Lejki</span><span class="sxs-lookup"><span data-stu-id="6c92e-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="6c92e-199">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="6c92e-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="6c92e-200">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="6c92e-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="6c92e-201">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="6c92e-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="6c92e-202">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6c92e-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
