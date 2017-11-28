---
title: "Szybki start — klaster Azure Kubernetes dla systemu Windows | Microsoft Docs"
description: "Szybka nauka tworzenia klastra Kubernetes dla kontenerów systemu Windows w usłudze Azure Container Service za pomocą interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: f9bf4c4094addfa9654e3b99d91add03079ee045
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="aac0a-103">Wdrażanie klastra Kubernetes dla kontenerów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="aac0a-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="aac0a-104">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="aac0a-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="aac0a-105">W tym przewodniku zawarto szczegółowe informacje dotyczące korzystania z interfejsu wiersza polecenia platformy Azure w celu wdrożenia klastra [Kubernetes](https://kubernetes.io/docs/home/) w [usłudze Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="aac0a-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="aac0a-106">Po wdrożeniu klastra nawiążesz z nim połączenie za pomocą narzędzia wiersza polecenia `kubectl` usługi Kubernetes i wdrożysz swój pierwszy kontener systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="aac0a-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="aac0a-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="aac0a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aac0a-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik szybkiego startu będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="aac0a-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="aac0a-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="aac0a-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="aac0a-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aac0a-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="aac0a-111">Obsługa kontenerów systemu Windows w rozwiązaniu Kubernetes w usłudze Azure Container Service jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="aac0a-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="aac0a-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="aac0a-112">Create a resource group</span></span>

<span data-ttu-id="aac0a-113">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="aac0a-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="aac0a-114">Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="aac0a-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="aac0a-115">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *eastus*.</span><span class="sxs-lookup"><span data-stu-id="aac0a-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="aac0a-116">Tworzenie klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="aac0a-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="aac0a-117">Utwórz klaster Kubernetes w usłudze Azure Container Service za pomocą polecenia [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="aac0a-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="aac0a-118">W poniższym przykładzie tworzony jest klaster o nazwie *myK8sCluster* z jednym węzłem głównym systemu Linux i dwoma węzłami agenta systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="aac0a-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="aac0a-119">Ten przykład tworzy klucze SSH potrzebne do nawiązania połączenia z węzłem głównym systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="aac0a-119">This example creates SSH keys needed to connect to the Linux master.</span></span> <span data-ttu-id="aac0a-120">W tym przykładzie *azureuser* to nazwa użytkownika administracyjnego, a *myPassword12* to hasło w węzłach systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="aac0a-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span></span> <span data-ttu-id="aac0a-121">Zmień te wartości, aby pasowały do Twojego środowiska.</span><span class="sxs-lookup"><span data-stu-id="aac0a-121">Update these values to something appropriate to your environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="aac0a-122">Po kilku minutach polecenie zostanie zakończone i wyświetlone zostaną informacje o wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="aac0a-122">After several minutes, the command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="aac0a-123">Instalowanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="aac0a-123">Install kubectl</span></span>

<span data-ttu-id="aac0a-124">Aby nawiązać połączenie z klastrem Kubernetes z komputera klienckiego, należy użyć klienta wiersza polecenia usługi Kubernetes [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/).</span><span class="sxs-lookup"><span data-stu-id="aac0a-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="aac0a-125">Jeśli korzystasz z usługi Azure CloudShell, narzędzie `kubectl` jest już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="aac0a-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="aac0a-126">Jeśli chcesz zainstalować je lokalnie, możesz użyć polecenia [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="aac0a-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="aac0a-127">Poniższy przykład interfejsu wiersza polecenia platformy Azure instaluje narzędzie `kubectl` w systemie.</span><span class="sxs-lookup"><span data-stu-id="aac0a-127">The following Azure CLI example installs `kubectl` to your system.</span></span> <span data-ttu-id="aac0a-128">W systemie Windows należy uruchomić to polecenie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="aac0a-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="aac0a-129">Nawiązywanie połączenia przy użyciu narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="aac0a-129">Connect with kubectl</span></span>

<span data-ttu-id="aac0a-130">Aby skonfigurować narzędzie `kubectl` w celu nawiązania połączenia z klastrem Kubernetes, uruchom polecenie [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="aac0a-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="aac0a-131">Poniższy przykład pobiera konfigurację klastra dla klastra Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="aac0a-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="aac0a-132">Aby sprawdzić połączenie z klastrem ze swojej maszyny, spróbuj uruchomić następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="aac0a-132">To verify the connection to your cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="aac0a-133">`kubectl` wyświetli węzeł główny i węzły agenta.</span><span class="sxs-lookup"><span data-stu-id="aac0a-133">`kubectl` lists the master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="aac0a-134">Wdrażanie kontenera usług IIS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="aac0a-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="aac0a-135">Kontener platformy Docker można uruchomić wewnątrz *zasobnika* rozwiązania Kubernetes zawierającego co najmniej jeden kontener.</span><span class="sxs-lookup"><span data-stu-id="aac0a-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="aac0a-136">W tym podstawowym przykładzie użyto pliku JSON do określenia kontenera usług Microsoft Internet Information Server (IIS), a następnie utworzono zasobnik przy użyciu polecenia `kubctl apply`.</span><span class="sxs-lookup"><span data-stu-id="aac0a-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span></span> 

<span data-ttu-id="aac0a-137">Utwórz plik lokalny o nazwie `iis.json` i skopiuj poniższy tekst.</span><span class="sxs-lookup"><span data-stu-id="aac0a-137">Create a local file named `iis.json` and copy the following text.</span></span> <span data-ttu-id="aac0a-138">Ten plik nakazuje rozwiązaniu Kubernetes uruchomienie usług IIS w systemie Windows Server 2016 Nano Server przy użyciu obrazu publicznego kontenera z witryny [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="aac0a-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="aac0a-139">Kontener korzysta z portu 80, ale początkowo jest dostępny tylko w ramach sieci klastra.</span><span class="sxs-lookup"><span data-stu-id="aac0a-139">The container uses port 80, but initially is only accessible within the cluster network.</span></span>

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

<span data-ttu-id="aac0a-140">Aby uruchomić zasobnik, wpisz:</span><span class="sxs-lookup"><span data-stu-id="aac0a-140">To start the pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="aac0a-141">Aby śledzić wdrożenie, wpisz:</span><span class="sxs-lookup"><span data-stu-id="aac0a-141">To track the deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="aac0a-142">Podczas wdrażania zasobnika ustawiany jest stan `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="aac0a-142">While the pod is deploying, the status is `ContainerCreating`.</span></span> <span data-ttu-id="aac0a-143">Może upłynąć kilka minut, zanim stan kontenera zmieni się na `Running`.</span><span class="sxs-lookup"><span data-stu-id="aac0a-143">It can take a few minutes for the container to enter the `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="aac0a-144">Wyświetlanie strony powitalnej usług IIS</span><span class="sxs-lookup"><span data-stu-id="aac0a-144">View the IIS welcome page</span></span>

<span data-ttu-id="aac0a-145">Aby udostępnić zasobnik światu z publicznym adresem IP, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="aac0a-145">To expose the pod to the world with a public IP address, type the following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="aac0a-146">To polecenie spowoduje utworzenie przez rozwiązanie Kubernetes usługi i [reguły usługi Azure Load Balancer](container-service-kubernetes-load-balancing.md) z publicznym adresem IP usługi.</span><span class="sxs-lookup"><span data-stu-id="aac0a-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for the service.</span></span> 

<span data-ttu-id="aac0a-147">Uruchom poniższe polecenie, aby wyświetlić stan usługi.</span><span class="sxs-lookup"><span data-stu-id="aac0a-147">Run the following command to see the status of the service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="aac0a-148">Początkowo adres IP będzie widoczny jako `pending`.</span><span class="sxs-lookup"><span data-stu-id="aac0a-148">Initially the IP address appears as `pending`.</span></span> <span data-ttu-id="aac0a-149">Po kilku minutach zostanie ustawiony zewnętrzny adres IP zasobnika `iis`:</span><span class="sxs-lookup"><span data-stu-id="aac0a-149">After a few minutes, the external IP address of the `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="aac0a-150">Możesz użyć wybranej przeglądarki internetowej, aby wyświetlić domyślną stronę powitalną usług IIS pod zewnętrznym adresem IP:</span><span class="sxs-lookup"><span data-stu-id="aac0a-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span></span>

![Obraz przedstawiający przechodzenie do usług IIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="aac0a-152">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="aac0a-152">Delete cluster</span></span>
<span data-ttu-id="aac0a-153">Gdy klaster nie będzie już potrzebny, możesz usunąć grupę zasobów, usługę kontenera i wszystkie pokrewne zasoby za pomocą polecenia [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="aac0a-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="aac0a-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aac0a-154">Next steps</span></span>

<span data-ttu-id="aac0a-155">W tym przewodniku Szybki start wdrożono klaster Kubernetes, nawiązano połączenie z narzędziem `kubectl` i wdrożono zasobnik za pomocą kontenera usług IIS.</span><span class="sxs-lookup"><span data-stu-id="aac0a-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="aac0a-156">Aby dowiedzieć się więcej na temat usługi Azure Container Service, przejdź do samouczka dotyczącego rozwiązania Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="aac0a-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aac0a-157">Zarządzanie klastrem Kubernetes usługi ASC</span><span class="sxs-lookup"><span data-stu-id="aac0a-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
