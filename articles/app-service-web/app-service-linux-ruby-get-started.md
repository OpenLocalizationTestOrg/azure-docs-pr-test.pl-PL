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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Tworzenie aplikacji dopisków fonetycznych w usłudze aplikacje sieci Web w systemie Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie. Ta opcja szybkiego startu przedstawia toocreate podstawowe Ruby w aplikacji szyny następnie wdrażania tooAzure jako aplikacji sieci Web w systemie Linux.

![Witaj świecie](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Wymagania wstępne

* [Ruby 2.4.1 lub nowszej](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* [Aktywną subskrypcją platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Pobierz przykładowe hello

W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie

Serwer szyny hello są uruchamiane w kolejności dla toowork aplikacji hello. Zmień toohello *hello world* katalogu i hello `rails server` polecenie uruchamia hello serwera.

```bash
cd hello-world\bin
rails server
```
    
Za pomocą przeglądarki sieci web przejdź zbyt`http://localhost:3000` tootest aplikacji hello lokalnie.  

![Witaj świecie](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Zmodyfikuj komunikat powitalny toodisplay aplikacji

Modyfikowanie aplikacji hello, dlatego wyświetla komunikat powitalny. Umożliwia zmianę kontrolera aplikacji hello, tak aby zwracało wiadomość hello jako przeglądarki toohello HTML. 

Otwórz *~/workspace/hello-world/app/controllers/application_controller.rb* do edycji. Modyfikowanie hello `ApplicationController` toolook klasy, takie jak powitania po przykładowym kodzie:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Aplikacja jest teraz skonfigurowany. Za pomocą przeglądarki sieci web przejdź zbyt`http://localhost:3000` strony docelowej głównego hello tooconfirm.

![Witaj świecie skonfigurowane](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Tworzenie aplikacji sieci web dopisków fonetycznych na platformie Azure

Użyj hello [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate polecenie plan usługi app service dla aplikacji sieci web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Następnie należy wystawić hello [tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp) aplikacji sieci web hello toocreate polecenia, który używa hello nowo utworzony plan usługi. Zwróć uwagę tego środowiska uruchomieniowego hello ustawiono zbyt`ruby|2.3`. Nie zapomnij tooreplace `<app name>` przy użyciu unikatowej nazwy aplikacji.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Po utworzeniu aplikacji sieci web hello **omówienie** strona jest dostępna tooview. Przejdź tooit. wyświetlane są następujące strony powitalnej Hello:

![Strony powitalnej](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Wdrażanie aplikacji

Użyj tooAzure dopisków fonetycznych aplikacji hello toodeploy Git. Hello aplikacji sieci web jest już skonfigurowana wdrożenia Git. Adres URL wdrożenia hello można pobrać przez wystawienie [wdrożenia aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) polecenia.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Należy zauważyć, że adres URL Git hello ma powitania po formularz bazujący na nazwę aplikacji sieci web:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Uruchom hello następujące polecenia toodeploy hello miejscowego tooyour witryny sieci Web platformy Azure:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Upewnij się, że operacje zdalnego wdrażania hello Raport powodzenie. Witaj polecenia produktu dane wyjściowe podobne toohello następującego tekstu:

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

Po zakończeniu wdrażania hello ponowne uruchomienie aplikacji sieci web dla efektu tootake wdrożenia hello przy użyciu hello [ponowne uruchomienie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#restart) polecenia, jak pokazano poniżej:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Przejdź do witryny tooyour i sprawdź wyniki hello.

```bash
http://<your web app name>.azurewebsites.net
```
![zaktualizowano aplikację sieci web](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Podczas ponownego uruchamiania aplikacji hello próby toobrowse hello lokacji powoduje kod stanu HTTP `Error 503 Server unavailable`. Może upłynąć kilka minut toofully ponownego uruchomienia komputera.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Następne kroki

[Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)