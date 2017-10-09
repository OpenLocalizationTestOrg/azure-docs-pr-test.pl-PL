---
title: "analizy aplikacji sieci web aaaJava w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności aplikacji sieci Web w języku Java za pomocą usługi Application Insights. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Wprowadzenie do usługi Application Insights w projekcie sieci Web w języku Java


[Usługa Application Insights](https://azure.microsoft.com/services/application-insights/) jest usługą extensible analizy dla deweloperów sieci web, które pomaga zrozumieć hello wydajności i użycia aplikacji na żywo. Użyj go za[wykrywanie i diagnozowanie problemów z wydajnością oraz wyjątków](app-insights-detect-triage-diagnose.md), i [napisać kod] [ api] tootrack, czy użytkownicy z aplikacją.

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

Usługa Application Insights obsługuje aplikacje w języku Java działające w systemach Linux, Unix lub Windows.

Potrzebne elementy:

* Środowisko Oracle JRE 1.6 lub nowsze albo Zulu JRE 1.6 lub nowsze
* Subskrypcja zbyt[Microsoft Azure](https://azure.microsoft.com/).

*Jeśli masz aplikację sieci web, która jest już na żywo można wykonać procedury alternatywne hello zbyt[dodać hello zestawu SDK w czasie wykonywania na serwerze sieci web hello](app-insights-java-live.md). To alternatywne rozwiązanie pozwala uniknąć ponownie skompilować kod hello, ale nie otrzymasz hello opcja toowrite tootrack użytkownika działania związane z kodem.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Uzyskiwanie klucza instrumentacji usługi Application Insights
1. Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com).
2. Utwórz zasób usługi Application Insights. Ustaw aplikację sieci web tooJava typu aplikacji hello.

    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-get-started/02-create.png)
3. Znajdź klucz Instrumentacji hello hello nowy zasób. Należy toopaste tego klucza w projekcie kodu wkrótce.

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Dodaj hello zestaw SDK usługi Application Insights dla programu Java tooyour projektu
*Wybierz odpowiedni sposób hello projektu.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Jeśli używasz Zaćmienie-toocreate projekt Maven lub dynamicznej sieci Web...
Użyj hello [zestaw SDK usługi Application Insights dla języka Java wtyczki][eclipse].

#### <a name="if-youre-using-maven"></a>Jeśli używasz narzędzia Maven...
Jeśli projekt jest już skonfigurowana toouse Maven dla kompilacji, scalić hello następującego pliku pom.xml tooyour kodu.

Następnie dane binarne odświeżania hello projektu zależności tooget hello pobrane.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *Błędy kompilacji lub walidacji sumy kontrolnej?* Spróbuj użyć określonej wersji, np.: `<version>1.0.n</version>`. Najnowsza wersja hello znajdziesz w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) lub w naszym [artefakty Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Należy tooupdate tooa nowego zestawu SDK?* Odśwież zależności projektu.

#### <a name="if-youre-using-gradle"></a>Jeśli używasz narzędzia Gradle...
Jeśli projekt jest już skonfigurowana toouse Gradle dla kompilacji, scalić hello poniższe plik build.gradle tooyour kodu.

Dane binarne odświeżania hello projektu zależności tooget hello pobierane.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Błędy kompilacji lub walidacji sumy kontrolnej? Spróbuj użyć określonej wersji, np.:* `version:'1.0.n'`. *Najnowsza wersja hello znajdziesz w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa nowego zestawu SDK*
  * Odśwież zależności projektu.

#### <a name="otherwise-"></a>W innym przypadku...
Ręcznie Dodaj hello SDK:

1. Pobierz hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/aijavasdk).
2. Wyodrębnij pliki binarne hello z pliku zip hello, a następnie dodać tooyour projektu.

### <a name="questions"></a>Pytania...
* *Co to jest relacja hello między hello `-core` i `-web` składników w hello zip?*

  * `applicationinsights-core`Umożliwia także hello interfejsu API systemu od zera. Ten składnik jest zawsze potrzebny.
  * Element `applicationinsights-web` dostarcza metryki do śledzenia liczby żądań HTTP i czasów odpowiedzi. Możesz pominąć ten składnik, jeśli nie chcesz automatycznie zbierać tych danych telemetrycznych. Na przykład, jeśli chcesz toowrite własnych.
* *Witaj tooupdate zestawu SDK, gdy firma Microsoft Opublikuj zmiany*

  * Pobierz najnowsze hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/qqkaq6) i Zamień hello stare.
  * Zmiany zostały opisane w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Dodawanie pliku .xml usługi Application Insights
Dodaj folder zasobów toohello ApplicationInsights.xml w projekcie, lub upewnij się, że jest ona dodawana ścieżka klasy wdrożenia tooyour projektu. Skopiuj powitania po XML do niego.

