---
title: "aaaSmart wykrywania - anomalii awarii, w usłudze Application Insights | Dokumentacja firmy Microsoft"
description: "Ostrzega o toounusual zmian w polu Szybkość hello aplikacji sieci web tooyour żądań zakończonych niepowodzeniem i udostępnia diagnostyczne analizy. Konfiguracja nie jest potrzebna."
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a>Inteligentne wykrywanie — błąd anomalii
[Usługa Application Insights](app-insights-overview.md) automatycznie powiadamia użytkownika, w czasie rzeczywistym near czy Twoja aplikacja sieci web napotyka nietypowy wzrost hello współczynnik żądań zakończonych niepowodzeniem. Ta funkcja wykrywa nietypowe wzrost hello liczba żądań HTTP lub wywołania zależności, które ma być zgłaszane nie powiodło się. Dla żądania żądań zakończonych niepowodzeniem są zwykle z kodami odpowiedź 400 lub nowszej. toohelp klasyfikowanie i diagnozowanie problemów hello, analizę cech hello hello błędy i powiązane dane telemetryczne znajduje się w hello powiadomień. Dostępne są także portalu Application Insights toohello łącza w celu przeprowadzenia dalszej diagnostyki. Witaj funkcja musi żadnych konfiguracji ani konfiguracji, ponieważ wykorzystuje uczenie maszynowe współczynnik awaryjności normalne hello toopredict algorytmów.

Ta funkcja działa w przypadku języka Java i ASP.NET aplikacji sieci web hostowanych w chmurze hello lub na własnych serwerach. Działa także dla wszystkich aplikacji, który generuje dane telemetryczne żądania lub zależności — na przykład jeśli masz roli procesu roboczego, który wywołuje [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) lub [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).

Po skonfigurowaniu [usługi Application Insights dla projektu](app-insights-overview.md), i pod warunkiem aplikacja generuje określoną minimalną ilość danych telemetrycznych, Inteligentne wykrywanie anomalii awarii przejście 24 godziny toolearn hello jest ich normalne zachowanie aplikacji, zanim jest włączone i wysyłać alerty.

Oto przykładowy alert.

