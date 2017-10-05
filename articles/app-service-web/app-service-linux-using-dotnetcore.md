---
title: "Używanie .NET Core w aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft"
description: "Użyj platformy .NET Core w aplikacji sieci Web w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="5dcbc-104">Używanie .NET Core w aplikacji sieci web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5dcbc-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="5dcbc-105">[Sieci Web aplikacji](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) w systemie Linux oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web przy użyciu systemu operacyjnego Linux.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="5dcbc-106">Ten samouczek zawiera instrukcje krok po kroku, pokazujący sposób tworzenia [.NET Core](https://docs.microsoft.com/aspnet/core/) aplikacji w aplikacji sieci web platformy Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Aplikacja sieci Web w systemie Linux][10]

<span data-ttu-id="5dcbc-108">Poniższe kroki możesz wykonać przy użyciu komputera z systemem Mac, Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dcbc-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5dcbc-109">Prerequisites</span></span> ##

<span data-ttu-id="5dcbc-110">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="5dcbc-111">Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="5dcbc-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="5dcbc-112">Zainstaluj [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="5dcbc-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="5dcbc-113">Tworzenie aplikacji platformy .NET Core lokalnej</span><span class="sxs-lookup"><span data-stu-id="5dcbc-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="5dcbc-114">Rozpocznij nową sesję terminala.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-114">Start a new terminal session.</span></span> <span data-ttu-id="5dcbc-115">Utwórz katalog o nazwie `hellodotnetcore`i zmień bieżący katalog.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="5dcbc-116">Następnie wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="5dcbc-117">To polecenie tworzy trzy pliki (*hellodotnetcore.csproj*, *Program.cs*, i *Startup.cs*) i jeden pusty folder (*wwwroot /*) w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="5dcbc-118">Zawartość `.csproj` pliku powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-118">The content of `.csproj` file should look like the following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="5dcbc-119">Ponieważ ta aplikacja to aplikacja sieci web, odwołanie do pakietu platformy ASP.NET Core została automatycznie dodana do *hellodotnetcore.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="5dcbc-120">Numer wersji pakietu jest ustawiona zgodnie z wybranym framework.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="5dcbc-121">W tym przykładzie odwołuje się do platformy ASP.NET Core wersji 1.1.2 ponieważ .NET Core 1.1 jest używany.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="5dcbc-122">Tworzenie i testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="5dcbc-122">Build and test the application locally</span></span> ##

<span data-ttu-id="5dcbc-123">Możesz skompilować i uruchomić aplikację .NET Core z `dotnet restore` polecenia następuje `dotnet run` polecenia, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="5dcbc-124">Podczas uruchamiania aplikacji, wyświetla komunikat informujący, że aplikacja nasłuchuje żądań przychodzących do portu.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="5dcbc-125">Ją przetestować, przechodząc do `http://localhost:5000/` przy użyciu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="5dcbc-126">Jeśli wszystko działa prawidłowo, zobacz "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="5dcbc-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="5dcbc-127">jako tekst wynik.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-127">as the result text.</span></span>

![Test z przeglądarki][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="5dcbc-129">Utwórz .NET Core aplikacji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5dcbc-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="5dcbc-130">Najpierw należy utworzyć pustą aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-130">First you need to create an empty web app.</span></span> <span data-ttu-id="5dcbc-131">Zaloguj się do [portalu Azure](https://portal.azure.com/) i utworzyć nową [aplikacji sieci Web w systemie Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="5dcbc-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Tworzenie aplikacji sieci web][1]

<span data-ttu-id="5dcbc-133">Gdy **Utwórz** zostanie otwarta strona, zawierają szczegółowe informacje o aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-133">When the **Create** page opens, provide details about your web app:</span></span>

![Wybieranie stosu środowiska uruchomieniowego .NET Core][2]

<span data-ttu-id="5dcbc-135">Skorzystaj z poniższej tabeli przedstawiono wskazówki do wypełniania **Utwórz** strony, a następnie wybierz **OK** i **Utwórz** do utworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="5dcbc-136">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="5dcbc-136">Setting</span></span>      | <span data-ttu-id="5dcbc-137">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="5dcbc-137">Suggested value</span></span>  | <span data-ttu-id="5dcbc-138">Opis</span><span class="sxs-lookup"><span data-stu-id="5dcbc-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="5dcbc-139">Nazwa aplikacji</span><span class="sxs-lookup"><span data-stu-id="5dcbc-139">App name</span></span> | <span data-ttu-id="5dcbc-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="5dcbc-140">hellodotnetcore</span></span>  | <span data-ttu-id="5dcbc-141">Nazwa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-141">The name of your app.</span></span> <span data-ttu-id="5dcbc-142">Ta nazwa musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-142">This name must be unique.</span></span> |
| <span data-ttu-id="5dcbc-143">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="5dcbc-143">Subscription</span></span> | <span data-ttu-id="5dcbc-144">Wybierz istniejącą subskrypcję</span><span class="sxs-lookup"><span data-stu-id="5dcbc-144">Choose an existing subscription</span></span> | <span data-ttu-id="5dcbc-145">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-145">The Azure subscription.</span></span> |
| <span data-ttu-id="5dcbc-146">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="5dcbc-146">Resource Group</span></span> | <span data-ttu-id="5dcbc-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5dcbc-147">myResourceGroup</span></span> |  <span data-ttu-id="5dcbc-148">Grupy zasobów platformy Azure w celu uwzględnienia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="5dcbc-149">Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="5dcbc-149">App Service Plan</span></span> | <span data-ttu-id="5dcbc-150">Nazwę istniejącego planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="5dcbc-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="5dcbc-151">Plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-151">The App Service plan.</span></span>  |
| <span data-ttu-id="5dcbc-152">Skonfiguruj kontener</span><span class="sxs-lookup"><span data-stu-id="5dcbc-152">Configure Container</span></span> | <span data-ttu-id="5dcbc-153">Oprogramowanie .NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="5dcbc-153">.NET Core 1.1</span></span> | <span data-ttu-id="5dcbc-154">Typ kontenera dla tej aplikacji sieci web: rejestru wbudowanych, Docker lub prywatnych.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="5dcbc-155">Źródło obrazu</span><span class="sxs-lookup"><span data-stu-id="5dcbc-155">Image source</span></span>  | <span data-ttu-id="5dcbc-156">Wbudowane</span><span class="sxs-lookup"><span data-stu-id="5dcbc-156">Built-in</span></span>  |  <span data-ttu-id="5dcbc-157">Źródło obrazu.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-157">The source of the image.</span></span> |
| <span data-ttu-id="5dcbc-158">Środowisko uruchomieniowe stosu</span><span class="sxs-lookup"><span data-stu-id="5dcbc-158">Runtime Stack</span></span>  | <span data-ttu-id="5dcbc-159">Oprogramowanie .NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="5dcbc-159">.NET Core 1.1</span></span>  | <span data-ttu-id="5dcbc-160">Stos środowiska uruchomieniowego i wersji.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="5dcbc-161">Wdrażanie aplikacji przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="5dcbc-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="5dcbc-162">Git umożliwia wdrażanie aplikacji .NET Core aplikację sieci Web usługi aplikacji Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="5dcbc-163">W nowej aplikacji sieci web platformy Azure jest już wdrażanie Git jest skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="5dcbc-164">Adres URL wdrożenia Git znajdziesz przechodząc pod następujący adres URL po wstawieniu nazwę aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="5dcbc-165">Adres URL Git ma następujący format oparte na nazwę aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="5dcbc-166">Uruchom następujące polecenia, aby wdrożyć aplikację lokalną do aplikacji sieci web platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="5dcbc-167">Nie trzeba push wszystkie pliki w obszarze *bin /* lub *obj /* katalogów aplikacji są wbudowane w chmurze, gdy pliki źródłowe aplikacji są przenoszone do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="5dcbc-168">Po zakończeniu procesu kompilacji plików binarnych, są kopiowane do katalogu aplikacji na */home/lokacji/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="5dcbc-169">Upewnij się, że operacje zdalnego wdrażania raportu Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="5dcbc-170">Operacje wypychania może potrwać od pakietu rozwiązania i działają w chmurze proces kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="5dcbc-171">Zobaczysz kilka komunikatów o stanie, między innymi informujący, że pliki zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="5dcbc-172">Dane wyjściowe powinny wyglądać podobnie do poniższej:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-172">The output should look similar to the following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="5dcbc-173">Po zakończeniu wdrożenia należy ponownie uruchomić aplikacji sieci web do wdrożenia zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="5dcbc-174">Aby to zrobić, przejdź do portalu Azure i przejdź do **omówienie** strony aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="5dcbc-175">Wybierz **ponowne uruchomienie** przycisku na stronie.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="5dcbc-176">Gdy w oknie podręcznym zostaną wyświetlone, wybierz **tak** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="5dcbc-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="5dcbc-177">Następnie można przeglądać aplikacji sieci web, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="5dcbc-177">You can then browse your web app, as shown here:</span></span>

![Przeglądanie aplikacji .NET Core wdrożony w usłudze Azure App Service w systemie Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="5dcbc-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5dcbc-179">Next steps</span></span>
* [<span data-ttu-id="5dcbc-180">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5dcbc-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
