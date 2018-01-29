---
title: "Co to jest usługa Azure Application Insights? | Microsoft Docs"
description: "Zarządzanie wydajnością aplikacji i śledzenie użycia działającej aplikacji sieci Web.  Wykrywanie, klasyfikacja i diagnozowanie problemów, rozumienie, jak użytkownicy używają Twojej aplikacji."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: overview
ms.custom: mvc
ms.date: 05/14/2017
ms.author: mbullwin
ms.openlocfilehash: 2e2a9e8491ad56bcbc42be64729715016f7ed17b
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
# <a name="what-is-application-insights"></a>Co to jest usługa Application Insights?
Usługa Application Insights jest rozszerzalną usługą zarządzania wydajnością aplikacji (APM) dla deweloperów sieci Web na wielu platformach. Użyj tej usługi do monitorowania aplikacji sieci Web na żywo. Usługa automatycznie wykryje nieprawidłowości w zakresie wydajności. Obejmuje ona zaawansowane narzędzia analityczne, dzięki którym możesz diagnozować problemy i zrozumieć sposób korzystania z aplikacji przez użytkowników.  Usługa ta pomaga w ciągłym doskonaleniu wydajności i użyteczności tworzonych rozwiązań. Działa w przypadku aplikacji na różnych platformach, w tym .NET, Node.js i J2EE, hostowanych lokalnie lub w chmurze. Integruje się ona z procesem DevOps i ma punkty połączenia z szeroką gamą narzędzi programistycznych. Może monitorować i analizować dane telemetryczne z aplikacji mobilnych dzięki integracji z usługą Visual Studio App Center i platformą HockeyApp.

![Udostępnia wykresy statystyki działań użytkownika lub przejście do szczegółów określonych zdarzeń.](./media/app-insights-overview/00-sample.png)

