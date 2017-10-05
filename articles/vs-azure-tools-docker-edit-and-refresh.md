---
title: Debugowanie aplikacji w kontenerze Docker lokalnym | Dokumentacja firmy Microsoft
description: "Modyfikowanie aplikacji, która jest uruchomiona w kontenerze Docker lokalnego, Odśwież kontenera za pomocą edycji i Odśwież i ustaw punkty przerwania debugowania"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: fcd58736d8915a61683a416fb9bf3892ba7b7bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="0eeab-103">Debugowanie aplikacji w lokalnym kontenerze platformy Docker</span><span class="sxs-lookup"><span data-stu-id="0eeab-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="0eeab-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0eeab-104">Overview</span></span>
<span data-ttu-id="0eeab-105">Visual Studio Tools for Docker zapewnia spójny sposób rozwijać w i weryfikowanie aplikacji lokalnie w kontenerze Docker systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0eeab-105">The Visual Studio Tools for Docker provides a consistent way to develop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="0eeab-106">Nie trzeba ponownie uruchomić kontenera zawsze, gdy należy zmienić kod.</span><span class="sxs-lookup"><span data-stu-id="0eeab-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="0eeab-107">W tym artykule przedstawiono sposób Użyj funkcji "Edytuj i Odśwież", aby uruchomić aplikację sieci Web platformy ASP.NET Core w kontenerze Docker lokalnym, wprowadź niezbędne zmiany, a następnie odśwież przeglądarkę, aby zobaczyć wpływ zmian.</span><span class="sxs-lookup"><span data-stu-id="0eeab-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="0eeab-108">W tym artykule przedstawiono również sposób ustawić punkty przerwania dla debugowania.</span><span class="sxs-lookup"><span data-stu-id="0eeab-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="0eeab-109">Obsługa kontenera systemu Windows zostanie udostępniona w przyszłej wersji</span><span class="sxs-lookup"><span data-stu-id="0eeab-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="0eeab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0eeab-110">Prerequisites</span></span>
<span data-ttu-id="0eeab-111">Muszą być zainstalowane następujące narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0eeab-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="0eeab-112">Najnowszą wersję programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0eeab-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="0eeab-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="0eeab-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="0eeab-114">Aby uruchomić kontenery Docker lokalnie, należy klienta lokalnego docker.</span><span class="sxs-lookup"><span data-stu-id="0eeab-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="0eeab-115">Można użyć [przybornika Docker](https://www.docker.com/products/docker-toolbox), co wymaga funkcji Hyper-V jest wyłączona lub można użyć [Docker dla systemu Windows](https://www.docker.com/get-docker), który korzysta z funkcji Hyper-V i wymaga systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0eeab-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="0eeab-116">Jeśli przy użyciu rozwiązania Docker przybornika, konieczne będzie [Konfigurowanie klienta platformy Docker](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="0eeab-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="0eeab-117">1. Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="0eeab-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="0eeab-118">2. Dodawanie obsługi Docker</span><span class="sxs-lookup"><span data-stu-id="0eeab-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="0eeab-119">3. Edytuj kod i odświeżanie</span><span class="sxs-lookup"><span data-stu-id="0eeab-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="0eeab-120">Aby szybko przejść zmian, można uruchomić aplikację w kontenerze i kontynuować wprowadzanie zmian, ich wyświetlania, jak w przypadku z programem IIS Express.</span><span class="sxs-lookup"><span data-stu-id="0eeab-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="0eeab-121">Ustaw dla konfiguracji rozwiązania `Debug` i naciśnij klawisz  **&lt;CTRL + F5 >** do tworzenia obrazu docker i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="0eeab-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="0eeab-122">Gdy obraz kontener został utworzony i działa w kontenerze Docker, Visual Studio spowoduje uruchomienie aplikacji sieci Web w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="0eeab-122">Once the container image has been built and is running in a Docker container, Visual Studio will launch the Web app in your default browser.</span></span>
    <span data-ttu-id="0eeab-123">Jeśli używasz przeglądarki Microsoft Edge lub w przeciwnym razie zawiera błędy, zobacz [Rozwiązywanie problemów](vs-azure-tools-docker-troubleshooting-docker-errors.md) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0eeab-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="0eeab-124">Przejdź do strony informacje, czyli gdzie zamierzamy naszych zmiany.</span><span class="sxs-lookup"><span data-stu-id="0eeab-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="0eeab-125">Wróć do programu Visual Studio i otworzyć `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0eeab-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="0eeab-126">Dodaj następującą zawartość HTML na końcu pliku, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="0eeab-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="0eeab-127">Po ukończeniu kompilacji platformy .NET i wyświetlić te wiersze jest wyświetlany w oknie danych wyjściowych, wrócić do przeglądarki, a następnie odśwież stronę informacje.</span><span class="sxs-lookup"><span data-stu-id="0eeab-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="0eeab-128">Zmiany zostały zastosowane!</span><span class="sxs-lookup"><span data-stu-id="0eeab-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="0eeab-129">4. Debugowanie przy użyciu punktów przerwania</span><span class="sxs-lookup"><span data-stu-id="0eeab-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="0eeab-130">Często zmiany będzie potrzebna jest dalsza inspekcję, wykorzystując funkcje debugowania programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0eeab-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="0eeab-131">Wróć do programu Visual Studio i Otwórz`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="0eeab-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="0eeab-132">Zamień zawartość metody About() następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0eeab-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="0eeab-133">Ustaw punkt przerwania z lewej strony `string message`... wiersza.</span><span class="sxs-lookup"><span data-stu-id="0eeab-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="0eeab-134">Trafienia  **&lt;F5 >** można rozpocząć debugowania.</span><span class="sxs-lookup"><span data-stu-id="0eeab-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="0eeab-135">Przejdź do strony informacje do trafiony punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="0eeab-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="0eeab-136">Przełącz się do programu Visual Studio, aby wyświetlić punkt przerwania i sprawdzić wartość komunikatu.</span><span class="sxs-lookup"><span data-stu-id="0eeab-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="0eeab-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0eeab-137">Summary</span></span>
