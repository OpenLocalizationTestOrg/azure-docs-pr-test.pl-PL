---
title: "rejestruje aaaExplore śledzenia Java w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Wyszukiwanie narzędzia Log4J lub Logback dane śledzenia w usłudze Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a>Eksploruj dzienniki śledzenia w usłudze Application Insights w języku Java
Jeśli używasz Logback lub Log4J (1.2 lub 2.0) śledzenia, program może automatycznie wysyłane szczegółowe informacje, których można eksplorować i ich wyszukiwanie tooApplication dzienników śledzenia.

## <a name="install-hello-java-sdk"></a>Zainstaluj zestaw SDK Java hello

Zainstaluj [zestaw SDK usługi Application Insights dla języka Java][java], jeśli jeszcze nie który.

(Jeśli nie chcesz, aby żądania tootrack HTTP, można pominąć większość hello plik XML w konfiguracji, ale musi zawierać co najmniej hello `InstrumentationKey` elementu. Należy także wywołać `new TelemetryClient()` hello tooinitialize zestawu SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Dodaj projekt tooyour bibliotek rejestrowania
*Wybierz odpowiedni sposób hello projektu.*

#### <a name="if-youre-using-maven"></a>Jeśli używasz narzędzia Maven...
Jeśli projekt jest już skonfigurowana toouse Maven dla kompilacji, scalić jedną powitania po wstawek kodu do pliku pom.xml.

Następnie Odśwież hello zależności projektu, tooget hello plików binarnych pobranych.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*1.2 Log4J*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Jeśli używasz narzędzia Gradle...
Jeśli projekt jest już skonfigurowana toouse Gradle dla kompilacji, dodanie hello następujące wiersze toohello `dependencies` w pliku build.gradle:

Następnie Odśwież hello zależności projektu, tooget hello plików binarnych pobranych.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**1.2 Log4J**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>W innym przypadku...
Pobierz i Wyodrębnij hello appendera odpowiednie, a następnie dodaj hello odpowiednią bibliotekę tooyour projektu:

| Rejestratora | Do pobrania | Biblioteka |
| --- | --- | --- |
| Logback |[Zestaw SDK z appendera Logback](https://aka.ms/xt62a4) |applicationinsights — rejestrowanie logback |
| Log4J v2.0 |[Zestaw SDK z narzędzia Log4J appendera v2](https://aka.ms/qypznq) |applicationinsights — rejestrowanie log4j2 |
| 1.2 Log4j |[Zestaw SDK z narzędzia Log4J appendera 1.2](https://aka.ms/ky9cbo) |applicationinsights — rejestrowanie log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Dodaj struktury rejestrowania tooyour appendera hello
toostart pobierania danych śledzenia, scalania hello odpowiedni fragment kodu toohello Log4J lub Logback pliku konfiguracji: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

*1.2 Log4J*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

Witaj appenders usługi Application Insights można odwoływać się przez wszystkie skonfigurowane rejestratora i niekoniecznie hello głównego rejestratora (jak pokazano w powyższych przykładach kodu hello).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Eksploruj dane śledzenia w portalu usługi Application Insights hello
Teraz, gdy skonfigurowano toosend Twojego projektu śledzi tooApplication szczegółowe informacje, można wyświetlać i przeszukiwać te operacje śledzenia w portalu usługi Application Insights hello w hello [wyszukiwania] [ diagnostic] bloku.

![W portalu usługi Application Insights hello Otwórz wyszukiwania](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Następne kroki
[Wyszukiwanie diagnostycznych][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


