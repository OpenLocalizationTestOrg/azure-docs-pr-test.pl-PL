---
title: "Samouczek usługi kontenera aaaAzure — Zarządzanie DC/OS | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — Zarządzanie DC/OS"
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
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="6a512-104">Samouczek usługi kontenera platformy Azure — Zarządzanie DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="6a512-105">DC/OS przewiduje uruchamianie nowoczesnych i konteneryzowanych aplikacji rozproszonej platformy.</span><span class="sxs-lookup"><span data-stu-id="6a512-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="6a512-106">Z usługi kontenera platformy Azure inicjowania obsługi klastra DC/OS gotowy produkcji jest proste i szybkie.</span><span class="sxs-lookup"><span data-stu-id="6a512-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="6a512-107">To szybki start szczegóły podstawowe kroki potrzebne toodeploy klastra DC/OS i wykonywania podstawowych obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a512-108">Tworzenie klastra usługi ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="6a512-109">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="6a512-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="6a512-110">Zainstaluj interfejs wiersza polecenia DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="6a512-111">Wdrażanie klastra toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a512-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="6a512-112">Skalowanie aplikacji w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="6a512-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="6a512-113">Skalowanie węzłów klastra DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="6a512-114">Podstawowe możliwości zarządzania DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="6a512-115">Usuń klaster DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="6a512-116">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6a512-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6a512-117">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6a512-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6a512-118">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6a512-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="6a512-119">Tworzenie klastra DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-119">Create DC/OS cluster</span></span>

