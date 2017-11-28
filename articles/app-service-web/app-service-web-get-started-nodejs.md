---
title: aaaCreate aplikacji sieci web Node.js na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdróż swoją pierwszą aplikację Hello World w środowisku Node.js w usłudze Azure App Service Web Apps w ciągu kilku minut."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="5114d-103">Tworzenie aplikacji internetowej Node.js na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5114d-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="5114d-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="5114d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="5114d-105">Ta opcja szybkiego startu przedstawia sposób toodeploy tooAzure aplikacji Node.js aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5114d-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="5114d-106">Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web toohello kodu Node.js Git toodeploy próbki.</span><span class="sxs-lookup"><span data-stu-id="5114d-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="5114d-108">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="5114d-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="5114d-109">Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.</span><span class="sxs-lookup"><span data-stu-id="5114d-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="5114d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5114d-110">Prerequisites</span></span>

<span data-ttu-id="5114d-111">toocomplete tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="5114d-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="5114d-112">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="5114d-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="5114d-113">Zainstaluj środowisko Node.js i menedżer NPM</span><span class="sxs-lookup"><span data-stu-id="5114d-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5114d-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5114d-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5114d-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="5114d-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5114d-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5114d-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="5114d-117">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="5114d-117">Download hello sample</span></span>

<span data-ttu-id="5114d-118">W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5114d-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="5114d-119">Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="5114d-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="5114d-120">Zmień katalog toohello, który zawiera hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="5114d-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="5114d-121">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="5114d-121">Run hello app locally</span></span>

<span data-ttu-id="5114d-122">Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `npm start` hello toolaunch skrypt wbudowany serwer Node.js HTTP.</span><span class="sxs-lookup"><span data-stu-id="5114d-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="5114d-123">Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację w http://localhost: 1337.</span><span class="sxs-lookup"><span data-stu-id="5114d-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="5114d-124">Zobacz hello **Hello World** wiadomość hello przykładowej aplikacji wyświetlane na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="5114d-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="5114d-126">W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="5114d-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="5114d-128">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="5114d-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="5114d-129">Przeglądaj toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="5114d-129">Browse toohello app</span></span>

<span data-ttu-id="5114d-130">Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="5114d-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="5114d-131">Witaj Node.js przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5114d-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="5114d-133">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="5114d-133">**Congratulations!**</span></span> <span data-ttu-id="5114d-134">Twoje pierwsze tooApp aplikacji Node.js usługi została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="5114d-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="5114d-135">Aktualizowanie i wdrożenie hello kodu</span><span class="sxs-lookup"><span data-stu-id="5114d-135">Update and redeploy hello code</span></span>

<span data-ttu-id="5114d-136">Za pomocą edytora tekstu, otwórz hello `index.js` plików w aplikacji Node.js hello i Ustaw tekst toohello niewielkie zmiany w wywołaniu hello zbyt`response.end`:</span><span class="sxs-lookup"><span data-stu-id="5114d-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="5114d-137">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="5114d-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="5114d-138">Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello **aplikacji toohello przeglądania** kroku i kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="5114d-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="5114d-140">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5114d-140">Manage your new Azure web app</span></span>

<span data-ttu-id="5114d-141">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.</span><span class="sxs-lookup"><span data-stu-id="5114d-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="5114d-142">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5114d-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="5114d-144">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="5114d-144">You see your web app's Overview page.</span></span> <span data-ttu-id="5114d-145">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="5114d-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="5114d-147">menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5114d-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="5114d-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5114d-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5114d-149">Środowisko Node.js z bazą danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="5114d-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
