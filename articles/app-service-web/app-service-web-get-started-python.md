---
title: aaaCreate Python aplikacji sieci web na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="4a840-103">Tworzenie aplikacji sieci Web w języku Python na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4a840-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="4a840-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="4a840-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="4a840-105">Ta opcja szybkiego startu przedstawiono sposób toodevelop i wdrażanie tooAzure aplikacji Python aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4a840-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="4a840-106">Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web toohello kodu Python Git toodeploy próbki.</span><span class="sxs-lookup"><span data-stu-id="4a840-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="4a840-108">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="4a840-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="4a840-109">Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.</span><span class="sxs-lookup"><span data-stu-id="4a840-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="4a840-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a840-110">Prerequisites</span></span>

<span data-ttu-id="4a840-111">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="4a840-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="4a840-112">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="4a840-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="4a840-113">Zainstaluj język Python</span><span class="sxs-lookup"><span data-stu-id="4a840-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4a840-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4a840-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4a840-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="4a840-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4a840-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a840-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="4a840-117">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="4a840-117">Download hello sample</span></span>

<span data-ttu-id="4a840-118">W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="4a840-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="4a840-119">Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="4a840-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="4a840-120">Zmień katalog toohello, który zawiera hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="4a840-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="4a840-121">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="4a840-121">Run hello app locally</span></span>

<span data-ttu-id="4a840-122">Instalowanie pakietów hello wymagane przy użyciu `pip`.</span><span class="sxs-lookup"><span data-stu-id="4a840-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="4a840-123">Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `Python` polecenia toolaunch hello wbudowanego Python serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="4a840-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="4a840-124">Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację w http://localhost: 5000.</span><span class="sxs-lookup"><span data-stu-id="4a840-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="4a840-125">Zostanie wyświetlony hello **Hello World** wiadomość hello przykładowej aplikacji wyświetlane na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="4a840-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="4a840-127">W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="4a840-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="4a840-129">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="4a840-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="4a840-130">Skonfiguruj toouse języka Python</span><span class="sxs-lookup"><span data-stu-id="4a840-130">Configure toouse Python</span></span>

<span data-ttu-id="4a840-131">Użyj hello [az aplikacji sieci Web config set](/cli/azure/webapp/config#set) wersji języka Python toouse aplikacji sieci web polecenia tooconfigure hello `3.4`.</span><span class="sxs-lookup"><span data-stu-id="4a840-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="4a840-132">Ustawienie wersji języka Python hello w ten sposób korzysta z domyślnego kontenera podał hello platformy.</span><span class="sxs-lookup"><span data-stu-id="4a840-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="4a840-133">toouse własne kontenera, zobacz hello odwołania interfejsu wiersza polecenia dla hello [zestaw kontenera konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/container#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4a840-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="4a840-134">Przeglądaj toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="4a840-134">Browse toohello app</span></span>

<span data-ttu-id="4a840-135">Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="4a840-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="4a840-136">Witaj Python przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4a840-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="4a840-138">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="4a840-138">**Congratulations!**</span></span> <span data-ttu-id="4a840-139">Z pierwszej aplikacji Python tooApp usługi została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="4a840-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="4a840-140">Aktualizowanie i wdrożenie hello kodu</span><span class="sxs-lookup"><span data-stu-id="4a840-140">Update and redeploy hello code</span></span>

<span data-ttu-id="4a840-141">Za pomocą edytora tekstu lokalnych Otwórz hello `main.py` pliku w aplikacji Python hello i upewnij niewielkie zmiany toohello dalej tekst toohello `return` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="4a840-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="4a840-142">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="4a840-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="4a840-143">Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello [aplikacji toohello przeglądania](#browse-to-the-app) krok i Odśwież hello strony.</span><span class="sxs-lookup"><span data-stu-id="4a840-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="4a840-145">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4a840-145">Manage your new Azure web app</span></span>

<span data-ttu-id="4a840-146">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4a840-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="4a840-147">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a840-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="4a840-149">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="4a840-149">You see your web app's Overview page.</span></span> <span data-ttu-id="4a840-150">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="4a840-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="4a840-152">menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4a840-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="4a840-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a840-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a840-154">Python z PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4a840-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
