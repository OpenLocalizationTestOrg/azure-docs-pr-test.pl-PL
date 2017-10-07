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
# <a name="create-a-nodejs-web-app-in-azure"></a>Tworzenie aplikacji internetowej Node.js na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.  Ta opcja szybkiego startu przedstawia sposób toodeploy tooAzure aplikacji Node.js aplikacji sieci Web. Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web toohello kodu Node.js Git toodeploy próbki.

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux. Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego przewodnika Szybki Start:

* [Zainstaluj oprogramowanie Git](https://git-scm.com/)
* [Zainstaluj środowisko Node.js i menedżer NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Pobierz przykładowe hello

W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.

Zmień katalog toohello, który zawiera hello przykładowy kod.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Uruchamianie aplikacji hello lokalnie

Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `npm start` hello toolaunch skrypt wbudowany serwer Node.js HTTP.

```bash
npm start
```

Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację w http://localhost: 1337.

Zobacz hello **Hello World** wiadomość hello przykładowej aplikacji wyświetlane na stronie powitania.

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-php/app-service-web-service-created.png)

Na platformie Azure została utworzona nowa pusta aplikacja internetowa.

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

## <a name="browse-toohello-app"></a>Przeglądaj toohello aplikacji

Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.

```bash
http://<app_name>.azurewebsites.net
```

Witaj Node.js przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Gratulacje!** Twoje pierwsze tooApp aplikacji Node.js usługi została wdrożona.

## <a name="update-and-redeploy-hello-code"></a>Aktualizowanie i wdrożenie hello kodu

Za pomocą edytora tekstu, otwórz hello `index.js` plików w aplikacji Node.js hello i Ustaw tekst toohello niewielkie zmiany w wywołaniu hello zbyt`response.end`:

```nodejs
response.end("Hello Azure!");
```

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git commit -am "updated output"
git push azure master
```

Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello **aplikacji toohello przeglądania** kroku i kliknij przycisk Odśwież.

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Zarządzanie nową aplikacją sieci Web platformy Azure

Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Zostanie wyświetlona strona Omówienie aplikacji internetowej. Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. 

![Blok usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Środowisko Node.js z bazą danych MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
