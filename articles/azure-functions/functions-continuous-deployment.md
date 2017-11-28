---
title: "Ciągłe wdrażanie dla usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Publikowanie funkcji platformy Azure przy użyciu urządzenia ciągłego wdrażania usługi Azure App Service."
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
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="96a2c-103">Ciągłe wdrażanie dla usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="96a2c-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="96a2c-104">Środowisko Azure Functions ułatwia wdrażanie aplikacji funkcji przy użyciu ciągłej integracji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="96a2c-105">Funkcje integruje się z BitBucket, Dropbox, GitHub i Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="96a2c-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="96a2c-106">Dzięki temu przepływu pracy gdzie kod funkcji aktualizacji przy użyciu jednej z tych wdrażanie wyzwalaczy zintegrowanych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="96a2c-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="96a2c-107">Jeśli jesteś nowym użytkownikiem usługi Azure Functions, Rozpocznij od [Azure Functions — omówienie](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="96a2c-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="96a2c-108">Ciągłe wdrażanie to doskonałe rozwiązanie dla projektów, w których ma miejsce częste współtworzenie wielu treści.</span><span class="sxs-lookup"><span data-stu-id="96a2c-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="96a2c-109">Umożliwia on również Obsługa kontroli źródła na kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="96a2c-110">Obecnie obsługiwane są następujące źródła wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="96a2c-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="96a2c-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="96a2c-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="96a2c-112">Skrzynki</span><span class="sxs-lookup"><span data-stu-id="96a2c-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="96a2c-113">Repozytorium zewnętrznego (Git lub Mercurial)</span><span class="sxs-lookup"><span data-stu-id="96a2c-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="96a2c-114">Lokalne repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="96a2c-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="96a2c-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="96a2c-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="96a2c-116">Usługi OneDrive</span><span class="sxs-lookup"><span data-stu-id="96a2c-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="96a2c-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="96a2c-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="96a2c-118">Wdrożenia są konfigurowane na poszczególnych funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="96a2c-119">Po włączeniu ciągłego wdrażania dostępu do kodu funkcji w portalu jest równa *tylko do odczytu*.</span><span class="sxs-lookup"><span data-stu-id="96a2c-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="96a2c-120">Wymagania dotyczące ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="96a2c-120">Continuous deployment requirements</span></span>

<span data-ttu-id="96a2c-121">W źródle wdrożenia przed skonfigurowaniem ciągłe wdrażanie musi mieć źródło wdrożenia skonfigurowane i kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="96a2c-122">We wdrożeniu aplikacji daną funkcję każdej funkcji znajduje się w podkatalogu o nazwie, gdzie nazwa katalogu jest nazwa funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="96a2c-123">Konfigurowanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="96a2c-123">Set up continuous deployment</span></span>
<span data-ttu-id="96a2c-124">Użyj tej procedury, aby skonfigurować ciągłego wdrażania dla istniejącej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="96a2c-125">Te kroki prezentują integracji z repozytorium GitHub, ale podobne kroki zastosować Visual Studio Team Services lub innych usługach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="96a2c-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="96a2c-126">W swoją aplikację przy użyciu funkcji [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="96a2c-128">Następnie w **wdrożeń** kliknij bloku **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="96a2c-130">W **źródło wdrożenia** bloku, kliknij przycisk **wybierz źródło**, następnie wypełnij informacje dotyczące źródła wybranego wdrożenia i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Wybierz źródło wdrożenia](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="96a2c-132">Po skonfigurowaniu ciągłego wdrażania, wszystkie zmiany w pliku w źródle wdrożenia są kopiowane do aplikacji funkcji i wdrażania witrynę w trybie pełnym zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="96a2c-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="96a2c-133">Witryny jest wdrożone podczas aktualizacji plików w źródle.</span><span class="sxs-lookup"><span data-stu-id="96a2c-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="96a2c-134">Opcje wdrażania</span><span class="sxs-lookup"><span data-stu-id="96a2c-134">Deployment options</span></span>

<span data-ttu-id="96a2c-135">Poniżej przedstawiono niektóre typowe wdrożeń:</span><span class="sxs-lookup"><span data-stu-id="96a2c-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="96a2c-136">Tworzenie tymczasowych wdrożenia</span><span class="sxs-lookup"><span data-stu-id="96a2c-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="96a2c-137">Przenieś istniejących funkcji ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="96a2c-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="96a2c-138">Tworzenie tymczasowych wdrożenia</span><span class="sxs-lookup"><span data-stu-id="96a2c-138">Create a staging deployment</span></span>

