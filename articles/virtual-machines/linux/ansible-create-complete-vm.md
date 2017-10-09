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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="38afc-103">Utwórz pełną środowiska maszyny wirtualnej systemu Linux na platformie Azure z Ansible</span><span class="sxs-lookup"><span data-stu-id="38afc-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="38afc-104">Ansible pozwala tooautomate hello wdrażania i konfigurowania zasobów w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="38afc-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="38afc-105">Można używać Ansible toomanage maszyn wirtualnych (VM) na platformie Azure, hello takie same jak w przypadku innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="38afc-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="38afc-106">W tym artykule opisano sposób toocreate kompletne środowisko systemu Linux i pomocnicze zasoby z Ansible.</span><span class="sxs-lookup"><span data-stu-id="38afc-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="38afc-107">Możesz też dowiedzieć się, jak za[Tworzenie podstawowej maszyny Wirtualnej z Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="38afc-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="38afc-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38afc-108">Prerequisites</span></span>
<span data-ttu-id="38afc-109">toomanage Azure zasoby z Ansible, należy po hello:</span><span class="sxs-lookup"><span data-stu-id="38afc-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="38afc-110">Ansible i hello Azure Python SDK modułów zainstalowanych w systemie hosta.</span><span class="sxs-lookup"><span data-stu-id="38afc-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="38afc-111">Zainstaluj na Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), i [SLES 12.2 z dodatkiem SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="38afc-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="38afc-112">Poświadczenia platformy Azure i toouse Ansible skonfigurowane je.</span><span class="sxs-lookup"><span data-stu-id="38afc-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="38afc-113">Utwórz poświadczenia platformy Azure i skonfigurować Ansible</span><span class="sxs-lookup"><span data-stu-id="38afc-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="38afc-114">Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="38afc-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="38afc-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="38afc-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="38afc-116">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38afc-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="38afc-117">Można również użyć [powłoki chmury](/azure/cloud-shell/quickstart) z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="38afc-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="38afc-118">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="38afc-118">Create virtual network</span></span>
<span data-ttu-id="38afc-119">Witaj następujące części podręcznika dotyczącego Ansible tworzy sieć wirtualną o nazwie *myVnet* w hello *10.0.0.0/16* przestrzeni adresów:</span><span class="sxs-lookup"><span data-stu-id="38afc-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="38afc-120">tooadd podsieci powitania po sekcji tworzy podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="38afc-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="38afc-121">Utwórz publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="38afc-121">Create public IP address</span></span>
<span data-ttu-id="38afc-122">tooaccess zasobów między hello Internet, Utwórz i przypisz publicznego tooyour adres IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="38afc-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="38afc-123">Witaj następujące części podręcznika dotyczącego Ansible tworzy publiczny adres IP o nazwie *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="38afc-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="38afc-124">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="38afc-124">Create Network Security Group</span></span>
<span data-ttu-id="38afc-125">Grupy zabezpieczeń sieci sterowania przepływem hello ruchu sieciowego do i z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="38afc-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="38afc-126">Witaj następujące części podręcznika dotyczącego Ansible tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* i definiuje reguły tooallow SSH ruch na porcie TCP 22:</span><span class="sxs-lookup"><span data-stu-id="38afc-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

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


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="38afc-127">Tworzenie wirtualnej karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="38afc-127">Create virtual network interface card</span></span>
<span data-ttu-id="38afc-128">Karty interfejsu sieci wirtualnej (NIC) nawiązuje połączenie z tooa maszyna wirtualna danej sieci wirtualnej, publiczny adres IP i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="38afc-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="38afc-129">Witaj następujące części podręcznika dotyczącego Ansible tworzy wirtualną kartę Sieciową o nazwie *myNIC* połączone toohello wirtualnego zasoby sieciowe zostały utworzone:</span><span class="sxs-lookup"><span data-stu-id="38afc-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

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


## <a name="create-virtual-machine"></a><span data-ttu-id="38afc-130">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="38afc-130">Create virtual machine</span></span>
<span data-ttu-id="38afc-131">Ostatnim krokiem Hello jest toocreate Maszynę wirtualną i korzystać ze wszystkich zasobów hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="38afc-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="38afc-132">Witaj następujące części podręcznika dotyczącego Ansible tworzy Maszynę wirtualną o nazwie *myVM* i dołącza hello wirtualnej karty Sieciowej o nazwie *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="38afc-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="38afc-133">Wprowadź własne dane klucza publicznego w hello *key_data* Sparuj w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38afc-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

## <a name="complete-ansible-playbook"></a><span data-ttu-id="38afc-134">Zakończenie podręcznikowym Ansible</span><span class="sxs-lookup"><span data-stu-id="38afc-134">Complete Ansible playbook</span></span>
<span data-ttu-id="38afc-135">toobring tych sekcji, Utwórz podręcznikowym Ansible o nazwie *azure_create_complete_vm.yml* i Wklej hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="38afc-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

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

<span data-ttu-id="38afc-136">Ansible musi toodeploy grupy zasobów do wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="38afc-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="38afc-137">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="38afc-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="38afc-138">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="38afc-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="38afc-139">toocreate hello kompletne maszyny Wirtualnej środowisko z Ansible, uruchom podręcznikowym hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38afc-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="38afc-140">Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład pokazujący hello, że maszyna wirtualna została pomyślnie utworzona:</span><span class="sxs-lookup"><span data-stu-id="38afc-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="38afc-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38afc-141">Next steps</span></span>
<span data-ttu-id="38afc-142">W tym przykładzie tworzy pełną środowiska maszyny Wirtualnej, w tym hello wymaganych zasobów sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="38afc-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="38afc-143">Dla bardziej bezpośrednie toocreate przykład Maszynę wirtualną do istniejących zasobów sieciowych z opcji domyślnych [tworzenie maszyny Wirtualnej](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="38afc-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
