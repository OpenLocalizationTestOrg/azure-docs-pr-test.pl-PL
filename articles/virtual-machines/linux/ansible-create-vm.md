---
title: aaaUse Ansible toocreate podstawowej maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Ansible toocreate i zarządzanie nimi podstawowej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Tworzenie podstawowej maszyny wirtualnej na platformie Azure z Ansible
Ansible pozwala tooautomate hello wdrażania i konfigurowania zasobów w danym środowisku. Można używać Ansible toomanage maszyn wirtualnych (VM) na platformie Azure, hello takie same jak w przypadku innych zasobów. W tym artykule opisano sposób toocreate podstawowej maszyny Wirtualnej z Ansible. Możesz też dowiedzieć się, jak za[utworzyć pełne środowisko maszyny Wirtualnej z Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Wymagania wstępne
toomanage Azure zasoby z Ansible, należy po hello:

- Ansible i hello Azure Python SDK modułów zainstalowanych w systemie hosta.
    - Zainstaluj na Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), i [SLES 12.2 z dodatkiem SP2](ansible-install-configure.md#sles-122-sp2)
- Poświadczenia platformy Azure i toouse Ansible skonfigurowane je.
    - [Utwórz poświadczenia platformy Azure i skonfigurować Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. 
    - Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). Można również użyć [powłoki chmury](/azure/cloud-shell/quickstart) z przeglądarki.


## <a name="create-supporting-azure-resources"></a>Tworzenie obsługi zasobów platformy Azure
W tym przykładzie tworzymy elementu runbook, który wdraża maszynę Wirtualną do istniejącej infrastruktury. Najpierw należy utworzyć grupy zasobów z [Tworzenie grupy az](/cli/azure/vm#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

Tworzenie sieci wirtualnej dla maszyny Wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Tworzenie i uruchamianie podręcznikowym Ansible
Utwórz podręcznikowym Ansible o nazwie **azure_create_vm.yml** i Wklej powitania po zawartości. W tym przykładzie tworzy jednej maszyny Wirtualnej i konfiguruje poświadczenia SSH. Wprowadź własne dane klucza publicznego w hello *key_data* Sparuj w następujący sposób:

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Witaj toocreate maszyny Wirtualnej z Ansible, uruchom podręcznikowym hello w następujący sposób:

```bash
ansible-playbook azure_create_vm.yml
```

Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład pokazujący hello, że maszyna wirtualna została pomyślnie utworzona:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Następne kroki
To przykładowe polecenie tworzy Maszynę wirtualną w istniejącej grupie zasobów i z siecią wirtualną już wdrożone. W przykładzie bardziej szczegółowe na temat toouse Ansible toocreate obsługi zasobów takich jak sieć wirtualną i reguł sieciowej grupy zabezpieczeń, zobacz [utworzyć pełne środowisko maszyny Wirtualnej z Ansible](ansible-create-complete-vm.md).
