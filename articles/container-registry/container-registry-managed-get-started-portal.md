---
title: prywatne aaaCreate Docker rejestru - portalu Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello portalu Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Tworzenie rejestru kontenera zarządzanych przy użyciu hello portalu Azure

Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker. Szczegóły tego Przewodnik tworzenia zarządzanego wystąpienia rejestru kontenera Azure za pomocą portalu Azure hello.

Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za toohello portalu Azure w http://portal.azure.com.

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów

1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

2. Marketplace hello wyszukiwania dla **rejestru kontenera platformy Azure** i zaznacz je.

3. Kliknij przycisk **Utwórz** który zostanie otwarty blok tworzenia hello ACR.

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. W hello **rejestru kontenera Azure** bloku, wprowadź hello następujących informacji. Po zakończeniu kliknij przycisk **Utwórz**.

    a. **Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru. W tym przykładzie nazwa rejestru hello jest *myAzureContainerRegistry1*, ale podstawić własną unikatową nazwę. Nazwa Hello może zawierać tylko litery i cyfry.

    b. **Grupa zasobów**: Wybierz istniejący [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.

    c. **Lokalizacja**: Wybierz lokalizację centrum danych Azure, gdzie usługa hello jest [dostępne](https://azure.microsoft.com/regions/services/), takich jak **południowo-środkowe stany**.

    d. **Administrator**: należy włączyć rejestru hello tooaccess użytkownika Administrator. Można zmienić to ustawienie po utworzeniu hello rejestru.

    e. **Użyj zarządzanego rejestru**: kliknij przycisk Tak toohave ACR automatycznie zarządzać magazynem rejestru hello, użyj elementów webhook, a uwierzytelnianie usługi AAD.

    f. **Warstwa cenowa**: wybierz warstwę cenową; zobacz cennik usługi ACR, aby uzyskać więcej informacji.

## <a name="log-in-tooacr-instance"></a>Zaloguj się w wystąpieniu tooACR

Przed wypychanie i ściąganie kontener obrazów, należy zalogować się toohello ACR wystąpienia. 

toodo tak, użycie hello Azure CLI 2.0. Po pierwsze, w razie potrzeby zaloguj się do platformy Azure przy użyciu hello [logowania az](/cli/azure/#login) polecenia. 

```azurecli
az login
```

Następnie użyj hello [logowania acr az](/cli/azure/acr#login) toolog polecenia w toohello rejestru kontenera platformy Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

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

W tym szybki start zostanie utworzona zarządzanego wystąpienia rejestru kontenera Azure za pomocą hello portalu Azure.

> [!div class="nextstepaction"]
> [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
