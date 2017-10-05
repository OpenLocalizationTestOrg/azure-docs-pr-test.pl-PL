---
title: "Różne sposoby, aby utworzyć Maszynę wirtualną systemu Linux za pomocą interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Informacje na temat różnych sposobów tworzenia maszyny wirtualnej z systemem Linux na platformie Azure oraz linki do narzędzi i samouczków dotyczących poszczególnych metod."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a>Różne sposoby tworzenia maszyny wirtualnej z systemem Linux na platformie Azure
Platforma Azure umożliwia elastyczne tworzenie maszyn wirtualnych z systemem Linux przy użyciu dowolnych narzędzi i przepływów pracy. Ten artykuł zawiera podsumowanie różnych sposobów oraz przykłady tworzenia maszyn wirtualnych z systemem Linux.

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Maszyny wirtualne na platformie Azure można tworzyć przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:

- Interfejs wiersza polecenia platformy Azure w wersji 1.0 — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami (w tym artykule)
- [Interfejs wiersza polecenia platformy Azure w wersji 2.0](../windows/creation-choices.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami

Interfejs wiersza polecenia platformy Azure w wersji 1.0 jest dostępny na wielu platformach przy użyciu pakietów menedżera npm, pakietów dostępnych dla określonych dystrybucji lub kontenera Docker. Jeśli chcesz, możesz uzyskać więcej informacji na temat [sposobu instalowania i konfigurowania interfejsu wiersza polecenia platformy Azure](../../cli-install-nodejs.md). Poniższe samouczki zawierają przykłady dotyczące używania interfejsu wiersza polecenia platformy Azure w wersji 1.0. Zapoznaj się z poszczególnymi artykułami, aby uzyskać więcej informacji na temat przedstawionych poleceń Szybki start interfejsu wiersza polecenia:

* [Tworzenie maszyny wirtualnej systemu Linux z poziomu interfejsu wiersza polecenia platformy Azure w celach programistycznych i testowych](quick-create-cli-nodejs.md)
  
  * Poniższy przykład tworzy CoreOS maszyny Wirtualnej za pomocą klucza publicznego o nazwie *azure_id_rsa.pub*:
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [Tworzenie zabezpieczonej maszyny wirtualnej systemu Linux przy użyciu szablonu Azure](create-ssh-secured-vm-from-template.md)
  
  * W poniższym przykładzie maszyna wirtualna jest tworzona przy użyciu szablonu przechowywanego w witrynie GitHub:
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [Tworzenie kompletnego środowiska systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure](create-cli-complete-nodejs.md)
  
  * Obejmuje tworzenie modułu równoważenia obciążenia i wielu maszyn wirtualnych w zestawie dostępności.
* [Dodawanie dysku do maszyny wirtualnej z systemem Linux](add-disk.md)
  
  * W poniższym przykładzie dodano *5* dysku Gb do istniejącej maszyny Wirtualnej o nazwie *myVM*:
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a>Azure Portal
Witryna [Azure Portal](https://portal.azure.com) umożliwia szybkie tworzenie maszyn wirtualnych, ponieważ nie wymaga instalacji żadnych składników w systemie. Użyj witryny Azure Portal, aby utworzyć maszynę wirtualną:

* [Tworzenie maszyny wirtualnej z systemem Linux przy użyciu witryny Azure Portal](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a>Wybór systemu operacyjnego i obrazu
Podczas tworzenia maszyny wirtualnej możesz wybrać obraz w oparciu o system operacyjny, który chcesz uruchomić. Platforma Azure i jej partnerzy oferują wiele obrazów, z których część zawiera wstępnie zainstalowane aplikacje i narzędzia. Możesz również przekazać własny obraz (więcej informacji można znaleźć w [poniższej sekcji](#use-your-own-image)).

### <a name="azure-images"></a>Obrazy platformy Azure
Użyj poleceń `azure vm image` interfejsu wiersza polecenia, aby wyświetlić dostępne obrazy według wydawcy, wersji dystrybucji i kompilacji.

Wyświetl dostępnych wydawców w następujący sposób:

```azurecli
azure vm image list-publishers --location eastus
```

Wyświetl dostępne produkty (oferty) w następujący sposób:

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

Wyświetl dostępne jednostki SKU (wersje dystrybucji) dla danej oferty w następujący sposób:

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

Wyświetl dostępne obrazy dla danego wydania w następujący sposób:

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

Polecenia `azure vm quick-create` i `azure vm create` mają aliasy umożliwiające szybki dostęp do najpopularniejszych dystrybucji i ich najnowszych wersji. Użycie aliasów jest zwykle łatwiejsze niż określanie wydawcy, oferty, jednostki SKU i wersji za każdym razem podczas tworzenia maszyny wirtualnej:

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
Jeśli potrzebujesz specjalnego dostosowania, możesz użyć obrazu opartego na istniejącej maszynie wirtualnej platformy Azure poprzez *przechwycenie* tej maszyny wirtualnej. Możesz również przekazać obraz utworzony lokalnie. Aby uzyskać więcej informacji o obsługiwanych dystrybucjach i sposobach wykorzystania własnych obrazów, zobacz następujące artykuły:

* [Dystrybucje zatwierdzone na platformie Azure](endorsed-distros.md)
* [Informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md)
* [Przekazywanie i tworzenie maszyny wirtualnej z systemem Linux z niestandardowego obrazu dysku](upload-vhd.md)
* [How to capture a Linux virtual machine as a Resource Manager template](capture-image.md) (Jak przechwycić maszynę wirtualną systemu Linux jako szablon usługi Resource Manager).
  
  * Przykładowe polecenia Szybki start umożliwiające przechwycenie istniejącej maszyny wirtualnej:
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a>Następne kroki
* Utwórz maszynę wirtualną z systemem Linux przy użyciu [portalu](quick-create-portal.md), interfejsu [wiersza polecenia platformy Azure](quick-create-cli.md) lub [szablonu](../windows/cli-deploy-templates.md) usługi Azure Resource Manager.
* Po utworzeniu maszyny wirtualnej z systemem Linux [dodaj dysk danych](add-disk.md).
* Szybkie kroki umożliwiające [zresetowanie hasła lub kluczy SSH i zarządzanie użytkownikami](using-vmaccess-extension.md)

