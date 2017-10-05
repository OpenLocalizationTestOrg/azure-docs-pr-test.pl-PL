---
title: "Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Za pomocą poleceń w tym artykule jest możliwe tworzenie i zarządzanie nimi w aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.
Można uruchomić przy użyciu nowej wersji interfejsu wiersza polecenia na dwa sposoby:

* [Instalowanie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.
* Przy użyciu [powłoki chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Tworzenie planu usługi aplikacji w systemie Linux

Aby utworzyć Plan usługi aplikacji systemu Linux, służy następujące polecenie:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Tworzenie niestandardowych kontenera Docker aplikacji sieci Web

Aby utworzyć aplikację sieci web i konfigurowanie go uruchomić niestandardowego kontenera Docker, służy następujące polecenie:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a>Aktywacja rejestrowania kontenera Docker

Aby aktywować rejestrowania kontenera Docker, służy następujące polecenie:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Zmiana niestandardowych kontenera Docker istniejącą aplikację sieci Web w aplikacji dla systemu Linux

Aby zmienić utworzonej wcześniej aplikacji, z bieżącego obrazu Docker do nowego obrazu, można użyć następującego polecenia:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Przy użyciu obrazy usługi Docker z rejestru prywatnych

Możesz skonfigurować aplikację, aby używać obrazów z rejestru prywatnych. Musisz podać adres url do rejestru, nazwę użytkownika i hasło. Można to osiągnąć przy użyciu następującego polecenia:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Włącz ciągłego wdrożenia niestandardowe obrazy usługi Docker

Za pomocą następującego polecenia można włączyć funkcję CD i uzyskać adres url elementu webhook. Ten adres url, można skonfigurować repozytoriów DockerHub lub rejestru kontenera platformy Azure.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Tworzenie aplikacji sieci Web w aplikacji systemu Linux przy użyciu jednej z naszych struktur wbudowanych środowiska wykonawczego

Aby utworzyć aplikację sieci Web 5.6 PHP w systemie Linux aplikacji który, służy następujące polecenie.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Zmień wersję framework dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux

Aby zmienić utworzonej wcześniej aplikacji, z bieżącej wersji framework do Node.js 6.11, można użyć następującego polecenia:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Konfigurowanie wdrożenia Git dla aplikacji sieci Web

Aby skonfigurować wdrożenia Git dla aplikacji, służy następujące polecenie:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Zainstaluj interfejs wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Powłoka chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)
* [Konfigurowanie środowisk w usłudze Azure App Service przejściowych](./web-sites-staged-publishing.md)
* [Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md)
