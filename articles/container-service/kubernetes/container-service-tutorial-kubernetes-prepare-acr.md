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
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="38f53-104">Wdrażanie i użytkowanie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38f53-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="38f53-105">Rejestru kontenera platformy Azure (ACR) to Azure, prywatnego rejestru dla obrazów kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="38f53-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="38f53-106">Ten samouczek, część dwa siedmiu, przeprowadzi Cię przez wdrożenie wystąpienia rejestru kontenera Azure i wypychanie tooit obrazu kontenera.</span><span class="sxs-lookup"><span data-stu-id="38f53-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="38f53-107">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="38f53-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38f53-108">Wdrażanie wystąpienia rejestru kontenera platformy Azure (ACR)</span><span class="sxs-lookup"><span data-stu-id="38f53-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="38f53-109">Znakowanie obrazu kontener dla ACR</span><span class="sxs-lookup"><span data-stu-id="38f53-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="38f53-110">Przekazywanie hello tooACR obrazu</span><span class="sxs-lookup"><span data-stu-id="38f53-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="38f53-111">W kolejnych samouczkach tego wystąpienia ACR jest zintegrowany z klastra Kubernetes usługi kontenera platformy Azure, aby bezpiecznie pracować z kontenera obrazów.</span><span class="sxs-lookup"><span data-stu-id="38f53-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="38f53-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="38f53-112">Before you begin</span></span>

