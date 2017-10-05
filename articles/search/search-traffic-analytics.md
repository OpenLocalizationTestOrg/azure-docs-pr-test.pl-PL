---
title: "Wyszukaj analizy ruchu w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Włącz analizy ruchu wyszukiwania dla usługi wyszukiwanie Azure, Usługa wyszukiwania w chmurze, obsługiwanych w systemie Microsoft Azure, aby odblokować informacjami na temat użytkowników i danych."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="cc751-103">Co to jest analiza ruchu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="cc751-103">What is search traffic analytics</span></span>
<span data-ttu-id="cc751-104">Analiza ruchu wyszukiwania to wzorzec wykonania sprzężenia zwrotnego dla usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="cc751-105">Ten wzorzec opisano niezbędnych danych i jak zbierać za pomocą usługi Application Insights, wiodące branży monitorowania usług w wielu platform.</span><span class="sxs-lookup"><span data-stu-id="cc751-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="cc751-106">Analizy ruchu wyszukiwania umożliwia wgląd we usługi wyszukiwania i odblokować informacjami na temat użytkowników i ich zachowanie.</span><span class="sxs-lookup"><span data-stu-id="cc751-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="cc751-107">Dzięki użyciu dane dotyczące użytkowników wybierz, jest możliwe do podjęcia decyzji, które dodatkowo udoskonalić wyszukiwania i wycofania, gdy wyniki są nie oczekiwano co.</span><span class="sxs-lookup"><span data-stu-id="cc751-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="cc751-108">Usługa Azure Search udostępnia rozwiązanie telemetrii integrującą Azure Application Insights i usługi Power BI, aby zapewnić szczegółowe monitorowanie i śledzenie.</span><span class="sxs-lookup"><span data-stu-id="cc751-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="cc751-109">Ponieważ interakcji z usługi Azure Search jest tylko za pośrednictwem interfejsów API, telemetrii musi być implementowana przez deweloperów w wyszukiwaniu, postępując zgodnie z instrukcjami na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="cc751-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="cc751-110">Zidentyfikuj odpowiednie wyszukiwanie danych</span><span class="sxs-lookup"><span data-stu-id="cc751-110">Identify the relevant search data</span></span>

