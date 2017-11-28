---
title: "Analiza przechowywania aaaUser dla aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Ilu użytkowników zwraca tooyour aplikacji?"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="25466-103">Analiza przechowywania użytkownika dla aplikacji sieci web za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="25466-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="25466-104">Funkcja przechowywania Hello [Azure Application Insights](app-insights-overview.md) pomaga analizować ilu użytkowników zwracać tooyour aplikacji i jak często wykonywać określone zadania lub osiągnięcia celów.</span><span class="sxs-lookup"><span data-stu-id="25466-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="25466-105">Na przykład po uruchomieniu gier lokacji można porównywać hello liczby użytkowników, którzy zwracać toohello lokacji po utracie gry o numerze hello którzy powrócić po nadanie pierwszeństwa.</span><span class="sxs-lookup"><span data-stu-id="25466-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="25466-106">Ta wiedza może pomóc w usprawnieniu zarówno użytkowników, jak i jej strategią biznesową.</span><span class="sxs-lookup"><span data-stu-id="25466-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="25466-107">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="25466-107">Get started</span></span>

<span data-ttu-id="25466-108">Jeśli nie widzisz jeszcze danych w narzędziu przechowywania hello w portalu usługi Application Insights hello [Dowiedz się, jak tooget pracę z narzędziami użycia hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25466-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="25466-109">Narzędzie do przechowywania Hello</span><span class="sxs-lookup"><span data-stu-id="25466-109">hello Retention tool</span></span>

![Narzędzie utrzymywania](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="25466-111">Hello narzędzi umożliwia użytkownikom toocreate nowe raporty przechowywania, otwórz istniejących raportów przechowywania, Zapisz bieżący raport do przechowywania lub Zapisz jako, Przywróć zmiany toosaved raporty, odświeżania danych w hello raport, udziału za pośrednictwem poczty e-mail lub bezpośredniego łącza i hello dostępu stronę dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="25466-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="25466-112">Domyślnie przechowywania zawiera wszystkich użytkowników, którzy niczego została następnie wrócił i czy czymkolwiek innym przez okres.</span><span class="sxs-lookup"><span data-stu-id="25466-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="25466-113">Można wybrać inną kombinację zdarzenia toonarrow hello fokus na działania konkretnego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25466-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="25466-114">Dodaj co najmniej jeden filtr właściwości.</span><span class="sxs-lookup"><span data-stu-id="25466-114">Add one or more filters on properties.</span></span> <span data-ttu-id="25466-115">Na przykład można skoncentrować się na użytkowników w danym kraju lub regionu.</span><span class="sxs-lookup"><span data-stu-id="25466-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="25466-116">Kliknij przycisk **aktualizacji** po ustawieniu filtrów hello.</span><span class="sxs-lookup"><span data-stu-id="25466-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="25466-117">Hello ogólną przechowywania wykres przedstawia podsumowanie przechowywania użytkownika między hello w wybranym okresie.</span><span class="sxs-lookup"><span data-stu-id="25466-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="25466-118">Siatka Hello pokazuje hello liczbę użytkowników, przechowywane zgodnie z konstruktora zapytań toohello w #2.</span><span class="sxs-lookup"><span data-stu-id="25466-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="25466-119">Każdy wiersz reprezentuje kohorty użytkowników, który wykonał wszystkie zdarzenia w czasie hello przedstawionym okresie.</span><span class="sxs-lookup"><span data-stu-id="25466-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="25466-120">Każdej komórki w wierszu hello pokazuje, ile tego kohorty zwróciła co najmniej raz w późniejszym terminie.</span><span class="sxs-lookup"><span data-stu-id="25466-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="25466-121">W przypadku niektórych użytkowników może zwrócić więcej niż jednym okresie.</span><span class="sxs-lookup"><span data-stu-id="25466-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="25466-122">karty insights Hello Pokaż górny pięć zdarzenia inicjujący i pięciu najwyższego zwracany zdarzenia toogive użytkowników lepiej zrozumieć ich przechowywania raportu.</span><span class="sxs-lookup"><span data-stu-id="25466-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Przesuwania myszy przechowywania](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="25466-124">Użytkownicy mogą umieść kursor nad komórek na powitania przechowywania narzędzia tooaccess hello analytics przycisku, która oznacza wyjaśniający, jakie komórki hello etykietki narzędzi.</span><span class="sxs-lookup"><span data-stu-id="25466-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="25466-125">przycisk Analytics Hello pobiera narzędzie analityczne toohello użytkowników z użytkownikami toogenerate wstępnie wypełnione zapytania hello komórki.</span><span class="sxs-lookup"><span data-stu-id="25466-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="25466-126">Użyj przechowywania tootrack zdarzenia biznesowe</span><span class="sxs-lookup"><span data-stu-id="25466-126">Use business events tootrack retention</span></span>

<span data-ttu-id="25466-127">tooget hello najbardziej przydatne przechowywania analizy, zdarzenia miary, które reprezentują znaczących działalności.</span><span class="sxs-lookup"><span data-stu-id="25466-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="25466-128">Na przykład wielu użytkowników może zostać otwarta strona w aplikacji bez gry hello, który jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="25466-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="25466-129">Śledzenie tylko hello wyświetleń strony w związku z tym Podaj oszacowanie niedokładne ile osób zwraca tooplay gry powitania po korzystających z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="25466-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="25466-130">tooget jasny obraz przekazujących odtwarzacze aplikacji należy wysłać zdarzenie niestandardowe, gdy użytkownik faktycznie jest odtwarzany.</span><span class="sxs-lookup"><span data-stu-id="25466-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="25466-131">Należy dobrze toocode niestandardowych zdarzeń, które reprezentują akcji klucza biznesowych i ich używać do przechowywania analizy.</span><span class="sxs-lookup"><span data-stu-id="25466-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="25466-132">toocapture hello wyniku gier, należy toowrite wiersz kodu toosend tooApplication zdarzenie niestandardowe szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="25466-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="25466-133">Podczas pisania kodu strony sieci web hello lub w środowisku Node.JS, wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="25466-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="25466-134">Lub w kodzie serwera ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="25466-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="25466-135">[Dowiedz się więcej na temat zapisywania zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="25466-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="25466-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25466-136">Next steps</span></span>
- <span data-ttu-id="25466-137">Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="25466-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="25466-138">Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.</span><span class="sxs-lookup"><span data-stu-id="25466-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="25466-139">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="25466-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="25466-140">Lejki</span><span class="sxs-lookup"><span data-stu-id="25466-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="25466-141">User Flows (Przepływy użytkowników)</span><span class="sxs-lookup"><span data-stu-id="25466-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="25466-142">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="25466-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="25466-143">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="25466-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


