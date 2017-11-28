---
title: "Wprowadzenie do usługi Azure Application Insights z językiem Java w środowisku Eclipse | Dokumentacja firmy Microsoft"
description: "Przy użyciu wtyczki Eclipse Dodaj wydajności i użycia monitorowania do witryny sieci Web Java z usługą Application Insights"
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="046b3-103">Wprowadzenie do usługi Application Insights z językiem Java w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="046b3-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="046b3-104">Zestaw SDK usługi Application Insights wysyła dane telemetryczne z aplikacji sieci web w języku Java, dzięki czemu można analizować użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="046b3-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="046b3-105">Wtyczki dla usługi Application Insights Eclipse automatycznie instaluje zestaw SDK w projekcie, tak aby uzyskać poza telemetrii pola, a także interfejs API, który służy do zapisywania telemetria niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="046b3-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="046b3-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="046b3-106">Prerequisites</span></span>
<span data-ttu-id="046b3-107">Obecnie wtyczki sprawdza w przypadku Maven projektów i dynamicznych projekty sieci Web w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="046b3-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="046b3-108">([Dodaj usługę Application Insights na inne typy projektu języka Java][java].)</span><span class="sxs-lookup"><span data-stu-id="046b3-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="046b3-109">Będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="046b3-109">You'll need:</span></span>

