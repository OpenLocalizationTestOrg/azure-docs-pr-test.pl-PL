---
title: Witaj aaaUse rozszerzenia maszyny Wirtualnej Azure Docker | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello tooquickly rozszerzenia maszyny Wirtualnej platformy Docker bezpiecznego wdrażania w środowisku Docker na platformie Azure przy użyciu szablonów usługi Resource Manager i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="347ff-103">Tworzenie środowiska Docker na platformie Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello</span><span class="sxs-lookup"><span data-stu-id="347ff-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="347ff-104">Docker jest popularnych kontenera zarządzania i tworzenia obrazu platformy, która umożliwia tooquickly pracy z kontenerami w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="347ff-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="347ff-105">Na platformie Azure istnieją różne sposoby, które można wdrożyć zgodnie z potrzebami tooyour Docker.</span><span class="sxs-lookup"><span data-stu-id="347ff-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="347ff-106">Ten artykuł skupia się na używanie rozszerzenia maszyny Wirtualnej platformy Docker hello i szablony usługi Azure Resource Manager z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="347ff-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="347ff-107">Można również wykonać te kroki hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="347ff-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="347ff-108">Omówienie rozszerzenia Docker maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="347ff-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="347ff-109">Witaj rozszerzenia maszyny Wirtualnej Azure Docker instaluje i konfiguruje demon Docker powitania klienta Docker i rozwiązania Docker Compose na maszynie wirtualnej systemu Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="347ff-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="347ff-110">Przy użyciu rozszerzenia maszyny Wirtualnej Azure Docker hello, mieć więcej kontroli i funkcji niż po prostu przy użyciu rozwiązania Docker maszyny lub tworzenie hostów Docker hello samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="347ff-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="347ff-111">Te dodatkowe funkcje, takie jak [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/), Ustaw rozszerzenie maszyny Wirtualnej Azure Docker hello nadaje się do bardziej niezawodne środowiska dewelopera lub produkcji.</span><span class="sxs-lookup"><span data-stu-id="347ff-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="347ff-112">Aby uzyskać więcej informacji na temat hello różne metody wdrażania, przy użyciu rozwiązania Docker maszyny i usługi kontenera platformy Azure, w tym temacie hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="347ff-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="347ff-113">Prototyp tooquickly usługi aplikacji, można utworzyć przy użyciu jednego hosta Docker [maszyny Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="347ff-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="347ff-114">toobuild gotowe do produkcji, skalowalnej środowiskach, które zapewniają dodatkowe planowanie i narzędzia do zarządzania, można wdrożyć [Docker Swarm klastra na usługi kontenera platformy Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="347ff-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="347ff-115">Wdrażanie szablonu z hello rozszerzenia maszyny Wirtualnej Azure Docker</span><span class="sxs-lookup"><span data-stu-id="347ff-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="347ff-116">Teraz Użyj istniejącego toocreate szablon szybkiego startu maszyny Wirtualnej systemu Ubuntu używa tooinstall rozszerzenia maszyny Wirtualnej Azure Docker hello i skonfiguruj hello Docker hosta.</span><span class="sxs-lookup"><span data-stu-id="347ff-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="347ff-117">Można wyświetlić szablon hello tutaj: [proste wdrożenie maszyny Wirtualnej systemu Ubuntu z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="347ff-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="347ff-118">Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="347ff-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="347ff-119">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="347ff-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="347ff-120">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="347ff-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="347ff-121">Następnie Wdróż maszynę Wirtualną za pomocą [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) zawierająca rozszerzenia maszyny Wirtualnej Azure Docker hello [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="347ff-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="347ff-122">Podać własne wartości *newStorageAccountName*, *adminUsername*, *adminPassword*, i *dnsNameForPublicIP* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="347ff-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="347ff-123">Trwa kilka minut, aż hello toofinish wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="347ff-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="347ff-124">Po ukończeniu wdrażania hello [Przenieś krok toonext](#deploy-your-first-nginx-container) tooyour tooSSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="347ff-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="347ff-125">Opcjonalnie dodaj monit toohello zwracany kontroli tooinstead i hello umożliwiają wdrożenie nadal w tle hello hello `--no-wait` Flaga toohello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="347ff-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="347ff-126">Dzięki temu tooperform pracować w hello CLI wdrożenia hello kontynuuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="347ff-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="347ff-127">Można wyświetlić szczegółowe informacje o stanie hosta Docker hello z [az maszyny wirtualnej pokazu](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="347ff-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="347ff-128">Hello poniższy przykład umożliwia sprawdzenie stanu hello hello maszyny Wirtualnej o nazwie *myDockerVM* (hello domyślną nazwę szablonu hello — nie zmieniać tej nazwy) w grupie zasobów hello o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="347ff-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="347ff-129">Jeśli to polecenie zwraca *zakończyło się pomyślnie*, hello wdrożenia zostało ukończone i można toohello SSH maszyny Wirtualnej w powitania po kroku.</span><span class="sxs-lookup"><span data-stu-id="347ff-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="347ff-130">Wdrażanie Twojego pierwszego kontener nginx</span><span class="sxs-lookup"><span data-stu-id="347ff-130">Deploy your first nginx container</span></span>
<span data-ttu-id="347ff-131">Szczegóły tooview maszyny wirtualnej, takie jak nazwa DNS hello, użyj `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="347ff-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="347ff-132">SSH tooyour Docker nowego hosta z komputera lokalnego w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="347ff-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="347ff-133">Po zalogowaniu toohello Docker hosta, uruchom teraz kontener nginx:</span><span class="sxs-lookup"><span data-stu-id="347ff-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="347ff-134">dane wyjściowe Hello jest toohello podobnie poniższy przykład, jak obraz nginx hello jest pobierany i kontener uruchomiona:</span><span class="sxs-lookup"><span data-stu-id="347ff-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="347ff-135">Sprawdź stan hello kontenerów hello uruchomionych na hoście Docker w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="347ff-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="347ff-136">dane wyjściowe Hello toohello podobnie poniższy przykład, przedstawiający ten kontener nginx hello jest uruchomiona i porty TCP 80 i 443 i przesyłane dalej:</span><span class="sxs-lookup"><span data-stu-id="347ff-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="347ff-137">Otwórz z kontenera akcji, toosee Konfigurowanie przeglądarki sieci web i wprowadź nazwę DNS hello danego hosta Docker:</span><span class="sxs-lookup"><span data-stu-id="347ff-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Kontener ngnix uruchomione](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="347ff-139">Odwołanie do szablonu Azure rozszerzenia maszyny Wirtualnej platformy Docker</span><span class="sxs-lookup"><span data-stu-id="347ff-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="347ff-140">Witaj w poprzednim przykładzie używa istniejący szablon szybkiego startu.</span><span class="sxs-lookup"><span data-stu-id="347ff-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="347ff-141">Można także wdrożyć rozszerzenie maszyny Wirtualnej Azure Docker hello z szablonami usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="347ff-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="347ff-142">toodo tak, Dodaj hello następujące szablony Menedżera zasobów tooyour, definiowanie hello `vmName` maszyny wirtualnej odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="347ff-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="347ff-143">Można znaleźć bardziej szczegółowe wskazówki na korzystanie z szablonów usługi Resource Manager odczytując [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="347ff-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="347ff-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="347ff-144">Next steps</span></span>
<span data-ttu-id="347ff-145">Warto zapoznać się z zbyt[skonfigurować port TCP demon Docker hello](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), zrozumieć [zabezpieczeń Docker](https://docs.docker.com/engine/security/security/), lub wdrażanie kontenerów przy użyciu [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="347ff-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="347ff-146">Aby uzyskać więcej informacji na powitania rozszerzenia maszyny Wirtualnej platformy Docker Azure się w temacie hello [projektu GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="347ff-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="347ff-147">Przeczytaj więcej informacji na temat opcji hello do wdrażania dodatkowych Docker na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="347ff-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="347ff-148">Użyj Docker maszyny z hello Azure sterownika</span><span class="sxs-lookup"><span data-stu-id="347ff-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="347ff-149">[Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="347ff-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="347ff-150">Wdrażanie klastra usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="347ff-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

