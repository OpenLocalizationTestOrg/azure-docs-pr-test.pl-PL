---
title: "Usługa Azure Application Insights dla aplikacji sieci Web w języku JavaScript | Microsoft Docs"
description: "Pobieranie liczników wyświetleń stron i sesji, danych klienta sieci Web oraz śledzenie wzorców użycia. Wykrywanie wyjątków i problemów z wydajnością na stronach sieci Web w języku JavaScript."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: mbullwin
ms.openlocfilehash: 7cc061b921109f173837352199ff64f055ae2483
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2017
---
# <a name="application-insights-for-web-pages"></a>Usługa Application Insights dla stron sieci Web
Poznaj wydajność i użycie strony sieci Web lub aplikacji. Jeśli dodasz usługę [Application Insights](app-insights-overview.md) do skryptu strony, uzyskasz chronometraż ładowania strony i wywołań AJAX, liczniki i szczegóły dotyczące wyjątków przeglądarki i błędów AJAX, a także liczniki użytkowników i sesji. Wszystkie te dane możesz rozdzielić według strony, systemu operacyjnego klienta i wersji przeglądarki, lokalizacji geograficznej i innych wymiarów. Możesz ustawić alerty związane z liczbami błędów lub powolnym ładowaniem strony. A wstawiając wywołania śledzenia w kodzie JavaScript, możesz śledzić sposób użycia różnych funkcji aplikacji strony sieci Web.

Usługi Application Insights można używać z dowolnymi stronami sieci Web — wystarczy dodać krótki fragment kodu JavaScript. Jeśli Twoja usługa sieci Web jest zaprogramowana w technologii [Java](app-insights-java-get-started.md) lub [ASP.NET](app-insights-asp-net.md), możesz zintegrować telemetrię pochodzącą z serwera i klientów.

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij pozycję Przeglądarka](./media/app-insights-javascript/03.png)

