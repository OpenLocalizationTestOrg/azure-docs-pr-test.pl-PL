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
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="36a1d-103">Wprowadzenie do usługi Application Insights w projekcie sieci Web w języku Java</span><span class="sxs-lookup"><span data-stu-id="36a1d-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="36a1d-104">[Usługa Application Insights](https://azure.microsoft.com/services/application-insights/) jest usługą extensible analizy dla deweloperów sieci web, które pomaga zrozumieć hello wydajności i użycia aplikacji na żywo.</span><span class="sxs-lookup"><span data-stu-id="36a1d-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="36a1d-105">Użyj go za[wykrywanie i diagnozowanie problemów z wydajnością oraz wyjątków](app-insights-detect-triage-diagnose.md), i [napisać kod] [ api] tootrack, czy użytkownicy z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="36a1d-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="36a1d-107">Usługa Application Insights obsługuje aplikacje w języku Java działające w systemach Linux, Unix lub Windows.</span><span class="sxs-lookup"><span data-stu-id="36a1d-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="36a1d-108">Potrzebne elementy:</span><span class="sxs-lookup"><span data-stu-id="36a1d-108">You need:</span></span>

* <span data-ttu-id="36a1d-109">Środowisko Oracle JRE 1.6 lub nowsze albo Zulu JRE 1.6 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="36a1d-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="36a1d-110">Subskrypcja zbyt[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="36a1d-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="36a1d-111">*Jeśli masz aplikację sieci web, która jest już na żywo można wykonać procedury alternatywne hello zbyt[dodać hello zestawu SDK w czasie wykonywania na serwerze sieci web hello](app-insights-java-live.md). To alternatywne rozwiązanie pozwala uniknąć ponownie skompilować kod hello, ale nie otrzymasz hello opcja toowrite tootrack użytkownika działania związane z kodem.*</span><span class="sxs-lookup"><span data-stu-id="36a1d-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="36a1d-112">1. Uzyskiwanie klucza instrumentacji usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="36a1d-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="36a1d-113">Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36a1d-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="36a1d-114">Utwórz zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36a1d-114">Create an Application Insights resource.</span></span> <span data-ttu-id="36a1d-115">Ustaw aplikację sieci web tooJava typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="36a1d-115">Set hello application type tooJava web application.</span></span>

    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="36a1d-117">Znajdź klucz Instrumentacji hello hello nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="36a1d-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="36a1d-118">Należy toopaste tego klucza w projekcie kodu wkrótce.</span><span class="sxs-lookup"><span data-stu-id="36a1d-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="36a1d-120">2. Dodaj hello zestaw SDK usługi Application Insights dla programu Java tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="36a1d-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="36a1d-121">*Wybierz odpowiedni sposób hello projektu.*</span><span class="sxs-lookup"><span data-stu-id="36a1d-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="36a1d-122">Jeśli używasz Zaćmienie-toocreate projekt Maven lub dynamicznej sieci Web...</span><span class="sxs-lookup"><span data-stu-id="36a1d-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="36a1d-123">Użyj hello [zestaw SDK usługi Application Insights dla języka Java wtyczki][eclipse].</span><span class="sxs-lookup"><span data-stu-id="36a1d-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="36a1d-124">Jeśli używasz narzędzia Maven...</span><span class="sxs-lookup"><span data-stu-id="36a1d-124">If you're using Maven...</span></span>
<span data-ttu-id="36a1d-125">Jeśli projekt jest już skonfigurowana toouse Maven dla kompilacji, scalić hello następującego pliku pom.xml tooyour kodu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="36a1d-126">Następnie dane binarne odświeżania hello projektu zależności tooget hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="36a1d-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

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

