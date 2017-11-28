---
title: "aaaUse rozwiązania Docker Compose na maszynie Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: Jak toouse Docker i tworzenia maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="d04ba-103">Pobierz wprowadzenie toodefine Docker i redagowanie i uruchomić aplikację usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d04ba-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="d04ba-104">Z [Redaguj](http://github.com/docker/compose), użyj toodefine plik prosty tekst aplikacja składająca się z wielu kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="d04ba-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="d04ba-105">Następnie pokrętła się na aplikację w jednym poleceniem, który jest toodeploy zdefiniowanych środowiska.</span><span class="sxs-lookup"><span data-stu-id="d04ba-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="d04ba-106">Na przykład w tym artykule opisano sposób tooquickly konfigurowania bloga WordPress z wewnętrznej bazy danych MariaDB SQL bazy danych na maszynie Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d04ba-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="d04ba-107">Umożliwia także tooset Redaguj się bardziej złożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d04ba-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="d04ba-108">Skonfiguruj Maszynę wirtualną systemu Linux jako Docker host</span><span class="sxs-lookup"><span data-stu-id="d04ba-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="d04ba-109">Można użyć różnych procedur Azure i dostępnych obrazów lub szablony Menedżera zasobów w hello Azure Marketplace toocreate Maszynę wirtualną systemu Linux i skonfigurować jako hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="d04ba-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="d04ba-110">Na przykład, zobacz [przy użyciu środowiska hello rozszerzenia maszyny Wirtualnej platformy Docker toodeploy](dockerextension.md) tooquickly tworzenia maszyny Wirtualnej systemu Ubuntu z hello rozszerzenia maszyny Wirtualnej platformy Docker Azure za pomocą [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d04ba-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="d04ba-111">Gdy używasz rozszerzenia maszyny Wirtualnej platformy Docker hello maszyny Wirtualnej jest automatycznie skonfigurowany jako Docker host i redagowanie jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="d04ba-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="d04ba-112">Utwórz hosta Docker 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d04ba-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="d04ba-113">Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d04ba-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d04ba-114">Najpierw utwórz grupę zasobów dla danego środowiska Docker [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d04ba-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d04ba-115">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="d04ba-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="d04ba-116">Następnie Wdróż maszynę Wirtualną za pomocą [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) zawierająca rozszerzenia maszyny Wirtualnej Azure Docker hello [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d04ba-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="d04ba-117">Podać własne wartości *newStorageAccountName*, *adminUsername*, *adminPassword*, i *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="d04ba-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="d04ba-118">Trwa kilka minut, aż hello toofinish wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d04ba-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="d04ba-119">Po ukończeniu wdrażania hello [Przenieś krok toonext](#verify-that-compose-is-installed) tooyour tooSSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d04ba-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="d04ba-120">Opcjonalnie dodaj monit toohello zwracany kontroli tooinstead i hello umożliwiają wdrożenie nadal w tle hello hello `--no-wait` Flaga toohello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="d04ba-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="d04ba-121">Dzięki temu tooperform pracować w hello CLI wdrożenia hello kontynuuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d04ba-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="d04ba-122">Można wyświetlić szczegółowe informacje o stanie hosta Docker hello z [az maszyny wirtualnej pokazu](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="d04ba-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="d04ba-123">Hello poniższy przykład umożliwia sprawdzenie stanu hello hello maszyny Wirtualnej o nazwie *myDockerVM* (hello domyślną nazwę szablonu hello — nie zmieniać tej nazwy) w grupie zasobów hello o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d04ba-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="d04ba-124">Jeśli to polecenie zwraca *zakończyło się pomyślnie*, hello wdrożenia zostało ukończone i można toohello SSH maszyny Wirtualnej w powitania po kroku.</span><span class="sxs-lookup"><span data-stu-id="d04ba-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="d04ba-125">Sprawdź, czy Redaguj jest zainstalowany</span><span class="sxs-lookup"><span data-stu-id="d04ba-125">Verify that Compose is installed</span></span>
<span data-ttu-id="d04ba-126">Po ukończeniu wdrażania hello SSH tooyour nowego Docker hosta przy użyciu nazwy DNS hello podane podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d04ba-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="d04ba-127">Można użyć `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview szczegóły maszyny wirtualnej, łącznie z nazwą DNS hello.</span><span class="sxs-lookup"><span data-stu-id="d04ba-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="d04ba-128">toocheck, które tworzą jest zainstalowany na powitania maszynę Wirtualną, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d04ba-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="d04ba-129">Zbyt wyświetlone dane wyjściowe podobne*rozwiązania docker compose 1.6.2, kompilacji 4d 72027*.</span><span class="sxs-lookup"><span data-stu-id="d04ba-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="d04ba-130">Jeśli użyto innej metody toocreate hostów Docker i muszą tooinstall tworzą samodzielnie, zobacz hello [tworzą dokumentacji](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="d04ba-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="d04ba-131">Utwórz plik docker-compose.yml konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d04ba-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="d04ba-132">Następnie należy utworzyć `docker-compose.yml` pliku, który jest tylko plik konfiguracji tekstu, toodefine hello Docker kontenery toorun na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d04ba-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="d04ba-133">Plik Hello określa toorun obraz powitania w każdego kontenera (lub może być kompilacji z plik Dockerfile), zmienne środowiskowe niezbędne i zależności, porty i hello łącza między kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d04ba-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="d04ba-134">Aby uzyskać więcej informacji o składni pliku yml, zobacz [tworzą odwołanie do pliku](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="d04ba-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="d04ba-135">Utwórz hello *docker-compose.yml* plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d04ba-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="d04ba-136">Użyj Twojej tooadd Edytor tekstu pliku toohello niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="d04ba-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="d04ba-137">Witaj poniższym przykładzie użyto hello *vi* edytora:</span><span class="sxs-lookup"><span data-stu-id="d04ba-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="d04ba-138">Witaj Wklej poniższy przykład w pliku tekstowym.</span><span class="sxs-lookup"><span data-stu-id="d04ba-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="d04ba-139">Ta konfiguracja korzysta z obrazów z hello [rejestru DockerHub](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello typu open source obsługi blogów i system zarządzania zawartością) i połączone wewnętrznej bazy danych MariaDB SQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d04ba-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="d04ba-140">Wprowadź własne *MYSQL_ROOT_PASSWORD* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d04ba-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="d04ba-141">Kontenery hello zaczynać się Redaguj</span><span class="sxs-lookup"><span data-stu-id="d04ba-141">Start hello containers with Compose</span></span>
<span data-ttu-id="d04ba-142">W hello sam katalogu jako sieci *docker-compose.yml* pliku, uruchom następujące polecenie hello (w zależności od środowiska, może być konieczne toorun `docker-compose` przy użyciu `sudo`):</span><span class="sxs-lookup"><span data-stu-id="d04ba-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="d04ba-143">To polecenie uruchamia kontenery Docker hello określone w *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="d04ba-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="d04ba-144">Trwa minutę lub dwie na toocomplete ten krok.</span><span class="sxs-lookup"><span data-stu-id="d04ba-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="d04ba-145">Zostaną wyświetlone dane wyjściowe toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="d04ba-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="d04ba-146">Należy się hello toouse **-d** opcja uruchamiania, aby uruchomić w tle hello stale hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d04ba-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="d04ba-147">tooverify, który kontenery hello są włączone, typ `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="d04ba-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="d04ba-148">Powinien zostać wyświetlony wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="d04ba-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="d04ba-149">Teraz możesz połączyć tooWordPress bezpośrednio na powitania maszyny Wirtualnej na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="d04ba-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="d04ba-150">Otwórz przeglądarkę sieci web i wprowadź nazwę DNS hello maszyny wirtualnej (takie jak `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="d04ba-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="d04ba-151">Powinna zostać wyświetlona hello WordPress uruchomić ekranu, w którym można ukończyć powitalnych instalację i wprowadzenie do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d04ba-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Ekran startowy WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="d04ba-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d04ba-153">Next steps</span></span>
* <span data-ttu-id="d04ba-154">Przejdź toohello [Podręcznik użytkownika rozszerzenia maszyny Wirtualnej platformy Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) więcej opcji tooconfigure Docker i Redaguj w maszynie Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d04ba-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="d04ba-155">Na przykład jedną z opcji jest tooput hello Redaguj yml pliku (przekonwertowanego tooJSON) bezpośrednio w konfiguracji hello hello rozszerzenia maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d04ba-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="d04ba-156">Zapoznaj się z hello [tworzą wiersza polecenia](http://docs.docker.com/compose/reference/) i [Podręcznik użytkownika](http://docs.docker.com/compose/) więcej przykładów dotyczących tworzenia i wdrażania aplikacji usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="d04ba-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="d04ba-157">Albo użyj szablonu usługi Azure Resource Manager, Twoje własne lub jeden przyczyniły się z hello [społeczności](https://azure.microsoft.com/documentation/templates/), skonfigurować toodeploy maszyny Wirtualnej platformy Azure, aplikacji i Docker Compose.</span><span class="sxs-lookup"><span data-stu-id="d04ba-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="d04ba-158">Na przykład Witaj [wdrażanie bloga WordPress z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) szablon używa Docker i redagowanie tooquickly wdrażanie WordPress z wewnętrznej bazy danych MySQL na maszynie Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d04ba-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="d04ba-159">Spróbuj integrowanie rozwiązania Docker Compose z klastrem Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="d04ba-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="d04ba-160">Zobacz [przy użyciu tworzą z Swarm](https://docs.docker.com/compose/swarm/) dla scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d04ba-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
