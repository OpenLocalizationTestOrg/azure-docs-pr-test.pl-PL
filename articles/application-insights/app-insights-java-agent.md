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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="a4a20-103">Monitor zależności, wyjątków i czasu wykonywania w aplikacji sieci web Java</span><span class="sxs-lookup"><span data-stu-id="a4a20-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="a4a20-104">Jeśli masz [instrumentacji aplikacji sieci web Java za pomocą usługi Application Insights][java], można użyć hello agenta Java tooget lepszy wgląd, bez żadnych zmian w kodzie:</span><span class="sxs-lookup"><span data-stu-id="a4a20-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="a4a20-105">**Zależności:** dane dotyczące wywołania, które aplikacji sprawia, że składniki tooother, w tym:</span><span class="sxs-lookup"><span data-stu-id="a4a20-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="a4a20-106">**Wywołania REST** wprowadzone za pośrednictwem HttpClient, OkHttp i RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="a4a20-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="a4a20-107">**Redis** wywołań za pośrednictwem hello Jedis klienta.</span><span class="sxs-lookup"><span data-stu-id="a4a20-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="a4a20-108">Jeśli wywołanie hello trwa dłużej niż 10s, hello agent również pobiera argumenty wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="a4a20-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="a4a20-109">**[Wywołania JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, bazy danych Oracle lub Apache DOM DB.</span><span class="sxs-lookup"><span data-stu-id="a4a20-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="a4a20-110">wywołania "executeBatch" są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a4a20-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="a4a20-111">MySQL i PostgreSQL, jeśli wywołanie hello trwa dłużej niż 10s, hello agenci będą raportować hello planu zapytania.</span><span class="sxs-lookup"><span data-stu-id="a4a20-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="a4a20-112">**Przechwycono wyjątkami:** dane dotyczące wyjątków, które są obsługiwane w kodzie.</span><span class="sxs-lookup"><span data-stu-id="a4a20-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="a4a20-113">**Czas wykonania metody:** dane dotyczące hello czasu zajmuje tooexecute konkretnych metod.</span><span class="sxs-lookup"><span data-stu-id="a4a20-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="a4a20-114">toouse hello agenta Java, należy zainstalować go na serwerze.</span><span class="sxs-lookup"><span data-stu-id="a4a20-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="a4a20-115">Aplikacje sieci web można wyposażyć hello [zestaw SDK Java usługi Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="a4a20-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="a4a20-116">Zainstaluj agenta usługi Application Insights hello for Java</span><span class="sxs-lookup"><span data-stu-id="a4a20-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="a4a20-117">Na komputerze hello uruchomiony serwer Java [Pobierz agenta hello](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="a4a20-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="a4a20-118">Edytowanie skryptu uruchamiania serwera aplikacji hello, a następnie dodaj następujące maszyny JVM hello:</span><span class="sxs-lookup"><span data-stu-id="a4a20-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="a4a20-119">`javaagent:`*Plik JAR agenta toohello Pełna ścieżka*</span><span class="sxs-lookup"><span data-stu-id="a4a20-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="a4a20-120">Na przykład w Tomcat na komputerze z systemem Linux:</span><span class="sxs-lookup"><span data-stu-id="a4a20-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="a4a20-121">Uruchom ponownie serwer aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4a20-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="a4a20-122">Konfigurowanie agenta hello</span><span class="sxs-lookup"><span data-stu-id="a4a20-122">Configure hello agent</span></span>
<span data-ttu-id="a4a20-123">Utwórz plik o nazwie `AI-Agent.xml` i umieścić go w hello tym samym folderze co plik JAR hello agenta.</span><span class="sxs-lookup"><span data-stu-id="a4a20-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="a4a20-124">Ustaw zawartości hello hello pliku xml.</span><span class="sxs-lookup"><span data-stu-id="a4a20-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="a4a20-125">Edytuj powitania po tooinclude przykład lub hello funkcje, które chcesz pominąć.</span><span class="sxs-lookup"><span data-stu-id="a4a20-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

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

<span data-ttu-id="a4a20-126">Masz tooenable raporty wyjątku i metody chronometrażu dla poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="a4a20-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="a4a20-127">Domyślnie `reportExecutionTime` ma wartość true i `reportCaughtExceptions` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="a4a20-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="a4a20-128">Wyświetlanie danych hello</span><span class="sxs-lookup"><span data-stu-id="a4a20-128">View hello data</span></span>
<span data-ttu-id="a4a20-129">W hello zasobu usługi Application Insights, pojawi się zagregowane zdalnego zależności i metody wykonywania razy [w obszarze hello wydajności Kafelek][metrics].</span><span class="sxs-lookup"><span data-stu-id="a4a20-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="a4a20-130">Otwórz toosearch dla poszczególnych wystąpień raportów zależności, wyjątków i metody, [wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="a4a20-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="a4a20-131">[Diagnozowanie problemów z zależności — Dowiedz się więcej](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="a4a20-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="a4a20-132">Pytania?</span><span class="sxs-lookup"><span data-stu-id="a4a20-132">Questions?</span></span> <span data-ttu-id="a4a20-133">Problemy?</span><span class="sxs-lookup"><span data-stu-id="a4a20-133">Problems?</span></span>
* <span data-ttu-id="a4a20-134">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="a4a20-134">No data?</span></span> [<span data-ttu-id="a4a20-135">Wyjątki zapory zestawu</span><span class="sxs-lookup"><span data-stu-id="a4a20-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="a4a20-136">Rozwiązywanie problemów z technologią Java</span><span class="sxs-lookup"><span data-stu-id="a4a20-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
