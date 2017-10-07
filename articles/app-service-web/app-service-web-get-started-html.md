---
title: aaaCreate statyczne HTML aplikacji sieci web na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorun aplikacje sieci web w usłudze Azure App Service, wdrażając statycznego HTML przykładową aplikację."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Tworzenie statycznej aplikacji sieci Web w języku HTML na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.  Tego przewodnika Szybki Start pokazuje, jak toodeploy podstawowe HTML + CSS lokacji tooAzure aplikacji sieci Web. Tworzenie aplikacji sieci web hello przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), i korzystania z aplikacji sieci web zawartości toohello Git toodeploy próbki kodu HTML.

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux. Po zainstalowaniu wymagań wstępnych hello trwa około pięciu minut toocomplete hello kroki.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego przewodnika Szybki Start:

- [Zainstaluj oprogramowanie Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Pobierz przykładowe hello

W oknie terminalu Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Możesz to toorun okno terminalu wszystkie polecenia hello w tego przewodnika Szybki Start.

## <a name="view-hello-html"></a>Witaj widok HTML

Przejdź toohello katalog, który zawiera przykładowy hello HTML. Otwórz hello *index.html* plik w przeglądarce.

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pusta strona aplikacji sieci Web](media/app-service-web-get-started-html/app-service-web-service-created.png)

Na platformie Azure została utworzona nowa pusta aplikacja internetowa.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Przeglądaj toohello aplikacji

W przeglądarce odwiedź adres URL aplikacji sieci web platformy Azure toohello:

```
http://<app_name>.azurewebsites.net
```

Strona Hello jest uruchomiona jako aplikacja sieci web usługi aplikacji Azure.

![Strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Gratulacje!** Z pierwszej aplikacji HTML tooApp usługi została wdrożona.

## <a name="update-and-redeploy-hello-app"></a>Aktualizowanie i wdrożenie aplikacji hello

Otwórz hello *index.html* plik w edytorze tekstów, a następnie wprowadź znaczników toohello zmiany. Na przykład zmienić nagłówek hello H1 z toojust "Azure aplikacji usługi — przykład statycznego HTML witryna" "Usługa aplikacji Azure".

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git commit -am "updated HTML"
git push azure master
```

Po zakończeniu wdrożenia należy odświeżyć zmiany hello toosee przeglądarki.

![Zaktualizowana strona główna przykładowej aplikacji](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Zarządzanie nową aplikacją sieci Web platformy Azure

Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-html/portal1.png)

Zostanie wyświetlona strona Omówienie aplikacji internetowej. Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. 

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-get-started-html/portal2.png)

menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Mapowanie domeny niestandardowej](app-service-web-tutorial-custom-domain.md)
