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
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="36077-103">Wprowadzenie do usługi Application Insights z językiem Java w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="36077-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="36077-104">Hello zestaw SDK usługi Application Insights wysyła dane telemetryczne z aplikacji sieci web w języku Java, dzięki czemu można analizować użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="36077-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="36077-105">tak, aby pobrać poza hello pole telemetrii, a także interfejsu API służy telemetria niestandardowa toowrite Hello Eclipse wtyczki dla usługi Application Insights automatycznie instaluje program hello zestawu SDK w projekcie.</span><span class="sxs-lookup"><span data-stu-id="36077-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="36077-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36077-106">Prerequisites</span></span>
<span data-ttu-id="36077-107">Obecnie hello wtyczki działa w przypadku Maven projektów i dynamicznych projekty sieci Web w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="36077-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="36077-108">([Dodaj usługę Application Insights tooother typy projektów języka Java][java].)</span><span class="sxs-lookup"><span data-stu-id="36077-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="36077-109">Będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="36077-109">You'll need:</span></span>

* <span data-ttu-id="36077-110">Oracle środowiska JRE wersji 1.6 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="36077-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="36077-111">Subskrypcja zbyt[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="36077-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="36077-112">[Zaćmienie-IDE for Java EE Developers](http://www.eclipse.org/downloads/), indygo lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="36077-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="36077-113">System Windows 7 lub nowszym lub Windows Server 2008 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="36077-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="36077-114">Zainstaluj hello zestawu SDK w środowisku Eclipse (jeden raz)</span><span class="sxs-lookup"><span data-stu-id="36077-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="36077-115">Masz tylko toodo to jeden raz w każdym komputerze.</span><span class="sxs-lookup"><span data-stu-id="36077-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="36077-116">Ta czynność powoduje zainstalowanie zestawu narzędzi, które można następnie dodać hello SDK tooeach dynamiczny projekt sieci Web.</span><span class="sxs-lookup"><span data-stu-id="36077-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="36077-117">W programie Eclipse kliknij przycisk Pomoc, instalowanie nowego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="36077-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Pomoc, należy zainstalować nowe oprogramowanie](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="36077-119">Hello zestawu SDK jest http://dl.microsoft.com/eclipse, w obszarze zestawu narzędzi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36077-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="36077-120">Usuń zaznaczenie pola wyboru **skontaktuj się z wszystkich witryn aktualizacji...**</span><span class="sxs-lookup"><span data-stu-id="36077-120">Uncheck **Contact all update sites...**</span></span>

    ![Dla zestawu SDK usługi Application Insights wyczyść skontaktuj się z wszystkich witryn aktualizacji](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="36077-122">Wykonaj pozostałe kroki dla każdego projektu języka Java hello.</span><span class="sxs-lookup"><span data-stu-id="36077-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="36077-123">Tworzenie zasobu usługi Application Insights na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="36077-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="36077-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36077-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="36077-125">Utwórz nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36077-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="36077-126">Ustaw aplikację sieci web tooJava typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="36077-126">Set hello application type tooJava web application.</span></span>  

    ![Kliknij + i wybierz opcję Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="36077-128">Znajdź klucz Instrumentacji hello hello nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="36077-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="36077-129">Będzie on potrzebny toopaste w projekcie kodu wkrótce.</span><span class="sxs-lookup"><span data-stu-id="36077-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="36077-131">Dodawanie usługi Application Insights tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="36077-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="36077-132">Dodawanie usługi Application Insights z menu kontekstowego hello projektu sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="36077-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="36077-134">Wklej klucza Instrumentacji hello pochodzący z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36077-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![W obszarze Przegląd nowych zasobów powitania kliknij polecenie Właściwości i skopiuj hello klucza Instrumentacji](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="36077-136">klucz Hello przesyłany wraz każdy element telemetrii i informuje toodisplay usługi Application Insights w zasobie.</span><span class="sxs-lookup"><span data-stu-id="36077-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="36077-137">Uruchamianie aplikacji hello i widzieć metryki</span><span class="sxs-lookup"><span data-stu-id="36077-137">Run hello application and see metrics</span></span>
<span data-ttu-id="36077-138">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="36077-138">Run your application.</span></span>

<span data-ttu-id="36077-139">Zwraca tooyour zasobu usługi Application Insights w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="36077-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="36077-140">Dane żądań HTTP będą wyświetlane na powitania omówienie bloku.</span><span class="sxs-lookup"><span data-stu-id="36077-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="36077-141">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="36077-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="36077-142">Odpowiedź serwera, liczby żądań i błędów</span><span class="sxs-lookup"><span data-stu-id="36077-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="36077-143">Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki.</span><span class="sxs-lookup"><span data-stu-id="36077-143">Click through any chart toosee more detailed metrics.</span></span>

![Liczba żądań według nazwy](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="36077-145">[Dowiedz się więcej o metrykach.][metrics]</span><span class="sxs-lookup"><span data-stu-id="36077-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="36077-146">Podczas przeglądania właściwości hello żądania, może uzyskać zdarzenia telemetrii hello skojarzonych z nim, takich jak żądania i wyjątków i.</span><span class="sxs-lookup"><span data-stu-id="36077-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Wszystkie ślady dla tego żądania](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="36077-148">Dane telemetryczne po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="36077-148">Client-side telemetry</span></span>
<span data-ttu-id="36077-149">W bloku Szybki Start hello kliknij przycisk Pobierz toomonitor kod stron sieci web:</span><span class="sxs-lookup"><span data-stu-id="36077-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![W bloku Omówienie aplikacji wybierz pozycję Szybki Start, Pobierz kod toomonitor stron sieci web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="36077-152">Wstaw hello fragment kodu w hello head pliki HTML.</span><span class="sxs-lookup"><span data-stu-id="36077-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="36077-153">Wyświetlanie danych po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="36077-153">View client-side data</span></span>
<span data-ttu-id="36077-154">Otwórz zaktualizowane stron sieci web i używać ich.</span><span class="sxs-lookup"><span data-stu-id="36077-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="36077-155">Zaczekaj minutę lub dwie, a następnie zwraca tooApplication Insights i otwórz hello użycia bloku.</span><span class="sxs-lookup"><span data-stu-id="36077-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="36077-156">(Za pomocą bloku omówienie hello, przewiń w dół i kliknij opcję użycia).</span><span class="sxs-lookup"><span data-stu-id="36077-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="36077-157">Strona widoku, użytkownika i sesji metryki pojawią się na blok wykorzystanie hello:</span><span class="sxs-lookup"><span data-stu-id="36077-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sesje, użytkowników i wyświetleń strony](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="36077-159">[Dowiedz się więcej o konfigurowaniu telemetrii po stronie klienta.][usage]</span><span class="sxs-lookup"><span data-stu-id="36077-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="36077-160">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="36077-160">Publish your application</span></span>
<span data-ttu-id="36077-161">Teraz publikowania serwera toohello aplikacji znajduje się w innym użytkownikom go używać i obserwować telemetrii hello widoczne w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="36077-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="36077-162">Upewnij się, że zapora pozwala toosend Twojej aplikacji telemetrii toothese portów:</span><span class="sxs-lookup"><span data-stu-id="36077-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="36077-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="36077-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="36077-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="36077-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="36077-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="36077-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="36077-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="36077-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="36077-167">Na serwerach systemu Windows zainstaluj:</span><span class="sxs-lookup"><span data-stu-id="36077-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="36077-168">Pakiet Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="36077-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="36077-169">(Umożliwi to działanie liczników wydajności).</span><span class="sxs-lookup"><span data-stu-id="36077-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="36077-170">Wyjątki i błędy żądań</span><span class="sxs-lookup"><span data-stu-id="36077-170">Exceptions and request failures</span></span>
<span data-ttu-id="36077-171">Nieobsługiwane wyjątki są zbierane automatycznie:</span><span class="sxs-lookup"><span data-stu-id="36077-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="36077-172">toocollect danych na inne wyjątki, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="36077-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="36077-173">[Wstaw wywołuje tooTrackException w kodzie](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="36077-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="36077-174">[Zainstaluj hello agenta Java na serwerze](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="36077-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="36077-175">Można określić metody hello ma toowatch.</span><span class="sxs-lookup"><span data-stu-id="36077-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="36077-176">Monitorowanie wywołań metod i zależności zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="36077-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="36077-177">[Zainstaluj agenta Java hello](app-insights-java-agent.md) toolog określone metody wewnętrznej i wywołań za pośrednictwem JDBC, z danych o chronometrażu.</span><span class="sxs-lookup"><span data-stu-id="36077-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="36077-178">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="36077-178">Performance counters</span></span>
<span data-ttu-id="36077-179">W bloku Przegląd, przewiń w dół i kliknij przycisk hello **serwerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="36077-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="36077-180">Zobaczysz zakresu liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="36077-180">You'll see a range of performance counters.</span></span>

![Przewiń w dół tooclick hello serwerów kafelka](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="36077-182">Dostosowywanie zbierania danych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="36077-182">Customize performance counter collection</span></span>
<span data-ttu-id="36077-183">Kolekcja toodisable hello standardowego zbioru liczników wydajności, Dodaj hello następującego kodu w węźle głównym hello hello ApplicationInsights.xml pliku:</span><span class="sxs-lookup"><span data-stu-id="36077-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="36077-184">Zbieranie danych dodatkowych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="36077-184">Collect additional performance counters</span></span>
<span data-ttu-id="36077-185">Można określić toobe liczniki wydajności zebrane.</span><span class="sxs-lookup"><span data-stu-id="36077-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="36077-186">Liczniki JMX (udostępnione przez hello maszyny wirtualnej Java)</span><span class="sxs-lookup"><span data-stu-id="36077-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="36077-187">`displayName`— Nazwa hello wyświetlana w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="36077-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="36077-188">`objectName`— Nazwa obiektu JMX hello.</span><span class="sxs-lookup"><span data-stu-id="36077-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="36077-189">`attribute`— Atrybut hello toofetch nazwa obiektu JMX hello</span><span class="sxs-lookup"><span data-stu-id="36077-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="36077-190">`type`(opcjonalnie) — Witaj typ atrybutu JMX obiektu:</span><span class="sxs-lookup"><span data-stu-id="36077-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="36077-191">wartość domyślna: typ prosty, np. int lub long.</span><span class="sxs-lookup"><span data-stu-id="36077-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="36077-192">`composite`: dane licznika wydajności hello jest w formacie hello "Attribute.Data"</span><span class="sxs-lookup"><span data-stu-id="36077-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="36077-193">`tabular`: dane licznika wydajności hello jest w formacie hello wiersza tabeli</span><span class="sxs-lookup"><span data-stu-id="36077-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="36077-194">Liczniki wydajności systemu Windows</span><span class="sxs-lookup"><span data-stu-id="36077-194">Windows performance counters</span></span>
<span data-ttu-id="36077-195">Każdy [licznika wydajności systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) jest członkiem grupy kategorii (w hello taki sam sposób, że pole jest elementem członkowskim klasy).</span><span class="sxs-lookup"><span data-stu-id="36077-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="36077-196">Kategorie mogą być globalne lub mogą mieć wystąpienia numerowane lub nazwane.</span><span class="sxs-lookup"><span data-stu-id="36077-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="36077-197">displayName — Witaj Nazwa wyświetlana w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="36077-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="36077-198">categoryName — Witaj kategorii licznika wydajności (obiekt wydajności) z którym skojarzony jest ten licznik wydajności.</span><span class="sxs-lookup"><span data-stu-id="36077-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="36077-199">counterName — nazwa hello hello licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36077-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="36077-200">instanceName — nazwa wystąpienia kategorii licznika wydajności hello hello lub ciąg pusty (""), jeśli kategoria hello zawiera jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="36077-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="36077-201">Jeśli hello CategoryName procesu i hello licznika wydajności, chcieliby toocollect znajduje się w bieżącym procesie JVM hello w uruchomionym aplikacji, określ `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="36077-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="36077-202">Liczniki wydajności są widoczne jako metryki niestandardowe w [Eksploratorze metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="36077-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="36077-203">Liczniki wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="36077-203">Unix performance counters</span></span>
* <span data-ttu-id="36077-204">[Instalowanie collectd przy użyciu wtyczki usługi Application Insights hello](app-insights-java-collectd.md) tooget szerokiego zakresu systemów i sieci danych.</span><span class="sxs-lookup"><span data-stu-id="36077-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="36077-205">Testy dostępności sieci Web</span><span class="sxs-lookup"><span data-stu-id="36077-205">Availability web tests</span></span>
<span data-ttu-id="36077-206">Usługa Application Insights można przetestować witryny sieci Web w toocheck w regularnych odstępach czasu, który jest, a także odpowiada.</span><span class="sxs-lookup"><span data-stu-id="36077-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="36077-207">[tooset się][availability], przewiń w dół tooclick dostępności.</span><span class="sxs-lookup"><span data-stu-id="36077-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Przewiń w dół, kliknij opcję Dostępność, a następnie opcję Dodaj test sieci Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="36077-209">Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.</span><span class="sxs-lookup"><span data-stu-id="36077-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Przykład testu sieci Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="36077-211">[Dowiedz się więcej o testach dostępności sieci Web.][availability]</span><span class="sxs-lookup"><span data-stu-id="36077-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="36077-212">Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="36077-212">Diagnostic logs</span></span>
<span data-ttu-id="36077-213">Jeśli używasz Logback lub Log4J (1.2 lub 2.0) śledzenia, program może automatycznie wysyłane szczegółowe informacje, których można eksplorować i ich wyszukiwanie tooApplication dzienników śledzenia.</span><span class="sxs-lookup"><span data-stu-id="36077-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="36077-214">[Dowiedz się więcej o dzienników diagnostycznych][javalogs]</span><span class="sxs-lookup"><span data-stu-id="36077-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="36077-215">Telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="36077-215">Custom telemetry</span></span>
<span data-ttu-id="36077-216">Wstaw kilku wierszy kodu w toofind aplikacji sieci web Java, tak się, co robią użytkownicy z nim lub toohelp diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="36077-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="36077-217">Strony sieci web JavaScript oraz powitania po stronie serwera w języku Java można wstawić kodu.</span><span class="sxs-lookup"><span data-stu-id="36077-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="36077-218">[Dowiedz się więcej o telemetrii niestandardowej][track]</span><span class="sxs-lookup"><span data-stu-id="36077-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="36077-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36077-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="36077-220">Wykrywanie i diagnozowanie problemów</span><span class="sxs-lookup"><span data-stu-id="36077-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="36077-221">[Dodaj telemetrię usługi sieci web klienta] [ usage] tooget telemetrii wydajności z powitania klienta sieci web.</span><span class="sxs-lookup"><span data-stu-id="36077-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="36077-222">[Ustawianie testów sieci web] [ availability] toomake się, że aplikacja pozostaje na żywo i szybko reagowały.</span><span class="sxs-lookup"><span data-stu-id="36077-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="36077-223">[Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toohelp diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="36077-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="36077-224">[Śledzenie narzędzia Log4J lub Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="36077-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="36077-225">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="36077-225">Track usage</span></span>
* <span data-ttu-id="36077-226">[Dodaj telemetrię usługi sieci web klienta] [ usage] toomonitor strony widoki i metryki użytkownika podstawowego.</span><span class="sxs-lookup"><span data-stu-id="36077-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="36077-227">[Śledzenie zdarzeń niestandardowych i metryki](app-insights-web-track-usage.md) toolearn o sposobie korzystania z aplikacji, zarówno na powitania klienta i serwera hello.</span><span class="sxs-lookup"><span data-stu-id="36077-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
