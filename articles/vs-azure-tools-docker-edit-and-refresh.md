---
title: aplikacje aaaDebugging w kontenerze Docker lokalnym | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomodify aplikacji, która jest uruchomiona w kontenerze Docker lokalnego, Odśwież hello kontenera za pomocą edycji i Odśwież i ustaw punkty przerwania debugowania"
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
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="cfc92-103">Debugowanie aplikacji w lokalnym kontenerze platformy Docker</span><span class="sxs-lookup"><span data-stu-id="cfc92-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="cfc92-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cfc92-104">Overview</span></span>
<span data-ttu-id="cfc92-105">Hello Visual Studio Tools for Docker zapewnia spójny sposób toodevelop w i zweryfikować Twojej aplikacji lokalnie w kontenerze Docker systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="cfc92-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="cfc92-106">Nie masz kontenera hello toorestart zawsze, gdy należy zmienić kod.</span><span class="sxs-lookup"><span data-stu-id="cfc92-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="cfc92-107">W tym artykule przedstawiono sposób toostart funkcji "Edytuj i Odśwież" hello toouse aplikacji sieci Web platformy ASP.NET Core w kontenerze Docker lokalnym, wprowadź niezbędne zmiany, a następnie Odśwież toosee przeglądarki hello te zmiany.</span><span class="sxs-lookup"><span data-stu-id="cfc92-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="cfc92-108">Ten artykuł zawiera także jak punkty przerwania tooset do debugowania.</span><span class="sxs-lookup"><span data-stu-id="cfc92-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="cfc92-109">Obsługa kontenera systemu Windows zostanie udostępniona w przyszłej wersji</span><span class="sxs-lookup"><span data-stu-id="cfc92-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="cfc92-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cfc92-110">Prerequisites</span></span>
<span data-ttu-id="cfc92-111">następujące narzędzia Hello musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="cfc92-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="cfc92-112">Najnowszą wersję programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cfc92-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="cfc92-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="cfc92-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="cfc92-114">lokalnie toorun Docker kontenerów, będziesz potrzebować klienta lokalnego docker.</span><span class="sxs-lookup"><span data-stu-id="cfc92-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="cfc92-115">Można użyć hello [przybornika Docker](https://www.docker.com/products/docker-toolbox), co wymaga funkcji Hyper-V toobe wyłączone lub można użyć [Docker dla systemu Windows](https://www.docker.com/get-docker), który korzysta z funkcji Hyper-V i wymaga systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cfc92-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="cfc92-116">Jeśli przy użyciu rozwiązania Docker przybornika, konieczne będzie zbyt[skonfigurować powitania klienta Docker](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="cfc92-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="cfc92-117">1. Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cfc92-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="cfc92-118">2. Dodawanie obsługi Docker</span><span class="sxs-lookup"><span data-stu-id="cfc92-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="cfc92-119">3. Edytuj kod i odświeżanie</span><span class="sxs-lookup"><span data-stu-id="cfc92-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="cfc92-120">tooquickly iteracyjne zmiany, możesz uruchomić aplikację w kontenerze i kontynuować toomake zmian, ich wyświetlania, jak w przypadku z programem IIS Express.</span><span class="sxs-lookup"><span data-stu-id="cfc92-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="cfc92-121">Ustaw hello konfiguracji rozwiązania za`Debug` i naciśnij klawisz  **&lt;CTRL + F5 >** toobuild Twojego docker obrazu i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cfc92-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="cfc92-122">Po hello kontenera obraz został utworzony i działa w kontenerze Docker, Visual Studio uruchomi hello aplikacji sieci Web w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="cfc92-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="cfc92-123">Jeśli używasz przeglądarki Microsoft Edge hello lub w przeciwnym razie zawiera błędy, zobacz [Rozwiązywanie problemów](vs-azure-tools-docker-troubleshooting-docker-errors.md) sekcji.</span><span class="sxs-lookup"><span data-stu-id="cfc92-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="cfc92-124">Przejdź toohello o stronę, czyli gdzie zamierzamy toomake naszych zmiany.</span><span class="sxs-lookup"><span data-stu-id="cfc92-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="cfc92-125">Zwraca tooVisual Studio i Otwórz `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="cfc92-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="cfc92-126">Dodaj hello toohello zawartości HTML końca pliku hello i Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="cfc92-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="cfc92-127">Wyświetlanie hello okno danych wyjściowych, po ukończeniu hello kompilacji platformy .NET i wyświetlić te wiersze, Przełącz tooyour Wstecz przeglądarki i Odśwież hello o stronie.</span><span class="sxs-lookup"><span data-stu-id="cfc92-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="cfc92-128">Zmiany zostały zastosowane!</span><span class="sxs-lookup"><span data-stu-id="cfc92-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="cfc92-129">4. Debugowanie przy użyciu punktów przerwania</span><span class="sxs-lookup"><span data-stu-id="cfc92-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="cfc92-130">Często zmiany należy dalszych kontroli, wykorzystując hello funkcji programu Visual Studio do debugowania.</span><span class="sxs-lookup"><span data-stu-id="cfc92-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="cfc92-131">Zwraca tooVisual Studio i Otwórz`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="cfc92-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="cfc92-132">Zastąp zawartość hello metody About() hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="cfc92-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="cfc92-133">Zestaw toohello punktu przerwania rogu hello `string message`... wiersza.</span><span class="sxs-lookup"><span data-stu-id="cfc92-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="cfc92-134">Trafienia  **&lt;F5 >** toostart debugowania.</span><span class="sxs-lookup"><span data-stu-id="cfc92-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="cfc92-135">Przejdź toohello o toohit strony punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="cfc92-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="cfc92-136">Przełącz tooVisual Studio tooview hello przerwania i sprawdzić wartość wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="cfc92-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="cfc92-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="cfc92-137">Summary</span></span>
<span data-ttu-id="cfc92-138">Z [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), możesz uzyskać produktywność hello lokalnie, Praca z wzrostu produkcji hello rozwijających się w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="cfc92-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cfc92-139">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="cfc92-139">Troubleshooting</span></span>
[<span data-ttu-id="cfc92-140">Rozwiązywanie problemów z tworzenia Docker Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cfc92-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="cfc92-141">Więcej informacji na temat rozwiązania Docker z programu Visual Studio, Windows i Azure</span><span class="sxs-lookup"><span data-stu-id="cfc92-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="cfc92-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) — tworzenie kodu platformy .NET Core w kontenerze</span><span class="sxs-lookup"><span data-stu-id="cfc92-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="cfc92-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) — tworzenie i wdrażanie kontenerów docker</span><span class="sxs-lookup"><span data-stu-id="cfc92-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="cfc92-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) -języka usługi do edycji plików docker z scenariuszy e2e pochodzących</span><span class="sxs-lookup"><span data-stu-id="cfc92-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="cfc92-145">[Informacje o kontenerze Windows](http://aka.ms/containers)— informacje o systemie Windows Server i Nano Server</span><span class="sxs-lookup"><span data-stu-id="cfc92-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="cfc92-146">[Usługa kontenera platformy Azure](https://azure.microsoft.com/services/container-service/) - [zawartości usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="cfc92-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="cfc92-147">Więcej przykładów dotyczących pracy z rozwiązaniem Docker, zobacz [pracy z rozwiązaniem Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) z hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [pokaz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="cfc92-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="cfc92-148">Przewodniki Szybki Start więcej z hello HealthClinic.biz demonstracyjnej, aby zapoznać [Przewodniki Szybki Start Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="cfc92-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="cfc92-149">Różne narzędzia Docker</span><span class="sxs-lookup"><span data-stu-id="cfc92-149">Various Docker tools</span></span>
[<span data-ttu-id="cfc92-150">Niektóre narzędzia dużą docker (blog Steve'a Lasker)</span><span class="sxs-lookup"><span data-stu-id="cfc92-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="cfc92-151">Artykuły dobra</span><span class="sxs-lookup"><span data-stu-id="cfc92-151">Good articles</span></span>
[<span data-ttu-id="cfc92-152">Wprowadzenie tooMicroservices z NGINX</span><span class="sxs-lookup"><span data-stu-id="cfc92-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="cfc92-153">Prezentacje</span><span class="sxs-lookup"><span data-stu-id="cfc92-153">Presentations</span></span>
* [<span data-ttu-id="cfc92-154">Steve Lasker: VS Wyszków 2016 - Docker e2e na żywo</span><span class="sxs-lookup"><span data-stu-id="cfc92-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="cfc92-155">Wprowadzenie tooASP.NET Core @ kompilacji 2016 - gdzie możesz w pokaz</span><span class="sxs-lookup"><span data-stu-id="cfc92-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="cfc92-156">Tworzenie aplikacji .NET w kontenerach, Channel 9</span><span class="sxs-lookup"><span data-stu-id="cfc92-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
