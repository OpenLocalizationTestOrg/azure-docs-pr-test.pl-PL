---
title: Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code
description: "W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web platformy ASP.NET Core za pomocą programu Visual Studio Code."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="40148-103">Tworzenie aplikacji sieci web platformy ASP.NET Core w programie Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="40148-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="40148-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="40148-104">Overview</span></span>
<span data-ttu-id="40148-105">W tym samouczku przedstawiono sposób tworzenia platformy ASP.NET Core sieci web app przy użyciu [programu Visual Studio (kod VS)](http://code.visualstudio.com//Docs/whyvscode) i wdrożyć ją [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="40148-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="40148-106">Mimo że ten artykuł dotyczy aplikacji sieci Web, ma również zastosowanie do aplikacji interfejsu API i aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="40148-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="40148-107">Platformy ASP.NET Core to znaczące one programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="40148-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="40148-108">Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia aplikacji sieci web opartych na chmurze nowoczesnych przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="40148-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="40148-109">Aby uzyskać więcej informacji, zobacz [wprowadzenie do platformy ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="40148-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="40148-110">Informacje o aplikacji sieci web w usłudze Azure App Service, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40148-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="40148-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40148-111">Prerequisites</span></span>
* <span data-ttu-id="40148-112">Zainstaluj [kodzie VS](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="40148-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="40148-113">Zainstaluj usługę Git — można ją zainstalować, korzystając z jednej z tych lokalizacji: [Chocolatey](https://chocolatey.org/packages/git) lub [git scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="40148-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="40148-114">Jeśli jesteś nowym użytkownikiem Git, wybierz [git scm.com](http://git-scm.com/downloads) i wybierz opcję **Git użycia z wiersza polecenia systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="40148-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="40148-115">Po zainstalowaniu programu Git, również należy ustawić nazwę użytkownika Git i poczty e-mail, ponieważ jest on niezbędny w dalszej części samouczka (przeprowadzania zatwierdzenia z kodu VS).</span><span class="sxs-lookup"><span data-stu-id="40148-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="40148-116">Instalowanie platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="40148-116">Install ASP.NET Core</span></span>
<span data-ttu-id="40148-117">Platformy ASP.NET Core jest gotowa stosu .NET do tworzenia nowoczesnych chmury i aplikacji sieci web, które można uruchamiać na OS X, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="40148-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="40148-118">Go został utworzony od podstaw w zapewnia platforma programistyczna zoptymalizowany dla aplikacji, które są wdrożone w chmurze lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="40148-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="40148-119">Składa się z moduły składniki przy minimalnym obciążeniu, aby zachować elastyczność podczas konstruowania rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="40148-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="40148-120">Ten samouczek jest przeznaczony do Rozpoczęcie tworzenia aplikacji z najnowszej wersji rozwoju platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="40148-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="40148-121">Poniższe instrukcje dotyczą systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="40148-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="40148-122">Aby uzyskać instrukcje instalacji na OS X, Linux i Windows, zobacz [wprowadzenie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="40148-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="40148-123">Aby uzyskać szczegółowe instrukcje dotyczące instalacji, OS X, Linux i Windows, temacie [instalowanie platformy ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="40148-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="40148-124">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="40148-124">Create the web app</span></span>
<span data-ttu-id="40148-125">W tej sekcji przedstawiono sposób tworzenia szkieletu nowej aplikacji ASP.NET aplikacji sieci web za pomocą narzędzia interfejsu wiersza polecenia platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="40148-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="40148-126">Wprowadź w wierszu polecenia, aby utworzyć folder projektu i utworzyć szkielet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="40148-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![platformy CLI - generatora platformy ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="40148-128">Aby przywrócić wymaganych pakietów NuGet, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40148-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="40148-129">Lokalne uruchamianie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="40148-129">Run the web app locally</span></span>
<span data-ttu-id="40148-130">Teraz, utworzono aplikację sieci web i pobrać wszystkie pakiety NuGet aplikacji dla aplikacji sieci web można uruchomić lokalnie.</span><span class="sxs-lookup"><span data-stu-id="40148-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="40148-131">Uruchom aplikację ( `dotnet run` polecenia będzie kompilowania aplikacji, gdy jest nieaktualny):</span><span class="sxs-lookup"><span data-stu-id="40148-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="40148-132">Otwórz przeglądarkę i przejdź do następującego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="40148-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="40148-133">**http://localhost: 5000**</span><span class="sxs-lookup"><span data-stu-id="40148-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="40148-134">Następujący zostanie wyświetlona strona domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="40148-134">The default page of the web app will appear as follows.</span></span>
   
    ![Aplikacji lokalnej sieci web w przeglądarce](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="40148-136">Zamknij przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="40148-136">Close your browser.</span></span> <span data-ttu-id="40148-137">W **okno polecenia**, naciśnij klawisz **klawisze Ctrl + C** zamknięcia aplikacji i zamknąć **okno polecenia**.</span><span class="sxs-lookup"><span data-stu-id="40148-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="40148-138">Tworzenie aplikacji sieci web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="40148-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="40148-139">Poniższe kroki przeprowadzi Cię przez proces tworzenia aplikacji sieci web w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="40148-140">Zaloguj się do [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40148-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40148-141">Kliknij przycisk **nowy** u góry po lewej części portalu.</span><span class="sxs-lookup"><span data-stu-id="40148-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="40148-142">Kliknij przycisk **Web Apps > sieci Web aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="40148-142">Click **Web Apps > Web App**.</span></span>
   
    ![Azure nowej aplikacji sieci web](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="40148-144">Wprowadź wartość dla **nazwa**, takich jak **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="40148-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="40148-145">Należy pamiętać, że ta nazwa musi być unikatowa i portalu będzie wymuszać który, podczas próby wprowadź nazwę.</span><span class="sxs-lookup"><span data-stu-id="40148-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="40148-146">Dlatego w przypadku wybrania wprowadź inną wartość, należy zastąpić tę wartość dla każdego wystąpienia **SampleWebAppDemo** widoczny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="40148-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="40148-147">Wybierz istniejący **planu usługi App Service** lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="40148-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="40148-148">Jeśli tworzysz nowy plan, wybierz warstwę cenową, lokalizacji i innych opcji.</span><span class="sxs-lookup"><span data-stu-id="40148-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="40148-149">Aby uzyskać więcej informacji na temat planów usługi App Service, zobacz artykuł, [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40148-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure nowego bloku aplikacja sieci web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="40148-151">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="40148-151">Click **Create**.</span></span>
   
    ![bloku aplikacja sieci Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="40148-153">Włączanie publikowania Git dla nowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="40148-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="40148-154">Git to system kontroli wersji rozproszonej, który służy do wdrażania aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="40148-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="40148-155">Utworzony kod dla aplikacji sieci Web zostanie zapisany w lokalnym repozytorium Git i wdrożony na platformie Azure przez wypchnięcie do repozytorium zdalnego.</span><span class="sxs-lookup"><span data-stu-id="40148-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="40148-156">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40148-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40148-157">Kliknij pozycję **Browse (Przeglądaj)**.</span><span class="sxs-lookup"><span data-stu-id="40148-157">Click **Browse**.</span></span>
3. <span data-ttu-id="40148-158">Kliknij przycisk **aplikacje sieci Web** Aby wyświetlić listę aplikacji sieci web skojarzony z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="40148-159">Wybierz utworzony w tym samouczku aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="40148-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="40148-160">W bloku aplikacja sieci web, kliknij przycisk **ustawienia** > **ciągłe wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="40148-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host aplikacji sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="40148-162">Kliknij przycisk **wybierz źródło > lokalne repozytorium Git**.</span><span class="sxs-lookup"><span data-stu-id="40148-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="40148-163">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="40148-163">Click **OK**.</span></span>
   
    ![Azure lokalnego repozytorium Git](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="40148-165">Jeśli nie ma poświadczeń wdrożenia do publikowania aplikacji sieci web lub innych aplikacji usługi app Service, skonfiguruj je teraz:</span><span class="sxs-lookup"><span data-stu-id="40148-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="40148-166">Kliknij przycisk **ustawienia** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="40148-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="40148-167">**Ustawić poświadczenia wdrażania** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="40148-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="40148-168">Utwórz nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="40148-168">Create a user name and password.</span></span>  <span data-ttu-id="40148-169">To hasło będzie potrzebne później podczas konfigurowania Git.</span><span class="sxs-lookup"><span data-stu-id="40148-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="40148-170">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="40148-170">Click **Save**.</span></span>
9. <span data-ttu-id="40148-171">W bloku aplikacja sieci web, kliknij przycisk **Ustawienia > właściwości**.</span><span class="sxs-lookup"><span data-stu-id="40148-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="40148-172">Adres URL zdalnego repozytorium Git, który będzie można wdrożyć do jest wyświetlany w obszarze **adres URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="40148-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="40148-173">Kopiuj **adres URL GIT** wartość do wykorzystania później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="40148-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Adres URL Git platformy Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="40148-175">Publikowanie aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="40148-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="40148-176">W tej sekcji utworzysz lokalne repozytorium Git i wypychania z tego repozytorium na platformie Azure, aby wdrożyć aplikację sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="40148-177">W kodzie VS wybierz **Git** opcji na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="40148-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Ikona Git w kodzie VS](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="40148-179">Wybierz **repozytorium git zainicjować** się upewnić, że obszar roboczy jest pod kontrolą źródła git.</span><span class="sxs-lookup"><span data-stu-id="40148-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Inicjowanie Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="40148-181">Otwórz okno polecenia i przejdź do katalogu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="40148-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="40148-182">Następnie wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40148-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="40148-183">To polecenie uniemożliwia problemu o tekstu, w którym są związane z zakończenia CRLF i LF zakończenia.</span><span class="sxs-lookup"><span data-stu-id="40148-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="40148-184">W kodzie VS Dodaj komunikat, zatwierdzania, a następnie kliknij przycisk **zatwierdzania wszystkich** Ikona znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="40148-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Git Zatwierdź wszystko](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="40148-186">Po zakończeniu przetwarzania Git zobaczysz, że nie ma żadnych plików wymienionych w oknie Git **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="40148-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git żadne zmiany](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="40148-188">Zmień okno polecenia gdzie wiersza polecenia wskazuje katalog, gdzie znajduje się aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="40148-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="40148-189">Utwórz zdalnego odwołania do wypychania aktualizacji do aplikacji sieci web za pomocą URL Git (kończących ".git"), które wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="40148-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="40148-190">Skonfiguruj Git lokalnie zapisywanie poświadczeń, dzięki czemu będzie można automatycznie dołączane do poleceń wypychania wygenerowane z kodu programu VS.</span><span class="sxs-lookup"><span data-stu-id="40148-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="40148-191">Wypchnij zmiany na platformę Azure, wprowadzając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="40148-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="40148-192">Po tej początkowej wypychanych na platformie Azure będzie można wykonać polecenia wypychania za kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="40148-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="40148-193">Zostanie wyświetlony monit o podanie hasła utworzonego wcześniej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="40148-194">**Uwaga: Hasła nie będą widoczne.**</span><span class="sxs-lookup"><span data-stu-id="40148-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="40148-195">Dane wyjściowe z powyższego polecenia kończy się z komunikatem, że wdrożenie zakończy się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="40148-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="40148-196">Jeśli wprowadzisz zmiany do aplikacji, można ponownie opublikować bezpośrednio w kodzie VS za pomocą wbudowanej funkcji Git, wybierając **zatwierdzić wszystkie** opcji następuje **Push** opcji.</span><span class="sxs-lookup"><span data-stu-id="40148-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="40148-197">Można znaleźć **Push** opcji dostępnych w menu rozwijanym obok pozycji **zatwierdzić wszystkie** i **Odśwież** przycisków.</span><span class="sxs-lookup"><span data-stu-id="40148-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="40148-198">Jeśli potrzebujesz współpracować nad projektem, należy rozważyć wypychania w witrynie GitHub Between Wypychanie do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="40148-199">Uruchom aplikację na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="40148-199">Run the app in Azure</span></span>
<span data-ttu-id="40148-200">Teraz, możesz wdrożyć aplikację sieci web umożliwia uruchamianie aplikacji podczas hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="40148-201">Można to zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="40148-201">This can be done in two ways:</span></span>

* <span data-ttu-id="40148-202">Otwórz przeglądarkę i wprowadź nazwę aplikacji sieci web w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="40148-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="40148-203">W portalu Azure Znajdź bloku aplikacja sieci web dla aplikacji sieci web, a następnie kliknij przycisk **Przeglądaj** Aby wyświetlić aplikację</span><span class="sxs-lookup"><span data-stu-id="40148-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="40148-204">w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="40148-204">in your default browser.</span></span>

![Aplikacja sieci web platformy Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="40148-206">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="40148-206">Summary</span></span>
<span data-ttu-id="40148-207">W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web w kodzie VS i wdrożyć go na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40148-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="40148-208">Aby uzyskać więcej informacji o kodzie VS, zobacz artykuł, [Dlaczego Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="40148-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="40148-209">Informacje o aplikacjach sieci web usługi aplikacji, zobacz [Omówienie aplikacji sieci Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40148-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

