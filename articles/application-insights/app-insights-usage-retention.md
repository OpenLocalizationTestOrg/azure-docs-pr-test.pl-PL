---
title: "Analiza przechowywania użytkownika dla aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zwraca liczbę użytkowników do aplikacji?"
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="cd234-103">Analiza przechowywania użytkownika dla aplikacji sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="cd234-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="cd234-104">Funkcja przechowywania w [Azure Application Insights](app-insights-overview.md) pomaga analizować ilu użytkowników powrót do aplikacji i jak często wykonywać określone zadania lub osiągnięcia celów.</span><span class="sxs-lookup"><span data-stu-id="cd234-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="cd234-105">Na przykład po uruchomieniu gier lokacji można porównywać liczby użytkowników, którzy wróć do witryny po utracie gry o numerze którzy powrócić po nadanie pierwszeństwa.</span><span class="sxs-lookup"><span data-stu-id="cd234-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="cd234-106">Ta wiedza może pomóc w usprawnieniu zarówno użytkowników, jak i jej strategią biznesową.</span><span class="sxs-lookup"><span data-stu-id="cd234-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="cd234-107">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="cd234-107">Get started</span></span>

<span data-ttu-id="cd234-108">Jeśli nie widzisz jeszcze danych w narzędziu przechowywania w portalu usługi Application Insights [Dowiedz się, jak rozpocząć pracę z narzędziami użycia](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd234-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="cd234-109">Narzędzie przechowywania</span><span class="sxs-lookup"><span data-stu-id="cd234-109">The Retention tool</span></span>

![Narzędzie utrzymywania](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="cd234-111">Pasek narzędzi umożliwia tworzenia nowych raportów przechowywania, otwórz istniejących raportów przechowywania, Zapisz bieżący raport przechowywania lub Zapisz jako cofnięcie zmian wprowadzonych do zapisanych raportów, odświeżania danych w raporcie udostępnianie raportów za pośrednictwem poczty e-mail lub bezpośredniego łącza i uzyskać dostęp do strony dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="cd234-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="cd234-112">Domyślnie przechowywania zawiera wszystkich użytkowników, którzy niczego została następnie wrócił i czy czymkolwiek innym przez okres.</span><span class="sxs-lookup"><span data-stu-id="cd234-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="cd234-113">Możesz wybrać inną kombinację zdarzeń, aby zawęzić na działania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd234-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="cd234-114">Dodaj co najmniej jeden filtr właściwości.</span><span class="sxs-lookup"><span data-stu-id="cd234-114">Add one or more filters on properties.</span></span> <span data-ttu-id="cd234-115">Na przykład można skoncentrować się na użytkowników w danym kraju lub regionu.</span><span class="sxs-lookup"><span data-stu-id="cd234-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="cd234-116">Kliknij przycisk **aktualizacji** kliknij ikonę znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="cd234-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="cd234-117">Ogólny wykresu przechowywania przedstawia podsumowanie przechowywania użytkownika przez wybrany okres czasu.</span><span class="sxs-lookup"><span data-stu-id="cd234-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="cd234-118">Siatka pokazuje liczbę użytkowników zachowane zgodnie z konstruktora zapytań w #2.</span><span class="sxs-lookup"><span data-stu-id="cd234-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="cd234-119">Każdy wiersz reprezentuje kohorty użytkowników, który wykonał wszystkie zdarzenia w przedstawionym okresie.</span><span class="sxs-lookup"><span data-stu-id="cd234-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="cd234-120">Każdej komórki w wierszu pokazuje, ile tego kohorty zwróciła co najmniej raz w późniejszym terminie.</span><span class="sxs-lookup"><span data-stu-id="cd234-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="cd234-121">W przypadku niektórych użytkowników może zwrócić więcej niż jednym okresie.</span><span class="sxs-lookup"><span data-stu-id="cd234-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="cd234-122">Karty insights Pokaż górny pięć inicjujący zdarzenia i górny pięć zwrócony umożliwić użytkownikom lepsze zrozumienie ich przechowywania raportu.</span><span class="sxs-lookup"><span data-stu-id="cd234-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Przesuwania myszy przechowywania](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="cd234-124">Użytkownicy mogą umieść kursor nad komórek narzędzie przechowywania dostępu etykietki narzędzia i przycisk analytics wyjaśniający, co oznacza komórki do.</span><span class="sxs-lookup"><span data-stu-id="cd234-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="cd234-125">Przycisk Analytics powoduje przejście do narzędzia do analizy za pomocą wstępnie wypełnionych kwerendy do generowania użytkowników z komórki.</span><span class="sxs-lookup"><span data-stu-id="cd234-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="cd234-126">Umożliwia śledzenie przechowywania zdarzeń biznesowych</span><span class="sxs-lookup"><span data-stu-id="cd234-126">Use business events to track retention</span></span>

<span data-ttu-id="cd234-127">Aby uzyskać najbardziej przydatne analizy przechowywania, pomiarów zdarzenia, które reprezentują znaczących działalności.</span><span class="sxs-lookup"><span data-stu-id="cd234-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="cd234-128">Na przykład wielu użytkowników może zostać otwarta strona w aplikacji bez gry, który jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="cd234-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="cd234-129">Śledzenia po prostu wyświetleń strony w związku z tym Podaj oszacowanie niedokładne ile osób powrócić do gry po korzystających z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="cd234-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="cd234-130">Aby uzyskać jasny obraz przekazujących odtwarzaczy, aplikacji należy wysłać zdarzenie niestandardowe, gdy użytkownik faktycznie odgrywa.</span><span class="sxs-lookup"><span data-stu-id="cd234-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="cd234-131">Jest dobrą praktyką jest kodem niestandardowych zdarzeń, które reprezentują akcji klucza biznesowych i ich używać do przechowywania analizy.</span><span class="sxs-lookup"><span data-stu-id="cd234-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="cd234-132">Aby przechwycić wyniku gier, należy napisać wiersza kodu w celu wysyłania niestandardowych zdarzeń do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cd234-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="cd234-133">Podczas pisania kodu strony sieci web lub w środowisku Node.JS, wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="cd234-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="cd234-134">Lub w kodzie serwera ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="cd234-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="cd234-135">[Dowiedz się więcej na temat zapisywania zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="cd234-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="cd234-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd234-136">Next steps</span></span>
- <span data-ttu-id="cd234-137">Aby umożliwić korzystanie z użycia, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="cd234-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="cd234-138">Jeżeli już zdarzeń niestandardowych lub wyświetleń strony, Poznaj narzędzia użycia, aby dowiedzieć się, jak używać usługi przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cd234-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="cd234-139">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="cd234-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="cd234-140">Lejki</span><span class="sxs-lookup"><span data-stu-id="cd234-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="cd234-141">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="cd234-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="cd234-142">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="cd234-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="cd234-143">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd234-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


