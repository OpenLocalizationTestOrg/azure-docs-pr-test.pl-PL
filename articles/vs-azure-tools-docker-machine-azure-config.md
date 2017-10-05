---
title: "Tworzenie hostów Docker na platformie Azure z maszyną Docker | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano stosowania Docker maszyny, aby utworzyć hostów docker na platformie Azure."
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
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="84e5f-103">Tworzenie hostów platformy Docker na platformie Azure przy użyciu maszyny platformy Docker</span><span class="sxs-lookup"><span data-stu-id="84e5f-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="84e5f-104">Uruchomiona [Docker](https://www.docker.com/) kontenery wymaga hosta demona docker uruchomionych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84e5f-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="84e5f-105">W tym temacie opisano sposób użycia [docker maszyny](https://docs.docker.com/machine/) polecenie, aby utworzyć nowych maszyn wirtualnych systemu Linux, skonfigurowano demona Docker działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="84e5f-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="84e5f-106">**Uwaga:**</span><span class="sxs-lookup"><span data-stu-id="84e5f-106">**Note:**</span></span> 

* <span data-ttu-id="84e5f-107">*W tym artykule zależy od 0.9.0-rc2 wersją maszyny docker lub większa*</span><span class="sxs-lookup"><span data-stu-id="84e5f-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="84e5f-108">*Kontenery systemu Windows będą obsługiwane za pośrednictwem docker maszyny w najbliższej przyszłości*</span><span class="sxs-lookup"><span data-stu-id="84e5f-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="84e5f-109">Tworzenie maszyn wirtualnych z maszyną Docker</span><span class="sxs-lookup"><span data-stu-id="84e5f-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="84e5f-110">Tworzenie docker hosta maszyn wirtualnych na platformie Azure z `docker-machine create` polecenie, używając `azure` sterownika.</span><span class="sxs-lookup"><span data-stu-id="84e5f-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="84e5f-111">Azure sterownik wymaga Twojego identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e5f-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="84e5f-112">Można użyć [interfejsu wiersza polecenia Azure](cli-install-nodejs.md) lub [Azure Portal](https://portal.azure.com) można pobrać subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84e5f-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="84e5f-113">**Przy użyciu portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="84e5f-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="84e5f-114">Wybierz **subskrypcje** ze strony nawigacji po lewej stronie i skopiuj identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e5f-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="84e5f-115">**Korzystanie z interfejsu wiersza polecenia platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="84e5f-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="84e5f-116">Typ ```azure account list``` i skopiuj identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84e5f-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="84e5f-117">Typ `docker-machine create --driver azure` opcje i ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="84e5f-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="84e5f-118">Możesz również sprawdzić [dokumentacji sterownika Azure Docker](https://docs.docker.com/machine/drivers/azure/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="84e5f-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="84e5f-119">Poniższy przykład, opiera się na [wartości domyślne](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ale opcjonalnie ustawiona te wartości:</span><span class="sxs-lookup"><span data-stu-id="84e5f-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="84e5f-120">usługi Azure dns dla nazwy skojarzonej z publicznego adresu IP i certyfikaty generowane.</span><span class="sxs-lookup"><span data-stu-id="84e5f-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="84e5f-121">Jest to nazwa DNS na komputerze wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="84e5f-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="84e5f-122">Maszyna wirtualna może, a następnie bezpiecznie Zatrzymaj, zwolnij dynamicznego adresu IP i umożliwiają Połącz ponownie, gdy maszyna wirtualna uruchamia się ponownie z nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="84e5f-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="84e5f-123">Prefiks nazwy musi być unikatowa w danym regionie UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="84e5f-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="84e5f-124">Otwórz port 80 na Maszynie wirtualnej wychodzący dostęp do Internetu</span><span class="sxs-lookup"><span data-stu-id="84e5f-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="84e5f-125">rozmiar maszyny Wirtualnej, aby korzystać z szybsze magazyn w warstwie premium</span><span class="sxs-lookup"><span data-stu-id="84e5f-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="84e5f-126">Magazyn w warstwie Premium przeznaczony dla dysku maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="84e5f-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="84e5f-127">Wybierz hosta z maszyną docker docker</span><span class="sxs-lookup"><span data-stu-id="84e5f-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="84e5f-128">Po utworzeniu wpisu docker maszyny dla hosta, można ustawić domyślnego hosta podczas uruchamiania polecenia docker.</span><span class="sxs-lookup"><span data-stu-id="84e5f-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="84e5f-129">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="84e5f-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="84e5f-130">Przy użyciu Bash</span><span class="sxs-lookup"><span data-stu-id="84e5f-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="84e5f-131">Teraz możesz uruchamiać polecenia docker na określonym hoście</span><span class="sxs-lookup"><span data-stu-id="84e5f-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="84e5f-132">Uruchom kontenera</span><span class="sxs-lookup"><span data-stu-id="84e5f-132">Run a container</span></span>
<span data-ttu-id="84e5f-133">Za pomocą skonfigurowanego można teraz uruchomić serwera sieci web proste, aby sprawdzić, czy host został skonfigurowany prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="84e5f-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="84e5f-134">W tym miejscu wyświetlonym możemy użyć obrazu standardowe nginx, określ, czy powinien nasłuchiwać na porcie 80, a także że po ponownym uruchomieniu hosta maszyny Wirtualnej, będą kontenera Uruchom ponownie również (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="84e5f-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="84e5f-135">Dane wyjściowe powinien wyglądać jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="84e5f-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="84e5f-136">Kontener testu</span><span class="sxs-lookup"><span data-stu-id="84e5f-136">Test the container</span></span>
<span data-ttu-id="84e5f-137">Sprawdź uruchomionych kontenerów przy użyciu `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="84e5f-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="84e5f-138">I wyświetlić uruchomionych kontenera, wpisz `docker-machine ip <VM name>` Aby znaleźć adres IP, aby wprowadzić w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="84e5f-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Kontener ngnix uruchomione](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="84e5f-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="84e5f-140">Summary</span></span>
<span data-ttu-id="84e5f-141">Docker komputera z można łatwo udostępnić hostów docker na platformie Azure dla operacji sprawdzania poprawności programu docker poszczególnych hosta.</span><span class="sxs-lookup"><span data-stu-id="84e5f-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="84e5f-142">W środowisku produkcyjnym hosting kontenerów, zobacz [usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="84e5f-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="84e5f-143">Aby opracować aplikacji .NET Core z programem Visual Studio, zobacz [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="84e5f-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

