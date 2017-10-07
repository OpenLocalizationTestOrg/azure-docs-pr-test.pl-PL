---
title: aaaCreate aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
description: "W tym samouczku przedstawiono, jak toocreate platformy ASP.NET Core sieci web przy użyciu programu Visual Studio Code aplikacji."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="92864-103">Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="92864-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="92864-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="92864-104">Overview</span></span>
<span data-ttu-id="92864-105">Ten samouczek pokazuje, jak toocreate platformy ASP.NET Core sieci web przy użyciu aplikacji [programu Visual Studio (kod VS)](http://code.visualstudio.com//Docs/whyvscode) i wdróż je za[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="92864-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="92864-106">Chociaż ten artykuł dotyczy aplikacji tooweb, ma również zastosowanie tooAPI aplikacji i aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="92864-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="92864-107">Platformy ASP.NET Core to znaczące one programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92864-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="92864-108">Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia aplikacji sieci web opartych na chmurze nowoczesnych przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="92864-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="92864-109">Aby uzyskać więcej informacji, zobacz [tooASP.NET wprowadzenie Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="92864-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="92864-110">Informacje o aplikacji sieci web w usłudze Azure App Service, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92864-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="92864-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92864-111">Prerequisites</span></span>
* <span data-ttu-id="92864-112">Zainstaluj [kodzie VS](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="92864-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="92864-113">Zainstaluj usługę Git — można ją zainstalować, korzystając z jednej z tych lokalizacji: [Chocolatey](https://chocolatey.org/packages/git) lub [git scm.com](http://git-scm.com/downloads). W przypadku nowych tooGit wybierz [git scm.com](http://git-scm.com/downloads) i wybierz opcję hello zbyt**Git użycia z wiersza polecenia systemu Windows hello**.</span><span class="sxs-lookup"><span data-stu-id="92864-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="92864-114">Po zainstalowaniu programu Git, należy również tooset hello Git użytkownika nazwę i adres e-mail jest wymagane później w samouczku hello (przeprowadzania zatwierdzenia z kodu VS).</span><span class="sxs-lookup"><span data-stu-id="92864-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="92864-115">Instalowanie platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="92864-115">Install ASP.NET Core</span></span>
<span data-ttu-id="92864-116">Platformy ASP.NET Core jest gotowa stosu .NET do tworzenia nowoczesnych chmury i aplikacji sieci web, które można uruchamiać na OS X, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="92864-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="92864-117">Go został utworzony z hello tła się tooprovide platforma programistyczna zoptymalizowany dla aplikacji, które są albo chmury wdrożonej toohello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="92864-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="92864-118">Składa się z moduły składniki przy minimalnym obciążeniu, aby zachować elastyczność podczas konstruowania rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="92864-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="92864-119">W tym samouczku jest zaprojektowana tooget rozpoczęciem tworzenia aplikacji hello najnowsze wersje rozwoju platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="92864-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="92864-120">Witaj, postępując zgodnie z instrukcjami są określone tooWindows.</span><span class="sxs-lookup"><span data-stu-id="92864-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="92864-121">Aby uzyskać instrukcje instalacji na OS X, Linux i Windows, zobacz [wprowadzenie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="92864-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="92864-122">Aby uzyskać szczegółowe instrukcje dotyczące instalacji, OS X, Linux i Windows, temacie [instalowanie platformy ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="92864-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="92864-123">Tworzenie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="92864-123">Create hello web app</span></span>
<span data-ttu-id="92864-124">W tej sekcji przedstawiono, jak tooscaffold nowej aplikacji platformy ASP.NET sieci web za pomocą narzędzia interfejsu wiersza polecenia .NET hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92864-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="92864-125">Wprowadź poniżej hello na powitania wiersza polecenia toocreate hello projektu folderu i szkieletu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92864-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![platformy CLI - generatora platformy ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="92864-127">toorestore hello niezbędne pakiety NuGet, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="92864-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="92864-128">Uruchamianie aplikacji sieci web hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="92864-128">Run hello web app locally</span></span>
<span data-ttu-id="92864-129">Teraz, utworzono aplikację sieci web hello i pobrać wszystkie pakiety NuGet hello aplikacji hello hello aplikacji sieci web można uruchomić lokalnie.</span><span class="sxs-lookup"><span data-stu-id="92864-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="92864-130">Uruchamianie aplikacji hello (hello `dotnet run` polecenia zostanie tworzenie aplikacji hello, gdy jest nieaktualny):</span><span class="sxs-lookup"><span data-stu-id="92864-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="92864-131">Otwórz przeglądarkę i przejdź toohello następującego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="92864-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="92864-132">**http://localhost: 5000**</span><span class="sxs-lookup"><span data-stu-id="92864-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="92864-133">następujący zostanie wyświetlona strona domyślna Hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="92864-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Aplikacji lokalnej sieci web w przeglądarce](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="92864-135">Zamknij przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="92864-135">Close your browser.</span></span> <span data-ttu-id="92864-136">W hello **okno polecenia**, naciśnij klawisz **klawisze Ctrl + C** tooshut aplikacji hello i zamknij hello **okno polecenia**.</span><span class="sxs-lookup"><span data-stu-id="92864-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="92864-137">Tworzenie aplikacji sieci web w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="92864-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="92864-138">Witaj następujące kroki przeprowadzi Cię przez proces tworzenia aplikacji sieci web w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="92864-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="92864-139">Zaloguj się za toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92864-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="92864-140">Kliknij przycisk **nowy** na powitania lewym górnym rogu hello portalu.</span><span class="sxs-lookup"><span data-stu-id="92864-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="92864-141">Kliknij przycisk **Web Apps > sieci Web aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="92864-141">Click **Web Apps > Web App**.</span></span>
   
    ![Azure nowej aplikacji sieci web](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="92864-143">Wprowadź wartość dla **nazwa**, takich jak **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="92864-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="92864-144">Należy pamiętać, że ta nazwa musi toobe unikatowy i hello portalu będzie wymuszać, który podczas próby tooenter hello nazwa.</span><span class="sxs-lookup"><span data-stu-id="92864-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="92864-145">Dlatego w przypadku wybrania wprowadź inną wartość, konieczne będzie toosubstitute, że wartość dla każdego wystąpienia **SampleWebAppDemo** widoczny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="92864-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="92864-146">Wybierz istniejący **planu usługi App Service** lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="92864-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="92864-147">Jeśli tworzysz nowy plan, wybierz hello warstwa cenowa, lokalizacji i inne opcje.</span><span class="sxs-lookup"><span data-stu-id="92864-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="92864-148">Aby uzyskać więcej informacji na temat planów usługi aplikacji, zobacz artykuł hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92864-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure nowego bloku aplikacja sieci web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="92864-150">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="92864-150">Click **Create**.</span></span>
   
    ![bloku aplikacja sieci Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="92864-152">Włączanie publikowania Git dla hello nowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="92864-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="92864-153">Git to system kontroli wersji rozproszonej służącego toodeploy aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="92864-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="92864-154">Będą przechowywane kod powitania dla aplikacji sieci web w lokalnym repozytorium Git, a w przypadku wdrażania tooAzure Twojego kodu wypychając tooa zdalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="92864-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="92864-155">Zaloguj się do hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92864-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="92864-156">Kliknij pozycję **Browse (Przeglądaj)**.</span><span class="sxs-lookup"><span data-stu-id="92864-156">Click **Browse**.</span></span>
3. <span data-ttu-id="92864-157">Kliknij przycisk **aplikacje sieci Web** tooview listę aplikacji sieci web hello skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92864-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="92864-158">Wybierz aplikację sieci web hello utworzony w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="92864-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="92864-159">W bloku aplikacja sieci web powitania kliknij **ustawienia** > **ciągłe wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="92864-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host aplikacji sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="92864-161">Kliknij przycisk **wybierz źródło > lokalne repozytorium Git**.</span><span class="sxs-lookup"><span data-stu-id="92864-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="92864-162">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="92864-162">Click **OK**.</span></span>
   
    ![Azure lokalnego repozytorium Git](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="92864-164">Jeśli nie ma poświadczeń wdrożenia do publikowania aplikacji sieci web lub innych aplikacji usługi app Service, skonfiguruj je teraz:</span><span class="sxs-lookup"><span data-stu-id="92864-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="92864-165">Kliknij przycisk **ustawienia** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="92864-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="92864-166">Witaj **ustawić poświadczenia wdrażania** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="92864-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="92864-167">Utwórz nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="92864-167">Create a user name and password.</span></span>  <span data-ttu-id="92864-168">To hasło będzie potrzebne później podczas konfigurowania Git.</span><span class="sxs-lookup"><span data-stu-id="92864-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="92864-169">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="92864-169">Click **Save**.</span></span>
9. <span data-ttu-id="92864-170">W bloku aplikacja sieci web, kliknij przycisk **Ustawienia > właściwości**.</span><span class="sxs-lookup"><span data-stu-id="92864-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="92864-171">adres URL Hello hello zdalnego repozytorium Git wdrażanego będzie wyświetlany w obszarze toois **adres URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="92864-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="92864-172">Kopiuj hello **adres URL GIT** wartość do wykorzystania później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="92864-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Adres URL Git platformy Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="92864-174">Publikowanie tooAzure aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="92864-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="92864-175">W tej sekcji utworzysz lokalne repozytorium Git i push z tego repozytorium tooAzure toodeploy tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="92864-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="92864-176">W kodzie VS wybierz hello **Git** opcji hello lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="92864-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Ikona Git w kodzie VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="92864-178">Wybierz **repozytorium git zainicjować** toomake się, że obszar roboczy jest pod kontrolą źródła git.</span><span class="sxs-lookup"><span data-stu-id="92864-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Inicjowanie Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="92864-180">Otwórz hello okno polecenia i zmień katalog toohello katalogów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="92864-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="92864-181">Następnie wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="92864-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="92864-182">To polecenie uniemożliwia problemu o tekstu, w którym są związane z zakończenia CRLF i LF zakończenia.</span><span class="sxs-lookup"><span data-stu-id="92864-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="92864-183">W kodzie VS Dodaj komunikat, zatwierdzania, a następnie kliknij przycisk hello **zatwierdzania wszystkich** Ikona znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="92864-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Git Zatwierdź wszystko](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="92864-185">Po zakończeniu przetwarzania Git zobaczysz, że nie ma żadnych plików wymienionych w oknie Git hello w obszarze **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="92864-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git żadne zmiany](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="92864-187">Zmień wstecz toohello okno polecenia gdzie wiersza polecenia hello wskazuje katalog toohello, gdzie znajduje się aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="92864-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="92864-188">Utwórz zdalnego odwołania do wypychania aplikacji sieci web tooyour aktualizacje za pomocą hello URL Git (kończących ".git"), które wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="92864-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="92864-189">Skonfiguruj poświadczenia Git toosave lokalnie, aby zostaną one automatycznie dołączany tooyour wypychania polecenia wygenerowane z kodu programu VS.</span><span class="sxs-lookup"><span data-stu-id="92864-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="92864-190">Wypchnij tooAzure Twoje zmiany, wprowadzając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="92864-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="92864-191">Po tym tooAzure wypychania początkowej będzie stanie toodo wypychania hello wszystkich poleceń z kodu programu VS.</span><span class="sxs-lookup"><span data-stu-id="92864-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="92864-192">Zostanie wyświetlony monit o hasło hello utworzone wcześniej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="92864-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="92864-193">**Uwaga: Hasła nie będą widoczne.**</span><span class="sxs-lookup"><span data-stu-id="92864-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="92864-194">dane wyjściowe Hello hello powyżej polecenie kończy się z komunikatem, że wdrożenie zakończy się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="92864-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="92864-195">Jeśli wprowadzisz zmiany tooyour aplikacji, można ponownie opublikować bezpośrednio w kodzie VS za pomocą wbudowanej funkcji Git hello wybierając hello **zatwierdzić wszystkie** opcji następuje hello **Push** opcji.</span><span class="sxs-lookup"><span data-stu-id="92864-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="92864-196">Można znaleźć hello **Push** opcja dostępna w hello menu rozwijanego dalej toohello **zatwierdzić wszystkie** i **Odśwież** przycisków.</span><span class="sxs-lookup"><span data-stu-id="92864-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="92864-197">Jeśli potrzebujesz toocollaborate w projekcie, należy rozważyć wypychanie tooGitHub Between wypychanie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="92864-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="92864-198">Uruchamianie aplikacji hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="92864-198">Run hello app in Azure</span></span>
<span data-ttu-id="92864-199">Teraz, możesz wdrożyć aplikację sieci web umożliwia uruchamianie aplikacji hello podczas hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="92864-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="92864-200">Można to zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="92864-200">This can be done in two ways:</span></span>

* <span data-ttu-id="92864-201">Otwórz przeglądarkę i wprowadź następujący hello nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="92864-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="92864-202">W hello portalu Azure Znajdź hello bloku aplikacja sieci web dla aplikacji sieci web i kliknij przycisk **Przeglądaj** tooview aplikacji</span><span class="sxs-lookup"><span data-stu-id="92864-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="92864-203">w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="92864-203">in your default browser.</span></span>

![Aplikacja sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="92864-205">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="92864-205">Summary</span></span>
<span data-ttu-id="92864-206">W tym samouczku można przedstawiono sposób toocreate aplikacji sieci web w kodzie VS i wdróż je tooAzure.</span><span class="sxs-lookup"><span data-stu-id="92864-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="92864-207">Aby uzyskać więcej informacji o kodzie VS, zobacz artykuł hello, [Dlaczego Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="92864-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="92864-208">Informacje o aplikacjach sieci web usługi aplikacji, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92864-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