<span data-ttu-id="38f53-113">W hello [poprzedniego samouczek](./container-service-tutorial-kubernetes-prepare-app.md), obrazu kontener został utworzony dla prostą aplikację Azure głosu.</span><span class="sxs-lookup"><span data-stu-id="38f53-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="38f53-114">W tym samouczku ten obraz jest wypychana tooan rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38f53-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="38f53-115">Jeśli nie utworzono hello Azure głosowania obraz aplikacji, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="38f53-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="38f53-116">Alternatywnie hello kroki szczegółowe tutaj współpracują z żadnego obrazu kontenera.</span><span class="sxs-lookup"><span data-stu-id="38f53-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="38f53-117">Ten samouczek wymaga, że używasz wersji interfejsu wiersza polecenia Azure hello 2.0.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="38f53-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="38f53-118">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="38f53-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="38f53-119">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38f53-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="38f53-120">Wdrażanie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38f53-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="38f53-121">W przypadku wdrażania rejestru kontenera platformy Azure, musisz najpierw grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="38f53-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="38f53-122">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="38f53-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="38f53-123">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="38f53-124">W tym przykładzie grupy zasobów o nazwie *myResourceGroup* jest tworzony w hello *westeurope* regionu.</span><span class="sxs-lookup"><span data-stu-id="38f53-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="38f53-125">Tworzenie kontenera Azure rejestru z hello [az acr utworzyć](/cli/azure/acr#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="38f53-126">Nazwa rejestru kontenera Hello **muszą być unikatowe**.</span><span class="sxs-lookup"><span data-stu-id="38f53-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="38f53-127">W całym hello pozostałej części tego samouczka używamy "acrname" jako symbolu zastępczego dla hello kontenera rejestru nazwy, która została wybrana opcja.</span><span class="sxs-lookup"><span data-stu-id="38f53-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="38f53-128">Kontener rejestru logowania</span><span class="sxs-lookup"><span data-stu-id="38f53-128">Container registry login</span></span>

<span data-ttu-id="38f53-129">Wystąpienie ACR tooyour należy zalogować się przed wypchnięciem tooit obrazów.</span><span class="sxs-lookup"><span data-stu-id="38f53-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="38f53-130">Użyj hello [logowania acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) polecenia toocomplete hello operacji.</span><span class="sxs-lookup"><span data-stu-id="38f53-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="38f53-131">Należy tooprovide hello unikatową nazwę podane toohello rejestru kontenera podczas jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="38f53-132">polecenie Hello zwraca komunikat "Logowanie zakończyło się pomyślnie." po ukończeniu.</span><span class="sxs-lookup"><span data-stu-id="38f53-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="38f53-133">Tag kontener obrazów</span><span class="sxs-lookup"><span data-stu-id="38f53-133">Tag container images</span></span>

<span data-ttu-id="38f53-134">Obraz każdego kontenera musi toobe oznakowane o nazwie loginServer hello hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="38f53-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="38f53-135">Ten tag jest używane do przesyłania przypadku wypychania kontener obrazów tooan obrazu rejestru.</span><span class="sxs-lookup"><span data-stu-id="38f53-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="38f53-136">listy obrazów bieżący, użyj hello toosee [obrazy usługi docker](https://docs.docker.com/engine/reference/commandline/images/) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="38f53-137">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="38f53-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="38f53-138">tooget hello loginServer nazwa, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="38f53-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="38f53-139">Teraz, tag hello *azure głos początku* obrazu o loginServer hello hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="38f53-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="38f53-140">Ponadto Dodaj `:redis-v1` toohello koniec hello nazwę obrazu.</span><span class="sxs-lookup"><span data-stu-id="38f53-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="38f53-141">Znacznik określa hello wersję obrazu.</span><span class="sxs-lookup"><span data-stu-id="38f53-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="38f53-142">Po oznakowany, należy uruchomić [obrazy usługi docker] operacji hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="38f53-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="38f53-143">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="38f53-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="38f53-144">Wypychanie tooregistry obrazów</span><span class="sxs-lookup"><span data-stu-id="38f53-144">Push images tooregistry</span></span>

<span data-ttu-id="38f53-145">Wypychanie hello *azure głos początku* rejestru toohello obrazu.</span><span class="sxs-lookup"><span data-stu-id="38f53-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="38f53-146">Przy użyciu hello poniższy przykład, zastąp nazwę loginServer ACR hello loginServer hello ze środowiska.</span><span class="sxs-lookup"><span data-stu-id="38f53-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="38f53-147">Trwa to kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="38f53-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="38f53-148">Listy obrazów w rejestrze</span><span class="sxs-lookup"><span data-stu-id="38f53-148">List images in registry</span></span>

<span data-ttu-id="38f53-149">listy obrazów, do których został przypisany do rejestru kontenera Azure tooyour, hello użytkownika tooreturn [listy repozytorium acr az](/cli/azure/acr/repository#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="38f53-150">Aktualizacja polecenia hello hello ACR wystąpienia nazwy.</span><span class="sxs-lookup"><span data-stu-id="38f53-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="38f53-151">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="38f53-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="38f53-152">A następnie toosee hello tagi dla określonego obrazu, użyj hello [az acr repozytorium Pokaż znaczniki](/cli/azure/acr/repository#show-tags) polecenia.</span><span class="sxs-lookup"><span data-stu-id="38f53-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="38f53-153">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="38f53-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="38f53-154">Po ukończeniu samouczka hello kontener obrazu przechowywanych w prywatnej wystąpienia rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38f53-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="38f53-155">Ten obraz jest rozmieszczany z klastra Kubernetes tooa ACR w kolejnych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="38f53-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f53-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38f53-156">Next steps</span></span>

<span data-ttu-id="38f53-157">W tym samouczku rejestru kontenera Azure zostało przygotowane do użycia w klastrze ACS Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="38f53-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="38f53-158">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38f53-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38f53-159">Wdrożone wystąpienie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38f53-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="38f53-160">Tagged image kontenera dla ACR</span><span class="sxs-lookup"><span data-stu-id="38f53-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="38f53-161">Przekazane hello tooACR obrazu</span><span class="sxs-lookup"><span data-stu-id="38f53-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="38f53-162">Przejdź dalej toolearn samouczka toohello dotyczących wdrażania klastra Kubernetes na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="38f53-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38f53-163">Wdrażanie klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="38f53-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)