* <span data-ttu-id="36a1d-127">*Błędy kompilacji lub walidacji sumy kontrolnej?*</span><span class="sxs-lookup"><span data-stu-id="36a1d-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="36a1d-128">Spróbuj użyć określonej wersji, np.: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="36a1d-129">Najnowsza wersja hello znajdziesz w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) lub w naszym [artefakty Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="36a1d-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="36a1d-130">*Należy tooupdate tooa nowego zestawu SDK?*</span><span class="sxs-lookup"><span data-stu-id="36a1d-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="36a1d-131">Odśwież zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="36a1d-132">Jeśli używasz narzędzia Gradle...</span><span class="sxs-lookup"><span data-stu-id="36a1d-132">If you're using Gradle...</span></span>
<span data-ttu-id="36a1d-133">Jeśli projekt jest już skonfigurowana toouse Gradle dla kompilacji, scalić hello poniższe plik build.gradle tooyour kodu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="36a1d-134">Dane binarne odświeżania hello projektu zależności tooget hello pobierane.</span><span class="sxs-lookup"><span data-stu-id="36a1d-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="36a1d-135">*Błędy kompilacji lub walidacji sumy kontrolnej? Spróbuj użyć określonej wersji, np.:* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="36a1d-136">*Najnowsza wersja hello znajdziesz w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="36a1d-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="36a1d-137">*tooupdate tooa nowego zestawu SDK*</span><span class="sxs-lookup"><span data-stu-id="36a1d-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="36a1d-138">Odśwież zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="36a1d-139">W innym przypadku...</span><span class="sxs-lookup"><span data-stu-id="36a1d-139">Otherwise ...</span></span>
<span data-ttu-id="36a1d-140">Ręcznie Dodaj hello SDK:</span><span class="sxs-lookup"><span data-stu-id="36a1d-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="36a1d-141">Pobierz hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="36a1d-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="36a1d-142">Wyodrębnij pliki binarne hello z pliku zip hello, a następnie dodać tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="36a1d-143">Pytania...</span><span class="sxs-lookup"><span data-stu-id="36a1d-143">Questions...</span></span>
* <span data-ttu-id="36a1d-144">*Co to jest relacja hello między hello `-core` i `-web` składników w hello zip?*</span><span class="sxs-lookup"><span data-stu-id="36a1d-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="36a1d-145">`applicationinsights-core`Umożliwia także hello interfejsu API systemu od zera.</span><span class="sxs-lookup"><span data-stu-id="36a1d-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="36a1d-146">Ten składnik jest zawsze potrzebny.</span><span class="sxs-lookup"><span data-stu-id="36a1d-146">You always need this component.</span></span>
  * <span data-ttu-id="36a1d-147">Element `applicationinsights-web` dostarcza metryki do śledzenia liczby żądań HTTP i czasów odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="36a1d-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="36a1d-148">Możesz pominąć ten składnik, jeśli nie chcesz automatycznie zbierać tych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="36a1d-149">Na przykład, jeśli chcesz toowrite własnych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="36a1d-150">*Witaj tooupdate zestawu SDK, gdy firma Microsoft Opublikuj zmiany*</span><span class="sxs-lookup"><span data-stu-id="36a1d-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="36a1d-151">Pobierz najnowsze hello [zestaw SDK usługi Application Insights dla języka Java](https://aka.ms/qqkaq6) i Zamień hello stare.</span><span class="sxs-lookup"><span data-stu-id="36a1d-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="36a1d-152">Zmiany zostały opisane w hello [informacje o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="36a1d-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="36a1d-153">3. Dodawanie pliku .xml usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="36a1d-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="36a1d-154">Dodaj folder zasobów toohello ApplicationInsights.xml w projekcie, lub upewnij się, że jest ona dodawana ścieżka klasy wdrożenia tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="36a1d-155">Skopiuj powitania po XML do niego.</span><span class="sxs-lookup"><span data-stu-id="36a1d-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="36a1d-156">Zastąp klucza Instrumentacji hello pochodzący z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36a1d-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="36a1d-157">klucz Instrumentacji Hello przesyłany wraz każdy element telemetrii i informuje toodisplay usługi Application Insights w zasobie.</span><span class="sxs-lookup"><span data-stu-id="36a1d-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="36a1d-158">Witaj składnika żądania HTTP jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="36a1d-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="36a1d-159">Automatycznie wysyła dane telemetryczne dotyczące żądań i odpowiedzi razy toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="36a1d-160">Korelacji zdarzeń to składnik dodawania toohello HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="36a1d-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="36a1d-161">Przypisuje identyfikator żądania tooeach odebranych przez serwer hello i dodaje ten identyfikator jako elementu właściwości tooevery dane telemetryczne jako właściwość hello "Operation.Id".</span><span class="sxs-lookup"><span data-stu-id="36a1d-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="36a1d-162">Umożliwia telemetrii hello toocorrelate skojarzone z każdym żądaniem przez ustawienie filtru [diagnostycznych wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="36a1d-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="36a1d-163">Klucz usługi Application Insights Hello mogą zostać przekazane dynamicznie z hello portalu Azure jako właściwość systemu (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="36a1d-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="36a1d-164">Jeśli nie zdefiniowano żadnej właściwości, sprawdzana jest zmienna środowiskowa (APPLICATION_INSIGHTS_IKEY) w ustawieniach aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36a1d-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="36a1d-165">Jeśli obie właściwości hello jest nieokreślona, z ApplicationInsights.xml używana jest domyślna hello InstrumentationKey.</span><span class="sxs-lookup"><span data-stu-id="36a1d-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="36a1d-166">Ta sekwencja pomaga toomanage InstrumentationKeys różne dla różnych środowisk dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="36a1d-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="36a1d-167">Klucz Instrumentacji hello tooset alternatywnych metod</span><span class="sxs-lookup"><span data-stu-id="36a1d-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="36a1d-168">Zestaw SDK usługi Application Insights jest szuka klucza hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="36a1d-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="36a1d-169">Właściwość systemu: -DAPPLICATION_INSIGHTS_IKEY=Twój_klucz_ikey</span><span class="sxs-lookup"><span data-stu-id="36a1d-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="36a1d-170">Zmienna środowiskowa: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="36a1d-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="36a1d-171">Plik konfiguracji: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="36a1d-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="36a1d-172">Możesz również [ustawić klucz w kodzie](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="36a1d-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="36a1d-173">4. Dodawanie filtru HTTP</span><span class="sxs-lookup"><span data-stu-id="36a1d-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="36a1d-174">ostatni krok konfiguracji Hello umożliwia toolog składnika żądania HTTP hello każdego żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="36a1d-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="36a1d-175">(Nie wymagane, jeśli tylko interfejsu API systemu od zera hello.)</span><span class="sxs-lookup"><span data-stu-id="36a1d-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="36a1d-176">Zlokalizuj i Otwórz plik web.xml hello w projekcie i następującego kodu w węźle hello aplikacji sieci web, której skonfigurowano filtry aplikacji hello scalania.</span><span class="sxs-lookup"><span data-stu-id="36a1d-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="36a1d-177">tooget hello najdokładniejszych wyników, filtr hello należy mapować przed wszystkie inne filtry.</span><span class="sxs-lookup"><span data-stu-id="36a1d-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="36a1d-178">Jeśli używasz środowiska Spring Web MVC 3.1 lub nowszego</span><span class="sxs-lookup"><span data-stu-id="36a1d-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="36a1d-179">Edycja tych elementów *-servlet.xml tooinclude hello usługi Application Insights pakietu:</span><span class="sxs-lookup"><span data-stu-id="36a1d-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="36a1d-180">Jeśli używasz środowiska Struts 2</span><span class="sxs-lookup"><span data-stu-id="36a1d-180">If you're using Struts 2</span></span>
<span data-ttu-id="36a1d-181">Dodaj ten element toohello poprzeczne plik konfiguracji (zazwyczaj nazwany struts.xml lub default.xml poprzeczne):</span><span class="sxs-lookup"><span data-stu-id="36a1d-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="36a1d-182">(Jeśli masz interceptory zdefiniowane w stosie domyślne interceptora powitania po prostu można dodać toothat stosu.)</span><span class="sxs-lookup"><span data-stu-id="36a1d-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="36a1d-183">5. Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="36a1d-183">5. Run your application</span></span>
<span data-ttu-id="36a1d-184">Uruchamiany w trybie debugowania na komputerze deweloperskim albo publikowanie tooyour server.</span><span class="sxs-lookup"><span data-stu-id="36a1d-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="36a1d-185">6. Wyświetlanie telemetrii w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="36a1d-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="36a1d-186">Zwraca tooyour zasobu usługi Application Insights w [portalu Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36a1d-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="36a1d-187">W bloku omówienie hello pojawi się dane żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="36a1d-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="36a1d-188">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="36a1d-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="36a1d-190">[Dowiedz się więcej o metrykach.][metrics]</span><span class="sxs-lookup"><span data-stu-id="36a1d-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="36a1d-191">Kliknij przycisk za pomocą dowolnego wykresu toosee bardziej szczegółowe agregowana metryki.</span><span class="sxs-lookup"><span data-stu-id="36a1d-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="36a1d-192">Usługi Application Insights zakłada hello format żądania HTTP dla aplikacji MVC: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="36a1d-193">Na przykład żądania `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` i `GET Home/Product/sdf96vws` są grupowane w ramach pozycji `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="36a1d-194">To grupowanie umożliwia zrozumiałe agregowanie żądań, na przykład podawanie liczby żądań i średniego czasu ich wykonania.</span><span class="sxs-lookup"><span data-stu-id="36a1d-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="36a1d-195">Dane wystąpienia</span><span class="sxs-lookup"><span data-stu-id="36a1d-195">Instance data</span></span>
<span data-ttu-id="36a1d-196">Kliknij określone żądanie wystąpień poszczególnych typów toosee.</span><span class="sxs-lookup"><span data-stu-id="36a1d-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="36a1d-197">W usłudze Application Insights są wyświetlane dwa rodzaje danych: dane zagregowane, przechowywane i wyświetlane jako średnie, liczniki i sumy, oraz dane wystąpienia — indywidualne raporty dotyczące żądań HTTP, wyjątków, wyświetleń stron lub zdarzeń niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="36a1d-198">Podczas przeglądania właściwości hello żądania, można przejrzeć zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="36a1d-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="36a1d-199">Analiza: zaawansowany język zapytań</span><span class="sxs-lookup"><span data-stu-id="36a1d-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="36a1d-200">Jak gromadzone większej ilości danych, można uruchomić zapytania zarówno tooaggregate danych i toofind poszczególnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="36a1d-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="36a1d-201">[Analiza](app-insights-analytics.md) jest zaawansowanym narzędziem, którego można używać zarówno w celu poznania wydajności i użycia, jak i do celów diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Przykład analizy](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="36a1d-203">7. Zainstaluj aplikację na powitania serwera</span><span class="sxs-lookup"><span data-stu-id="36a1d-203">7. Install your app on hello server</span></span>
<span data-ttu-id="36a1d-204">Teraz publikowania serwera toohello aplikacji znajduje się w innym użytkownikom go używać i obserwować telemetrii hello widoczne w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="36a1d-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="36a1d-205">Upewnij się, że zapora pozwala toosend Twojej aplikacji telemetrii toothese portów:</span><span class="sxs-lookup"><span data-stu-id="36a1d-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="36a1d-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="36a1d-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="36a1d-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="36a1d-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="36a1d-208">Jeśli ruch wychodzący ma być kierowany przez zaporę, zdefiniuj właściwości systemu `http.proxyHost` i `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="36a1d-209">Na serwerach systemu Windows zainstaluj:</span><span class="sxs-lookup"><span data-stu-id="36a1d-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="36a1d-210">Pakiet Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="36a1d-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="36a1d-211">Ten składnik umożliwia działanie liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="36a1d-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="36a1d-212">Wyjątki i błędy żądań</span><span class="sxs-lookup"><span data-stu-id="36a1d-212">Exceptions and request failures</span></span>
<span data-ttu-id="36a1d-213">Nieobsługiwane wyjątki są zbierane automatycznie:</span><span class="sxs-lookup"><span data-stu-id="36a1d-213">Unhandled exceptions are automatically collected:</span></span>

![Otwórz ustawienia, błędy](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="36a1d-215">toocollect danych na inne wyjątki, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="36a1d-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="36a1d-216">[Wstaw wywołuje tootrackException() w kodzie][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="36a1d-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="36a1d-217">[Zainstaluj hello agenta Java na serwerze](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="36a1d-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="36a1d-218">Można określić metody hello ma toowatch.</span><span class="sxs-lookup"><span data-stu-id="36a1d-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="36a1d-219">Monitorowanie wywołań metod i zależności zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="36a1d-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="36a1d-220">[Zainstaluj agenta Java hello](app-insights-java-agent.md) toolog określone metody wewnętrznej i wywołań za pośrednictwem JDBC, z danych o chronometrażu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="36a1d-221">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="36a1d-221">Performance counters</span></span>
<span data-ttu-id="36a1d-222">Otwórz **ustawienia**, **serwerów**, toosee zakresu liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="36a1d-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="36a1d-223">Dostosowywanie zbierania danych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="36a1d-223">Customize performance counter collection</span></span>
<span data-ttu-id="36a1d-224">Kolekcja toodisable hello standardowego zbioru liczników wydajności, Dodaj hello następującego kodu w węźle głównym hello hello ApplicationInsights.xml pliku:</span><span class="sxs-lookup"><span data-stu-id="36a1d-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="36a1d-225">Zbieranie danych dodatkowych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="36a1d-225">Collect additional performance counters</span></span>
<span data-ttu-id="36a1d-226">Można określić toobe liczniki wydajności zebrane.</span><span class="sxs-lookup"><span data-stu-id="36a1d-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="36a1d-227">Liczniki JMX (udostępnione przez hello maszyny wirtualnej Java)</span><span class="sxs-lookup"><span data-stu-id="36a1d-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="36a1d-228">`displayName`— Nazwa hello wyświetlana w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="36a1d-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="36a1d-229">`objectName`— Nazwa obiektu JMX hello.</span><span class="sxs-lookup"><span data-stu-id="36a1d-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="36a1d-230">`attribute`— Atrybut hello toofetch nazwa obiektu JMX hello</span><span class="sxs-lookup"><span data-stu-id="36a1d-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="36a1d-231">`type`(opcjonalnie) — Witaj typ atrybutu JMX obiektu:</span><span class="sxs-lookup"><span data-stu-id="36a1d-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="36a1d-232">wartość domyślna: typ prosty, np. int lub long.</span><span class="sxs-lookup"><span data-stu-id="36a1d-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="36a1d-233">`composite`: dane licznika wydajności hello jest w formacie hello "Attribute.Data"</span><span class="sxs-lookup"><span data-stu-id="36a1d-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="36a1d-234">`tabular`: dane licznika wydajności hello jest w formacie hello wiersza tabeli</span><span class="sxs-lookup"><span data-stu-id="36a1d-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="36a1d-235">Liczniki wydajności systemu Windows</span><span class="sxs-lookup"><span data-stu-id="36a1d-235">Windows performance counters</span></span>
<span data-ttu-id="36a1d-236">Każdy [licznika wydajności systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) jest członkiem grupy kategorii (w hello taki sam sposób, że pole jest elementem członkowskim klasy).</span><span class="sxs-lookup"><span data-stu-id="36a1d-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="36a1d-237">Kategorie mogą być globalne lub mogą mieć wystąpienia numerowane lub nazwane.</span><span class="sxs-lookup"><span data-stu-id="36a1d-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="36a1d-238">displayName — Witaj Nazwa wyświetlana w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="36a1d-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="36a1d-239">categoryName — Witaj kategorii licznika wydajności (obiekt wydajności) z którym skojarzony jest ten licznik wydajności.</span><span class="sxs-lookup"><span data-stu-id="36a1d-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="36a1d-240">counterName — nazwa hello hello licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36a1d-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="36a1d-241">instanceName — nazwa wystąpienia kategorii licznika wydajności hello hello lub ciąg pusty (""), jeśli kategoria hello zawiera jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="36a1d-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="36a1d-242">Jeśli hello CategoryName procesu i hello licznika wydajności, chcieliby toocollect znajduje się w bieżącym procesie JVM hello w uruchomionym aplikacji, określ `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="36a1d-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="36a1d-243">Liczniki wydajności są widoczne jako metryki niestandardowe w [Eksploratorze metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="36a1d-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="36a1d-244">Liczniki wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="36a1d-244">Unix performance counters</span></span>
* <span data-ttu-id="36a1d-245">[Instalowanie collectd przy użyciu wtyczki usługi Application Insights hello](app-insights-java-collectd.md) tooget szerokiego zakresu systemów i sieci danych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="36a1d-246">Pobieranie danych użytkownika i sesji</span><span class="sxs-lookup"><span data-stu-id="36a1d-246">Get user and session data</span></span>
<span data-ttu-id="36a1d-247">Wysyłasz już telemetrię z serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="36a1d-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="36a1d-248">Teraz tooget hello widok 360 stopni aplikacji, można dodać więcej monitorowania:</span><span class="sxs-lookup"><span data-stu-id="36a1d-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="36a1d-249">[Dodawanie stron sieci web tooyour telemetrii] [ usage] toomonitor strony widoki i metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36a1d-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="36a1d-250">[Ustawianie testów sieci web] [ availability] toomake się, że aplikacja pozostaje na żywo i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="36a1d-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="36a1d-251">Przechwytywanie danych dziennika śledzenia</span><span class="sxs-lookup"><span data-stu-id="36a1d-251">Capture log traces</span></span>
<span data-ttu-id="36a1d-252">Można użyć tooslice usługi Application Insights i wykorzystuj dzienniki z narzędzia Log4J, Logback lub innych platform rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="36a1d-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="36a1d-253">Dzienniki hello jest skorelowany z żądań HTTP i innych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="36a1d-254">[Dowiedz się, jak to zrobić][javalogs].</span><span class="sxs-lookup"><span data-stu-id="36a1d-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="36a1d-255">Wysyłanie własnej telemetrii</span><span class="sxs-lookup"><span data-stu-id="36a1d-255">Send your own telemetry</span></span>
<span data-ttu-id="36a1d-256">Teraz, po zainstalowaniu hello zestawu SDK, można użyć toosend interfejsu API hello własnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="36a1d-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="36a1d-257">[Śledzenie zdarzeń niestandardowych i metryki] [ api] toolearn, jakie użytkownicy wirtualni z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="36a1d-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="36a1d-258">[Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toohelp diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="36a1d-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="36a1d-259">Testy dostępności sieci Web</span><span class="sxs-lookup"><span data-stu-id="36a1d-259">Availability web tests</span></span>
<span data-ttu-id="36a1d-260">Usługa Application Insights można przetestować witryny sieci Web w toocheck w regularnych odstępach czasu, który jest, a także odpowiada.</span><span class="sxs-lookup"><span data-stu-id="36a1d-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="36a1d-261">[tooset się][availability], kliknij przycisk testy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="36a1d-261">[tooset up][availability], click Web tests.</span></span>

![Kliknij pozycję Testy sieci Web, a następnie kliknij pozycję Dodaj test sieci Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="36a1d-263">Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.</span><span class="sxs-lookup"><span data-stu-id="36a1d-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Przykład testu sieci Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="36a1d-265">[Dowiedz się więcej o testach dostępności sieci Web.][availability]</span><span class="sxs-lookup"><span data-stu-id="36a1d-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="36a1d-266">Pytania?</span><span class="sxs-lookup"><span data-stu-id="36a1d-266">Questions?</span></span> <span data-ttu-id="36a1d-267">Problemy?</span><span class="sxs-lookup"><span data-stu-id="36a1d-267">Problems?</span></span>
[<span data-ttu-id="36a1d-268">Rozwiązywanie problemów z technologią Java</span><span class="sxs-lookup"><span data-stu-id="36a1d-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="36a1d-269">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="36a1d-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="36a1d-270">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36a1d-270">Next steps</span></span>
* [<span data-ttu-id="36a1d-271">Monitorowanie wywołań zależności</span><span class="sxs-lookup"><span data-stu-id="36a1d-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="36a1d-272">Monitorowanie liczników wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="36a1d-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="36a1d-273">Dodaj [monitorowanie stron sieci web tooyour](app-insights-javascript.md) czas ładowania strony toomonitor, wywołania AJAX wyjątków przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="36a1d-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="36a1d-274">Zapis [telemetria niestandardowa](app-insights-api-custom-events-metrics.md) tootrack użycia w przeglądarce hello lub na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="36a1d-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="36a1d-275">Utwórz [pulpity nawigacyjne](app-insights-dashboards.md) toobring razem hello klucza wykresy do monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="36a1d-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="36a1d-276">Tworzenie zaawansowanych zapytań dotyczących telemetrii z poziomu aplikacji przy użyciu usługi [Analytics](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="36a1d-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="36a1d-277">Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="36a1d-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
