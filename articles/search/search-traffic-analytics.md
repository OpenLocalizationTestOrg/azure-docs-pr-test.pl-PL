---
title: "aaaSearch analizy ruchu dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Włącz analizy ruchu wyszukiwania dla usługi wyszukiwanie Azure, Usługa wyszukiwania w chmurze, obsługiwanych w systemie Microsoft Azure, toounlock wgląd w użytkowników oraz danych."
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
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="1ec62-103">Co to jest analiza ruchu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1ec62-103">What is search traffic analytics</span></span>
<span data-ttu-id="1ec62-104">Analiza ruchu wyszukiwania to wzorzec wykonania sprzężenia zwrotnego dla usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="1ec62-105">Ten wzorzec opisano hello niezbędnych danych i jak toocollect za pomocą usługi Application Insights, wiodące branży monitorowania usług w wielu platform.</span><span class="sxs-lookup"><span data-stu-id="1ec62-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="1ec62-106">Analizy ruchu wyszukiwania umożliwia wgląd we usługi wyszukiwania i odblokować informacjami na temat użytkowników i ich zachowanie.</span><span class="sxs-lookup"><span data-stu-id="1ec62-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="1ec62-107">Dzięki użyciu dane dotyczące użytkowników wybierz, jest możliwe toomake decyzji, które dodatkowo poprawy wyników wyszukiwania i tooback poza kiedy hello wyniki są nie oczekiwano co.</span><span class="sxs-lookup"><span data-stu-id="1ec62-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="1ec62-108">Usługa Azure Search udostępnia rozwiązanie telemetrii integrującą usługi Application Insights dla platformy Azure i usługi Power BI tooprovide szczegółowe monitorowanie oraz śledzenie.</span><span class="sxs-lookup"><span data-stu-id="1ec62-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="1ec62-109">Ponieważ interakcji z usługi Azure Search jest tylko za pośrednictwem interfejsów API, telemetrii hello musi być implementowana przez deweloperów hello za pomocą wyszukiwania, postępując zgodnie z instrukcjami hello na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="1ec62-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="1ec62-110">Identyfikowanie hello odpowiednich wyszukiwania danych</span><span class="sxs-lookup"><span data-stu-id="1ec62-110">Identify hello relevant search data</span></span>

<span data-ttu-id="1ec62-111">toohave wyszukiwania przydatne metryki, jest konieczne toolog niektóre sygnały od użytkowników hello hello aplikacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="1ec62-112">Te sygnały oznaczającego zawartości, że użytkownicy są zainteresowani, a uważają, że odpowiednie tootheir musi.</span><span class="sxs-lookup"><span data-stu-id="1ec62-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="1ec62-113">Istnieją dwa sygnałów, których potrzebuje analizy ruchu wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="1ec62-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="1ec62-114">Zdarzenia wyszukiwania użytkownika wygenerowany: tylko zapytania wyszukiwania zainicjowane przez użytkownika są interesujące.</span><span class="sxs-lookup"><span data-stu-id="1ec62-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="1ec62-115">Wyszukiwanie żądań używanych toopopulate aspektów, dodatkową zawartość lub informacje o wewnętrznych, nie są ważne i pochylanie i bias wyniki.</span><span class="sxs-lookup"><span data-stu-id="1ec62-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="1ec62-116">Zdarzenia kliknięcia użytkownika wygenerowany: przez kliknięć w tym dokumencie, firma Microsoft można znaleźć użytkownika tooa wybranie wynik wyszukiwania określonego zwrócone w wyniku zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="1ec62-117">Kliknięcie zazwyczaj oznacza, że dokument odpowiednich wyników zapytania wyszukiwania określonych.</span><span class="sxs-lookup"><span data-stu-id="1ec62-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="1ec62-118">Łącząc zdarzenia wyszukiwania i kliknij przycisk z identyfikatorem korelacji jest możliwe tooanalyze hello zachowania użytkowników w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ec62-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="1ec62-119">Te szczegółowe dane wyszukiwania będą niemożliwe tooobtain z tylko dzienników ruchu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="1ec62-120">Jak tooimplement wyszukiwania analizy ruchu</span><span class="sxs-lookup"><span data-stu-id="1ec62-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="1ec62-121">sygnały Hello wymieniony w poprzednim hello sekcji należy zbierać z aplikacji wyszukiwania hello jako hello użytkownik wchodzi w interakcję z nią.</span><span class="sxs-lookup"><span data-stu-id="1ec62-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="1ec62-122">Usługa Application Insights jest rozszerzalne rozwiązanie monitorowania, dostępne dla wielu platform przy użyciu opcji elastyczne instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="1ec62-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="1ec62-123">Użycie usługi Application Insights pozwala korzystać z raportów wyszukiwania usługi Power BI hello utworzone przez usługę Azure Search toomake hello analizy danych.</span><span class="sxs-lookup"><span data-stu-id="1ec62-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="1ec62-124">W hello [portal](https://portal.azure.com) strona dla usługi Azure Search, bloku analizy ruchu wyszukiwania hello zawiera arkusz wskazówkami na następujących tego wzorca telemetrii.</span><span class="sxs-lookup"><span data-stu-id="1ec62-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="1ec62-125">Można również wybrać lub utworzyć zasobu usługi Application Insights i zobacz hello niezbędnych danych, w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="1ec62-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Instrukcje dotyczące analizy ruchu wyszukiwania][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="1ec62-127">1. Wybierz zasób usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="1ec62-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="1ec62-128">Należy tooselect toouse zasobu usługi Application Insights lub utwórz je, jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="1ec62-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="1ec62-129">Korzystając z zasobem, który ma już w hello toolog Użyj wymagany zdarzeń niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="1ec62-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="1ec62-130">Tworząc nowy zasób usługi Application Insights, wszystkie typy aplikacji są prawidłowe dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="1ec62-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="1ec62-131">Wybierz hello jedną, która najlepiej pasuje do platformy hello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1ec62-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="1ec62-132">Należy hello klucza Instrumentacji do tworzenia powitania klienta telemetrii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ec62-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="1ec62-133">Możesz pobrać go z pulpitu nawigacyjnego portalu Application Insights hello, lub możesz pobrać go ze strony analizy ruchu wyszukiwania hello, wybierając wystąpienia hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="1ec62-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="1ec62-134">2. Instrumentacja aplikacji</span><span class="sxs-lookup"><span data-stu-id="1ec62-134">2. Instrument your application</span></span>

