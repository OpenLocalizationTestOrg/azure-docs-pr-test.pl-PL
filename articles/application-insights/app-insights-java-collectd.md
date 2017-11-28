---
title: "aaaMonitor wydajność aplikacji sieci web Java w systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Rozszerzone monitorowanie wydajności aplikacji witryny sieci Web Java z hello CollectD wtyczki dla usługi Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="88f34-103">collectd: metryki wydajności systemu Linux w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="88f34-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="88f34-104">metryki wydajności systemu Linux tooexplore w [usługi Application Insights](app-insights-overview.md), zainstaluj [collectd](http://collectd.org/), wraz z jej usługi Application Insights wtyczki.</span><span class="sxs-lookup"><span data-stu-id="88f34-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="88f34-105">To rozwiązanie open source zbiera dane statystyczne różnych systemów i sieci.</span><span class="sxs-lookup"><span data-stu-id="88f34-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="88f34-106">Zazwyczaj będzie używać collectd, jeśli masz już [zinstrumentowane usługi sieci web Java z usługą Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="88f34-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="88f34-107">Daje więcej danych toohelp tooenhance możesz wydajności aplikacji i diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="88f34-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Wykresy próbki](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="88f34-109">Uzyskaj swój klucz Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="88f34-109">Get your instrumentation key</span></span>
<span data-ttu-id="88f34-110">W hello [portalu Microsoft Azure](https://portal.azure.com), otwórz hello [usługi Application Insights](app-insights-overview.md) miejscu hello tooappear danych zasobów.</span><span class="sxs-lookup"><span data-stu-id="88f34-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="88f34-111">(Lub [utworzyć nowy zasób](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="88f34-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="88f34-112">Należy wykonać kopię klucza Instrumentacji hello, które identyfikuje hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="88f34-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Przeglądaj wszystkie, otwórz zasobu, a następnie w hello Essentials listy rozwijanej wybierz, a następnie skopiuj hello klucza Instrumentacji](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="88f34-114">Zainstaluj collectd i hello wtyczki</span><span class="sxs-lookup"><span data-stu-id="88f34-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="88f34-115">Na komputerach serwerów Linux:</span><span class="sxs-lookup"><span data-stu-id="88f34-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="88f34-116">Zainstaluj [collectd](http://collectd.org/) wersji 5.4.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="88f34-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="88f34-117">Pobierz hello [usługi Application Insights collectd zapisywania wtyczki](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="88f34-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="88f34-118">Zanotuj numer wersji powitania.</span><span class="sxs-lookup"><span data-stu-id="88f34-118">Note hello version number.</span></span>
3. <span data-ttu-id="88f34-119">Skopiuj wtyczki hello JAR w `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="88f34-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="88f34-120">Edytuj `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="88f34-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="88f34-121">Upewnij się, że [hello wtyczki Java](https://collectd.org/wiki/index.php/Plugin:Java) jest włączona.</span><span class="sxs-lookup"><span data-stu-id="88f34-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="88f34-122">Zaktualizuj hello JVMArg dla hello tooinclude java.class.path powitania po JAR.</span><span class="sxs-lookup"><span data-stu-id="88f34-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="88f34-123">Aktualizacja hello wersji numer toomatch hello pobranego co:</span><span class="sxs-lookup"><span data-stu-id="88f34-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="88f34-124">Dodaj następujący fragment kodu przy użyciu hello klucza Instrumentacji z zasobu:</span><span class="sxs-lookup"><span data-stu-id="88f34-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="88f34-125">W tym miejscu jest częścią przykładowy plik konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="88f34-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="88f34-126">Konfigurowanie innych [wtyczek collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), które może zbierać różne dane z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="88f34-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="88f34-127">Uruchom ponownie collectd zgodnie z tooits [ręczne](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="88f34-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="88f34-128">Wyświetlanie danych hello w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="88f34-128">View hello data in Application Insights</span></span>
<span data-ttu-id="88f34-129">Zasób usługi Application Insights, otwórz [Eksploratora metryk i Dodaj wykresy][metrics], wybierając metryki hello ma toosee z hello kategorię niestandardową.</span><span class="sxs-lookup"><span data-stu-id="88f34-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="88f34-130">Domyślnie metryki hello są agregowane na wszystkich komputerach hosta, z których zebrano hello metryki.</span><span class="sxs-lookup"><span data-stu-id="88f34-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="88f34-131">metryki hello tooview jednego hosta, w bloku szczegóły wykresu hello włączyć grupowanie, a następnie wybierz toogroup przez CollectD hosta.</span><span class="sxs-lookup"><span data-stu-id="88f34-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="88f34-132">przekazywanie tooexclude poszczególnych statystyk</span><span class="sxs-lookup"><span data-stu-id="88f34-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="88f34-133">Domyślnie wtyczkę usługi Application Insights hello wysyła wszystkie hello zebrane przez wszystkie collectd hello włączone "odczytu danych" wtyczek.</span><span class="sxs-lookup"><span data-stu-id="88f34-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="88f34-134">tooexclude danych z konkretnych źródeł danych lub wtyczek:</span><span class="sxs-lookup"><span data-stu-id="88f34-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="88f34-135">Edytuj hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="88f34-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="88f34-136">W `<Plugin ApplicationInsightsWriter>`, Dodaj dyrektywy wiersze następująco:</span><span class="sxs-lookup"><span data-stu-id="88f34-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="88f34-137">Dyrektywy</span><span class="sxs-lookup"><span data-stu-id="88f34-137">Directive</span></span> | <span data-ttu-id="88f34-138">Efekt</span><span class="sxs-lookup"><span data-stu-id="88f34-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="88f34-139">Wyklucz wszystkie dane zebrane przez hello `disk` wtyczki</span><span class="sxs-lookup"><span data-stu-id="88f34-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="88f34-140">Wyklucz źródła hello o nazwie `read` i `write` z hello `disk` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="88f34-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="88f34-141">Oddzielne dyrektywy z nowym wierszem.</span><span class="sxs-lookup"><span data-stu-id="88f34-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="88f34-142">Problemy?</span><span class="sxs-lookup"><span data-stu-id="88f34-142">Problems?</span></span>
<span data-ttu-id="88f34-143">*Nie widać danych w portalu hello*</span><span class="sxs-lookup"><span data-stu-id="88f34-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="88f34-144">Otwórz [wyszukiwania] [ diagnostic] toosee Jeśli następować hello zdarzenia pierwotnych.</span><span class="sxs-lookup"><span data-stu-id="88f34-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="88f34-145">Czasami podejmują tooappear dłużej w Eksploratorze metryk.</span><span class="sxs-lookup"><span data-stu-id="88f34-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="88f34-146">Może być konieczne zbyt[Ustaw wyjątki zapory dla danych wychodzących](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="88f34-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="88f34-147">Włącz śledzenie w hello wtyczkę usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="88f34-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="88f34-148">Dodaj następujący wiersz w `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="88f34-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="88f34-149">Otwórz terminal i uruchom collectd w trybie informacji pełnej, toosee problemów tak:</span><span class="sxs-lookup"><span data-stu-id="88f34-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="88f34-150">Znany problem</span><span class="sxs-lookup"><span data-stu-id="88f34-150">Known issue</span></span>

<span data-ttu-id="88f34-151">Dodatek zapisu Insights aplikacji Hello jest niezgodna z niektórych wtyczek odczytu.</span><span class="sxs-lookup"><span data-stu-id="88f34-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="88f34-152">Niektóre wtyczki czasami wysyłania "NaN", gdzie wtyczkę usługi Application Insights hello oczekuje liczba zmiennoprzecinkowa.</span><span class="sxs-lookup"><span data-stu-id="88f34-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="88f34-153">Objaw: hello collectd dziennika zawiera błędy, które obejmują "AI:... SyntaxError: nieoczekiwany token N ".</span><span class="sxs-lookup"><span data-stu-id="88f34-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="88f34-154">Obejście problemu: Wykluczanie danych zbieranych przez hello problem zapisu wtyczek.</span><span class="sxs-lookup"><span data-stu-id="88f34-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


