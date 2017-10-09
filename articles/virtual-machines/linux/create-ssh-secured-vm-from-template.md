---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure w ramach szablonu | Dokumentacja firmy Microsoft"
description: "Jak toouse hello Azure CLI 2.0 toocreate Maszynę wirtualną systemu Linux w ramach szablonu usługi Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Jak toocreate maszyny wirtualnej systemu Linux przy użyciu szablonów usługi Azure Resource Manager
W tym artykule opisano sposób tooquickly wdrażania maszyny wirtualnej systemu Linux (VM) z szablonów usługi Azure Resource Manager i hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Przegląd szablonów
Szablony usługi Azure Resource Manager są plikami JSON, definiujące hello infrastrukturze i konfiguracji rozwiązania Azure. Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu. toolearn więcej informacji na temat formatu hello hello szablonu i konstrukcji, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Witaj tooview składni JSON dla typów zasobów, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Tworzenie grupy zasobów
Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Grupy zasobów musi zostać utworzone przed maszyny wirtualnej. Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupVM* w hello *eastus* regionu:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
Witaj poniższy przykład tworzy Maszynę wirtualną z [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create). Podaj wartość hello własny klucz publiczny SSH, takie jak zawartość hello *~/.ssh/id_rsa.pub*. Jeśli potrzebujesz toocreate parę kluczy SSH, zobacz [jak toocreate i używanie SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

W tym przykładzie wybrano szablon przechowywany w serwisie GitHub. Można również pobrać lub utworzyć szablon i określ ścieżkę lokalną hello z hello tego samego `--template-file` parametru.

tooyour tooSSH maszyny Wirtualnej, Uzyskaj hello publicznego adresu IP z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Następnie można tooyour SSH maszyny Wirtualnej jako normalne:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Następne kroki
W tym przykładzie utworzono podstawowej maszyny Wirtualnej systemu Linux. W przypadku więcej szablonów Menedżera zasobów, które obejmują struktur aplikacji lub utworzyć bardziej złożonych środowiskach, należy wyszukać hello [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).
