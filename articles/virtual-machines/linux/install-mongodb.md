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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Jak tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux
[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL. W tym artykule opisano sposób tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](install-mongodb-nodejs.md). Przykłady są wyświetlane szczegóły tego jak do:

* [Ręcznie zainstaluj i skonfiguruj podstawowe wystąpienie bazy danych MongoDB](#manually-install-and-configure-mongodb-on-a-vm)
* [Utwórz podstawowe wystąpienie bazy danych MongoDB przy użyciu szablonu usługi Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Tworzenie złożonych bazy danych MongoDB ustawia podzielonej klaster z repliki przy użyciu szablonu usługi Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Ręcznie zainstaluj i skonfiguruj bazy danych MongoDB na maszynie Wirtualnej
Bazy danych MongoDB [zawierają instrukcje instalacji](https://docs.mongodb.com/manual/administration/install-on-linux/) dla dystrybucjach systemu Linux, łącznie z Red Hat / CentOS, SUSE, Ubuntu i Debian. Witaj poniższy przykład tworzy *CentOS* maszyny Wirtualnej. toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z użytkownikiem o nazwie *azureuser* przy użyciu uwierzytelniania klucza publicznego SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Toohello SSH maszyny Wirtualnej przy użyciu własnej nazwy użytkownika i hello `publicIpAddress` wymienionych w danych wyjściowych hello hello w poprzednim kroku:

```bash
ssh azureuser@<publicIpAddress>
```

Tworzenie źródła instalacji hello tooadd bazy danych mongodb, **yum** plik repozytorium w następujący sposób:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Otwórz plik w repozytorium bazy danych MongoDB hello do edycji. Dodaj następujące wiersze hello:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Instalowanie przy użyciu bazy danych MongoDB **yum** w następujący sposób:

```bash
sudo yum install -y mongodb-org
```

Domyślnie SELinux są wymuszane na obrazy CentOS, które uniemożliwiają dostęp do bazy danych MongoDB. Zainstaluj narzędzia do zarządzania zasadami i skonfigurować SELinux tooallow MongoDB toooperate na jego domyślny port TCP 27017 w następujący sposób:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Uruchom usługi MongoDB hello w następujący sposób:

```bash
sudo service mongod start
```

Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta:

```bash
mongo
```

Teraz testu hello wystąpienie bazy danych MongoDB, dodając niektórych danych, a następnie wyszukiwania:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

W razie potrzeby można skonfigurować bazy danych MongoDB toostart automatycznie podczas ponownego uruchomienia systemu:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Utwórz podstawowe wystąpienie bazy danych MongoDB na CentOS przy użyciu szablonu
Podstawowe wystąpienie bazy danych MongoDB można tworzyć na jednej maszyny Wirtualnej CentOS przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub. Ten szablon używa hello rozszerzenia niestandardowego skryptu dla systemu Linux tooadd **yum** tooyour repozytorium nowo tworzone maszyny Wirtualnej CentOS, a następnie zainstalować bazy danych MongoDB.

* [Podstawowe wystąpienie bazy danych MongoDB na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

Następnie Wdróż hello szablonu bazy danych MongoDB z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create). Definiowanie własnych zasobów nazwy i rozmiar w razie potrzeby, takie jak w przypadku *newStorageAccountName*, *virtualNetworkName*, i *vmSize*:

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

Zaloguj się na toohello maszyny Wirtualnej przy użyciu publicznego adresu DNS hello maszyny wirtualnej. Możesz wyświetlić hello publicznego adresu DNS z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

Tooyour SSH maszyny Wirtualnej przy użyciu własnego nazwy użytkownika i publicznego adresu DNS:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Sprawdź hello instalacji bazy danych MongoDB, nawiązując połączenie za pomocą lokalne powitania `mongo` klienta w następujący sposób:

```bash
mongo
```

Teraz hello wystąpieniem testu przez dodanie niektóre dane i wyszukiwanie w następujący sposób:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Tworzenie złożonych bazy danych MongoDB klastra podzielonej na CentOS przy użyciu szablonu
Można utworzyć klastra złożonych podzielonej bazy danych MongoDB, przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub. Ten szablon jest zgodny hello [MongoDB podzielonej klastra najlepszych rozwiązań](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide nadmiarowości i wysokiej dostępności. Szablon Hello tworzy dwa niezależne, z trzema węzłami w każdego zestawu replik. Jedna replika serwera konfiguracji ustawiony za pomocą trzech węzłów tworzona jest również, oraz dwa **mongos** router serwerów tooprovide spójności tooapplications z między odłamków hello.

* [Bazy danych MongoDB dzielenia na fragmenty klastra na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Wdrażanie tego złożonych klastra podzielonej bazy danych MongoDB wymaga więcej niż 20 rdzenie, co jest typowe liczby rdzeni domyślne hello na region na subskrypcję. Otwórz tooincrease żądania pomocy technicznej platformy Azure z liczby rdzeni.

toocreate tego środowiska, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

Następnie Wdróż hello szablonu bazy danych MongoDB z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create). Definiowanie własnych zasobów nazwy i rozmiar w razie potrzeby, takie jak w przypadku *mongoAdminUsername*, *sizeOfDataDiskInGB*, i *configNodeVmSize*:

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

To wdrożenie może przejąć toodeploy godzinę i skonfiguruj wszystkich wystąpień maszyn wirtualnych hello. Witaj `--no-wait` flaga jest wykorzystywana w końcu hello hello poprzedzających wiersza polecenia polecenie tooreturn kontroli toohello po wdrażania szablonu hello został zaakceptowany przez hello platformy Azure. Można wyświetlić stan wdrożenia hello z [Pokaż wdrożenia grupy az](/cli/azure/group/deployment#show). Witaj następujące widoki przykład Witaj stan hello *myMongoDBCluster* wdrożenia w hello *myResourceGroup* grupy zasobów:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Następne kroki
W tym przykładzie połączenie wystąpienie bazy danych MongoDB toohello lokalnie z hello maszyny Wirtualnej. Jeśli chcesz, aby wystąpienie bazy danych MongoDB toohello tooconnect z innej maszyny Wirtualnej lub sieci, upewnij się, hello odpowiednie [reguł sieciowej grupy zabezpieczeń są tworzone](nsg-quickstart.md).

Te przykłady wdrażania hello podstawowej bazy danych MongoDB środowiska do celów programistycznych. Zastosowanie opcji konfiguracji zabezpieczeń hello wymagane dla danego środowiska. Aby uzyskać więcej informacji, zobacz hello [docs zabezpieczeń bazy danych MongoDB](https://docs.mongodb.com/manual/security/).

Aby uzyskać więcej informacji na temat tworzenia za pomocą szablonów, zobacz hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Szablony usługi Azure Resource Manager Hello Użyj hello niestandardowe rozszerzenie skryptu toodownload i wykonywanie skryptów na maszyny wirtualne. Aby uzyskać więcej informacji, zobacz [hello Using Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux](extensions-customscript.md).

