---
title: "aaaInstall i skonfigurować Ansible do użycia z maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i skonfigurować Ansible na potrzeby zarządzania zasobami platformy Azure na SLES, Ubuntu i CentOS"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="a0bd4-103">Instalowanie i konfigurowanie maszyn wirtualnych toomanage Ansible na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a0bd4-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="a0bd4-104">W tym artykule szczegółowo sposób tooinstall Ansible i wymagane moduły Azure Python SDK dla niektórych hello najczęściej dystrybucjach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="a0bd4-105">Można zainstalować Ansible na inne dystrybucjach dostosowując hello zainstalowane pakiety toofit określonej platformy.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="a0bd4-106">toocreate Azure zasobów w sposób bezpieczny, możesz także dowiedzieć się, jak toocreate i zdefiniuj poświadczenia dla Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="a0bd4-107">Więcej opcji instalacji i kroki dla dodatkowych platform, zobacz hello [Przewodnik instalacji Ansible](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="a0bd4-108">Zainstaluj Ansible</span><span class="sxs-lookup"><span data-stu-id="a0bd4-108">Install Ansible</span></span>
<span data-ttu-id="a0bd4-109">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a0bd4-110">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAnsible* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="a0bd4-111">Teraz Utwórz maszynę Wirtualną i zainstaluj Ansible dla jednego z następujących dystrybucjach hello:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="a0bd4-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a0bd4-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="a0bd4-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="a0bd4-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="a0bd4-114">SLES 12.2 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="a0bd4-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="a0bd4-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a0bd4-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="a0bd4-116">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a0bd4-117">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a0bd4-118">SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` zanotowanym w hello operacji tworzenia dane wyjściowe hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a0bd4-119">Na maszynie Wirtualnej zainstalować pakiety hello wymagane dla modułów Azure Python SDK hello i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="a0bd4-120">Teraz przejść za[poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="a0bd4-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="a0bd4-121">CentOS 7.3</span></span>
<span data-ttu-id="a0bd4-122">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a0bd4-123">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a0bd4-124">SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` zanotowanym w hello operacji tworzenia dane wyjściowe hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a0bd4-125">Na maszynie Wirtualnej zainstalować pakiety hello wymagane dla modułów Azure Python SDK hello i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="a0bd4-126">Teraz przejść za[poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="a0bd4-127">SLES 12.2 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="a0bd4-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="a0bd4-128">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a0bd4-129">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a0bd4-130">SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` zanotowanym w hello operacji tworzenia dane wyjściowe hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="a0bd4-131">Na maszynie Wirtualnej zainstalować pakiety hello wymagane dla modułów Azure Python SDK hello i Ansible w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="a0bd4-132">Teraz przejść za[poświadczenia Azure utworzyć](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="a0bd4-133">Utwórz poświadczenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0bd4-133">Create Azure credentials</span></span>
<span data-ttu-id="a0bd4-134">Ansible komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="a0bd4-135">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak Ansible.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="a0bd4-136">Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="a0bd4-137">tooimprove zabezpieczeń za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="a0bd4-138">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i dane wyjściowe hello poświadczenia, które wymaga Ansible:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="a0bd4-139">Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="a0bd4-140">tooauthenticate tooAzure, należy również tooobtain identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="a0bd4-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="a0bd4-141">W następnym krokiem hello jest używany hello dane wyjściowe tych dwóch poleceń.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="a0bd4-142">Utwórz plik poświadczeń Ansible</span><span class="sxs-lookup"><span data-stu-id="a0bd4-142">Create Ansible credentials file</span></span>
<span data-ttu-id="a0bd4-143">tooprovide poświadczenia tooAnsible, zdefiniuj zmienne środowiskowe lub utworzyć plik poświadczeń lokalnych.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="a0bd4-144">Aby uzyskać więcej informacji o tym, jak poświadczenia Ansible toodefine, zobacz [tooAzure dostarczanie poświadczeń modułów](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="a0bd4-145">Środowisko deweloperskie, można utworzyć *poświadczenia* plik Ansible na hoście maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="a0bd4-146">Witaj *poświadczenia* sam plik łączy hello identyfikator subskrypcji z danych wyjściowych hello tworzenia nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="a0bd4-147">Dane wyjściowe z poprzedniego hello [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest sama hello zamówienie potrzebuje do *client_id*, *klucz tajny*, i *dzierżawy* .</span><span class="sxs-lookup"><span data-stu-id="a0bd4-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="a0bd4-148">Witaj następujący przykład *poświadczenia* plik zawiera te wartości dopasowania hello poprzednie dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="a0bd4-149">Wprowadź własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0bd4-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="a0bd4-150">Używać zmiennych środowiskowych Ansible</span><span class="sxs-lookup"><span data-stu-id="a0bd4-150">Use Ansible environment variables</span></span>
<span data-ttu-id="a0bd4-151">Jeśli zamierzasz toouse narzędzi, takich jak wieża Ansible lub Wpięć można zdefiniować zmienne środowiskowe w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="a0bd4-152">Te zmienne łączyć hello identyfikator subskrypcji z danymi wyjściowymi hello tworzenie główną usługi.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="a0bd4-153">Dane wyjściowe z poprzedniego hello [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest sama hello zamówienie potrzebuje do *AZURE_CLIENT_ID*, *AZURE_SECRET*, i *AZURE_ DZIERŻAWY*.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="a0bd4-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0bd4-154">Next steps</span></span>
<span data-ttu-id="a0bd4-155">Masz teraz Ansible i wymagane hello Azure Python SDK modułów zainstalowanych i poświadczeń określonych dla Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="a0bd4-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="a0bd4-156">Dowiedz się, jak za[utworzyć Maszynę wirtualną z Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="a0bd4-157">Możesz też dowiedzieć się, jak za[utworzyć pełną maszyny Wirtualnej platformy Azure i pomocnicze zasoby z Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a0bd4-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