<span data-ttu-id="1ec62-135">W tej fazie jest, gdzie możesz Instrumentacja własnych aplikacji wyszukiwania przy użyciu hello zasobu usługi Application Insights z hello utworzonego w kroku powyżej.</span><span class="sxs-lookup"><span data-stu-id="1ec62-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="1ec62-136">Istnieją cztery kroki procesu toothis:</span><span class="sxs-lookup"><span data-stu-id="1ec62-136">There are four steps toothis process:</span></span>

<span data-ttu-id="1ec62-137">**I. Tworzenie klienta telemetrii** obiekt hello, która wysyła zdarzenia toohello zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1ec62-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="1ec62-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="1ec62-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="1ec62-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1ec62-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="1ec62-140">Dla innych języków i platform, zobacz hello pełną [listy](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="1ec62-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="1ec62-141">**II. Żądaj Identyfikatora wyszukiwania dla korelacji** wyszukiwania toocorrelate żądań kliknięć, jest konieczne toohave identyfikator korelacji, które odnoszą się te dwa następujące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="1ec62-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="1ec62-142">Usługa wyszukiwanie Azure umożliwia identyfikatora wyszukiwania możesz poprosić o nagłówka:</span><span class="sxs-lookup"><span data-stu-id="1ec62-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="1ec62-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="1ec62-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="1ec62-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1ec62-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="1ec62-145">**III. Zdarzenia dziennika wyszukiwania**</span><span class="sxs-lookup"><span data-stu-id="1ec62-145">**III. Log Search events**</span></span>

<span data-ttu-id="1ec62-146">Zawsze żądania wyszukiwania wystawiony przez użytkownika, należy rejestrować który jako zdarzenie wyszukiwania z powitania po schematu niestandardowego zdarzenia usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1ec62-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="1ec62-147">**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (globalny guid) hello zapytania wyszukiwania (polega na odpowiedź wyszukiwania hello) **IndexName**: indeks usługi wyszukiwania (ciąg) toobe proszeni **QueryTerms**: terminy wyszukiwania (ciąg) wprowadzonej przez użytkownika hello **ResultCount**: (int) liczba dokumentów, które zostały zwrócone (polega na odpowiedź wyszukiwania hello)  **ScoringProfile**: hello oceniania profil używany, jeśli nazwa (ciąg)</span><span class="sxs-lookup"><span data-stu-id="1ec62-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="1ec62-148">Liczba żądań na kwerendach użytkownika wygenerowany przez dodanie $count = true tooyour zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="1ec62-149">Więcej informacji można znaleźć [tutaj](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="1ec62-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="1ec62-150">Należy pamiętać, tooonly zapytania wyszukiwania dziennika, które są generowane przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1ec62-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="1ec62-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="1ec62-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="1ec62-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1ec62-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="1ec62-153">**IV. Kliknij dziennika zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="1ec62-153">**IV. Log Click events**</span></span>

