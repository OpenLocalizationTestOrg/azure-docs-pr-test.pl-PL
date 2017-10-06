---
title: "aaaMonitor aplikacji kondycji i użycia za pomocą usługi Application Insights"
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
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Monitorowanie wydajności w aplikacjach sieci Web


Upewnij się, że aplikacja działa optymalnie i Dowiedz się szybko o zakończą się niepowodzeniem. [Usługa Application Insights] [ start] informujące o wszelkich problemów z wydajnością oraz wyjątków i pomocy Znajdź i diagnozowanie hello główne przyczyny.

Usługa Application Insights można monitorować aplikacji sieci web zarówno Java, jak i platformy ASP.NET i usługi, usługi WCF. Mogą to być obsługiwana lokalnie, w przypadku maszyn wirtualnych lub jako witryny sieci Web Microsoft Azure. 

Po stronie klienta hello usługi Application Insights może zająć telemetrii ze stron sieci web i różnych urządzeniami, takimi jak systemy iOS, Android i aplikacji ze Sklepu Windows.

>[!Note]
> Wprowadzono nowe środowisko dostępne do znajdowania powolne wykonywania stron w aplikacji sieci web. Jeśli nie masz dostępu tooit ją włączyć, konfigurując opcje podglądu z hello [bloku Podgląd](app-insights-previews.md). Przeczytaj informacje o nowe środowisko w [Znajdowanie i rozwiązywanie problemów wąskich gardeł wydajności hello interakcyjne wydajności postępowaniu](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Konfigurowanie monitorowania wydajności
Jeśli jeszcze nie dodano tooyour usługi Application Insights projektu (Jeśli nie ma ApplicationInsights.config), wybierz jedną z następujących sposobów tooget uruchomiona:

* [Aplikacje sieci web ASP.NET](app-insights-asp-net.md)
  * [Dodaj monitorowanie wyjątków](app-insights-asp-net-exceptions.md)
  * [Dodaj monitorowanie zależności](app-insights-monitor-performance-live-website-now.md)
* [Aplikacje sieci web J2EE](app-insights-java-get-started.md)
  * [Dodaj monitorowanie zależności](app-insights-java-agent.md)

## <a name="view"></a>Eksploracja metryki wydajności
W [hello portalu Azure](https://portal.azure.com), przejdź do zasobu usługi Application Insights toohello skonfigurowanego dla aplikacji. bloku omówienie Hello przedstawia dane wydajności podstawowe:

Kliknij opcję żadnych toosee wykresu więcej szczegółów, a wyniki toosee przez dłuższy czas. Na przykład kliknij Kafelek żądania hello, a następnie wybierz zakres czasu:

![Kliknij za pośrednictwem toomore danych i wybierz zakres czasu](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Kliknij toochoose wykresu metryk, które wyświetla, lub Dodaj nowy wykres i wybrać jego metryki:

![Kliknij przycisk metryki toochoose wykresu](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Usuń zaznaczenie pola wyboru wszystkie metryki hello** toosee hello pełne zaznaczenia, która jest dostępna. metryki Hello należą do grup; Po wybraniu dowolnego członka grupy hello innych członków tej grupy są wyświetlane tylko.

## <a name="metrics"></a>Jaki jest średnią wszystkich? Kafelki wydajności i raporty
Istnieją różne metryki wydajności, które można pobrać. Zacznijmy od tych, które są wyświetlane domyślnie w bloku aplikacji hello.

### <a name="requests"></a>Żądania
Liczba Hello żądania HTTP odebrane w określonym przedziale czasu. To porównać z wynikami hello na inne toosee raporty zachowania aplikacji jako hello obciążenia.

Żądania HTTP obejmują wszystkie żądania GET lub POST dla stron, danych i obrazów.

Polecenie hello kafelka tooget liczniki dla określonych adresów URL.

### <a name="average-response-time"></a>Średni czas odpowiedzi
Środki hello czas między wprowadzania aplikacji i hello odpowiedź zwracana żądania sieci web.

punkty Hello pokazują, ruchomą średnią. Jeśli istnieje wiele żądań, mogą wystąpić, które odbiegają od średniej hello bez widocznych szczytu lub zanurzyć hello wykresie.

Poszukaj nietypowe szczytów. Ogólnie rzecz biorąc można spodziewać się toorise czasu odpowiedzi z wzrost żądania. W przypadku nieproporcjonalnie powstanie hello aplikacji może być naciśnięcie limit zasobów, takie jak procesor CPU lub hello pojemność usługi, które są używane.

Kliknij przycisk hello kafelka tooget razy dla określonych adresów URL.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Najwolniejsze żądań
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Pokazuje, które żądania może być konieczne dostrojenie wydajności.

### <a name="failed-requests"></a>Żądań zakończonych niepowodzeniem
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Liczba żądań, które zwrócił nieprzechwyconych wyjątków.

Kliknij hello kafelka toosee hello szczegółów określonych niepowodzeń i wybierz toosee oddzielne żądanie jego szczegóły. 

Tylko reprezentatywnej próbki błędów jest przechowywany dla poszczególnych kontroli.

### <a name="other-metrics"></a>Innych metryk
toosee jakie inne metryki, można wyświetlać, kliknij wykres i usuń zaznaczenie wszystkich hello metryki toosee hello pełnej dostępnych zestawów. Kliknij przycisk (i) toosee definicji wszystkie metryki.

![Odznacz wszystkie metryki toosee hello całego zestawu](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Wybranie dowolnego hello wyłącza metryki innych osób, które nie mogą występować w hello tego samego wykresu.

## <a name="set-alerts"></a>Ustawianie alertów
powiadomienie e-mail o nietypowych wartościach dowolnej metryki toobe dodać alert. Można wybrać toosend hello e-mail toohello konta administratorów lub toospecific adresy e-mail.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Ustaw zasób hello przed hello inne właściwości. Nie wybierz hello webtest zasoby, jeśli chcesz otrzymywać alerty tooset na wydajność lub metryki użycia.

Być dokładne toonote hello jednostki, w których użytkownik jest proszony wartość progowa hello tooenter.

*Nie widzę Alert przycisku Dodaj hello.* — To toowhich konta grupy mają dostęp tylko do odczytu? Skontaktuj się z administratorem konta hello.

## <a name="diagnosis"></a>Diagnozowanie problemów
Poniżej przedstawiono kilka wskazówek do znajdowania i diagnozowanie problemów z wydajnością:

* Konfigurowanie [testów sieci web] [ availability] toobe alert, jeśli witryna sieci web ulegnie awarii lub odpowiada nieprawidłowo lub powoli. 
* Porównaj hello liczbę żądań z innych metryk toosee w przypadku awarii lub powolna odpowiedź tooload pokrewne.
* [Wstaw i wyszukiwania instrukcji śledzenia] [ diagnostic] w toohelp Twojego kodu identyfikowanie problemów.
* Monitorowanie aplikacji sieci Web w operację, podając [strumień na żywo metryki][livestream].
* Przechwyć stan hello aplikacji .net z [debugera migawki][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Znajdź i napraw wąskich gardeł wydajności z dochodzenia interakcyjne wydajności

Możesz użyć hello nowej usługi Application Insights interakcyjne wydajności dochodzenia toolocate obszary aplikacji sieci Web są spowolnieniem ogólną wydajność. Można szybko znaleźć określonych stron, które są spowolnieniem i użyj hello [narzędzia profilowania](app-insights-profiler.md) toosee, jeśli występuje korelacja te strony.

### <a name="create-a-list-of-slow-performing-pages"></a>Utwórz listę powolne wykonywania strony 

pierwszym krokiem Hello znajdowanie problemów z wydajnością jest tooget listę hello wolno odpowiadać stron. ekranie powitania zrzut poniżej przedstawiono przy użyciu hello wydajności bloku tooget listę potencjalnych tooinvestigate więcej stron. Możliwe jest szybkie wyświetlenie na tej stronie czy wystąpił spowolnienia hello czas odpowiedzi aplikacji hello na około 6:00 PM i ponownie na około 10 PM. Można również sprawdzić, czy operacja szczegóły klienta/GET hello miał niektóre długotrwałe operacje z czasem odpowiedzi środkowej 507.05 milisekund. 

![Wydajność interakcyjne Insights aplikacji](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Przechodzenie do określonych stron

Po utworzeniu migawki wydajności aplikacji, więcej informacji można uzyskać na określonych powolna wykonywania operacji. Polecenie żadnej operacji w hello listy toosee hello uzyskać szczegółowe informacje, jak pokazano poniżej. Z wykresu hello widać, jeśli wydajność hello oparto na zależność. Możesz również sprawdzić ile hello doświadczeni użytkownicy różnych czas odpowiedzi. 

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Przechodzenie w określonym przedziale czasu

Po zidentyfikowaniu punktu w czasie tooinvestigate przechodzenie nawet dalsze toolook na powitania określonych operacji, które mogły spowodować hello spowolnienia wydajności. Po kliknięciu określonego punktu w czasie otrzymasz szczegóły hello hello strony, jak pokazano poniżej. Hello przykład poniżej przedstawiono operacje hello wymienionych w danym okresie oraz kody odpowiedzi serwera hello i czasu trwania operacji hello. Masz również hello adres url do otwarcia elementu roboczego TFS, jeśli potrzebujesz toosend zespół deweloperów tooyour tej informacji.

![Przedział czasu Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Przechodzenie do określonej operacji

Po zidentyfikowaniu punktu w czasie tooinvestigate przechodzenie nawet dalsze toolook na powitania określonych operacji, które mogły spowodować hello spowolnienia wydajności. Kliknij działanie od hello listy toosee hello szczegóły operacji hello, jak pokazano poniżej. W tym przykładzie widocznej hello operacja nie powiodła się, czy usługi Application Insights udostępnił hello szczegóły hello zgłosiła wyjątek aplikacji hello. Ponownie można łatwo utworzyć elementu roboczego TFS z poziomu tego bloku.

![Application Insights operacji bloku](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Następne kroki
[Testów sieci Web] [ availability] -żądań sieci web wysłali tooyour aplikacji w regularnych odstępach czasu z wokół hello world.

[Przechwytywanie i wyszukiwać dane śledzenia diagnostycznego] [ diagnostic] — Wstaw śledzenie wywołań i zapoznawanie hello wyniki toopinpoint problemów.

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



