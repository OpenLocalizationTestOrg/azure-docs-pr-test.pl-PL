---
title: "aaaPerformance monitorowania aplikacji sieci web Java w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Rozszerzone wydajności monitorowania użycia witryny sieci Web Java z usługą Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Monitor zależności, wyjątków i czasu wykonywania w aplikacji sieci web Java


Jeśli masz [instrumentacji aplikacji sieci web Java za pomocą usługi Application Insights][java], można użyć hello agenta Java tooget lepszy wgląd, bez żadnych zmian w kodzie:

* **Zależności:** dane dotyczące wywołania, które aplikacji sprawia, że składniki tooother, w tym:
  * **Wywołania REST** wprowadzone za pośrednictwem HttpClient, OkHttp i RestTemplate (Spring).
  * **Redis** wywołań za pośrednictwem hello Jedis klienta. Jeśli wywołanie hello trwa dłużej niż 10s, hello agent również pobiera argumenty wywołania hello.
  * **[Wywołania JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, bazy danych Oracle lub Apache DOM DB. wywołania "executeBatch" są obsługiwane. MySQL i PostgreSQL, jeśli wywołanie hello trwa dłużej niż 10s, hello agenci będą raportować hello planu zapytania.
* **Przechwycono wyjątkami:** dane dotyczące wyjątków, które są obsługiwane w kodzie.
* **Czas wykonania metody:** dane dotyczące hello czasu zajmuje tooexecute konkretnych metod.

toouse hello agenta Java, należy zainstalować go na serwerze. Aplikacje sieci web można wyposażyć hello [zestaw SDK Java usługi Application Insights][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Zainstaluj agenta usługi Application Insights hello for Java
1. Na komputerze hello uruchomiony serwer Java [Pobierz agenta hello](https://aka.ms/aijavasdk).
2. Edytowanie skryptu uruchamiania serwera aplikacji hello, a następnie dodaj następujące maszyny JVM hello:
   
    `javaagent:`*Plik JAR agenta toohello Pełna ścieżka*
   
    Na przykład w Tomcat na komputerze z systemem Linux:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Uruchom ponownie serwer aplikacji.

## <a name="configure-hello-agent"></a>Konfigurowanie agenta hello
Utwórz plik o nazwie `AI-Agent.xml` i umieścić go w hello tym samym folderze co plik JAR hello agenta.

Ustaw zawartości hello hello pliku xml. Edytuj powitania po tooinclude przykład lub hello funkcje, które chcesz pominąć.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

Masz tooenable raporty wyjątku i metody chronometrażu dla poszczególnych metod.

Domyślnie `reportExecutionTime` ma wartość true i `reportCaughtExceptions` ma wartość false.

## <a name="view-hello-data"></a>Wyświetlanie danych hello
W hello zasobu usługi Application Insights, pojawi się zagregowane zdalnego zależności i metody wykonywania razy [w obszarze hello wydajności Kafelek][metrics].

Otwórz toosearch dla poszczególnych wystąpień raportów zależności, wyjątków i metody, [wyszukiwania][diagnostic].

[Diagnozowanie problemów z zależności — Dowiedz się więcej](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Pytania? Problemy?
* Brak danych? [Wyjątki zapory zestawu](app-insights-ip-addresses.md)
* [Rozwiązywanie problemów z technologią Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
