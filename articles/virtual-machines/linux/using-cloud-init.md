---
title: aaaUse toocustomize init chmury maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: Jak toouse toocustomize init chmury a Linux VM podczas tworzenia z hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Użyj podczas tworzenia chmury init toocustomize Maszynę wirtualną systemu Linux
W tym artykule przedstawiono sposób toomake tooset skryptu init chmury hello hostname zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników z hello Azure CLI 2.0. skrypty chmurze init Hello są wywoływane po utworzeniu maszyny wirtualnej (VM) z wiersza polecenia platformy Azure. Na pełniejsze omówienie na instalowanie aplikacji, zapisywanie plików konfiguracji i wstrzyknięcie kluczy z usługi Key Vault, zobacz [w tym samouczku](tutorial-automate-vm-deployment.md). Można również wykonać te kroki hello [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Szybkie polecenia
Utwórz skrypt init.txt chmury, który ustawia hello hostname, wszystkie pakiety aktualizacji i dodaje tooLinux użytkownika sudo.

```yaml
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

Tworzenie maszyn wirtualnych do o toolaunch grupy zasobów [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy hello grupy zasobów o nazwie *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu z hello `--custom-data` parametru.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb. [Init chmury](https://cloudinit.readthedocs.org) jest tooinject standardowy sposób skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux jest uruchamiany dla powitania po raz pierwszy.

Na platformie Azure, istnieją na kilka różnych sposobów toomake zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.

* Wstaw skrypty przy użyciu inicjowania chmury.
* Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md).
* Szablonu platformy Azure przy użyciu inicjowania chmury.
* Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md).

skrypty tooinject w dowolnym momencie po rozruchu:

* SSH toorun bezpośrednio poleceń
* Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md), imperatively lub szablonu platformy Azure
* Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.

> [!NOTE]
> Rozszerzenia VMAccess wykonuje skrypt główny w hello takie same jak przy użyciu protokołu SSH może. Jednak używanie hello rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:
| Alias | Wydawca | Oferta | SKU | Wersja | init chmury |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |najnowsza |Brak |
| CoreOS |CoreOS |CoreOS |Stable |najnowsza |Tak |
| Debian |credativ |Debian |8 |najnowsza |Brak |
| openSUSE |SUSE |openSUSE |13.2 |najnowsza |Brak |
| RHEL |Redhat |RHEL |7.2 |najnowsza |Brak |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |najnowsza |Tak |

Możemy pracy z naszych partnerów tooget chmury inicjowania uwzględnione i Praca w obrazach hello udostępniają one tooAzure.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Dodaj utworzenie init chmury skryptu toohello maszyny Wirtualnej z hello wiersza polecenia platformy Azure
toolaunch skryptu chmury init, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury hello przy użyciu interfejsu wiersza polecenia Azure hello `--custom-data` przełącznika.

Tworzenie maszyn wirtualnych do o toolaunch grupy zasobów [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy hello grupy zasobów o nazwie *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Utwórz nazwę chmury init skryptu tooset hello hosta maszyny wirtualnej systemu Linux
Jedną z najważniejszych ustawień żadnej maszyny Wirtualnej systemu Linux i hello najprostszym byłoby hello nazwy hosta. Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Podczas hello wstępnego uruchamiania hello maszyny Wirtualnej, ten skrypt init chmury ustawia hello hostname zbyt*myservername*. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Logowania i sprawdź nazwę hosta hello hello nowej maszyny Wirtualnej.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Utwórz skrypt init chmury
Dla bezpieczeństwa ma tooupdate Twojej maszyny Wirtualnej systemu Ubuntu przy pierwszym hello. Przy użyciu chmury init możemy, z hello Wykonaj skrypt, w zależności od hello dystrybucja systemu Linux, którego używasz.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` dla hello Debian rodziny
```yaml
#cloud-config
apt_upgrade: true
```

Po uruchomieniu systemu Linux, wszystkich pakietów hello zainstalowane są aktualizowane za pośrednictwem **stanie get**. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Utwórz tooadd skryptu init chmury tooLinux użytkownika
Jeden z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest tooadd użytkownika dla siebie lub przy użyciu tooavoid *głównego*. SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane toohello *~/.ssh/authorized_keys* plików za pomocą tego skryptu init chmury.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Po uruchomieniu systemu Linux, wszyscy użytkownicy hello wymienione są utworzone i dodać toohello sudo grupy. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

[Temat funkcji i rozszerzeń maszyny wirtualnej](extensions-features.md)

[Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess](using-vmaccess-extension.md)
