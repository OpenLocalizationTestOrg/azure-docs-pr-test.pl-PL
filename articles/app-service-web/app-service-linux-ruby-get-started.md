---
title: "aaaCreate aplikacji Ruby, przy użyciu aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate Ruby aplikacji za pomocą wpp sieci web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, linux, oss, ruby"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="033f6-104">Tworzenie aplikacji dopisków fonetycznych w usłudze aplikacje sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="033f6-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="033f6-105">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="033f6-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="033f6-106">Ta opcja szybkiego startu przedstawia toocreate podstawowe Ruby w aplikacji szyny następnie wdrażania tooAzure jako aplikacji sieci Web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="033f6-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Witaj świecie](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="033f6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="033f6-108">Prerequisites</span></span>

* <span data-ttu-id="033f6-109">[Ruby 2.4.1 lub nowszej](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="033f6-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="033f6-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="033f6-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="033f6-111">[Aktywną subskrypcją platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="033f6-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="033f6-112">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="033f6-112">Download hello sample</span></span>

<span data-ttu-id="033f6-113">W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="033f6-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="033f6-114">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="033f6-114">Run hello application locally</span></span>

<span data-ttu-id="033f6-115">Serwer szyny hello są uruchamiane w kolejności dla toowork aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="033f6-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="033f6-116">Zmień toohello *hello world* katalogu i hello `rails server` polecenie uruchamia hello serwera.</span><span class="sxs-lookup"><span data-stu-id="033f6-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="033f6-117">Za pomocą przeglądarki sieci web przejdź zbyt`http://localhost:3000` tootest aplikacji hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="033f6-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Witaj świecie](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="033f6-119">Zmodyfikuj komunikat powitalny toodisplay aplikacji</span><span class="sxs-lookup"><span data-stu-id="033f6-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="033f6-120">Modyfikowanie aplikacji hello, dlatego wyświetla komunikat powitalny.</span><span class="sxs-lookup"><span data-stu-id="033f6-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="033f6-121">Umożliwia zmianę kontrolera aplikacji hello, tak aby zwracało wiadomość hello jako przeglądarki toohello HTML.</span><span class="sxs-lookup"><span data-stu-id="033f6-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="033f6-122">Otwórz *~/workspace/hello-world/app/controllers/application_controller.rb* do edycji.</span><span class="sxs-lookup"><span data-stu-id="033f6-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="033f6-123">Modyfikowanie hello `ApplicationController` toolook klasy, takie jak powitania po przykładowym kodzie:</span><span class="sxs-lookup"><span data-stu-id="033f6-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="033f6-124">Aplikacja jest teraz skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="033f6-124">Your app is now configured.</span></span> <span data-ttu-id="033f6-125">Za pomocą przeglądarki sieci web przejdź zbyt`http://localhost:3000` strony docelowej głównego hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="033f6-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Witaj świecie skonfigurowane](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="033f6-127">Tworzenie aplikacji sieci web dopisków fonetycznych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="033f6-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="033f6-128">Użyj hello [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate polecenie plan usługi app service dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="033f6-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="033f6-129">Następnie należy wystawić hello [tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp) aplikacji sieci web hello toocreate polecenia, który używa hello nowo utworzony plan usługi.</span><span class="sxs-lookup"><span data-stu-id="033f6-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="033f6-130">Zwróć uwagę tego środowiska uruchomieniowego hello ustawiono zbyt`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="033f6-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="033f6-131">Nie zapomnij tooreplace `<app name>` przy użyciu unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="033f6-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="033f6-132">Po utworzeniu aplikacji sieci web hello **omówienie** strona jest dostępna tooview.</span><span class="sxs-lookup"><span data-stu-id="033f6-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="033f6-133">Przejdź tooit.</span><span class="sxs-lookup"><span data-stu-id="033f6-133">Navigate tooit.</span></span> <span data-ttu-id="033f6-134">wyświetlane są następujące strony powitalnej Hello:</span><span class="sxs-lookup"><span data-stu-id="033f6-134">hello following splash page is displayed:</span></span>

![Strony powitalnej](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="033f6-136">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="033f6-136">Deploy your application</span></span>

<span data-ttu-id="033f6-137">Użyj tooAzure dopisków fonetycznych aplikacji hello toodeploy Git.</span><span class="sxs-lookup"><span data-stu-id="033f6-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="033f6-138">Hello aplikacji sieci web jest już skonfigurowana wdrożenia Git.</span><span class="sxs-lookup"><span data-stu-id="033f6-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="033f6-139">Adres URL wdrożenia hello można pobrać przez wystawienie [wdrożenia aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) polecenia.</span><span class="sxs-lookup"><span data-stu-id="033f6-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="033f6-140">Należy zauważyć, że adres URL Git hello ma powitania po formularz bazujący na nazwę aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="033f6-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="033f6-141">Uruchom hello następujące polecenia toodeploy hello miejscowego tooyour witryny sieci Web platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="033f6-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="033f6-142">Upewnij się, że operacje zdalnego wdrażania hello Raport powodzenie.</span><span class="sxs-lookup"><span data-stu-id="033f6-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="033f6-143">Witaj polecenia produktu dane wyjściowe podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="033f6-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="033f6-144">Po zakończeniu wdrażania hello ponowne uruchomienie aplikacji sieci web dla efektu tootake wdrożenia hello przy użyciu hello [ponowne uruchomienie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#restart) polecenia, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="033f6-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="033f6-145">Przejdź do witryny tooyour i sprawdź wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="033f6-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![zaktualizowano aplikację sieci web](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="033f6-147">Podczas ponownego uruchamiania aplikacji hello próby toobrowse hello lokacji powoduje kod stanu HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="033f6-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="033f6-148">Może upłynąć kilka minut toofully ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="033f6-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="033f6-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="033f6-149">Next steps</span></span>

[<span data-ttu-id="033f6-150">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="033f6-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)