---
title: "toocreate aaaHow obrazów maszyn wirtualnych Azure Linux z pakujący | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse pakujący toocreate obrazów maszyn wirtualnych systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Jak obrazy maszyny wirtualnej systemu Linux toocreate pakujący toouse na platformie Azure
Każda maszyna wirtualna (VM) na platformie Azure jest tworzony z obrazu, który definiuje hello dystrybucji systemu Linux i wersji systemu operacyjnego. Obrazy mogą obejmować wstępnie zainstalowane aplikacje i konfiguracje. Hello Azure Marketplace zawiera wiele obrazów pierwszy i innych firm dla najczęściej używane dystrybucje i aplikacji w środowiskach, lub można utworzyć własne niestandardowe obrazy dostosowane tooyour potrzeb. W tym artykule szczegółowo sposób toouse hello otworzyć narzędzie źródła [pakujący](https://www.packer.io/) toodefine i kompilacji niestandardowych obrazów na platformie Azure.


## <a name="create-azure-resource-group"></a>Tworzenie grupy zasobów platformy Azure
W trakcie kompilacji hello pakujący tworzy tymczasowy zasobów platformy Azure zbudował hello źródłowej maszyny Wirtualnej. toocapture, który źródła do użycia jako obraz maszyny Wirtualnej, należy zdefiniować grupę zasobów. Witaj dane wyjściowe z procesu tworzenia pakujący hello są przechowywane w tej grupie zasobów.

Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Utwórz poświadczenia platformy Azure
Pakujący jest uwierzytelniany w usłudze Azure przy użyciu nazwy głównej usługi. Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak pakujący. Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure.

Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i dane wyjściowe hello poświadczeń pakujący musi:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, należy również tooobtain identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

W następnym krokiem hello jest używany hello dane wyjściowe tych dwóch poleceń.


## <a name="define-packer-template"></a>Zdefiniuj szablon pakujący
obrazy toobuild tworzenia szablonu w formacie JSON. W szablonie hello definiować konstruktorów i provisioners wykonujące hello rzeczywisty proces kompilacji. Ma pakujący [administracyjnej dla platformy Azure](https://www.packer.io/docs/builders/azure.html) pozwala toodefine Azure zasoby, takie jak poświadczenia główne usługi hello utworzone w hello poprzedzających krok.

Utwórz plik o nazwie *ubuntu.json* i Wklej powitania po zawartości. Wprowadź własne wartości dla następujących hello:

| Parametr                           | Gdzie tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Pierwszy wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *appId* |
| *client_secret*                     | Drugi wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *hasła* |
| *tenant_id*                         | Trzeci wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *dzierżawy* |
| *IDENTYFIKATOR_SUBSKRYPCJI*                   | Dane wyjściowe z `az account show` polecenia |
| *managed_image_resource_group_name* | Nazwa grupy zasobów, utworzonego w pierwszym krokiem hello |
| *managed_image_name*                | Nazwę hello dysków zarządzanych w obrazu, który jest tworzony |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Ten szablon tworzy obraz Ubuntu 16.04 LTS, instaluje NGINX, a następnie deprovisions hello maszyny Wirtualnej.

> [!NOTE]
> Po rozwinięciu tego szablonu tooprovision poświadczeń, Dostosuj polecenia administracyjnej hello czy deprovisions hello tooread agenta programu Azure `-deprovision` zamiast `deprovision+user`.
> Witaj `+user` flagi spowoduje usunięcie wszystkich kont użytkowników z hello źródłowej maszyny Wirtualnej.


## <a name="build-packer-image"></a>Utwórz obraz pakujący
Jeśli nie masz jeszcze pakujący zainstalowany na komputerze lokalnym [wykonaj instrukcje dotyczące instalacji pakujący hello](https://www.packer.io/docs/install/index.html).

Utwórz hello obraz, określając pakujący Twojego pliku szablonu w następujący sposób:

```bash
./packer build ubuntu.json
```

Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Tworzenie maszyny Wirtualnej z obrazu platformy Azure
Można teraz utworzyć Maszynę wirtualną z obrazu z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Określ obraz został utworzony z hello hello `--image` parametru. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z *myPackerImage* i generuje klucze SSH, jeśli jeszcze nie istnieje:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Może potrwać kilka minut hello toocreate maszyny Wirtualnej. Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure. Ten adres jest używany tooaccess hello NGINX lokacji za pośrednictwem przeglądarki sieci web.

tooallow web tooreach ruch maszyny Wirtualnej, otwórz port 80 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Test maszyny Wirtualnej i NGINX
Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `http://publicIpAddress` na pasku adresu hello. Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu. Strona NGINX domyślne Hello jest wyświetlana tak jak hello poniższy przykład:

![Domyślna witryna serwera NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Następne kroki
W tym przykładzie użyto toocreate pakujący obrazu maszyny Wirtualnej z NGINX już zainstalowana. Można użyć tego obrazu maszyny Wirtualnej będą widoczne obok istniejących przepływów pracy wdrażania, takie jak toodeploy Twojego tooVMs aplikacji utworzone na podstawie hello obrazu z Ansible, Chef lub Puppet.

Dla szablonów pakujący dodatkowe przykładowe dla innych dystrybucjach systemu Linux, zobacz [tego repozytorium GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).