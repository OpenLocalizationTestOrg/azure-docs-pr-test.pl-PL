---
title: "Analiza użytkowników, sesji i zdarzeń w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="02f20-103">Analiza użytkownikami, sesjami i zdarzeń w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="02f20-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="02f20-104">Dowiedz się, gdy użytkownicy korzystają z aplikacji sieci web, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają.</span><span class="sxs-lookup"><span data-stu-id="02f20-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="02f20-105">Analizowanie telemetrii działalności biznesowej i użycia za pomocą [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f20-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="02f20-106">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="02f20-106">Get started</span></span>

<span data-ttu-id="02f20-107">Jeśli nie widzisz jeszcze dane użytkowników, sesji lub bloków zdarzenia w portalu usługi Application Insights [Dowiedz się, jak rozpocząć pracę z narzędziami użycia](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f20-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="02f20-108">Narzędzie segmentacji użytkowników, sesji i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="02f20-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="02f20-109">Trzy bloków użycia umożliwia tego samego narzędzia selekcji i dane telemetryczne z aplikacji sieci web z trzema perspektyw.</span><span class="sxs-lookup"><span data-stu-id="02f20-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="02f20-110">Filtrowanie i dzielenia danych, można ujawnić informacjami na temat względną użycie różnych stron i funkcji.</span><span class="sxs-lookup"><span data-stu-id="02f20-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="02f20-111">**Narzędzie Użytkownicy**: używane wiele aplikacji i ich funkcje.</span><span class="sxs-lookup"><span data-stu-id="02f20-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="02f20-112">Użytkownicy są liczone przy użyciu anonimowego identyfikatorów przechowywane w plikach cookie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="02f20-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="02f20-113">Jedna osoba, za pomocą różnych przeglądarkach lub maszyny będą liczone jako więcej niż jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02f20-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="02f20-114">**Narzędzie sesje**: ile sesji aktywności użytkowników, zostały uwzględnione w pewnych stron i funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02f20-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="02f20-115">Sesja jest traktowane po pół godziny czas braku aktywności użytkownika, lub 24 godziny ciągłego użytkowania.</span><span class="sxs-lookup"><span data-stu-id="02f20-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="02f20-116">**Narzędzie zdarzenia**: jak często używane pewnych stron i funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02f20-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="02f20-117">Widok strony jest liczony przeglądarką załadowanie strony z aplikacji, pod warunkiem, że [zinstrumentowane on](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="02f20-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="02f20-118">Zdarzenie niestandardowe reprezentuje jedno wystąpienie określonego zdarzenia w aplikacji, często interakcji użytkownika, np. Kliknij przycisk lub zakończenie niektórych zadań.</span><span class="sxs-lookup"><span data-stu-id="02f20-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="02f20-119">Wstaw kod aplikacji w celu [generowanie zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="02f20-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Użycie narzędzia](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="02f20-121">Wykonywanie zapytania dla niektórych użytkowników</span><span class="sxs-lookup"><span data-stu-id="02f20-121">Querying for Certain Users</span></span> 

<span data-ttu-id="02f20-122">Zapoznaj się z różnych grup użytkowników, zmieniając opcje zapytania w górnej części narzędzia użytkowników:</span><span class="sxs-lookup"><span data-stu-id="02f20-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="02f20-123">Kto używane: Wybierz niestandardowych zdarzeń i wyświetlenia strony.</span><span class="sxs-lookup"><span data-stu-id="02f20-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="02f20-124">W trakcie: Wybierz zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="02f20-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="02f20-125">Przez: Wybierz sposób pojemnik danych przez pewien czas lub innej właściwości, takie jak przeglądarki lub Miasto.</span><span class="sxs-lookup"><span data-stu-id="02f20-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="02f20-126">Dzielenie przez: Wybierz właściwość za pomocą którego podziału lub segmentu danych.</span><span class="sxs-lookup"><span data-stu-id="02f20-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="02f20-127">Dodaj filtry: Ograniczyć zapytanie do niektórych użytkowników, sesji lub zdarzenia na podstawie ich właściwości, takie jak przeglądarki lub Miasto.</span><span class="sxs-lookup"><span data-stu-id="02f20-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="02f20-128">Zapisywanie i udostępnianie raportów</span><span class="sxs-lookup"><span data-stu-id="02f20-128">Saving and sharing reports</span></span> 
<span data-ttu-id="02f20-129">Użytkownicy raportów, prywatne tylko dla Ciebie w sekcji Moje raporty lub udostępnionego można zapisać z inne osoby z dostępem do tego zasobu usługi Application Insights w sekcji udostępnionych raportów.</span><span class="sxs-lookup"><span data-stu-id="02f20-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="02f20-130">Podczas zapisywania raportu lub edytowania jego właściwości, wybierz polecenie "Bieżący względny zakres czasu" Aby zapisać raport będzie stale odświeżyć dane, wracając niektórych stałej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="02f20-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="02f20-131">Wybierz opcję "Bieżący bezwzględny zakres czasu" Aby zapisać raport ustalonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="02f20-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="02f20-132">Należy pamiętać, że dane w usłudze Application Insights tylko są przechowywane przez 90 dni, więc jeśli minęło ponad 90 dni od raport z zakresem bezwzględnego czasu został zapisany, raport zostanie wyświetlona pusta.</span><span class="sxs-lookup"><span data-stu-id="02f20-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="02f20-133">Przykład wystąpień</span><span class="sxs-lookup"><span data-stu-id="02f20-133">Example instances</span></span>

<span data-ttu-id="02f20-134">Sekcja wystąpień przykład zawiera informacje o kilka poszczególnych użytkowników, sesji lub zdarzeń, które są dopasowane wg bieżącego zapytania.</span><span class="sxs-lookup"><span data-stu-id="02f20-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="02f20-135">Biorąc pod uwagę i eksploracji zachowania jednostek, oprócz agregacje, zapewniają wgląd w sposób osoby faktycznie używają Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02f20-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="02f20-136">Insights</span><span class="sxs-lookup"><span data-stu-id="02f20-136">Insights</span></span> 

<span data-ttu-id="02f20-137">Pasek boczny szczegółowe informacje zawiera dużych klastrach użytkowników, które mają wspólne właściwości.</span><span class="sxs-lookup"><span data-stu-id="02f20-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="02f20-138">Tych klastrów można ujawnić zaskakująco trendy w sposób użytkownicy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02f20-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="02f20-139">Na przykład, jeśli 40% wszystkich użycia aplikacji pochodzi z osoby za pomocą jednej funkcji.</span><span class="sxs-lookup"><span data-stu-id="02f20-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="02f20-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02f20-140">Next steps</span></span>
- <span data-ttu-id="02f20-141">Aby umożliwić korzystanie z użycia, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="02f20-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="02f20-142">Jeżeli już zdarzeń niestandardowych lub wyświetleń strony, Poznaj narzędzia użycia, aby dowiedzieć się, jak używać usługi przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="02f20-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="02f20-143">Lejki</span><span class="sxs-lookup"><span data-stu-id="02f20-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="02f20-144">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="02f20-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="02f20-145">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="02f20-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="02f20-146">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="02f20-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="02f20-147">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="02f20-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

