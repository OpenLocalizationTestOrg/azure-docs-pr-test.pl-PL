---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Utwórz maszynę wirtualną przy użyciu istniejącego dysku systemu operacyjnego zarządzanego z interfejsu wiersza polecenia

Ten skrypt tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego. Użyj tego skryptu w poprzednich scenariuszach:
* Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został skopiowany z dysków zarządzanych w innej subskrypcji
* Tworzenie maszyny Wirtualnej z istniejącego dysku zarządzanego utworzony na podstawie specjalne pliku wirtualnego dysku twardego 
* Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został utworzony na podstawie migawki 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące właściwości dysku tooget zarządzane poleceń, Dołącz tooa dysków zarządzanych w nowej maszyny Wirtualnej i tworzenie maszyny Wirtualnej. Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż dysku az](https://docs.microsoft.com/cli/azure/disk#show) | Pobiera właściwości dysków zarządzanych przy użyciu nazwy dysku i nazwę grupy zasobów. Identyfikator właściwości jest używane tooattach tooa dysków zarządzanych w nowej maszyny Wirtualnej |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy Maszynę wirtualną przy użyciu zarządzanego dysku systemu operacyjnego |
## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
