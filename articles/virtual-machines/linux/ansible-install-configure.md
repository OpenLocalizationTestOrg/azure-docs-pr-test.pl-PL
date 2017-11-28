---
title: "Instalowanie i konfigurowanie Ansible do użytku z maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować i skonfigurować Ansible dla zarządzania zasobami platformy Azure na SLES, Ubuntu i CentOS"
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
ms.openlocfilehash: 52b763274437961dccfc862c8a45fbd57ea9fc4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a><span data-ttu-id="a2ab4-103">Instalowanie i konfigurowanie Ansible do zarządzania maszynami wirtualnymi na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a2ab4-103">Install and configure Ansible to manage virtual machines in Azure</span></span>
<span data-ttu-id="a2ab4-104">Ten artykuł zawiera szczegóły dotyczące sposobu instalowania Ansible i wymagane moduły Azure Python SDK dla niektórych typowych dystrybucjach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-104">This article details how to install Ansible and required Azure Python SDK modules for some of the most common Linux distros.</span></span> <span data-ttu-id="a2ab4-105">Ansible można zainstalować na innych dystrybucjach, dopasowując zainstalowanych pakietów do określonej platformy.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-105">You can install Ansible on other distros by adjusting the installed packages to fit your particular platform.</span></span> <span data-ttu-id="a2ab4-106">Tworzenie zasobów Azure, w sposób bezpieczny, możesz również Dowiedz się, jak utworzyć i zdefiniować poświadczenia dla Ansible do użycia.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-106">To create Azure resources in a secure manner, you also learn how to create and define credentials for Ansible to use.</span></span> 

<span data-ttu-id="a2ab4-107">Więcej opcji instalacji i kroki dla dodatkowych platform, zobacz [Przewodnik instalacji Ansible](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-107">For more installation options and steps for additional platforms, see the [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="a2ab4-108">Zainstaluj Ansible</span><span class="sxs-lookup"><span data-stu-id="a2ab4-108">Install Ansible</span></span>
<span data-ttu-id="a2ab4-109">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a2ab4-110">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAnsible* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-110">The following example creates a resource group named *myResourceGroupAnsible* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="a2ab4-111">Teraz Utwórz maszynę Wirtualną i zainstaluj Ansible dla jednego z następujących dystrybucjach:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-111">Now create a VM and install Ansible for one of the following distros:</span></span>

- [<span data-ttu-id="a2ab4-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a2ab4-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="a2ab4-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="a2ab4-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="a2ab4-114">SLES 12.2 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="a2ab4-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="a2ab4-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a2ab4-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="a2ab4-116">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a2ab4-117">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-117">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a2ab4-118">SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-118">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a2ab4-119">Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-119">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="a2ab4-120">Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-120">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="a2ab4-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="a2ab4-121">CentOS 7.3</span></span>
<span data-ttu-id="a2ab4-122">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a2ab4-123">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-123">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a2ab4-124">SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-124">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a2ab4-125">Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-125">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="a2ab4-126">Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-126">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="a2ab4-127">SLES 12.2 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="a2ab4-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="a2ab4-128">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a2ab4-129">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-129">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a2ab4-130">SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-130">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a2ab4-131">Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-131">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="a2ab4-132">Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-132">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="a2ab4-133">Utwórz poświadczenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a2ab4-133">Create Azure credentials</span></span>
<span data-ttu-id="a2ab4-134">Ansible komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="a2ab4-135">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak Ansible.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="a2ab4-136">Kontrolowanie i definiowanie uprawnień określające, jakie operacje nazwy głównej usługi można wykonać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="a2ab4-137">Zwiększające bezpieczeństwo za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="a2ab4-138">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i poświadczenia, które wymaga Ansible wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="a2ab4-139">Przykład danych wyjściowych z poprzedniego polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-139">An example of the output from the preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="a2ab4-140">Aby uwierzytelniać na platformie Azure, również należy uzyskać identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="a2ab4-140">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="a2ab4-141">Dane wyjściowe z tych dwóch poleceń należy użyć w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-141">You use the output from these two commands in the next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="a2ab4-142">Utwórz plik poświadczeń Ansible</span><span class="sxs-lookup"><span data-stu-id="a2ab4-142">Create Ansible credentials file</span></span>
<span data-ttu-id="a2ab4-143">Aby podać poświadczenia, aby Ansible, zdefiniuj zmienne środowiskowe, lub utworzyć plik lokalne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-143">To provide credentials to Ansible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="a2ab4-144">Aby uzyskać więcej informacji na temat definiowania Ansible poświadczeń, zobacz [dostarczanie poświadczeń do modułów Azure](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-144">For more information about how to define Ansible credentials, see [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="a2ab4-145">Środowisko deweloperskie, można utworzyć *poświadczenia* plik Ansible na hoście maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="a2ab4-146">*Poświadczenia* sam plik łączy identyfikator subskrypcji z danych wyjściowych Tworzenie nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-146">The *credentials* file itself combines the subscription ID with the output of creating a service principal.</span></span> <span data-ttu-id="a2ab4-147">Dane wyjściowe z poprzedniej [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest tej samej kolejności, w razie potrzeby dla *client_id*, *klucz tajny*, i *dzierżawy*.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-147">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="a2ab4-148">Poniższy przykład *poświadczenia* plik zawiera wartości te dane wyjściowe poprzedniego dopasowania.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-148">The following example *credentials* file shows these values matching the previous output.</span></span> <span data-ttu-id="a2ab4-149">Wprowadź własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a2ab4-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="a2ab4-150">Używać zmiennych środowiskowych Ansible</span><span class="sxs-lookup"><span data-stu-id="a2ab4-150">Use Ansible environment variables</span></span>
<span data-ttu-id="a2ab4-151">Jeśli zamierzasz używać narzędzi, takich jak wieża Ansible lub Wpięć, można zdefiniować zmienne środowiskowe w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-151">If you are going to use tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="a2ab4-152">Te zmienne łączyć identyfikator subskrypcji z danymi wyjściowymi tworzenie główną usługi.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-152">These variables combine the subscription ID with the output from creating a service principal.</span></span> <span data-ttu-id="a2ab4-153">Dane wyjściowe z poprzedniej [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest tej samej kolejności, w razie potrzeby dla *AZURE_CLIENT_ID*, *AZURE_SECRET*, i *AZURE_TENANT* .</span><span class="sxs-lookup"><span data-stu-id="a2ab4-153">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="a2ab4-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2ab4-154">Next steps</span></span>
<span data-ttu-id="a2ab4-155">Masz teraz Ansible oraz wymagane moduły Azure Python SDK zainstalowany i poświadczeń określonych dla Ansible do użycia.</span><span class="sxs-lookup"><span data-stu-id="a2ab4-155">You now have Ansible and the required Azure Python SDK modules installed, and credentials defined for Ansible to use.</span></span> <span data-ttu-id="a2ab4-156">Dowiedz się, jak [utworzyć Maszynę wirtualną z Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-156">Learn how to [create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="a2ab4-157">Możesz też dowiedzieć się, jak [utworzyć pełną maszyny Wirtualnej platformy Azure i pomocnicze zasoby z Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a2ab4-157">You can also learn how to [create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>