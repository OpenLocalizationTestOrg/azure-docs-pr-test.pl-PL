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
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a>Instalowanie i konfigurowanie Ansible do zarządzania maszynami wirtualnymi na platformie Azure
Ten artykuł zawiera szczegóły dotyczące sposobu instalowania Ansible i wymagane moduły Azure Python SDK dla niektórych typowych dystrybucjach systemu Linux. Ansible można zainstalować na innych dystrybucjach, dopasowując zainstalowanych pakietów do określonej platformy. Tworzenie zasobów Azure, w sposób bezpieczny, możesz również Dowiedz się, jak utworzyć i zdefiniować poświadczenia dla Ansible do użycia. 

Więcej opcji instalacji i kroki dla dodatkowych platform, zobacz [Przewodnik instalacji Ansible](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Zainstaluj Ansible
Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAnsible* w *eastus* lokalizacji:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Teraz Utwórz maszynę Wirtualną i zainstaluj Ansible dla jednego z następujących dystrybucjach:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 Z DODATKIEM SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:

```bash
ssh azureuser@<publicIpAddress>
```

Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:

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

Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:

```bash
ssh azureuser@<publicIpAddress>
```

Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 Z DODATKIEM SP2
Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create). Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH przy użyciu maszyny Wirtualnej `publicIpAddress` zauważyć w danych wyjściowych z maszyny Wirtualnej operacji tworzenia:

```bash
ssh azureuser@<publicIpAddress>
```

Na maszynie Wirtualnej Zainstaluj wymagane pakiety dla modułów Azure Python SDK i Ansible w następujący sposób:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Teraz przejść do [poświadczenia Azure utworzyć](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Utwórz poświadczenia platformy Azure
Ansible komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi. Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak Ansible. Kontrolowanie i definiowanie uprawnień określające, jakie operacje nazwy głównej usługi można wykonać na platformie Azure. Zwiększające bezpieczeństwo za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.

Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i poświadczenia, które wymaga Ansible wyjściowe:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Przykład danych wyjściowych z poprzedniego polecenia jest następujący:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

Aby uwierzytelniać na platformie Azure, również należy uzyskać identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Dane wyjściowe z tych dwóch poleceń należy użyć w następnym kroku.


## <a name="create-ansible-credentials-file"></a>Utwórz plik poświadczeń Ansible
Aby podać poświadczenia, aby Ansible, zdefiniuj zmienne środowiskowe, lub utworzyć plik lokalne poświadczenia. Aby uzyskać więcej informacji na temat definiowania Ansible poświadczeń, zobacz [dostarczanie poświadczeń do modułów Azure](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Środowisko deweloperskie, można utworzyć *poświadczenia* plik Ansible na hoście maszyny Wirtualnej w następujący sposób:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

*Poświadczenia* sam plik łączy identyfikator subskrypcji z danych wyjściowych Tworzenie nazwy głównej usługi. Dane wyjściowe z poprzedniej [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest tej samej kolejności, w razie potrzeby dla *client_id*, *klucz tajny*, i *dzierżawy*. Poniższy przykład *poświadczenia* plik zawiera wartości te dane wyjściowe poprzedniego dopasowania. Wprowadź własne wartości w następujący sposób:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Używać zmiennych środowiskowych Ansible
Jeśli zamierzasz używać narzędzi, takich jak wieża Ansible lub Wpięć, można zdefiniować zmienne środowiskowe w następujący sposób. Te zmienne łączyć identyfikator subskrypcji z danymi wyjściowymi tworzenie główną usługi. Dane wyjściowe z poprzedniej [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) polecenie jest tej samej kolejności, w razie potrzeby dla *AZURE_CLIENT_ID*, *AZURE_SECRET*, i *AZURE_TENANT* . 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Następne kroki
Masz teraz Ansible oraz wymagane moduły Azure Python SDK zainstalowany i poświadczeń określonych dla Ansible do użycia. Dowiedz się, jak [utworzyć Maszynę wirtualną z Ansible](ansible-create-vm.md). Możesz też dowiedzieć się, jak [utworzyć pełną maszyny Wirtualnej platformy Azure i pomocnicze zasoby z Ansible](ansible-create-complete-vm.md).