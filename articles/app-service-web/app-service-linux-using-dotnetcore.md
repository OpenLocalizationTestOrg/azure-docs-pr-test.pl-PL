---
title: aaaUse .NET Core w aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="6cb62-104">Używanie .NET Core w aplikacji sieci web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6cb62-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="6cb62-105">[Sieci Web aplikacji](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) w systemie Linux udostępnia usługi hostingu sieci web wysoce skalowalną, własnym stosowania poprawek za pomocą systemu operacyjnego Linux hello.</span><span class="sxs-lookup"><span data-stu-id="6cb62-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="6cb62-106">Ten samouczek zawiera instrukcje krok po kroku przedstawiający sposób toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) aplikacji w aplikacji sieci web platformy Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6cb62-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Aplikacja sieci Web w systemie Linux][10]

<span data-ttu-id="6cb62-108">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="6cb62-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cb62-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6cb62-109">Prerequisites</span></span> ##

<span data-ttu-id="6cb62-110">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="6cb62-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="6cb62-111">Zainstaluj hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="6cb62-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="6cb62-112">Zainstaluj [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="6cb62-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="6cb62-113">Tworzenie aplikacji platformy .NET Core lokalnej</span><span class="sxs-lookup"><span data-stu-id="6cb62-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="6cb62-114">Rozpocznij nową sesję terminala.</span><span class="sxs-lookup"><span data-stu-id="6cb62-114">Start a new terminal session.</span></span> <span data-ttu-id="6cb62-115">Utwórz katalog o nazwie `hellodotnetcore`i zmień hello bieżącego katalogu tooit.</span><span class="sxs-lookup"><span data-stu-id="6cb62-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="6cb62-116">Następnie wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6cb62-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="6cb62-117">To polecenie tworzy trzy pliki (*hellodotnetcore.csproj*, *Program.cs*, i *Startup.cs*) i jeden pusty folder (*wwwroot /*) w obszarze hello bieżącego katalogu.</span><span class="sxs-lookup"><span data-stu-id="6cb62-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="6cb62-118">Witaj zawartości `.csproj` plik powinien wyglądać jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="6cb62-118">hello content of `.csproj` file should look like hello following:</span></span> 

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

<span data-ttu-id="6cb62-119">Ponieważ ta aplikacja to aplikacja sieci web, tooan odwołanie do pakietu platformy ASP.NET Core została automatycznie dodana toohello *hellodotnetcore.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="6cb62-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="6cb62-120">numer wersji pakietu hello Hello jest ustawiona zgodnie z toohello wybrany framework.</span><span class="sxs-lookup"><span data-stu-id="6cb62-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="6cb62-121">W tym przykładzie odwołuje się do platformy ASP.NET Core wersji 1.1.2 ponieważ .NET Core 1.1 jest używany.</span><span class="sxs-lookup"><span data-stu-id="6cb62-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="6cb62-122">Tworzenie i testowanie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="6cb62-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="6cb62-123">Możesz skompilować i uruchamianie aplikacji .NET Core hello `dotnet restore` polecenia następuje hello `dotnet run` polecenia, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6cb62-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="6cb62-124">Po uruchomieniu aplikacji hello wyświetla komunikat informujący, że aplikacja hello nasłuchuje żądań tooincoming w porcie.</span><span class="sxs-lookup"><span data-stu-id="6cb62-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="6cb62-125">Ją przetestować, przeglądając zbyt`http://localhost:5000/` przy użyciu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6cb62-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="6cb62-126">Jeśli wszystko działa prawidłowo, zobacz "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="6cb62-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="6cb62-127">jako tekst wynikowy hello.</span><span class="sxs-lookup"><span data-stu-id="6cb62-127">as hello result text.</span></span>

![Test z przeglądarki][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="6cb62-129">Tworzenie aplikacji platformy .NET Core w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6cb62-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="6cb62-130">Najpierw należy toocreate pustą aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cb62-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="6cb62-131">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) i utworzyć nową [aplikacji sieci Web w systemie Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="6cb62-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Tworzenie aplikacji sieci web][1]

<span data-ttu-id="6cb62-133">Gdy hello **Utwórz** zostanie otwarta strona, zawierają szczegółowe informacje o aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="6cb62-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Wybieranie stosu środowiska uruchomieniowego .NET Core][2]

<span data-ttu-id="6cb62-135">Użyj hello poniższej tabeli jako toofill przewodnik, limit hello **Utwórz** strony, a następnie wybierz **OK** i **Utwórz** toocreate hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cb62-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="6cb62-136">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="6cb62-136">Setting</span></span>      | <span data-ttu-id="6cb62-137">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="6cb62-137">Suggested value</span></span>  | <span data-ttu-id="6cb62-138">Opis</span><span class="sxs-lookup"><span data-stu-id="6cb62-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="6cb62-139">Nazwa aplikacji</span><span class="sxs-lookup"><span data-stu-id="6cb62-139">App name</span></span> | <span data-ttu-id="6cb62-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="6cb62-140">hellodotnetcore</span></span>  | <span data-ttu-id="6cb62-141">Witaj Nazwa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cb62-141">hello name of your app.</span></span> <span data-ttu-id="6cb62-142">Ta nazwa musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="6cb62-142">This name must be unique.</span></span> |
| <span data-ttu-id="6cb62-143">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="6cb62-143">Subscription</span></span> | <span data-ttu-id="6cb62-144">Wybierz istniejącą subskrypcję</span><span class="sxs-lookup"><span data-stu-id="6cb62-144">Choose an existing subscription</span></span> | <span data-ttu-id="6cb62-145">Witaj subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb62-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="6cb62-146">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="6cb62-146">Resource Group</span></span> | <span data-ttu-id="6cb62-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6cb62-147">myResourceGroup</span></span> |  <span data-ttu-id="6cb62-148">Witaj zasobów platformy Azure grupy toocontain hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cb62-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="6cb62-149">Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="6cb62-149">App Service Plan</span></span> | <span data-ttu-id="6cb62-150">Nazwę istniejącego planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="6cb62-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="6cb62-151">Witaj planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cb62-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="6cb62-152">Skonfiguruj kontener</span><span class="sxs-lookup"><span data-stu-id="6cb62-152">Configure Container</span></span> | <span data-ttu-id="6cb62-153">Oprogramowanie .NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="6cb62-153">.NET Core 1.1</span></span> | <span data-ttu-id="6cb62-154">Typ kontenera dla tej aplikacji sieci web Hello: rejestru wbudowanych, Docker lub prywatnych.</span><span class="sxs-lookup"><span data-stu-id="6cb62-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="6cb62-155">Źródło obrazu</span><span class="sxs-lookup"><span data-stu-id="6cb62-155">Image source</span></span>  | <span data-ttu-id="6cb62-156">Wbudowane</span><span class="sxs-lookup"><span data-stu-id="6cb62-156">Built-in</span></span>  |  <span data-ttu-id="6cb62-157">Źródło Hello hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="6cb62-157">hello source of hello image.</span></span> |
| <span data-ttu-id="6cb62-158">Środowisko uruchomieniowe stosu</span><span class="sxs-lookup"><span data-stu-id="6cb62-158">Runtime Stack</span></span>  | <span data-ttu-id="6cb62-159">Oprogramowanie .NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="6cb62-159">.NET Core 1.1</span></span>  | <span data-ttu-id="6cb62-160">stos środowiska uruchomieniowego Hello i wersji.</span><span class="sxs-lookup"><span data-stu-id="6cb62-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="6cb62-161">Wdrażanie aplikacji przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="6cb62-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="6cb62-162">Git toodeploy hello .NET Core aplikacji tooAzure aplikację usługi aplikacji sieci Web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6cb62-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="6cb62-163">Hello nowej aplikacji sieci web platformy Azure jest już skonfigurowany wdrożenia usługi Git.</span><span class="sxs-lookup"><span data-stu-id="6cb62-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="6cb62-164">Adres URL wdrożenia Git hello znajdziesz przechodząc toohello następującego adresu URL po wstawieniu nazwę aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="6cb62-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="6cb62-165">adres URL Git Hello ma powitania po formularz bazujący na nazwę aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="6cb62-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="6cb62-166">Uruchom następujące polecenia toodeploy hello miejscowego tooyour aplikacji sieci web Azure hello:</span><span class="sxs-lookup"><span data-stu-id="6cb62-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="6cb62-167">Nie ma potrzeby toopush wszystkie pliki w obszarze *bin /* lub *obj /* katalogów aplikacji są wbudowane w chmurze powitania po hello aplikacji tooAzure przesyłanych plików źródłowych.</span><span class="sxs-lookup"><span data-stu-id="6cb62-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="6cb62-168">Po zakończeniu procesu kompilacji hello pliki binarne są kopiowane do katalogu aplikacji hello */home/lokacji/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="6cb62-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="6cb62-169">Upewnij się, że operacje zdalnego wdrażania hello Raport powodzenie.</span><span class="sxs-lookup"><span data-stu-id="6cb62-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="6cb62-170">Operacje wypychania może potrwać od pakietu rozwiązania i uruchomić w chmurze hello proces kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6cb62-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="6cb62-171">Zobaczysz kilka komunikatów o stanie, między innymi informujący, że pliki zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="6cb62-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="6cb62-172">Witaj dane wyjściowe powinny wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="6cb62-172">hello output should look similar toohello following:</span></span>

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="6cb62-173">Po zakończeniu wdrażania hello, ponownie uruchom aplikację sieci web dla efektu tootake wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="6cb62-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="6cb62-174">toodo, przejdź toohello portalu Azure i przejdź toohello **omówienie** strony aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cb62-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="6cb62-175">Wybierz hello **ponowne uruchomienie** przycisk na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="6cb62-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="6cb62-176">Gdy w oknie podręcznym zostaną wyświetlone, wybierz **tak** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="6cb62-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="6cb62-177">Następnie można przeglądać aplikacji sieci web, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6cb62-177">You can then browse your web app, as shown here:</span></span>

![Przeglądanie .NET Core aplikacja wdrożona tooAzure usługi aplikacji w systemie Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="6cb62-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cb62-179">Next steps</span></span>
* [<span data-ttu-id="6cb62-180">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="6cb62-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