<span data-ttu-id="0eeab-138">Z [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), możesz uzyskać produktywność lokalnie, Praca z wzrostu produkcji rozwijających się w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="0eeab-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0eeab-139">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="0eeab-139">Troubleshooting</span></span>
[<span data-ttu-id="0eeab-140">Rozwiązywanie problemów z tworzenia Docker Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0eeab-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="0eeab-141">Więcej informacji na temat rozwiązania Docker z programu Visual Studio, Windows i Azure</span><span class="sxs-lookup"><span data-stu-id="0eeab-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="0eeab-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) — tworzenie kodu platformy .NET Core w kontenerze</span><span class="sxs-lookup"><span data-stu-id="0eeab-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="0eeab-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) — tworzenie i wdrażanie kontenerów docker</span><span class="sxs-lookup"><span data-stu-id="0eeab-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="0eeab-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) -języka usługi do edycji plików docker z scenariuszy e2e pochodzących</span><span class="sxs-lookup"><span data-stu-id="0eeab-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="0eeab-145">[Informacje o kontenerze Windows](http://aka.ms/containers)— informacje o systemie Windows Server i Nano Server</span><span class="sxs-lookup"><span data-stu-id="0eeab-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="0eeab-146">[Usługa kontenera platformy Azure](https://azure.microsoft.com/services/container-service/) - [zawartości usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="0eeab-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="0eeab-147">Więcej przykładów dotyczących pracy z rozwiązaniem Docker, zobacz [pracy z rozwiązaniem Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) z [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [pokaz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="0eeab-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="0eeab-148">Aby uzyskać więcej materiałów szybkiego startu z w wersji demonstracyjnej witryny HealthClinic.biz, zobacz [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts) (Materiały szybkiego startu narzędzi deweloperskich platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="0eeab-148">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="0eeab-149">Różne narzędzia Docker</span><span class="sxs-lookup"><span data-stu-id="0eeab-149">Various Docker tools</span></span>
[<span data-ttu-id="0eeab-150">Niektóre narzędzia dużą docker (blog Steve'a Lasker)</span><span class="sxs-lookup"><span data-stu-id="0eeab-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="0eeab-151">Artykuły dobra</span><span class="sxs-lookup"><span data-stu-id="0eeab-151">Good articles</span></span>
[<span data-ttu-id="0eeab-152">Wprowadzenie do Mikrousług z NGINX</span><span class="sxs-lookup"><span data-stu-id="0eeab-152">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="0eeab-153">Prezentacje</span><span class="sxs-lookup"><span data-stu-id="0eeab-153">Presentations</span></span>
* [<span data-ttu-id="0eeab-154">Steve Lasker: VS Wyszków 2016 - Docker e2e na żywo</span><span class="sxs-lookup"><span data-stu-id="0eeab-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="0eeab-155">Wprowadzenie do platformy ASP.NET Core @ kompilacji 2016 - gdzie możesz w pokaz</span><span class="sxs-lookup"><span data-stu-id="0eeab-155">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="0eeab-156">Tworzenie aplikacji .NET w kontenerach, Channel 9</span><span class="sxs-lookup"><span data-stu-id="0eeab-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
