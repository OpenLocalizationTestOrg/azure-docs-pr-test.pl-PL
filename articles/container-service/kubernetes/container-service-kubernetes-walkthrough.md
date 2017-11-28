---
title: aaaQuickstart - klastra Azure Kubernetes dla systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klastra Kubernetes dla systemu Linux kontenerów w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="fef29-103">Wdrażanie klastra Kubernetes dla kontenerów systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fef29-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="fef29-104">W tym szybki start klastra Kubernetes jest wdrażane za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fef29-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="fef29-105">Następnie wdrożone i uruchomić w klastrze hello aplikacji kontenera wielu składające się z frontonu sieci web oraz wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="fef29-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="fef29-106">Po ukończeniu aplikacji hello jest dostępny za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="fef29-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="fef29-107">Witaj przykładowej aplikacji używane w tym dokumencie są zapisywane w języku Python.</span><span class="sxs-lookup"><span data-stu-id="fef29-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="fef29-108">Hello pojęcia i szczegółowe tutaj kroki mogą być używane toodeploy każdy kontener obrazu w klastrze Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="fef29-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="fef29-109">Witaj kodu, plik Dockerfile i wstępnie utworzony projekt toothis powiązane pliki manifestu Kubernetes są dostępne na [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="fef29-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Obraz przeglądania tooAzure głosu](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="fef29-111">To szybki start założono podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje na temat Kubernetes Zobacz hello [dokumentacji Kubernetes]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="fef29-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="fef29-112">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fef29-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fef29-113">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="fef29-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fef29-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="fef29-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fef29-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fef29-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="fef29-116">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="fef29-116">Create a resource group</span></span>

<span data-ttu-id="fef29-117">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="fef29-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fef29-118">Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="fef29-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fef29-119">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fef29-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="fef29-120">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="fef29-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="fef29-121">Tworzenie klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="fef29-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="fef29-122">Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="fef29-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="fef29-123">Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fef29-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="fef29-124">Po kilku minutach polecenia hello kończy i zwraca informacje o formacie json o hello klastra.</span><span class="sxs-lookup"><span data-stu-id="fef29-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="fef29-125">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="fef29-125">Connect toohello cluster</span></span>

<span data-ttu-id="fef29-126">Użyj toomanage klastrze Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="fef29-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="fef29-127">Jeśli korzystasz z usługi Azure CloudShell, narzędzie kubectl jest już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="fef29-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="fef29-128">Jeśli chcesz, aby tooinstall lokalnie, użytkownik może użyć hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.</span><span class="sxs-lookup"><span data-stu-id="fef29-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="fef29-129">tooconfigure kubectl tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia.</span><span class="sxs-lookup"><span data-stu-id="fef29-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="fef29-130">Ten krok pobiera poświadczenia i konfiguruje hello toouse Kubernetes CLI je.</span><span class="sxs-lookup"><span data-stu-id="fef29-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="fef29-131">tooverify hello połączenia tooyour klastra, użyj hello [kubectl uzyskać](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooreturn polecenia listy hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="fef29-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="fef29-132">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="fef29-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="fef29-133">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="fef29-133">Run hello application</span></span>

<span data-ttu-id="fef29-134">Plik manifestu Kubernetes definiuje żądanego stanu dla klastra hello, w tym, co powinna być uruchomiona kontener obrazów.</span><span class="sxs-lookup"><span data-stu-id="fef29-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="fef29-135">Na przykład manifestu jest toocreate używane wszystkie obiekty, potrzebne toorun hello Azure głos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fef29-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="fef29-136">Utwórz plik o nazwie `azure-vote.yml` i skopiuj do niego hello następujących yaml programu.</span><span class="sxs-lookup"><span data-stu-id="fef29-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="fef29-137">Jeśli pracujesz w usłudze Azure Cloud Shell, ten plik można utworzyć przy użyciu serwera vi lub Nano tak jak podczas pracy w systemie wirtualnym lub fizycznym.</span><span class="sxs-lookup"><span data-stu-id="fef29-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="fef29-138">Użyj hello [kubectl utworzyć](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) polecenia aplikacji hello toorun.</span><span class="sxs-lookup"><span data-stu-id="fef29-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="fef29-139">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="fef29-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="fef29-140">Testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="fef29-140">Test hello application</span></span>

<span data-ttu-id="fef29-141">Jak aplikacja hello jest uruchamiana, [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, że ujawnia hello toohello fronton aplikacji internetowych.</span><span class="sxs-lookup"><span data-stu-id="fef29-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="fef29-142">Ten proces może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fef29-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="fef29-143">postęp toomonitor, użyj hello [kubectl pobrać usługi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) z hello `--watch` argumentu.</span><span class="sxs-lookup"><span data-stu-id="fef29-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="fef29-144">Początkowo hello **IP zewnętrznego** dla hello *azure głos początku* usługi pojawia się jako *oczekujące*.</span><span class="sxs-lookup"><span data-stu-id="fef29-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="fef29-145">Gdy adres IP zewnętrznego hello zmienił się z *oczekujące* tooan *adres IP*, użyj `CTRL-C` toostop hello kubectl czujki procesu.</span><span class="sxs-lookup"><span data-stu-id="fef29-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="fef29-146">Użytkownik może przeglądać toohello zewnętrznego adresu IP adres toosee hello Azure głos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fef29-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Obraz przeglądania tooAzure głosu](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="fef29-148">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="fef29-148">Delete cluster</span></span>
<span data-ttu-id="fef29-149">Gdy hello klastra nie jest już potrzebne, można użyć hello [az grupę Usuń](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, usługi kontenera i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="fef29-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="fef29-150">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="fef29-150">Get hello code</span></span>

<span data-ttu-id="fef29-151">W tym szybki start kontenera wstępnie utworzony obrazy zostały toocreate używane wdrożenia Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="fef29-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="fef29-152">Witaj związane z kodu aplikacji, plik Dockerfile, i plik manifestu Kubernetes są dostępne w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="fef29-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="fef29-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="fef29-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="fef29-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fef29-154">Next steps</span></span>

<span data-ttu-id="fef29-155">W tym szybki start wdrożeniu klastra Kubernetes i wdrożone tooit wielu kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fef29-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="fef29-156">toolearn więcej informacji na temat usługi kontenera platformy Azure i krokach związanych z pełny toodeployment przykład kodu, nadal toohello Kubernetes klastra samouczka.</span><span class="sxs-lookup"><span data-stu-id="fef29-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fef29-157">Zarządzanie klastrem Kubernetes usługi ASC</span><span class="sxs-lookup"><span data-stu-id="fef29-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
