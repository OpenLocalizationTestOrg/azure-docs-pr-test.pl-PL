---
title: "wprowadzenie do usługi Azure Application Insights z językiem Java w środowisku Eclipse aaaGet | Dokumentacja firmy Microsoft"
description: "Użyj hello Eclipse wtyczki tooadd wydajności i użycia monitorowania tooyour Java witryny sieci Web z usługą Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Wprowadzenie do usługi Application Insights z językiem Java w środowisku Eclipse
Hello zestaw SDK usługi Application Insights wysyła dane telemetryczne z aplikacji sieci web w języku Java, dzięki czemu można analizować użycia i wydajności. tak, aby pobrać poza hello pole telemetrii, a także interfejsu API służy telemetria niestandardowa toowrite Hello Eclipse wtyczki dla usługi Application Insights automatycznie instaluje program hello zestawu SDK w projekcie.   

## <a name="prerequisites"></a>Wymagania wstępne
Obecnie hello wtyczki działa w przypadku Maven projektów i dynamicznych projekty sieci Web w programie Eclipse.
([Dodaj usługę Application Insights tooother typy projektów języka Java][java].)

Będą potrzebne:

* Oracle środowiska JRE wersji 1.6 lub nowszej
* Subskrypcja zbyt[Microsoft Azure](https://azure.microsoft.com/).
* [Zaćmienie-IDE for Java EE Developers](http://www.eclipse.org/downloads/), indygo lub nowszej.
* System Windows 7 lub nowszym lub Windows Server 2008 lub nowszy

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Zainstaluj hello zestawu SDK w środowisku Eclipse (jeden raz)
Masz tylko toodo to jeden raz w każdym komputerze. Ta czynność powoduje zainstalowanie zestawu narzędzi, które można następnie dodać hello SDK tooeach dynamiczny projekt sieci Web.

1. W programie Eclipse kliknij przycisk Pomoc, instalowanie nowego oprogramowania.

    ![Pomoc, należy zainstalować nowe oprogramowanie](./media/app-insights-java-eclipse/0-plugin.png)
2. Hello zestawu SDK jest http://dl.microsoft.com/eclipse, w obszarze zestawu narzędzi platformy Azure.
3. Usuń zaznaczenie pola wyboru **skontaktuj się z wszystkich witryn aktualizacji...**

    ![Dla zestawu SDK usługi Application Insights wyczyść skontaktuj się z wszystkich witryn aktualizacji](./media/app-insights-java-eclipse/1-plugin.png)

Wykonaj pozostałe kroki dla każdego projektu języka Java hello.

## <a name="create-an-application-insights-resource-in-azure"></a>Tworzenie zasobu usługi Application Insights na platformie Azure
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Utwórz nowy zasób usługi Application Insights. Ustaw aplikację sieci web tooJava typu aplikacji hello.  

    ![Kliknij + i wybierz opcję Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. Znajdź klucz Instrumentacji hello hello nowy zasób. Będzie on potrzebny toopaste w projekcie kodu wkrótce.  

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Dodawanie usługi Application Insights tooyour projektu
1. Dodawanie usługi Application Insights z menu kontekstowego hello projektu sieci web Java.

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/02-context-menu.png)
2. Wklej klucza Instrumentacji hello pochodzący z hello portalu Azure.

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/03-ikey.png)

klucz Hello przesyłany wraz każdy element telemetrii i informuje toodisplay usługi Application Insights w zasobie.

## <a name="run-hello-application-and-see-metrics"></a>Uruchamianie aplikacji hello i widzieć metryki
Uruchom aplikację.

Zwraca tooyour zasobu usługi Application Insights w Microsoft Azure.

Dane żądań HTTP będą wyświetlane na powitania omówienie bloku. (Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).

![Odpowiedź serwera, liczby żądań i błędów ](./media/app-insights-java-eclipse/5-results.png)

Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki.

![Liczba żądań według nazwy](./media/app-insights-java-eclipse/6-barchart.png)

[Dowiedz się więcej o metrykach.][metrics]

Podczas przeglądania właściwości hello żądania, może uzyskać zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątków i.

![Wszystkie ślady dla tego żądania](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Dane telemetryczne po stronie klienta
W bloku Szybki Start hello kliknij przycisk Pobierz toomonitor kod stron sieci web:

![W bloku Omówienie aplikacji wybierz pozycję Szybki Start, Pobierz kod toomonitor stron sieci web. Skopiuj skrypt hello.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Wstaw hello fragment kodu w hello head pliki HTML.

#### <a name="view-client-side-data"></a>Wyświetlanie danych po stronie klienta
Otwórz zaktualizowane stron sieci web i używać ich. Zaczekaj minutę lub dwie, a następnie zwraca tooApplication Insights i otwórz hello użycia bloku. (Za pomocą bloku omówienie hello, przewiń w dół i kliknij opcję użycia).

Strona widoku, użytkownika i sesji metryki pojawią się na blok wykorzystanie hello:

![Sesje, użytkowników i wyświetleń strony](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Dowiedz się więcej o konfigurowaniu telemetrii po stronie klienta.][usage]

## <a name="publish-your-application"></a>Publikowanie aplikacji
Teraz publikowania serwera toohello aplikacji znajduje się w innym użytkownikom go używać i obserwować telemetrii hello widoczne w portalu hello.

* Upewnij się, że zapora pozwala toosend Twojej aplikacji telemetrii toothese portów:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Na serwerach systemu Windows zainstaluj:

  * [Pakiet Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    (Umożliwi to działanie liczników wydajności).

## <a name="exceptions-and-request-failures"></a>Wyjątki i błędy żądań
Nieobsługiwane wyjątki są zbierane automatycznie:

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect danych na inne wyjątki, dostępne są dwie opcje:

* [Wstaw wywołuje tooTrackException w kodzie](app-insights-api-custom-events-metrics.md#trackexception).
* [Zainstaluj hello agenta Java na serwerze](app-insights-java-agent.md). Można określić metody hello ma toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorowanie wywołań metod i zależności zewnętrznych
[Zainstaluj agenta Java hello](app-insights-java-agent.md) toolog określone metody wewnętrznej i wywołań za pośrednictwem JDBC, z danych o chronometrażu.

## <a name="performance-counters"></a>Liczniki wydajności
W bloku Przegląd, przewiń w dół i kliknij przycisk hello **serwerów** kafelka. Zobaczysz zakresu liczników wydajności.

![Przewiń w dół tooclick hello serwerów kafelka](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Dostosowywanie zbierania danych liczników wydajności
Kolekcja toodisable hello standardowego zbioru liczników wydajności, Dodaj hello następującego kodu w węźle głównym hello hello ApplicationInsights.xml pliku:

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Zbieranie danych dodatkowych liczników wydajności
Można określić toobe liczniki wydajności zebrane.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Liczniki JMX (udostępnione przez hello maszyny wirtualnej Java)

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`— Nazwa hello wyświetlana w portalu usługi Application Insights hello.
* `objectName`— Nazwa obiektu JMX hello.
* `attribute`— Atrybut hello toofetch nazwa obiektu JMX hello
* `type`(opcjonalnie) — Witaj typ atrybutu JMX obiektu:
  * wartość domyślna: typ prosty, np. int lub long.
  * `composite`: dane licznika wydajności hello jest w formacie hello "Attribute.Data"
  * `tabular`: dane licznika wydajności hello jest w formacie hello wiersza tabeli

#### <a name="windows-performance-counters"></a>Liczniki wydajności systemu Windows
Każdy [licznika wydajności systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) jest członkiem grupy kategorii (w hello taki sam sposób, że pole jest elementem członkowskim klasy). Kategorie mogą być globalne lub mogą mieć wystąpienia numerowane lub nazwane.

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName — Witaj Nazwa wyświetlana w portalu usługi Application Insights hello.
* categoryName — Witaj kategorii licznika wydajności (obiekt wydajności) z którym skojarzony jest ten licznik wydajności.
* counterName — nazwa hello hello licznika wydajności.
* instanceName — nazwa wystąpienia kategorii licznika wydajności hello hello lub ciąg pusty (""), jeśli kategoria hello zawiera jedno wystąpienie. Jeśli hello CategoryName procesu i hello licznika wydajności, chcieliby toocollect znajduje się w bieżącym procesie JVM hello w uruchomionym aplikacji, określ `"__SELF__"`.

Liczniki wydajności są widoczne jako metryki niestandardowe w [Eksploratorze metryk][metrics].

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Liczniki wydajności sytemu Unix
* [Instalowanie collectd przy użyciu wtyczki usługi Application Insights hello](app-insights-java-collectd.md) tooget szerokiego zakresu systemów i sieci danych.

## <a name="availability-web-tests"></a>Testy dostępności sieci Web
Usługa Application Insights można przetestować witryny sieci Web w toocheck w regularnych odstępach czasu, który jest, a także odpowiada. [tooset się][availability], przewiń w dół tooclick dostępności.

![Przewiń w dół, kliknij opcję Dostępność, a następnie opcję Dodaj test sieci Web](./media/app-insights-java-eclipse/31-config-web-test.png)

Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.

![Przykład testu sieci Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Dowiedz się więcej o testach dostępności sieci Web.][availability]

## <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Jeśli używasz Logback lub Log4J (1.2 lub 2.0) śledzenia, program może automatycznie wysyłane szczegółowe informacje, których można eksplorować i ich wyszukiwanie tooApplication dzienników śledzenia.

[Dowiedz się więcej o dzienników diagnostycznych][javalogs]

## <a name="custom-telemetry"></a>Telemetria niestandardowa
Wstaw kilku wierszy kodu w toofind aplikacji sieci web Java, tak się, co robią użytkownicy z nim lub toohelp diagnozowania problemów.

Strony sieci web JavaScript oraz powitania po stronie serwera w języku Java można wstawić kodu.

[Dowiedz się więcej o telemetrii niestandardowej][track]

## <a name="next-steps"></a>Następne kroki
#### <a name="detect-and-diagnose-issues"></a>Wykrywanie i diagnozowanie problemów
* [Dodaj telemetrię usługi sieci web klienta] [ usage] tooget telemetrii wydajności z powitania klienta sieci web.
* [Ustawianie testów sieci web] [ availability] toomake się, że aplikacja pozostaje na żywo i szybko reagowały.
* [Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toohelp diagnozowania problemów.
* [Śledzenie narzędzia Log4J lub Logback][javalogs]

#### <a name="track-usage"></a>Śledzenie użycia
* [Dodaj telemetrię usługi sieci web klienta] [ usage] toomonitor strony widoki i metryki użytkownika podstawowego.
* [Śledzenie zdarzeń niestandardowych i metryki](app-insights-web-track-usage.md) toolearn o sposobie korzystania z aplikacji, zarówno na powitania klienta i serwera hello.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
