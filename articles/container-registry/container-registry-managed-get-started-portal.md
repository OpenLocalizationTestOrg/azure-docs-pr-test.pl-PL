---
title: "Tworzenie prywatnego rejestru platformy Docker — witryna Azure Portal | Microsoft Doc"
description: "Rozpoczynanie pracy z tworzeniem prywatnych rejestrów kontenerów platformy Docker za pomocą witryny Azure Portal i zarządzaniem nimi"
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
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="61933-103">Tworzenie zarządzanego rejestru kontenerów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61933-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="61933-104">Usługa Azure Container Registry to zarządzana usługa rejestru kontenerów platformy Docker używana do przechowywania prywatnych obrazów kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="61933-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="61933-105">W tym przewodniku znajdują się szczegółowe informacje dotyczące tworzenia zarządzanego wystąpienia usługi Azure Container Registry przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61933-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="61933-106">Zarządzane rejestry kontenerów platformy Azure są w wersji zapoznawczej i nie są dostępne we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="61933-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="61933-107">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61933-107">Log in to Azure</span></span>

<span data-ttu-id="61933-108">Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="61933-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="61933-109">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="61933-109">Create a container registry</span></span>

1. <span data-ttu-id="61933-110">Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61933-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="61933-111">W portalu Marketplace wyszukaj usługę **Azure Container Registry** i wybierz ją.</span><span class="sxs-lookup"><span data-stu-id="61933-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="61933-112">Kliknij pozycję **Utwórz**, aby otworzyć blok tworzenia usługi ACR.</span><span class="sxs-lookup"><span data-stu-id="61933-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="61933-114">W bloku usługi **Azure Container Registry** wprowadź następujące informacje.</span><span class="sxs-lookup"><span data-stu-id="61933-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="61933-115">Po zakończeniu kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="61933-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="61933-116">a.</span><span class="sxs-lookup"><span data-stu-id="61933-116">a.</span></span> <span data-ttu-id="61933-117">**Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru.</span><span class="sxs-lookup"><span data-stu-id="61933-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="61933-118">W tym przykładzie nazwa rejestru to *myAzureContainerRegistry1*, ale zastąp ją własną unikatową nazwą.</span><span class="sxs-lookup"><span data-stu-id="61933-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="61933-119">Nazwa może zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="61933-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="61933-120">b.</span><span class="sxs-lookup"><span data-stu-id="61933-120">b.</span></span> <span data-ttu-id="61933-121">**Grupa zasobów**: wybierz istniejącą [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub wprowadź nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="61933-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="61933-122">c.</span><span class="sxs-lookup"><span data-stu-id="61933-122">c.</span></span> <span data-ttu-id="61933-123">**Lokalizacja**: wybierz taką lokalizację centrum danych Azure, gdzie usługa jest [dostępna](https://azure.microsoft.com/regions/services/), na przykład **Południowo-środkowe stany USA**.</span><span class="sxs-lookup"><span data-stu-id="61933-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="61933-124">d.</span><span class="sxs-lookup"><span data-stu-id="61933-124">d.</span></span> <span data-ttu-id="61933-125">**Administrator**: jeśli chcesz, umożliw administratorowi dostęp do rejestru.</span><span class="sxs-lookup"><span data-stu-id="61933-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="61933-126">Po utworzeniu rejestru można zmienić to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="61933-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="61933-127">e.</span><span class="sxs-lookup"><span data-stu-id="61933-127">e.</span></span> <span data-ttu-id="61933-128">**Użyj rejestru zarządzanego**: wybierz opcję Tak, aby usługa ACR automatycznie zarządzała magazynem rejestru, korzystała z elementów webhook i używała uwierzytelniania w usłudze AAD.</span><span class="sxs-lookup"><span data-stu-id="61933-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="61933-129">f.</span><span class="sxs-lookup"><span data-stu-id="61933-129">f.</span></span> <span data-ttu-id="61933-130">**Warstwa cenowa**: wybierz warstwę cenową; zobacz cennik usługi ACR, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="61933-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="61933-131">Logowanie do wystąpienia usługi ACR</span><span class="sxs-lookup"><span data-stu-id="61933-131">Log in to ACR instance</span></span>

<span data-ttu-id="61933-132">Przed wypychaniem i ściąganiem obrazów kontenerów musisz zalogować się do wystąpienia usługi ACR.</span><span class="sxs-lookup"><span data-stu-id="61933-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="61933-133">Aby to zrobić, użyj interfejsu wiersza polecenia platformy Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="61933-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="61933-134">Najpierw, w razie potrzeby, zaloguj się do platformy Azure za pomocą polecenia [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="61933-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="61933-135">Następnie użyj polecenia [az acr login](/cli/azure/acr#login), aby zalogować się do usługi Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="61933-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="61933-136">Korzystanie z usługi Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="61933-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="61933-137">Tworzenie listy obrazów kontenerów</span><span class="sxs-lookup"><span data-stu-id="61933-137">List container images</span></span>

<span data-ttu-id="61933-138">Użyj poleceń interfejsu wiersza polecenia `az acr` do tworzenia zapytań dotyczących obrazów i tagów w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="61933-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="61933-139">Obecnie usługa Container Registry nie obsługuje tworzenia zapytań dotyczących obrazów i tagów przy użyciu polecenia `docker search`.</span><span class="sxs-lookup"><span data-stu-id="61933-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="61933-140">Tworzenie listy repozytoriów</span><span class="sxs-lookup"><span data-stu-id="61933-140">List repositories</span></span>

<span data-ttu-id="61933-141">W poniższym przykładzie przedstawiono listę repozytoriów w rejestrze w formacie JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="61933-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="61933-142">Tworzenie listy tagów</span><span class="sxs-lookup"><span data-stu-id="61933-142">List tags</span></span>

<span data-ttu-id="61933-143">W poniższym przykładzie przedstawiono listę tagów w repozytorium **samples/nginx** w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="61933-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="61933-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61933-144">Next steps</span></span>

<span data-ttu-id="61933-145">W tym przewodniku Szybki start utworzono zarządzane wystąpienie usługi Azure Container Registry za pomocą witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61933-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="61933-146">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md) (Wypychanie pierwszego obrazu za pomocą interfejsu wiersza polecenia platformy Docker)</span><span class="sxs-lookup"><span data-stu-id="61933-146">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md)</span></span>