---
title: "aaaApplication szczegółowych informacji dla języka Java sieci web aplikacji, które znajdują się już na żywo"
description: "Rozpocznij monitorowanie aplikacji sieci web, która jest już uruchomiona na serwerze"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights dla aplikacji sieci web Java, które znajdują się już na żywo


Jeśli aplikacja sieci web, która jest już uruchomiona na serwerze J2EE, można rozpocząć monitorowanie za pomocą [usługi Application Insights](app-insights-overview.md) bez hello toomake kodu zmiany lub ponownie skompilować projekt. Po wybraniu tej opcji możesz uzyskać informacje o żądaniach HTTP wysyłane tooyour serwera, nieobsługiwanych wyjątków i liczniki wydajności.

Będziesz potrzebować subskrypcji zbyt[Microsoft Azure](https://azure.com).

> [!NOTE]
> procedury Hello na tej stronie dodaje aplikacji sieci web tooyour SDK hello w czasie wykonywania. Tego środowiska uruchomieniowego Instrumentacji jest przydatne, jeśli nie chcesz tooupdate lub Odbuduj kodu źródłowego. Ale jeśli to możliwe, zalecamy [Dodaj kod źródłowy toohello SDK hello](app-insights-java-get-started.md) zamiast tego. Która zapewnia dodatkowe opcje, takie jak zapisywanie aktywności użytkownika tootrack kodu.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Uzyskiwanie klucza instrumentacji usługi Application Insights
1. Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com)
2. Utwórz nowy zasób usługi Application Insights i ustaw aplikacji sieci web tooJava typu aplikacji hello.
   
    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-live/02-create.png)

    Witaj zasób został utworzony w ciągu kilku sekund.

4. Otwórz nowy zasób hello i uzyskać jego klucza instrumentacji. Należy toopaste tego klucza w projekcie kodu wkrótce.
   
    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Pobierz hello zestawu SDK
1. Pobierz hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/aijavasdk). 
2. Na serwerze Wyodrębnij hello SDK zawartość toohello katalogu z którego są załadowane dane binarne Twojego projektu. Jeśli używasz Tomcat ten katalog będzie zazwyczaj w obszarze`webapps/<your_app_name>/WEB-INF/lib`

Należy pamiętać, że toorepeat to konieczne w każdym wystąpieniu serwera i dla każdej aplikacji.

## <a name="3-add-an-application-insights-xml-file"></a>3. Dodaj plik xml usługi Application Insights
Utwórz ApplicationInsights.xml w folderze hello, w którym dodano hello zestawu SDK. Umieść w nim hello następujących XML.

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
* Korelacji zdarzeń to składnik dodawania toohello HTTP żądania. Przypisuje identyfikator żądania tooeach odebranych przez serwer hello i dodaje ten identyfikator jako elementu właściwości tooevery dane telemetryczne jako właściwość hello "Operation.Id". Umożliwia telemetrii hello toocorrelate skojarzone z każdym żądaniem przez ustawienie filtru [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Dodawanie filtru HTTP
Zlokalizuj i Otwórz plik web.xml hello w projekcie i po fragment kodu w węźle hello aplikacji sieci web, z której skonfigurowano filtry aplikacji hello scalania.

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

## <a name="5-check-firewall-exceptions"></a>5. Sprawdź wyjątki zapory
Może być konieczne zbyt[ustawić wyjątki, danych wychodzących toosend](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Uruchom ponownie aplikację sieci web
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Wyświetlanie telemetrii w usłudze Application Insights
Zwraca tooyour zasobu usługi Application Insights w [portalu Microsoft Azure](https://portal.azure.com).

Dane telemetryczne dotyczące żądań HTTP jest wyświetlane na powitania omówienie bloku. (Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).

![dane przykładowe](./media/app-insights-java-live/5-results.png)

Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki. 

![](./media/app-insights-java-live/6-barchart.png)

Podczas przeglądania właściwości hello żądania, może uzyskać zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątków i.

![](./media/app-insights-java-live/7-instance.png)

[Dowiedz się więcej o metrykach.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Następne kroki
* [Dodawanie stron sieci web tooyour telemetrii](app-insights-javascript.md) toomonitor strony widoki i metryki użytkownika.
* [Ustawianie testów sieci web](app-insights-monitor-web-app-availability.md) toomake się, że aplikacja pozostaje na żywo i szybko reagowały.
* [Śledzenie dziennika](app-insights-java-trace-logs.md)
* [Wyszukiwanie zdarzeń i dzienniki](app-insights-diagnostic-search.md) toohelp diagnozowania problemów.

