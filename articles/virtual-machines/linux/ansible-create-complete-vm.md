---
title: "aaaUse Ansible toocreate pełną maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Ansible toocreate i zarządzanie nimi pełną środowiska maszyny wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Utwórz pełną środowiska maszyny wirtualnej systemu Linux na platformie Azure z Ansible
Ansible pozwala tooautomate hello wdrażania i konfigurowania zasobów w danym środowisku. Można używać Ansible toomanage maszyn wirtualnych (VM) na platformie Azure, hello takie same jak w przypadku innych zasobów. W tym artykule opisano sposób toocreate kompletne środowisko systemu Linux i pomocnicze zasoby z Ansible. Możesz też dowiedzieć się, jak za[Tworzenie podstawowej maszyny Wirtualnej z Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Wymagania wstępne
toomanage Azure zasoby z Ansible, należy po hello:

- Ansible i hello Azure Python SDK modułów zainstalowanych w systemie hosta.
    - Zainstaluj na Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), i [SLES 12.2 z dodatkiem SP2](ansible-install-configure.md#sles-122-sp2)
- Poświadczenia platformy Azure i toouse Ansible skonfigurowane je.
    - [Utwórz poświadczenia platformy Azure i skonfigurować Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. 
    - Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). Można również użyć [powłoki chmury](/azure/cloud-shell/quickstart) z przeglądarki.


## <a name="create-virtual-network"></a>Tworzenie sieci wirtualnej
Witaj następujące części podręcznika dotyczącego Ansible tworzy sieć wirtualną o nazwie *myVnet* w hello *10.0.0.0/16* przestrzeni adresów:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd podsieci powitania po sekcji tworzy podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Utwórz publiczny adres IP
tooaccess zasobów między hello Internet, Utwórz i przypisz publicznego tooyour adres IP maszyny Wirtualnej. Witaj następujące części podręcznika dotyczącego Ansible tworzy publiczny adres IP o nazwie *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Utwórz grupę zabezpieczeń sieci
Grupy zabezpieczeń sieci sterowania przepływem hello ruchu sieciowego do i z maszyną Wirtualną. Witaj następujące części podręcznika dotyczącego Ansible tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* i definiuje reguły tooallow SSH ruch na porcie TCP 22:

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a>Tworzenie wirtualnej karty sieciowej
Karty interfejsu sieci wirtualnej (NIC) nawiązuje połączenie z tooa maszyna wirtualna danej sieci wirtualnej, publiczny adres IP i grupy zabezpieczeń sieci. Witaj następujące części podręcznika dotyczącego Ansible tworzy wirtualną kartę Sieciową o nazwie *myNIC* połączone toohello wirtualnego zasoby sieciowe zostały utworzone:

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
Ostatnim krokiem Hello jest toocreate Maszynę wirtualną i korzystać ze wszystkich zasobów hello utworzony. Witaj następujące części podręcznika dotyczącego Ansible tworzy Maszynę wirtualną o nazwie *myVM* i dołącza hello wirtualnej karty Sieciowej o nazwie *myNIC*. Wprowadź własne dane klucza publicznego w hello *key_data* Sparuj w następujący sposób:

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a>Zakończenie podręcznikowym Ansible
toobring tych sekcji, Utwórz podręcznikowym Ansible o nazwie *azure_create_complete_vm.yml* i Wklej hello następującej zawartości:

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Ansible musi toodeploy grupy zasobów do wszystkich zasobów. Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/vm#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello kompletne maszyny Wirtualnej środowisko z Ansible, uruchom podręcznikowym hello w następujący sposób:

```bash
ansible-playbook azure_create_complete_vm.yml
```

Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład pokazujący hello, że maszyna wirtualna została pomyślnie utworzona:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a>Następne kroki
W tym przykładzie tworzy pełną środowiska maszyny Wirtualnej, w tym hello wymaganych zasobów sieci wirtualnych. Dla bardziej bezpośrednie toocreate przykład Maszynę wirtualną do istniejących zasobów sieciowych z opcji domyślnych [tworzenie maszyny Wirtualnej](ansible-create-vm.md).
