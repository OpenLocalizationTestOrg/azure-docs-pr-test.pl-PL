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
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="642f7-103">Eksploruj dzienniki śledzenia w usłudze Application Insights w języku Java</span><span class="sxs-lookup"><span data-stu-id="642f7-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="642f7-104">Jeśli używasz Logback lub Log4J (1.2 lub 2.0) śledzenia, program może automatycznie wysyłane szczegółowe informacje, których można eksplorować i ich wyszukiwanie tooApplication dzienników śledzenia.</span><span class="sxs-lookup"><span data-stu-id="642f7-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="642f7-105">Zainstaluj zestaw SDK Java hello</span><span class="sxs-lookup"><span data-stu-id="642f7-105">Install hello Java SDK</span></span>

<span data-ttu-id="642f7-106">Zainstaluj [zestaw SDK usługi Application Insights dla języka Java][java], jeśli jeszcze nie który.</span><span class="sxs-lookup"><span data-stu-id="642f7-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="642f7-107">(Jeśli nie chcesz, aby żądania tootrack HTTP, można pominąć większość hello plik XML w konfiguracji, ale musi zawierać co najmniej hello `InstrumentationKey` elementu.</span><span class="sxs-lookup"><span data-stu-id="642f7-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="642f7-108">Należy także wywołać `new TelemetryClient()` hello tooinitialize zestawu SDK.)</span><span class="sxs-lookup"><span data-stu-id="642f7-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="642f7-109">Dodaj projekt tooyour bibliotek rejestrowania</span><span class="sxs-lookup"><span data-stu-id="642f7-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="642f7-110">*Wybierz odpowiedni sposób hello projektu.*</span><span class="sxs-lookup"><span data-stu-id="642f7-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="642f7-111">Jeśli używasz narzędzia Maven...</span><span class="sxs-lookup"><span data-stu-id="642f7-111">If you're using Maven...</span></span>
<span data-ttu-id="642f7-112">Jeśli projekt jest już skonfigurowana toouse Maven dla kompilacji, scalić jedną powitania po wstawek kodu do pliku pom.xml.</span><span class="sxs-lookup"><span data-stu-id="642f7-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="642f7-113">Następnie Odśwież hello zależności projektu, tooget hello plików binarnych pobranych.</span><span class="sxs-lookup"><span data-stu-id="642f7-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="642f7-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="642f7-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="642f7-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="642f7-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="642f7-116">*1.2 Log4J*</span><span class="sxs-lookup"><span data-stu-id="642f7-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="642f7-117">Jeśli używasz narzędzia Gradle...</span><span class="sxs-lookup"><span data-stu-id="642f7-117">If you're using Gradle...</span></span>
<span data-ttu-id="642f7-118">Jeśli projekt jest już skonfigurowana toouse Gradle dla kompilacji, dodanie hello następujące wiersze toohello `dependencies` w pliku build.gradle:</span><span class="sxs-lookup"><span data-stu-id="642f7-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="642f7-119">Następnie Odśwież hello zależności projektu, tooget hello plików binarnych pobranych.</span><span class="sxs-lookup"><span data-stu-id="642f7-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="642f7-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="642f7-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="642f7-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="642f7-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="642f7-122">**1.2 Log4J**</span><span class="sxs-lookup"><span data-stu-id="642f7-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="642f7-123">W innym przypadku...</span><span class="sxs-lookup"><span data-stu-id="642f7-123">Otherwise ...</span></span>
<span data-ttu-id="642f7-124">Pobierz i Wyodrębnij hello appendera odpowiednie, a następnie dodaj hello odpowiednią bibliotekę tooyour projektu:</span><span class="sxs-lookup"><span data-stu-id="642f7-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="642f7-125">Rejestratora</span><span class="sxs-lookup"><span data-stu-id="642f7-125">Logger</span></span> | <span data-ttu-id="642f7-126">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="642f7-126">Download</span></span> | <span data-ttu-id="642f7-127">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="642f7-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="642f7-128">Logback</span><span class="sxs-lookup"><span data-stu-id="642f7-128">Logback</span></span> |[<span data-ttu-id="642f7-129">Zestaw SDK z appendera Logback</span><span class="sxs-lookup"><span data-stu-id="642f7-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="642f7-130">applicationinsights — rejestrowanie logback</span><span class="sxs-lookup"><span data-stu-id="642f7-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="642f7-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="642f7-131">Log4J v2.0</span></span> |[<span data-ttu-id="642f7-132">Zestaw SDK z narzędzia Log4J appendera v2</span><span class="sxs-lookup"><span data-stu-id="642f7-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="642f7-133">applicationinsights — rejestrowanie log4j2</span><span class="sxs-lookup"><span data-stu-id="642f7-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="642f7-134">1.2 Log4j</span><span class="sxs-lookup"><span data-stu-id="642f7-134">Log4j v1.2</span></span> |[<span data-ttu-id="642f7-135">Zestaw SDK z narzędzia Log4J appendera 1.2</span><span class="sxs-lookup"><span data-stu-id="642f7-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="642f7-136">applicationinsights — rejestrowanie log4j1_2</span><span class="sxs-lookup"><span data-stu-id="642f7-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="642f7-137">Dodaj struktury rejestrowania tooyour appendera hello</span><span class="sxs-lookup"><span data-stu-id="642f7-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="642f7-138">toostart pobierania danych śledzenia, scalania hello odpowiedni fragment kodu toohello Log4J lub Logback pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="642f7-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="642f7-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="642f7-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="642f7-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="642f7-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="642f7-141">*1.2 Log4J*</span><span class="sxs-lookup"><span data-stu-id="642f7-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="642f7-142">Witaj appenders usługi Application Insights można odwoływać się przez wszystkie skonfigurowane rejestratora i niekoniecznie hello głównego rejestratora (jak pokazano w powyższych przykładach kodu hello).</span><span class="sxs-lookup"><span data-stu-id="642f7-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="642f7-143">Eksploruj dane śledzenia w portalu usługi Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="642f7-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="642f7-144">Teraz, gdy skonfigurowano toosend Twojego projektu śledzi tooApplication szczegółowe informacje, można wyświetlać i przeszukiwać te operacje śledzenia w portalu usługi Application Insights hello w hello [wyszukiwania] [ diagnostic] bloku.</span><span class="sxs-lookup"><span data-stu-id="642f7-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![W portalu usługi Application Insights hello Otwórz wyszukiwania](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="642f7-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="642f7-146">Next steps</span></span>
<span data-ttu-id="642f7-147">[Wyszukiwanie diagnostycznych][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="642f7-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