<span data-ttu-id="6a512-120">Najpierw utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6a512-121">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="6a512-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="6a512-122">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6a512-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="6a512-123">Następnie Utwórz klaster DC/OS z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="6a512-124">Witaj poniższy przykład tworzy klaster DC/OS o nazwie *myDCOSCluster* i tworzy kluczy SSH, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="6a512-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="6a512-125">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="6a512-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="6a512-126">Po kilku minutach polecenia hello kończy i zwraca informacje na temat wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="6a512-127">Połącz klaster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="6a512-128">Po utworzeniu klastra DC/OS, może być dostęp za pośrednictwem tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="6a512-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="6a512-129">Uruchom następujące polecenia tooreturn hello publicznego adresu IP wzorca DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="6a512-130">Ten adres IP jest przechowywana w zmiennej i używane w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6a512-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="6a512-131">toocreate hello tunelu SSH, uruchom następujące polecenie hello i hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="6a512-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="6a512-132">Jeśli port 80 jest już w użyciu, hello polecenie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6a512-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="6a512-133">Aktualizacja hello tunelowane tooone portu nieużywany, takich jak `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="6a512-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="6a512-134">Instalowanie interfejsu wiersza polecenia DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-134">Install DC/OS CLI</span></span>

<span data-ttu-id="6a512-135">Zainstaluj interfejs wiersza polecenia hello DC/OS jest przy użyciu hello [az dcos acs install-cli](/azure/acs/dcos#install-cli) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="6a512-136">Jeśli używasz usługi Azure CloudShell hello interfejsu wiersza polecenia DC/OS jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="6a512-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="6a512-137">Jeśli używasz hello Azure CLI macOS lub Linux, może być konieczne toorun hello polecenie sudo.</span><span class="sxs-lookup"><span data-stu-id="6a512-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="6a512-138">Przed hello interfejsu wiersza polecenia można używać z klastrem hello musi ona być tunelu SSH hello toouse skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="6a512-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="6a512-139">toodo tak, uruchom hello następujące polecenia, dostosowywania hello portu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6a512-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="6a512-140">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a512-140">Run an application</span></span>

<span data-ttu-id="6a512-141">Domyślnie Hello planowania mechanizm dla klastra usługi ACS DC/OS jest Marathon.</span><span class="sxs-lookup"><span data-stu-id="6a512-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="6a512-142">Marathon jest toostart używanych aplikacji i zarządzanie stanem hello aplikacji hello w klastrze DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="6a512-143">tooschedule aplikacji za pośrednictwem platformy Marathon, Utwórz plik o nazwie **marathon app.json**, i hello kopiowania zawartości do niego.</span><span class="sxs-lookup"><span data-stu-id="6a512-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="6a512-144">Uruchom następujące polecenie tooschedule hello aplikacji toorun w klastrze DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="6a512-145">toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="6a512-146">Gdy hello **zadania** zmienia wartość kolumny z *0/1* za*1/1*, wdrażanie aplikacji zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="6a512-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="6a512-147">Skalowanie aplikacji platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="6a512-147">Scale Marathon application</span></span>

<span data-ttu-id="6a512-148">W poprzednim przykładzie hello została utworzona aplikacja pojedynczego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6a512-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="6a512-149">To wdrożenie, aby trzy wystąpienia aplikacji hello są dostępne, otwarcie hello tooupdate **marathon app.json** pliku, a następnie zaktualizuj hello wystąpienia właściwości too3.</span><span class="sxs-lookup"><span data-stu-id="6a512-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="6a512-150">Aktualizowanie aplikacji hello przy użyciu hello `dcos marathon app update` polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="6a512-151">toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="6a512-152">Gdy hello **zadania** zmienia wartość kolumny z *1/3* za*3/1*, wdrażanie aplikacji zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="6a512-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="6a512-153">Uruchamianie aplikacji dostępny z Internetu</span><span class="sxs-lookup"><span data-stu-id="6a512-153">Run internet accessible app</span></span>

<span data-ttu-id="6a512-154">Witaj ACS DC/OS klaster składa się z dwóch zestawów węzła, jeden publiczny, który jest dostępny na hello internet i prywatnego, który nie jest dostępny na hello internet.</span><span class="sxs-lookup"><span data-stu-id="6a512-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="6a512-155">Hello domyślny zestaw jest hello prywatnej węzłów, użytego w przykładzie ostatniego hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="6a512-156">toomake aplikacji, które są dostępne na hello internet, wdrażania ich toohello zestaw węzłów publicznych.</span><span class="sxs-lookup"><span data-stu-id="6a512-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="6a512-157">toodo tak, nadaj hello `acceptedResourceRoles` obiekt wartość `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="6a512-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="6a512-158">Utwórz plik o nazwie **nginx public.json** i hello kopiowania zawartości do niego.</span><span class="sxs-lookup"><span data-stu-id="6a512-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="6a512-159">Uruchom następujące polecenie tooschedule hello aplikacji toorun w klastrze DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="6a512-160">Pobierz publiczny adres IP hello agentów publicznych klastra DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="6a512-161">Przeglądanie adres toothis zwraca hello domyślnej NGINX witryny.</span><span class="sxs-lookup"><span data-stu-id="6a512-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="6a512-163">Skalowanie klastra DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="6a512-164">W poprzednich przykładach hello aplikacji była skalowana toomultiple wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6a512-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="6a512-165">Hello DC/OS infrastruktury można także skalowanie tooprovide więcej lub mniej wydajności obliczeniowej.</span><span class="sxs-lookup"><span data-stu-id="6a512-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="6a512-166">Jest to zrobić za pomocą hello [skalować acs az]() polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="6a512-167">toosee hello bieżąca liczba agentów DC/OS, użyj hello [Pokaż acs az](/cli/azure/acs#show) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="6a512-168">tooincrease hello too5 liczby, użyj hello [skalować acs az](/cli/azure/acs#scale) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a512-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="6a512-169">Usuń klaster DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="6a512-170">Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove klastra DC/OS i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6a512-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="6a512-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a512-171">Next steps</span></span>

<span data-ttu-id="6a512-172">W tym samouczku uzyskanych o podstawowe zadania zarządzania DC/OS w tym następujących hello.</span><span class="sxs-lookup"><span data-stu-id="6a512-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6a512-173">Tworzenie klastra usługi ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="6a512-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="6a512-174">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="6a512-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="6a512-175">Zainstaluj interfejs wiersza polecenia DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="6a512-176">Wdrażanie klastra toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a512-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="6a512-177">Skalowanie aplikacji w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="6a512-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="6a512-178">Skalowanie węzłów klastra DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="6a512-179">Usuń klaster DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="6a512-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="6a512-180">ADVANCE toohello następny samouczek toolearn o załadować równoważenia aplikacji w DC/OS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6a512-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a512-181">Równoważenie obciążenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a512-181">Load balance applications</span></span>](container-service-load-balancing.md)