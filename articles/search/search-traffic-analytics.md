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
# <a name="what-is-search-traffic-analytics"></a>Co to jest analiza ruchu wyszukiwania
Analiza ruchu wyszukiwania to wzorzec wykonania sprzężenia zwrotnego dla usługi wyszukiwania. Ten wzorzec opisano hello niezbędnych danych i jak toocollect za pomocą usługi Application Insights, wiodące branży monitorowania usług w wielu platform.

Analizy ruchu wyszukiwania umożliwia wgląd we usługi wyszukiwania i odblokować informacjami na temat użytkowników i ich zachowanie. Dzięki użyciu dane dotyczące użytkowników wybierz, jest możliwe toomake decyzji, które dodatkowo poprawy wyników wyszukiwania i tooback poza kiedy hello wyniki są nie oczekiwano co.

Usługa Azure Search udostępnia rozwiązanie telemetrii integrującą usługi Application Insights dla platformy Azure i usługi Power BI tooprovide szczegółowe monitorowanie oraz śledzenie. Ponieważ interakcji z usługi Azure Search jest tylko za pośrednictwem interfejsów API, telemetrii hello musi być implementowana przez deweloperów hello za pomocą wyszukiwania, postępując zgodnie z instrukcjami hello na tej stronie.

## <a name="identify-hello-relevant-search-data"></a>Identyfikowanie hello odpowiednich wyszukiwania danych

toohave wyszukiwania przydatne metryki, jest konieczne toolog niektóre sygnały od użytkowników hello hello aplikacji wyszukiwania. Te sygnały oznaczającego zawartości, że użytkownicy są zainteresowani, a uważają, że odpowiednie tootheir musi.

Istnieją dwa sygnałów, których potrzebuje analizy ruchu wyszukiwania:

1. Zdarzenia wyszukiwania użytkownika wygenerowany: tylko zapytania wyszukiwania zainicjowane przez użytkownika są interesujące. Wyszukiwanie żądań używanych toopopulate aspektów, dodatkową zawartość lub informacje o wewnętrznych, nie są ważne i pochylanie i bias wyniki.

2. Zdarzenia kliknięcia użytkownika wygenerowany: przez kliknięć w tym dokumencie, firma Microsoft można znaleźć użytkownika tooa wybranie wynik wyszukiwania określonego zwrócone w wyniku zapytania wyszukiwania. Kliknięcie zazwyczaj oznacza, że dokument odpowiednich wyników zapytania wyszukiwania określonych.

Łącząc zdarzenia wyszukiwania i kliknij przycisk z identyfikatorem korelacji jest możliwe tooanalyze hello zachowania użytkowników w aplikacji. Te szczegółowe dane wyszukiwania będą niemożliwe tooobtain z tylko dzienników ruchu wyszukiwania.

## <a name="how-tooimplement-search-traffic-analytics"></a>Jak tooimplement wyszukiwania analizy ruchu

sygnały Hello wymieniony w poprzednim hello sekcji należy zbierać z aplikacji wyszukiwania hello jako hello użytkownik wchodzi w interakcję z nią. Usługa Application Insights jest rozszerzalne rozwiązanie monitorowania, dostępne dla wielu platform przy użyciu opcji elastyczne instrumentacji. Użycie usługi Application Insights pozwala korzystać z raportów wyszukiwania usługi Power BI hello utworzone przez usługę Azure Search toomake hello analizy danych.

