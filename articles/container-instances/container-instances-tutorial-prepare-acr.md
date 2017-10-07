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
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="2830a-104">Wdrażanie i użytkowanie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="2830a-105">Jest to część dwa trzech części samouczka.</span><span class="sxs-lookup"><span data-stu-id="2830a-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="2830a-106">W hello [poprzedniego kroku](./container-instances-tutorial-prepare-app.md), obrazu kontener został utworzony dla prostą aplikację sieci web napisany w [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="2830a-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="2830a-107">W tym samouczku ten obraz jest wypychana tooan rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2830a-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="2830a-108">Jeśli nie utworzono hello kontener obrazu, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazu](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="2830a-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="2830a-109">Witaj rejestru kontenera Azure jest rejestru Azure, prywatnego obrazów kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="2830a-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="2830a-110">Ten samouczek przeprowadzi Cię przez wdrożenie wystąpienia rejestru kontenera Azure i wypychanie tooit obrazu kontenera.</span><span class="sxs-lookup"><span data-stu-id="2830a-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="2830a-111">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="2830a-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2830a-112">Wdrażanie wystąpienia rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="2830a-113">Znakowanie kontener obrazu do rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="2830a-114">Przekazywanie obrazu tooAzure rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="2830a-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="2830a-115">W kolejnych samouczkach kontenera hello jest wdrażanie z sieci prywatnej rejestru tooAzure wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="2830a-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2830a-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2830a-116">Before you begin</span></span>

<span data-ttu-id="2830a-117">Ten samouczek wymaga, że używasz wersji interfejsu wiersza polecenia Azure hello 2.0.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="2830a-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2830a-118">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="2830a-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2830a-119">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2830a-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="2830a-120">Wdrażanie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="2830a-121">W przypadku wdrażania rejestru kontenera platformy Azure, musisz najpierw grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="2830a-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="2830a-122">Grupy zasobów platformy Azure jest logiczną kolekcji, w której maszyny wirtualne Azure zasoby są wdrażane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="2830a-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="2830a-123">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2830a-124">W tym przykładzie grupy zasobów o nazwie *myResourceGroup* jest tworzony w hello *eastus* regionu.</span><span class="sxs-lookup"><span data-stu-id="2830a-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2830a-125">Tworzenie kontenera Azure rejestru z hello [az acr utworzyć](/cli/azure/acr#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="2830a-126">Nazwa rejestru kontenera Hello **muszą być unikatowe**.</span><span class="sxs-lookup"><span data-stu-id="2830a-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="2830a-127">W hello poniższy przykład, używamy nazwy hello *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="2830a-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="2830a-128">W całym hello pozostałej części tego samouczka, używamy `<acrname>` jako hello kontenera rejestru nazwę, który został wybrany.</span><span class="sxs-lookup"><span data-stu-id="2830a-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="2830a-129">Kontener rejestru logowania</span><span class="sxs-lookup"><span data-stu-id="2830a-129">Container registry login</span></span>

<span data-ttu-id="2830a-130">Wystąpienie ACR tooyour należy zalogować się przed wypchnięciem tooit obrazów.</span><span class="sxs-lookup"><span data-stu-id="2830a-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="2830a-131">Użyj hello [logowania acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) polecenia toocomplete hello operacji.</span><span class="sxs-lookup"><span data-stu-id="2830a-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="2830a-132">Należy tooprovide hello unikatową nazwę podane toohello rejestru kontenera podczas jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="2830a-133">polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="2830a-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="2830a-134">Tag obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="2830a-134">Tag container image</span></span>

<span data-ttu-id="2830a-135">toodeploy obraz kontenera z rejestru prywatnej obraz powitania musi toobe oznaczane hello `loginServer` nazwa hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="2830a-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="2830a-136">listy obrazów bieżący, użyj hello toosee `docker images` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="2830a-137">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2830a-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="2830a-138">tooget hello loginServer nazwa, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="2830a-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="2830a-139">Tag hello *aci samouczek aplikacji* obrazu o loginServer hello hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="2830a-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="2830a-140">Ponadto Dodaj `:v1` toohello koniec hello nazwę obrazu.</span><span class="sxs-lookup"><span data-stu-id="2830a-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="2830a-141">Znacznik określa numer wersji obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="2830a-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="2830a-142">Po oznakowany, uruchom `docker images` tooverify hello operacji.</span><span class="sxs-lookup"><span data-stu-id="2830a-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="2830a-143">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2830a-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="2830a-144">Wypychanie tooAzure obrazu rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="2830a-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="2830a-145">Wypychanie hello *aci samouczek aplikacji* rejestru toohello obrazu.</span><span class="sxs-lookup"><span data-stu-id="2830a-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="2830a-146">Przy użyciu hello poniższy przykład, zastąp nazwę loginServer rejestru kontenera hello loginServer hello ze środowiska.</span><span class="sxs-lookup"><span data-stu-id="2830a-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="2830a-147">Listy obrazów w rejestrze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="2830a-148">listy obrazów, do których został przypisany do rejestru kontenera Azure tooyour, hello użytkownika tooreturn [listy repozytorium acr az](/cli/azure/acr/repository#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="2830a-149">Aktualizacja polecenia hello hello kontenera rejestru nazwy.</span><span class="sxs-lookup"><span data-stu-id="2830a-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="2830a-150">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2830a-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="2830a-151">A następnie toosee hello tagi dla określonego obrazu, użyj hello [az acr repozytorium Pokaż znaczniki](/cli/azure/acr/repository#show-tags) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2830a-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="2830a-152">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2830a-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="2830a-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2830a-153">Next steps</span></span>

<span data-ttu-id="2830a-154">W tym samouczku rejestru kontenera platformy Azure został przygotowany do użycia z wystąpień kontenera Azure i hello kontenera obraz został naciśnięty.</span><span class="sxs-lookup"><span data-stu-id="2830a-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="2830a-155">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2830a-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2830a-156">Wdrażanie wystąpienia rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="2830a-157">Znakowanie kontener obrazu do rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2830a-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="2830a-158">Przekazywanie obrazu tooAzure rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="2830a-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="2830a-159">Przejdź dalej toolearn samouczka toohello o wdrażaniu hello tooAzure kontenera za pomocą wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2830a-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2830a-160">Wdrażanie kontenerów tooAzure wystąpień kontenera</span><span class="sxs-lookup"><span data-stu-id="2830a-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
