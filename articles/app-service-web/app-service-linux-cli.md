---
title: "aaaManage aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, interfejsu wiersza polecenia, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Za pomocą poleceń hello w tym artykule są toocreate stanie i zarządzać aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.
Możesz rozpocząć korzystanie z nowej wersji hello hello CLI na dwa sposoby:

* [Instalowanie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.
* Przy użyciu [powłoki chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Tworzenie planu usługi aplikacji w systemie Linux

toocreate Plan usługi aplikacji systemu Linux, możesz użyć hello następujące polecenie:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Tworzenie niestandardowych kontenera Docker aplikacji sieci Web

toocreate aplikacji sieci web i skonfigurowania go toorun kontener Docker niestandardowych, można użyć hello następujące polecenie:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Aktywacja rejestrowania kontenera Docker hello

tooactivate hello rejestrowania kontenera Docker, możesz użyć hello następujące polecenie:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Zmień hello niestandardowych kontenera Docker dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux

toochange utworzonej wcześniej aplikacji, z hello bieżącego Docker obrazu tooa nowy obraz, możesz użyć hello następujące polecenie:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Przy użyciu obrazy usługi Docker z rejestru prywatnych

Można skonfigurować obrazów toouse aplikacji z rejestru prywatnych. Adres url hello tooprovide potrzebę rejestru, nazwę użytkownika i hasło. Można to osiągnąć przy użyciu hello następujące polecenie:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Włącz ciągłego wdrożenia niestandardowe obrazy usługi Docker

Z hello następujące polecenia można włączyć funkcję CD hello i uzyskać adres url elementu webhook hello. Ten adres url może być używane tooconfigure możesz DockerHub lub rejestru kontenera Azure repozytoriów.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Tworzenie aplikacji sieci Web w aplikacji systemu Linux przy użyciu jednej z naszych struktur wbudowanych środowiska wykonawczego

toocreate 5.6 aplikacji sieci Web PHP na Linux aplikacji, których można używać hello następujące polecenia.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Zmień wersję framework dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux

toochange utworzonej wcześniej aplikacji, z tooNode.js hello do wersji bieżącej framework 6.11, możesz użyć hello następujące polecenie:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Konfigurowanie wdrożenia Git dla aplikacji sieci Web

tooset się wdrożenia Git dla aplikacji, można użyć hello następujące polecenie:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Zainstaluj interfejs wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Powłoka chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)
* [Konfigurowanie środowisk w usłudze Azure App Service przejściowych](./web-sites-staged-publishing.md)
* [Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md)
