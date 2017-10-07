---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz maszynę Wirtualną z wirtualnego dysku twardego | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną przy użyciu wirtualnego dysku twardego."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Utwórz maszynę Wirtualną z wirtualnym dyskiem twardym

W tym przykładzie jest tworzony przy użyciu dysku VHD maszyny wirtualnej.
Tworzy grupę zasobów, konto magazynu i kontener, a następnie tworzy Maszynę wirtualną przekazując hello wirtualnego dysku twardego toohello kontenera.
Zastępuje hello ssh publicznego klucza kluczem publicznym, tak aby było możliwe toohello dostęp do maszyny Wirtualnej.

Będziesz potrzebować rozruchowy wirtualny dysk twardy.
Możesz pobrać hello dysku VHD, które zostały użyte z https://azclisamples.blob.core.windows.net/vhds/sample.vhd, lub użyć własnych wirtualnego dysku twardego. Wyszukuje skryptu Hello `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Lista kont magazynu az](https://docs.microsoft.com/cli/azure/storage/account#list) | Listy kont magazynu |
| [Sprawdź — nazwa az konta magazynu](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Sprawdza, czy nazwa konta magazynu jest prawidłowa i że jeszcze nie istnieje |
| [Lista kluczy kont magazynu az](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Wyświetla listę kluczy w przypadku kont magazynu hello |
| [istnieje az obiektu blob magazynu](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Sprawdza, czy istnieje hello obiektów blob |
| [Tworzenie kontenera magazynu az](https://docs.microsoft.com/cli/azure/storage/container#create) | Tworzy kontener na koncie magazynu. |
| [Przekazywanie obiektu blob magazynu az](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Tworzy obiekt blob w kontenerze hello przy hello przekazywanie wirtualnego dysku twardego. |
| [AZ listy maszyny wirtualnej](https://docs.microsoft.com/cli/azure/vm#list) | Używane z `--query` Sprawdź, czy nazwa maszyny Wirtualnej hello jest używany. | 
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Tworzy hello maszyn wirtualnych. |
| [AZ wirtualna dostęp zestaw linux użytkownika](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Resetuje hello SSH klucza toogive hello bieżącego użytkownika dostępu toohello maszyny Wirtualnej. |
| [AZ vm--adresy ip](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Pobiera adres IP hello hello maszynę Wirtualną, która została utworzona. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