<span data-ttu-id="cc751-111">Aby wyszukiwania przydatne metryki, jest niezbędne do logowania niektórych sygnały od użytkowników aplikacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="cc751-112">Te sygnały wskazują zawartość, która jest zainteresowanych użytkowników i ich zdaniem ich potrzebom.</span><span class="sxs-lookup"><span data-stu-id="cc751-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="cc751-113">Istnieją dwa sygnałów, których potrzebuje analizy ruchu wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="cc751-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="cc751-114">Zdarzenia wyszukiwania użytkownika wygenerowany: tylko zapytania wyszukiwania zainicjowane przez użytkownika są interesujące.</span><span class="sxs-lookup"><span data-stu-id="cc751-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="cc751-115">Żądania wyszukiwania służące do wypełniania aspektów, dodatkową zawartość lub informacje o wewnętrznych, nie są ważne i pochylanie i bias wyniki.</span><span class="sxs-lookup"><span data-stu-id="cc751-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="cc751-116">Zdarzenia kliknięcia użytkownika wygenerowany: przez kliknięć w tym dokumencie, możemy odwoływać się do użytkownika, wybierając wynik wyszukiwania określonego zwrócone w wyniku zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="cc751-117">Kliknięcie zazwyczaj oznacza, że dokument odpowiednich wyników zapytania wyszukiwania określonych.</span><span class="sxs-lookup"><span data-stu-id="cc751-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="cc751-118">Łączenie zdarzeń wyszukiwania i kliknij przycisk z identyfikatorem korelacji, istnieje możliwość do analizy zachowania użytkowników w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc751-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="cc751-119">Te szczegółowe dane wyszukiwania będą możliwe uzyskanie z tylko dzienników ruchu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="cc751-120">Jak zaimplementować analizy ruchu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="cc751-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="cc751-121">Sygnałów, o których wspomniano w poprzedniej sekcji musi można zbierać z aplikacji wyszukiwania, ponieważ użytkownik wchodzi w interakcję z nią.</span><span class="sxs-lookup"><span data-stu-id="cc751-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="cc751-122">Usługa Application Insights jest rozszerzalne rozwiązanie monitorowania, dostępne dla wielu platform przy użyciu opcji elastyczne instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="cc751-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="cc751-123">Użycie usługi Application Insights pozwala korzystać z raportów wyszukiwania usługi Power BI utworzonych przez usługi Azure Search, aby ułatwić analizę danych.</span><span class="sxs-lookup"><span data-stu-id="cc751-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="cc751-124">W [portal](https://portal.azure.com) arkusz wskazówkami na następujących tego wzorca telemetrii zawiera strony dla usługi Azure Search, bloku analizy ruchu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="cc751-125">Można również wybrać lub utworzyć zasobu usługi Application Insights i zobacz niezbędnych danych, w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="cc751-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Instrukcje dotyczące analizy ruchu wyszukiwania][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="cc751-127">1. Wybierz zasób usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc751-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="cc751-128">Musisz wybrać zasobu usługi Application Insights do użycia lub utwórz taki, jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="cc751-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="cc751-129">Korzystając z zasobem, który jest już używany do rejestrowania zdarzeń niestandardowych wymagane.</span><span class="sxs-lookup"><span data-stu-id="cc751-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="cc751-130">Tworząc nowy zasób usługi Application Insights, wszystkie typy aplikacji są prawidłowe dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="cc751-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="cc751-131">Wybierz jedną, która najlepiej pasuje do używanej platformy.</span><span class="sxs-lookup"><span data-stu-id="cc751-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="cc751-132">Do tworzenia klienta telemetrii w aplikacji potrzebny jest klucz instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="cc751-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="cc751-133">Możesz pobrać go z pulpitu nawigacyjnego portalu Application Insights, lub możesz pobrać go ze strony analizy ruchu wyszukiwania, wybierając wystąpienie, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="cc751-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="cc751-134">2. Instrumentacja aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc751-134">2. Instrument your application</span></span>

<span data-ttu-id="cc751-135">W tej fazie jest, gdzie możesz Instrumentacja własnych aplikacji wyszukiwania przy użyciu zasobu usługi Application Insights z utworzonego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="cc751-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="cc751-136">Istnieją cztery kroki, aby ten proces:</span><span class="sxs-lookup"><span data-stu-id="cc751-136">There are four steps to this process:</span></span>

<span data-ttu-id="cc751-137">**I. Tworzenie klienta telemetrii** jest obiekt, który wysyła zdarzenia do zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc751-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="cc751-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc751-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="cc751-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cc751-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="cc751-140">Dla innych języków i platform, zobacz pełne [listy](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="cc751-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="cc751-141">**II. Żądaj Identyfikatora wyszukiwania dla korelacji** służące do skorelowania żądania wyszukiwania kliknięć, należy mieć identyfikator korelacji, które odnoszą się te dwa następujące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="cc751-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="cc751-142">Usługa wyszukiwanie Azure umożliwia identyfikatora wyszukiwania możesz poprosić o nagłówka:</span><span class="sxs-lookup"><span data-stu-id="cc751-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="cc751-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc751-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="cc751-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cc751-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="cc751-145">**III. Zdarzenia dziennika wyszukiwania**</span><span class="sxs-lookup"><span data-stu-id="cc751-145">**III. Log Search events**</span></span>

<span data-ttu-id="cc751-146">Żądania wyszukiwania wystawiony przez użytkownika, zawsze należy rejestrować który jako zdarzenie wyszukiwania z następującego schematu na zdarzenie niestandardowe usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="cc751-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="cc751-147">**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (guid) z zapytania wyszukiwania (jest dostarczany w odpowiedzi wyszukiwania) **IndexName**: indeks usługi wyszukiwania (ciąg) jako Kwerenda **QueryTerms**: terminy wyszukiwania (ciąg) wprowadzony przez użytkownika **ResultCount**: (int) liczba dokumentów, które zostały zwrócone (jest dostarczany w odpowiedzi wyszukiwania)  **ScoringProfile**: (ciąg) Nazwa profilu oceniania używane, jeśli istnieje</span><span class="sxs-lookup"><span data-stu-id="cc751-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="cc751-148">Liczba żądań na kwerendach użytkownika wygenerowany przez dodanie $count = true, aby zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="cc751-149">Więcej informacji można znaleźć [tutaj](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="cc751-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="cc751-150">Pamiętaj, aby zalogować się wyłącznie zapytania wyszukiwania, które są generowane przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cc751-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="cc751-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc751-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="cc751-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cc751-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="cc751-153">**IV. Kliknij dziennika zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="cc751-153">**IV. Log Click events**</span></span>

<span data-ttu-id="cc751-154">Zawsze użytkownik kliknie dokumentu, który jest sygnał, który musi być zalogowany na potrzeby analizy wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="cc751-155">Niestandardowe zdarzenia usługi Application Insights umożliwia rejestrowanie zdarzeń z następującego schematu:</span><span class="sxs-lookup"><span data-stu-id="cc751-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="cc751-156">**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (globalny guid) zapytania wyszukiwania powiązanych **identyfikator**: identyfikator dokumentu (ciąg) **pozycji** : strona wyników rangę (int) dokumentu w wyszukiwaniu</span><span class="sxs-lookup"><span data-stu-id="cc751-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="cc751-157">Pozycja odwołuje się do kardynalnej kolejności w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc751-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="cc751-158">Jesteś mogą określać ten numer, tak długo, jak jest zawsze taki sam, aby umożliwić do porównania.</span><span class="sxs-lookup"><span data-stu-id="cc751-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="cc751-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="cc751-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="cc751-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cc751-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="cc751-161">3. Analizowanie z Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="cc751-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="cc751-162">Po instrumentacji aplikacji i sprawdzić, czy aplikacja jest poprawnie podłączony do usługi Application Insights, można użyć wstępnie zdefiniowanego szablonu utworzonych przez usługi Azure Search dla usługi Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="cc751-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="cc751-163">Ten szablon zawiera wykresów i tabel, które ułatwiają podejmowanie bardziej świadomych decyzji aby poprawić wydajność wyszukiwania, a znaczenie dla.</span><span class="sxs-lookup"><span data-stu-id="cc751-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="cc751-164">Do utworzenia wystąpienia szablonu pulpitu usługi Power BI, potrzebne są trzy informacje na temat usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc751-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="cc751-165">Te dane można znaleźć na stronie analizy ruchu wyszukiwania po wybraniu zasobu należy użyć</span><span class="sxs-lookup"><span data-stu-id="cc751-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Dane usługi Application Insights w bloku analizy ruchu wyszukiwania][2]

<span data-ttu-id="cc751-167">Metryki zawarte w szablonie pulpitu usługi Power BI:</span><span class="sxs-lookup"><span data-stu-id="cc751-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="cc751-168">Kliknij przycisk za pośrednictwem szybkość kont (.): współczynnik użytkowników, którzy kliknij na konkretny dokument do liczby całkowitej wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="cc751-169">Wyszukuje bez kliknięć: warunki dla zapytań, które zarejestrować kliknięć nie z góry</span><span class="sxs-lookup"><span data-stu-id="cc751-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="cc751-170">Najbardziej kliknięty dokumentów: najbardziej kliknięty dokumentów za pomocą Identyfikatora w ostatnich 24 godzin, 7 dni i 30 dni.</span><span class="sxs-lookup"><span data-stu-id="cc751-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="cc751-171">Pary popularnych dokumentu termin: warunki wynikających z tego samego dokumentu kliknięty, uporządkowanych według kliknięć.</span><span class="sxs-lookup"><span data-stu-id="cc751-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="cc751-172">Czas kliknij: zasobnikach kliknięć w okresie od zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="cc751-172">Time to click: clicks bucketed by time since the search query</span></span>

![Power BI szablonu do odczytywania z usługi Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="cc751-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc751-174">Next Steps</span></span>
<span data-ttu-id="cc751-175">Instrumentacja aplikacji wyszukiwania można pobrać wydajny i interesującego dane dotyczące usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cc751-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="cc751-176">Można znaleźć więcej informacji na temat usługi Application Insights [tutaj](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="cc751-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="cc751-177">Odwiedź stronę usługi Application Insights [cennikiem](https://azure.microsoft.com/pricing/details/application-insights/) Aby dowiedzieć się więcej na temat ich różnych warstwach usług.</span><span class="sxs-lookup"><span data-stu-id="cc751-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="cc751-178">Dowiedz się więcej na temat tworzenia wspaniałych raportów.</span><span class="sxs-lookup"><span data-stu-id="cc751-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="cc751-179">Zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="cc751-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