<span data-ttu-id="96a2c-139">Funkcja aplikacji jeszcze nie obsługuje miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="96a2c-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="96a2c-140">Można jednak nadal zarządzać oddzielnych wdrożeń tymczasowych i produkcyjnych przy użyciu ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="96a2c-141">Proces konfigurowania i pracować z wdrażania przejściowego wygląda zazwyczaj następująco:</span><span class="sxs-lookup"><span data-stu-id="96a2c-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="96a2c-142">Utwórz dwie aplikacje funkcji w subskrypcji, jeden dla kodu produkcyjnego i jeden dla przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="96a2c-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="96a2c-143">Utwórz źródło wdrożenia, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="96a2c-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="96a2c-144">W tym przykładzie użyto [GitHub].</span><span class="sxs-lookup"><span data-stu-id="96a2c-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="96a2c-145">Dla aplikacji funkcja produkcji, pełną kroki **skonfigurowano ciągłe wdrażanie** i ustaw gałąź wdrożenia do głównej gałęzi repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="96a2c-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Wybierz gałąź wdrożenia](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="96a2c-147">Powtórz ten krok dla tymczasowej aplikacjami funkcji, ale wybierz tymczasowej gałęzi zamiast w Twojego repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="96a2c-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="96a2c-148">Jeśli źródło wdrożenia nie obsługuje tworzenia rozgałęzień, należy użyć innego folderu.</span><span class="sxs-lookup"><span data-stu-id="96a2c-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="96a2c-149">Aktualizowanie kodu tymczasowej gałęzi lub folder, a następnie sprawdź, czy te zmiany zostaną odzwierciedlone w tymczasowej wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="96a2c-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="96a2c-150">Po zakończeniu testowania, Scal zmiany w tymczasowej gałęzi głównej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="96a2c-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="96a2c-151">Tę operację scalania wyzwala wdrożenia do produkcji funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="96a2c-152">Jeśli źródło wdrożenia nie obsługuje gałęzie, Zastąp pliki w folderze produkcji pliki z folderu przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="96a2c-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="96a2c-153">Przenieś istniejących funkcji ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="96a2c-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="96a2c-154">Jeśli masz istniejące funkcje, które ma być tworzone i obsługiwane w portalu, należy pobrać istniejących plików kodu funkcji za pomocą protokołu FTP lub lokalnego repozytorium Git przed można skonfigurować ciągłego wdrażania, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="96a2c-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="96a2c-155">Można to zrobić w ustawieniach usługi aplikacji — dla aplikacji funkcja.</span><span class="sxs-lookup"><span data-stu-id="96a2c-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="96a2c-156">Po pobraniu plików, może przekazywać je do źródła wybrany ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="96a2c-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="96a2c-157">Po skonfigurowaniu integracji ciągłej już będzie możliwości edytowania plików źródłowych w portalu funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="96a2c-158">Porady: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="96a2c-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="96a2c-159">Porady: pobieranie plików przy użyciu FTP</span><span class="sxs-lookup"><span data-stu-id="96a2c-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="96a2c-160">Porady: pobieranie plików przy użyciu lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="96a2c-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="96a2c-161">Porady: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="96a2c-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="96a2c-162">Przed pobraniem plików z aplikacji funkcji za pomocą protokołu FTP lub lokalnego repozytorium Git, należy skonfigurować poświadczenia dostępu do witryny.</span><span class="sxs-lookup"><span data-stu-id="96a2c-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="96a2c-163">Poświadczenia są ustawione na poziomie aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="96a2c-164">Aby ustawić poświadczenia wdrażania w portalu Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="96a2c-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="96a2c-165">W swoją aplikację przy użyciu funkcji [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Konfigurowanie poświadczeń wdrożenia lokalnego](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="96a2c-167">Wpisz nazwę użytkownika i hasło, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="96a2c-168">Te poświadczenia można teraz używać dostęp do aplikacji funkcji z FTP lub wbudowanych repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="96a2c-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="96a2c-169">Porady: pobieranie plików przy użyciu FTP</span><span class="sxs-lookup"><span data-stu-id="96a2c-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="96a2c-170">W swoją aplikację przy użyciu funkcji [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **właściwości**, następnie skopiować wartości **użytkownika serwera FTP/wdrożenia**, **nazwa hosta FTP**, i **nazwy hosta FTPS**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="96a2c-171">**Użytkownika serwera FTP/wdrożenia** należy podać wyświetlaną w portalu, w tym nazwę aplikacji w celu zapewnienia prawidłowego kontekstu dla serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="96a2c-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Uzyskaj informacje wdrożenia](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="96a2c-173">Z tego klienta FTP należy użyć informacji o połączeniu zebranych Aby podłączyć się do aplikacji i Pobierz pliki źródłowe dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="96a2c-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="96a2c-174">Porady: pobieranie plików przy użyciu lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="96a2c-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="96a2c-175">W swoją aplikację przy użyciu funkcji [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="96a2c-177">Następnie w **wdrożeń** kliknij bloku **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="96a2c-179">W **źródło wdrożenia** bloku, kliknij przycisk **repozytorium Git lokalnego** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="96a2c-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="96a2c-180">W **funkcji platformy**, kliknij przycisk **właściwości** i zanotuj wartość adresu URL Git.</span><span class="sxs-lookup"><span data-stu-id="96a2c-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="96a2c-182">Klonuj repozytorium na komputerze lokalnym przy użyciu wiersza polecenia programu Git-aware lub ulubionego narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="96a2c-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="96a2c-183">Polecenie klonowania Git wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="96a2c-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="96a2c-184">Pobieranie plików z aplikacji funkcja klonu komputera lokalnego, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="96a2c-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="96a2c-185">Jeśli jest to wymagane, podaj użytkownika [skonfigurowane poświadczenia wdrażania](#credentials).</span><span class="sxs-lookup"><span data-stu-id="96a2c-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="96a2c-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="96a2c-186">[GitHub]: https://github.com/</span></span>
