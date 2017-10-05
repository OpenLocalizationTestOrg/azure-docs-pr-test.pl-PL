---
title: "Tworzenie podstawowej maszyny Wirtualnej systemu Linux na platformie Azure za pomocą Ansible | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Ansible tworzenie i zarządzanie nimi podstawowej maszyny wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="23d77-103">Tworzenie podstawowej maszyny wirtualnej na platformie Azure z Ansible</span><span class="sxs-lookup"><span data-stu-id="23d77-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="23d77-104">Ansible umożliwia automatyzację wdrożenia i konfiguracji zasobów w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="23d77-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="23d77-105">Ansible służy do zarządzania maszyn wirtualnych (VM) na platformie Azure, takie same jak w przypadku innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="23d77-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="23d77-106">W tym artykule przedstawiono sposób tworzenia podstawowej maszyny Wirtualnej z Ansible.</span><span class="sxs-lookup"><span data-stu-id="23d77-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="23d77-107">Możesz też dowiedzieć się, jak [utworzyć pełne środowisko maszyny Wirtualnej z Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="23d77-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="23d77-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="23d77-108">Prerequisites</span></span>
<span data-ttu-id="23d77-109">Do zarządzania zasobami Azure z Ansible, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="23d77-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="23d77-110">Ansible i moduły Azure Python SDK zainstalowanych w systemie hosta.</span><span class="sxs-lookup"><span data-stu-id="23d77-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="23d77-111">Zainstaluj na Ansible [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), i [SLES 12.2 z dodatkiem SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="23d77-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="23d77-112">Poświadczenia platformy Azure i Ansible skonfigurowane do korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="23d77-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="23d77-113">Utwórz poświadczenia platformy Azure i skonfigurować Ansible</span><span class="sxs-lookup"><span data-stu-id="23d77-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="23d77-114">Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="23d77-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="23d77-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="23d77-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="23d77-116">Jeśli konieczne będzie uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23d77-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="23d77-117">Można również użyć [powłoki chmury](/azure/cloud-shell/quickstart) z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="23d77-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="23d77-118">Tworzenie obsługi zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="23d77-118">Create supporting Azure resources</span></span>
<span data-ttu-id="23d77-119">W tym przykładzie tworzymy elementu runbook, który wdraża maszynę Wirtualną do istniejącej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="23d77-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="23d77-120">Najpierw należy utworzyć grupy zasobów z [Tworzenie grupy az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="23d77-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="23d77-121">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="23d77-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="23d77-122">Tworzenie sieci wirtualnej dla maszyny Wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="23d77-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="23d77-123">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="23d77-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="23d77-124">Tworzenie i uruchamianie podręcznikowym Ansible</span><span class="sxs-lookup"><span data-stu-id="23d77-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="23d77-125">Utwórz podręcznikowym Ansible o nazwie **azure_create_vm.yml** i Wklej poniższą zawartość.</span><span class="sxs-lookup"><span data-stu-id="23d77-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="23d77-126">W tym przykładzie tworzy jednej maszyny Wirtualnej i konfiguruje poświadczenia SSH.</span><span class="sxs-lookup"><span data-stu-id="23d77-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="23d77-127">Wprowadź własne danych kluczy publicznych w *key_data* Sparuj w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="23d77-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

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

<span data-ttu-id="23d77-128">Aby utworzyć maszynę Wirtualną z Ansible, uruchom podręcznikowym w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="23d77-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="23d77-129">Dane wyjściowe wygląda podobnie do poniższego przykładu, pokazujący, że pomyślnie utworzono maszynę Wirtualną:</span><span class="sxs-lookup"><span data-stu-id="23d77-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="23d77-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23d77-130">Next steps</span></span>
<span data-ttu-id="23d77-131">To przykładowe polecenie tworzy Maszynę wirtualną w istniejącej grupie zasobów i z siecią wirtualną już wdrożone.</span><span class="sxs-lookup"><span data-stu-id="23d77-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="23d77-132">Aby bardziej szczegółowy przykład dotyczące używania Ansible utworzyć obsługi zasobów, takich jak sieć wirtualną i reguł sieciowej grupy zabezpieczeń, zobacz [utworzyć pełne środowisko maszyny Wirtualnej z Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="23d77-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>