---
title: "Umożliwia tworzenie hosty systemu Linux na platformie Azure maszyny Docker | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące używania maszyny Docker można utworzyć hostów Docker na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a><span data-ttu-id="a56fe-103">Tworzenie hostów na platformie Azure przy użyciu rozwiązania Docker maszyny</span><span class="sxs-lookup"><span data-stu-id="a56fe-103">How to use Docker Machine to create hosts in Azure</span></span>
<span data-ttu-id="a56fe-104">W tym artykule szczegółowo sposób użycia [maszyny Docker](https://docs.docker.com/machine/) utworzyć hostów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a56fe-104">This article details how to use [Docker Machine](https://docs.docker.com/machine/) to create hosts in Azure.</span></span> <span data-ttu-id="a56fe-105">`docker-machine` Polecenie tworzy maszynę wirtualną systemu Linux (VM) na platformie Azure, a następnie instaluje Docker.</span><span class="sxs-lookup"><span data-stu-id="a56fe-105">The `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="a56fe-106">Następnie można zarządzać hostach Docker na platformie Azure przy użyciu tych samych narzędzi lokalnych i przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="a56fe-106">You can then manage your Docker hosts in Azure using the same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="a56fe-107">Tworzenie maszyn wirtualnych z maszyną Docker</span><span class="sxs-lookup"><span data-stu-id="a56fe-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="a56fe-108">Najpierw uzyskać identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a56fe-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="a56fe-109">Tworzenie maszyn wirtualnych z hostów Docker na platformie Azure z `docker-machine create` , określając *azure* jako sterownika.</span><span class="sxs-lookup"><span data-stu-id="a56fe-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as the driver.</span></span> <span data-ttu-id="a56fe-110">Aby uzyskać więcej informacji, zobacz [dokumentacji Docker Azure sterownika](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="a56fe-110">For more information, see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="a56fe-111">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*, tworzy konto użytkownika o nazwie *azureuser*i powoduje otwarcie portu *80* na hoście maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a56fe-111">The following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on the host VM.</span></span> <span data-ttu-id="a56fe-112">Wykonaj żadnych monitów, aby zalogować się do konta platformy Azure i udzielić maszyny Docker uprawnienia do tworzenia i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="a56fe-112">Follow any prompts to log in to your Azure account and grant Docker Machine permissions to create and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="a56fe-113">Dane wyjściowe wygląda podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="a56fe-113">The output looks similar to the following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="a56fe-114">Skonfiguruj powłoki Docker</span><span class="sxs-lookup"><span data-stu-id="a56fe-114">Configure your Docker shell</span></span>
<span data-ttu-id="a56fe-115">Aby połączyć się z hostów Docker na platformie Azure, należy zdefiniować odpowiednie ustawienia połączeń.</span><span class="sxs-lookup"><span data-stu-id="a56fe-115">To connect to your Docker host in Azure, define the appropriate connection settings.</span></span> <span data-ttu-id="a56fe-116">Jak wspomniano na końcu danych wyjściowych, wyświetlić informacje o połączeniu dla hosta Docker w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a56fe-116">As noted at the end of the output, view the connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="a56fe-117">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="a56fe-117">The output is similar to the following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="a56fe-118">Zdefiniować połączenie ustawienia, można uruchomić polecenie sugerowanych konfiguracji (`eval $(docker-machine env myvmdocker)`), lub ręcznie ustawić zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="a56fe-118">To define the connection settings you can either run the suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set the environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="a56fe-119">Uruchom kontenera</span><span class="sxs-lookup"><span data-stu-id="a56fe-119">Run a container</span></span>
<span data-ttu-id="a56fe-120">Aby wyświetlić kontenera akcji, umożliwia uruchamianie podstawowy serwer sieci Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="a56fe-120">To see a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="a56fe-121">Tworzenie kontenera z `docker run` i ujawnia port 80 dla ruchu w sieci web w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a56fe-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="a56fe-122">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="a56fe-122">The output is similar to the following example:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="a56fe-123">Widok uruchomionych kontenerów z `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="a56fe-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="a56fe-124">Następujące przykładowe dane wyjściowe wyglądają kontener NGINX z portu 80 udostępniane:</span><span class="sxs-lookup"><span data-stu-id="a56fe-124">The following example output shows the NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a><span data-ttu-id="a56fe-125">Kontener testu</span><span class="sxs-lookup"><span data-stu-id="a56fe-125">Test the container</span></span>
<span data-ttu-id="a56fe-126">Uzyskaj publiczny adres IP hosta Docker w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a56fe-126">Obtain the public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="a56fe-127">Aby wyświetlić kontenera w akcji, otwórz przeglądarkę sieci web i wprowadź publicznego adresu IP w danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="a56fe-127">To see the container in action, open a web browser and enter the public IP address noted in the output of the preceding command:</span></span>

![Kontener ngnix uruchomione](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="a56fe-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a56fe-129">Next steps</span></span>
<span data-ttu-id="a56fe-130">Można również utworzyć hostów z [rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="a56fe-130">You can also create hosts with the [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="a56fe-131">Przykłady przy użyciu rozwiązania Docker Compose można znaleźć [wprowadzenie Docker i redagowanie na platformie Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="a56fe-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
