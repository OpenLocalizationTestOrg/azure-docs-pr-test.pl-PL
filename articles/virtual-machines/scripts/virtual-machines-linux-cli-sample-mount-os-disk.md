---
title: "Przykładowy skrypt interfejsu wiersza polecenia — dysk systemu operacyjnego instalacji aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - instalacji dysk systemu operacyjnego"
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Rozwiązywanie problemów z dyskiem systemu operacyjnego maszyny wirtualne

Ten skrypt instaluje hello dysku systemu operacyjnego maszyny wirtualnej nie powiodło się lub problemem jako dane dysku tooa drugiej maszyny wirtualnej. Może to być przydatne podczas rozwiązywania problemów z dysku problemy lub odzyskiwania danych. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż wirtualna az](https://docs.microsoft.com/cli/azure/vm#show) | Zwraca listę maszyn wirtualnych. W takim przypadku hello opcja zapytania jest dysk systemu operacyjnego maszyny wirtualnej hello tooreturn używane. Ta wartość jest następnie dodawana tooa nazwę zmiennej "uri". |
| [AZ usuwania maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm#delete) | Usuwa maszynę wirtualną. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) | Tworzy maszynę wirtualną.  |
| [Dołącz az dysku maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Dołącza maszynę wirtualną tooa dysku. |
| [AZ vm--adresy ip](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Zwraca hello adresów IP maszyny wirtualnej. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
