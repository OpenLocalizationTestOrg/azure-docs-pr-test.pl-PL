---
title: "Samouczek usługi kontenera aaaAzure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — wdrażanie aplikacji"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="7c89d-104">Uruchamianie aplikacji w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7c89d-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="7c89d-105">W tym samouczku część cztery siedmiu, przykładowa aplikacja jest wdrażana w klastrze Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7c89d-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="7c89d-106">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="7c89d-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c89d-107">Pobierz pliki manifestu Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7c89d-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="7c89d-108">Uruchom aplikację w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7c89d-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="7c89d-109">Testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7c89d-109">Test hello application</span></span>

<span data-ttu-id="7c89d-110">W kolejnych samouczkach tej aplikacji jest skalowanie, aktualizacji i Operations Management Suite skonfigurowany toomonitor hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="7c89d-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="7c89d-111">Ten samouczek zakłada podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje na temat Kubernetes Zobacz hello [dokumentacji Kubernetes](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="7c89d-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c89d-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7c89d-112">Before you begin</span></span>

<span data-ttu-id="7c89d-113">W poprzednich samouczki aplikacji zostało umieszczone w obrazie kontenera, ten obraz został przekazany tooAzure rejestru kontenera i klaster Kubernetes został utworzony.</span><span class="sxs-lookup"><span data-stu-id="7c89d-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="7c89d-114">Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7c89d-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="7c89d-115">Co najmniej tego samouczka wymaga Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="7c89d-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="7c89d-116">Pobierz plik manifestu</span><span class="sxs-lookup"><span data-stu-id="7c89d-116">Get manifest file</span></span>

<span data-ttu-id="7c89d-117">W tym samouczku [obiektów Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) są wdrażane za pomocą Kubernetes manifestu.</span><span class="sxs-lookup"><span data-stu-id="7c89d-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="7c89d-118">Kubernetes manifest jest yaml programu lub JSON sformatowanym plikiem instrukcjami Kubernetes obiektu wdrażania i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c89d-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="7c89d-119">Plik manifestu aplikacji Hello w tym samouczku jest dostępna w hello Azure głos aplikacji repozytorium, który został sklonowany w poprzednim samouczka.</span><span class="sxs-lookup"><span data-stu-id="7c89d-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="7c89d-120">Jeśli nie zostało to jeszcze zrobione, klonowanie repozytorium hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7c89d-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="7c89d-121">Plik manifestu Hello znajduje się w hello następującego katalogu hello sklonować repozytorium.</span><span class="sxs-lookup"><span data-stu-id="7c89d-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="7c89d-122">Aktualizacja pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="7c89d-122">Update manifest file</span></span>

<span data-ttu-id="7c89d-123">Jeśli za pomocą rejestru kontenera Azure toostore hello kontener obrazów, toobe manifestu potrzeb hello zaktualizowane hello nazwa ACR loginServer.</span><span class="sxs-lookup"><span data-stu-id="7c89d-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="7c89d-124">Pobierz nazwę serwera hello ACR logowania z hello [listy acr az](/cli/azure/acr#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c89d-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="7c89d-125">Witaj próbki manifest został wstępnie utworzone przy użyciu nazwy repozytorium *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="7c89d-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="7c89d-126">Otwórz plik hello w dowolnym edytorze tekstu i Zastąp hello *microsoft* wartości z nazwą serwera logowania hello wystąpienia ACR.</span><span class="sxs-lookup"><span data-stu-id="7c89d-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="7c89d-127">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7c89d-127">Deploy application</span></span>

<span data-ttu-id="7c89d-128">Użyj hello [kubectl utworzyć](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) polecenia aplikacji hello toorun.</span><span class="sxs-lookup"><span data-stu-id="7c89d-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="7c89d-129">Tego polecenia po analizie hello pliku manifestu i tworzenie obiektów Kubernetes hello zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="7c89d-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="7c89d-130">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7c89d-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="7c89d-131">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7c89d-131">Test application</span></span>

<span data-ttu-id="7c89d-132">A [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, który udostępnia toohello aplikacji hello internet.</span><span class="sxs-lookup"><span data-stu-id="7c89d-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="7c89d-133">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7c89d-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="7c89d-134">postęp toomonitor, użyj hello [kubectl pobrać usługi](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) z hello `--watch` argumentu.</span><span class="sxs-lookup"><span data-stu-id="7c89d-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="7c89d-135">Początkowo hello **IP zewnętrznego** dla hello *azure głos początku* usługi pojawia się jako *oczekujące*.</span><span class="sxs-lookup"><span data-stu-id="7c89d-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="7c89d-136">Gdy adres IP zewnętrznego hello zmienił się z *oczekujące* tooan *adres IP*, użyj `CTRL-C` toostop hello kubectl czujki procesu.</span><span class="sxs-lookup"><span data-stu-id="7c89d-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="7c89d-137">Aplikacja hello toosee, przeglądania toohello zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="7c89d-137">toosee hello application, browse toohello external IP address.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="7c89d-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c89d-139">Next steps</span></span>

<span data-ttu-id="7c89d-140">W tym samouczku hello Azure głos aplikacji został wdrożony tooan klastra Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c89d-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="7c89d-141">Zadania ukończone obejmują:</span><span class="sxs-lookup"><span data-stu-id="7c89d-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="7c89d-142">Pobierz pliki manifestu Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7c89d-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="7c89d-143">Uruchamianie aplikacji hello w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7c89d-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="7c89d-144">Aplikacja hello przetestowany</span><span class="sxs-lookup"><span data-stu-id="7c89d-144">Tested hello application</span></span>

<span data-ttu-id="7c89d-145">Przejdź dalej toolearn toohello temat skalowania aplikacji Kubernetes jak hello podstawowej infrastruktury Kubernetes samouczka.</span><span class="sxs-lookup"><span data-stu-id="7c89d-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c89d-146">Skala Kubernetes aplikacji i infrastruktury</span><span class="sxs-lookup"><span data-stu-id="7c89d-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)