Potrzebna jest subskrypcja platformy [Microsoft Azure](https://azure.com). Jeśli zespół ma subskrypcję organizacyjną, poproś właściciela, aby dodał do niej Twoje konto Microsoft. Tworząc strony i używając ich na małą skalę, nie poniesiesz żadnych kosztów.

## <a name="set-up-application-insights-for-your-web-page"></a>Konfigurowanie usługi Application Insights dla strony sieci Web
Dodaj fragment kodu modułu ładującego do stron sieci Web w opisany poniżej sposób.

### <a name="open-or-create-application-insights-resource"></a>Otwieranie lub tworzenie zasobu usługi Application Insights
Zasób usługi Application Insights jest miejscem, w którym będą wyświetlane dane dotyczące wydajności i użycia strony. 

Zaloguj się do [portalu Azure](https://portal.azure.com).

Jeśli skonfigurowano już monitorowanie po stronie serwera aplikacji, zasób jest już utworzony:

![Wybierz kolejno opcje Przeglądaj, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-find.png)

Jeśli nie ma zasobu, utwórz go:

![Wybierz kolejno opcje Nowe, Usługi dla deweloperów, Application Insights.](./media/app-insights-javascript/01-create.png)

*Już masz pytania?* [Więcej informacji na temat tworzenia zasobu](app-insights-create-new-resource.md).

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a>Dodawanie skryptu zestawu SDK do aplikacji lub stron sieci Web
Ze strony Szybki start pobierz skrypt dla stron sieci Web:

![W bloku przeglądu aplikacji wybierz kolejno opcje Szybki start, Pobierz kod umożliwiający monitorowanie stron sieci Web. Skopiuj skrypt.](./media/app-insights-javascript/02-monitor-web-page.png)

Wstaw skrypt tuż przed tagiem `</head>` na każdej stronie, którą chcesz śledzić. Jeśli witryna ma stronę wzorcową, możesz umieścić skrypt na tej stronie. Na przykład:

* W projekcie ASP.NET MVC możesz umieścić go w pliku `View\Shared\_Layout.cshtml`
* W przypadku witryny programu SharePoint w panelu sterowania otwórz plik [Ustawienia witryny / Strona wzorcowa](app-insights-sharepoint.md).

Skrypt zawiera klucz instrumentacji, który kieruje dane do odpowiedniego zasobu usługi Application Insights. 

([Dokładniejsze objaśnienia dotyczące skryptu](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/)).

*(Jeśli używasz dobrze znanej struktury stron sieci Web, poszukaj adapterów usługi Application Insights. Takim adapterem jest na przykład [moduł AngularJS](http://ngmodules.org/modules/angular-appinsights)).*

## <a name="detailed-configuration"></a>Konfiguracja szczegółowa
Istnieje kilka [parametrów](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), które można ustawić, chociaż w większości przypadków nie jest to potrzebne. Na przykład można wyłączyć zgłaszanie wywołań Ajax lub ograniczyć liczbę tych wywołań zgłaszanych na wyświetlenie strony (w celu zmniejszenia ruchu). Można także ustawić tryb debugowania, aby dane telemetrii były szybciej przesyłane przez potok, a nie przekazywane w trybie wsadowym.

Aby ustawić te parametry, poszukaj tego wiersza we fragmencie kodu i dodaj po nim więcej elementów rozdzielonych przecinkami:

    })({
      instrumentationKey: "..."
      // Insert here
    });

[Dostępne parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) obejmują:

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Uruchamianie aplikacji
Uruchom aplikację sieci Web, używaj jej przez pewien czas, aby wygenerować dane telemetryczne, i odczekaj kilka sekund. Aplikację możesz uruchomić za pomocą klawisza **F5** na maszynie deweloperskiej lub opublikować ją i pozwolić na korzystanie z niej przez użytkowników.

Jeśli chcesz sprawdzić telemetrię, którą aplikacja sieci Web wysyła do usługi Application Insights, użyj narzędzi debugowania w przeglądarce (**F12** w wielu przeglądarkach). Dane są przesyłane do witryny dc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Eksplorowanie danych wydajności przeglądarki
Otwórz blok Przeglądarka, aby wyświetlić agregowane dane wydajności z przeglądarek użytkowników.

![W witrynie portal.azure.com otwórz zasób swojej aplikacji, a następnie kliknij kolejno opcje Ustawienia, Przeglądarki](./media/app-insights-javascript/03.png)

*Jeszcze nie ma danych? Kliknij przycisk **Odśwież** w górnej części strony. Nadal nic? Zobacz [Rozwiązywanie problemów ](app-insights-troubleshoot-faq.md).*

Blok Przeglądarka jest [blokiem Eksploratora metryk](app-insights-metrics-explorer.md) z wstępnie ustawionymi filtrami i wybranymi wykresami. Jeśli chcesz, możesz edytować przedział czasu, filtry i konfiguracje wykresów, a następnie zapisać wynik jako ulubiony. Kliknij przycisk **Przywróć domyślne**, aby wrócić do oryginalnej konfiguracji bloku.

## <a name="page-load-performance"></a>Wydajność ładowania strony
U góry znajduje się segmentowany wykres czasów ładowania strony. Całkowita wysokość wykresu reprezentuje średni czas ładowania oraz wyświetlania stron z aplikacji w przeglądarkach użytkowników. Czas jest mierzony od momentu wysłania z przeglądarki początkowego żądania HTTP do momentu przetworzenia wszystkich synchronicznych zdarzeń ładowania, wraz z układem i uruchamianiem skryptów. Nie obejmuje zadań asynchronicznych, takich jak ładowanie składników Web Part z wywołań AJAX.

Na wykresie całkowity czas ładowania strony jest podzielony na segmenty obejmujące [standardowe chronometraże zdefiniowane przez organizację W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Zauważ, że czas *nawiązywania połączenia sieciowego* często jest krótszy niż spodziewany, ponieważ jest średnią dla wszystkich żądań z przeglądarki do serwera. Wiele indywidualnych żądań ma czas nawiązywania połączenia równy 0, ponieważ połączenie z serwerem jest już aktywne.

### <a name="slow-loading"></a>Powolne ładowanie?
Powolne ładowanie stron jest głównym powodem niezadowolenia użytkowników. Jeśli wykres wskazuje powolne ładowanie stron, łatwo można wykonać badania diagnostyczne.

Wykres ten przedstawia średnią dla wszystkich operacji ładowania stron w aplikacji. Aby sprawdzić, czy problem jest ograniczony do konkretnych stron, spójrz dalej na dół bloku, gdzie znajduje się siatka posegmentowana według adresów URL stron:

![](./media/app-insights-javascript/09-page-perf.png)

Zwróć uwagę na liczbę wyświetleń stron i odchylenie standardowe. Jeśli liczba wyświetleń stron jest bardzo niska, problem nie ma znacznego wpływu na użytkowników. Wysokie odchylenie standardowe (porównywalne do samej średniej) wskazuje na znaczne różnice między poszczególnymi pomiarami.

**Wyświetl szczegóły dla jednego adresu URL i jednej strony.** Kliknij nazwę dowolnej strony, aby zobaczyć blok wykresów dotyczących przeglądarki filtrowanych według tego adresu URL, a następnie kliknij wystąpienie wyświetlenia strony.

![](./media/app-insights-javascript/35.png)

Kliknij przycisk `...`, aby uzyskać pełną listę właściwości tego zdarzenia, lub zbadaj wywołania Ajax i powiązane z nimi zdarzenia. Powolne wywołania Ajax, jeśli są synchroniczne, wpływają na ogólny czas ładowania strony. Powiązane zdarzenia obejmują żądania serwera dotyczące tego samego adresu URL (jeśli skonfigurowano usługę Application Insights na serwerze sieci Web).

**Wydajność stron w czasie.** Wróć do bloku Przeglądarki i zmień siatkę Wyświetlenie strony — czas ładowania na wykres liniowy, aby zobaczyć, czy wystąpiły wartości szczytowe w określonym czasie:

![Kliknij nagłówek siatki i wybierz nowy typ wykresu](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentowanie według innych wymiarów.** Może strony są ładowane wolniej w konkretnej przeglądarce, systemie operacyjnym klienta lub lokalizacji użytkownika? Dodaj nowy wykres i poeksperymentuj z operacją **Grupuj według** wymiaru.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Wydajność wywołań AJAX
Upewnij się. że dowolne wywołania AJAX na stronach sieci Web działają poprawnie. Często są one używane do asynchronicznego wypełniania elementów na stronie. Chociaż cała strona może ładować się szybko, użytkownicy mogą być sfrustrowani, jeśli muszą wpatrywać się w puste składniki Web Part w oczekiwaniu na wyświetlenie w nich danych.

Wywołania AJAX ze strony sieci Web są wyświetlane w bloku Przeglądarki jako zależności.

W górnej części bloku znajdują się wykresy podsumowujące:

![](./media/app-insights-javascript/31.png)

a poniżej szczegółowe siatki:

![](./media/app-insights-javascript/33.png)

Klikaj poszczególne wiersze, aby uzyskać szczegółowe informacje.

> [!NOTE]
> Jeśli usuniesz filtr Przeglądarki w bloku, zarówno serwer, jak i zależności AJAX zostaną uwzględnione na tych wykresach. Kliknij przycisk Przywróć domyślne, aby ponownie skonfigurować filtr.
> 
> 

**Aby przejść do szczegółów niepowodzeń wywołań Ajax** przewiń w dół do siatki błędów zależności, a następnie kliknij wiersz, aby wyświetlić określone wystąpienia.

![](./media/app-insights-javascript/37.png)


Kliknij przycisk `...`, aby uzyskać pełną telemetrię wywołania Ajax.

### <a name="no-ajax-calls-reported"></a>Brak zgłoszonych wywołań Ajax?
Wywołania AJAX obejmują dowolne wywołania HTTP/HTTPS dokonywane ze skryptu na stronie sieci Web. Jeśli nie widzisz ich w raporcie, sprawdź, czy we fragmencie kodu nie zostały ustawione [parametry](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` lub `maxAjaxCallsPerView`.

## <a name="browser-exceptions"></a>Wyjątki przeglądarki
W bloku Przeglądarki znajduje się wykres podsumowania wyjątków, a poniżej niego siatka typów wyjątków.

![](./media/app-insights-javascript/39.png)

Jeśli nie widzisz wyjątków przeglądarki w raporcie, sprawdź, czy we fragmencie kodu nie został ustawiony [parametr](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.

## <a name="inspect-individual-page-view-events"></a>Badanie zdarzeń wyświetlania pojedynczej strony

Zazwyczaj telemetria wyświetlania strony jest analizowana w usłudze Application Insights i widoczne są jedynie raporty zbiorcze, uśrednione dla wszystkich użytkowników. Jednak na potrzeby debugowania, możesz zapoznać się ze zdarzeniami wyświetlania pojedynczej strony.

W bloku Wyszukiwanie diagnostyczne jako Filtry ustaw Wyświetlenie strony.

![](./media/app-insights-javascript/12-search-pages.png)

Wybierz dowolne zdarzenie, aby wyświetlić więcej szczegółów. Na stronie szczegółów kliknij przycisk „...”, aby wyświetlić jeszcze więcej szczegółów.

> [!NOTE]
> Jeśli używasz pola [Wyszukiwanie](app-insights-diagnostic-search.md), zauważ, że musisz dopasowywać całe wyrazy: wpisy „Abou” i „bout” nie odpowiadają słowu „About”.
> 
> 

Można także użyć zaawansowanego [języka zapytań usługi Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) do przeszukiwania wyświetleń stron.

### <a name="page-view-properties"></a>Właściwości wyświetlania stron
* **Czas trwania wyświetlania stron** 
  
  * Domyślnie czas potrzebny do załadowania strony, od żądania klienta do pełnego załadowania (w tym plików pomocniczych, ale z wyłączeniem zadań asynchronicznych, takich jak wywołania Ajax). 
  * Jeśli ustawisz parametr `overridePageViewDuration` w [konfiguracji strony](#detailed-configuration), czas ten jest liczony od żądania klienta do wykonania pierwszego wywołania `trackPageView`. W przypadku przeniesienia wywołania trackPageView ze zwykłej pozycji po zainicjowaniu skryptu ta wartość będzie inna.
  * Jeśli parametr `overridePageViewDuration` jest ustawiony, a argument czasu trwania jest podany w wywołaniu `trackPageView()`, zastępczo zostanie użyta wartość argumentu. 

## <a name="custom-page-counts"></a>Niestandardowe liczby stron
Domyślnie strony są zliczane przy każdym załadowaniu nowej strony do przeglądarki klienta.  Jednak warto zliczać dodatkowe wyświetlenia stron. Na przykład zawartość strony może być wyświetlana na kartach i warto zliczać strony, gdy użytkownik zmienia karty. Ponadto kod JavaScript na stronie może ładować nową zawartość bez zmiany adresu URL w przeglądarce.

Wstaw takie wywołanie JavaScript we właściwym miejscu w kodzie klienta:

    appInsights.trackPageView(myPageName);

Nazwa strony może zawierać te same znaki co adres URL, ale wszystko po znakach „#” i „?” będzie ignorowane.

## <a name="usage-tracking"></a>Śledzenie użycia
Chcesz dowiedzieć się, w jaki sposób użytkownicy korzystają z aplikacji?

* [Informacje na temat śledzenia użycia](app-insights-web-track-usage.md)
* [Informacje o interfejsie API do monitorowania niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Wideo


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Następne kroki
* [Śledzenie użycia](app-insights-web-track-usage.md)
* [Niestandardowe zdarzenia i metryki](app-insights-api-custom-events-metrics.md)
* [Tworzenie — pomiar— nauka](app-insights-web-track-usage.md)

