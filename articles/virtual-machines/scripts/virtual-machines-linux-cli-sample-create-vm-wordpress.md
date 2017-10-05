---
title: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z WordPress | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a>Utwórz maszynę Wirtualną z WordPress

Ten skrypt tworzy maszynę wirtualną, a następnie używa maszyny wirtualnej Azure rozszerzenie skryptu niestandardowego do zainstalowania WordPress. Po uruchomieniu skryptu, można uzyskać dostępu do witrynę WordPress konfiguracji pod `http://<public IP of VM>/wordpress`. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "szybkie tworzenie maszyn wirtualnych")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG. To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.  |
| [open — port az maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm#open-port) | Tworzy reguły grupy zabezpieczeń sieci, aby zezwalać na ruch przychodzący. W tym przykładzie port 80 jest otwarty dla ruchu HTTP. |
| [zestaw rozszerzeń maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Dodaj niestandardowe rozszerzenie skryptu do maszyny wirtualnej, która wywołuje skrypt instalacji WordPress. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
