---
title: "Analiza aplikacji sieci Web w języku Java za pomocą usługi Application Insights | Microsoft Docs"
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
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="e0003-103">Wprowadzenie do usługi Application Insights w projekcie sieci Web w języku Java</span><span class="sxs-lookup"><span data-stu-id="e0003-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="e0003-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) jest rozszerzalną usługą analizy dla deweloperów sieci Web, która ułatwia zrozumienie wydajności i użycia aktywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0003-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="e0003-105">Służy do [wykrywania i diagnozowania problemów z wydajnością i wyjątków](app-insights-detect-triage-diagnose.md) oraz [pisania kodu][api] do śledzenia korzystania z aplikacji przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e0003-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="e0003-107">Usługa Application Insights obsługuje aplikacje w języku Java działające w systemach Linux, Unix lub Windows.</span><span class="sxs-lookup"><span data-stu-id="e0003-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="e0003-108">Potrzebne elementy:</span><span class="sxs-lookup"><span data-stu-id="e0003-108">You need:</span></span>

* <span data-ttu-id="e0003-109">Środowisko Oracle JRE 1.6 lub nowsze albo Zulu JRE 1.6 lub nowsze</span><span class="sxs-lookup"><span data-stu-id="e0003-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="e0003-110">Subskrypcja platformy [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e0003-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="e0003-111">*Jeśli masz aplikację sieci Web, która już działa, możesz wykonać alternatywną procedurę, aby [dodać zestaw SDK w czasie wykonywania na serwerze sieci Web](app-insights-java-live.md). Ta alternatywa pozwala uniknąć ponownego kompilowania kodu, ale nie udostępnia opcji pisania kodu w celu śledzenia działań użytkownika.*</span><span class="sxs-lookup"><span data-stu-id="e0003-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="e0003-112">1. Uzyskiwanie klucza instrumentacji usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0003-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="e0003-113">Zaloguj się do [Portalu Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0003-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e0003-114">Utwórz zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0003-114">Create an Application Insights resource.</span></span> <span data-ttu-id="e0003-115">Jako typ aplikacji ustaw wartość Aplikacja sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="e0003-115">Set the application type to Java web application.</span></span>

    ![Wypełnij nazwę, wybierz aplikację sieci Web Java i kliknij przycisk Utwórz](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="e0003-117">Znajdź klucz instrumentacji nowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="e0003-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="e0003-118">Wkrótce będzie trzeba wkleić ten klucz do projektu kodu.</span><span class="sxs-lookup"><span data-stu-id="e0003-118">You'll need to paste this key into your code project shortly.</span></span>

    ![W opisie nowego zasobu kliknij opcję Właściwości i skopiuj klucz instrumentacji](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="e0003-120">2. Dodawanie zestawu SDK usługi Application Insights dla środowiska Java do projektu</span><span class="sxs-lookup"><span data-stu-id="e0003-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="e0003-121">*Wybierz odpowiedni sposób dla danego projektu.*</span><span class="sxs-lookup"><span data-stu-id="e0003-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="e0003-122">Jeśli używasz środowiska Eclipse do tworzenia projektu Maven lub dynamicznego projektu sieci Web...</span><span class="sxs-lookup"><span data-stu-id="e0003-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="e0003-123">Użyj [wtyczki zestawu SDK Application Insights dla środowiska Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="e0003-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="e0003-124">Jeśli używasz narzędzia Maven...</span><span class="sxs-lookup"><span data-stu-id="e0003-124">If you're using Maven...</span></span>
<span data-ttu-id="e0003-125">Jeśli projekt jest już skonfigurowany do używania narzędzia Maven w celu kompilacji, scal następujący kod z plikiem pom.xml.</span><span class="sxs-lookup"><span data-stu-id="e0003-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="e0003-126">Następnie odśwież zależności projektu, aby pliki binarne zostały pobrane.</span><span class="sxs-lookup"><span data-stu-id="e0003-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

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

* <span data-ttu-id="e0003-127">*Błędy kompilacji lub walidacji sumy kontrolnej?*</span><span class="sxs-lookup"><span data-stu-id="e0003-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="e0003-128">Spróbuj użyć określonej wersji, np.: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="e0003-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="e0003-129">Najbardziej aktualną wersję z najdziesz w [informacjach o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) lub wśród naszych [artefaktów Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="e0003-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="e0003-130">*Trzeba zaktualizować zestaw SDK?*</span><span class="sxs-lookup"><span data-stu-id="e0003-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="e0003-131">Odśwież zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="e0003-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="e0003-132">Jeśli używasz narzędzia Gradle...</span><span class="sxs-lookup"><span data-stu-id="e0003-132">If you're using Gradle...</span></span>
<span data-ttu-id="e0003-133">Jeśli projekt jest już skonfigurowany do używania narzędzia Gradle w celu kompilacji, scal następujący kod z plikiem build.gradle.</span><span class="sxs-lookup"><span data-stu-id="e0003-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="e0003-134">Następnie odśwież zależności projektu, aby pliki binarne zostały pobrane.</span><span class="sxs-lookup"><span data-stu-id="e0003-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="e0003-135">*Błędy kompilacji lub walidacji sumy kontrolnej? Spróbuj użyć określonej wersji, np.:* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="e0003-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="e0003-136">*Najbardziej aktualną wersję znajdziesz w [informacjach o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="e0003-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="e0003-137">*Aby zaktualizować zestaw SDK*</span><span class="sxs-lookup"><span data-stu-id="e0003-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="e0003-138">Odśwież zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="e0003-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="e0003-139">W innym przypadku...</span><span class="sxs-lookup"><span data-stu-id="e0003-139">Otherwise ...</span></span>
<span data-ttu-id="e0003-140">Ręcznie dodaj zestaw SDK:</span><span class="sxs-lookup"><span data-stu-id="e0003-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="e0003-141">Pobierz [Zestaw SDK usługi Application Insights dla środowiska Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="e0003-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="e0003-142">Wyodrębnij pliki binarne z pliku zip i dodaj je do projektu.</span><span class="sxs-lookup"><span data-stu-id="e0003-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="e0003-143">Pytania...</span><span class="sxs-lookup"><span data-stu-id="e0003-143">Questions...</span></span>
* <span data-ttu-id="e0003-144">*Jaki jest związek między składnikami `-core` i `-web` w pliku zip?*</span><span class="sxs-lookup"><span data-stu-id="e0003-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="e0003-145">Element `applicationinsights-core` dostarcza podstawowy interfejs API.</span><span class="sxs-lookup"><span data-stu-id="e0003-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="e0003-146">Ten składnik jest zawsze potrzebny.</span><span class="sxs-lookup"><span data-stu-id="e0003-146">You always need this component.</span></span>
  * <span data-ttu-id="e0003-147">Element `applicationinsights-web` dostarcza metryki do śledzenia liczby żądań HTTP i czasów odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e0003-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="e0003-148">Możesz pominąć ten składnik, jeśli nie chcesz automatycznie zbierać tych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="e0003-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="e0003-149">Na przykład jeśli chcesz zaprogramować zbieranie samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="e0003-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="e0003-150">*Aby zaktualizować zestaw SDK po opublikowaniu zmian*</span><span class="sxs-lookup"><span data-stu-id="e0003-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="e0003-151">Pobierz najnowszy [Zestaw SDK usługi Application Insights dla środowiska Java](https://aka.ms/qqkaq6) i zastąp nim stary.</span><span class="sxs-lookup"><span data-stu-id="e0003-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="e0003-152">Zmiany są opisane w [informacjach o wersji zestawu SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="e0003-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="e0003-153">3. Dodawanie pliku .xml usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0003-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="e0003-154">Dodaj plik ApplicationInsights.xml do folderu zasobów w projekcie lub upewnij się, że jest dodany do ścieżki klas wdrażania projektu.</span><span class="sxs-lookup"><span data-stu-id="e0003-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="e0003-155">Skopiuj do niego następujący kod XML.</span><span class="sxs-lookup"><span data-stu-id="e0003-155">Copy the following XML into it.</span></span>

<span data-ttu-id="e0003-156">Zastąp klucz instrumentacji kluczem pobranym z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0003-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="e0003-157">Klucz instrumentacji jest wysyłany wraz z każdym elementem telemetrii i dzięki temu te elementy mogą być wyświetlane dla odpowiedniego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0003-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="e0003-158">Składnik żądań HTTP jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e0003-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="e0003-159">Powoduje automatyczne wysyłanie telemetrii dotyczącej żądań i czasów odpowiedzi do portalu.</span><span class="sxs-lookup"><span data-stu-id="e0003-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="e0003-160">Korelacja zdarzeń jest dodatkiem do składnika żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0003-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="e0003-161">Przypisuje identyfikator do każdego żądania odebranego przez serwer i dodaje go do każdego elementu telemetrii jako właściwość „Operation.Id”.</span><span class="sxs-lookup"><span data-stu-id="e0003-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="e0003-162">Umożliwia korelowanie telemetrii skojarzonej z każdym żądaniem przez ustawienie filtru w [wyszukiwaniu diagnostycznym][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e0003-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="e0003-163">Klucz usługi Application Insights może zostać przekazany dynamicznie z witryny Azure Portal jako właściwość systemu (-DAPPLICATION_INSIGHTS_IKEY=Twój_klucz_ikey).</span><span class="sxs-lookup"><span data-stu-id="e0003-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="e0003-164">Jeśli nie zdefiniowano żadnej właściwości, sprawdzana jest zmienna środowiskowa (APPLICATION_INSIGHTS_IKEY) w ustawieniach aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0003-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="e0003-165">Jeśli obie właściwości nie są zdefiniowane, używana jest domyślna właściwość InstrumentationKey z pliku ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="e0003-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="e0003-166">Ta sekwencja ułatwia dynamiczne zarządzanie elementami InstrumentationKey dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="e0003-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="e0003-167">Alternatywne sposoby ustawienia klucza instrumentacji</span><span class="sxs-lookup"><span data-stu-id="e0003-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="e0003-168">Zestaw SDK usługi Application Insights szuka klucza w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="e0003-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="e0003-169">Właściwość systemu: -DAPPLICATION_INSIGHTS_IKEY=Twój_klucz_ikey</span><span class="sxs-lookup"><span data-stu-id="e0003-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="e0003-170">Zmienna środowiskowa: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="e0003-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="e0003-171">Plik konfiguracji: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="e0003-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="e0003-172">Możesz również [ustawić klucz w kodzie](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="e0003-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="e0003-173">4. Dodawanie filtru HTTP</span><span class="sxs-lookup"><span data-stu-id="e0003-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="e0003-174">Ostatni krok konfiguracji umożliwia składnikowi żądania HTTP rejestrowanie wszystkich żądań sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e0003-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="e0003-175">(Nie jest to wymagane, jeśli potrzebujesz tylko podstawowego interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="e0003-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="e0003-176">Znajdź i otwórz plik web.xml w projekcie, a następnie scal poniższy kod w obszarze węzła web-app, w którym skonfigurowano filtry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0003-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="e0003-177">Aby uzyskać najbardziej dokładne wyniki, ten filtr powinien być mapowany przed wszystkimi innymi filtrami.</span><span class="sxs-lookup"><span data-stu-id="e0003-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="e0003-178">Jeśli używasz środowiska Spring Web MVC 3.1 lub nowszego</span><span class="sxs-lookup"><span data-stu-id="e0003-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="e0003-179">Edytuj te elementy w pliku *-servlet.xml, aby uwzględnić pakiet usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="e0003-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="e0003-180">Jeśli używasz środowiska Struts 2</span><span class="sxs-lookup"><span data-stu-id="e0003-180">If you're using Struts 2</span></span>
<span data-ttu-id="e0003-181">Dodaj ten element do pliku konfiguracyjnego Struts (zwykle o nazwie struts.xml lub struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="e0003-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="e0003-182">(Jeśli masz interceptory zdefiniowane w stosie domyślnym, możesz po prostu dodać interceptor do tego stosu).</span><span class="sxs-lookup"><span data-stu-id="e0003-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="e0003-183">5. Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e0003-183">5. Run your application</span></span>
<span data-ttu-id="e0003-184">Uruchom aplikację w trybie debugowania na komputerze deweloperskim albo opublikuj na serwerze.</span><span class="sxs-lookup"><span data-stu-id="e0003-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="e0003-185">6. Wyświetlanie telemetrii w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0003-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="e0003-186">Wróć do zasobu usługi Application Insights w witrynie [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0003-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e0003-187">W bloku przeglądu zostaną wyświetlone dane żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0003-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="e0003-188">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="e0003-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dane przykładowe](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="e0003-190">[Dowiedz się więcej o metrykach.][metrics]</span><span class="sxs-lookup"><span data-stu-id="e0003-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="e0003-191">Klikaj elementy wykresów, aby wyświetlać bardziej szczegółowe metryki zagregowane.</span><span class="sxs-lookup"><span data-stu-id="e0003-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="e0003-192">Usługa Application Insights zakłada, że format żądania HTTP dla aplikacji MVC to: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="e0003-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="e0003-193">Na przykład żądania `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` i `GET Home/Product/sdf96vws` są grupowane w ramach pozycji `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="e0003-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="e0003-194">To grupowanie umożliwia zrozumiałe agregowanie żądań, na przykład podawanie liczby żądań i średniego czasu ich wykonania.</span><span class="sxs-lookup"><span data-stu-id="e0003-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="e0003-195">Dane wystąpienia</span><span class="sxs-lookup"><span data-stu-id="e0003-195">Instance data</span></span>
<span data-ttu-id="e0003-196">Kliknij określony typ żądania, aby wyświetlić poszczególne wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e0003-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="e0003-197">W usłudze Application Insights są wyświetlane dwa rodzaje danych: dane zagregowane, przechowywane i wyświetlane jako średnie, liczniki i sumy, oraz dane wystąpienia — indywidualne raporty dotyczące żądań HTTP, wyjątków, wyświetleń stron lub zdarzeń niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e0003-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="e0003-198">Podczas wyświetlania właściwości żądania można wyświetlić skojarzone zdarzenia telemetrii, takie jak żądania i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="e0003-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="e0003-199">Analiza: zaawansowany język zapytań</span><span class="sxs-lookup"><span data-stu-id="e0003-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="e0003-200">W miarę zgromadzenia większej ilości danych można uruchamiać zapytania zarówno w celu agregowania danych, jak i w celu znajdowania poszczególnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="e0003-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="e0003-201">[Analiza](app-insights-analytics.md) jest zaawansowanym narzędziem, którego można używać zarówno w celu poznania wydajności i użycia, jak i do celów diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="e0003-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Przykład analizy](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="e0003-203">7. Instalowanie aplikacji na serwerze</span><span class="sxs-lookup"><span data-stu-id="e0003-203">7. Install your app on the server</span></span>
<span data-ttu-id="e0003-204">Teraz opublikuj aplikację na serwerze, pozwól z niej korzystać innym osobom, a następnie obejrzyj telemetrię wyświetlaną w portalu.</span><span class="sxs-lookup"><span data-stu-id="e0003-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="e0003-205">Upewnij się, że zapora pozwala aplikacji na wysłanie telemetrii do tych portów:</span><span class="sxs-lookup"><span data-stu-id="e0003-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="e0003-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e0003-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e0003-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e0003-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="e0003-208">Jeśli ruch wychodzący ma być kierowany przez zaporę, zdefiniuj właściwości systemu `http.proxyHost` i `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="e0003-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="e0003-209">Na serwerach systemu Windows zainstaluj:</span><span class="sxs-lookup"><span data-stu-id="e0003-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="e0003-210">Pakiet Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="e0003-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="e0003-211">Ten składnik umożliwia działanie liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="e0003-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="e0003-212">Wyjątki i błędy żądań</span><span class="sxs-lookup"><span data-stu-id="e0003-212">Exceptions and request failures</span></span>
<span data-ttu-id="e0003-213">Nieobsługiwane wyjątki są zbierane automatycznie:</span><span class="sxs-lookup"><span data-stu-id="e0003-213">Unhandled exceptions are automatically collected:</span></span>

![Otwórz ustawienia, błędy](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="e0003-215">Istnieją dwie opcje zbierania danych o innych wyjątkach:</span><span class="sxs-lookup"><span data-stu-id="e0003-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="e0003-216">[Wstawianie wywołań metody trackException() w kodzie][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="e0003-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="e0003-217">[Instalacja agenta Java na serwerze](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="e0003-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="e0003-218">Trzeba określić metody, które chcesz śledzić.</span><span class="sxs-lookup"><span data-stu-id="e0003-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="e0003-219">Monitorowanie wywołań metod i zależności zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="e0003-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="e0003-220">[Zainstaluj agenta programu Java](app-insights-java-agent.md) w celu rejestrowania określonych metod wewnętrznych i wywołań za pośrednictwem JDBC z danymi chronometrażu.</span><span class="sxs-lookup"><span data-stu-id="e0003-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="e0003-221">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="e0003-221">Performance counters</span></span>
<span data-ttu-id="e0003-222">Otwórz pozycję **Ustawienia**, **Serwery**, aby wyświetlić zakres liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="e0003-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="e0003-223">Dostosowywanie zbierania danych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="e0003-223">Customize performance counter collection</span></span>
<span data-ttu-id="e0003-224">Aby wyłączyć zbieranie standardowego zestawu liczników wydajności, dodaj następujący kod w węźle głównym pliku ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="e0003-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="e0003-225">Zbieranie danych dodatkowych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="e0003-225">Collect additional performance counters</span></span>
<span data-ttu-id="e0003-226">Możesz określić dodatkowe liczniki wydajności do zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="e0003-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="e0003-227">Liczniki JMX (udostępniane przez maszynę wirtualną Java)</span><span class="sxs-lookup"><span data-stu-id="e0003-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="e0003-228">`displayName` — nazwa wyświetlana w portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0003-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e0003-229">`objectName` — nazwa obiektu JMX.</span><span class="sxs-lookup"><span data-stu-id="e0003-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="e0003-230">`attribute` — atrybut nazwy obiektu JMX do pobrania.</span><span class="sxs-lookup"><span data-stu-id="e0003-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="e0003-231">`type` (opcjonalnie) — typ atrybutu obiektu JMX:</span><span class="sxs-lookup"><span data-stu-id="e0003-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="e0003-232">wartość domyślna: typ prosty, np. int lub long.</span><span class="sxs-lookup"><span data-stu-id="e0003-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="e0003-233">`composite`: dane licznika wydajności są w formacie „Atrybut.Dane”</span><span class="sxs-lookup"><span data-stu-id="e0003-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="e0003-234">`tabular`: dane licznika wydajności są w formacie wiersza tabeli</span><span class="sxs-lookup"><span data-stu-id="e0003-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="e0003-235">Liczniki wydajności systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e0003-235">Windows performance counters</span></span>
<span data-ttu-id="e0003-236">Każdy [licznik wydajności systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) należy do kategorii (w taki sam sposób, w jaki pole należy do klasy).</span><span class="sxs-lookup"><span data-stu-id="e0003-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="e0003-237">Kategorie mogą być globalne lub mogą mieć wystąpienia numerowane lub nazwane.</span><span class="sxs-lookup"><span data-stu-id="e0003-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="e0003-238">displayName — nazwa wyświetlana w portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0003-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e0003-239">categoryName — kategoria licznika wydajności (obiekt wydajności), z którą skojarzony jest ten licznik wydajności.</span><span class="sxs-lookup"><span data-stu-id="e0003-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="e0003-240">counterName — nazwa licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="e0003-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="e0003-241">instanceName — nazwa wystąpienia kategorii licznika wydajności lub ciąg pusty (""), jeśli kategoria zawiera jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="e0003-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="e0003-242">Jeśli categoryName to Proces, a licznik wydajności, którego dane chcesz zbierać, pochodzi z bieżącego procesu maszyny JVM, na której jest uruchomiona aplikacja, podaj wartość `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="e0003-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="e0003-243">Liczniki wydajności są widoczne jako metryki niestandardowe w [Eksploratorze metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="e0003-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="e0003-244">Liczniki wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="e0003-244">Unix performance counters</span></span>
* <span data-ttu-id="e0003-245">[Zainstaluj program collectd z wtyczką Application Insights](app-insights-java-collectd.md), aby uzyskać szeroką gamę danych na temat systemu i sieci.</span><span class="sxs-lookup"><span data-stu-id="e0003-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="e0003-246">Pobieranie danych użytkownika i sesji</span><span class="sxs-lookup"><span data-stu-id="e0003-246">Get user and session data</span></span>
<span data-ttu-id="e0003-247">Wysyłasz już telemetrię z serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e0003-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="e0003-248">Teraz, aby zyskać pełny wgląd w dane aplikacji, możesz dodać więcej opcji monitorowania:</span><span class="sxs-lookup"><span data-stu-id="e0003-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="e0003-249">[Dodaj telemetrię do stron sieci Web][usage], aby monitorować wyświetlenia stron i metryki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e0003-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="e0003-250">[Konfigurowanie testów sieci Web][availability], aby upewnić się, że aplikacja stale działa i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="e0003-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="e0003-251">Przechwytywanie danych dziennika śledzenia</span><span class="sxs-lookup"><span data-stu-id="e0003-251">Capture log traces</span></span>
<span data-ttu-id="e0003-252">Usługi Application Insights mogą służyć do analizowania pod różnymi kątami danych z dzienników Log4J, Logback lub innych platform rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e0003-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="e0003-253">Dzienniki można skorelować z żądaniami HTTP i inną telemetrią.</span><span class="sxs-lookup"><span data-stu-id="e0003-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="e0003-254">[Dowiedz się, jak to zrobić][javalogs].</span><span class="sxs-lookup"><span data-stu-id="e0003-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="e0003-255">Wysyłanie własnej telemetrii</span><span class="sxs-lookup"><span data-stu-id="e0003-255">Send your own telemetry</span></span>
<span data-ttu-id="e0003-256">Teraz, po zainstalowaniu zestawu SDK, możesz użyć interfejsu API do wysyłania własnej telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0003-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="e0003-257">[Śledź niestandardowe zdarzenia i metryki][api], aby dowiedzieć się, jak użytkownicy korzystają z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0003-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="e0003-258">[Wyszukiwanie zdarzeń i dzienników][diagnostic], aby łatwiej diagnozować problemy.</span><span class="sxs-lookup"><span data-stu-id="e0003-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="e0003-259">Testy dostępności sieci Web</span><span class="sxs-lookup"><span data-stu-id="e0003-259">Availability web tests</span></span>
<span data-ttu-id="e0003-260">Usługa Application Insights może służyć do testowania witryny sieci Web w regularnych odstępach czasu, aby sprawdzić, czy witryna działa i odpowiada poprawnie.</span><span class="sxs-lookup"><span data-stu-id="e0003-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="e0003-261">[Aby skonfigurować tę funkcję][availability], kliknij pozycję Testy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e0003-261">[To set up][availability], click Web tests.</span></span>

![Kliknij pozycję Testy sieci Web, a następnie kliknij pozycję Dodaj test sieci Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="e0003-263">Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.</span><span class="sxs-lookup"><span data-stu-id="e0003-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Przykład testu sieci Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="e0003-265">[Dowiedz się więcej o testach dostępności sieci Web.][availability]</span><span class="sxs-lookup"><span data-stu-id="e0003-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="e0003-266">Pytania?</span><span class="sxs-lookup"><span data-stu-id="e0003-266">Questions?</span></span> <span data-ttu-id="e0003-267">Problemy?</span><span class="sxs-lookup"><span data-stu-id="e0003-267">Problems?</span></span>
[<span data-ttu-id="e0003-268">Rozwiązywanie problemów z technologią Java</span><span class="sxs-lookup"><span data-stu-id="e0003-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="e0003-269">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="e0003-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e0003-270">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0003-270">Next steps</span></span>
* [<span data-ttu-id="e0003-271">Monitorowanie wywołań zależności</span><span class="sxs-lookup"><span data-stu-id="e0003-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="e0003-272">Monitorowanie liczników wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="e0003-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="e0003-273">Dodawanie [monitorowania do stron sieci Web](app-insights-javascript.md) w celu monitorowania czasów ładowania stron, wywołań AJAX i wyjątków przeglądarki</span><span class="sxs-lookup"><span data-stu-id="e0003-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="e0003-274">Zapisywanie [niestandardowych danych telemetrycznych](app-insights-api-custom-events-metrics.md) w celu śledzenia użycia w przeglądarce lub na serwerze.</span><span class="sxs-lookup"><span data-stu-id="e0003-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="e0003-275">Tworzenie [pulpitów nawigacyjnych](app-insights-dashboards.md) umożliwiających przygotowywanie kluczowych wykresów na potrzeby monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="e0003-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="e0003-276">Tworzenie zaawansowanych zapytań dotyczących telemetrii z poziomu aplikacji przy użyciu usługi [Analytics](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="e0003-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="e0003-277">Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="e0003-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
