---
title: "aaaAzure Szybki Start usługi kontenera - wdrożyć klaster DC/OS | Dokumentacja firmy Microsoft"
description: "Azure kontenera usługi Szybki Start — wdrażanie klastra DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="661a9-104">Wdrażanie klastra DC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="661a9-105">DC/OS przewiduje uruchamianie nowoczesnych i konteneryzowanych aplikacji rozproszonej platformy.</span><span class="sxs-lookup"><span data-stu-id="661a9-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="661a9-106">Z usługi kontenera platformy Azure inicjowania obsługi klastra DC/OS gotowy produkcji jest proste i szybkie.</span><span class="sxs-lookup"><span data-stu-id="661a9-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="661a9-107">To szybki start szczegóły hello podstawowe wymagane czynności toodeploy klastra DC/OS i wykonywania podstawowych obciążenia.</span><span class="sxs-lookup"><span data-stu-id="661a9-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="661a9-108">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="661a9-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="661a9-109">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="661a9-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="661a9-110">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="661a9-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="661a9-111">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="661a9-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="661a9-112">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="661a9-112">Log in tooAzure</span></span> 

<span data-ttu-id="661a9-113">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="661a9-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="661a9-114">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="661a9-114">Create a resource group</span></span>

<span data-ttu-id="661a9-115">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="661a9-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="661a9-116">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="661a9-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="661a9-117">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="661a9-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="661a9-118">Tworzenie klastra DC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-118">Create DC/OS cluster</span></span>

<span data-ttu-id="661a9-119">Tworzenie klastra DC/OS z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="661a9-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="661a9-120">Witaj poniższy przykład tworzy klaster DC/OS o nazwie *myDCOSCluster* i tworzy kluczy SSH, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="661a9-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="661a9-121">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="661a9-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="661a9-122">Po kilku minutach polecenia hello kończy i zwraca informacje na temat wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="661a9-123">Połącz klaster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="661a9-124">Po utworzeniu klastra DC/OS, może być dostęp za pośrednictwem tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="661a9-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="661a9-125">Uruchom następujące polecenia tooreturn hello publicznego adresu IP wzorca DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="661a9-126">Ten adres IP jest przechowywana w zmiennej i używane w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="661a9-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="661a9-127">toocreate hello tunelu SSH, uruchom następujące polecenie hello i hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="661a9-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="661a9-128">Jeśli port 80 jest już w użyciu, hello polecenie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="661a9-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="661a9-129">Aktualizacja hello tunelowane tooone portu nieużywany, takich jak `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="661a9-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="661a9-130">Tunel SSH Hello mogą być testowane za przeglądanie za`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="661a9-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="661a9-131">Jeśli port innych czy 80 został użyty, Dostosuj hello toomatch lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="661a9-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="661a9-132">W przypadku tunelowania SSH hello została pomyślnie utworzona, jest zwracana hello DC/OS portalu.</span><span class="sxs-lookup"><span data-stu-id="661a9-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![DCOS INTERFEJSU UŻYTKOWNIKA](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="661a9-134">Instalowanie interfejsu wiersza polecenia DC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-134">Install DC/OS CLI</span></span>

<span data-ttu-id="661a9-135">Interfejs wiersza polecenia DC/OS Hello jest używany toomanage klastra DC/OS z hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="661a9-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="661a9-136">Zainstaluj interfejs wiersza polecenia hello DC/OS jest przy użyciu hello [az dcos acs install-cli](/azure/acs/dcos#install-cli) polecenia.</span><span class="sxs-lookup"><span data-stu-id="661a9-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="661a9-137">Jeśli używasz usługi Azure CloudShell hello interfejsu wiersza polecenia DC/OS jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="661a9-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="661a9-138">Jeśli używasz hello Azure CLI macOS lub Linux, może być konieczne toorun hello polecenie sudo.</span><span class="sxs-lookup"><span data-stu-id="661a9-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="661a9-139">Przed hello interfejsu wiersza polecenia można używać z klastrem hello musi ona być tunelu SSH hello toouse skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="661a9-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="661a9-140">toodo tak, uruchom hello następujące polecenia, dostosowywania hello portu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="661a9-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="661a9-141">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="661a9-141">Run an application</span></span>

<span data-ttu-id="661a9-142">Domyślnie Hello planowania mechanizm dla klastra usługi ACS DC/OS jest Marathon.</span><span class="sxs-lookup"><span data-stu-id="661a9-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="661a9-143">Marathon jest toostart używanych aplikacji i zarządzanie stanem hello aplikacji hello w klastrze DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="661a9-144">tooschedule aplikacji za pośrednictwem platformy Marathon, Utwórz plik o nazwie *marathon app.json*, i hello kopiowania zawartości do niego.</span><span class="sxs-lookup"><span data-stu-id="661a9-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="661a9-145">Uruchom następujące polecenie tooschedule hello aplikacji toorun w klastrze DC/OS hello hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="661a9-146">toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="661a9-147">Gdy hello **oczekiwania** zmienia wartość kolumny z *True* za*False*, wdrażanie aplikacji zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="661a9-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="661a9-148">Pobierz publiczny adres IP hello agentów klastra DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="661a9-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="661a9-149">Przeglądanie adres toothis zwraca hello domyślnej NGINX witryny.</span><span class="sxs-lookup"><span data-stu-id="661a9-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="661a9-151">Usuń klaster DC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="661a9-152">Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove klastra DC/OS i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="661a9-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="661a9-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="661a9-153">Next steps</span></span>

<span data-ttu-id="661a9-154">W tym szybki start wdrożeniu klastra DC/OS i zostały uruchomione proste kontenera Docker na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="661a9-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="661a9-155">toolearn więcej informacji na temat usługi kontenera platformy Azure, nadal samouczki toohello ACS.</span><span class="sxs-lookup"><span data-stu-id="661a9-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="661a9-156">Zarządzanie klastrem ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="661a9-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)