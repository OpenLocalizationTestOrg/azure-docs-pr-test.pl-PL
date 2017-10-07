---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w innym regionie | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w tych samych lub różnych subskrypcji"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Eksport/kopiowania zarządzane migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie z interfejsu wiersza polecenia

Ten skrypt eksportuje migawki zarządzanego konta magazynu tooa w innym regionie. Najpierw generuje hello identyfikatora URI połączenia SAS hello migawki, a następnie używa go po toocopy go tooa konta magazynu w innym regionie. Użyj tej kopii zapasowej toomaintain skryptu dysków zarządzanych w innym regionie odzyskiwania po awarii. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń toogenerate identyfikator URI sygnatury dostępu Współdzielonego dla zarządzanych hello migawki i kopii migawki tooa konto magazynu przy użyciu identyfikatora URI połączenia SAS. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [AZ migawki Udziel dostępu](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Generuje SAS tylko do odczytu, używane toocopy podstawowego konta magazynu tooa pliku wirtualnego dysku twardego lub pobrać ją tooon lokalnych  |
| [Uruchom kopiowania obiektu blob magazynu az](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Kopiuje obiekt blob asynchronicznie z jednego tooanother konta magazynu |

## <a name="next-steps"></a>Następne kroki

[Tworzenie dysku zarządzanego z wirtualnego dysku twardego](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Utwórz maszynę wirtualną z dyskiem zarządzanym](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
