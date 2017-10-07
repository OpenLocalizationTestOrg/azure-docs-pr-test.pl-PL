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
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="e1c26-103">Tworzenie rejestru kontenera zarządzanych przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e1c26-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="e1c26-104">Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="e1c26-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="e1c26-105">Szczegóły tego Przewodnik tworzenia zarządzanego wystąpienia rejestru kontenera Azure za pomocą portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e1c26-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="e1c26-106">Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="e1c26-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="e1c26-107">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="e1c26-107">Log in tooAzure</span></span>

<span data-ttu-id="e1c26-108">Zaloguj się za toohello portalu Azure w http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e1c26-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="e1c26-109">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="e1c26-109">Create a container registry</span></span>

1. <span data-ttu-id="e1c26-110">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c26-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="e1c26-111">Marketplace hello wyszukiwania dla **rejestru kontenera platformy Azure** i zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="e1c26-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="e1c26-112">Kliknij przycisk **Utwórz** który zostanie otwarty blok tworzenia hello ACR.</span><span class="sxs-lookup"><span data-stu-id="e1c26-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="e1c26-114">W hello **rejestru kontenera Azure** bloku, wprowadź hello następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="e1c26-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="e1c26-115">Po zakończeniu kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e1c26-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="e1c26-116">a.</span><span class="sxs-lookup"><span data-stu-id="e1c26-116">a.</span></span> <span data-ttu-id="e1c26-117">**Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru.</span><span class="sxs-lookup"><span data-stu-id="e1c26-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="e1c26-118">W tym przykładzie nazwa rejestru hello jest *myAzureContainerRegistry1*, ale podstawić własną unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="e1c26-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="e1c26-119">Nazwa Hello może zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="e1c26-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="e1c26-120">b.</span><span class="sxs-lookup"><span data-stu-id="e1c26-120">b.</span></span> <span data-ttu-id="e1c26-121">**Grupa zasobów**: Wybierz istniejący [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.</span><span class="sxs-lookup"><span data-stu-id="e1c26-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="e1c26-122">c.</span><span class="sxs-lookup"><span data-stu-id="e1c26-122">c.</span></span> <span data-ttu-id="e1c26-123">**Lokalizacja**: Wybierz lokalizację centrum danych Azure, gdzie usługa hello jest [dostępne](https://azure.microsoft.com/regions/services/), takich jak **południowo-środkowe stany**.</span><span class="sxs-lookup"><span data-stu-id="e1c26-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="e1c26-124">d.</span><span class="sxs-lookup"><span data-stu-id="e1c26-124">d.</span></span> <span data-ttu-id="e1c26-125">**Administrator**: należy włączyć rejestru hello tooaccess użytkownika Administrator.</span><span class="sxs-lookup"><span data-stu-id="e1c26-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="e1c26-126">Można zmienić to ustawienie po utworzeniu hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="e1c26-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="e1c26-127">e.</span><span class="sxs-lookup"><span data-stu-id="e1c26-127">e.</span></span> <span data-ttu-id="e1c26-128">**Użyj zarządzanego rejestru**: kliknij przycisk Tak toohave ACR automatycznie zarządzać magazynem rejestru hello, użyj elementów webhook, a uwierzytelnianie usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e1c26-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="e1c26-129">f.</span><span class="sxs-lookup"><span data-stu-id="e1c26-129">f.</span></span> <span data-ttu-id="e1c26-130">**Warstwa cenowa**: wybierz warstwę cenową; zobacz cennik usługi ACR, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e1c26-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="e1c26-131">Zaloguj się w wystąpieniu tooACR</span><span class="sxs-lookup"><span data-stu-id="e1c26-131">Log in tooACR instance</span></span>

<span data-ttu-id="e1c26-132">Przed wypychanie i ściąganie kontener obrazów, należy zalogować się toohello ACR wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e1c26-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="e1c26-133">toodo tak, użycie hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e1c26-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="e1c26-134">Po pierwsze, w razie potrzeby zaloguj się do platformy Azure przy użyciu hello [logowania az](/cli/azure/#login) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e1c26-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="e1c26-135">Następnie użyj hello [logowania acr az](/cli/azure/acr#login) toolog polecenia w toohello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c26-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="e1c26-136">Korzystanie z usługi Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="e1c26-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="e1c26-137">Tworzenie listy obrazów kontenerów</span><span class="sxs-lookup"><span data-stu-id="e1c26-137">List container images</span></span>

<span data-ttu-id="e1c26-138">Użyj hello `az acr` polecenia interfejsu wiersza polecenia tooquery hello obrazów i tagów w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="e1c26-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c26-139">Obecnie rejestru kontenera nie obsługuje hello `docker search` tooquery polecenia dla obrazów i tagów.</span><span class="sxs-lookup"><span data-stu-id="e1c26-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="e1c26-140">Tworzenie listy repozytoriów</span><span class="sxs-lookup"><span data-stu-id="e1c26-140">List repositories</span></span>

<span data-ttu-id="e1c26-141">Hello poniższym przykładzie przedstawiono repozytoria hello w rejestrze, w formacie JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="e1c26-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="e1c26-142">Tworzenie listy tagów</span><span class="sxs-lookup"><span data-stu-id="e1c26-142">List tags</span></span>

<span data-ttu-id="e1c26-143">Witaj poniższy przykład zawiera tagi hello na powitania **przykłady/nginx** repozytorium, w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="e1c26-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="e1c26-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1c26-144">Next steps</span></span>

<span data-ttu-id="e1c26-145">W tym szybki start zostanie utworzona zarządzanego wystąpienia rejestru kontenera Azure za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c26-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1c26-146">Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="e1c26-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
