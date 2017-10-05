---
title: "Init chmury umożliwia dostosowywanie Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
description: "Dostosowywanie maszyny Wirtualnej systemu Linux podczas tworzenia 2.0 interfejsu wiersza polecenia platformy Azure przy użyciu init chmury"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a>Umożliwia dostosowanie Maszynę wirtualną systemu Linux podczas tworzenia init chmury
W tym artykule przedstawiono sposób wprowadzania skryptu init chmury ustawienie Nazwa hosta, zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników 2.0 interfejsu wiersza polecenia platformy Azure. Skrypty chmurze init są wywoływane po utworzeniu maszyny wirtualnej (VM) z wiersza polecenia platformy Azure. Na pełniejsze omówienie na instalowanie aplikacji, zapisywanie plików konfiguracji i wstrzyknięcie kluczy z usługi Key Vault, zobacz [w tym samouczku](tutorial-automate-vm-deployment.md). Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Szybkie polecenia
Utwórz skrypt init.txt chmury, który ustawia nazwę hosta, wszystkie pakiety aktualizacji i dodaje użytkownika sudo do systemu Linux.

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

Utwórz grupę zasobów do uruchamiania maszyn wirtualnych do o [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu z `--custom-data` parametru.

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
Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb. [Init chmury](https://cloudinit.readthedocs.org) jest standardowym sposobem wstrzyknąć skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux, jak jest uruchamiany dla po raz pierwszy.

Na platformie Azure, są na kilka różnych sposobów, aby wprowadzić zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.

* Wstaw skrypty przy użyciu inicjowania chmury.
* Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md).
* Szablonu platformy Azure przy użyciu inicjowania chmury.
* Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md).

Do dodania skryptów w dowolnym momencie po rozruchu:

* SSH do uruchamiania poleceń, bezpośrednio
* Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md), imperatively lub szablonu platformy Azure
* Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.

> [!NOTE]
> Rozszerzenia VMAccess wykonuje skryptu, tak jak w głównym w taki sam sposób, przy użyciu protokołu SSH. Jednak przy użyciu rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:
| Alias | Wydawca | Oferta | SKU | Wersja | init chmury |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |najnowsza |Brak |
| CoreOS |CoreOS |CoreOS |Stable |najnowsza |Tak |
| Debian |credativ |Debian |8 |najnowsza |Brak |
| openSUSE |SUSE |openSUSE |13.2 |najnowsza |Brak |
| RHEL |Redhat |RHEL |7.2 |najnowsza |Brak |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |najnowsza |Tak |

Pracujemy nad z naszych partnerów uzyskanie init chmury uwzględnione i Praca w obrazach, zapewniające na platformie Azure.

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a>Skrypt init chmury do tworzenia maszyny Wirtualnej z wiersza polecenia platformy Azure
Aby uruchomić skrypt init chmury, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury przy użyciu interfejsu wiersza polecenia Azure `--custom-data` przełącznika.

Utwórz grupę zasobów do uruchamiania maszyn wirtualnych do o [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a>Utwórz skrypt init chmurze hostname maszyny wirtualnej systemu Linux
Jedno z ustawień najprostszym i najważniejszych żadnej maszyny Wirtualnej systemu Linux jest nazwą hosta. Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Podczas wstępnego uruchamiania maszyny Wirtualnej, ten skrypt init chmury ustawia nazwę hosta *myservername*. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Logowania i sprawdź nazwę hosta nowej maszyny Wirtualnej.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Utwórz skrypt init chmury
Dla bezpieczeństwa ma maszyny Wirtualnej systemu Ubuntu aktualizacji po pierwszym uruchomieniu komputera. Przy użyciu chmury init robimy można przy użyciu skryptu wykonaj, w zależności od używanych dystrybucji systemu Linux.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a>Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` Debian rodziny
```yaml
#cloud-config
apt_upgrade: true
```

Po uruchomieniu systemu Linux, wszystkie zainstalowane pakiety są aktualizowane za pośrednictwem **stanie get**. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.

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
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a>Utwórz skrypt init chmury, aby dodać użytkownika do systemu Linux
Jedno z pierwszym zadań na nowej maszyny Wirtualnej z systemem Linux jest dodać użytkownika dla siebie lub unikać *głównego*. SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane do *~/.ssh/authorized_keys* plików za pomocą tego skryptu init chmury.

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

Po uruchomieniu systemu Linux, wyświetlani użytkownicy są tworzone i dodawane do grupy sudo. Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Logowania i Sprawdź nowo utworzonego użytkownika.

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
Init chmurze staje się coraz standardowy sposób zmodyfikować maszyny Wirtualnej systemu Linux na rozruchu. Platforma Azure ma rozszerzenia maszyny Wirtualnej, które umożliwiają modyfikowanie użytkownika LinuxVM przy rozruchu lub jest uruchomiona. Na przykład można użyć Azure VMAccessExtension można zresetować informacje o użytkowniku lub SSH uruchomionej maszyny Wirtualnej. Z inicjowaniem chmury może być konieczne ponowne uruchomienie w celu zresetowania hasła.

[Temat funkcji i rozszerzeń maszyny wirtualnej](extensions-features.md)

[Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux platformy Azure przy użyciu rozszerzenia VMAccess](using-vmaccess-extension.md)