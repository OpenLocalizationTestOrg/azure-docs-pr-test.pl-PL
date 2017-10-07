---
title: "Analiza aaaUser sesji i zdarzeń w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analiza demograficznych użytkowników aplikacji sieci web."
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="4c20b-103">Analiza użytkownikami, sesjami i zdarzeń w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="4c20b-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="4c20b-104">Dowiedz się, gdy użytkownicy korzystają z aplikacji sieci web, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają.</span><span class="sxs-lookup"><span data-stu-id="4c20b-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="4c20b-105">Analizowanie telemetrii działalności biznesowej i użycia za pomocą [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c20b-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="4c20b-106">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="4c20b-106">Get started</span></span>

<span data-ttu-id="4c20b-107">Jeśli nie widzisz jeszcze danych w hello użytkowników, sesji lub bloków zdarzenia w portalu usługi Application Insights hello [Dowiedz się, jak tooget pracę z narzędziami użycia hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c20b-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="4c20b-108">Narzędzie segmentacji Hello użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4c20b-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="4c20b-109">Trzy użycia hello używać bloków hello tego samego narzędzia tooslice i kości dane telemetryczne z aplikacji sieci web z trzema perspektyw.</span><span class="sxs-lookup"><span data-stu-id="4c20b-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="4c20b-110">Filtrowanie i dzielenia danych hello, można ujawnić informacjami na temat hello względną użycie różnych stron i funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="4c20b-111">**Narzędzie Użytkownicy**: używane wiele aplikacji i ich funkcje.</span><span class="sxs-lookup"><span data-stu-id="4c20b-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="4c20b-112">Użytkownicy są liczone przy użyciu anonimowego identyfikatorów przechowywane w plikach cookie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="4c20b-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="4c20b-113">Jedna osoba, za pomocą różnych przeglądarkach lub maszyny będą liczone jako więcej niż jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4c20b-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="4c20b-114">**Narzędzie sesje**: ile sesji aktywności użytkowników, zostały uwzględnione w pewnych stron i funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="4c20b-115">Sesja jest traktowane po pół godziny czas braku aktywności użytkownika, lub 24 godziny ciągłego użytkowania.</span><span class="sxs-lookup"><span data-stu-id="4c20b-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="4c20b-116">**Narzędzie zdarzenia**: jak często używane pewnych stron i funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="4c20b-117">Widok strony jest liczony przeglądarką załadowanie strony z aplikacji, pod warunkiem, że [zinstrumentowane on](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="4c20b-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="4c20b-118">Zdarzenie niestandardowe reprezentuje jedno wystąpienie określonego zdarzenia w aplikacji, często interakcji z użytkownikiem jak kliknij przycisk hello zakończenie niektórych zadań.</span><span class="sxs-lookup"><span data-stu-id="4c20b-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="4c20b-119">W aplikacji Wstawianie zbyt kodu[generowanie zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="4c20b-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Użycie narzędzia](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="4c20b-121">Wykonywanie zapytania dla niektórych użytkowników</span><span class="sxs-lookup"><span data-stu-id="4c20b-121">Querying for Certain Users</span></span> 

<span data-ttu-id="4c20b-122">Zapoznaj się z różnych grup użytkowników przez dostosowanie wartości opcji zapytania hello u góry hello hello użytkowników narzędzia:</span><span class="sxs-lookup"><span data-stu-id="4c20b-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="4c20b-123">Kto używane: Wybierz niestandardowych zdarzeń i wyświetlenia strony.</span><span class="sxs-lookup"><span data-stu-id="4c20b-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="4c20b-124">W trakcie: Wybierz zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="4c20b-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="4c20b-125">Przez: Wybierz, jak toobucket hello danych przez pewien czas lub innej właściwości, takie jak przeglądarki lub Miasto.</span><span class="sxs-lookup"><span data-stu-id="4c20b-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="4c20b-126">Dzielenie przez: Wybierz właściwość przez danych hello toosplit lub segmentu.</span><span class="sxs-lookup"><span data-stu-id="4c20b-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="4c20b-127">Dodaj filtry: Ograniczyć hello zapytania toocertain użytkowników, sesji lub zdarzenia na podstawie ich właściwości, takie jak przeglądarki lub Miasto.</span><span class="sxs-lookup"><span data-stu-id="4c20b-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="4c20b-128">Zapisywanie i udostępnianie raportów</span><span class="sxs-lookup"><span data-stu-id="4c20b-128">Saving and sharing reports</span></span> 
<span data-ttu-id="4c20b-129">Można zapisać raportów użytkowników, albo prywatnej tooyou tylko w sekcji Moje raporty hello, lub udostępniać inne osoby z toothis dostępu do zasobu usługi Application Insights w hello sekcji udostępnionych raportów.</span><span class="sxs-lookup"><span data-stu-id="4c20b-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="4c20b-130">Podczas zapisywania raportu lub edytowania jego właściwości, wybierz toosave "Bieżący względny zakres czasu", który raport będzie stale odświeżyć dane, wracając niektórych stałej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="4c20b-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="4c20b-131">Wybierz raport o ustalony zbiór danych toosave "Bieżący bezwzględny zakres czasu".</span><span class="sxs-lookup"><span data-stu-id="4c20b-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="4c20b-132">Należy pamiętać, że dane w usłudze Application Insights tylko są przechowywane przez 90 dni, więc jeśli minęło ponad 90 dni od raport z zakresem bezwzględnego czasu został zapisany, hello raportu zostanie wyświetlona pusta.</span><span class="sxs-lookup"><span data-stu-id="4c20b-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="4c20b-133">Przykład wystąpień</span><span class="sxs-lookup"><span data-stu-id="4c20b-133">Example instances</span></span>

<span data-ttu-id="4c20b-134">Hello przykład wystąpień sekcja zawiera informacje o kilka poszczególnych użytkowników, sesji lub zdarzeń, które są dopasowane wg hello bieżącego zapytania.</span><span class="sxs-lookup"><span data-stu-id="4c20b-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="4c20b-135">Biorąc pod uwagę i eksploracji hello zachowania jednostek w tooaggregates dodanie zapewniają wgląd w sposób osoby faktycznie używają Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="4c20b-136">Insights</span><span class="sxs-lookup"><span data-stu-id="4c20b-136">Insights</span></span> 

<span data-ttu-id="4c20b-137">pasek boczny Insights Hello pokazuje dużych klastrach użytkowników, które mają wspólne właściwości.</span><span class="sxs-lookup"><span data-stu-id="4c20b-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="4c20b-138">Tych klastrów można ujawnić zaskakująco trendy w sposób użytkownicy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="4c20b-139">Na przykład, jeśli 40% wszystkich hello użycia aplikacji pochodzi z osoby za pomocą jednej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c20b-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="4c20b-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c20b-140">Next steps</span></span>
- <span data-ttu-id="4c20b-141">Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="4c20b-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="4c20b-142">Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.</span><span class="sxs-lookup"><span data-stu-id="4c20b-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="4c20b-143">Lejki</span><span class="sxs-lookup"><span data-stu-id="4c20b-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="4c20b-144">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="4c20b-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="4c20b-145">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="4c20b-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="4c20b-146">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="4c20b-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="4c20b-147">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="4c20b-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

