---
title: "Samouczek usługi kontenera aaaAzure — przygotowanie ACR | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — przygotowanie ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Wdrażanie i użytkowanie rejestru kontenera platformy Azure

Rejestru kontenera platformy Azure (ACR) to Azure, prywatnego rejestru dla obrazów kontenera Docker. Ten samouczek, część dwa siedmiu, przeprowadzi Cię przez wdrożenie wystąpienia rejestru kontenera Azure i wypychanie tooit obrazu kontenera. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Wdrażanie wystąpienia rejestru kontenera platformy Azure (ACR)
> * Znakowanie obrazu kontener dla ACR
> * Przekazywanie hello tooACR obrazu

W kolejnych samouczkach tego wystąpienia ACR jest zintegrowany z klastra Kubernetes usługi kontenera platformy Azure, aby bezpiecznie pracować z kontenera obrazów. 

## <a name="before-you-begin"></a>Przed rozpoczęciem

W hello [poprzedniego samouczek](./container-service-tutorial-kubernetes-prepare-app.md), obrazu kontener został utworzony dla prostą aplikację Azure głosu. W tym samouczku ten obraz jest wypychana tooan rejestru kontenera platformy Azure. Jeśli nie utworzono hello Azure głosowania obraz aplikacji, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). Alternatywnie hello kroki szczegółowe tutaj współpracują z żadnego obrazu kontenera.

Ten samouczek wymaga, że używasz wersji interfejsu wiersza polecenia Azure hello 2.0.4 lub nowszym. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Wdrażanie rejestru kontenera platformy Azure

W przypadku wdrażania rejestru kontenera platformy Azure, musisz najpierw grupę zasobów. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. W tym przykładzie grupy zasobów o nazwie *myResourceGroup* jest tworzony w hello *westeurope* regionu.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Tworzenie kontenera Azure rejestru z hello [az acr utworzyć](/cli/azure/acr#create) polecenia. Nazwa rejestru kontenera Hello **muszą być unikatowe**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

W całym hello pozostałej części tego samouczka używamy "acrname" jako symbolu zastępczego dla hello kontenera rejestru nazwy, która została wybrana opcja.

## <a name="container-registry-login"></a>Kontener rejestru logowania

Wystąpienie ACR tooyour należy zalogować się przed wypchnięciem tooit obrazów. Użyj hello [logowania acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) polecenia toocomplete hello operacji. Należy tooprovide hello unikatową nazwę podane toohello rejestru kontenera podczas jej tworzenia.

```azurecli
az acr login --name <acrName>
```

polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.

## <a name="tag-container-images"></a>Tag kontener obrazów

Obraz każdego kontenera musi toobe oznakowane o nazwie loginServer hello hello rejestru. Ten tag jest używane do przesyłania przypadku wypychania kontener obrazów tooan obrazu rejestru.

listy obrazów bieżący, użyj hello toosee [obrazy usługi docker](https://docs.docker.com/engine/reference/commandline/images/) polecenia.

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

tooget hello loginServer nazwa, uruchom następujące polecenie hello.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Teraz, tag hello *azure głos początku* obrazu o loginServer hello hello kontenera rejestru. Ponadto Dodaj `:redis-v1` toohello koniec hello nazwę obrazu. Znacznik określa hello wersję obrazu.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Po oznakowany, należy uruchomić [obrazy usługi docker] operacji hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Wypychanie tooregistry obrazów

Wypychanie hello *azure głos początku* rejestru toohello obrazu. 

Przy użyciu hello poniższy przykład, zastąp nazwę loginServer ACR hello loginServer hello ze środowiska.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Trwa to kilka minut toocomplete.

## <a name="list-images-in-registry"></a>Listy obrazów w rejestrze

listy obrazów, do których został przypisany do rejestru kontenera Azure tooyour, hello użytkownika tooreturn [listy repozytorium acr az](/cli/azure/acr/repository#list) polecenia. Aktualizacja polecenia hello hello ACR wystąpienia nazwy.

```azurecli
az acr repository list --name <acrName> --output table
```

Dane wyjściowe:

```azurecli
Result
----------------
azure-vote-front
```

A następnie toosee hello tagi dla określonego obrazu, użyj hello [az acr repozytorium Pokaż znaczniki](/cli/azure/acr/repository#show-tags) polecenia.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Dane wyjściowe:

```azurecli
Result
--------
redis-v1
```

Po ukończeniu samouczka hello kontener obrazu przechowywanych w prywatnej wystąpienia rejestru kontenera platformy Azure. Ten obraz jest rozmieszczany z klastra Kubernetes tooa ACR w kolejnych samouczkach.

## <a name="next-steps"></a>Następne kroki

W tym samouczku rejestru kontenera Azure zostało przygotowane do użycia w klastrze ACS Kubernetes. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Wdrożone wystąpienie rejestru kontenera platformy Azure
> * Tagged image kontenera dla ACR
> * Przekazane hello tooACR obrazu

Przejdź dalej toolearn samouczka toohello dotyczących wdrażania klastra Kubernetes na platformie Azure.

> [!div class="nextstepaction"]
> [Wdrażanie klastra Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md)