Zastąp klucza Instrumentacji hello pochodzący z hello portalu Azure.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* klucz Instrumentacji Hello przesyłany wraz każdy element telemetrii i informuje toodisplay usługi Application Insights w zasobie.
* Witaj składnika żądania HTTP jest opcjonalna. Automatycznie wysyła dane telemetryczne dotyczące żądań i odpowiedzi razy toohello portalu.
* Korelacji zdarzeń to składnik dodawania toohello HTTP żądania. Przypisuje identyfikator żądania tooeach odebranych przez serwer hello i dodaje ten identyfikator jako elementu właściwości tooevery dane telemetryczne jako właściwość hello "Operation.Id". Umożliwia telemetrii hello toocorrelate skojarzone z każdym żądaniem przez ustawienie filtru [diagnostycznych wyszukiwania][diagnostic].
* Klucz usługi Application Insights Hello mogą zostać przekazane dynamicznie z hello portalu Azure jako właściwość systemu (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Jeśli nie zdefiniowano żadnej właściwości, sprawdzana jest zmienna środowiskowa (APPLICATION_INSIGHTS_IKEY) w ustawieniach aplikacji platformy Azure. Jeśli obie właściwości hello jest nieokreślona, z ApplicationInsights.xml używana jest domyślna hello InstrumentationKey. Ta sekwencja pomaga toomanage InstrumentationKeys różne dla różnych środowisk dynamicznie.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Klucz Instrumentacji hello tooset alternatywnych metod
Zestaw SDK usługi Application Insights jest szuka klucza hello w następującej kolejności:

1. Właściwość systemu: -DAPPLICATION_INSIGHTS_IKEY=Twój_klucz_ikey
2. Zmienna środowiskowa: APPLICATION_INSIGHTS_IKEY
3. Plik konfiguracji: ApplicationInsights.xml

Możesz również [ustawić klucz w kodzie](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Dodawanie filtru HTTP
ostatni krok konfiguracji Hello umożliwia toolog składnika żądania HTTP hello każdego żądania sieci web. (Nie wymagane, jeśli tylko interfejsu API systemu od zera hello.)

Zlokalizuj i Otwórz plik web.xml hello w projekcie i następującego kodu w węźle hello aplikacji sieci web, której skonfigurowano filtry aplikacji hello scalania.

tooget hello najdokładniejszych wyników, filtr hello należy mapować przed wszystkie inne filtry.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Jeśli używasz środowiska Spring Web MVC 3.1 lub nowszego
Edycja tych elementów *-servlet.xml tooinclude hello usługi Application Insights pakietu:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Jeśli używasz środowiska Struts 2
Dodaj ten element toohello poprzeczne plik konfiguracji (zazwyczaj nazwany struts.xml lub default.xml poprzeczne):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Jeśli masz interceptory zdefiniowane w stosie domyślne interceptora powitania po prostu można dodać toothat stosu.)

## <a name="5-run-your-application"></a>5. Uruchamianie aplikacji
Uruchamiany w trybie debugowania na komputerze deweloperskim albo publikowanie tooyour server.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Wyświetlanie telemetrii w usłudze Application Insights
Zwraca tooyour zasobu usługi Application Insights w [portalu Microsoft Azure](https://portal.azure.com).

W bloku omówienie hello pojawi się dane żądania HTTP. (Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

[Dowiedz się więcej o metrykach.][metrics]

Kliknij przycisk za pomocą dowolnego wykresu toosee bardziej szczegółowe agregowana metryki.

![](./media/app-insights-java-get-started/6-barchart.png)

> Usługi Application Insights zakłada hello format żądania HTTP dla aplikacji MVC: `VERB controller/action`. Na przykład żądania `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` i `GET Home/Product/sdf96vws` są grupowane w ramach pozycji `GET Home/Product`. To grupowanie umożliwia zrozumiałe agregowanie żądań, na przykład podawanie liczby żądań i średniego czasu ich wykonania.
>
>

### <a name="instance-data"></a>Dane wystąpienia
Kliknij określone żądanie wystąpień poszczególnych typów toosee.

W usłudze Application Insights są wyświetlane dwa rodzaje danych: dane zagregowane, przechowywane i wyświetlane jako średnie, liczniki i sumy, oraz dane wystąpienia — indywidualne raporty dotyczące żądań HTTP, wyjątków, wyświetleń stron lub zdarzeń niestandardowych.

Podczas przeglądania właściwości hello żądania, można przejrzeć zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątki.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analiza: zaawansowany język zapytań
Jak gromadzone większej ilości danych, można uruchomić zapytania zarówno tooaggregate danych i toofind poszczególnych wystąpień.  [Analiza](app-insights-analytics.md) jest zaawansowanym narzędziem, którego można używać zarówno w celu poznania wydajności i użycia, jak i do celów diagnostycznych.

![Przykład analizy](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Zainstaluj aplikację na powitania serwera
Teraz publikowania serwera toohello aplikacji znajduje się w innym użytkownikom go używać i obserwować telemetrii hello widoczne w portalu hello.

* Upewnij się, że zapora pozwala toosend Twojej aplikacji telemetrii toothese portów:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Jeśli ruch wychodzący ma być kierowany przez zaporę, zdefiniuj właściwości systemu `http.proxyHost` i `http.proxyPort`.

* Na serwerach systemu Windows zainstaluj:

  * [Pakiet Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    Ten składnik umożliwia działanie liczników wydajności.


## <a name="exceptions-and-request-failures"></a>Wyjątki i błędy żądań
Nieobsługiwane wyjątki są zbierane automatycznie:

![Otwórz ustawienia, błędy](./media/app-insights-java-get-started/21-exceptions.png)

toocollect danych na inne wyjątki, dostępne są dwie opcje:

* [Wstaw wywołuje tootrackException() w kodzie][apiexceptions].
* [Zainstaluj hello agenta Java na serwerze](app-insights-java-agent.md). Można określić metody hello ma toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorowanie wywołań metod i zależności zewnętrznych
[Zainstaluj agenta Java hello](app-insights-java-agent.md) toolog określone metody wewnętrznej i wywołań za pośrednictwem JDBC, z danych o chronometrażu.

## <a name="performance-counters"></a>Liczniki wydajności
Otwórz **ustawienia**, **serwerów**, toosee zakresu liczników wydajności.

![](./media/app-insights-java-get-started/11-perf-counters.png)

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

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Liczniki wydajności sytemu Unix
* [Instalowanie collectd przy użyciu wtyczki usługi Application Insights hello](app-insights-java-collectd.md) tooget szerokiego zakresu systemów i sieci danych.

## <a name="get-user-and-session-data"></a>Pobieranie danych użytkownika i sesji
Wysyłasz już telemetrię z serwera sieci Web. Teraz tooget hello widok 360 stopni aplikacji, można dodać więcej monitorowania:

* [Dodawanie stron sieci web tooyour telemetrii] [ usage] toomonitor strony widoki i metryki użytkownika.
* [Ustawianie testów sieci web] [ availability] toomake się, że aplikacja pozostaje na żywo i szybko reagowały.

## <a name="capture-log-traces"></a>Przechwytywanie danych dziennika śledzenia
Można użyć tooslice usługi Application Insights i wykorzystuj dzienniki z narzędzia Log4J, Logback lub innych platform rejestrowania. Dzienniki hello jest skorelowany z żądań HTTP i innych danych telemetrycznych. [Dowiedz się, jak to zrobić][javalogs].

## <a name="send-your-own-telemetry"></a>Wysyłanie własnej telemetrii
Teraz, po zainstalowaniu hello zestawu SDK, można użyć toosend interfejsu API hello własnych danych telemetrycznych.

* [Śledzenie zdarzeń niestandardowych i metryki] [ api] toolearn, jakie użytkownicy wirtualni z aplikacją.
* [Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toohelp diagnozowania problemów.

## <a name="availability-web-tests"></a>Testy dostępności sieci Web
Usługa Application Insights można przetestować witryny sieci Web w toocheck w regularnych odstępach czasu, który jest, a także odpowiada. [tooset się][availability], kliknij przycisk testy sieci Web.

![Kliknij pozycję Testy sieci Web, a następnie kliknij pozycję Dodaj test sieci Web](./media/app-insights-java-get-started/31-config-web-test.png)

Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.

![Przykład testu sieci Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Dowiedz się więcej o testach dostępności sieci Web.][availability]

## <a name="questions-problems"></a>Pytania? Problemy?
[Rozwiązywanie problemów z technologią Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie wywołań zależności](app-insights-java-agent.md)
* [Monitorowanie liczników wydajności sytemu Unix](app-insights-java-collectd.md)
* Dodaj [monitorowanie stron sieci web tooyour](app-insights-javascript.md) czas ładowania strony toomonitor, wywołania AJAX wyjątków przeglądarki.
* Zapis [telemetria niestandardowa](app-insights-api-custom-events-metrics.md) tootrack użycia w przeglądarce hello lub na powitania serwera.
* Utwórz [pulpity nawigacyjne](app-insights-dashboards.md) toobring razem hello klucza wykresy do monitorowania systemu.
* Tworzenie zaawansowanych zapytań dotyczących telemetrii z poziomu aplikacji przy użyciu usługi [Analytics](app-insights-analytics.md)
* Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