![Alert wykrycia inteligentne przykład przedstawiający analizy klastra wokół awarii](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> Domyślnie otrzymasz krótszą poczty format od tego przykładu. Ale możesz [formatu szczegółowego toothis przełącznika](#configure-alerts).
>
>

Należy zauważyć, że informuje o tym:

* współczynnik awaryjności Hello porównywany toonormal zachowanie aplikacji.
* Ilu użytkowników dotyczy — aby wiedzieć, ile tooworry.
* Wzorzec charakterystyczny skojarzone z błędami hello. W tym przykładzie brak określonej odpowiedzi kod, Nazwa żądania (operacji) i wersji aplikacji. Które natychmiast informuje, gdzie toostart w kodzie. Może to być innych możliwości konkretny system operacyjny klienta lub dotyczących przeglądarki.
* Witaj wyjątek, ślady dziennika i błąd zależności (baz danych lub innych składników zewnętrznych) wyświetlane toobe skojarzone z błędami hello jest określony.
* Łączy bezpośrednio toorelevant wyszukiwania na powitania telemetrii w usłudze Application Insights.

## <a name="benefits-of-smart-detection"></a>Zalety inteligentne wykrywania
Zwykłe [metryki alerty](app-insights-alerts.md) informujące o tym, być może wystąpił problem. Ale inteligentne wykrywanie uruchamia hello pracy diagnostyki dla Ciebie wykonywania partii hello analizy, w przeciwnym razie trzeba będzie toodo samodzielnie. Możesz szybko wyników hello starannie opakowane, pomaga tooget głównego toohello hello problemu.

## <a name="how-it-works"></a>Jak to działa
Inteligentne wykrywanie monitoruje telemetrii hello odebranych z aplikacji, a w szczególności hello awariami. Ta zasada oblicza hello liczba żądań, dla których hello `Successful request` właściwość ma wartość false, a hello liczba zależności wywołań dla których hello `Successful call` właściwość ma wartość false. Dla żądania, domyślnie `Successful request == (resultCode < 400)` (o ile nie musieli napisać kod niestandardowy zbyt[filtru](app-insights-api-filtering-sampling.md#filtering) lub wygenerować własny [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) wywołania). 

Wydajność aplikacji ma typowy wzorzec zachowania. Niektóre żądania lub wywołania zależności będą bardziej podatne toofailure niż inne; i hello ogólną szybkość błąd może miarę wzrostu obciążenia. Wykrywanie inteligentne używa machine learning toofind tych nieprawidłowości.

Jako dane telemetryczne wejścia usługi Application Insights z aplikacji sieci web, Inteligentne wykrywanie porównuje bieżące zachowanie hello wzorami hello widoczne za pośrednictwem hello kilka dni. Jeżeli w porównaniu z poprzednim wydajności jest nietypowy wzrost częstość niepowodzeń, analiza zostanie wywołany.

Po wyzwoleniu analizy usługi hello dokonuje analizy klastra hello nieudanych żądań, tooidentify tootry wzorzec wartości charakteryzujące hello błędów. W powyższym przykładzie hello analizy hello wykrył, że większość awarii nastąpi kod wyniku określone, Nazwa żądania, adres URL serwera hosta i wystąpienia roli. Z kolei analizy hello wykrył, że właściwości systemu operacyjnego klienta hello jest rozproszone na wielu wartości, a więc nie ma na liście.

Gdy usługi są instrumentowane przy użyciu tych wywołań telemetrii, analizator hello szuka wyjątek i błąd zależności, które są skojarzone z żądań w klaster hello zidentyfikował, wraz z przykładem wszystkie dzienniki śledzenia skojarzonych z tymi żądania.

Wynikowa analizy Hello jest wysyłany tooyou jako alertu, o ile nie skonfigurowano jej nie.

Podobnie jak hello [alerty ręcznie ustawić](app-insights-alerts.md), można sprawdzić stan hello hello alertu i skonfigurować go w bloku alerty hello zasobu usługi Application Insights. Jednak w przeciwieństwie do innych alertów, nie należy tooset się lub skonfiguruj wykrywanie inteligentne. Jeśli chcesz, możesz ją wyłączyć lub zmienić jego docelowych adresów e-mail.

## <a name="configure-alerts"></a>Konfigurowanie alertów
Można wyłączyć inteligentne wykrywanie, zmienić hello adresatów wiadomości e-mail, tworzenia elementu webhook lub włączyć toomore szczegółowe komunikaty alertów.

Otwórz stronę alerty hello. Błąd anomalii znajduje się wraz z żadnych alertów, należy ręcznie ustawić, które można zobaczyć, czy aktualnie jest w stanie alertu hello.

![Na stronie Przegląd powitania kliknij Kafelek alerty. Lub na każdej stronie metryki, kliknij przycisk alertów.](./media/app-insights-proactive-failure-diagnostics/021.png)

Kliknij hello alert tooconfigure go.

![Konfiguracja](./media/app-insights-proactive-failure-diagnostics/032.png)

Powiadomienie, że można wyłączyć inteligentne wykrywanie, ale nie można go usunąć (lub utwórz inny).

#### <a name="detailed-alerts"></a>Szczegółowe alertów
Wybranie opcji "Pobierz bardziej szczegółową diagnostykę" hello poczty e-mail będzie zawierać więcej informacji diagnostycznych. Czasami będziesz w stanie toodiagnose hello problem tylko na podstawie danych hello w wiadomości e-mail hello.

Brak nieznaczne ryzyko, że hello alert bardziej szczegółowe mogą zawierać poufne informacje, ponieważ zawiera on wyjątek i śledzenia wiadomości. Jednak to się tylko stanie, jeśli kod umożliwia poufne informacje w tych komunikatach.

## <a name="triaging-and-diagnosing-an-alert"></a>Klasyfikowane i diagnozowania alertu
Alert wskazuje, że wykryto nietypowy wzrost częstości nieudanych żądań hello. Istnieje prawdopodobieństwo, że istnieje problem związany z aplikacji lub z jego środowiska.

Z hello Procent żądań i liczbę użytkowników, których dotyczy problem, można zdecydować, jak pilny problem hello jest. W powyższym przykładzie hello współczynnik awaryjności hello 22,5% porównuje normalną szybkość % 1, wskazuje, czy zły coś. Na hello drugiej strony, użytkownicy tylko 11 zostały zainfekowane. Jeśli był aplikacji, może być możliwe tooassess jak poważny, który jest.

W wielu przypadkach będzie problem hello toodiagnose mogli szybko z nazwy żądania hello, wyjątków, zależności błędu i śledzenia danych udostępnionych.

Brak niektórych innych operacji. Na przykład hello współczynnik awaryjności zależności w tym przykładzie jest hello taka sama, jak hello szybkość wyjątek (89.3%). Sugeruje to, że wyjątek hello wynika bezpośrednio z błędu zależności hello — umożliwiając dalsze gdzie toostart w kodzie.

tooinvestigate Ponadto hello łącza w każdej sekcji prowadzą proste tooa [stronę wyszukiwania](app-insights-diagnostic-search.md) filtrowane toohello odpowiednich żądań, wyjątków, zależności lub śledzenia. Alternatywnie możesz otworzyć hello [portalu Azure](https://portal.azure.com), przejdź toohello zasobu usługi Application Insights dla aplikacji, a otwarcie bloku błędów hello.

W tym przykładzie klikając łącze hello 'Wyświetlanie zależności błędów szczegółów"powoduje otwarcie bloku wyszukiwania usługi Application Insights hello. Widoczny jest hello instrukcję SQL, która zawiera przykład hello głównej przyczyny: wartości null zostały podane na pola wymagane i nie przeszedł sprawdzania poprawności podczas hello operacji zapisywania.

![Wyszukiwanie diagnostyczne](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a>Ostatnie alerty można przeglądać

Kliknij przycisk **inteligentne wykrywanie** tooget toohello najnowszych alertu:

![Podsumowanie alertów](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a>Co to jest różnicą hello...
Inteligentne wykrywanie anomalii awarii uzupełnia inne podobne ale różne funkcje usługi Application Insights.

* [Alerty metryki](app-insights-alerts.md) są ustawiane przez Ciebie i monitorować szeroką gamę metryk, takich jak miejsce zajmowane przez procesor CPU, żądań, czasy ładowania stron i tak dalej. Można ich używać toowarn można na przykład, jeśli potrzebujesz tooadd więcej zasobów. Z kolei inteligentne wykrywanie anomalii awarii obejmuje toonotify niewielki zakres metryki krytycznych (obecnie tylko nieudanych żądań szybkości), przeznaczone, należy w niemal w czasie rzeczywistym sposób po znacznie zwiększa się częstotliwość nieudanych żądań aplikacji sieci web w porównaniu tooweb aplikacji normalne zachowanie.

    Inteligentne wykrywanie automatycznie dostosowuje progu w warunkach tooprevailing odpowiedzi.

    Inteligentne wykrywanie uruchamia hello diagnostycznych odpowiada.
* [Inteligentne wykrywanie anomalii wydajności](app-insights-proactive-performance-diagnostics.md) również używa komputera toodiscover analizy nietypowe wzorce w Twoje metryki i nie jest wymagana żadna konfiguracja przez użytkownika. Ale w odróżnieniu od inteligentne wykrywanie anomalii awarii hello celem inteligentne wykrywanie anomalii wydajności jest segmentów toofind Twojego kolektora użycia, które mogą być udostępniane nieprawidłowo — na przykład określonych stron dla określonego typu przeglądarki. Analiza Hello jest wykonywane codziennie, a jeśli dowolny wynik zostanie znaleziony, jest prawdopodobnie toobe znacznie mniej pilne niż alertu. Z kolei hello analizy w celu wykrycia nieprawidłowości awarii jest wykonywane stale na przychodzące dane telemetryczne, a otrzymasz powiadomienie w ciągu minut Jeśli awariami serwera jest większa, niż oczekiwano.

## <a name="if-you-receive-a-smart-detection-alert"></a>Jeśli zostanie wyświetlony alert inteligentne wykrywania
*Dlaczego otrzymali ten alert?*

* Wykryliśmy nietypowy wzrost liczby żądań zakończonych niepowodzeniem w proporcji toohello normalnej linii bazowej hello poprzedzający okres. Po analizie hello błędów i skojarzone dane telemetryczne naszym zdaniem, że istnieje problem, który powinien wyglądać w.

*Powiadomienie hello oznacza, że problem występuje ostatecznie?*

* Spróbujemy tooalert na przerw w działaniu aplikacji lub pogorszenia się, ale tylko można pełni zrozumieć semantyki hello i hello wpływa na aplikacji hello lub użytkowników.

*Tak guys przeglądania danych?*

* Nie. Usługa Hello jest całkowicie automatyczne. Tylko otrzymasz hello powiadomienia. Twoje dane są [prywatnej](app-insights-data-retention-privacy.md).

*Czy mają toosubscribe toothis alert?*

* Nie. Każda aplikacja, że wysyła żądanie telemetrii ma hello inteligentne wykrywanie alertu.

*Można anulować subskrypcję lub otrzymywać powiadomień hello zamiast tego wysyłane współpracowników toomy?*

* Tak, reguły w alertów, kliknij przycisk tooconfigure reguła wykrywania inteligentne hello go. Wyłącz alerty hello lub zmieniać adresatów hello alertu.

*Utratą hello poczty e-mail. Gdzie można znaleźć hello powiadomienia w portalu hello?*

* W dziennikach działania hello. Na platformie Azure Otwórz hello zasobu usługi Application Insights dla aplikacji, a następnie wybierz Dzienniki aktywności.

*Niektóre alerty hello około znane problemy i nie chcesz tooreceive je.*

* Mamy pomijania alertów w naszej listy prac.

## <a name="next-steps"></a>Następne kroki
Te narzędzia diagnostyczne pomóc sprawdzić telemetrii hello z aplikacji:

* [Eksplorator metryk](app-insights-metrics-explorer.md)
* [Eksplorator wyszukiwania](app-insights-diagnostic-search.md)
* [Analiza - język zaawansowanych zapytań](app-insights-analytics-tour.md)

Inteligentne wykryć są całkowicie automatyczne. A może chcesz tooset niektóre alerty więcej?

* [Ręcznie skonfigurowanej metryki alertów](app-insights-alerts.md)
* [Dostępność testy sieci web](app-insights-monitor-web-app-availability.md)
