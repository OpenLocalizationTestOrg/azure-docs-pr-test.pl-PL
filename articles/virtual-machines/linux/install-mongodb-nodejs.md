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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Jak tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI w wersji 1.0
[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL. W tym artykule opisano sposób tooinstall i skonfigurować bazy danych MongoDB na Maszynę wirtualną systemu Linux na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello. Przykłady są wyświetlane szczegóły tego jak do:

* [Ręcznie zainstaluj i skonfiguruj podstawowe wystąpienie bazy danych MongoDB](#manually-install-and-configure-mongodb-on-a-vm)
* [Utwórz podstawowe wystąpienie bazy danych MongoDB przy użyciu szablonu usługi Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Tworzenie złożonych bazy danych MongoDB ustawia podzielonej klaster z repliki przy użyciu szablonu usługi Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- Azure CLI 1.0 — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Ręcznie zainstaluj i skonfiguruj bazy danych MongoDB na maszynie Wirtualnej
Bazy danych MongoDB [zawierają instrukcje instalacji](https://docs.mongodb.com/manual/administration/install-on-linux/) dla dystrybucjach systemu Linux, łącznie z Red Hat / CentOS, SUSE, Ubuntu i Debian. Witaj poniższy przykład tworzy *CentOS* maszyny Wirtualnej przy użyciu klucza SSH przechowywane w *~/.ssh/id_rsa.pub*. Witaj odpowiedzi monit o podanie nazwy konta magazynu, nazwa DNS i poświadczenia administratora:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Zaloguj się na toohello maszyny Wirtualnej przy użyciu hello publicznego adresu IP wyświetlane na końcu hello hello poprzedzających krok tworzenia maszyny Wirtualnej:

```bash
ssh azureuser@40.78.23.145
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

Domyślnie SELinux są wymuszane na obrazy CentOS, które uniemożliwiają dostęp do bazy danych MongoDB. Zainstaluj narzędzia do zarządzania zasadami i skonfigurować SELinux tooallow MongoDB toooperate na jego domyślny port TCP 27017 w następujący sposób. 

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
Podstawowe wystąpienie bazy danych MongoDB można tworzyć na jednej maszyny Wirtualnej CentOS przy użyciu powitania po szablonie Szybki Start Azure z usługi GitHub. Ten szablon używa hello rozszerzenia niestandardowego skryptu dla systemu Linux tooadd `yum` tooyour repozytorium nowo tworzone maszyny Wirtualnej CentOS, a następnie zainstalować bazy danych MongoDB.

* [Podstawowe wystąpienie bazy danych MongoDB na CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Witaj poniższy przykład tworzy grupę zasobów o nazwie hello `myResourceGroup` w hello `eastus` regionu. Wprowadź własne wartości w następujący sposób:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI powrót tooa wiersza w ciągu kilku sekund tworzenia hello wdrożenia, ale hello instalacji i konfiguracji zajmuje kilka minut toocomplete. Sprawdź stan hello hello wdrożenia z `azure group deployment show myResourceGroup`, odpowiednio wprowadzania hello nazwę grupy zasobów. Poczekaj na powitania **ProvisioningState** pokazuje *zakończyło się pomyślnie* przed w trakcie toohello tooSSH maszyny Wirtualnej.

Po zakończeniu wdrażania hello jest Ukończ, toohello SSH maszyny Wirtualnej. Uzyskaj adres IP hello maszyny wirtualnej przy użyciu hello `azure vm show` jak hello poniższy przykład polecenia:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Zbliża się koniec hello hello dane wyjściowe zostanie wyświetlony hello publicznego adresu IP. Tooyour SSH maszyny Wirtualnej z adresem IP hello maszyny wirtualnej:

```bash
ssh azureuser@138.91.149.74
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

Witaj poniższy przykład tworzy grupę zasobów o nazwie hello *myResourceGroup* w hello *eastus* regionu. Wprowadź własne wartości w następujący sposób:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI powrót tooa wiersza w ciągu kilku sekund tworzenia hello wdrożenia, ale hello instalacji i konfiguracji może potrwać ponad godzinę toocomplete. Sprawdź stan hello hello wdrożenia z `azure group deployment show myResourceGroup`, odpowiednio dostosowywania hello nazwę grupy zasobów. Poczekaj na powitania **ProvisioningState** pokazuje *zakończyło się pomyślnie* przed połączeniem toohello maszyn wirtualnych.


## <a name="next-steps"></a>Następne kroki
W tym przykładzie połączenie wystąpienie bazy danych MongoDB toohello lokalnie z hello maszyny Wirtualnej. Jeśli chcesz, aby wystąpienie bazy danych MongoDB toohello tooconnect z innej maszyny Wirtualnej lub sieci, upewnij się, hello odpowiednie [reguł sieciowej grupy zabezpieczeń są tworzone](nsg-quickstart.md).

Aby uzyskać więcej informacji na temat tworzenia za pomocą szablonów, zobacz hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Szablony usługi Azure Resource Manager Hello Użyj hello niestandardowe rozszerzenie skryptu toodownload i wykonywanie skryptów na maszyny wirtualne. Aby uzyskać więcej informacji, zobacz [hello Using Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux](extensions-customscript.md).

