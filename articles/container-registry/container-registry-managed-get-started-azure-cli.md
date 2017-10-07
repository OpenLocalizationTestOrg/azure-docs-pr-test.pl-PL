---
title: aaaCreate prywatnej rejestru kontenera Docker - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Tworzenie rejestru kontenera zarządzanych przy użyciu hello wiersza polecenia platformy Azure

Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker. Szczegóły tego Przewodnik tworzenia zarządzanego wystąpienia rejestru kontenera Azure za pomocą interfejsu wiersza polecenia Azure hello.

Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westcentralus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów

Utwórz wystąpienie ACR przy użyciu hello [az acr utworzyć](/cli/azure/acr#create) polecenia.

> [!NOTE]
> Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.

 Nazwa rejestru Hello w przykładzie hello jest *myContainerRegistry1*, podstawić własną unikatową nazwę.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Po utworzeniu rejestru hello dane wyjściowe hello jest podobne toohello następujące:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Zaloguj się w wystąpieniu tooACR

Przed wypychanie i ściąganie kontener obrazów, należy zalogować się toohello ACR wystąpienia. toodo tak, użycie hello [logowania acr az](/cli/azure/acr#login) polecenia.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.

## <a name="use-azure-container-registry"></a>Korzystanie z usługi Azure Container Registry

### <a name="list-container-images"></a>Tworzenie listy obrazów kontenerów

Użyj hello `az acr` polecenia interfejsu wiersza polecenia tooquery hello obrazów i tagów w repozytorium.

> [!NOTE]
> Obecnie rejestru kontenera nie obsługuje hello `docker search` tooquery polecenia dla obrazów i tagów.

### <a name="list-repositories"></a>Tworzenie listy repozytoriów

Hello poniższym przykładzie przedstawiono repozytoria hello w rejestrze, w formacie JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Tworzenie listy tagów

Witaj poniższy przykład zawiera tagi hello na powitania **przykłady/nginx** repozytorium, w formacie JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Następne kroki

W tym szybki start zostanie utworzona zarządzanego wystąpienia rejestru kontenera Azure za pomocą hello wiersza polecenia platformy Azure.

> [!div class="nextstepaction"]
> [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
