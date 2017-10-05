---
title: "Użyj rozwiązania Docker Compose się na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak używać Docker i tworzenia maszyn wirtualnych systemu Linux z wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="a06a8-103">Rozpoczynanie pracy z Docker i wysyłanych do definiowania i uruchomić aplikację usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a06a8-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="a06a8-104">Z [Redaguj](http://github.com/docker/compose), zdefiniuj aplikacja składająca się z wielu kontenerów Docker przy użyciu pliku zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="a06a8-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="a06a8-105">Następnie pokrętła się na aplikację za pomocą jednego polecenia, który wykonuje wszystkie informacje niezbędne do wdrożenia środowiska zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="a06a8-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="a06a8-106">Na przykład w tym artykule przedstawiono sposób szybko skonfigurować bloga WordPress z bazy danych MariaDB SQL na maszynie Wirtualnej systemu Ubuntu wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a06a8-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="a06a8-107">Redaguj umożliwia również skonfigurowanie bardziej złożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a06a8-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="a06a8-108">Skonfiguruj Maszynę wirtualną systemu Linux jako Docker host</span><span class="sxs-lookup"><span data-stu-id="a06a8-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="a06a8-109">Aby utworzyć Maszynę wirtualną systemu Linux i skonfigurować jako hosta Docker można użyć różnych procedur Azure i dostępnych obrazów lub szablony Menedżera zasobów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a06a8-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="a06a8-110">Na przykład, zobacz [wdrażanie środowiska za pomocą rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md) do szybkiego tworzenia maszyny Wirtualnej systemu Ubuntu rozszerzenie maszyny Wirtualnej platformy Docker Azure za pomocą [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="a06a8-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="a06a8-111">Gdy używasz rozszerzenia maszyny Wirtualnej platformy Docker maszyny Wirtualnej jest automatycznie skonfigurowany jako Docker host i redagowanie jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="a06a8-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="a06a8-112">Utwórz hosta Docker 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a06a8-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="a06a8-113">Zainstaluj najnowszą [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się do platformy Azure konta przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a06a8-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a06a8-114">Najpierw utwórz grupę zasobów dla danego środowiska Docker [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a06a8-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a06a8-115">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *westus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a06a8-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="a06a8-116">Następnie należy wdrożyć maszynę Wirtualną z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) zawierającej rozszerzenie Azure Docker VM z [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="a06a8-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="a06a8-117">Podać własne wartości *newStorageAccountName*, *adminUsername*, *adminPassword*, i *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="a06a8-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="a06a8-118">Trwa kilka minut dla wdrożenia, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="a06a8-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="a06a8-119">Po zakończeniu wdrożenia [Przenieś do następnego kroku](#verify-that-compose-is-installed) do SSH do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a06a8-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="a06a8-120">Opcjonalnie, aby zamiast tego zwrócić kontrolkę na ten monit i pozwolić wdrożenia kontynuowane w tle, należy dodać `--no-wait` Flaga poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="a06a8-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="a06a8-121">Ten proces pozwala wykonywać inne zadania w interfejsu wiersza polecenia, gdy wdrożenie nadal kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a06a8-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="a06a8-122">Można wyświetlić szczegółowe informacje o stanie hosta Docker z [az maszyny wirtualnej pokazu](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="a06a8-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="a06a8-123">Poniższy przykład umożliwia sprawdzenie stanu maszyny wirtualnej o nazwie *myDockerVM* (nazwa domyślnego szablonu — nie zmieniać tej nazwy) w grupie zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a06a8-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="a06a8-124">Jeśli to polecenie zwraca *zakończyło się pomyślnie*, wdrożenie zostało ukończone i można SSH dla maszyny wirtualnej w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="a06a8-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="a06a8-125">Sprawdź, czy Redaguj jest zainstalowany</span><span class="sxs-lookup"><span data-stu-id="a06a8-125">Verify that Compose is installed</span></span>
<span data-ttu-id="a06a8-126">Po zakończeniu wdrożenia SSH z nowy host platformy Docker za pomocą DNS nazw zostanie podana podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a06a8-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="a06a8-127">Można użyć `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` Aby wyświetlić szczegóły maszyny Wirtualnej, łącznie z nazwą DNS.</span><span class="sxs-lookup"><span data-stu-id="a06a8-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="a06a8-128">Aby sprawdzić, czy Redaguj jest zainstalowany na Maszynie wirtualnej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a06a8-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="a06a8-129">Zobacz dane wyjściowe podobne do *rozwiązania docker compose 1.6.2, kompilacji 4d 72027*.</span><span class="sxs-lookup"><span data-stu-id="a06a8-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="a06a8-130">Jeśli używasz innej metody do tworzenia hostów Docker i trzeba instalować samodzielnie utworzyć, zobacz [tworzą dokumentacji](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="a06a8-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="a06a8-131">Utwórz plik docker-compose.yml konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a06a8-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="a06a8-132">Następnie należy utworzyć `docker-compose.yml` pliku, który jest tylko konfiguracja pliku tekstowego, aby zdefiniować kontenery Docker do uruchamiania na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a06a8-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="a06a8-133">Plik Określa obraz do uruchamiania na każdego kontenera (lub może być kompilacji z plik Dockerfile), zmienne środowiskowe niezbędne i zależności, porty i linki między kontenerów.</span><span class="sxs-lookup"><span data-stu-id="a06a8-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="a06a8-134">Aby uzyskać więcej informacji o składni pliku yml, zobacz [tworzą odwołanie do pliku](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="a06a8-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="a06a8-135">Utwórz *docker-compose.yml* plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a06a8-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="a06a8-136">Aby dodać niektóre dane do pliku, użyj w ulubionym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a06a8-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="a06a8-137">W poniższym przykładzie użyto *vi* edytora:</span><span class="sxs-lookup"><span data-stu-id="a06a8-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="a06a8-138">Wklej poniższy przykład w pliku tekstowym.</span><span class="sxs-lookup"><span data-stu-id="a06a8-138">Paste the following example into your text file.</span></span> <span data-ttu-id="a06a8-139">Ta konfiguracja korzysta z obrazów z [rejestru DockerHub](https://registry.hub.docker.com/_/wordpress/) zainstalować WordPress (typu open source obsługi blogów i system zarządzania zawartością) i połączone wewnętrznej bazy danych MariaDB SQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a06a8-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="a06a8-140">Wprowadź własne *MYSQL_ROOT_PASSWORD* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a06a8-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="a06a8-141">Kontenery zaczynać się Redaguj</span><span class="sxs-lookup"><span data-stu-id="a06a8-141">Start the containers with Compose</span></span>
<span data-ttu-id="a06a8-142">W tym samym katalogu co Twoje *docker-compose.yml* plików, uruchom następujące polecenie (w zależności od środowiska, może być konieczne uruchomienie `docker-compose` przy użyciu `sudo`):</span><span class="sxs-lookup"><span data-stu-id="a06a8-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="a06a8-143">To polecenie uruchamia kontenery Docker określone w *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="a06a8-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="a06a8-144">Trwa minutę lub dwie do ukończenia tego kroku.</span><span class="sxs-lookup"><span data-stu-id="a06a8-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="a06a8-145">Zostaną wyświetlone dane wyjściowe podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="a06a8-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="a06a8-146">Należy użyć **-d** opcję przy uruchamianiu, dzięki czemu kontenery stale uruchomione w tle.</span><span class="sxs-lookup"><span data-stu-id="a06a8-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="a06a8-147">Aby sprawdzić, czy kontenery są uruchomione, wpisz `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="a06a8-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="a06a8-148">Powinien zostać wyświetlony wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="a06a8-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="a06a8-149">Można teraz nawiązać WordPress bezpośrednio na Maszynie wirtualnej na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="a06a8-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="a06a8-150">Otwórz przeglądarkę sieci web, a następnie wprowadź nazwę DNS maszyny Wirtualnej (takie jak `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="a06a8-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="a06a8-151">Powinien zostać wyświetlony WordPress ekranu startowego, gdzie może ukończyć instalację i rozpocząć pracę z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a06a8-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![Ekran startowy WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="a06a8-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a06a8-153">Next steps</span></span>
* <span data-ttu-id="a06a8-154">Przejdź do [Podręcznik użytkownika rozszerzenia maszyny Wirtualnej platformy Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) dla więcej opcji, aby skonfigurować Docker i redagowanie w maszynie Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="a06a8-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="a06a8-155">Na przykład jedną opcję jest umieszczony plik yml Redaguj (przekonwertowane na format JSON) bezpośrednio w konfiguracji rozszerzenia maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="a06a8-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="a06a8-156">Zapoznaj się z [tworzą wiersza polecenia](http://docs.docker.com/compose/reference/) i [Podręcznik użytkownika](http://docs.docker.com/compose/) więcej przykładów dotyczących tworzenia i wdrażania aplikacji usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="a06a8-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="a06a8-157">Albo użyj szablonu usługi Azure Resource Manager, Twoje własne lub jeden przyczyniły się z [społeczności](https://azure.microsoft.com/documentation/templates/), aby wdrożyć maszyny Wirtualnej platformy Azure z tworzenia aplikacji i Docker.</span><span class="sxs-lookup"><span data-stu-id="a06a8-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="a06a8-158">Na przykład [wdrażanie bloga WordPress z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) szablon używa Docker i redagowanie można szybko wdrożyć WordPress z wewnętrznej bazy danych MySQL na maszynie Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a06a8-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="a06a8-159">Spróbuj integrowanie rozwiązania Docker Compose z klastrem Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a06a8-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="a06a8-160">Zobacz [przy użyciu tworzą z Swarm](https://docs.docker.com/compose/swarm/) dla scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="a06a8-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
