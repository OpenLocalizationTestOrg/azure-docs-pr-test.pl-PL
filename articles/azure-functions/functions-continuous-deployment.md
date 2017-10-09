---
title: "wdrożenie usługi Azure Functions aaaContinuous | Dokumentacja firmy Microsoft"
description: "Użyj ciągłego wdrażania urządzenia z usługi aplikacji Azure toopublish funkcji platformy Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="4c15b-103">Ciągłe wdrażanie dla usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4c15b-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="4c15b-104">Azure Functions umożliwia łatwe toodeploy aplikacji funkcji przy użyciu ciągłej integracji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="4c15b-105">Funkcje integruje się z BitBucket, Dropbox, GitHub i Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="4c15b-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="4c15b-106">Dzięki temu przepływu pracy gdzie kod funkcji aktualizacji przy użyciu jednej z tych usług zintegrowanych wyzwalacza wdrożenia tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4c15b-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="4c15b-107">W przypadku nowych funkcji tooAzure rozpoczynać [Azure Functions — omówienie](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c15b-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="4c15b-108">Ciągłe wdrażanie to doskonałe rozwiązanie dla projektów, w których ma miejsce częste współtworzenie wielu treści.</span><span class="sxs-lookup"><span data-stu-id="4c15b-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="4c15b-109">Umożliwia on również Obsługa kontroli źródła na kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="4c15b-110">następujące źródła wdrożenia Hello są obecnie obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="4c15b-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="4c15b-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="4c15b-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="4c15b-112">Skrzynki</span><span class="sxs-lookup"><span data-stu-id="4c15b-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="4c15b-113">Repozytorium zewnętrznego (Git lub Mercurial)</span><span class="sxs-lookup"><span data-stu-id="4c15b-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="4c15b-114">Lokalne repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="4c15b-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="4c15b-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="4c15b-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="4c15b-116">Usługi OneDrive</span><span class="sxs-lookup"><span data-stu-id="4c15b-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="4c15b-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4c15b-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="4c15b-118">Wdrożenia są konfigurowane na poszczególnych funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="4c15b-119">Po włączeniu ciągłe wdrażanie kodu toofunction dostępu w portalu hello ustawiono zbyt*tylko do odczytu*.</span><span class="sxs-lookup"><span data-stu-id="4c15b-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="4c15b-120">Wymagania dotyczące ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="4c15b-120">Continuous deployment requirements</span></span>

<span data-ttu-id="4c15b-121">Musi mieć źródła wdrożenia skonfigurowane i kod funkcji hello źródła wdrożenia przed skonfigurowaniem ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4c15b-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="4c15b-122">We wdrożeniu aplikacji daną funkcję każdej funkcji znajduje się w podkatalogu o nazwie, gdzie nazwa katalogu hello jest nazwą hello hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="4c15b-123">Konfigurowanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="4c15b-123">Set up continuous deployment</span></span>
<span data-ttu-id="4c15b-124">Użyj tej procedury tooconfigure ciągłego wdrażania dla istniejącej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="4c15b-125">Te kroki prezentują integracji z repozytorium GitHub, ale podobne kroki zastosować Visual Studio Team Services lub innych usługach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4c15b-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="4c15b-126">W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="4c15b-128">Następnie w hello **wdrożeń** kliknij bloku **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="4c15b-130">W hello **źródło wdrożenia** bloku, kliknij przycisk **wybierz źródło**, a następnie wypełnij informacje hello źródła wdrożenia wybranej i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Wybierz źródło wdrożenia](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="4c15b-132">Po skonfigurowaniu ciągłego wdrażania, wszystkie zmiany pliku źródła wdrożenia zostaną skopiowane toohello funkcji aplikacji i wdrożenia witrynę w trybie pełnym zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="4c15b-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="4c15b-133">witryny Hello jest wdrożone podczas aktualizacji plików hello źródła.</span><span class="sxs-lookup"><span data-stu-id="4c15b-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="4c15b-134">Opcje wdrażania</span><span class="sxs-lookup"><span data-stu-id="4c15b-134">Deployment options</span></span>

<span data-ttu-id="4c15b-135">Witaj poniżej przedstawiono niektóre typowe wdrożeń:</span><span class="sxs-lookup"><span data-stu-id="4c15b-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="4c15b-136">Tworzenie tymczasowych wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4c15b-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="4c15b-137">Przenieś istniejące wdrożenie toocontinuous funkcji</span><span class="sxs-lookup"><span data-stu-id="4c15b-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="4c15b-138">Tworzenie tymczasowych wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4c15b-138">Create a staging deployment</span></span>

<span data-ttu-id="4c15b-139">Funkcja aplikacji jeszcze nie obsługuje miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4c15b-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="4c15b-140">Można jednak nadal zarządzać oddzielnych wdrożeń tymczasowych i produkcyjnych przy użyciu ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="4c15b-141">Hello tooconfigure procesu i pracy z wdrożeniem przemieszczania wygląda zazwyczaj następująco:</span><span class="sxs-lookup"><span data-stu-id="4c15b-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="4c15b-142">Utwórz dwie aplikacje funkcji w subskrypcji, jeden dla kodu produkcyjnego hello i jeden dla przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="4c15b-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="4c15b-143">Utwórz źródło wdrożenia, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4c15b-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="4c15b-144">W tym przykładzie użyto [GitHub].</span><span class="sxs-lookup"><span data-stu-id="4c15b-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="4c15b-145">Dla aplikacji funkcja produkcji, pełną hello poprzednie kroki **skonfigurowano ciągłe wdrażanie** i zestaw hello wdrożenia gałęzi toohello głównej gałęzi repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c15b-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Wybierz gałąź wdrożenia](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="4c15b-147">Powtórz ten krok dla hello przemieszczania funkcji aplikacji, ale wybierz hello przemieszczania gałęzi zamiast tego w Twojego repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c15b-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="4c15b-148">Jeśli źródło wdrożenia nie obsługuje tworzenia rozgałęzień, należy użyć innego folderu.</span><span class="sxs-lookup"><span data-stu-id="4c15b-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="4c15b-149">Wprowadzić kod tooyour aktualizacje w hello przemieszczania gałęzi lub folderu, a następnie sprawdź, czy te zmiany zostaną odzwierciedlone w hello przemieszczania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4c15b-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="4c15b-150">Po zakończeniu testowania, Scal zmiany z gałęzi przemieszczania hello hello gałęzi głównej.</span><span class="sxs-lookup"><span data-stu-id="4c15b-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="4c15b-151">Tę operację scalania wyzwala wdrożenie toohello produkcji funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="4c15b-152">Jeśli źródło wdrożenia nie obsługuje gałęzie, Zastąp hello pliki w folderze produkcji hello hello pliki z folderu przemieszczania hello.</span><span class="sxs-lookup"><span data-stu-id="4c15b-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="4c15b-153">Przenieś istniejące wdrożenie toocontinuous funkcji</span><span class="sxs-lookup"><span data-stu-id="4c15b-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="4c15b-154">Jeśli masz istniejące funkcje, które utworzono i obsługiwane w portalu hello należy toodownload istniejącą funkcji plików kodu przy użyciu FTP lub hello lokalnego repozytorium Git, zanim można skonfigurować ciągłego wdrażania, jak opisano powyżej.</span><span class="sxs-lookup"><span data-stu-id="4c15b-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="4c15b-155">Można to zrobić w hello ustawień usługi aplikacji — dla aplikacji funkcja.</span><span class="sxs-lookup"><span data-stu-id="4c15b-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="4c15b-156">Po pobraniu plików, możesz przekazać je tooyour wybrane źródło ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4c15b-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="4c15b-157">Po skonfigurowaniu ciągłej integracji będzie już możliwe tooedit źródła plików hello funkcje portalu.</span><span class="sxs-lookup"><span data-stu-id="4c15b-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="4c15b-158">Porady: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4c15b-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="4c15b-159">Porady: pobieranie plików przy użyciu FTP</span><span class="sxs-lookup"><span data-stu-id="4c15b-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="4c15b-160">Porady: pobieranie plików przy użyciu hello lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="4c15b-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="4c15b-161">Porady: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4c15b-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="4c15b-162">Przed pobraniem plików z aplikacji funkcji za pomocą protokołu FTP lub lokalnego repozytorium Git, należy skonfigurować witryny hello tooaccess poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4c15b-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="4c15b-163">Poświadczenia są ustawione na poziomie aplikacji hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="4c15b-164">Użyj hello następujące poświadczenia wdrażania tooset kroki w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4c15b-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="4c15b-165">W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Konfigurowanie poświadczeń wdrożenia lokalnego](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="4c15b-167">Wpisz nazwę użytkownika i hasło, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="4c15b-168">Tooaccess te poświadczenia można teraz używać aplikacji funkcji z FTP lub hello wbudowanych repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="4c15b-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="4c15b-169">Porady: pobieranie plików przy użyciu FTP</span><span class="sxs-lookup"><span data-stu-id="4c15b-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="4c15b-170">W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **właściwości**, następnie skopiować wartości hello **użytkownika serwera FTP/wdrożenia**, **Nazwa hosta FTP**, i **nazwy hosta FTPS**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="4c15b-171">**Użytkownika serwera FTP/wdrożenia** należy podać wyświetlaną w portalu hello, łącznie z nazwą aplikacji hello, tooprovide prawidłowego kontekstu serwera hello FTP.</span><span class="sxs-lookup"><span data-stu-id="4c15b-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Uzyskaj informacje wdrożenia](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="4c15b-173">Z tego klienta FTP Użyj hello połączenia zebranych informacji tooconnect tooyour aplikacji i Pobierz pliki źródłowe hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c15b-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="4c15b-174">Porady: pobieranie plików przy użyciu lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="4c15b-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="4c15b-175">W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="4c15b-177">Następnie w hello **wdrożeń** kliknij bloku **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="4c15b-179">W hello **źródło wdrożenia** bloku, kliknij przycisk **repozytorium Git lokalnego** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c15b-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="4c15b-180">W **funkcji platformy**, kliknij przycisk **właściwości** i zanotuj wartość hello Git adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4c15b-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="4c15b-182">Klonuj repozytorium hello na komputerze lokalnym przy użyciu wiersza polecenia programu Git-aware lub ulubionego narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="4c15b-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="4c15b-183">polecenie klonowania Git Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4c15b-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="4c15b-184">Pobieranie plików z klonu toohello aplikacji z funkcji na komputerze lokalnym, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4c15b-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="4c15b-185">Jeśli jest to wymagane, podaj użytkownika [skonfigurowane poświadczenia wdrażania](#credentials).</span><span class="sxs-lookup"><span data-stu-id="4c15b-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
