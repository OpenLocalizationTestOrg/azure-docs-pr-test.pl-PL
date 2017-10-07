---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — ponowne uruchomienie maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — ponowne uruchomienie maszyn wirtualnych, za pomocą tagu i identyfikator"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Ponowne uruchomienie maszyn wirtualnych

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

W tym przykładzie pokazano kilka sposobów tooget niektórych maszyn wirtualnych i uruchomić je ponownie.

Witaj najpierw powoduje ponowne uruchomienie wszystkich hello maszyn wirtualnych w grupie zasobów hello.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Witaj drugi hello pobiera oznakowane maszyn wirtualnych przy użyciu `az resouce list` filtry toohello zasoby, które są maszyny wirtualne i ponowne uruchomienie tych maszyn wirtualnych.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

W tym przykładzie działanie powłoki Bash. Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows hello Azure CLI](../windows/cli-options.md).


## <a name="sample-script"></a>Przykładowy skrypt

przykład Witaj ma trzy skryptów.
Witaj pierwszy z nich obsługuje hello maszyny wirtualne.
Opcja oczekiwania nie hello jest używany tak hello polecenie zwraca bez oczekiwania na każdym toobe maszyny Wirtualnej, udostępnione.
Witaj drugi czeka na powitania toobe maszyn wirtualnych w pełni zaaprowizowanym.
trzeci skryptu Hello ponowne uruchomienie wszystkich maszyn wirtualnych hello, które zostały udostępnione, a następnie tylko hello oznakowane maszyn wirtualnych.

### <a name="provision-hello-vms"></a>Zainicjuj obsługę hello maszyny wirtualne

Ten skrypt tworzy grupę zasobów, a następnie tworzy trzy toorestart maszyn wirtualnych.
Dwa z nich są oznaczone.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Oczekiwanie

Ten skrypt sprawdza na powitania stanu udostępniania co 20 sekund, dopóki wszystkie trzy maszyny wirtualne są udostępnione lub jeden z nich tooprovision zakończy się niepowodzeniem.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Uruchom ponownie hello maszyny wirtualne

Ten skrypt powoduje ponowne uruchomienie wszystkich maszyn wirtualnych hello w hello grupy zasobów, a następnie ponowne uruchomienie po prostu hello oznakowane maszyn wirtualnych.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grup zasobów hello tooremove używane, maszyn wirtualnych i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Tworzy hello maszyn wirtualnych.  |
| [AZ listy maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm#list) | Używane z `--query` hello tooensure maszyny wirtualne są udostępniane przed ponownym uruchomieniem je, a następnie tooget hello identyfikatorów toorestart maszyn wirtualnych hello je. |
| [Lista zasobów az](https://docs.microsoft.com/cli/azure/vm#list) | Używane z `--query` tooget hello identyfikatorów hello maszyn wirtualnych przy użyciu tagu hello. |
| [ponowne uruchomienie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#list) | Uruchamia ponownie hello maszyn wirtualnych. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
