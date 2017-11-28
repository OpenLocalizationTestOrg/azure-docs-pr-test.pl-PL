---
title: "Samouczek usługi kontenera aaaAzure — wdrażanie klastra | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — wdrażanie klastra"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="7d51b-104">Wdrażanie klastra Kubernetes usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7d51b-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="7d51b-105">Kubernetes zapewnia platformę rozproszonej konteneryzowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d51b-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="7d51b-106">Z usługi kontenera platformy Azure inicjowania obsługi klastra produkcyjnego gotowe Kubernetes jest proste i szybkie.</span><span class="sxs-lookup"><span data-stu-id="7d51b-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="7d51b-107">W tym samouczku, część 3 7, wdrożono klaster Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d51b-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="7d51b-108">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="7d51b-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d51b-109">Wdrażanie klastra usług ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7d51b-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="7d51b-110">Instalacja hello Kubernetes interfejsu wiersza polecenia (kubectl)</span><span class="sxs-lookup"><span data-stu-id="7d51b-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="7d51b-111">Konfiguracja kubectl</span><span class="sxs-lookup"><span data-stu-id="7d51b-111">Configuration of kubectl</span></span>

<span data-ttu-id="7d51b-112">W kolejnych samouczkach hello Azure głos aplikacja jest wdrożona toohello klastra, skalowania, zaktualizować, a Operations Management Suite jest skonfigurowany toomonitor hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="7d51b-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7d51b-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7d51b-113">Before you begin</span></span>

<span data-ttu-id="7d51b-114">W poprzednich samouczki obrazu kontenera został utworzony i przekazać tooan rejestru kontenera Azure wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="7d51b-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="7d51b-115">Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7d51b-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="7d51b-116">Tworzenie klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7d51b-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="7d51b-117">W hello [poprzedniego samouczek](./container-service-tutorial-kubernetes-prepare-acr.md), grupy zasobów o nazwie *myResourceGroup* został utworzony.</span><span class="sxs-lookup"><span data-stu-id="7d51b-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="7d51b-118">Jeśli użytkownik nie zostało zrobione, Utwórz teraz tej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7d51b-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="7d51b-119">Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d51b-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="7d51b-120">Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7d51b-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="7d51b-121">Po kilku minutach hello polecenie zostanie wykonane, a w formacie json zwraca informacji o wdrażaniu hello ACS.</span><span class="sxs-lookup"><span data-stu-id="7d51b-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="7d51b-122">Zainstaluj kubectl hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7d51b-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="7d51b-123">tooconnect toohello Kubernetes klastra z komputera klienta, użyj [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="7d51b-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="7d51b-124">Jeśli korzystasz z usługi Azure CloudShell, narzędzie `kubectl` jest już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="7d51b-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="7d51b-125">Jeśli chcesz, aby tooinstall lokalnie, użyj hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d51b-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="7d51b-126">Jeśli uruchomiona w systemie Linux lub macOS, może być konieczne toorun z sudo.</span><span class="sxs-lookup"><span data-stu-id="7d51b-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="7d51b-127">W systemie Windows upewnij się, że powłoki zostało uruchomione jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7d51b-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="7d51b-128">W systemie Windows, instalacja domyślna hello jest *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="7d51b-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="7d51b-129">Tooadd może być konieczne tej ścieżki pliku toohello systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="7d51b-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="7d51b-130">Nawiązywanie połączenia przy użyciu narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="7d51b-130">Connect with kubectl</span></span>

<span data-ttu-id="7d51b-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d51b-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="7d51b-132">tooverify hello połączenia tooyour klastra, uruchom hello [kubectl uzyskać węzłów](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d51b-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="7d51b-133">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d51b-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="7d51b-134">Po ukończeniu samouczka masz klastry ACS Kubernetes dla obciążeń.</span><span class="sxs-lookup"><span data-stu-id="7d51b-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="7d51b-135">W kolejnych samouczkach aplikacji kontenera wielu jest wdrożone toothis klaster, skalowana w poziomie, aktualizacji i monitorowane.</span><span class="sxs-lookup"><span data-stu-id="7d51b-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d51b-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d51b-136">Next steps</span></span>

<span data-ttu-id="7d51b-137">W tym samouczku klastra Kubernetes usługi kontenera platformy Azure została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="7d51b-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="7d51b-138">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7d51b-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d51b-139">Wdrożone klastra Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="7d51b-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="7d51b-140">Zainstalowane hello Kubernetes interfejsu wiersza polecenia (kubectl)</span><span class="sxs-lookup"><span data-stu-id="7d51b-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="7d51b-141">Skonfigurowany kubectl</span><span class="sxs-lookup"><span data-stu-id="7d51b-141">Configured kubectl</span></span>

<span data-ttu-id="7d51b-142">Przejdź dalej toolearn toohello dotyczące uruchamiania aplikacji w klastrze hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="7d51b-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d51b-143">Wdrażanie aplikacji w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7d51b-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