* <span data-ttu-id="046b3-110">Oracle środowiska JRE wersji 1.6 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="046b3-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="046b3-111">Subskrypcja platformy [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="046b3-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="046b3-112">[Zaćmienie-IDE for Java EE Developers](http://www.eclipse.org/downloads/), indygo lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="046b3-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="046b3-113">System Windows 7 lub nowszym lub Windows Server 2008 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="046b3-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="046b3-114">Zainstaluj zestaw SDK w środowisku Eclipse (jeden raz)</span><span class="sxs-lookup"><span data-stu-id="046b3-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="046b3-115">Wystarczy wykonać to jeden raz dla poszczególnych komputerów.</span><span class="sxs-lookup"><span data-stu-id="046b3-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="046b3-116">Ta czynność powoduje zainstalowanie zestawu narzędzi, które można następnie dodać zestawu SDK do każdego dynamiczny projekt sieci Web.</span><span class="sxs-lookup"><span data-stu-id="046b3-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="046b3-117">W programie Eclipse kliknij przycisk Pomoc, instalowanie nowego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="046b3-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Pomoc, należy zainstalować nowe oprogramowanie](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="046b3-119">Zestaw SDK jest http://dl.microsoft.com/eclipse, w obszarze zestawu narzędzi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="046b3-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="046b3-120">Usuń zaznaczenie pola wyboru **skontaktuj się z wszystkich witryn aktualizacji...**</span><span class="sxs-lookup"><span data-stu-id="046b3-120">Uncheck **Contact all update sites...**</span></span>

    ![Dla zestawu SDK usługi Application Insights wyczyść skontaktuj się z wszystkich witryn aktualizacji](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="046b3-122">Wykonaj pozostałe kroki dla każdego projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="046b3-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="046b3-123">Tworzenie zasobu usługi Application Insights na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="046b3-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="046b3-124">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="046b3-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="046b3-125">Utwórz nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="046b3-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="046b3-126">Jako typ aplikacji ustaw wartość Aplikacja sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="046b3-126">Set the application type to Java web application.</span></span>  

    ![Kliknij + i wybierz opcję Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="046b3-128">Znajdź klucz instrumentacji nowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="046b3-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="046b3-129">Wkrótce będzie trzeba wkleić go do projektu kodu.</span><span class="sxs-lookup"><span data-stu-id="046b3-129">You'll need to paste this into your code project shortly.</span></span>  

    ![W opisie nowego zasobu kliknij opcję Właściwości i skopiuj klucz instrumentacji](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="046b3-131">Dodaj usługę Application Insights do swojego projektu</span><span class="sxs-lookup"><span data-stu-id="046b3-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="046b3-132">Dodawanie usługi Application Insights z menu kontekstowego projektu sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="046b3-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![W opisie nowego zasobu kliknij opcję Właściwości i skopiuj klucz instrumentacji](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="046b3-134">Wklej klucz Instrumentacji pochodzący z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="046b3-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![W opisie nowego zasobu kliknij opcję Właściwości i skopiuj klucz instrumentacji](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="046b3-136">Klucz jest wysyłany razem z każdy element telemetrii i informuje usługi Application Insights, aby go wyświetlić w zasobie.</span><span class="sxs-lookup"><span data-stu-id="046b3-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="046b3-137">Uruchom aplikację i widzieć metryki</span><span class="sxs-lookup"><span data-stu-id="046b3-137">Run the application and see metrics</span></span>
<span data-ttu-id="046b3-138">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="046b3-138">Run your application.</span></span>

<span data-ttu-id="046b3-139">Wróć do zasobu usługi Application Insights w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="046b3-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="046b3-140">W bloku przeglądu zostaną wyświetlone dane żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="046b3-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="046b3-141">(Jeśli ich tam nie ma, odczekaj kilka sekund, a następnie kliknij przycisk Odśwież).</span><span class="sxs-lookup"><span data-stu-id="046b3-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="046b3-142">Odpowiedź serwera, liczby żądań i błędów</span><span class="sxs-lookup"><span data-stu-id="046b3-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="046b3-143">Klikaj elementy wykresów, aby wyświetlać bardziej szczegółowe metryki.</span><span class="sxs-lookup"><span data-stu-id="046b3-143">Click through any chart to see more detailed metrics.</span></span>

![Liczba żądań według nazwy](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="046b3-145">[Dowiedz się więcej o metrykach.][metrics]</span><span class="sxs-lookup"><span data-stu-id="046b3-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="046b3-146">Podczas przeglądania właściwości żądania, może uzyskać zdarzenia telemetrii skojarzonych z nim, takich jak żądania i wyjątków i.</span><span class="sxs-lookup"><span data-stu-id="046b3-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Wszystkie ślady dla tego żądania](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="046b3-148">Dane telemetryczne po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="046b3-148">Client-side telemetry</span></span>
<span data-ttu-id="046b3-149">W bloku Szybki Start kliknij przycisk Pobierz kod umożliwiający monitorowanie stron sieci web:</span><span class="sxs-lookup"><span data-stu-id="046b3-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![W bloku przeglądu aplikacji wybierz kolejno opcje Szybki start, Pobierz kod umożliwiający monitorowanie stron sieci Web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="046b3-152">Wstawianie fragmentu kodu w nagłówku pliki HTML.</span><span class="sxs-lookup"><span data-stu-id="046b3-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="046b3-153">Wyświetlanie danych po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="046b3-153">View client-side data</span></span>
<span data-ttu-id="046b3-154">Otwórz zaktualizowane stron sieci web i używać ich.</span><span class="sxs-lookup"><span data-stu-id="046b3-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="046b3-155">Zaczekaj minutę lub dwie, a następnie wróć do usługi Application Insights i otwórz blok wykorzystanie.</span><span class="sxs-lookup"><span data-stu-id="046b3-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="046b3-156">(Za pomocą bloku omówienie przewiń w dół i kliknij opcję użycia).</span><span class="sxs-lookup"><span data-stu-id="046b3-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="046b3-157">Strona widoku, użytkownika i sesji metryki pojawi się blok wykorzystanie:</span><span class="sxs-lookup"><span data-stu-id="046b3-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sesje, użytkowników i wyświetleń strony](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="046b3-159">[Dowiedz się więcej o konfigurowaniu telemetrii po stronie klienta.][usage]</span><span class="sxs-lookup"><span data-stu-id="046b3-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="046b3-160">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="046b3-160">Publish your application</span></span>
<span data-ttu-id="046b3-161">Teraz opublikuj aplikację na serwerze, pozwól z niej korzystać innym osobom, a następnie obejrzyj telemetrię wyświetlaną w portalu.</span><span class="sxs-lookup"><span data-stu-id="046b3-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="046b3-162">Upewnij się, że zapora pozwala aplikacji na wysłanie telemetrii do tych portów:</span><span class="sxs-lookup"><span data-stu-id="046b3-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="046b3-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="046b3-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="046b3-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="046b3-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="046b3-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="046b3-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="046b3-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="046b3-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="046b3-167">Na serwerach systemu Windows zainstaluj:</span><span class="sxs-lookup"><span data-stu-id="046b3-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="046b3-168">Pakiet Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="046b3-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="046b3-169">(Umożliwi to działanie liczników wydajności).</span><span class="sxs-lookup"><span data-stu-id="046b3-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="046b3-170">Wyjątki i błędy żądań</span><span class="sxs-lookup"><span data-stu-id="046b3-170">Exceptions and request failures</span></span>
<span data-ttu-id="046b3-171">Nieobsługiwane wyjątki są zbierane automatycznie:</span><span class="sxs-lookup"><span data-stu-id="046b3-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="046b3-172">Istnieją dwie opcje zbierania danych o innych wyjątkach:</span><span class="sxs-lookup"><span data-stu-id="046b3-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="046b3-173">[Wstawianie wywołania do TrackException w kodzie](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="046b3-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="046b3-174">[Instalacja agenta Java na serwerze](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="046b3-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="046b3-175">Trzeba określić metody, które chcesz śledzić.</span><span class="sxs-lookup"><span data-stu-id="046b3-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="046b3-176">Monitorowanie wywołań metod i zależności zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="046b3-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="046b3-177">[Zainstaluj agenta programu Java](app-insights-java-agent.md) w celu rejestrowania określonych metod wewnętrznych i wywołań za pośrednictwem JDBC z danymi chronometrażu.</span><span class="sxs-lookup"><span data-stu-id="046b3-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="046b3-178">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="046b3-178">Performance counters</span></span>
<span data-ttu-id="046b3-179">W bloku Przegląd, przewiń w dół i kliknij przycisk **serwerów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="046b3-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="046b3-180">Zobaczysz zakresu liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="046b3-180">You'll see a range of performance counters.</span></span>

![Przewiń w dół kliknij Kafelek serwery](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="046b3-182">Dostosowywanie zbierania danych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="046b3-182">Customize performance counter collection</span></span>
<span data-ttu-id="046b3-183">Aby wyłączyć zbieranie standardowego zestawu liczników wydajności, dodaj następujący kod w węźle głównym pliku ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="046b3-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="046b3-184">Zbieranie danych dodatkowych liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="046b3-184">Collect additional performance counters</span></span>
<span data-ttu-id="046b3-185">Możesz określić dodatkowe liczniki wydajności do zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="046b3-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="046b3-186">Liczniki JMX (udostępniane przez maszynę wirtualną Java)</span><span class="sxs-lookup"><span data-stu-id="046b3-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="046b3-187">`displayName` — nazwa wyświetlana w portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="046b3-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="046b3-188">`objectName` — nazwa obiektu JMX.</span><span class="sxs-lookup"><span data-stu-id="046b3-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="046b3-189">`attribute` — atrybut nazwy obiektu JMX do pobrania.</span><span class="sxs-lookup"><span data-stu-id="046b3-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="046b3-190">`type` (opcjonalnie) — typ atrybutu obiektu JMX:</span><span class="sxs-lookup"><span data-stu-id="046b3-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="046b3-191">wartość domyślna: typ prosty, np. int lub long.</span><span class="sxs-lookup"><span data-stu-id="046b3-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="046b3-192">`composite`: dane licznika wydajności są w formacie „Atrybut.Dane”</span><span class="sxs-lookup"><span data-stu-id="046b3-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="046b3-193">`tabular`: dane licznika wydajności są w formacie wiersza tabeli</span><span class="sxs-lookup"><span data-stu-id="046b3-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="046b3-194">Liczniki wydajności systemu Windows</span><span class="sxs-lookup"><span data-stu-id="046b3-194">Windows performance counters</span></span>
<span data-ttu-id="046b3-195">Każdy [licznik wydajności systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) należy do kategorii (w taki sam sposób, w jaki pole należy do klasy).</span><span class="sxs-lookup"><span data-stu-id="046b3-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="046b3-196">Kategorie mogą być globalne lub mogą mieć wystąpienia numerowane lub nazwane.</span><span class="sxs-lookup"><span data-stu-id="046b3-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="046b3-197">displayName — nazwa wyświetlana w portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="046b3-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="046b3-198">categoryName — kategoria licznika wydajności (obiekt wydajności), z którą skojarzony jest ten licznik wydajności.</span><span class="sxs-lookup"><span data-stu-id="046b3-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="046b3-199">counterName — nazwa licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="046b3-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="046b3-200">instanceName — nazwa wystąpienia kategorii licznika wydajności lub ciąg pusty (""), jeśli kategoria zawiera jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="046b3-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="046b3-201">Jeśli categoryName to Proces, a licznik wydajności, którego dane chcesz zbierać, pochodzi z bieżącego procesu maszyny JVM, na której jest uruchomiona aplikacja, podaj wartość `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="046b3-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="046b3-202">Liczniki wydajności są widoczne jako metryki niestandardowe w [Eksploratorze metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="046b3-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="046b3-203">Liczniki wydajności sytemu Unix</span><span class="sxs-lookup"><span data-stu-id="046b3-203">Unix performance counters</span></span>
* <span data-ttu-id="046b3-204">[Zainstaluj program collectd z wtyczką Application Insights](app-insights-java-collectd.md), aby uzyskać szeroką gamę danych na temat systemu i sieci.</span><span class="sxs-lookup"><span data-stu-id="046b3-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="046b3-205">Testy dostępności sieci Web</span><span class="sxs-lookup"><span data-stu-id="046b3-205">Availability web tests</span></span>
<span data-ttu-id="046b3-206">Usługa Application Insights może służyć do testowania witryny sieci Web w regularnych odstępach czasu, aby sprawdzić, czy witryna działa i odpowiada poprawnie.</span><span class="sxs-lookup"><span data-stu-id="046b3-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="046b3-207">[Aby skonfigurować][availability], przewiń w dół do kliknięcia dostępności.</span><span class="sxs-lookup"><span data-stu-id="046b3-207">[To set up][availability], scroll down to click Availability.</span></span>

![Przewiń w dół, kliknij opcję Dostępność, a następnie opcję Dodaj test sieci Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="046b3-209">Uzyskasz wykresy czasów odpowiedzi oraz powiadomienia e-mail w razie wyłączenia witryny.</span><span class="sxs-lookup"><span data-stu-id="046b3-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Przykład testu sieci Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="046b3-211">[Dowiedz się więcej o testach dostępności sieci Web.][availability]</span><span class="sxs-lookup"><span data-stu-id="046b3-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="046b3-212">Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="046b3-212">Diagnostic logs</span></span>
<span data-ttu-id="046b3-213">Jeśli używasz Logback lub Log4J (1.2 lub 2.0) śledzenia, może mieć dzienników śledzenia automatycznie przesyłane do usługi Application Insights, gdzie można eksplorować i ich wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="046b3-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="046b3-214">[Dowiedz się więcej o dzienników diagnostycznych][javalogs]</span><span class="sxs-lookup"><span data-stu-id="046b3-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="046b3-215">Telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="046b3-215">Custom telemetry</span></span>
<span data-ttu-id="046b3-216">Wstaw kilku wierszy kodu w aplikacji sieci web Java, aby dowiedzieć się, co robią użytkownicy z nim lub do diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="046b3-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="046b3-217">Możesz wstawić kod zarówno strony sieci web JavaScript i Java po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="046b3-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="046b3-218">[Dowiedz się więcej o telemetrii niestandardowej][track]</span><span class="sxs-lookup"><span data-stu-id="046b3-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="046b3-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="046b3-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="046b3-220">Wykrywanie i diagnozowanie problemów</span><span class="sxs-lookup"><span data-stu-id="046b3-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="046b3-221">[Dodaj telemetrię usługi sieci web klienta] [ usage] do Pobierz dane telemetryczne wydajności klienta sieci web.</span><span class="sxs-lookup"><span data-stu-id="046b3-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="046b3-222">[Konfigurowanie testów sieci Web][availability], aby upewnić się, że aplikacja stale działa i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="046b3-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="046b3-223">[Wyszukiwanie zdarzeń i dzienników][diagnostic], aby łatwiej diagnozować problemy.</span><span class="sxs-lookup"><span data-stu-id="046b3-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="046b3-224">[Śledzenie narzędzia Log4J lub Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="046b3-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="046b3-225">Śledzenie użycia</span><span class="sxs-lookup"><span data-stu-id="046b3-225">Track usage</span></span>
* <span data-ttu-id="046b3-226">[Dodaj telemetrię usługi sieci web klienta] [ usage] wyświetleń strony monitora i metryki użytkownika podstawowego.</span><span class="sxs-lookup"><span data-stu-id="046b3-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="046b3-227">[Śledzenie zdarzeń niestandardowych i metryki](app-insights-web-track-usage.md) Aby dowiedzieć się więcej o sposobie korzystania z aplikacji, zarówno na kliencie i serwerze.</span><span class="sxs-lookup"><span data-stu-id="046b3-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
