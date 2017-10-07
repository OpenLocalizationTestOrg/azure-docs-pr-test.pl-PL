---
title: aaaUsing ACR z klastrem Azure DC/OS | Dokumentacja firmy Microsoft
description: "Rejestru kontenera Azure za pomocą klastra DC/OS usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, kontenerów, Micro-services, Mesos, Azure, udziału plików, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="b815b-104">Za pomocą ACR toodeploy klastra DC/OS aplikacji</span><span class="sxs-lookup"><span data-stu-id="b815b-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="b815b-105">W tym artykule, firma Microsoft Eksploruj jak toouse rejestru kontenera platformy Azure z klastrem DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b815b-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="b815b-106">Przy użyciu ACR pozwala tooprivately magazynu obrazów i zarządzanie nimi kontenera.</span><span class="sxs-lookup"><span data-stu-id="b815b-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="b815b-107">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b815b-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b815b-108">Wdrażanie rejestru kontenera platformy Azure (w razie potrzeby)</span><span class="sxs-lookup"><span data-stu-id="b815b-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="b815b-109">Skonfiguruj uwierzytelnianie ACR w klastrze DC/OS</span><span class="sxs-lookup"><span data-stu-id="b815b-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="b815b-110">Przekazać obraz toohello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b815b-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="b815b-111">Uruchom obrazu kontenera z hello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b815b-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="b815b-112">Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b815b-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="b815b-113">W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="b815b-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="b815b-114">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b815b-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b815b-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="b815b-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b815b-116">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b815b-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="b815b-117">Wdrażanie rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b815b-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="b815b-118">W razie potrzeby utwórz rejestru kontenera Azure z hello [az acr utworzyć](/cli/azure/acr#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b815b-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="b815b-119">Witaj poniższy przykład tworzy rejestru z losowo wygenerować nazwę.</span><span class="sxs-lookup"><span data-stu-id="b815b-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="b815b-120">rejestru Hello jest również konfigurowany za pomocą konta administratora przy użyciu hello `--admin-enabled` argumentu.</span><span class="sxs-lookup"><span data-stu-id="b815b-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="b815b-121">Po utworzeniu rejestru hello hello Azure CLI generuje dane podobne toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="b815b-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="b815b-122">Zwróć uwagę na powitania `name` i `loginServer`, są one używane w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="b815b-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="b815b-123">Uzyskiwanie poświadczeń rejestru kontenera hello przy użyciu hello [Pokaż poświadczeń acr az](/cli/azure/acr/credential) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b815b-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="b815b-124">SUBSTITUTE hello `--name` z jedną zanotowanym w ostatnim kroku hello hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="b815b-125">Zwróć uwagę jednego hasła jest potrzebna w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="b815b-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="b815b-126">Aby uzyskać więcej informacji na rejestru kontenera platformy Azure, zobacz [rejestrów kontenera Docker tooprivate wprowadzenie](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b815b-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="b815b-127">Zarządzanie ACR uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b815b-127">Manage ACR authentication</span></span>

<span data-ttu-id="b815b-128">Hello konwencjonalnej sposób toopush i ściągania obrazu z rejestru prywatnej toofirst uwierzytelniania za pomocą rejestru hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="b815b-129">toodo tak, czy użycie hello `docker login` na klienta, który wymaga tooaccess hello prywatnej rejestru.</span><span class="sxs-lookup"><span data-stu-id="b815b-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="b815b-130">Ponieważ klaster DC/OS może zawierać wiele węzłów, które wymagają toobe uwierzytelniani hello ACR, jest przydatne tooautomate ten proces w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="b815b-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="b815b-131">Utwórz magazyn udostępniony</span><span class="sxs-lookup"><span data-stu-id="b815b-131">Create shared storage</span></span>

<span data-ttu-id="b815b-132">Ten proces wykorzystuje na udział plików na platformę Azure, który został zainstalowany w każdym węźle klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="b815b-133">Jeśli Magazyn udostępniony nie mają już skonfigurowany, zobacz [udział plików w klastrze DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="b815b-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="b815b-134">Skonfiguruj uwierzytelnianie ACR</span><span class="sxs-lookup"><span data-stu-id="b815b-134">Configure ACR authentication</span></span>

<span data-ttu-id="b815b-135">Najpierw pobierz hello FQDN hello DC/OS wzorca i zapisze go w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="b815b-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="b815b-136">Utwórz połączenie SSH z głównego hello (lub hello pierwszego serwera głównego) klastra systemu DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b815b-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="b815b-137">Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne.</span><span class="sxs-lookup"><span data-stu-id="b815b-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="b815b-138">Uruchom następujące polecenia toologin toohello rejestru kontenera Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="b815b-139">Zastąp hello `--username` o nazwie hello hello kontenera rejestru i hello `--password` z haseł hello podane.</span><span class="sxs-lookup"><span data-stu-id="b815b-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="b815b-140">Zastąp hello ostatni argument *mycontainerregistry.azurecr.io* w przykładzie hello o nazwie loginServer hello hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="b815b-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="b815b-141">To polecenie zapisuje wartości uwierzytelniania hello lokalnie w hello `~/.docker` ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b815b-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="b815b-142">Tworzenie pliku skompresowanego, który zawiera wartości uwierzytelniania hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="b815b-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="b815b-143">Skopiuj ten plik toohello udostępnionym w klastrze magazynu.</span><span class="sxs-lookup"><span data-stu-id="b815b-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="b815b-144">Ten krok sprawia, że plik hello dostępne we wszystkich węzłach klastra DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="b815b-145">Przekaż obraz tooACR</span><span class="sxs-lookup"><span data-stu-id="b815b-145">Upload image tooACR</span></span>

<span data-ttu-id="b815b-146">Teraz z komputerze deweloperskim lub inne systemy z Docker zainstalowane, tworzenie obrazu i przekaż go toohello rejestru kontenera Azure.</span><span class="sxs-lookup"><span data-stu-id="b815b-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="b815b-147">Utwórz kontener z hello Ubuntu obrazu.</span><span class="sxs-lookup"><span data-stu-id="b815b-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="b815b-148">Teraz przechwytywania hello kontenera do nowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b815b-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="b815b-149">Nazwa obrazu Hello musi tooinclude hello `loginServer` nazwa hello registrywith kontenera w formacie `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="b815b-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="b815b-150">Zaloguj się do hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b815b-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="b815b-151">Zamień nazwę hello hello loginServer nazwę, hello — nazwa użytkownika o nazwie hello hello kontenera rejestru i hello — haseł hello podać hasło.</span><span class="sxs-lookup"><span data-stu-id="b815b-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="b815b-152">Na koniec przekazać hello obrazu toohello ACR rejestru.</span><span class="sxs-lookup"><span data-stu-id="b815b-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="b815b-153">W tym przykładzie przesyła obraz o nazwie dcos demonstracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b815b-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="b815b-154">Uruchom obrazu z ACR</span><span class="sxs-lookup"><span data-stu-id="b815b-154">Run an image from ACR</span></span>

<span data-ttu-id="b815b-155">toouse jako obraz z rejestru ACR hello, Utwórz plik nazwy *acrDemo.json* i hello kopiowania tekstu do niego.</span><span class="sxs-lookup"><span data-stu-id="b815b-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="b815b-156">Zamień nazwę obrazu hello hello kontenera rejestru loginServer nazwę i nazwa obrazu, na przykład `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="b815b-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="b815b-157">Zwróć uwagę na powitania `uris` właściwości.</span><span class="sxs-lookup"><span data-stu-id="b815b-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="b815b-158">Ta właściwość przechowuje lokalizacji hello hello kontenera rejestru uwierzytelniania pliku, który w tym przypadku jest hello udział plików na platformę Azure, który jest zainstalowany na każdym węźle w klastrze DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="b815b-159">Wdrażanie aplikacji hello przy użyciu interfejsu wiersza polecenia DC / ° c hello.</span><span class="sxs-lookup"><span data-stu-id="b815b-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="b815b-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b815b-160">Next steps</span></span>

<span data-ttu-id="b815b-161">W tym samouczku zostały skonfiguruj toouse DC/OS, który rejestru kontenera Azure tym hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b815b-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b815b-162">Wdrażanie rejestru kontenera platformy Azure (w razie potrzeby)</span><span class="sxs-lookup"><span data-stu-id="b815b-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="b815b-163">Skonfiguruj uwierzytelnianie ACR w klastrze DC/OS</span><span class="sxs-lookup"><span data-stu-id="b815b-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="b815b-164">Przekazać obraz toohello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b815b-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="b815b-165">Uruchom obrazu kontenera z hello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b815b-165">Run a container image from hello Azure Container Registry</span></span>
