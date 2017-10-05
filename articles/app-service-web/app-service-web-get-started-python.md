---
title: "Tworzenie aplikacji internetowej w języku Python na platformie Azure | Microsoft Docs"
description: "Wdróż swoją pierwszą aplikację Hello World w języku Python w usłudze Azure App Service Web Apps w ciągu kilku minut."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="09dc2-103">Tworzenie aplikacji sieci Web w języku Python na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="09dc2-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="09dc2-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="09dc2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="09dc2-105">Ten podręcznik Szybki start przeprowadzi Cię przez tworzenie i wdrażanie aplikacji w języku Python w usłudze Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="09dc2-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="09dc2-106">Możesz utworzyć aplikację internetową przy użyciu [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), a usługa Git umożliwia wdrażanie przykładowego kodu języka Python w aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="09dc2-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="09dc2-108">Poniższe kroki możesz wykonać przy użyciu komputera z systemem Mac, Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="09dc2-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="09dc2-109">Po zainstalowaniu wymagań wstępnych wykonanie czynności trwa około pięciu minut.</span><span class="sxs-lookup"><span data-stu-id="09dc2-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="09dc2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="09dc2-110">Prerequisites</span></span>

<span data-ttu-id="09dc2-111">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="09dc2-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="09dc2-112">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="09dc2-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="09dc2-113">Zainstaluj język Python</span><span class="sxs-lookup"><span data-stu-id="09dc2-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="09dc2-114">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="09dc2-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="09dc2-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="09dc2-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="09dc2-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="09dc2-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="09dc2-117">Pobierz przykład</span><span class="sxs-lookup"><span data-stu-id="09dc2-117">Download the sample</span></span>

<span data-ttu-id="09dc2-118">W oknie terminala uruchom następujące polecenie, aby sklonować przykładowe repozytorium aplikacji na maszynę lokalną.</span><span class="sxs-lookup"><span data-stu-id="09dc2-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="09dc2-119">To okno terminala umożliwia uruchamianie wszystkich poleceń z tego przewodnika Szybki start.</span><span class="sxs-lookup"><span data-stu-id="09dc2-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="09dc2-120">Przejdź do katalogu, który zawiera przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="09dc2-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="09dc2-121">Lokalne uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="09dc2-121">Run the app locally</span></span>

<span data-ttu-id="09dc2-122">Zainstaluj wymagane pakiety za pomocą polecenia `pip`.</span><span class="sxs-lookup"><span data-stu-id="09dc2-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="09dc2-123">Uruchom aplikację lokalnie, otwierając okno terminala i korzystając z polecenia języka `Python` w celu uruchomienia wbudowanego serwera internetowego języka Python.</span><span class="sxs-lookup"><span data-stu-id="09dc2-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="09dc2-124">Otwórz przeglądarkę internetową i przejdź do przykładowej aplikacji pod adresem http://localhost:5000.</span><span class="sxs-lookup"><span data-stu-id="09dc2-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="09dc2-125">Na stronie zostanie wyświetlony komunikat **Witaj, świecie** z przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="09dc2-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="09dc2-127">W oknie terminalu naciśnij kombinację klawiszy **Ctrl + C**, aby zamknąć serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="09dc2-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="09dc2-129">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="09dc2-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="09dc2-130">Konfigurowanie do używania środowiska Python</span><span class="sxs-lookup"><span data-stu-id="09dc2-130">Configure to use Python</span></span>

<span data-ttu-id="09dc2-131">Użyj polecenia [az webapp config set](/cli/azure/webapp/config#set) do skonfigurowania aplikacji internetowej korzystającej z języka Python w wersji `3.4`.</span><span class="sxs-lookup"><span data-stu-id="09dc2-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="09dc2-132">Podczas ustawiania wersji języka Python w ten sposób jest używany domyślny kontener udostępniany przez platformę.</span><span class="sxs-lookup"><span data-stu-id="09dc2-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="09dc2-133">Aby korzystać z własnego kontenera, zapoznaj się z opisem polecenia [az webapp config container set](/cli/azure/webapp/config/container#set) w dokumentacji dotyczącej interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="09dc2-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="09dc2-134">Przechodzenie do aplikacji</span><span class="sxs-lookup"><span data-stu-id="09dc2-134">Browse to the app</span></span>

<span data-ttu-id="09dc2-135">Przejdź do wdrożonej aplikacji za pomocą przeglądarki sieci Web.</span><span class="sxs-lookup"><span data-stu-id="09dc2-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="09dc2-136">Przykładowy kod w języku Python jest uruchamiany w aplikacji internetowej usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="09dc2-136">The Python sample code is running in an Azure App Service web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="09dc2-138">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="09dc2-138">**Congratulations!**</span></span> <span data-ttu-id="09dc2-139">Udało Ci się wdrożyć pierwszą własną aplikację w języku Python w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="09dc2-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="09dc2-140">Aktualizowanie i ponowne wdrażanie kodu</span><span class="sxs-lookup"><span data-stu-id="09dc2-140">Update and redeploy the code</span></span>

<span data-ttu-id="09dc2-141">Za pomocą lokalnego edytora tekstów otwórz plik `main.py` w aplikacji w języku Python i wprowadź niewielką zmianę w tekście obok instrukcji `return`:</span><span class="sxs-lookup"><span data-stu-id="09dc2-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="09dc2-142">Zatwierdź zmiany w narzędziu Git, a następnie wypchnij zmiany kodu na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="09dc2-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="09dc2-143">Po zakończeniu wdrożenia przejdź z powrotem do okna przeglądarki otwartego w kroku [przechodzenia do aplikacji](#browse-to-the-app), a następnie odśwież stronę.</span><span class="sxs-lookup"><span data-stu-id="09dc2-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="09dc2-145">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="09dc2-145">Manage your new Azure web app</span></span>

<span data-ttu-id="09dc2-146">Przejdź do witryny <a href="https://portal.azure.com" target="_blank">Azure Portal</a>, aby zarządzać utworzoną aplikacją internetową.</span><span class="sxs-lookup"><span data-stu-id="09dc2-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="09dc2-147">W menu po lewej stronie kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji internetowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09dc2-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="09dc2-149">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="09dc2-149">You see your web app's Overview page.</span></span> <span data-ttu-id="09dc2-150">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="09dc2-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="09dc2-152">Menu po lewej stronie zawiera różne strony służące do konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="09dc2-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="09dc2-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09dc2-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09dc2-154">Python z PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="09dc2-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
