---
title: "Rozwiązywanie problemów z usługi Application Insights w projekcie sieci web Java"
description: "Przewodnik rozwiązywania problemów — monitorowania na żywo aplikacji Java za pomocą usługi Application Insights."
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: mbullwin
ms.openlocfilehash: 6b1cfa2b52e8e9e2b6a8ab87be6d4269cbe3f1cf
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Rozwiązywanie problemów oraz pytania i odpowiedzi dotyczące usługi Application Insights dla języka Java
Pytania lub problemy z [Azure Application Insights w języku Java][java]? Poniżej przedstawiono kilka wskazówek.

## <a name="build-errors"></a>Błędy kompilacji
**W środowisku Eclipse, dodając zestaw SDK usługi Application Insights za pośrednictwem Maven i Gradle pojawiają się błędy weryfikacji kompilacji lub sumy kontrolnej.**

* Jeśli zależność <version> element jest używanie wzorca z symboli wieloznacznych (np. (Maven) `<version>[1.0,)</version>` lub (Gradle) `version:'1.0.+'`), spróbuj zamiast tego określić określonej wersji, takich jak `1.0.2`. Zobacz [informacje o wersji](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) najnowszej wersji.

## <a name="no-data"></a>Brak danych
**I dodać usługi Application Insights i uruchomiono mojej aplikacji, ale nigdy nie przejrzane danych w portalu.**

