---
title: "Tworzenie prywatnego rejestru kontenerów platformy Docker — interfejs wiersza polecenia platformy Azure | Microsoft Doc"
description: "Rozpoczynanie pracy z tworzeniem prywatnych rejestrów kontenerów platformy Docker za pomocą interfejsu wiersza polecenia platformy Azure w wersji 2.0 i zarządzaniem nimi"
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
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="47264-103">Tworzenie zarządzanego rejestru kontenerów przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47264-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="47264-104">Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="47264-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="47264-105">W tym przewodniku znajdują się szczegółowe informacje dotyczące tworzenia zarządzanego wystąpienia usługi Azure Container Registry przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47264-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="47264-106">Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="47264-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="47264-107">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik szybkiego startu będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="47264-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="47264-108">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="47264-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="47264-109">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="47264-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="47264-110">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="47264-110">Create a resource group</span></span>

<span data-ttu-id="47264-111">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="47264-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="47264-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="47264-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="47264-113">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *westcentralus*.</span><span class="sxs-lookup"><span data-stu-id="47264-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="47264-114">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="47264-114">Create a container registry</span></span>

<span data-ttu-id="47264-115">Utwórz wystąpienie usługi ACR za pomocą polecenia [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="47264-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="47264-116">Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="47264-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="47264-117">W przykładzie nazwa rejestru to *myContainerRegistry1*, ale możesz ją zastąpić własną, unikatową nazwą.</span><span class="sxs-lookup"><span data-stu-id="47264-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="47264-118">Po utworzeniu rejestru dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="47264-118">When the registry is created, the output is similar to the following:</span></span>

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

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="47264-119">Logowanie do wystąpienia usługi ACR</span><span class="sxs-lookup"><span data-stu-id="47264-119">Log in to ACR instance</span></span>

<span data-ttu-id="47264-120">Przed wypychaniem i ściąganiem obrazów kontenerów musisz zalogować się do wystąpienia usługi ACR.</span><span class="sxs-lookup"><span data-stu-id="47264-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="47264-121">Aby to zrobić, użyj polecenia [az acr login](/cli/azure/acr#login).</span><span class="sxs-lookup"><span data-stu-id="47264-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="47264-122">Polecenie zwraca komunikat „Logowanie pomyślne” po ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="47264-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="47264-123">Korzystanie z usługi Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="47264-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="47264-124">Tworzenie listy obrazów kontenerów</span><span class="sxs-lookup"><span data-stu-id="47264-124">List container images</span></span>

<span data-ttu-id="47264-125">Użyj poleceń interfejsu wiersza polecenia `az acr` do tworzenia zapytań dotyczących obrazów i tagów w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="47264-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="47264-126">Obecnie usługa Container Registry nie obsługuje tworzenia zapytań dotyczących obrazów i tagów przy użyciu polecenia `docker search`.</span><span class="sxs-lookup"><span data-stu-id="47264-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="47264-127">Tworzenie listy repozytoriów</span><span class="sxs-lookup"><span data-stu-id="47264-127">List repositories</span></span>

<span data-ttu-id="47264-128">W poniższym przykładzie przedstawiono listę repozytoriów w rejestrze w formacie JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="47264-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="47264-129">Tworzenie listy tagów</span><span class="sxs-lookup"><span data-stu-id="47264-129">List tags</span></span>

<span data-ttu-id="47264-130">W poniższym przykładzie przedstawiono listę tagów w repozytorium **samples/nginx** w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="47264-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="47264-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47264-131">Next steps</span></span>

<span data-ttu-id="47264-132">W tym przewodniku Szybki start utworzono zarządzane wystąpienie usługi Azure Container Registry przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47264-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="47264-133">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md) (Wypychanie pierwszego obrazu za pomocą interfejsu wiersza polecenia platformy Docker)</span><span class="sxs-lookup"><span data-stu-id="47264-133">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md)</span></span>
