---
title: "aaaTroubleshoot usługi Application Insights w projekcie sieci web Java"
description: "Przewodnik rozwiązywania problemów — monitorowania na żywo aplikacji Java za pomocą usługi Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Rozwiązywanie problemów oraz pytania i odpowiedzi dotyczące usługi Application Insights dla języka Java
Pytania lub problemy z [Azure Application Insights w języku Java][java]? Poniżej przedstawiono kilka wskazówek.

## <a name="build-errors"></a>Błędy kompilacji
**W środowisku Eclipse podczas dodawania hello zestaw SDK usługi Application Insights za pośrednictwem Maven i Gradle, pojawia się błędy sprawdzania poprawności kompilacji lub sumy kontrolnej.**

* Jeśli hello zależności <version> element jest używanie wzorca z symboli wieloznacznych (np. (Maven) `<version>[1.0,)</version>` lub (Gradle) `version:'1.0.+'`), spróbuj zamiast tego określić określonej wersji, takich jak `1.0.2`. Zobacz hello [informacje o wersji](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) hello najnowszej wersji.

## <a name="no-data"></a>Brak danych
**I dodać usługi Application Insights i uruchomiono mojej aplikacji, ale nigdy nie przejrzane danych w portalu hello.**

* Poczekaj kilka minut i kliknij przycisk Odśwież. Wykresy Hello odświeżania się okresowo, ale można również odświeżyć ręcznie. Interwał odświeżania Hello zależy od zakresu czasu hello hello wykresu.
* Sprawdź, czy klucz Instrumentacji zdefiniowane w pliku ApplicationInsights.xml hello (w folderze zasobów hello w projekcie)
* Sprawdź, czy jest nie `<DisableTelemetry>true</DisableTelemetry>` węzła w pliku xml hello.
* W zaporze konieczne może być tooopen porty TCP 80 i 443 dla toodc.services.visualstudio.com ruchu wychodzącego. Zobacz hello [pełnej listy wyjątków zapory](app-insights-ip-addresses.md)
* Uruchom tablicy w hello Microsoft Azure, zobacz Mapowanie stanu usługi hello. W przypadku niektórych alertów oznaczeń, poczekaj, aż one zwrócono tooOK, a następnie zamknij i otwórz ponownie z bloku aplikacji usługi Application Insights.
* Włącz rejestrowanie toohello okna konsoli IDE, dodając `<SDKLogger />` elementu w węźle głównym hello hello ApplicationInsights.xml pliku (w hello folder zasobów w projekcie) i sprawdź, czy wpisy poprzedzone znakiem [Błąd].
* Upewnij się, że poprawny plik ApplicationInsights.xml został pomyślnie załadowany przez hello zestawu Java SDK, analizując komunikaty wyjściowe hello konsoli dla instrukcji "pliku konfiguracyjnego pomyślnie znaleziono" hello.
* Jeśli nie znaleziono pliku konfiguracji hello, sprawdź hello dane wyjściowe komunikaty toosee, gdzie hello pliku konfiguracji są wyszukiwane i upewnij się, że powitalne ApplicationInsights.xml znajduje się w jednej z tych lokalizacji wyszukiwania. Jako zasadą można umieścić plik konfiguracji hello niemal JARs hello Application Insights zestawu SDK. Na przykład: w Tomcat, może oznaczać to hello folderu sieci WEB-INF/lib.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Użycie danych toosee, ale została zatrzymana
* Sprawdź hello [blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).
* Czy osiągnięto limitu przydziału miesięcznego punktów danych? Otwórz ustawienia/przydziału i toofind cennik wychodzących. Jeśli tak, możesz uaktualnić swój plan lub zapłacić za dodatkowe pojemności. Zobacz hello [cennik schemat](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Nie jest wyświetlane wszystkie dane hello używam I oczekiwana
* Otwórz hello przydziałów i cenach bloku i sprawdź, czy [próbkowania](app-insights-sampling.md) jest używany w operacji. (transmisji 100% oznacza, że próbkowania nie jest w operacji). Witaj usługa Application Insights może być zestaw tooaccept tylko część telemetrii hello, przychodzący z aplikacji. Dzięki temu można przechowywać w wykorzystaniu całego przydziału miesięcznego dane telemetryczne. 

## <a name="no-usage-data"></a>Dane użycia
**Dane dotyczące żądań i czasy odpowiedzi, ale nie widoku strony, przeglądarki lub dane użytkownika są widoczne.**

Pomyślnie ustawiono telemetrii toosend aplikacji z powitania serwera. Po następnym krokiem jest zbyt[ustawione telemetrii toosend stron sieci web za pomocą przeglądarki sieci web hello][usage].

Alternatywnie Jeśli klient jest aplikacją w [telefonu lub innego urządzenia][platforms], może wysłać dane telemetryczne z tego miejsca. 

Użyj hello sam tooset klucza Instrumentacji w górę telemetrii klienta i serwera. Witaj danych będą wyświetlane w hello tego samego zasobu usługi Application Insights i będziesz w stanie toocorrelate zdarzenia z klienta i serwera.


## <a name="disabling-telemetry"></a>Wyłączanie telemetrii
**Jak wyłączyć telemetrię kolekcji?**

W kodzie:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Lub** 

Zaktualizuj ApplicationInsights.xml (w folderze zasobów hello w projekcie). Dodaj następujące hello w węźle głównym hello:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Aplikacja hello toorestart metodą XML hello mają po zmianie wartości hello.

## <a name="changing-hello-target"></a>Zmiana hello docelowego
**Jak zmienić projektu wysyła dane do zasobów platformy Azure?**

* [Pobierz klucz Instrumentacji hello hello nowy zasób.][java]
* Jeśli dodano usługę Application Insights tooyour projektu przy użyciu hello Azure zestawu narzędzi dla programu Eclipse kliknij prawym przyciskiem myszy projektu sieci web, wybierz **Azure**, **Konfiguruj usługę Application Insights**i zmienić wartość klucza hello.
* W przeciwnym razie zaktualizować klucza hello w ApplicationInsights.xml hello folderu zasobów w projekcie.

## <a name="debug-data-from-hello-sdk"></a>Debugowanie danych z hello zestawu SDK

**Jak można sprawdzić jakie hello wykonywanie operacji zestawu SDK?**

Dodaj więcej informacji o tym, co się dzieje w hello interfejsu API, tooget `<SDKLogger/>` w węźle głównym hello pliku konfiguracyjnego ApplicationInsights.xml hello.

Można także skonfigurować hello rejestratora toooutput tooa pliku:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Witaj pliki znajdują się w obszarze `%temp%\javasdklogs` lub `java.io.tmpdir` w przypadku serwera Tomcat.


## <a name="hello-azure-start-screen"></a>Witaj ekranu startowego Azure
**Wyświetlane [hello portalu Azure](https://portal.azure.com). Mapy hello Powiedz mi coś o mojej aplikacji?**

Nie, pokazuje kondycję hello Azure serwerów wokół hello world.

*Z tablicy hello Azure start (ekranu głównego) jak znaleźć dane o mojej aplikacji?*

Wykonując [Konfigurowanie aplikacji dla usługi Application Insights][java], kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie wybierz zasób aplikacji hello utworzony dla twojej aplikacji. tooget szybciej w przyszłości, można przypiąć tablicy start toohello aplikacji.

## <a name="intranet-servers"></a>Intranetowych serwerów
**W moim intranecie można monitorować serwer?**

Tak, pod warunkiem, serwer może wysyłać dane telemetryczne portalu Application Insights toohello za pośrednictwem hello publicznej sieci internet. 

W zaporze konieczne może być tooopen porty TCP 80 i 443 dla toodc.services.visualstudio.com ruchu wychodzącego i f5.services.visualstudio.com.

## <a name="data-retention"></a>Przechowywanie danych
**Jak długo dane są przechowywane w portalu hello? Czy jest bezpieczna?**

Zobacz [przechowywanie danych i ochrona prywatności][data].

## <a name="next-steps"></a>Następne kroki
**Skonfigurować usługi Application Insights dla aplikacja Mój serwer Java. Co można zrobić?**

* [Monitorowanie dostępności stron sieci web][availability]
* [Monitorowanie użycia strony sieci web][usage]
* [Śledzenie użycia i diagnozowanie problemów w aplikacji dla urządzeń][platforms]
* [Pisanie kodu tootrack użycia aplikacji][track]
* [Przechwyć dzienników diagnostycznych][javalogs]

## <a name="get-help"></a>Uzyskiwanie pomocy
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

