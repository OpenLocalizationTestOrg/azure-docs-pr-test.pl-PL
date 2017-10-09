---
title: "aplikacje sieci web usługi Application Insights aaaAzure JavaScript | Dokumentacja firmy Microsoft"
description: "Pobieranie liczników wyświetleń stron i sesji, danych klienta sieci Web oraz śledzenie wzorców użycia. Wykrywanie wyjątków i problemów z wydajnością na stronach sieci Web w języku JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Usługa Application Insights dla stron sieci Web
Dowiedz się o hello wydajności i użycia aplikacji lub strony sieci web. Jeśli dodasz [usługi Application Insights](app-insights-overview.md) tooyour skrypt strony, możesz uzyskać chronometrażu ładunków strona i wywołania AJAX, liczby i szczegóły błędów AJAX, a także użytkowników i liczby sesji w wyjątków przeglądarki. Wszystkie te dane możesz rozdzielić według strony, systemu operacyjnego klienta i wersji przeglądarki, lokalizacji geograficznej i innych wymiarów. Możesz ustawić alerty związane z liczbami błędów lub powolnym ładowaniem strony. I zaznaczając śledzenie wywołań kodu JavaScript, można śledzić używania różnych funkcji hello aplikacji strony sieci web.

Usługi Application Insights można używać z dowolnymi stronami sieci Web — wystarczy dodać krótki fragment kodu JavaScript. Jeśli Twoja usługa sieci Web jest zaprogramowana w technologii [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md), możesz zintegrować telemetrię pochodzącą z serwera i klientów.

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij pozycję Przeglądarka](./media/app-insights-javascript/03.png)

