---
title: Tworzenie aplikacji internetowej Node.js na platformie Azure | Microsoft Docs
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="1e81e-103">Tworzenie aplikacji internetowej Node.js na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1e81e-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="1e81e-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="1e81e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1e81e-105">Ten samouczek Szybki start przedstawia sposób wdrażania aplikacji Node.js w usłudze Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1e81e-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="1e81e-106">Aplikację internetową możesz utworzyć przy użyciu [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), a usługa Git umożliwia wdrażanie przykładowego kodu w języku Node.js w aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="1e81e-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="1e81e-108">Poniższe kroki możesz wykonać przy użyciu komputera z systemem Mac, Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="1e81e-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1e81e-109">Po zainstalowaniu wymagań wstępnych wykonanie czynności trwa około pięciu minut.</span><span class="sxs-lookup"><span data-stu-id="1e81e-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="1e81e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e81e-110">Prerequisites</span></span>

<span data-ttu-id="1e81e-111">Aby ukończyć ten przewodnik Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="1e81e-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="1e81e-112">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="1e81e-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1e81e-113">Zainstaluj środowisko Node.js i menedżer NPM</span><span class="sxs-lookup"><span data-stu-id="1e81e-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e81e-114">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1e81e-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1e81e-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="1e81e-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="1e81e-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e81e-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="1e81e-117">Pobierz przykład</span><span class="sxs-lookup"><span data-stu-id="1e81e-117">Download the sample</span></span>

<span data-ttu-id="1e81e-118">W oknie terminala uruchom następujące polecenie, aby sklonować przykładowe repozytorium aplikacji na maszynę lokalną.</span><span class="sxs-lookup"><span data-stu-id="1e81e-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="1e81e-119">To okno terminala umożliwia uruchamianie wszystkich poleceń z tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="1e81e-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="1e81e-120">Przejdź do katalogu, który zawiera przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="1e81e-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="1e81e-121">Lokalne uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e81e-121">Run the app locally</span></span>

<span data-ttu-id="1e81e-122">Uruchom aplikację lokalnie, otwierając okno terminala i korzystając ze skryptu `npm start` w celu uruchomienia wbudowanego serwera HTTP środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="1e81e-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="1e81e-123">Otwórz przeglądarkę internetową i przejdź do przykładowej aplikacji pod adresem http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="1e81e-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="1e81e-124">Na stronie zostanie wyświetlony komunikat **Hello World** z przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e81e-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="1e81e-126">W oknie terminalu naciśnij kombinację klawiszy **Ctrl + C**, aby zamknąć serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1e81e-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="1e81e-128">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="1e81e-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="1e81e-129">Przechodzenie do aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e81e-129">Browse to the app</span></span>

<span data-ttu-id="1e81e-130">Przejdź do wdrożonej aplikacji za pomocą przeglądarki sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1e81e-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1e81e-131">Przykładowy kod w języku Node.js jest uruchamiany w aplikacji internetowej usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1e81e-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="1e81e-133">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="1e81e-133">**Congratulations!**</span></span> <span data-ttu-id="1e81e-134">Udało Ci się wdrożyć pierwszą własną aplikację w języku Node.js w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="1e81e-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="1e81e-135">Aktualizowanie i ponowne wdrażanie kodu</span><span class="sxs-lookup"><span data-stu-id="1e81e-135">Update and redeploy the code</span></span>

<span data-ttu-id="1e81e-136">Za pomocą edytora tekstów otwórz plik `index.js` w aplikacji Node.js i wprowadź niewielką zmianę w tekście w wywołaniu `response.end`:</span><span class="sxs-lookup"><span data-stu-id="1e81e-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="1e81e-137">Zatwierdź zmiany w narzędziu Git, a następnie wypchnij zmiany kodu na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="1e81e-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1e81e-138">Po zakończeniu wdrożenia przejdź z powrotem do okna przeglądarki otwartego w kroku **przechodzenia do aplikacji**, a następnie kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="1e81e-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1e81e-140">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1e81e-140">Manage your new Azure web app</span></span>

<span data-ttu-id="1e81e-141">Przejdź do witryny <a href="https://portal.azure.com" target="_blank">Azure Portal</a>, aby zarządzać utworzoną aplikacją internetową.</span><span class="sxs-lookup"><span data-stu-id="1e81e-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="1e81e-142">W menu po lewej stronie kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji internetowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1e81e-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="1e81e-144">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="1e81e-144">You see your web app's Overview page.</span></span> <span data-ttu-id="1e81e-145">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="1e81e-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1e81e-147">Menu po lewej stronie zawiera różne strony służące do konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e81e-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1e81e-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e81e-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e81e-149">Środowisko Node.js z bazą danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="1e81e-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
