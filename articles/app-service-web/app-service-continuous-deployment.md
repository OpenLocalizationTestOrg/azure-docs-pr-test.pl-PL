---
title: "aaaContinuous tooAzure wdrożenia usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable tooAzure ciągłego wdrażania usługi aplikacji."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="31593-103">Ciągłe wdrażanie tooAzure usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="31593-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="31593-104">W tym samouczku przedstawiono sposób tooconfigure przepływu pracy ciągłego wdrażania dla użytkownika [usłudze Azure App Service] aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31593-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="31593-105">Usługi aplikacji integracji z BitBucket, GitHub, i [programu Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) umożliwia ciągłego przepływ pracy wdrożenia, którym Azure ściąga hello najnowsze aktualizacje z projektu opublikowane tooone tych usług.</span><span class="sxs-lookup"><span data-stu-id="31593-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="31593-106">Ciągłe wdrażanie to doskonałe rozwiązanie dla projektów, w których ma miejsce częste współtworzenie wielu treści.</span><span class="sxs-lookup"><span data-stu-id="31593-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="31593-107">toofind się jak tooconfigure ciągłe wdrażanie ręcznie z repozytorium chmury nie są wyświetlane według hello portalu Azure (takich jak [GitLab](https://gitlab.com/)), zobacz [Konfigurowanie ciągłego wdrażania przy użyciu ręczne](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="31593-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="31593-108"><a name="overview"></a>Włącz ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="31593-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="31593-109">tooenable ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="31593-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="31593-110">Publikuj repozytorium zawartości toohello aplikacji, która będzie służyć do ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="31593-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="31593-111">Aby uzyskać więcej informacji na temat publikowania usług toothese projektu, zobacz [Tworzenie repozytorium (GitHub)], [Tworzenie repozytorium (BitBucket)], i [wprowadzenie do programu VSTS].</span><span class="sxs-lookup"><span data-stu-id="31593-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="31593-112">W bloku menu aplikacji w hello [portalu Azure], kliknij przycisk **wdrażania aplikacji > Opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="31593-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="31593-113">Kliknij przycisk **wybierz źródło**, a następnie wybierz pozycję hello źródło wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="31593-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="31593-114">tooconfigure konto programu VSTS dla wdrożenia usługi App Service można znaleźć pod adresem to [samouczek](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="31593-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="31593-115">Hello pełny przepływ pracy autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="31593-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="31593-116">W hello **źródło wdrożenia** bloku, wybierz projekt hello i toodeploy z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="31593-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="31593-117">Gdy skończysz, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="31593-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="31593-118">Podczas włączania ciągłego wdrażania za pomocą usługi GitHub lub BitBucket zostaną wyświetlone zarówno projekty publiczne, jak i prywatne.</span><span class="sxs-lookup"><span data-stu-id="31593-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="31593-119">Usługi aplikacji tworzy skojarzenie z repozytorium wybranego hello, w przypadku plików hello hello określonej gałęzi i obsługuje klonowania repozytorium na aplikację usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31593-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="31593-120">Podczas konfigurowania programu VSTS ciągłego wdrażania od hello portalu Azure hello integracji używa usługi aplikacji hello [aparat wdrażania Kudu](https://github.com/projectkudu/kudu/wiki), który już automatyzuje zadania kompilacji i wdrażania związane z każdego `git push`.</span><span class="sxs-lookup"><span data-stu-id="31593-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="31593-121">Nie trzeba tooseparately skonfigurowano ciągłe wdrażanie w VSTS.</span><span class="sxs-lookup"><span data-stu-id="31593-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="31593-122">Po zakończeniu tego procesu, hello **opcje wdrażania** bloku aplikacji będą wyświetlane aktywne wdrożenie wskazującą wdrażania zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="31593-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="31593-123">Aplikacja hello tooverify zostanie pomyślnie wdrożona, kliknij przycisk hello **adres URL** u góry bloku aplikacji hello w portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="31593-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="31593-124">tooverify ciągłe wdrażanie informacji związanych z repozytorium hello wybranym push repozytorium toohello zmiany.</span><span class="sxs-lookup"><span data-stu-id="31593-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="31593-125">Aplikację należy zaktualizować zmiany hello tooreflect wkrótce po zakończeniu hello wypychania toohello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="31593-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="31593-126">Możesz sprawdzić, czy ma pobierane w aktualizacji hello w hello **opcje wdrażania** bloku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31593-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="31593-127"><a name="VSsolution"></a>Ciągłe wdrażanie za pomocą rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31593-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="31593-128">Wypychanie tooAzure rozwiązania Visual Studio usługi aplikacji jest równie proste jak naciśnięcie plik index.html proste.</span><span class="sxs-lookup"><span data-stu-id="31593-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="31593-129">proces wdrażania usługi aplikacji Hello usprawnia wszystkich szczegółów hello, takich jak przywracanie zależności NuGet i tworzenia plików binarnych aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="31593-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="31593-130">Można stosować najlepsze rozwiązania kontroli źródła hello obsługi kodu tylko w repozytorium Git i umożliwić zajmie się hello rest wdrożenia usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="31593-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="31593-131">Witaj kroki do wypychania tooApp rozwiązania programu Visual Studio, są usługi hello takie same jak hello [poprzedniej sekcji](#overview), pod warunkiem, że możesz skonfigurować rozwiązanie i repozytorium w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="31593-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="31593-132">Użyj hello Visual Studio źródła formantu opcja toogenerate `.gitignore` plików, takich jak hello obraz poniżej lub ręcznie Dodaj `.gitignore` pliku w katalogu głównym repozytorium, z zawartości toothis podobne [próbki .gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="31593-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="31593-133">Dodaj hello całego rozwiązania katalogu drzewa tooyour repozytorium z hello plik .sln w katalogu głównym repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="31593-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="31593-134">Po Konfigurowanie repozytorium, zgodnie z opisem i skonfigurowany aplikacji na platformie Azure do ciągłego publikowania z jednego z hello online repozytoria Git, mogą tworzyć aplikacji ASP.NET lokalnie w programie Visual Studio i stale po prostu przez wdrażanie kodu Wypychanie zmiany tooyour online repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="31593-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="31593-135"><a name="disableCD"></a>Wyłączanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="31593-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="31593-136">toodisable ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="31593-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="31593-137">W bloku menu aplikacji w hello [portalu Azure], kliknij przycisk **wdrażania aplikacji > Opcje wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="31593-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="31593-138">Następnie kliknij przycisk **rozłączenia** w hello **opcje wdrażania** bloku.</span><span class="sxs-lookup"><span data-stu-id="31593-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="31593-139">Po odebraniu **tak** toohello komunikat potwierdzający, możesz wrócić bloku tooyour aplikacji i kliknij przycisk **wdrażania aplikacji > Opcje wdrażania** Jeśli chcesz tooset się publikowanie z innego źródła.</span><span class="sxs-lookup"><span data-stu-id="31593-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31593-140">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="31593-140">Additional Resources</span></span>
* [<span data-ttu-id="31593-141">Jak tooinvestigate typowe problemy związane z ciągłe wdrażanie</span><span class="sxs-lookup"><span data-stu-id="31593-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="31593-142">[Jak toouse programu PowerShell dla usługi Azure]</span><span class="sxs-lookup"><span data-stu-id="31593-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="31593-143">[Jak toouse hello narzędzia wiersza polecenia platformy Azure dla komputerów Mac i Linux]</span><span class="sxs-lookup"><span data-stu-id="31593-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="31593-144">[Dokumentacja usługi Git]</span><span class="sxs-lookup"><span data-stu-id="31593-144">[Git documentation]</span></span>
* [<span data-ttu-id="31593-145">Projekt Kudu</span><span class="sxs-lookup"><span data-stu-id="31593-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="31593-146">Użyj Azure tooautomatically Generowanie CI/CD potoku toodeploy ASP.NET 4 aplikacji</span><span class="sxs-lookup"><span data-stu-id="31593-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="31593-147">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="31593-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="31593-148">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="31593-148">No credit cards required; no commitments.</span></span>
> 
> 

[usłudze Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portalu Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Jak toouse programu PowerShell dla usługi Azure]: /powershell/azureps-cmdlets-docs
[Jak toouse hello narzędzia wiersza polecenia platformy Azure dla komputerów Mac i Linux]:../cli-install-nodejs.md
[Dokumentacja usługi Git]: http://git-scm.com/documentation

[Tworzenie repozytorium (GitHub)]: https://help.github.com/articles/create-a-repo
[Tworzenie repozytorium (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[wprowadzenie do programu VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
