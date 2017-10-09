---
title: aaaUsing toocustomize init chmury maszyny Wirtualnej systemu Linux, podczas tworzenia na platformie Azure | Dokumentacja firmy Microsoft
description: Jak toouse toocustomize init chmury a Linux VM podczas tworzenia z hello Azure CLI w wersji 1.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Użyj toocustomize init chmury maszyny Wirtualnej systemu Linux podczas tworzenia z hello Azure CLI w wersji 1.0
W tym artykule przedstawiono sposób toomake tooset skryptu init chmury hello hostname zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników.  skrypty chmurze init Hello są wywoływane podczas hello tworzenie maszyny Wirtualnej za pomocą wiersza polecenia platformy Azure.  wymaga artykułu Hello:

* konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));
* Witaj [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) logowania `azure login`.
* Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="quick-commands"></a>Szybkie polecenia
Utwórz skrypt init.txt chmury, który ustawia hello hostname, wszystkie pakiety aktualizacji i dodaje tooLinux użytkownika sudo.

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
Tworzenie maszyn wirtualnych do toolaunch grupy zasobów.

```azurecli
azure group create myResourceGroup westus
```

Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
### <a name="introduction"></a>Wprowadzenie
Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb. [Init chmury](https://cloudinit.readthedocs.org) jest tooinject standardowy sposób skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux jest uruchamiany dla powitania po raz pierwszy.

Na platformie Azure, istnieją trzy różne sposoby toomake zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.

* Wstaw skrypty przy użyciu inicjowania chmury.
* Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Szablonu platformy Azure przy użyciu inicjowania chmury.
* Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

skrypty tooinject w dowolnym momencie po rozruchu:

* SSH toorun bezpośrednio poleceń
* Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively lub szablonu platformy Azure
* Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.

> [!NOTE]
> : Rozszerzenia VMAccess wykonuje skrypt główny w hello takie same jak przy użyciu protokołu SSH może.  Jednak używanie hello rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:
| Alias | Wydawca | Oferta | SKU | Wersja | init chmury |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |najnowsza |Brak |
| CoreOS |CoreOS |CoreOS |Stable |najnowsza |Tak |
| Debian |credativ |Debian |8 |najnowsza |Brak |
| openSUSE |SUSE |openSUSE |13.2 |najnowsza |Brak |
| RHEL |Redhat |RHEL |7.2 |najnowsza |Brak |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |najnowsza |Tak |

Firma Microsoft jest praca z naszych partnerów tooget chmury inicjowania uwzględnione pracy w obrazach hello udostępniają one tooAzure.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Dodawanie utworzenie init chmury skryptu toohello maszyny Wirtualnej z hello wiersza polecenia platformy Azure
toolaunch skryptu chmury init, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury hello przy użyciu interfejsu wiersza polecenia Azure hello `--custom-data` przełącznika.

Tworzenie maszyn wirtualnych do toolaunch grupy zasobów.

```azurecli
azure group create myResourceGroup westus
```

Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Tworzenie chmury init skryptu tooset hello nazwa hosta maszyny wirtualnej systemu Linux
Jedną z najważniejszych ustawień żadnej maszyny Wirtualnej systemu Linux i hello najprostszym byłoby hello nazwy hosta. Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Podczas hello wstępnego uruchamiania hello maszyny Wirtualnej, ten skrypt init chmury ustawia hello hostname zbyt`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Logowania i sprawdź nazwę hosta hello hello nowej maszyny Wirtualnej.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Tworzenie chmury init tooupdate skryptu systemu Linux
Dla bezpieczeństwa ma tooupdate Twojej maszyny Wirtualnej systemu Ubuntu przy pierwszym hello.  Przy użyciu chmury init możemy, z hello Wykonaj skrypt, w zależności od hello dystrybucja systemu Linux, którego używasz.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` dla hello Debian rodziny
```sh
#cloud-config
apt_upgrade: true
```

Po uruchomieniu systemu Linux, wszystkich pakietów hello zainstalowane są aktualizowane za pośrednictwem `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

Logowania i sprawdź wszystkie pakiety zostały zaktualizowane.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Tworzenie tooadd skryptu init chmury tooLinux użytkownika
Jeden z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest tooadd użytkownika dla siebie lub przy użyciu tooavoid `root`. SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane toohello `~/.ssh/authorized_keys` plików za pomocą tego skryptu init chmury.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Po uruchomieniu systemu Linux, wszyscy użytkownicy hello wymienione są utworzone i dodać toohello sudo grupy.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

Logowania i weryfikacji hello nowo utworzonego użytkownika.

```bash
ssh myVM
cat /etc/group
```

Dane wyjściowe

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Następne kroki
Init chmurze staje się jeden toomodify standardowy sposób przy rozruchu maszyny Wirtualnej systemu Linux. Platforma Azure ma rozszerzenia maszyny Wirtualnej, które pozwalają toomodify Twojego LinuxVM przy rozruchu lub jest uruchomiona. Na przykład można użyć hello Azure VMAccessExtension tooreset SSH lub informacje o użytkowniku hello maszyna wirtualna jest uruchomiona. Z inicjowaniem chmury będzie potrzebny hasła hello tooreset ponowne uruchomienie komputera.

[Temat funkcji i rozszerzeń maszyny wirtualnej](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

