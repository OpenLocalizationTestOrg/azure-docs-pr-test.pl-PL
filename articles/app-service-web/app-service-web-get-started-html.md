---
title: aaaCreate statyczne HTML aplikacji sieci web na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorun aplikacje sieci web w usłudze Azure App Service, wdrażając statycznego HTML przykładową aplikację."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="53539-103">Tworzenie statycznej aplikacji sieci Web w języku HTML na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="53539-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="53539-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="53539-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="53539-105">Tego przewodnika Szybki Start pokazuje, jak toodeploy podstawowe HTML + CSS lokacji tooAzure aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="53539-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="53539-106">Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web zawartości toohello Git toodeploy próbki kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="53539-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="53539-108">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="53539-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="53539-109">Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.</span><span class="sxs-lookup"><span data-stu-id="53539-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53539-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="53539-110">Prerequisites</span></span>

<span data-ttu-id="53539-111">toocomplete tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="53539-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="53539-112">[Zainstaluj oprogramowanie Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="53539-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="53539-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="53539-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="53539-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="53539-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="53539-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53539-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="53539-116">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="53539-116">Download hello sample</span></span>

<span data-ttu-id="53539-117">W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="53539-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="53539-118">Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="53539-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="53539-119">Witaj widok HTML</span><span class="sxs-lookup"><span data-stu-id="53539-119">View hello HTML</span></span>

<span data-ttu-id="53539-120">Przejdź toohello katalog, który zawiera przykładowy hello HTML.</span><span class="sxs-lookup"><span data-stu-id="53539-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="53539-121">Otwórz hello *index.html* plik w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="53539-121">Open hello *index.html* file in your browser.</span></span>

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji sieci Web](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="53539-124">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="53539-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="53539-125">Przeglądaj toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="53539-125">Browse toohello app</span></span>

<span data-ttu-id="53539-126">W przeglądarce odwiedź adres URL aplikacji sieci web platformy Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="53539-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="53539-127">Strona Hello jest uruchomiona jako aplikacja sieci web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="53539-127">hello page is running as an Azure App Service web app.</span></span>

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="53539-129">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="53539-129">**Congratulations!**</span></span> <span data-ttu-id="53539-130">Z pierwszej aplikacji HTML tooApp usługi została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="53539-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="53539-131">Aktualizowanie i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="53539-131">Update and redeploy hello app</span></span>

<span data-ttu-id="53539-132">Otwórz hello *index.html* plik w edytorze tekstów, a następnie wprowadź znaczników toohello zmiany.</span><span class="sxs-lookup"><span data-stu-id="53539-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="53539-133">Na przykład zmienić nagłówek hello H1 z toojust "Azure aplikacji usługi — przykład statycznego HTML witryna" "Usługa aplikacji Azure".</span><span class="sxs-lookup"><span data-stu-id="53539-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="53539-134">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="53539-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="53539-135">Po zakończeniu wdrożenia należy odświeżyć zmiany hello toosee przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="53539-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Zaktualizowana strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="53539-137">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="53539-137">Manage your new Azure web app</span></span>

<span data-ttu-id="53539-138">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.</span><span class="sxs-lookup"><span data-stu-id="53539-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="53539-139">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53539-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="53539-141">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="53539-141">You see your web app's Overview page.</span></span> <span data-ttu-id="53539-142">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="53539-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="53539-144">menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53539-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="53539-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53539-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53539-146">Mapowanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="53539-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
