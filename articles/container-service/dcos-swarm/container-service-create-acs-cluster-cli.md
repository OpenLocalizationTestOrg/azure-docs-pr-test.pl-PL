---
title: aaaDeploy klaster kontenera Docker - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie rozwiązania Kubernetes, DC/OS lub Docker Swarm w usłudze Azure Container Service przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="c1d78-103">Wdrażanie rozwiązania przy użyciu hello Azure CLI 2.0 hostingu kontener Docker</span><span class="sxs-lookup"><span data-stu-id="c1d78-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="c1d78-104">Użyj hello `az acs` polecenia w toocreate hello Azure CLI 2.0 i zarządzania klastrami usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d78-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="c1d78-105">Można także wdrożyć klaster usługi kontenera platformy Azure przy użyciu hello [portalu Azure](container-service-deployment.md) lub hello interfejsów API usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d78-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="c1d78-106">Aby uzyskać pomoc dotyczącą `az acs` poleceń, Przekaż hello `-h` polecenia tooany parametru.</span><span class="sxs-lookup"><span data-stu-id="c1d78-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="c1d78-107">Na przykład: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="c1d78-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c1d78-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c1d78-108">Prerequisites</span></span>
<span data-ttu-id="c1d78-109">toocreate klastra usługi kontenera platformy Azure przy użyciu hello Azure CLI 2.0, należy:</span><span class="sxs-lookup"><span data-stu-id="c1d78-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="c1d78-110">Konto platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="c1d78-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="c1d78-111">zainstalować i skonfigurować hello [2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="c1d78-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="c1d78-112">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="c1d78-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="c1d78-113">Zaloguj się na koncie tooyour</span><span class="sxs-lookup"><span data-stu-id="c1d78-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="c1d78-114">Wykonaj hello toolog monity w interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="c1d78-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="c1d78-115">Dla innych metod toolog w, zobacz [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c1d78-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="c1d78-116">Ustawianie swojej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c1d78-116">Set your Azure subscription</span></span>

<span data-ttu-id="c1d78-117">Jeśli masz więcej niż jedną subskrypcją platformy Azure, należy ustawić hello domyślne subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1d78-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="c1d78-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c1d78-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="c1d78-119">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c1d78-119">Create a resource group</span></span>
<span data-ttu-id="c1d78-120">Zaleca się utworzenie grupy zasobów dla każdego klastra.</span><span class="sxs-lookup"><span data-stu-id="c1d78-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="c1d78-121">Określ region świadczenia usługi Azure, w którym jest [dostępna](https://azure.microsoft.com/en-us/regions/services/) usługa Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="c1d78-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="c1d78-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c1d78-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="c1d78-123">Dane wyjściowe są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c1d78-123">Output is similar toohello following:</span></span>

![Tworzenie grupy zasobów](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="c1d78-125">Tworzenie klastra usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c1d78-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="c1d78-126">toocreate klaster, użyj `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="c1d78-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="c1d78-127">Nazwa klastra hello i hello nazwę grupy zasobów hello utworzony w poprzednim kroku hello są obowiązkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c1d78-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="c1d78-128">Inne dane wejściowe są ustawione wartości toodefault (zobacz po ekranie powitania), chyba że zastąpione za pomocą ich odpowiednich przełączników.</span><span class="sxs-lookup"><span data-stu-id="c1d78-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="c1d78-129">Na przykład hello orchestrator jest ustawiana przez domyślny tooDC/OS.</span><span class="sxs-lookup"><span data-stu-id="c1d78-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="c1d78-130">A jeśli nie określono, prefiks nazwy DNS jest tworzone na podstawie nazwy klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c1d78-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![Sposób użycia polecenia az acs create](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="c1d78-132">Szybkie wykonanie polecenia `acs create` z użyciem ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="c1d78-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="c1d78-133">Jeśli masz pliku klucza publicznego SSH RSA `id_rsa.pub` w lokalizacji domyślnej hello (lub utworzony dla [OS X i Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../../virtual-machines/linux/ssh-from-windows.md)), użyj polecenia takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c1d78-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="c1d78-134">Jeśli nie masz klucza publicznego SSH, użyj drugiego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c1d78-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="c1d78-135">To polecenie z hello `--generate-ssh-keys` przełącznika je tworzy.</span><span class="sxs-lookup"><span data-stu-id="c1d78-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="c1d78-136">Po wprowadzeniu polecenia hello Poczekaj około 10 minut na powitania toobe klastra utworzone.</span><span class="sxs-lookup"><span data-stu-id="c1d78-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="c1d78-137">dane wyjściowe polecenia Hello obejmuje pełni kwalifikowanych nazw domen (FQDN) głównego hello i węzłów agenta i SSH polecenie tooconnect toohello pierwszego serwera głównego.</span><span class="sxs-lookup"><span data-stu-id="c1d78-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="c1d78-138">Poniżej przedstawiono skrócone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1d78-138">Here is abbreviated output:</span></span>

![Obraz przedstawiający polecenie acs create](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="c1d78-140">Witaj [wskazówki Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md) przedstawia sposób toouse `az acs create` z domyślnej wartości toocreate Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="c1d78-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="c1d78-141">Zarządzanie klastrami usługi ACS</span><span class="sxs-lookup"><span data-stu-id="c1d78-141">Manage ACS clusters</span></span>

<span data-ttu-id="c1d78-142">Użyj dodatkowych `az acs` polecenia toomanage klastra.</span><span class="sxs-lookup"><span data-stu-id="c1d78-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="c1d78-143">Oto kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="c1d78-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="c1d78-144">Wyświetlanie listy klastrów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c1d78-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="c1d78-145">Wyświetlanie listy klastrów w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="c1d78-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![Polecenie acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="c1d78-147">Wyświetlanie szczegółów klastra usługi kontenera</span><span class="sxs-lookup"><span data-stu-id="c1d78-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![Polecenie acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="c1d78-149">Klaster w skali hello</span><span class="sxs-lookup"><span data-stu-id="c1d78-149">Scale hello cluster</span></span>
<span data-ttu-id="c1d78-150">Dozwolone jest skalowanie węzłów agentów zarówno na zewnątrz, jak i do wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="c1d78-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="c1d78-151">Witaj parametru `new-agent-count` jest nowy numer hello agentów w klastrze hello ACS.</span><span class="sxs-lookup"><span data-stu-id="c1d78-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![Polecenie acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="c1d78-153">Usuwanie klastra usługi kontenera</span><span class="sxs-lookup"><span data-stu-id="c1d78-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="c1d78-154">To polecenie nie powoduje usunięcia wszystkich zasobów (sieci i magazynu) podczas tworzenia usługi kontenera hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="c1d78-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="c1d78-155">toodelete wszystkie zasoby, zaleca się wdrażania poszczególnych klastrów w grupie zasobów distinct.</span><span class="sxs-lookup"><span data-stu-id="c1d78-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="c1d78-156">Następnie usuń hello grupy zasobów, gdy hello klastra nie jest już wymagane.</span><span class="sxs-lookup"><span data-stu-id="c1d78-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1d78-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1d78-157">Next steps</span></span>
<span data-ttu-id="c1d78-158">Teraz, gdy masz działający klaster, możesz zapoznać się z tymi dokumentami, aby uzyskać szczegółowe informacje na temat połączeń i zarządzania:</span><span class="sxs-lookup"><span data-stu-id="c1d78-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="c1d78-159">Połącz tooan klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c1d78-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="c1d78-160">Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS</span><span class="sxs-lookup"><span data-stu-id="c1d78-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="c1d78-161">Współpraca z usługą Azure Container Service i rozwiązaniem Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c1d78-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="c1d78-162">Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c1d78-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)