[Obejrzyj animację wprowadzającą](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>Jak działa usługa Application Insights?
Zainstaluj mały pakiet instrumentacji w swojej aplikacji i skonfiguruj zasób usługi Application Insights w witrynie Microsoft Azure Portal. Instrumentacja monitoruje Twoją aplikację i wysyła dane telemetryczne do portalu. (Aplikację można uruchomić gdziekolwiek — nie musi być ona hostowana na platformie Azure).

Instrumentacja może obejmować nie tylko aplikację usługi sieci Web, ale również wszystkie składniki tła i skrypty JavaScript na samych stronach sieci Web. 

![Instrumentacja usługi Application Insights w Twojej aplikacji wysyła dane telemetryczne do zasobu usługi Application Insights.](./media/app-insights-overview/01-scheme.png)


Ponadto możesz ściągnąć dane telemetryczne ze środowisk hostów, takich jak liczniki wydajności, diagnostyka platformy Azure lub dzienniki platformy Docker. Możesz też skonfigurować testy sieci Web, które okresowo wysyłają syntetyczne żądania do usługi sieci Web.

Wszystkie te strumienie telemetrii są zintegrowane w witrynie Azure Portal, gdzie możesz zastosować zaawansowane narzędzia do analizy i wyszukiwania do danych pierwotnych.


### <a name="whats-the-overhead"></a>Co to jest narzut?
Wpływ na wydajność Twojej aplikacji jest bardzo mały. Wywołania śledzenia nie powodują blokowania oraz są łączone w partie i wysłane w oddzielnym wątku.

## <a name="what-does-application-insights-monitor"></a>Co monitoruje usługa Application Insights?

Usługa Application Insights jest przeznaczona dla zespołu deweloperów po to, aby pomóc zrozumieć, jak działa Twoja aplikacja i jak jest używana. Monitoruje ona:

* **Liczby żądań, czasy reakcji i współczynniki błędów** — dowiedz się, które strony są najbardziej popularne, o jakiej porze dnia i gdzie są Twoi użytkownicy. Zobacz, które strony działają najlepiej. Jeśli Twoje czasy odpowiedzi i częstotliwości awarii są duże, gdy jest więcej żądań, być może masz problem z zasobami. 
* **Współczynniki zależności, czasy reakcji i współczynniki błędów** — dowiedz się, czy usługi zewnętrzne nie spowalniają pracy.
* **Wyjątki** — analizowanie zagregowanych danych statystycznych lub wybieranie określonych wystąpień i przechodzenie do szczegółów śladu stosu i powiązanych żądań. Są zgłaszane zarówno wyjątki serwera, jak i przeglądarki.
* **Wydajność ładowania i wyświetleń stron** — zgłoszona przez przeglądarki użytkowników.
* **Wywołania AJAX** ze stron sieci Web — liczba, czasy reakcji i współczynniki błędów.
* **Liczby użytkowników i sesji**.
* **Liczniki wydajności** z serwerów systemu Windows lub Linux, takie jak użycie procesora CPU, pamięci i sieci. 
* **Diagnostyka hosta** z platformy Docker lub Azure. 
* **Diagnostyczne dzienniki śledzenia** z Twojej aplikacji — dzięki temu możesz skorelować zdarzenia śledzenia z żądaniami.
* **Niestandardowe zdarzenia i metryki**, które samodzielnie zapisujesz w kodzie klienta lub serwera, do śledzenia zdarzeń biznesowych, takich jak sprzedane towary lub wygrane gry.

## <a name="where-do-i-see-my-telemetry"></a>Gdzie mogę zobaczyć swoją telemetrię?

Istnieje wiele sposobów eksploracji danych. Zapoznaj się z następującymi artykułami:

|  |  |
| --- | --- |
| [**Inteligentne wykrywanie i ręczne alerty**](app-insights-proactive-diagnostics.md)<br/>Alerty automatyczne dostosowują się do normalnych wzorców telemetrii Twojej aplikacji i są wyzwalane, gdy wystąpi coś poza zwykłym wzorcem. Możesz też [ustawić alerty](app-insights-alerts.md) dla konkretnych poziomów metryk niestandardowych lub standardowych. |![Przykładowy alert](./media/app-insights-overview/alerts-tn.png) |
| [**Mapa aplikacji**](app-insights-app-map.md)<br/>Składniki Twojej aplikacji wraz z kluczowymi metrykami i alertami. |![Mapa aplikacji](./media/app-insights-overview/appmap-tn.png)  |
| [**Profiler**](app-insights-profiler.md)<br/>Inspekcja profilów wykonania próbek żądań. |![Profiler](./media/app-insights-overview/profiler.png) |
| [**Analiza użycia**](app-insights-usage-overview.md)<br/>Analiza segmentacji i utrzymywania użytkowników.|![Narzędzie utrzymywania](./media/app-insights-overview/retention.png) |
| [**Wyszukiwanie diagnostyczne danych dla wystąpienia**](app-insights-diagnostic-search.md)<br/>Wyszukiwanie i filtrowanie zdarzeń, takich jak żądania, wyjątki, wywołania zależności, dzienniki śledzenia i wyświetlenia stron.  |![Wyszukiwanie telemetrii](./media/app-insights-overview/search-tn.png) |
| [**Eksplorator metryk dla danych zagregowanych**](app-insights-metrics-explorer.md)<br/>Eksploruj, filtruj i segmentuj zagregowane dane, takie jak liczby żądań, błędów i wyjątków, czasy reakcji, czasy ładowania stron. |![Metryki](./media/app-insights-overview/metrics-tn.png) |
| [**Pulpity nawigacyjne**](app-insights-dashboards.md#dashboards)<br/>Połącz dane z wielu zasobów i udostępnij innym osobom. Opcja ta doskonale nadaje się dla aplikacji wieloskładnikowych i ciągłego wyświetlania w pomieszczeniu zespołu. |![Przykładowy pulpit nawigacyjny](./media/app-insights-overview/dashboard-tn.png) |
| [**Transmisja strumieniowa metryk na żywo**](app-insights-live-stream.md)<br/>Podczas wdrażania nowej kompilacji obejrzyj te wskaźniki wydajności prawie w czasie rzeczywistym, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami. |![Przykładowe metryki na żywo](./media/app-insights-overview/live-metrics-tn.png) |
| [**Analiza**](app-insights-analytics.md)<br/>Odpowiedz na trudne pytania dotyczące wydajności i użycia Twojej aplikacji za pomocą tego zaawansowanego języka zapytań. |![Przykładowa analiza](./media/app-insights-overview/analytics-tn.png) |
| [**Program Visual Studio**](app-insights-visual-studio.md)<br/>Zobacz dane dotyczące wydajności w kodzie. Przejdź do kodu ze śladów stosu.|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Debuger migawek**](app-insights-snapshot-debugger.md)<br/>Debuguje próbki migawek pobrane z operacji na żywo, używając wartości parametrów.|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Integruje metryki użycia z innymi analizami biznesowymi.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**Interfejs API REST**](https://dev.applicationinsights.io/)<br/>Napisz kod, aby uruchamiać zapytania dla swoich metryk i danych pierwotnych.| ![Interfejs API REST](./media/app-insights-overview/rest-tn.png) |
| [**Eksport ciągły**](app-insights-export-telemetry.md)<br/>Zbiorczy eksport danych pierwotnych do magazynu zaraz po ich odebraniu. |![Eksportowanie](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Jak mogę używać usługi Application Insights?

### <a name="monitor"></a>Monitorowanie
Zainstaluj usługę Application Insights w swojej aplikacji, skonfiguruj [testy sieci Web dostępności](app-insights-monitor-web-app-availability.md) oraz:

* Skonfiguruj [pulpit nawigacyjny](app-insights-dashboards.md) dla pomieszczenia zespołu, aby śledzić obciążenie, elastyczność i wydajność zależności, ładowania stron i wywołania AJAX.
* Wykryj, jakie żądania są najwolniejsze i najczęściej kończą się niepowodzeniem.
* Obejrzyj [transmisję strumieniową na żywo](app-insights-live-stream.md) podczas wdrażania nowej wersji, aby od razu dowiedzieć się o wszelkich pogorszeniach.

### <a name="detect-diagnose"></a>Wykrywanie, diagnozowanie
Po odebraniu alertu lub odnalezieniu problemu:

* Oceń, na ilu użytkowników ma to wpływ.
* Skoreluj błędy z wyjątkami, wywołaniami i śledzeniem zależności.
* Sprawdź profilera, migawki, zrzuty stosu i dzienniki śledzenia.

### <a name="build-measure-learn"></a>Kompilowanie, mierzenie, poznawanie
[Zmierz efektywność](app-insights-usage-overview.md) każdej nowo wdrażanej funkcji.

* Zaplanuj pomiar sposobu używania nowych funkcji środowiska użytkownika lub biznesowych przez klientów.
* Zapisz niestandardową telemetrię do kodu.
* Oprzyj następny cyklu rozwoju na twardych dowodach ze swojej telemetrii.

## <a name="get-started"></a>Rozpoczęcie pracy
Usługa Application Insights jest jedną z wielu usług hostowanych na platformie Microsoft Azure, a dane telemetryczne są przesyłane do analizy i prezentacji. Dlatego przed wykonaniem jakichkolwiek innych czynności będzie potrzebna subskrypcja platformy [Microsoft Azure](http://azure.com). Rejestracja jest bezpłatna, a jeśli wybierzesz podstawowy [plan cenowy](https://azure.microsoft.com/pricing/details/application-insights/) usługi Application Insights, nie będzie opłat do chwili, gdy aplikacja rozrośnie się na tyle, aby mieć znaczne wykorzystanie. Jeśli Twoja organizacja ma już subskrypcję, może ona dodać do niej Twoje konto Microsoft.

Istnieje kilka sposobów, aby rozpocząć. Zacznij od tego, co najlepiej sprawdza się w Twoim przypadku. Resztę możesz dodać później.

* **W czasie wykonywania: wdróż instrumentację aplikacji sieci Web na serwerze.** Pozwala uniknąć wszelkich aktualizacji kodu. Musisz mieć dostęp administracyjny do serwera.
  * [**Usługi IIS lokalnie lub na maszynie wirtualnej**](app-insights-monitor-performance-live-website-now.md)
  * [**Aplikacja sieci Web lub maszyna wirtualna na platformie Azure**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **W czasie tworzenia: dodaj usługę Application Insights do swojego kodu.** Umożliwia pisanie niestandardowych telemetrii oraz instrumentację zaplecza i aplikacji komputerowych.
  * [Program Visual Studio](app-insights-asp-net.md) 2013 Update 2 lub nowszy.
  * Język Java w środowisku [Eclipse](app-insights-java-eclipse.md) lub [innych narzędziach](app-insights-java-get-started.md)
  * [Node.js](app-insights-nodejs.md)
  * [Inne platformy](app-insights-platforms.md)
* **[Instrumentacja stron sieci Web](app-insights-javascript.md)** dla widoku strony, wywołań AJAX i innych telemetrii po stronie klienta.
* **[Analizowanie użycia aplikacji mobilnej](app-insights-mobile-center-quickstart.md)** dzięki integracji z usługą Visual Studio App Center.
* **[Testy dostępności](app-insights-monitor-web-app-availability.md)** — regularnie używaj polecenia ping dla witryny sieci Web z naszych serwerów.


## <a name="next-steps"></a>Następne kroki
Rozpocznij pracę w czasie wykonywania za pomocą rozwiązań:

* [Serwer usług IIS](app-insights-monitor-performance-live-website-now.md)
* [Serwer J2EE](app-insights-java-live.md)

Rozpocznij pracę w czasie programowania za pomocą rozwiązań:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Pomoc techniczna i opinie
* Pytania i problemy:
  * [Rozwiązywanie problemów][qna]
  * [Forum MSDN](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Twoje sugestie:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Blog usługi Application Insights](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Filmy wideo

[![Wprowadzenie animowane](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
