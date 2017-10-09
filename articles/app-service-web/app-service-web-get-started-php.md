---
title: aaaCreate PHP sieci web aplikacji na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdróż swoją pierwszą aplikację Hello World w środowisku PHP w usłudze Azure App Service Web Apps w ciągu kilku minut."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="34814-103">Tworzenie aplikacji sieci Web w języku PHP na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="34814-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="34814-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="34814-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="34814-105">Ten samouczek Szybki Start pokazuje, jak toodeploy tooAzure aplikacji PHP aplikacje sieci Web.</span><span class="sxs-lookup"><span data-stu-id="34814-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="34814-106">Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) powłoki usługi w chmurze i korzystania z aplikacji sieci web toohello kodu PHP Git toodeploy próbki.</span><span class="sxs-lookup"><span data-stu-id="34814-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="34814-107">![Przykładowa aplikacja działająca na platformie Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="34814-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="34814-108">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="34814-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="34814-109">Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.</span><span class="sxs-lookup"><span data-stu-id="34814-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34814-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34814-110">Prerequisites</span></span>

<span data-ttu-id="34814-111">toocomplete tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="34814-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="34814-112">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="34814-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="34814-113">Zainstaluj środowisko PHP</span><span class="sxs-lookup"><span data-stu-id="34814-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="34814-114">Pobierz przykładowe hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="34814-114">Download hello sample locally</span></span>

<span data-ttu-id="34814-115">W oknie terminalu, uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="34814-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="34814-116">To spowoduje klonowania komputer lokalny tooyour hello przykładowej aplikacji, a następnie przejdź toohello katalogu zawierającego hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="34814-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="34814-117">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="34814-117">Run hello app locally</span></span>

<span data-ttu-id="34814-118">Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `php` polecenia toolaunch hello wbudowanego PHP serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="34814-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="34814-119">Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację pod adresem http://localhost: 8080.</span><span class="sxs-lookup"><span data-stu-id="34814-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="34814-120">Zobacz hello **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="34814-120">You see hello **Hello World!**</span></span> <span data-ttu-id="34814-121">komunikat z hello przykładowej aplikacji wyświetlane na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="34814-121">message from hello sample app displayed in hello page.</span></span>

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="34814-123">W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="34814-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="34814-125">Na platformie Azure została utworzona nowa pusta aplikacja internetowa.</span><span class="sxs-lookup"><span data-stu-id="34814-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="34814-126">Przeglądaj toohello aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="34814-126">Browse toohello app locally</span></span>

<span data-ttu-id="34814-127">Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="34814-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="34814-128">Witaj PHP przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="34814-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="34814-130">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="34814-130">**Congratulations!**</span></span> <span data-ttu-id="34814-131">Z pierwszej aplikacji PHP tooApp usługi została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="34814-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="34814-132">Zaktualizuj lokalnie i wdrożenie hello kodu</span><span class="sxs-lookup"><span data-stu-id="34814-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="34814-133">Za pomocą edytora tekstu lokalnych Otwórz hello `index.php` pliku w aplikacji PHP hello i upewnić tekstu toohello niewielkie zmiany w ciągu hello obok zbyt`echo`:</span><span class="sxs-lookup"><span data-stu-id="34814-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="34814-134">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="34814-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="34814-135">Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello **aplikacji toohello przeglądania** krok i Odśwież hello strony.</span><span class="sxs-lookup"><span data-stu-id="34814-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="34814-137">Zarządzanie nową aplikacją sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34814-137">Manage your new Azure web app</span></span>

<span data-ttu-id="34814-138">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.</span><span class="sxs-lookup"><span data-stu-id="34814-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="34814-139">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="34814-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="34814-141">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="34814-141">You see your web app's Overview page.</span></span> <span data-ttu-id="34814-142">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="34814-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="34814-144">menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34814-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="34814-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34814-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="34814-146">Środowisko PHP z bazą danych MySQL</span><span class="sxs-lookup"><span data-stu-id="34814-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
