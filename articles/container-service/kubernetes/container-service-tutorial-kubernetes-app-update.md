---
title: "Samouczek usługi kontenera aaaAzure — aktualizacja aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — aktualizacja aplikacji"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="9ed6a-104">Aktualizuj aplikację w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9ed6a-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="9ed6a-105">Po wdrożeniu aplikacji w Kubernetes może zostać zaktualizowana, podając nowy obraz kontenera lub wersję obrazu.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="9ed6a-106">Podczas aktualizacji aplikacji hello aktualizacji wdrożenia są przygotowywane powoduje, że tylko część wdrożenia hello jest jednocześnie zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="9ed6a-107">Ta aktualizacja przemieszczanego umożliwia uruchamianie procesu aktualizacji hello tookeep aplikacji hello i udostępnia mechanizm wycofywania w przypadku niepowodzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="9ed6a-108">W tym samouczku sześciu część siedmiu hello przykładową aplikację Azure głos jest aktualizowana.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="9ed6a-109">Zadania, które należy wykonać obejmują:</span><span class="sxs-lookup"><span data-stu-id="9ed6a-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ed6a-110">Aktualizowanie hello kod aplikacji frontonu</span><span class="sxs-lookup"><span data-stu-id="9ed6a-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="9ed6a-111">Tworzenie obrazu zaktualizowane kontenera</span><span class="sxs-lookup"><span data-stu-id="9ed6a-111">Creating an updated container image</span></span>
> * <span data-ttu-id="9ed6a-112">Wypychanie hello kontener obrazu tooAzure rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="9ed6a-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9ed6a-113">Wdrażanie hello zaktualizowano kontener obrazu</span><span class="sxs-lookup"><span data-stu-id="9ed6a-113">Deploying hello updated container image</span></span>

<span data-ttu-id="9ed6a-114">W kolejnych samouczkach Operations Management Suite jest skonfigurowany toomonitor hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9ed6a-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9ed6a-115">Before you begin</span></span>

<span data-ttu-id="9ed6a-116">W poprzednich samouczków aplikacji zostało umieszczone w obrazie kontenera, przekazać obraz powitania tooAzure rejestru kontenera i utworzyć klaster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="9ed6a-117">Aplikacja Hello następnie zostało uruchomione na powitania Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="9ed6a-118">Jeśli nie zostały wykonane następujące kroki i chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="9ed6a-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="9ed6a-119">Aktualizowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ed6a-119">Update application</span></span>

<span data-ttu-id="9ed6a-120">toocomplete hello kroki opisane w tym samouczku, użytkownik musi zostały sklonowane kopię hello Azure głos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="9ed6a-121">W razie potrzeby Utwórz tę kopię sklonowany z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9ed6a-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="9ed6a-122">Otwórz hello `config_file.cfg` pliku w dowolnym edytorze kodu i tekstu.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="9ed6a-123">Można znaleźć tego pliku w obszarze hello następującego katalogu hello sklonować repozytorium.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="9ed6a-124">Zmienianie wartości hello `VOTE1VALUE` i `VOTE2VALUE`, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="9ed6a-125">Użyj [rozwiązania docker compose](https://docs.docker.com/compose/) toore — tworzenie hello frontonu obrazu i aplikacji hello wykonywania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="9ed6a-126">Testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="9ed6a-126">Test application locally</span></span>

<span data-ttu-id="9ed6a-127">Przeglądaj zbyt`http://localhost:8080` toosee hello aktualizacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="9ed6a-129">Obrazy tagu i wypychania</span><span class="sxs-lookup"><span data-stu-id="9ed6a-129">Tag and push images</span></span>

<span data-ttu-id="9ed6a-130">Tag hello *azure głos początku* obrazu o loginServer hello hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="9ed6a-131">Jeśli używasz rejestru kontenera Azure Pobierz hello nazwa serwera logowania z hello [listy acr az](/cli/azure/acr#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="9ed6a-132">Użyj [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="9ed6a-133">Zastąp `<acrLoginServer>` z nazwą serwera logowania rejestru kontenera platformy Azure lub rejestru publicznej nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9ed6a-134">Użyj [wypychania docker](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello obrazu tooyour rejestru.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="9ed6a-135">Zastąp `<acrLoginServer>` z nazwą serwera logowania rejestru kontenera platformy Azure lub rejestru publicznej nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="9ed6a-136">Wdrażanie aktualizacji aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ed6a-136">Deploy update application</span></span>

<span data-ttu-id="9ed6a-137">Maksymalny czas działania tooensure wiele wystąpień pod aplikacji hello musi być uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="9ed6a-138">Sprawdź konfigurację tego z hello [kubectl Pobierz pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="9ed6a-139">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9ed6a-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="9ed6a-140">Jeśli masz wiele stanowiskami systemem hello azure głos początku obrazu skalować hello *azure głos początku* wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="9ed6a-141">tooupdate hello aplikacji, użyj hello [zestaw kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="9ed6a-142">Aktualizacja `<acrLoginServer>` z hello logowania serwera lub nazwę hosta rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9ed6a-143">toomonitor hello wdrożenia, użyj hello [kubectl Pobierz pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="9ed6a-144">Hello zaktualizowane aplikacja jest wdrażana, Twoje stanowiskami są zakończone i utworzony ponownie z hello nowego kontenera obrazu.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="9ed6a-145">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9ed6a-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="9ed6a-146">Zaktualizowano test aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ed6a-146">Test updated application</span></span>

<span data-ttu-id="9ed6a-147">Pobierz hello zewnętrzny adres IP hello *azure głos początku* usługi.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="9ed6a-148">Przeglądaj toohello IP address toosee hello aktualizacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-148">Browse toohello IP address toosee hello updated application.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="9ed6a-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ed6a-150">Next steps</span></span>

<span data-ttu-id="9ed6a-151">W tym samouczku aktualizacji aplikacji i wprowadzanie klastra Kubernetes tooa tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="9ed6a-152">Zakończono Hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="9ed6a-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ed6a-153">Kod aplikacji frontonu hello zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="9ed6a-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="9ed6a-154">Utworzony obraz zaktualizowane kontenera</span><span class="sxs-lookup"><span data-stu-id="9ed6a-154">Created an updated container image</span></span>
> * <span data-ttu-id="9ed6a-155">Wypychana hello kontener obrazu tooAzure rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="9ed6a-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9ed6a-156">Aplikacja hello wdrożonych aktualizacji</span><span class="sxs-lookup"><span data-stu-id="9ed6a-156">Deployed hello updated application</span></span>

<span data-ttu-id="9ed6a-157">Następny samouczek toolearn toohello o tym, jak poprawić toomonitor Kubernetes w usłudze Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9ed6a-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ed6a-158">Monitorowanie rozwiązania Kubernetes za pomocą pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="9ed6a-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)