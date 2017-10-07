---
title: "Samouczek wystąpień kontenera aaaAzure — przygotowanie rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Samouczek wystąpień kontenera platformy Azure — przygotowanie rejestru kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Wdrażanie i użytkowanie rejestru kontenera platformy Azure

Jest to część dwa trzech części samouczka. W hello [poprzedniego kroku](./container-instances-tutorial-prepare-app.md), obrazu kontener został utworzony dla prostą aplikację sieci web napisany w [Node.js](http://nodejs.org). W tym samouczku ten obraz jest wypychana tooan rejestru kontenera platformy Azure. Jeśli nie utworzono hello kontener obrazu, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazu](./container-instances-tutorial-prepare-app.md). 

Witaj rejestru kontenera Azure jest rejestru Azure, prywatnego obrazów kontenera Docker. Ten samouczek przeprowadzi Cię przez wdrożenie wystąpienia rejestru kontenera Azure i wypychanie tooit obrazu kontenera. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Wdrażanie wystąpienia rejestru kontenera platformy Azure
> * Znakowanie kontener obrazu do rejestru kontenera platformy Azure
> * Przekazywanie obrazu tooAzure rejestru kontenera

W kolejnych samouczkach kontenera hello jest wdrażanie z sieci prywatnej rejestru tooAzure wystąpień kontenera.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Ten samouczek wymaga, że używasz wersji interfejsu wiersza polecenia Azure hello 2.0.4 lub nowszym. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Wdrażanie rejestru kontenera platformy Azure

W przypadku wdrażania rejestru kontenera platformy Azure, musisz najpierw grupę zasobów. Grupy zasobów platformy Azure jest logiczną kolekcji, w której maszyny wirtualne Azure zasoby są wdrażane i zarządzane.

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. W tym przykładzie grupy zasobów o nazwie *myResourceGroup* jest tworzony w hello *eastus* regionu.

```azurecli
az group create --name myResourceGroup --location eastus
```

Tworzenie kontenera Azure rejestru z hello [az acr utworzyć](/cli/azure/acr#create) polecenia. Nazwa rejestru kontenera Hello **muszą być unikatowe**. W hello poniższy przykład, używamy nazwy hello *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

W całym hello pozostałej części tego samouczka, używamy `<acrname>` jako hello kontenera rejestru nazwę, który został wybrany.

## <a name="container-registry-login"></a>Kontener rejestru logowania

Wystąpienie ACR tooyour należy zalogować się przed wypchnięciem tooit obrazów. Użyj hello [logowania acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) polecenia toocomplete hello operacji. Należy tooprovide hello unikatową nazwę podane toohello rejestru kontenera podczas jej tworzenia.

```azurecli
az acr login --name <acrName>
```

polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.

## <a name="tag-container-image"></a>Tag obrazu kontenera

toodeploy obraz kontenera z rejestru prywatnej obraz powitania musi toobe oznaczane hello `loginServer` nazwa hello rejestru.

listy obrazów bieżący, użyj hello toosee `docker images` polecenia.

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

tooget hello loginServer nazwa, uruchom następujące polecenie hello.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Tag hello *aci samouczek aplikacji* obrazu o loginServer hello hello kontenera rejestru. Ponadto Dodaj `:v1` toohello koniec hello nazwę obrazu. Znacznik określa numer wersji obrazu hello.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Po oznakowany, uruchom `docker images` tooverify hello operacji.

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Wypychanie tooAzure obrazu rejestru kontenera

Wypychanie hello *aci samouczek aplikacji* rejestru toohello obrazu.

Przy użyciu hello poniższy przykład, zastąp nazwę loginServer rejestru kontenera hello loginServer hello ze środowiska.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Listy obrazów w rejestrze kontenera platformy Azure

listy obrazów, do których został przypisany do rejestru kontenera Azure tooyour, hello użytkownika tooreturn [listy repozytorium acr az](/cli/azure/acr/repository#list) polecenia. Aktualizacja polecenia hello hello kontenera rejestru nazwy.

```azurecli
az acr repository list --name <acrName> --output table
```

Dane wyjściowe:

```azurecli
Result
----------------
aci-tutorial-app
```

A następnie toosee hello tagi dla określonego obrazu, użyj hello [az acr repozytorium Pokaż znaczniki](/cli/azure/acr/repository#show-tags) polecenia.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Dane wyjściowe:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku rejestru kontenera platformy Azure został przygotowany do użycia z wystąpień kontenera Azure i hello kontenera obraz został naciśnięty. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Wdrażanie wystąpienia rejestru kontenera platformy Azure
> * Znakowanie kontener obrazu do rejestru kontenera platformy Azure
> * Przekazywanie obrazu tooAzure rejestru kontenera

Przejdź dalej toolearn samouczka toohello o wdrażaniu hello tooAzure kontenera za pomocą wystąpień kontenera platformy Azure.

> [!div class="nextstepaction"]
> [Wdrażanie kontenerów tooAzure wystąpień kontenera](./container-instances-tutorial-deploy-app.md)
