---
title: aaaQuickstart - klastra Azure Kubernetes dla systemu Windows | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klastra Kubernetes kontenerów systemu Windows w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="653dd-103">Wdrażanie klastra Kubernetes dla kontenerów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="653dd-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="653dd-104">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="653dd-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="653dd-105">Ta szczegółów przewodnik przy użyciu hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/) klastra w [usługi kontenera platformy Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="653dd-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="653dd-106">Po wdrożeniu klastra hello tooit należy połączyć z hello Kubernetes `kubectl` narzędzia wiersza polecenia, a wdrażanie Twojego pierwszego kontenera systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="653dd-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="653dd-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="653dd-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="653dd-108">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="653dd-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="653dd-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="653dd-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="653dd-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="653dd-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="653dd-111">Obsługa kontenerów systemu Windows w rozwiązaniu Kubernetes w usłudze Azure Container Service jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="653dd-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="653dd-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="653dd-112">Create a resource group</span></span>

<span data-ttu-id="653dd-113">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="653dd-114">Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="653dd-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="653dd-115">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="653dd-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="653dd-116">Tworzenie klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="653dd-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="653dd-117">Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="653dd-118">Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i dwa węzły agenta systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="653dd-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="653dd-119">W tym przykładzie tworzy SSH klucze wymagane tooconnect toohello Linux wzorca.</span><span class="sxs-lookup"><span data-stu-id="653dd-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="653dd-120">W tym przykładzie użyto *azureuser* dla nazwy użytkownika administracyjnego i *myPassword12* jako hasło hello na węzłach Windows hello.</span><span class="sxs-lookup"><span data-stu-id="653dd-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="653dd-121">Zaktualizować te wartości toosomething tooyour odpowiednie środowisko.</span><span class="sxs-lookup"><span data-stu-id="653dd-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="653dd-122">Po kilku minutach polecenia hello kończy i pokazuje informacje dotyczące wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="653dd-123">Instalowanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="653dd-123">Install kubectl</span></span>

<span data-ttu-id="653dd-124">tooconnect toohello Kubernetes klastra z komputera klienta, użyj [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="653dd-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="653dd-125">Jeśli korzystasz z usługi Azure CloudShell, narzędzie `kubectl` jest już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="653dd-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="653dd-126">Jeśli chcesz, aby tooinstall lokalnie, użytkownik może użyć hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="653dd-127">Witaj następującego wiersza polecenia platformy Azure przykład instaluje `kubectl` tooyour systemu.</span><span class="sxs-lookup"><span data-stu-id="653dd-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="653dd-128">W systemie Windows należy uruchomić to polecenie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="653dd-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="653dd-129">Nawiązywanie połączenia przy użyciu narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="653dd-129">Connect with kubectl</span></span>

<span data-ttu-id="653dd-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="653dd-131">Witaj poniższy przykład pobiera hello konfigurację klastra dla klastra Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="653dd-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="653dd-132">tooverify hello połączenia tooyour klaster z komputera, spróbuj uruchomić:</span><span class="sxs-lookup"><span data-stu-id="653dd-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="653dd-133">`kubectl`Wyświetla listę węzłów hello wzorca i agenta.</span><span class="sxs-lookup"><span data-stu-id="653dd-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="653dd-134">Wdrażanie kontenera usług IIS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="653dd-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="653dd-135">Kontener platformy Docker można uruchomić wewnątrz *zasobnika* rozwiązania Kubernetes zawierającego co najmniej jeden kontener.</span><span class="sxs-lookup"><span data-stu-id="653dd-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="653dd-136">Ten prosty przykład używa toospecify pliku JSON kontenera usług Microsoft Internet Information Server (IIS), a następnie tworzy pod hello przy użyciu hello `kubctl apply` polecenia.</span><span class="sxs-lookup"><span data-stu-id="653dd-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="653dd-137">Tworzenie pliku lokalnego o nazwie `iis.json` i hello kopiowania tekstu.</span><span class="sxs-lookup"><span data-stu-id="653dd-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="653dd-138">Ten plik zawiera informacje toorun Kubernetes usług IIS w systemie Windows Server 2016 Nano Server przy użyciu obrazu publicznego kontenera z [Centrum Docker](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="653dd-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="653dd-139">kontener Hello korzysta z portu 80, ale początkowo jest dostępny tylko w ramach hello sieci klastra.</span><span class="sxs-lookup"><span data-stu-id="653dd-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="653dd-140">toostart hello pod, wpisz:</span><span class="sxs-lookup"><span data-stu-id="653dd-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="653dd-141">wdrożenie hello tootrack, wpisz:</span><span class="sxs-lookup"><span data-stu-id="653dd-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="653dd-142">Podczas wdrożenia hello pod jest stan hello `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="653dd-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="653dd-143">Może upłynąć kilka minut, aż hello kontenera tooenter hello `Running` stanu.</span><span class="sxs-lookup"><span data-stu-id="653dd-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="653dd-144">Widok hello strona powitalna usług IIS</span><span class="sxs-lookup"><span data-stu-id="653dd-144">View hello IIS welcome page</span></span>

<span data-ttu-id="653dd-145">tooexpose hello pod toohello world z publicznym adresem IP hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="653dd-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="653dd-146">To polecenie Kubernetes tworzy usługę i [reguły modułu równoważenia obciążenia Azure](container-service-kubernetes-load-balancing.md) z publicznym adresem IP hello usługi.</span><span class="sxs-lookup"><span data-stu-id="653dd-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="653dd-147">Uruchom następujące polecenie toosee hello stanu usługi hello hello.</span><span class="sxs-lookup"><span data-stu-id="653dd-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="653dd-148">Początkowo hello adres IP jest wyświetlany jako `pending`.</span><span class="sxs-lookup"><span data-stu-id="653dd-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="653dd-149">Po kilku minutach hello zewnętrzny adres IP hello `iis` ustawiono pod:</span><span class="sxs-lookup"><span data-stu-id="653dd-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="653dd-150">Można użyć przeglądarki sieci web na wybór toosee hello domyślne IIS strony powitalnej na powitania zewnętrzny adres IP:</span><span class="sxs-lookup"><span data-stu-id="653dd-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Obraz przeglądania tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="653dd-152">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="653dd-152">Delete cluster</span></span>
<span data-ttu-id="653dd-153">Gdy hello klastra nie jest już potrzebne, można użyć hello [az grupę Usuń](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, usługi kontenera i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="653dd-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="653dd-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="653dd-154">Next steps</span></span>

<span data-ttu-id="653dd-155">W tym przewodniku Szybki start wdrożono klaster Kubernetes, nawiązano połączenie z narzędziem `kubectl` i wdrożono zasobnik za pomocą kontenera usług IIS.</span><span class="sxs-lookup"><span data-stu-id="653dd-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="653dd-156">toolearn więcej informacji na temat usługi kontenera platformy Azure, nadal toohello Kubernetes samouczka.</span><span class="sxs-lookup"><span data-stu-id="653dd-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="653dd-157">Zarządzanie klastrem Kubernetes usługi ASC</span><span class="sxs-lookup"><span data-stu-id="653dd-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
