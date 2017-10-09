---
title: "Samouczek usługi kontenera aaaAzure — skalowania aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — skalowania aplikacji"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Kubernetes, platforma Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="83800-104">Infrastruktura Kubernetes i stanowiskami Kubernetes skali</span><span class="sxs-lookup"><span data-stu-id="83800-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="83800-105">Jeśli została już następujące samouczki hello, masz działające Kubernetes klastra usługi kontenera platformy Azure i hello Azure głosowania aplikacja została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="83800-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="83800-106">W tym samouczku, część 5, 7 skalowanie w poziomie stanowiskami hello w aplikacji hello i spróbuj pod Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="83800-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="83800-107">Możesz też dowiedzieć się, jak tooscale hello liczba toochange węzłów agenta maszyny Wirtualnej Azure hello wydajności obsługi obciążeń klastra.</span><span class="sxs-lookup"><span data-stu-id="83800-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="83800-108">Zadania ukończone obejmują:</span><span class="sxs-lookup"><span data-stu-id="83800-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83800-109">Ręcznie skalowanie stanowiskami Kubernetes</span><span class="sxs-lookup"><span data-stu-id="83800-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="83800-110">Konfigurowanie stanowiskami skalowania automatycznego uruchamiania fronton aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="83800-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="83800-111">Skalowanie hello Kubernetes agenta programu Azure węzłów</span><span class="sxs-lookup"><span data-stu-id="83800-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="83800-112">W kolejnych samouczkach hello aplikacji Azure głos jest aktualizowana, a usługi Operations Management Suite skonfigurowane toomonitor hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="83800-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="83800-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="83800-113">Before you begin</span></span>

<span data-ttu-id="83800-114">W poprzednich samouczków aplikacji zostało umieszczone w obrazie kontenera, ten obraz przekazany tooAzure rejestru kontenera i utworzyć klaster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="83800-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="83800-115">Aplikacja Hello następnie zostało uruchomione na powitania Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="83800-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="83800-116">Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć toohello [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="83800-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="83800-117">Co najmniej tego samouczka wymaga klastra Kubernetes z działającej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83800-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="83800-118">Ręcznie skalować stanowiskami</span><span class="sxs-lookup"><span data-stu-id="83800-118">Manually scale pods</span></span>

<span data-ttu-id="83800-119">W związku z tym do tej pory, zostały wdrożone hello Azure głos frontonu i wystąpienia pamięci podręcznej Redis, każda z pojedynczą replikę.</span><span class="sxs-lookup"><span data-stu-id="83800-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="83800-120">tooverify Uruchom hello [kubectl uzyskać](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.</span><span class="sxs-lookup"><span data-stu-id="83800-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="83800-121">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="83800-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="83800-122">Ręcznie zmień liczbę hello stanowiskami w hello `azure-vote-front` wdrożenia przy użyciu hello [kubectl skali](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) polecenia.</span><span class="sxs-lookup"><span data-stu-id="83800-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="83800-123">W tym przykładzie zwiększa numer too5 hello.</span><span class="sxs-lookup"><span data-stu-id="83800-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="83800-124">Uruchom [kubectl uzyskać stanowiskami](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify czy Kubernetes tworzy stanowiskami hello.</span><span class="sxs-lookup"><span data-stu-id="83800-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="83800-125">Po minucie lub tak system hello stanowiskami dodatkowe:</span><span class="sxs-lookup"><span data-stu-id="83800-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="83800-126">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="83800-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="83800-127">Stanowiskami skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="83800-127">Autoscale pods</span></span>

<span data-ttu-id="83800-128">Obsługuje Kubernetes [Skalowanie automatyczne poziome pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello liczba stanowiskami we wdrożeniu w zależności od użycia procesora CPU lub inne wybrać metryki.</span><span class="sxs-lookup"><span data-stu-id="83800-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="83800-129">toouse hello autoscaler, Twoje stanowiskami musi mieć żądań procesora CPU i zdefiniowano limitów.</span><span class="sxs-lookup"><span data-stu-id="83800-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="83800-130">W hello `azure-vote-front` wdrożenia, hello Procesora żądań 0,25 kontenera frontonu, limit 0,5 procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="83800-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="83800-131">Ustawienia Hello następującą postać:</span><span class="sxs-lookup"><span data-stu-id="83800-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="83800-132">Witaj poniższym przykładzie użyto hello [skalowania automatycznego kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) polecenia tooautoscale hello liczba stanowiskami w hello `azure-vote-front` wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="83800-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="83800-133">W tym miejscu Jeśli wykorzystanie procesora CPU przekracza 50%, hello autoscaler zwiększa hello stanowiskami tooa maksymalnie 10.</span><span class="sxs-lookup"><span data-stu-id="83800-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="83800-134">Stan hello toosee autoscaler hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="83800-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="83800-135">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="83800-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="83800-136">Po upływie kilku minut przy minimalnym obciążeniu hello Azure głos aplikacji hello liczby replik pod zmniejsza automatycznie too3.</span><span class="sxs-lookup"><span data-stu-id="83800-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="83800-137">Agenci hello skali</span><span class="sxs-lookup"><span data-stu-id="83800-137">Scale hello agents</span></span>

<span data-ttu-id="83800-138">Jeśli utworzony klaster Kubernetes przy użyciu polecenia domyślne w samouczku poprzedniej hello ma trzy węzły agenta.</span><span class="sxs-lookup"><span data-stu-id="83800-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="83800-139">Hello liczby agentów można dostosować ręcznie, jeśli planujesz więcej lub mniej obciążeń kontenera w klastrze.</span><span class="sxs-lookup"><span data-stu-id="83800-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="83800-140">Użyj hello [skalować acs az](/cli/azure/acs#scale) polecenia i określić hello liczby agentów z hello `--new-agent-count` parametru.</span><span class="sxs-lookup"><span data-stu-id="83800-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="83800-141">Hello poniższy przykład zwiększa liczbę hello agenta too4 węzłów w klastrze Kubernetes hello o nazwie *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="83800-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="83800-142">polecenie Hello zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="83800-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="83800-143">Hello dane wyjściowe polecenia zawiera hello numer agenta węzłów w wartości hello `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="83800-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="83800-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83800-144">Next steps</span></span>

<span data-ttu-id="83800-145">W tym samouczku użyto różnych funkcji skalowania w klastrze Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="83800-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="83800-146">Uwzględnione objętych zadań:</span><span class="sxs-lookup"><span data-stu-id="83800-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83800-147">Ręcznie skalowanie stanowiskami Kubernetes</span><span class="sxs-lookup"><span data-stu-id="83800-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="83800-148">Konfigurowanie stanowiskami skalowania automatycznego uruchamiania fronton aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="83800-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="83800-149">Skalowanie hello Kubernetes agenta programu Azure węzłów</span><span class="sxs-lookup"><span data-stu-id="83800-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="83800-150">Przejdź dalej toolearn toohello dotyczące aktualizowania aplikacji w Kubernetes samouczka.</span><span class="sxs-lookup"><span data-stu-id="83800-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83800-151">Aktualizuj aplikację w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="83800-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

