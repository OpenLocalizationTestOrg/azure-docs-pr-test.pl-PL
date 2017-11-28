---
title: aaaInstall MongoDB na maszynie Wirtualnej systemu Linux z hello Azure CLI | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfigurować bazy danych MongoDB na systemie Linux hello iusing maszyny wirtualnej Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="c7945-103">Jak tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c7945-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="c7945-104">[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="c7945-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="c7945-105">W tym artykule opisano sposób tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c7945-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="c7945-106">Można również wykonać te kroki hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7945-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="c7945-107">Przykłady są wyświetlane szczegóły tego jak do:</span><span class="sxs-lookup"><span data-stu-id="c7945-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="c7945-108">Ręcznie zainstaluj i skonfiguruj podstawowe wystąpienie bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="c7945-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="c7945-109">Utwórz podstawowe wystąpienie bazy danych MongoDB przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7945-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="c7945-110">Tworzenie złożonych bazy danych MongoDB ustawia podzielonej klaster z repliki przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7945-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="c7945-111">Ręcznie zainstaluj i skonfiguruj bazy danych MongoDB na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7945-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="c7945-112">Bazy danych MongoDB [zawierają instrukcje instalacji](https://docs.mongodb.com/manual/administration/install-on-linux/) dla dystrybucjach systemu Linux, łącznie z Red Hat / CentOS, SUSE, Ubuntu i Debian.</span><span class="sxs-lookup"><span data-stu-id="c7945-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="c7945-113">Witaj poniższy przykład tworzy *CentOS* maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7945-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="c7945-114">toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c7945-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c7945-115">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c7945-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c7945-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c7945-117">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c7945-118">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z użytkownikiem o nazwie *azureuser* przy użyciu uwierzytelniania klucza publicznego SSH</span><span class="sxs-lookup"><span data-stu-id="c7945-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="c7945-119">Toohello SSH maszyny Wirtualnej przy użyciu własnej nazwy użytkownika i hello `publicIpAddress` wymienionych w danych wyjściowych hello hello w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="c7945-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="c7945-120">Tworzenie źródła instalacji hello tooadd bazy danych mongodb, **yum** plik repozytorium w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="c7945-121">Otwórz plik w repozytorium bazy danych MongoDB hello do edycji.</span><span class="sxs-lookup"><span data-stu-id="c7945-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="c7945-122">Dodaj następujące wiersze hello:</span><span class="sxs-lookup"><span data-stu-id="c7945-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="c7945-123">Instalowanie przy użyciu bazy danych MongoDB **yum** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="c7945-124">Domyślnie SELinux są wymuszane na obrazy CentOS, które uniemożliwiają dostęp do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c7945-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="c7945-125">Zainstaluj narzędzia do zarządzania zasadami i skonfigurować SELinux tooallow MongoDB toooperate na jego domyślny port TCP 27017 w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="c7945-126">Uruchom usługi MongoDB hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="c7945-127">Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta:</span><span class="sxs-lookup"><span data-stu-id="c7945-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="c7945-128">Teraz testu hello wystąpienie bazy danych MongoDB, dodając niektórych danych, a następnie wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="c7945-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="c7945-129">W razie potrzeby można skonfigurować bazy danych MongoDB toostart automatycznie podczas ponownego uruchomienia systemu:</span><span class="sxs-lookup"><span data-stu-id="c7945-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="c7945-130">Utwórz podstawowe wystąpienie bazy danych MongoDB na CentOS przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="c7945-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="c7945-131">Podstawowe wystąpienie bazy danych MongoDB można tworzyć na jednej maszyny Wirtualnej CentOS przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="c7945-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="c7945-132">Ten szablon używa hello rozszerzenia niestandardowego skryptu dla systemu Linux tooadd **yum** tooyour repozytorium nowo tworzone maszyny Wirtualnej CentOS, a następnie zainstalować bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c7945-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="c7945-133">[Podstawowe wystąpienie bazy danych MongoDB na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c7945-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="c7945-134">toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c7945-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="c7945-135">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c7945-136">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c7945-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c7945-137">Następnie Wdróż hello szablonu bazy danych MongoDB z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="c7945-138">Definiowanie własnych zasobów nazwy i rozmiar w razie potrzeby, takie jak w przypadku *newStorageAccountName*, *virtualNetworkName*, i *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="c7945-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="c7945-139">Zaloguj się na toohello maszyny Wirtualnej przy użyciu publicznego adresu DNS hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7945-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="c7945-140">Możesz wyświetlić hello publicznego adresu DNS z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="c7945-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="c7945-141">Tooyour SSH maszyny Wirtualnej przy użyciu własnego nazwy użytkownika i publicznego adresu DNS:</span><span class="sxs-lookup"><span data-stu-id="c7945-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="c7945-142">Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="c7945-143">Teraz hello wystąpieniem testu przez dodanie niektóre dane i wyszukiwanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7945-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="c7945-144">Tworzenie złożonych bazy danych MongoDB klastra podzielonej na CentOS przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="c7945-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="c7945-145">Można utworzyć klastra złożonych podzielonej bazy danych MongoDB, przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="c7945-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="c7945-146">Ten szablon jest zgodny hello [MongoDB podzielonej klastra najlepszych rozwiązań](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide nadmiarowości i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="c7945-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="c7945-147">Szablon Hello tworzy dwa niezależne, z trzema węzłami w każdego zestawu replik.</span><span class="sxs-lookup"><span data-stu-id="c7945-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="c7945-148">Jedna replika serwera konfiguracji ustawiony za pomocą trzech węzłów tworzona jest również, oraz dwa **mongos** router serwerów tooprovide spójności tooapplications z między odłamków hello.</span><span class="sxs-lookup"><span data-stu-id="c7945-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="c7945-149">[Bazy danych MongoDB dzielenia na fragmenty klastra na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c7945-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="c7945-150">Wdrażanie tego złożonych klastra podzielonej bazy danych MongoDB wymaga więcej niż 20 rdzenie, co jest typowe liczby rdzeni domyślne hello na region na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c7945-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="c7945-151">Otwórz tooincrease żądania pomocy technicznej platformy Azure z liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="c7945-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="c7945-152">toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c7945-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="c7945-153">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c7945-154">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c7945-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c7945-155">Następnie Wdróż hello szablonu bazy danych MongoDB z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="c7945-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="c7945-156">Definiowanie własnych zasobów nazwy i rozmiar w razie potrzeby, takie jak w przypadku *mongoAdminUsername*, *sizeOfDataDiskInGB*, i *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="c7945-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="c7945-157">To wdrożenie może przejąć toodeploy godzinę i skonfiguruj wszystkich wystąpień maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="c7945-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="c7945-158">Witaj `--no-wait` flaga jest wykorzystywana w końcu hello hello poprzedzających wiersza polecenia polecenie tooreturn kontroli toohello po wdrażania szablonu hello został zaakceptowany przez hello platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7945-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="c7945-159">Można wyświetlić stan wdrożenia hello z [Pokaż wdrożenia grupy az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="c7945-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="c7945-160">Witaj następujące widoki przykład Witaj stan hello *myMongoDBCluster* wdrożenia w hello *myResourceGroup* grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="c7945-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="c7945-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7945-161">Next steps</span></span>
<span data-ttu-id="c7945-162">W tym przykładzie połączenie wystąpienie bazy danych MongoDB toohello lokalnie z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7945-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="c7945-163">Jeśli chcesz, aby wystąpienie bazy danych MongoDB toohello tooconnect z innej maszyny Wirtualnej lub sieci, upewnij się, hello odpowiednie [reguł sieciowej grupy zabezpieczeń są tworzone](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c7945-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="c7945-164">Te przykłady wdrażania hello podstawowej bazy danych MongoDB środowiska do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="c7945-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="c7945-165">Zastosowanie opcji konfiguracji zabezpieczeń hello wymagane dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="c7945-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="c7945-166">Aby uzyskać więcej informacji, zobacz hello [docs zabezpieczeń bazy danych MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="c7945-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="c7945-167">Aby uzyskać więcej informacji na temat tworzenia za pomocą szablonów, zobacz hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7945-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="c7945-168">Szablony usługi Azure Resource Manager Hello Użyj hello niestandardowe rozszerzenie skryptu toodownload i wykonywanie skryptów na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c7945-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="c7945-169">Aby uzyskać więcej informacji, zobacz [hello Using Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="c7945-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

