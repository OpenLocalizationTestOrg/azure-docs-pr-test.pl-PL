---
title: "obsługuje aaaCreate Docker na platformie Azure z maszyną Docker | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Użyj hostów docker toocreate maszyny Docker na platformie Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="6abd0-103">Tworzenie hostów platformy Docker na platformie Azure przy użyciu maszyny platformy Docker</span><span class="sxs-lookup"><span data-stu-id="6abd0-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="6abd0-104">Uruchomiona [Docker](https://www.docker.com/) kontenery wymaga hosta maszyny Wirtualnej uruchomionej hello docker demon.</span><span class="sxs-lookup"><span data-stu-id="6abd0-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="6abd0-105">W tym temacie opisano sposób toouse hello [docker maszyny](https://docs.docker.com/machine/) polecenia toocreate nowych maszyn wirtualnych systemu Linux, skonfigurowano hello demona Docker, działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6abd0-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="6abd0-106">**Uwaga:**</span><span class="sxs-lookup"><span data-stu-id="6abd0-106">**Note:**</span></span> 

* <span data-ttu-id="6abd0-107">*W tym artykule zależy od 0.9.0-rc2 wersją maszyny docker lub większa*</span><span class="sxs-lookup"><span data-stu-id="6abd0-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="6abd0-108">*Kontenery systemu Windows, które będą obsługiwane za pośrednictwem docker maszyny w hello Najbliższa przyszłość*</span><span class="sxs-lookup"><span data-stu-id="6abd0-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="6abd0-109">Tworzenie maszyn wirtualnych z maszyną Docker</span><span class="sxs-lookup"><span data-stu-id="6abd0-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="6abd0-110">Tworzenie docker hosta maszyn wirtualnych na platformie Azure z hello `docker-machine create` polecenia przy użyciu hello `azure` sterownika.</span><span class="sxs-lookup"><span data-stu-id="6abd0-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="6abd0-111">Hello Azure sterownik wymaga Twojego identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6abd0-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="6abd0-112">Można użyć hello [interfejsu wiersza polecenia Azure](cli-install-nodejs.md) lub hello [Azure Portal](https://portal.azure.com) tooretrieve subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6abd0-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="6abd0-113">**Przy użyciu hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="6abd0-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="6abd0-114">Wybierz **subskrypcje** z hello nawigacji po lewej stronie strony i skopiuj hello identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6abd0-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="6abd0-115">**Przy użyciu hello wiersza polecenia platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="6abd0-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="6abd0-116">Typ ```azure account list``` i identyfikator subskrypcji hello kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6abd0-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="6abd0-117">Typ `docker-machine create --driver azure` toosee hello opcje i ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="6abd0-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="6abd0-118">Możesz również sprawdzić hello [dokumentacji sterownika Azure Docker](https://docs.docker.com/machine/drivers/azure/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6abd0-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="6abd0-119">Witaj poniższy przykład, opiera się na powitania [wartości domyślne](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ale opcjonalnie ustawiona te wartości:</span><span class="sxs-lookup"><span data-stu-id="6abd0-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="6abd0-120">usługi Azure dns dla nazwy hello skojarzone z hello publicznego adresu IP i certyfikaty generowane.</span><span class="sxs-lookup"><span data-stu-id="6abd0-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="6abd0-121">Jest to nazwa DNS hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6abd0-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="6abd0-122">Hello maszyny Wirtualnej może, a następnie bezpiecznie Zatrzymaj, zwolnij hello dynamicznego adresu IP i podaj tooreconnect możliwości powitania po hello wirtualna uruchamia się ponownie z nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6abd0-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="6abd0-123">Prefiks nazwy Hello musi być unikatowa w danym regionie UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6abd0-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="6abd0-124">Otwórz port 80 na powitania wirtualna wychodzący dostęp do Internetu</span><span class="sxs-lookup"><span data-stu-id="6abd0-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="6abd0-125">rozmiar hello wirtualna tooutilize szybsze magazyn w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="6abd0-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="6abd0-126">Magazyn w warstwie Premium przeznaczony dla hello dysku maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6abd0-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="6abd0-127">Wybierz hosta z maszyną docker docker</span><span class="sxs-lookup"><span data-stu-id="6abd0-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="6abd0-128">Po utworzeniu wpisu docker maszyny dla hosta, możesz ustawić hello domyślnego hosta podczas uruchamiania polecenia docker.</span><span class="sxs-lookup"><span data-stu-id="6abd0-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="6abd0-129">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6abd0-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="6abd0-130">Przy użyciu Bash</span><span class="sxs-lookup"><span data-stu-id="6abd0-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="6abd0-131">Teraz możesz uruchamiać polecenia docker na określonym hoście hello</span><span class="sxs-lookup"><span data-stu-id="6abd0-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="6abd0-132">Uruchom kontenera</span><span class="sxs-lookup"><span data-stu-id="6abd0-132">Run a container</span></span>
<span data-ttu-id="6abd0-133">Z hosta skonfigurowane teraz możesz uruchomić tootest serwera sieci web proste czy host został skonfigurowany prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="6abd0-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="6abd0-134">W tym miejscu wyświetlonym możemy użyć obrazu standardowe nginx, określ, czy powinien nasłuchiwać na porcie 80 i że hello hosta maszyny Wirtualnej zostanie ponownie uruchomiony, kontener hello spowoduje ponowne uruchomienie również (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="6abd0-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="6abd0-135">dane wyjściowe Hello powinien wyglądać jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="6abd0-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="6abd0-136">Kontener testu hello</span><span class="sxs-lookup"><span data-stu-id="6abd0-136">Test hello container</span></span>
<span data-ttu-id="6abd0-137">Sprawdź uruchomionych kontenerów przy użyciu `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="6abd0-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="6abd0-138">I hello toosee systemem kontenera, typu `docker-machine ip <VM name>` toofind hello IP address tooenter w przeglądarce hello:</span><span class="sxs-lookup"><span data-stu-id="6abd0-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Kontener ngnix uruchomione](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="6abd0-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6abd0-140">Summary</span></span>
<span data-ttu-id="6abd0-141">Docker komputera z można łatwo udostępnić hostów docker na platformie Azure dla operacji sprawdzania poprawności programu docker poszczególnych hosta.</span><span class="sxs-lookup"><span data-stu-id="6abd0-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="6abd0-142">W środowisku produkcyjnym hosting kontenerów, zobacz hello [usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="6abd0-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="6abd0-143">toodevelop .NET Core aplikacji za pomocą programu Visual Studio, zobacz [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="6abd0-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