<span data-ttu-id="1ec62-154">Zawsze użytkownik kliknie dokumentu, który jest sygnał, który musi być zalogowany na potrzeby analizy wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="1ec62-155">Za pomocą usługi Application Insights zdarzeń niestandardowych toolog te zdarzenia hello następującego schematu:</span><span class="sxs-lookup"><span data-stu-id="1ec62-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="1ec62-156">**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (globalny guid) zapytania wyszukiwania powiązanych hello **identyfikator**: identyfikator dokumentu (ciąg) **pozycji** : strona wyników (int) rangę dokumentu hello na powitania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1ec62-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="1ec62-157">Pozycja odwołuje się kolejność toohello kardynalnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ec62-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="1ec62-158">Jesteś wolnego tooset ten numer tak długo, jak ma zawsze hello sam tooallow do porównania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="1ec62-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="1ec62-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="1ec62-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1ec62-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="1ec62-161">3. Analizowanie z Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1ec62-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="1ec62-162">Po instrumentacji aplikacji i zweryfikować, że aplikacja jest poprawnie połączony tooApplication szczegółowe informacje, można użyć wstępnie zdefiniowanego szablonu utworzonych przez usługi Azure Search dla usługi Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="1ec62-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="1ec62-163">Ten szablon zawiera wykresy, i tabele, które ułatwiają upewnij więcej świadomych decyzji tooimprove swoją wydajność wyszukiwania i przydatności.</span><span class="sxs-lookup"><span data-stu-id="1ec62-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="1ec62-164">Witaj tooinstantiate usługi Power BI szablonu pulpitu, potrzebne są trzy informacje na temat usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1ec62-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="1ec62-165">Te dane znajdują się w stronę analizy ruchu wyszukiwania hello, po wybraniu hello toouse zasobów</span><span class="sxs-lookup"><span data-stu-id="1ec62-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Dane usługi Application Insights w bloku analizy ruchu wyszukiwania hello][2]

<span data-ttu-id="1ec62-167">Metryki zawarte w szablonie pulpitu hello usługi Power BI:</span><span class="sxs-lookup"><span data-stu-id="1ec62-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="1ec62-168">Kliknij przycisk za pośrednictwem szybkość kont (.): współczynnik użytkowników, którzy klikną określonego dokumentu toohello liczby całkowitej wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="1ec62-169">Wyszukuje bez kliknięć: warunki dla zapytań, które zarejestrować kliknięć nie z góry</span><span class="sxs-lookup"><span data-stu-id="1ec62-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="1ec62-170">Najbardziej kliknięty dokumentów: najbardziej kliknięty dokumentów za pomocą Identyfikatora w hello ostatnich 24 godzin, 7 dni i 30 dni.</span><span class="sxs-lookup"><span data-stu-id="1ec62-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="1ec62-171">Pary popularnych dokumentu termin: terminów, które powoduje hello kliknięty tego samego dokumentu, uporządkowanych według kliknięć.</span><span class="sxs-lookup"><span data-stu-id="1ec62-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="1ec62-172">Czas tooclick: zasobnikach kliknięć w okresie od hello zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1ec62-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Power BI szablonu do odczytywania z usługi Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="1ec62-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ec62-174">Next Steps</span></span>
<span data-ttu-id="1ec62-175">Instrumentacja wyszukiwania tooget wydajny i interesującego danych aplikacji dotyczących usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1ec62-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="1ec62-176">Można znaleźć więcej informacji na temat usługi Application Insights [tutaj](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="1ec62-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="1ec62-177">Odwiedź stronę usługi Application Insights [cennikiem](https://azure.microsoft.com/pricing/details/application-insights/) toolearn więcej informacji na temat ich różnych warstwach usług.</span><span class="sxs-lookup"><span data-stu-id="1ec62-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="1ec62-178">Dowiedz się więcej na temat tworzenia wspaniałych raportów.</span><span class="sxs-lookup"><span data-stu-id="1ec62-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="1ec62-179">Zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="1ec62-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
