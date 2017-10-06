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
# <a name="create-a-python-web-app-in-azure"></a>Tworzenie aplikacji sieci Web w języku Python na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.  Ta opcja szybkiego startu przedstawiono sposób toodevelop i wdrażanie tooAzure aplikacji Python aplikacji sieci Web. Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web toohello kodu Python Git toodeploy próbki.

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux. Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.
## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

1. [Zainstaluj oprogramowanie Git](https://git-scm.com/)
1. [Zainstaluj język Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Pobierz przykładowe hello

W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.

Zmień katalog toohello, który zawiera hello przykładowy kod.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Uruchamianie aplikacji hello lokalnie

Instalowanie pakietów hello wymagane przy użyciu `pip`.

```bash
pip install -r requirements.txt
```

Uruchamianie aplikacji hello lokalnie, Otwórz okno terminala i użyj hello `Python` polecenia toolaunch hello wbudowanego Python serwera sieci web.

```bash
python main.py
```

Otwórz przeglądarkę sieci web i przejdź toohello przykładową aplikację w http://localhost: 5000.

Zostanie wyświetlony hello **Hello World** wiadomość hello przykładowej aplikacji wyświetlane na stronie powitania.

![Przykładowa aplikacja działająca w środowisku lokalnym](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

W oknie terminalu, naciśnij klawisz **klawisze Ctrl + C** serwera sieci web hello tooexit.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji internetowej](media/app-service-web-get-started-python/app-service-web-service-created.png)

Na platformie Azure została utworzona nowa pusta aplikacja internetowa.

## <a name="configure-toouse-python"></a>Skonfiguruj toouse języka Python

Użyj hello [az aplikacji sieci Web config set](/cli/azure/webapp/config#set) wersji języka Python toouse aplikacji sieci web polecenia tooconfigure hello `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Ustawienie wersji języka Python hello w ten sposób korzysta z domyślnego kontenera podał hello platformy. toouse własne kontenera, zobacz hello odwołania interfejsu wiersza polecenia dla hello [zestaw kontenera konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/container#set) polecenia.

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

## <a name="browse-toohello-app"></a>Przeglądaj toohello aplikacji

Przeglądaj toohello wdrożonych aplikacji za pomocą przeglądarki sieci web.

```bash
http://<app_name>.azurewebsites.net
```

Witaj Python przykładowy kod jest uruchomiony w aplikacji sieci web platformy Azure App Service.

![Przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Gratulacje!** Z pierwszej aplikacji Python tooApp usługi została wdrożona.

## <a name="update-and-redeploy-hello-code"></a>Aktualizowanie i wdrożenie hello kodu

Za pomocą edytora tekstu lokalnych Otwórz hello `main.py` pliku w aplikacji Python hello i upewnij niewielkie zmiany toohello dalej tekst toohello `return` instrukcji:

```python
return 'Hello, Azure!'
```

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git commit -am "updated output"
git push azure master
```

Po zakończeniu wdrożenia przełącznika wstecz toohello okna przeglądarki, które otwarty w hello [aplikacji toohello przeglądania](#browse-to-the-app) krok i Odśwież hello strony.

![Zaktualizowana przykładowa aplikacja działająca na platformie Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [Python z PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
