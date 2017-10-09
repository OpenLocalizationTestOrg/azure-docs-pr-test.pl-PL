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
# <a name="create-a-php-web-app-in-azure"></a>Tworzenie aplikacji sieci Web w języku PHP na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.  Ten samouczek Szybki Start pokazuje, jak toodeploy tooAzure aplikacji PHP aplikacje sieci Web. Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) powłoki usługi w chmurze i korzystania z aplikacji sieci web toohello kodu PHP Git toodeploy próbki.

![Przykładowa aplikacja działająca na platformie Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux. Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego przewodnika Szybki Start:

* [Zainstaluj oprogramowanie Git](https://git-scm.com/)
* [Zainstaluj środowisko PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Pobierz przykładowe hello lokalnie

W oknie terminalu, uruchom następujące polecenia hello. To spowoduje klonowania komputer lokalny tooyour hello przykładowej aplikacji, a następnie przejdź toohello katalogu zawierającego hello przykładowy kod.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Uruchamianie aplikacji hello lokalnie

Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `php` polecenia toolaunch hello wbudowanego PHP serwera sieci web.

```bash
php -S localhost:8080
```

Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację pod adresem http://localhost: 8080.

Zobacz hello **Hello World!** komunikat z hello przykładowej aplikacji wyświetlane na stronie powitania.

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-php/app-service-web-service-created.png)

Na platformie Azure została utworzona nowa pusta aplikacja internetowa.

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

## <a name="browse-toohello-app-locally"></a>Przeglądaj toohello aplikacji lokalnie

Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.

```bash
http://<app_name>.azurewebsites.net
```

Witaj PHP przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Gratulacje!** Z pierwszej aplikacji PHP tooApp usługi została wdrożona.

## <a name="update-locally-and-redeploy-hello-code"></a>Zaktualizuj lokalnie i wdrożenie hello kodu

Za pomocą edytora tekstu lokalnych Otwórz hello `index.php` pliku w aplikacji PHP hello i upewnić tekstu toohello niewielkie zmiany w ciągu hello obok zbyt`echo`:

```php
echo "Hello Azure!";
```

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git commit -am "updated output"
git push azure master
```

Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello **aplikacji toohello przeglądania** krok i Odśwież hello strony.

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Zarządzanie nową aplikacją sieci Web platformy Azure

Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Zostanie wyświetlona strona Omówienie aplikacji internetowej. Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Środowisko PHP z bazą danych MySQL](app-service-web-tutorial-php-mysql.md)
