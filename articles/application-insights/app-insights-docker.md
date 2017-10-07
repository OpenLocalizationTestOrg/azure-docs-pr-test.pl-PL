---
title: "aaaMonitor Docker aplikacji w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Docker liczników wydajności, zdarzeń i wyjątków mogą być wyświetlane w usłudze Application Insights wraz z telemetrii hello z aplikacji hello konteneryzowanych."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="d6abb-103">Monitorowanie aplikacji Docker w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="d6abb-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="d6abb-104">Zdarzenia cyklu życia i wydajności liczników z [Docker](https://www.docker.com/) kontenerów może być na wykresie na usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6abb-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="d6abb-105">Zainstaluj hello [usługi Application Insights](app-insights-overview.md) obrazu w kontenerze w hoście, a wyświetli liczniki wydajności dla hosta hello oraz jak w przypadku hello inne obrazy.</span><span class="sxs-lookup"><span data-stu-id="d6abb-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="d6abb-106">Z rozwiązaniem Docker, z dystrybucji w kontenerach lekkie ukończone wszystkie zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6abb-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="d6abb-107">By działały na dowolnym komputerze hosta z systemem aparatem platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d6abb-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="d6abb-108">Po uruchomieniu hello [obrazu usługi Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) na hoście Docker, możesz uzyskać następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d6abb-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="d6abb-109">Cykl życia telemetrii dotyczące wszystkich kontenerów hello uruchomiona na hoście hello — uruchamianie, zatrzymywanie i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d6abb-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="d6abb-110">Liczniki wydajności dla wszystkich kontenerów hello.</span><span class="sxs-lookup"><span data-stu-id="d6abb-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="d6abb-111">Procesor CPU, pamięci, użycie sieci i inne.</span><span class="sxs-lookup"><span data-stu-id="d6abb-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="d6abb-112">Jeśli użytkownik [zainstalowany zestaw SDK usługi Application Insights dla języka Java](app-insights-java-live.md) w aplikacji hello w kontenerach hello, wszystkie telemetrii hello tych aplikacji będą miały dodatkowe właściwości hello kontenera i komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="d6abb-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="d6abb-113">Tak na przykład jeśli masz wystąpienie aplikacji uruchomionej w więcej niż jednego hosta, łatwo filtrować telemetrii aplikacji przez hosta.</span><span class="sxs-lookup"><span data-stu-id="d6abb-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Przykład](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="d6abb-115">Ustawianie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d6abb-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="d6abb-116">Zaloguj się do [portalu Microsoft Azure](https://azure.com) , a następnie otwórz hello zasobu usługi Application Insights dla aplikacji; lub [Utwórz nową](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d6abb-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="d6abb-117">*Którego zasobu należy użyć?*</span><span class="sxs-lookup"><span data-stu-id="d6abb-117">*Which resource should I use?*</span></span> <span data-ttu-id="d6abb-118">Jeśli hello aplikacje, które są uruchomione na hoście zostały opracowane przez innego użytkownika, a następnie należy zbyt[utworzyć nowy zasób usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d6abb-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="d6abb-119">Jest to, gdzie przeglądać i analizować dane telemetryczne hello.</span><span class="sxs-lookup"><span data-stu-id="d6abb-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="d6abb-120">(Wybierz Ogólne, dla typu aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="d6abb-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="d6abb-121">Ale jeśli hello Deweloper aplikacji hello, następnie mamy nadzieję, że możesz [dodaje zestaw SDK usługi Application Insights](app-insights-java-live.md) tooeach z nich.</span><span class="sxs-lookup"><span data-stu-id="d6abb-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="d6abb-122">Jeśli są one wszystkich naprawdę składników aplikacji biznesowej, a następnie można skonfigurować ich wszystkich zasobów tooone telemetrii toosend i będzie używać tego samego zasobu toodisplay hello Docker cykl życia i wydajności danych.</span><span class="sxs-lookup"><span data-stu-id="d6abb-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="d6abb-123">Trzeci scenariusz jest opracowany większość aplikacji hello, że używasz toodisplay oddzielne zasoby ich telemetrii.</span><span class="sxs-lookup"><span data-stu-id="d6abb-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="d6abb-124">W takim przypadku należy prawdopodobnie również chcesz toocreate oddzielne zasobu hello danych Docker.</span><span class="sxs-lookup"><span data-stu-id="d6abb-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="d6abb-125">Dodaj hello Docker kafelka: Wybierz **dodać Kafelek**, przeciągnij Kafelek Docker hello z galerii hello, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="d6abb-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![Przykład](./media/app-insights-docker/03.png)
3. <span data-ttu-id="d6abb-127">Kliknij przycisk hello **Essentials** listy rozwijanej i skopiuj hello klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="d6abb-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="d6abb-128">Użyj tego hello tootell SDK gdzie toosend jego telemetrii.</span><span class="sxs-lookup"><span data-stu-id="d6abb-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![Przykład](./media/app-insights-docker/02-props.png)

<span data-ttu-id="d6abb-130">Zachowanie tego okna przeglądarki przydatną, jak będzie powrocie tooit wkrótce toolook na telemetrii.</span><span class="sxs-lookup"><span data-stu-id="d6abb-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="d6abb-131">Uruchom monitor usługi Application Insights hello na hoście</span><span class="sxs-lookup"><span data-stu-id="d6abb-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="d6abb-132">Skoro masz gdzieś toodisplay hello telemetrii, można skonfigurować hello konteneryzowanych aplikację, która będzie gromadzić i wysłać go.</span><span class="sxs-lookup"><span data-stu-id="d6abb-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="d6abb-133">Połącz tooyour Docker hosta.</span><span class="sxs-lookup"><span data-stu-id="d6abb-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="d6abb-134">Edytuj klucz Instrumentacji do tego polecenia, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="d6abb-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="d6abb-135">Tylko jeden obraz usługi Application Insights jest wymagany na hoście Docker.</span><span class="sxs-lookup"><span data-stu-id="d6abb-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="d6abb-136">Jeśli aplikacja jest wdrażana na wielu hostach Docker, następnie powtórz polecenie hello na każdym hoście.</span><span class="sxs-lookup"><span data-stu-id="d6abb-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="d6abb-137">Aktualizowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d6abb-137">Update your app</span></span>
<span data-ttu-id="d6abb-138">Jeśli aplikacja jest instrumentowane przy użyciu hello [zestaw SDK usługi Application Insights dla języka Java](app-insights-java-get-started.md), Dodaj powitania po wierszu do pliku ApplicationInsights.xml hello w projekcie, w obszarze hello `<TelemetryInitializers>` elementu:</span><span class="sxs-lookup"><span data-stu-id="d6abb-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="d6abb-139">Spowoduje to dodanie Docker informacje, takie jak kontener i hosta tooevery telemetrii elementu identyfikatora wysyłane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6abb-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="d6abb-140">Wyświetlanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="d6abb-140">View your telemetry</span></span>
<span data-ttu-id="d6abb-141">Przejdź wstecz tooyour zasobu usługi Application Insights w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6abb-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="d6abb-142">Kliknij Kafelek Docker hello.</span><span class="sxs-lookup"><span data-stu-id="d6abb-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="d6abb-143">Wkrótce zobaczysz danych otrzymywanych z aplikacji Docker hello, zwłaszcza, jeśli masz inne kontenery zasilany z aparatem platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d6abb-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="d6abb-144">Poniżej przedstawiono niektóre hello widoków, które można pobrać.</span><span class="sxs-lookup"><span data-stu-id="d6abb-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="d6abb-145">Liczniki wydajności przez hosta, działania przez obraz</span><span class="sxs-lookup"><span data-stu-id="d6abb-145">Perf counters by host, activity by image</span></span>
![Przykład](./media/app-insights-docker/10.png)

![Przykład](./media/app-insights-docker/11.png)

<span data-ttu-id="d6abb-148">Kliknij dowolną nazwę hosta lub obraz, aby uzyskać więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="d6abb-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="d6abb-149">toocustomize hello widok, kliknij dowolnego wykresu, nagłówek siatki hello, lub użyj Dodawanie wykresu.</span><span class="sxs-lookup"><span data-stu-id="d6abb-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="d6abb-150">[Dowiedz się więcej o Eksploratora metryk](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="d6abb-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="d6abb-151">Zdarzenia kontenera docker</span><span class="sxs-lookup"><span data-stu-id="d6abb-151">Docker container events</span></span>
![Przykład](./media/app-insights-docker/13.png)

<span data-ttu-id="d6abb-153">tooinvestigate poszczególne zdarzenia, kliknij [wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d6abb-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="d6abb-154">Wyszukaj i Filtruj toofind hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d6abb-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="d6abb-155">Kliknij przycisk tooget żadnych zdarzeń więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="d6abb-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="d6abb-156">Wyjątki według nazwy kontenera</span><span class="sxs-lookup"><span data-stu-id="d6abb-156">Exceptions by container name</span></span>
![Przykład](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="d6abb-158">Kontekst docker dodane tooapp telemetrii</span><span class="sxs-lookup"><span data-stu-id="d6abb-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="d6abb-159">Dane telemetryczne żądania wysyłane z aplikacji hello Instrumentacji z zestawem SDK AI, wzbogaconych Docker kontekstu:</span><span class="sxs-lookup"><span data-stu-id="d6abb-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![Przykład](./media/app-insights-docker/16.png)

<span data-ttu-id="d6abb-161">Liczniki wydajności dostępnej pamięci i czasu procesora wzbogacone i pogrupowane według nazwy kontenera Docker:</span><span class="sxs-lookup"><span data-stu-id="d6abb-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Przykład](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="d6abb-163">Pytania i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d6abb-163">Q & A</span></span>
<span data-ttu-id="d6abb-164">*Co to oznacza usługi Application Insights udzielenia mnie, który nie może odczytać Docker?*</span><span class="sxs-lookup"><span data-stu-id="d6abb-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="d6abb-165">Szczegółowy podział liczniki wydajności przez kontener i obrazów.</span><span class="sxs-lookup"><span data-stu-id="d6abb-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="d6abb-166">Integrowanie aplikacji i kontenera danych na jednym pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="d6abb-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="d6abb-167">[Eksportuj dane telemetryczne](app-insights-export-telemetry.md) dla dalszego analizy tooa bazy danych usługi Power BI lub innymi pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6abb-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="d6abb-168">*Jak uzyskać dane telemetryczne z aplikacji hello?*</span><span class="sxs-lookup"><span data-stu-id="d6abb-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="d6abb-169">Zainstaluj zestaw SDK usługi Application Insights hello w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d6abb-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="d6abb-170">Dowiedz się, jak dla: [aplikacje sieci web Java](app-insights-java-get-started.md), [aplikacji sieci web systemu Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="d6abb-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="d6abb-171">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="d6abb-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d6abb-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6abb-172">Next steps</span></span>

* [<span data-ttu-id="d6abb-173">Application Insights dla języka Java</span><span class="sxs-lookup"><span data-stu-id="d6abb-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="d6abb-174">Usługa Application Insights dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="d6abb-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="d6abb-175">Application Insights dla platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d6abb-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
