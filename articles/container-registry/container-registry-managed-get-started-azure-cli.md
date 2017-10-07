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
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="dfdf0-103">Tworzenie rejestru kontenera zarządzanych przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dfdf0-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="dfdf0-104">Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="dfdf0-105">Szczegóły tego Przewodnik tworzenia zarządzanego wystąpienia rejestru kontenera Azure za pomocą interfejsu wiersza polecenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="dfdf0-106">Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dfdf0-107">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dfdf0-108">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dfdf0-109">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dfdf0-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="dfdf0-110">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="dfdf0-110">Create a resource group</span></span>

<span data-ttu-id="dfdf0-111">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="dfdf0-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="dfdf0-113">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westcentralus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="dfdf0-114">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="dfdf0-114">Create a container registry</span></span>

<span data-ttu-id="dfdf0-115">Utwórz wystąpienie ACR przy użyciu hello [az acr utworzyć](/cli/azure/acr#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="dfdf0-116">Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="dfdf0-117">Nazwa rejestru Hello w przykładzie hello jest *myContainerRegistry1*, podstawić własną unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="dfdf0-118">Po utworzeniu rejestru hello dane wyjściowe hello jest podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="dfdf0-118">When hello registry is created, hello output is similar toohello following:</span></span>

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

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="dfdf0-119">Zaloguj się w wystąpieniu tooACR</span><span class="sxs-lookup"><span data-stu-id="dfdf0-119">Log in tooACR instance</span></span>

<span data-ttu-id="dfdf0-120">Przed wypychanie i ściąganie kontener obrazów, należy zalogować się toohello ACR wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="dfdf0-121">toodo tak, użycie hello [logowania acr az](/cli/azure/acr#login) polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="dfdf0-122">polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="dfdf0-123">Korzystanie z usługi Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="dfdf0-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="dfdf0-124">Tworzenie listy obrazów kontenerów</span><span class="sxs-lookup"><span data-stu-id="dfdf0-124">List container images</span></span>

<span data-ttu-id="dfdf0-125">Użyj hello `az acr` polecenia interfejsu wiersza polecenia tooquery hello obrazów i tagów w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="dfdf0-126">Obecnie rejestru kontenera nie obsługuje hello `docker search` tooquery polecenia dla obrazów i tagów.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="dfdf0-127">Tworzenie listy repozytoriów</span><span class="sxs-lookup"><span data-stu-id="dfdf0-127">List repositories</span></span>

<span data-ttu-id="dfdf0-128">Hello poniższym przykładzie przedstawiono repozytoria hello w rejestrze, w formacie JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="dfdf0-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="dfdf0-129">Tworzenie listy tagów</span><span class="sxs-lookup"><span data-stu-id="dfdf0-129">List tags</span></span>

<span data-ttu-id="dfdf0-130">Witaj poniższy przykład zawiera tagi hello na powitania **przykłady/nginx** repozytorium, w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="dfdf0-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="dfdf0-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dfdf0-131">Next steps</span></span>

<span data-ttu-id="dfdf0-132">W tym szybki start zostanie utworzona zarządzanego wystąpienia rejestru kontenera Azure za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dfdf0-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dfdf0-133">Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="dfdf0-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