* Poczekaj kilka minut i kliknij przycisk Odśwież. Wykresy odświeżania się okresowo, ale można również odświeżyć ręcznie. Interwał odświeżania zależy od zakresu czasu wykresu.
* Sprawdź, czy klucz Instrumentacji zdefiniowane w pliku ApplicationInsights.xml (w folderze zasobów w projekcie)
* Sprawdź, czy jest nie `<DisableTelemetry>true</DisableTelemetry>` węzła w pliku xml.
* W zaporze może być konieczne otwarcie portów TCP 80 i 443 dla ruchu wychodzącego dc.services.visualstudio.com. Zobacz [pełnej listy wyjątków zapory](app-insights-ip-addresses.md)
* Uruchom tablicy w Microsoft Azure, zobacz Mapowanie stanu usługi. W przypadku niektórych alertów oznaczeń, poczekaj, aż one zwrócono do OK, a następnie zamknij i otwórz ponownie z bloku aplikacji usługi Application Insights.
* Włącz rejestrowanie w oknie konsoli IDE, dodając `<SDKLogger />` elementu w obszarze węzła głównego w pliku ApplicationInsights.xml (w folderze zasobów w projekcie) i sprawdź, czy wpisy poprzedzone znakiem [Błąd].
* Upewnij się, że właściwy plik ApplicationInsights.xml został pomyślnie załadowany przez zestawu Java SDK analizując komunikaty wyjściowe konsoli dla instrukcji "pliku konfiguracyjnego pomyślnie znaleziono".
* Jeśli nie znaleziono pliku konfiguracji, sprawdź komunikaty, aby zobaczyć, których pliku konfiguracji są wyszukiwane i upewnij się, że ApplicationInsights.xml znajduje się w jednej z tych lokalizacji wyszukiwania. Jako zasadą można umieścić w pliku config niemal Application Insights SDK JARs. Na przykład: w Tomcat, oznacza to, czy folder w sieci WEB-INF/lib.

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>Używany do wyświetlania danych, ale została zatrzymana
* Sprawdź [blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).
* Czy osiągnięto limitu przydziału miesięcznego punktów danych? Otwórz ustawienia/przydziału i cennik, aby dowiedzieć się. Jeśli tak, możesz uaktualnić swój plan lub zapłacić za dodatkowe pojemności. Zobacz [cennik schemat](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-the-data-im-expecting"></a>Nie widzę wszystkich danych I czy oczekiwana
* Otwórz przydziały i cenach bloku i sprawdź, czy [próbkowania](app-insights-sampling.md) jest używany w operacji. (transmisji 100% oznacza, że próbkowania nie jest w operacji). Usługa Application Insights można ustawić do akceptowania tylko część danych telemetrii, przychodzący z aplikacji. Dzięki temu można przechowywać w wykorzystaniu całego przydziału miesięcznego dane telemetryczne. 

## <a name="no-usage-data"></a>Dane użycia
**Dane dotyczące żądań i czasy odpowiedzi, ale nie widoku strony, przeglądarki lub dane użytkownika są widoczne.**

Pomyślnie tak skonfigurować aplikację, aby wysłać dane telemetryczne z serwera. Teraz z następnym krokiem jest [ustawić stron sieci web, aby wysłać dane telemetryczne z przeglądarki sieci web][usage].

Alternatywnie Jeśli klient jest aplikacją w [telefonu lub innego urządzenia][platforms], może wysłać dane telemetryczne z tego miejsca. 

Aby skonfigurować dane telemetryczne klienta i serwera, należy używać tego samego klucza instrumentacji. Dane będą wyświetlane w tym samym zasobu usługi Application Insights i będzie możliwe do korelowanie zdarzeń z klienta i serwera.


## <a name="disabling-telemetry"></a>Wyłączanie telemetrii
**Jak wyłączyć telemetrię kolekcji?**

W kodzie:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Lub** 

Zaktualizuj ApplicationInsights.xml (w folderze zasobów w projekcie). Dodaj następujący kod w węźle głównym:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Przy użyciu metody XML, należy ponownie uruchomić aplikację po zmianie wartości.

## <a name="changing-the-target"></a>Zmiana obiektu docelowego
**Jak zmienić projektu wysyła dane do zasobów platformy Azure?**

* [Pobierz klucz Instrumentacji nowego zasobu.][java]
* Jeśli dodano usługę Application Insights do projektu przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse, kliknij prawym przyciskiem myszy projektu sieci web, wybierz **Azure**, **Konfiguruj usługę Application Insights**i zmienić wartość klucza.
* W przeciwnym razie zaktualizować klucza w ApplicationInsights.xml w folderze zasobów w projekcie.

## <a name="debug-data-from-the-sdk"></a>Debugowanie danych z zestawu SDK

**Jak można sprawdzić czynności zestawu SDK?**

Aby uzyskać więcej informacji o tym, co się dzieje w interfejsie API, Dodaj `<SDKLogger/>` w węźle głównym ApplicationInsights.xml pliku konfiguracji.

Można także skonfigurować rejestratora do wypełniania wyjściowego pliku:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Pliki można znaleźć w `%temp%\javasdklogs` lub `java.io.tmpdir` w przypadku serwera Tomcat.


## <a name="the-azure-start-screen"></a>Ekranu startowego Azure
**Wyświetlane [portalu Azure](https://portal.azure.com). Mapy Powiedz mi coś o mojej aplikacji?**

Nie, przedstawia prawidłowość serwerów platformy Azure na świecie.

*Z tablicy Azure start (ekranu głównego) jak znaleźć dane o mojej aplikacji?*

Wykonując [Konfigurowanie aplikacji dla usługi Application Insights][java], kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie wybierz zasób aplikacji utworzone dla aplikacji. Aby uzyskać szybciej w przyszłości, można przypiąć swoją aplikację w celu rozpoczęcia tablicy.

## <a name="intranet-servers"></a>Intranetowych serwerów
**W moim intranecie można monitorować serwer?**

Tak, pod warunkiem, że serwer może wysłać dane telemetryczne do portalu usługi Application Insights za pośrednictwem publicznej sieci internet. 

W zaporze może być konieczne otwarcie portów TCP 80 i 443 dla ruchu wychodzącego dc.services.visualstudio.com i f5.services.visualstudio.com.

## <a name="data-retention"></a>Przechowywanie danych
**Jak długo dane są przechowywane w portalu Czy jest bezpieczna?**

Zobacz [przechowywanie danych i ochrona prywatności][data].

## <a name="debug-logging"></a>Funkcję rejestrowania debugowania
Korzysta z usługi Application Insights `org.apache.http`. To jest przenoszony w słoików podstawowe usługi Application Insights w przestrzeni nazw `com.microsoft.applicationinsights.core.dependencies.http`. Dzięki temu usługi Application Insights do obsługi scenariuszy, w przypadku, gdy różne wersje tego samego `org.apache.http` istnieje w jeden podstawowy kod. 

>[!NOTE]
>Jeśli włączysz poziomu rejestrowania debugowania dla wszystkich obszarów nazw w aplikacji, będą honorowane przez wszystkie moduły wykonywanego w tym `org.apache.http` przemianowana `com.microsoft.applicationinsights.core.dependencies.http`. Usługa Application Insights nie będzie można zastosować filtrowanie dla tych wywołań, ponieważ wywołanie dziennika jest wykonywane przez biblioteki Apache. Poziom rejestrowania debugowania utworzyć znaczną ilość danych dziennika i nie jest zalecane dla wystąpień produkcyjnym.


## <a name="next-steps"></a>Następne kroki
**Skonfigurować usługi Application Insights dla aplikacja Mój serwer Java. Co można zrobić?**

* [Monitorowanie dostępności stron sieci web][availability]
* [Monitorowanie użycia strony sieci web][usage]
* [Śledzenie użycia i diagnozowanie problemów w aplikacji dla urządzeń][platforms]
* [Napisz kod umożliwiający śledzenie użycia aplikacji][track]
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

