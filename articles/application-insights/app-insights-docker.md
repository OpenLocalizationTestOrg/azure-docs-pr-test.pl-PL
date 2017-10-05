---
title: "Monitorowanie aplikacji Docker w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Docker liczników wydajności, zdarzeń i wyjątków mogą być wyświetlane w usłudze Application Insights oraz dane telemetryczne z aplikacji konteneryzowanych."
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="e0bd8-103">Monitorowanie aplikacji Docker w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0bd8-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="e0bd8-104">Zdarzenia cyklu życia i wydajności liczników z [Docker](https://www.docker.com/) kontenerów może być na wykresie na usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="e0bd8-105">Zainstaluj [usługi Application Insights](app-insights-overview.md) obrazu w kontenerze w hoście, a wyświetli liczniki wydajności dla hosta, a także inne obrazy.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="e0bd8-106">Z rozwiązaniem Docker, z dystrybucji w kontenerach lekkie ukończone wszystkie zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="e0bd8-107">By działały na dowolnym komputerze hosta z systemem aparatem platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="e0bd8-108">Po uruchomieniu [obrazu usługi Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) na hoście Docker, możesz uzyskać następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="e0bd8-109">Cykl życia telemetrii dotyczące wszystkich kontenerów, które są uruchomione na hoście — uruchamianie, zatrzymywanie i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="e0bd8-110">Liczniki wydajności dla wszystkich kontenerów.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-110">Performance counters for all the containers.</span></span> <span data-ttu-id="e0bd8-111">Procesor CPU, pamięci, użycie sieci i inne.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="e0bd8-112">Jeśli użytkownik [zainstalowany zestaw SDK usługi Application Insights dla języka Java](app-insights-java-live.md) w aplikacje uruchomione w kontenerach, wszystkie dane telemetryczne tych aplikacji będą miały dodatkowe właściwości identyfikacji komputera hosta i kontenera.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="e0bd8-113">Tak na przykład jeśli masz wystąpienie aplikacji uruchomionej w więcej niż jednego hosta, łatwo filtrować telemetrii aplikacji przez hosta.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Przykład](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="e0bd8-115">Ustawianie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0bd8-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="e0bd8-116">Zaloguj się do [portalu Microsoft Azure](https://azure.com) , a następnie otwórz zasobu usługi Application Insights dla aplikacji; lub [Utwórz nową](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="e0bd8-117">*Którego zasobu należy użyć?*</span><span class="sxs-lookup"><span data-stu-id="e0bd8-117">*Which resource should I use?*</span></span> <span data-ttu-id="e0bd8-118">Jeśli aplikacje, które są uruchomione na hoście zostały opracowane przez innego użytkownika, a następnie trzeba [utworzyć nowy zasób usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="e0bd8-119">Jest to, gdzie przeglądać i analizować dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="e0bd8-120">(Wybierz Ogólne, dla typu aplikacji).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="e0bd8-121">Ale jeśli jesteś Deweloper aplikacji, a następnie mamy nadzieję [dodaje zestaw SDK usługi Application Insights](app-insights-java-live.md) do każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="e0bd8-122">Jeśli są one wszystkich naprawdę składników aplikacji biznesowej, można skonfigurować wszystkie z nich do wysyłania danych telemetrycznych do jednego zasobu, a więc będzie używać tego samego zasobu do wyświetlenia danych wydajności i cyklem życia rozwiązania Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="e0bd8-123">Trzeci scenariusz jest opracowany większość aplikacji, że używasz oddzielnych zasobów do wyświetlenia ich telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="e0bd8-124">W takim przypadku użytkownik może być także tworzenie oddzielnych zasobu danych Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="e0bd8-125">Dodaj kafelka Docker: Wybierz **dodać Kafelek**, przeciągnij Kafelek Docker z poziomu galerii, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![Przykład](./media/app-insights-docker/03.png)
3. <span data-ttu-id="e0bd8-127">Kliknij przycisk **Essentials** listy rozwijanej i skopiuj klucz instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="e0bd8-128">Możesz użyć tego stwierdzić, gdzie jego danych telemetrycznych zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![Przykład](./media/app-insights-docker/02-props.png)

<span data-ttu-id="e0bd8-130">Zachowaj przydatne, to okno przeglądarki, jak będzie wrócić do niego wkrótce aby przyjrzeć się telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="e0bd8-131">Uruchom monitor usługi Application Insights na hoście</span><span class="sxs-lookup"><span data-stu-id="e0bd8-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="e0bd8-132">Skoro masz innym miejscu, aby wyświetlić dane telemetryczne, można skonfigurować konteneryzowanych aplikację, która będzie gromadzić i wysłać go.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="e0bd8-133">Łączą się z hostem Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="e0bd8-134">Edytuj klucz Instrumentacji do tego polecenia, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="e0bd8-135">Tylko jeden obraz usługi Application Insights jest wymagany na hoście Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="e0bd8-136">Jeśli aplikacja jest wdrażana na wielu hostach Docker, następnie powtórz polecenie na każdym hoście.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="e0bd8-137">Aktualizowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e0bd8-137">Update your app</span></span>
<span data-ttu-id="e0bd8-138">Jeśli aplikacja jest instrumentowane przy użyciu [zestaw SDK usługi Application Insights dla języka Java](app-insights-java-get-started.md), Dodaj następujący wiersz w pliku ApplicationInsights.xml w projekcie, w obszarze `<TelemetryInitializers>` elementu:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="e0bd8-139">Spowoduje to dodanie Docker takie informacje jak kontener i identyfikator hosta do każdego elementu danych telemetrycznych wysłanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="e0bd8-140">Wyświetlanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="e0bd8-140">View your telemetry</span></span>
<span data-ttu-id="e0bd8-141">Wróć do zasobu usługi Application Insights w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="e0bd8-142">Kliknij Kafelek Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-142">Click through the Docker tile.</span></span>

<span data-ttu-id="e0bd8-143">Wkrótce zobaczysz danych otrzymywanych z aplikacji Docker, zwłaszcza, jeśli masz inne kontenery zasilany z aparatem platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="e0bd8-144">Poniżej przedstawiono niektóre widoki, które można pobrać.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="e0bd8-145">Liczniki wydajności przez hosta, działania przez obraz</span><span class="sxs-lookup"><span data-stu-id="e0bd8-145">Perf counters by host, activity by image</span></span>
![Przykład](./media/app-insights-docker/10.png)

![Przykład](./media/app-insights-docker/11.png)

<span data-ttu-id="e0bd8-148">Kliknij dowolną nazwę hosta lub obraz, aby uzyskać więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="e0bd8-149">Aby dostosować widok, kliknij dowolnego wykresu, siatki nagłówka, lub użyj Dodawanie wykresu.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="e0bd8-150">[Dowiedz się więcej o Eksploratora metryk](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="e0bd8-151">Zdarzenia kontenera docker</span><span class="sxs-lookup"><span data-stu-id="e0bd8-151">Docker container events</span></span>
![Przykład](./media/app-insights-docker/13.png)

<span data-ttu-id="e0bd8-153">Aby zbadać pojedynczych zdarzeń, kliknij przycisk [wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="e0bd8-154">Wyszukaj i Filtruj zdarzenia, które chcesz odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="e0bd8-155">Kliknij przycisk dowolnego zdarzenia, aby uzyskać więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="e0bd8-156">Wyjątki według nazwy kontenera</span><span class="sxs-lookup"><span data-stu-id="e0bd8-156">Exceptions by container name</span></span>
![Przykład](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="e0bd8-158">Docker dodano kontekst do telemetrii aplikacji</span><span class="sxs-lookup"><span data-stu-id="e0bd8-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="e0bd8-159">Dane telemetryczne żądania wysyłane z aplikacji Instrumentacji z zestawem SDK AI, wzbogaconych Docker kontekstu:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![Przykład](./media/app-insights-docker/16.png)

<span data-ttu-id="e0bd8-161">Liczniki wydajności dostępnej pamięci i czasu procesora wzbogacone i pogrupowane według nazwy kontenera Docker:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Przykład](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="e0bd8-163">Pytania i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e0bd8-163">Q & A</span></span>
<span data-ttu-id="e0bd8-164">*Co to oznacza usługi Application Insights udzielenia mnie, który nie może odczytać Docker?*</span><span class="sxs-lookup"><span data-stu-id="e0bd8-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="e0bd8-165">Szczegółowy podział liczniki wydajności przez kontener i obrazów.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="e0bd8-166">Integrowanie aplikacji i kontenera danych na jednym pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="e0bd8-167">[Eksportuj dane telemetryczne](app-insights-export-telemetry.md) do dalszej analizy do bazy danych, usługi Power BI lub innymi pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="e0bd8-168">*Jak uzyskać dane telemetryczne z aplikacji?*</span><span class="sxs-lookup"><span data-stu-id="e0bd8-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="e0bd8-169">Zainstaluj zestaw SDK usługi Application Insights w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="e0bd8-170">Dowiedz się, jak dla: [aplikacje sieci web Java](app-insights-java-get-started.md), [aplikacji sieci web systemu Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="e0bd8-171">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="e0bd8-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e0bd8-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0bd8-172">Next steps</span></span>

* [<span data-ttu-id="e0bd8-173">Application Insights dla języka Java</span><span class="sxs-lookup"><span data-stu-id="e0bd8-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="e0bd8-174">Usługa Application Insights dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="e0bd8-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="e0bd8-175">Application Insights dla platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e0bd8-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
