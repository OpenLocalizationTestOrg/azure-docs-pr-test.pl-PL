---
title: "aaaDifferent sposobów toocreate Maszynę wirtualną systemu Linux na platformie Azure | Microsoft Azure"
description: "Dowiedz się toocreate różne sposoby hello maszyny wirtualnej systemu Linux na platformie Azure, w tym tootools łącza i samouczki dotyczące każdej z metod."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Różne sposoby toocreate Maszynę wirtualną systemu Linux
Masz hello elastyczność w Azure toocreate maszyny wirtualnej systemu Linux (VM) przy użyciu narzędzia i przepływów pracy tooyou samodzielnej. Ten artykuł zawiera podsumowanie tych różnic oraz przykłady tworzenia maszyn wirtualnych systemu Linux, łącznie z hello Azure CLI 2.0. Można również wyświetlić w tym hello opcji tworzenia [Azure CLI 1.0](creation-choices-nodejs.md).

Witaj [Azure CLI 2.0](/cli/azure/install-az-cli2) jest dostępny na platformach za pomocą pakietu npm, wprowadzone do distro pakietów lub kontener Docker. Zainstaluj hello kompilacji najbardziej odpowiednie dla danego środowiska, a następnie zaloguj się za pomocą konta Azure tooan [az logowania](/cli/azure/#login)

* [Utwórz Maszynę wirtualną systemu Linux z hello Azure CLI 2.0](quick-create-cli.md)
  
  * Za pomocą polecenia [az group create](/cli/azure/group#create) utwórz grupę zasobów o nazwie *myResourceGroup*: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) o nazwie *myVM* przy użyciu najnowszych hello *UbuntuLTS* obrazu i generowanie kluczy SSH, jeśli nie już istnieją w *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Tworzenie maszyny wirtualnej z systemem Linux przy użyciu szablonu platformy Azure](create-ssh-secured-vm-from-template.md)
  
  * Witaj poniższym przykładzie użyto [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) toocreate Maszynę wirtualną z szablonu przechowywany w serwisie GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Tworzenie maszyny wirtualnej z systemem Linux i dostosowywanie jej za pomocą skryptów cloud-init](tutorial-automate-vm-deployment.md)

* [Tworzenie aplikacji wysokiej dostępności ze zrównoważonym obciążeniem na wielu maszynach wirtualnych z systemem Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure Portal
Witaj [portalu Azure](https://portal.azure.com) pozwala tooquickly tworzenie maszyny Wirtualnej, ponieważ nie ma nic tooinstall w tym systemie. Użyj hello Azure toocreate portalu hello maszyny Wirtualnej:

* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello portalu Azure](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Wybór systemu operacyjnego i obrazu
Podczas tworzenia maszyny Wirtualnej, należy wybrać obraz oparty na powitania ma toorun systemu operacyjnego. Platforma Azure i jej partnerzy oferują wiele obrazów, z których część zawiera wstępnie zainstalowane aplikacje i narzędzia. Lub przekazać jeden z własnych obrazów (zobacz [hello następujących sekcji](#use-your-own-image)).

### <a name="azure-images"></a>Obrazy platformy Azure
Użyj hello [obrazu maszyny wirtualnej az](/cli/azure/vm/image) polecenia toosee, co jest dostępne, wydawca, wersja distro i kompilacji.

Aby wyświetlić dostępnych wydawców:

```azurecli
az vm image list-publishers --location eastus
```

Aby wyświetlić dostępne produkty (oferty) dla wybranego wydawcy:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Aby wyświetlić dostępne jednostki SKU (wersje dystrybucji) dla danej oferty:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Aby wyświetlić dostępne obrazy dla danego wydania:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Aby uzyskać więcej przykładów z przeglądaniem i wykorzystywaniem dostępnych obrazów, zobacz [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą interfejsu wiersza polecenia Azure hello](cli-ps-findimage.md).

Witaj [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia zawiera aliasy tooquickly dostępu można użyć hello częściej dystrybucjach i ich najnowsze wersje. Używanie aliasów często jest szybsza niż określenie hello wydawcy, oferty, jednostki SKU i wersji w przypadku tworzenia maszyny Wirtualnej:

| Alias | Wydawca | Oferta | SKU | Wersja |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |najnowsza |
| CoreOS |CoreOS |CoreOS |Stable |najnowsza |
| Debian |credativ |Debian |8 |najnowsza |
| openSUSE |SUSE |openSUSE |13.2 |najnowsza |
| RHEL |Redhat |RHEL |7.2 |najnowsza |
| SLES |SLES |SLES |12-SP1 |najnowsza |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |najnowsza |

### <a name="use-your-own-image"></a>Użycie własnego obrazu
Jeśli potrzebujesz specjalnego dostosowania, możesz użyć obrazu opartego na istniejącej maszynie wirtualnej platformy Azure poprzez przechwycenie tej maszyny wirtualnej. Możesz również przekazać obraz utworzony lokalnie. Aby uzyskać więcej informacji o obsługiwanych dystrybucjach i toouse własnych obrazów, zobacz temat hello następujące artykuły:

* [Dystrybucje zatwierdzone na platformie Azure](endorsed-distros.md)
* [Informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md)
* [Jak toocreate obrazu z istniejącej maszyny Wirtualnej Azure](tutorial-custom-images.md).
  
  * Szybki start przykład polecenia toocreate obrazu z istniejącej maszyny Wirtualnej platformy Azure:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Następne kroki
* Utwórz Maszynę wirtualną systemu Linux z hello [CLI](quick-create-cli.md), z hello [portal](quick-create-portal.md), lub za pomocą [szablonu usługi Azure Resource Manager](../windows/cli-deploy-templates.md).
* Po utworzeniu maszyny wirtualnej z systemem Linux [dowiedz się więcej o dyskach i magazynie platformy Azure](tutorial-manage-disks.md).
* Szybkie kroki zbyt[zresetowanie hasła lub kluczy SSH i zarządzanie użytkownikami](using-vmaccess-extension.md).