Musisz mieć subskrypcję za[Microsoft Azure](https://azure.com). Jeśli zespół ma organizacyjnej subskrypcji, poproś hello właściciela tooadd Twojego tooit Account firmy Microsoft. Tworząc strony i używając ich na małą skalę, nie poniesiesz żadnych kosztów.

## <a name="set-up-application-insights-for-your-web-page"></a>Konfigurowanie usługi Application Insights dla strony sieci Web
Dodaj hello modułu ładującego kodu fragment tooyour stron sieci web, w następujący sposób.

### <a name="open-or-create-application-insights-resource"></a>Otwieranie lub tworzenie zasobu usługi Application Insights
Hello zasobu usługi Application Insights jest, gdzie są wyświetlane dane dotyczące wydajności i użycia ze strony. 

Zaloguj się do [portalu Azure](https://portal.azure.com).

Jeśli już skonfigurowane monitorowania po stronie serwera na powitania aplikacji, masz już zasobu:

![Wybierz kolejno opcje Przeglądaj, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-find.png)

Jeśli nie ma zasobu, utwórz go:

![Wybierz kolejno opcje Nowe, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-create.png)

*Już masz pytania?* [Więcej informacji na temat tworzenia zasobu](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Dodaj hello SDK skryptu tooyour aplikacji lub strony sieci web
W Szybki Start Pobierz hello skryptu dla stron sieci web:

![W bloku Omówienie aplikacji wybierz pozycję Szybki Start, Pobierz kod toomonitor stron sieci web. Skopiuj skrypt hello.](./media/app-insights-javascript/02-monitor-web-page.png)

Wstaw skrypt hello tuż przed hello `</head>` tag każdej strony ma tootrack. Jeśli strony głównej witryny sieci Web, można umieścić hello skryptu. Na przykład:

* W projekcie ASP.NET MVC możesz umieścić go w pliku `View\Shared\_Layout.cshtml`
* W witrynie programu SharePoint, na panelu sterowania hello, otwórz [ustawienia witryny / strony wzorcowej](app-insights-sharepoint.md).

skrypt Hello zawiera klucz Instrumentacji hello kieruje zasobu usługi Application Insights tooyour danych hello. 

([Bardziej szczegółowy opis hello skryptu. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Jeśli używasz dobrze znanej struktury stron sieci Web, poszukaj adapterów usługi Application Insights. Takim adapterem jest na przykład [moduł AngularJS](http://ngmodules.org/modules/angular-appinsights)).*

## <a name="detailed-configuration"></a>Konfiguracja szczegółowa
Istnieje kilka [parametrów](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), które można ustawić, chociaż w większości przypadków nie jest to potrzebne. Na przykład można wyłączyć lub Ogranicz liczbę hello wywołania Ajax zgłaszanych w ciągu widok strony (tooreduce ruch). Można także ustawić debugowania trybu toohave telemetrii Przenieś szybko przez potok hello bez jest umieścić w zadaniu wsadowym.

tooset tych parametrów, Wyszukaj ten wiersz w hello fragment kodu i dodać więcej elementów oddzielonych przecinkami po nim:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Witaj [dostępne parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) obejmują:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Uruchamianie aplikacji
Uruchom aplikację sieci web i używać go podczas toogenerate telemetrii i zaczekaj kilka sekund. Możesz uruchomić go za pomocą hello **F5** klucza na komputerze deweloperskim lub opublikować go, pozwalając użytkownikom na odtwarzania z nim.

Toocheck hello telemetrii, że aplikacja sieci web wysyła tooApplication szczegółowe informacje, należy użyć narzędzia debugowania w przeglądarce (**F12** w wielu przeglądarkach). Dane są wysyłane toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Eksplorowanie danych wydajności przeglądarki
Otwórz hello tooshow bloku przeglądarki zagregowane dane dotyczące wydajności z przeglądarki użytkownika.

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij kolejno opcje Ustawienia, Przeglądarki](./media/app-insights-javascript/03.png)

*Jeszcze nie ma danych? Kliknij przycisk **Odśwież** u góry hello hello strony. Nadal nic? Zobacz [Rozwiązywanie problemów ](app-insights-troubleshoot-faq.md).*

Blok przeglądarki Hello jest [bloku Eksploratora metryk](app-insights-metrics-explorer.md) filtry ustawień wstępnych i wyboru wykresu. Zakres czasu hello, filtrów i konfiguracji wykresu można edytować, jeśli i zapisać wynik hello jako ulubioną. Kliknij przycisk **przywrócić ustawienia domyślne** tooget toohello wstecz oryginalną konfigurację bloku.

## <a name="page-load-performance"></a>Wydajność ładowania strony
Na powitania top jest segmentowanych wykres czasy ładowania stron. Witaj całkowita wysokość wykresu hello reprezentuje hello Średni czas tooload i wyświetlania stron z aplikacji w przeglądarce użytkownika. Witaj czas jest mierzony z, gdy przeglądarka hello wysyła hello początkowe żądanie HTTP do wszystkich synchroniczne obciążenia, który zdarzenia są przetwarzane w tym układ i uruchamianie skryptów. Nie obejmuje zadań asynchronicznych, takich jak ładowanie składników Web Part z wywołań AJAX.

Wykres Hello segmenty czas ładowania strony całkowita hello na powitania [standardowe czasy określone przez W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Należy pamiętać, że hello *połączeń sieciowych* czasu jest niższa niż oczekujesz może często, ponieważ jest to wartość średnia za pośrednictwem wszystkich żądań z serwera toohello przeglądarki hello. Wiele żądań poszczególnych ma czas połączenia, 0, ponieważ istnieje już serwer toohello aktywnego połączenia.

### <a name="slow-loading"></a>Powolne ładowanie?
Powolne ładowanie stron jest głównym powodem niezadowolenia użytkowników. Jeśli hello wykres wskazuje powolne obciążeń, jest łatwe toodo przeanalizować diagnostycznych.

Witaj wykres pokazuje średnią hello ładunków strona w aplikacji. toosee, jeśli hello problem jest ograniczone tooparticular stron, wygląd dalsze dół hello bloku, w przypadku, gdy istnieje siatka segmentowanych przez adres URL strony:

![](./media/app-insights-javascript/09-page-perf.png)

Zwróć uwagę, liczba widoku strony hello i odchylenie standardowe. Jeśli liczba stron hello jest bardzo niskie, następnie hello problem nie ma wpływu na użytkowników znacznie. Wysoka odchylenie standardowe (średnia porównywalne toohello, sam) wskazuje wiele odmiany między pojedynczych pomiarów.

**Wyświetl szczegóły dla jednego adresu URL i jednej strony.** Kliknij pozycję wszystkie strony toosee Nazwa bloku przeglądarki wykresy filtrowane toothat tylko adres URL; a następnie na wystąpienie strony widoku.

![](./media/app-insights-javascript/35.png)

Kliknij przycisk `...` pełną listę właściwości dla tego zdarzenia, lub zbadać wywołania Ajax hello oraz powiązanych zdarzeń. Powolnych połączeń Ajax hello mają wpływ na ogólne strony czas ładowania, jeśli są one synchronicznego. Powiązane zdarzenia zawierają żądań serwera na powitania tego samego adresu URL (Jeśli po skonfigurowaniu usługi Application Insights na serwerze sieci web).

**Wydajność stron w czasie.** W bloku przeglądarki hello zmienić hello czas ładowania strony widoku siatki w toosee wykresu wiersza, jeśli wystąpiły pików w określonym czasie:

![Kliknij nagłówek hello hello siatki i wybierz nowy typ wykresu](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentowanie według innych wymiarów.** Może być stron sieci są wolniejszej tooload w określonej lokalizacji przeglądarki, system operacyjny klienta lub użytkownika? Dodaj nowy wykres i eksperymentować hello **Group by** wymiaru.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Wydajność wywołań AJAX
Upewnij się. że dowolne wywołania AJAX na stronach sieci Web działają poprawnie. Są często używane toofill elementów na stronie asynchronicznie. Mimo że hello całej strony może załadować natychmiast, użytkowników można można frustracji przez uruchomieniem w części sieci web puste oczekiwanie na dane tooappear w nich.

Wywołania AJAX ze strony sieci web są wyświetlane w bloku przeglądarki hello jako zależności.

Istnieją wykresy podsumowań w górnej części bloku hello hello:

![](./media/app-insights-javascript/31.png)

a poniżej szczegółowe siatki:

![](./media/app-insights-javascript/33.png)

Klikaj poszczególne wiersze, aby uzyskać szczegółowe informacje.

> [!NOTE]
> Jeśli usuniesz hello filtru przeglądarki w bloku hello zarówno serwera, jak i zależności AJAX zostaną uwzględnione w wykresach. Kliknij przycisk Przywróć domyślne filtrów hello tooreconfigure.
> 
> 

**toodrill do wywołania Ajax nie powiodło się** przewiń w dół siatki błędów zależności toohello, a następnie kliknij określonych wystąpień toosee wiersza.

![](./media/app-insights-javascript/37.png)


Kliknij przycisk `...` dla hello pełne dane telemetryczne dla wywołania Ajax.

### <a name="no-ajax-calls-reported"></a>Brak zgłoszonych wywołań Ajax?
Wywołania AJAX obejmują wszystkie wywołania HTTP/HTTPS ze skryptu hello strony sieci web. Jeśli nie widzisz ich zgłoszone, Sprawdź ten fragment kodu hello nie ustawia hello `disableAjaxTracking` lub `maxAjaxCallsPerView` [parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Wyjątki przeglądarki
W bloku przeglądarki hello jest wykres podsumowania wyjątki oraz siatka typów wyjątków dalsze dół hello bloku.

![](./media/app-insights-javascript/39.png)

Jeśli nie widzisz zgłaszane wyjątki przeglądarki, Sprawdź ten fragment kodu hello nie ustawia hello `disableExceptionTracking` [parametru](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Badanie zdarzeń wyświetlania pojedynczej strony

Zazwyczaj telemetria wyświetlania strony jest analizowana w usłudze Application Insights i widoczne są jedynie raporty zbiorcze, uśrednione dla wszystkich użytkowników. Jednak na potrzeby debugowania, możesz zapoznać się ze zdarzeniami wyświetlania pojedynczej strony.

W bloku diagnostycznych wyszukiwania hello ustawić filtry tooPage widoku.

![](./media/app-insights-javascript/12-search-pages.png)

Wybierz wszystkie zdarzenia toosee więcej szczegółów. Na stronie szczegółów hello kliknij toosee "..." jeszcze więcej szczegółów.

> [!NOTE]
> Jeśli używasz [wyszukiwania](app-insights-diagnostic-search.md), powiadomienia, że masz toomatch całe wyrazy: "Formacje o programie" i "informacje" nie odpowiada "Temat".
> 
> 

Można również użyć hello zaawansowanych [języka zapytań usługi Analiza dzienników](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch wyświetleń strony.

### <a name="page-view-properties"></a>Właściwości wyświetlania stron
* **Czas trwania wyświetlania stron** 
  
  * Domyślnie program hello czasu zajmuje tooload hello strony, toofull żądania klienta obciążenia (w tym plików pomocniczych, ale z wyłączeniem zadania asynchroniczne, takie jak wywołania Ajax). 
  * Jeśli ustawisz `overridePageViewDuration` w hello [konfigurację strony](#detailed-configuration), najpierw hello odstęp między tooexecution żądania klienta z hello `trackPageView`. Jeśli trackPageView jest przenoszony z położenia zwykle po zainicjowaniu hello hello skryptu, zostaną one zastosowane inną wartość.
  * Jeśli `overridePageViewDuration` jest ustawiony, a czas trwania argument znajduje się w hello `trackPageView()` wywołań, a następnie zamiast niego jest używana wartość argumentu hello. 

## <a name="custom-page-counts"></a>Niestandardowe liczby stron
Domyślnie liczba stron występuje zawsze, gdy ładuje nowej strony do przeglądarki klienta hello.  Ale może być toocount dodatkowa strona widoków. Na przykład strona może wyświetlać zawartość w kartach i mają toocount strony, gdy użytkownik hello przełącza karty. Lub kodu JavaScript na stronie powitania może załadować nowej zawartości bez zmiany adresu URL hello przeglądarki.

Wstawianie wywołania języka JavaScript takie punkcie odpowiednie hello w kodzie klienta:

    appInsights.trackPageView(myPageName);

Nazwa strony Hello może zawierać hello same znaki jako adres URL, ale cokolwiek po "#" lub "?" zostanie zignorowany.

## <a name="usage-tracking"></a>Śledzenie użycia
Chcesz toofind limit użytkowników czy z aplikacją?

* [Informacje na temat śledzenia użycia](app-insights-web-track-usage.md)
* [Informacje o interfejsie API do monitorowania niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Wideo


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Następne kroki
* [Śledzenie użycia](app-insights-web-track-usage.md)
* [Niestandardowe zdarzenia i metryki](app-insights-api-custom-events-metrics.md)
* [Tworzenie — pomiar— nauka](app-insights-web-track-usage.md)

