---
title: "Monitorowanie kondycji i użycia za pomocą usługi Application Insights aplikacji"
description: "Wprowadzenie do usługi Application Insights. Analizowanie użycia, dostępności i wydajności lokalnej lub w aplikacji Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a>Monitorowanie wydajności w aplikacjach sieci Web


Upewnij się, że aplikacja działa optymalnie i Dowiedz się szybko o zakończą się niepowodzeniem. [Usługa Application Insights] [ start] informujące o wszelkich problemów z wydajnością oraz wyjątków i ułatwiają znajdowanie i diagnozowanie głównej przyczyny.

Usługa Application Insights można monitorować aplikacji sieci web zarówno Java, jak i platformy ASP.NET i usługi, usługi WCF. Mogą to być obsługiwana lokalnie, w przypadku maszyn wirtualnych lub jako witryny sieci Web Microsoft Azure. 

Po stronie klienta usługi Application Insights może zająć telemetrii ze stron sieci web i różnych urządzeniami, takimi jak systemy iOS, Android i aplikacji ze Sklepu Windows.

>[!Note]
> Wprowadzono nowe środowisko dostępne do znajdowania powolne wykonywania stron w aplikacji sieci web. Jeśli nie masz do niego dostęp, ją włączyć, konfigurując opcje podglądu z [bloku Podgląd](app-insights-previews.md). Przeczytaj informacje o nowe środowisko w [Znajdowanie i rozwiązywanie problemów wąskich gardeł wydajności interakcyjne postępowaniu wydajności](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Konfigurowanie monitorowania wydajności
Jeśli nie zostały jeszcze dodane usługi Application Insights do projektu (Jeśli nie ma ApplicationInsights.config), wybierz jedną z tych sposobów na rozpoczęcie pracy:

* [Aplikacje sieci web ASP.NET](app-insights-asp-net.md)
  * [Dodaj monitorowanie wyjątków](app-insights-asp-net-exceptions.md)
  * [Dodaj monitorowanie zależności](app-insights-monitor-performance-live-website-now.md)
* [Aplikacje sieci web J2EE](app-insights-java-get-started.md)
  * [Dodaj monitorowanie zależności](app-insights-java-agent.md)

## <a name="view"></a>Eksploracja metryki wydajności
W [portalu Azure](https://portal.azure.com), przejdź do zasobu usługi Application Insights, skonfigurowanego dla aplikacji. Blok omówienie przedstawia dane wydajności podstawowe:

Kliknij przycisk dowolnego wykresu, aby zobaczyć więcej szczegółów, a także aby zobaczyć wyniki przez dłuższy czas. Na przykład kliknij Kafelek żądania, a następnie wybierz zakres czasu:

![Kliknij, aby większej ilości danych, a następnie wybierz zakres czasu](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Kliknij wykres, aby wybrać metryki, które wyświetla, lub Dodaj nowy wykres i wybrać jego metryki:

![Kliknij wykres, aby wybrać metryki](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Usuń zaznaczenie pola wyboru wszystkie metryki** oglądanie pełnej zaznaczenia, która jest dostępna. Metryki należą do grup; Po wybraniu dowolnego członka grupy są wyświetlane tylko innych członków tej grupy.

## <a name="metrics"></a>Jaki jest średnią wszystkich? Kafelki wydajności i raporty
Istnieją różne metryki wydajności, które można pobrać. Zacznijmy od tych, które są wyświetlane domyślnie w bloku aplikacji.

### <a name="requests"></a>Żądania
Liczba żądań HTTP odebrane w określonym przedziale czasu. Porównaj te wyniki na inne raporty, aby wyświetlić zachowania aplikacji jako obciążenia zmienia się.

Żądania HTTP obejmują wszystkie żądania GET lub POST dla stron, danych i obrazów.

Kliknij Kafelek, aby uzyskać liczby dla określonych adresów URL.

### <a name="average-response-time"></a>Średni czas odpowiedzi
Mierzy czas między żądania sieci web wprowadzania aplikacji i odpowiedzi zostały zwrócone.

Punkty Pokaż, ruchomą średnią. Jeśli istnieje wiele żądań, mogą wystąpić, które odbiegają od średniej bez widocznych szczytu lub zanurzyć na wykresie.

Poszukaj nietypowe szczytów. Ogólnie rzecz biorąc oczekiwany czas odpowiedzi wzrasta z wzrost żądania. W przypadku nieproporcjonalnie wzrostu aplikacji może być naciśnięcie limit zasobów, takie jak Procesor lub pojemność usługi, które są używane.

Kliknij Kafelek, aby pobrać razy dla określonych adresów URL.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Najwolniejsze żądań
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Pokazuje, które żądania może być konieczne dostrojenie wydajności.

### <a name="failed-requests"></a>Żądań zakończonych niepowodzeniem
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Liczba żądań, które zwrócił nieprzechwyconych wyjątków.

Kliknij Kafelek, aby wyświetlić szczegóły określonych niepowodzeń, a następnie wybierz indywidualne żądanie, aby wyświetlić jego szczegóły. 

Tylko reprezentatywnej próbki błędów jest przechowywany dla poszczególnych kontroli.

### <a name="other-metrics"></a>Innych metryk
Aby zobaczyć, ustaw innych metryk można wyświetlać, kliknij wykres i usuń zaznaczenie opcji wszystkie metryki, aby wyświetlić dostępne pełnej. Kliknij (i), aby zobaczyć wszystkie metryki definicji.

![Odznacz wszystkie metryki, aby zobaczyć cały zestaw](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Wybranie dowolnego Metryka wyłącza innych, które nie mogą występować w tym samym wykresie.

## <a name="set-alerts"></a>Ustawianie alertów
Aby otrzymywać powiadomienia pocztą e-mail o nietypowych wartościach dowolnej metryki, należy dodać alert. Można wybrać do wysyłania wiadomości e-mail do administratorów, kont lub na adresy e-mail określone.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Ustaw zasób przed inne właściwości. Nie należy wybierać zasoby w teście sieci Web, aby ustawić alertów dla metryki wydajności i użycia.

Należy zachować ostrożność, należy pamiętać, jednostki, w których użytkownik jest proszony o wprowadź wartość progu.

*Przycisk Dodaj alertu nie jest widoczny.* -To jest grupa kont, do których masz dostęp tylko do odczytu? Skontaktuj się z administratorem konta.

## <a name="diagnosis"></a>Diagnozowanie problemów
Poniżej przedstawiono kilka wskazówek do znajdowania i diagnozowanie problemów z wydajnością:

* Konfigurowanie [testów sieci web] [ availability] alertów, jeśli witryna sieci web ulegnie awarii lub odpowiada nieprawidłowo lub powoli. 
* Porównuje liczbę żądań z innych metryk w celu sprawdzenia, czy błędy lub powolna odpowiedź dotyczą obciążenia.
* [Wstaw i wyszukiwania instrukcji śledzenia] [ diagnostic] w kodzie, aby ułatwić identyfikowanie problemów.
* Monitorowanie aplikacji sieci Web w operację, podając [strumień na żywo metryki][livestream].
* Przechwyć stan z aplikacji .net [debugera migawki][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Znajdź i napraw wąskich gardeł wydajności z dochodzenia interakcyjne wydajności

Nowym postępowaniem interakcyjne wydajności usługi Application Insights umożliwia zlokalizować obszary aplikacji sieci Web, które są spowolnieniem ogólną wydajność. Można szybko znaleźć określonych stron, które są spowolnieniem i użyj [narzędzia profilowania](app-insights-profiler.md) czy jest korelacja te strony.

### <a name="create-a-list-of-slow-performing-pages"></a>Utwórz listę powolne wykonywania strony 

Pierwszym krokiem do znajdowania problemy z wydajnością jest w celu uzyskania listy powolne odpowiada strony. Zrzut poniżej ekranu pokazuje, używając bloku wydajności, aby uzyskać listę potencjalnych strony, aby zbadać dokładnie. Możliwe jest szybkie wyświetlenie na tej stronie czy wystąpił spowolnienia czas odpowiedzi aplikacji na około 6:00 PM i ponownie na około 10 PM. Można również sprawdzić, czy operacja szczegóły klienta/GET miał niektórych długotrwałe operacje z czasem odpowiedzi środkowej 507.05 milisekund. 

![Wydajność interakcyjne Insights aplikacji](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Przechodzenie do określonych stron

Po utworzeniu migawki wydajności aplikacji, więcej informacji można uzyskać na określonych powolna wykonywania operacji. Polecenie żadnej operacji na liście, aby wyświetlić szczegóły, jak pokazano poniżej. Z wykresu jest widoczny czy wydajność oparto na zależność. Można również sprawdzić, ilu użytkowników działa w różnym czasie odpowiedzi. 

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Przechodzenie w określonym przedziale czasu

Po zidentyfikowaniu punktu w czasie, aby zbadać, przejść do szczegółów nawet w przypadku znajduje się w określonej operacji, które mogły spowodować spowolnienia wydajności. Po kliknięciu określonego punktu w czasie otrzymasz szczegóły strony, jak pokazano poniżej. W poniższym przykładzie widoczny operacje wymienione w danym okresie oraz kody odpowiedzi serwera i czas trwania operacji. Masz również adres url do otwarcia elementu roboczego TFS, aby wysyłać tych informacji do zespołu deweloperów.

![Przedział czasu Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Przechodzenie do określonej operacji

Po zidentyfikowaniu punktu w czasie, aby zbadać, przejść do szczegółów nawet w przypadku znajduje się w określonej operacji, które mogły spowodować spowolnienia wydajności. Polecenie operacji z listy, aby wyświetlić szczegóły operacji, jak pokazano poniżej. W tym przykładzie widać, operacja nie powiodła się, czy usługa Application Insights udostępnił szczegóły aplikacja zgłosiła wyjątek. Ponownie można łatwo utworzyć elementu roboczego TFS z poziomu tego bloku.

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Następne kroki
[Testów sieci Web] [ availability] -żądania sieci web wysyłanych do aplikacji w regularnych odstępach czasu w całym świecie.

[Przechwytywanie i wyszukiwać dane śledzenia diagnostycznego] [ diagnostic] — Wstaw śledzenie wywołań i zapoznawanie wyników, aby zidentyfikować problemy.

[Śledzenie użycia] [ usage] -dowiedzieć się, jak użytkownicy korzystają z aplikacji.

[Rozwiązywanie problemów z] [ qna] -Q & A i



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



