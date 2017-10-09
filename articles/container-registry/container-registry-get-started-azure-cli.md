---
title: aaaCreate prywatnej rejestru kontenera Docker - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Utwórz prywatne rejestru kontenera Docker przy użyciu hello Azure CLI 2.0
Używanie poleceń w hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate rejestru kontenera i zarządzać jego ustawienia z komputera z systemem Linux, Mac lub Windows. Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md) lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Tło i pojęcia dla [hello — omówienie](container-registry-intro.md)
* Aby uzyskać pomoc dotyczącą polecenia interfejsu wiersza polecenia kontenera rejestru (`az acr` poleceń), Przekaż hello `-h` polecenia tooany parametru.


## <a name="prerequisites"></a>Wymagania wstępne
* **Azure CLI 2.0**: tooinstall i rozpoczynanie pracy z hello 2.0 interfejsu wiersza polecenia, zobacz hello [instrukcje dotyczące instalacji](/cli/azure/install-azure-cli). Zaloguj się za tooyour subskrypcji platformy Azure, uruchamiając `az login`. Aby uzyskać więcej informacji, zobacz [wprowadzenie hello 2.0 interfejsu wiersza polecenia](/cli/azure/get-started-with-azure-cli).
* **Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów. Upewnij się, że grupa zasobów hello znajduje się w lokalizacji hello usługa Rejestr kontenera [dostępne](https://azure.microsoft.com/regions/services/). grupy zasobów przy użyciu toocreate hello 2.0 interfejsu wiersza polecenia, zobacz [hello odwołanie 2.0 interfejsu wiersza polecenia](/cli/azure/group).
* **Konto magazynu** (opcjonalnie): Utwórz standardowy Azure [konta magazynu](../storage/common/storage-introduction.md) tooback hello kontener klucza rejestru hello tej samej lokalizacji. Jeśli nie określisz konta magazynu podczas tworzenia rejestru z `az acr create`, hello polecenie tworzy go dla Ciebie. toocreate przy użyciu konta magazynu hello 2.0 interfejsu wiersza polecenia, zobacz [hello odwołanie 2.0 interfejsu wiersza polecenia](/cli/azure/storage/account). Usługa Premium Storage nie jest obecnie obsługiwana.
* **Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru hello interfejsu wiersza polecenia, po domyślnie go nie ustawiono dostępu. W zależności od potrzeb, możesz przypisać istniejący Rejestr tooa główną usługi Azure Active Directory (lub Utwórz i Przypisz nowy), lub Włącz rejestru hello konta administratora. Zobacz hello sekcje w dalszej części tego artykułu. Aby uzyskać więcej informacji na temat dostępu do rejestru, zobacz [Uwierzytelnij z rejestru kontenera hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów
Uruchom hello `az acr create` toocreate polecenia rejestru kontenera.

> [!TIP]
> Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry. Nazwa rejestru Hello w przykładach hello jest `myRegistry1`, ale podstawić własną unikatową nazwę.
>
>

Witaj następujące polecenia używa hello minimalnego parametry toocreate kontenera rejestru `myRegistry1` w grupie zasobów hello `myResourceGroup`i przy użyciu hello *podstawowe* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* Parametr `--storage-account-name` jest opcjonalny. Jeśli nie jest określony, konto magazynu jest tworzony z nazwą składającą się z nazwy rejestru hello i sygnaturę czasową w hello określonej grupy zasobów.

Po utworzeniu rejestru hello dane wyjściowe hello jest podobne toohello następujące:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Zwróć szczególną uwagę na następujące elementy:

* `id`— Identyfikator rejestru hello w ramach subskrypcji, który jest wymagany, jeśli chcesz, aby tooassign nazwy głównej usługi.
* `loginServer`-hello Pełna nazwa należy określić zbyt[Zaloguj się w rejestrze toohello](container-registry-authentication.md). W tym przykładzie nazwa hello jest `myregistry1.exp.azurecr.io` (tylko małe litery).

## <a name="assign-a-service-principal"></a>Przypisywanie nazwy głównej usługi
Za pomocą interfejsu wiersza polecenia 2.0 polecenia tooassign rejestr tooa główną usługi Azure Active Directory. Witaj nazwy głównej usługi w tych przykładach przypisany hello właściciela roli, ale można przypisać [innych ról](../active-directory/role-based-access-control-configure.md) Jeśli chcesz.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Tworzenie nazwy głównej usługi i przypisywanie dostępu toohello rejestru
W hello następujące polecenia, nowej nazwy głównej usługi jest przypisywana właściciela roli dostępu toohello rejestru identyfikator przekazany z hello `--scopes` parametru. Określ silne hasło z hello `--password` parametru.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Przypisywanie istniejącej nazwy głównej usługi
Jeśli już masz nazwy głównej usługi i chcesz tooassign jej właściciela roli dostępu toohello rejestru, uruchom polecenie toohello podobne, poniższy przykład. Przekaż identyfikator podmiotu zabezpieczeń aplikacji usługi hello przy użyciu hello `--assignee` parametru:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Zarządzanie poświadczeniami administratora
Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone. Witaj w następujących przykładach `az acr` poświadczenia administratora hello toomanage rejestru kontenera polecenia interfejsu wiersza polecenia.

### <a name="obtain-admin-user-credentials"></a>Uzyskiwanie poświadczeń użytkownika administratora
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Włączanie użytkownika administratora dla istniejącego rejestru
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Wyłączanie użytkownika administratora dla istniejącego rejestru
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Tworzenie listy obrazów i tagów
Użyj hello `az acr` polecenia interfejsu wiersza polecenia tooquery hello obrazów i tagów w repozytorium.

> [!NOTE]
> Obecnie rejestru kontenera nie obsługuje hello `docker search` tooquery polecenia dla obrazów i tagów.


### <a name="list-repositories"></a>Tworzenie listy repozytoriów
Hello poniższym przykładzie przedstawiono repozytoria hello w rejestrze, w formacie JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Tworzenie listy tagów
Witaj poniższy przykład zawiera tagi hello na powitania **przykłady/nginx** repozytorium, w formacie JSON:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Następne kroki
* [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
