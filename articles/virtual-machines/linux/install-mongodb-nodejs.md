---
title: "aaaInstall MongoDB na maszynie Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i skonfigurować na maszynie wirtualnej systemu Linux na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello bazy danych MongoDB."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="acaa7-103">Jak tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="acaa7-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="acaa7-104">[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="acaa7-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="acaa7-105">W tym artykule opisano sposób tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="acaa7-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="acaa7-106">Przykłady są wyświetlane szczegóły tego jak do:</span><span class="sxs-lookup"><span data-stu-id="acaa7-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="acaa7-107">Ręcznie zainstaluj i skonfiguruj podstawowe wystąpienie bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="acaa7-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="acaa7-108">Utwórz podstawowe wystąpienie bazy danych MongoDB przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acaa7-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="acaa7-109">Tworzenie złożonych bazy danych MongoDB ustawia podzielonej klaster z repliki przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acaa7-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="acaa7-110">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="acaa7-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="acaa7-111">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="acaa7-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="acaa7-112">Azure CLI 1.0 — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="acaa7-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="acaa7-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="acaa7-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="acaa7-114">Ręcznie zainstaluj i skonfiguruj bazy danych MongoDB na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="acaa7-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="acaa7-115">Bazy danych MongoDB [zawierają instrukcje instalacji](https://docs.mongodb.com/manual/administration/install-on-linux/) dla dystrybucjach systemu Linux, łącznie z Red Hat / CentOS, SUSE, Ubuntu i Debian.</span><span class="sxs-lookup"><span data-stu-id="acaa7-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="acaa7-116">Witaj poniższy przykład tworzy *CentOS* maszyny Wirtualnej przy użyciu klucza SSH przechowywane w *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="acaa7-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="acaa7-117">Witaj odpowiedzi monit o podanie nazwy konta magazynu, nazwa DNS i poświadczenia administratora:</span><span class="sxs-lookup"><span data-stu-id="acaa7-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="acaa7-118">Zaloguj się na toohello maszyny Wirtualnej przy użyciu hello publicznego adresu IP wyświetlane na końcu hello hello poprzedzających krok tworzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="acaa7-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="acaa7-119">Tworzenie źródła instalacji hello tooadd bazy danych mongodb, **yum** plik repozytorium w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="acaa7-120">Otwórz plik w repozytorium bazy danych MongoDB hello do edycji.</span><span class="sxs-lookup"><span data-stu-id="acaa7-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="acaa7-121">Dodaj następujące wiersze hello:</span><span class="sxs-lookup"><span data-stu-id="acaa7-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="acaa7-122">Instalowanie przy użyciu bazy danych MongoDB **yum** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="acaa7-123">Domyślnie SELinux są wymuszane na obrazy CentOS, które uniemożliwiają dostęp do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="acaa7-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="acaa7-124">Zainstaluj narzędzia do zarządzania zasadami i skonfigurować SELinux tooallow MongoDB toooperate na jego domyślny port TCP 27017 w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="acaa7-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="acaa7-125">Uruchom usługi MongoDB hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="acaa7-126">Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta:</span><span class="sxs-lookup"><span data-stu-id="acaa7-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="acaa7-127">Teraz testu hello wystąpienie bazy danych MongoDB, dodając niektórych danych, a następnie wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="acaa7-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="acaa7-128">W razie potrzeby można skonfigurować bazy danych MongoDB toostart automatycznie podczas ponownego uruchomienia systemu:</span><span class="sxs-lookup"><span data-stu-id="acaa7-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="acaa7-129">Utwórz podstawowe wystąpienie bazy danych MongoDB na CentOS przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="acaa7-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="acaa7-130">Podstawowe wystąpienie bazy danych MongoDB można tworzyć na jednej maszyny Wirtualnej CentOS przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="acaa7-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="acaa7-131">Ten szablon używa hello rozszerzenia niestandardowego skryptu dla systemu Linux tooadd `yum` tooyour repozytorium nowo tworzone maszyny Wirtualnej CentOS, a następnie zainstalować bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="acaa7-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="acaa7-132">[Podstawowe wystąpienie bazy danych MongoDB na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="acaa7-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="acaa7-133">Witaj poniższy przykład tworzy grupę zasobów o nazwie hello `myResourceGroup` w hello `eastus` regionu.</span><span class="sxs-lookup"><span data-stu-id="acaa7-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="acaa7-134">Wprowadź własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="acaa7-135">Hello Azure CLI powrót tooa wiersza w ciągu kilku sekund tworzenia hello wdrożenia, ale hello instalacji i konfiguracji zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="acaa7-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="acaa7-136">Sprawdź stan hello hello wdrożenia z `azure group deployment show myResourceGroup`, odpowiednio wprowadzania hello nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="acaa7-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="acaa7-137">Poczekaj na powitania **ProvisioningState** pokazuje *zakończyło się pomyślnie* przed w trakcie toohello tooSSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="acaa7-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="acaa7-138">Po zakończeniu wdrażania hello jest Ukończ, toohello SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="acaa7-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="acaa7-139">Uzyskaj adres IP hello maszyny wirtualnej przy użyciu hello `azure vm show` jak hello poniższy przykład polecenia:</span><span class="sxs-lookup"><span data-stu-id="acaa7-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="acaa7-140">Zbliża się koniec hello hello dane wyjściowe zostanie wyświetlony hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="acaa7-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="acaa7-141">Tooyour SSH maszyny Wirtualnej z adresem IP hello maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="acaa7-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="acaa7-142">Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="acaa7-143">Teraz hello wystąpieniem testu przez dodanie niektóre dane i wyszukiwanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="acaa7-144">Tworzenie złożonych bazy danych MongoDB klastra podzielonej na CentOS przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="acaa7-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="acaa7-145">Można utworzyć klastra złożonych podzielonej bazy danych MongoDB, przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="acaa7-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="acaa7-146">Ten szablon jest zgodny hello [MongoDB podzielonej klastra najlepszych rozwiązań](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide nadmiarowości i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="acaa7-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="acaa7-147">Szablon Hello tworzy dwa niezależne, z trzema węzłami w każdego zestawu replik.</span><span class="sxs-lookup"><span data-stu-id="acaa7-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="acaa7-148">Jedna replika serwera konfiguracji ustawiony za pomocą trzech węzłów tworzona jest również, oraz dwa **mongos** router serwerów tooprovide spójności tooapplications z między odłamków hello.</span><span class="sxs-lookup"><span data-stu-id="acaa7-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="acaa7-149">[Bazy danych MongoDB dzielenia na fragmenty klastra na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="acaa7-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="acaa7-150">Wdrażanie tego złożonych klastra podzielonej bazy danych MongoDB wymaga więcej niż 20 rdzenie, co jest typowe liczby rdzeni domyślne hello na region na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="acaa7-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="acaa7-151">Otwórz tooincrease żądania pomocy technicznej platformy Azure z liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="acaa7-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="acaa7-152">Witaj poniższy przykład tworzy grupę zasobów o nazwie hello *myResourceGroup* w hello *eastus* regionu.</span><span class="sxs-lookup"><span data-stu-id="acaa7-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="acaa7-153">Wprowadź własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="acaa7-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="acaa7-154">Hello Azure CLI powrót tooa wiersza w ciągu kilku sekund tworzenia hello wdrożenia, ale hello instalacji i konfiguracji może potrwać ponad godzinę toocomplete.</span><span class="sxs-lookup"><span data-stu-id="acaa7-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="acaa7-155">Sprawdź stan hello hello wdrożenia z `azure group deployment show myResourceGroup`, odpowiednio dostosowywania hello nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="acaa7-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="acaa7-156">Poczekaj na powitania **ProvisioningState** pokazuje *zakończyło się pomyślnie* przed połączeniem toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="acaa7-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="acaa7-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="acaa7-157">Next steps</span></span>
<span data-ttu-id="acaa7-158">W tym przykładzie połączenie wystąpienie bazy danych MongoDB toohello lokalnie z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="acaa7-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="acaa7-159">Jeśli chcesz, aby wystąpienie bazy danych MongoDB toohello tooconnect z innej maszyny Wirtualnej lub sieci, upewnij się, hello odpowiednie [reguł sieciowej grupy zabezpieczeń są tworzone](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="acaa7-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="acaa7-160">Aby uzyskać więcej informacji na temat tworzenia za pomocą szablonów, zobacz hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="acaa7-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="acaa7-161">Szablony usługi Azure Resource Manager Hello Użyj hello niestandardowe rozszerzenie skryptu toodownload i wykonywanie skryptów na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="acaa7-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="acaa7-162">Aby uzyskać więcej informacji, zobacz [hello Using Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="acaa7-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