W hello [portal](https://portal.azure.com) strona dla usługi Azure Search, bloku analizy ruchu wyszukiwania hello zawiera arkusz wskazówkami na następujących tego wzorca telemetrii. Można również wybrać lub utworzyć zasobu usługi Application Insights i zobacz hello niezbędnych danych, w jednym miejscu.

![Instrukcje dotyczące analizy ruchu wyszukiwania][1]

### <a name="1-select-an-application-insights-resource"></a>1. Wybierz zasób usługi Application Insights

Należy tooselect toouse zasobu usługi Application Insights lub utwórz je, jeśli nie masz już. Korzystając z zasobem, który ma już w hello toolog Użyj wymagany zdarzeń niestandardowych.

Tworząc nowy zasób usługi Application Insights, wszystkie typy aplikacji są prawidłowe dla tego scenariusza. Wybierz hello jedną, która najlepiej pasuje do platformy hello, którego używasz.

Należy hello klucza Instrumentacji do tworzenia powitania klienta telemetrii aplikacji. Możesz pobrać go z pulpitu nawigacyjnego portalu Application Insights hello, lub możesz pobrać go ze strony analizy ruchu wyszukiwania hello, wybierając wystąpienia hello ma toouse.

### <a name="2-instrument-your-application"></a>2. Instrumentacja aplikacji

W tej fazie jest, gdzie możesz Instrumentacja własnych aplikacji wyszukiwania przy użyciu hello zasobu usługi Application Insights z hello utworzonego w kroku powyżej. Istnieją cztery kroki procesu toothis:

**I. Tworzenie klienta telemetrii** obiekt hello, która wysyła zdarzenia toohello zasobu usługi Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Dla innych języków i platform, zobacz hello pełną [listy](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Żądaj Identyfikatora wyszukiwania dla korelacji** wyszukiwania toocorrelate żądań kliknięć, jest konieczne toohave identyfikator korelacji, które odnoszą się te dwa następujące zdarzenia. Usługa wyszukiwanie Azure umożliwia identyfikatora wyszukiwania możesz poprosić o nagłówka:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Zdarzenia dziennika wyszukiwania**

Zawsze żądania wyszukiwania wystawiony przez użytkownika, należy rejestrować który jako zdarzenie wyszukiwania z powitania po schematu niestandardowego zdarzenia usługi Application Insights:

**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (globalny guid) hello zapytania wyszukiwania (polega na odpowiedź wyszukiwania hello) **IndexName**: indeks usługi wyszukiwania (ciąg) toobe proszeni **QueryTerms**: terminy wyszukiwania (ciąg) wprowadzonej przez użytkownika hello **ResultCount**: (int) liczba dokumentów, które zostały zwrócone (polega na odpowiedź wyszukiwania hello)  **ScoringProfile**: hello oceniania profil używany, jeśli nazwa (ciąg)

> [!NOTE]
> Liczba żądań na kwerendach użytkownika wygenerowany przez dodanie $count = true tooyour zapytania wyszukiwania. Więcej informacji można znaleźć [tutaj](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Należy pamiętać, tooonly zapytania wyszukiwania dziennika, które są generowane przez użytkowników.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Kliknij dziennika zdarzeń**

Zawsze użytkownik kliknie dokumentu, który jest sygnał, który musi być zalogowany na potrzeby analizy wyszukiwania. Za pomocą usługi Application Insights zdarzeń niestandardowych toolog te zdarzenia hello następującego schematu:

**ServiceName**: Nazwa usługi wyszukiwania (ciąg) **SearchId**: Unikatowy identyfikator (globalny guid) zapytania wyszukiwania powiązanych hello **identyfikator**: identyfikator dokumentu (ciąg) **pozycji** : strona wyników (int) rangę dokumentu hello na powitania wyszukiwania

> [!NOTE]
> Pozycja odwołuje się kolejność toohello kardynalnej w aplikacji. Jesteś wolnego tooset ten numer tak długo, jak ma zawsze hello sam tooallow do porównania.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Analizowanie z Power BI Desktop

Po instrumentacji aplikacji i zweryfikować, że aplikacja jest poprawnie połączony tooApplication szczegółowe informacje, można użyć wstępnie zdefiniowanego szablonu utworzonych przez usługi Azure Search dla usługi Power BI desktop.
Ten szablon zawiera wykresy, i tabele, które ułatwiają upewnij więcej świadomych decyzji tooimprove swoją wydajność wyszukiwania i przydatności.

Witaj tooinstantiate usługi Power BI szablonu pulpitu, potrzebne są trzy informacje na temat usługi Application Insights. Te dane znajdują się w stronę analizy ruchu wyszukiwania hello, po wybraniu hello toouse zasobów

![Dane usługi Application Insights w bloku analizy ruchu wyszukiwania hello][2]

Metryki zawarte w szablonie pulpitu hello usługi Power BI:

*   Kliknij przycisk za pośrednictwem szybkość kont (.): współczynnik użytkowników, którzy klikną określonego dokumentu toohello liczby całkowitej wyszukiwania.
*   Wyszukuje bez kliknięć: warunki dla zapytań, które zarejestrować kliknięć nie z góry
*   Najbardziej kliknięty dokumentów: najbardziej kliknięty dokumentów za pomocą Identyfikatora w hello ostatnich 24 godzin, 7 dni i 30 dni.
*   Pary popularnych dokumentu termin: terminów, które powoduje hello kliknięty tego samego dokumentu, uporządkowanych według kliknięć.
*   Czas tooclick: zasobnikach kliknięć w okresie od hello zapytania wyszukiwania

![Power BI szablonu do odczytywania z usługi Application Insights][3]


## <a name="next-steps"></a>Następne kroki
Instrumentacja wyszukiwania tooget wydajny i interesującego danych aplikacji dotyczących usługi wyszukiwania.

Można znaleźć więcej informacji na temat usługi Application Insights [tutaj](https://go.microsoft.com/fwlink/?linkid=842905). Odwiedź stronę usługi Application Insights [cennikiem](https://azure.microsoft.com/pricing/details/application-insights/) toolearn więcej informacji na temat ich różnych warstwach usług.

Dowiedz się więcej na temat tworzenia wspaniałych raportów. Zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Aby uzyskać więcej informacji

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
