---
title: dysk aaaExpand systemu operacyjnego na maszynie Wirtualnej systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooexpand hello wirtualny dysk systemu operacyjnego (OS) na maszynie Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Zwiększ rozmiar dysku systemu operacyjnego na maszynie Wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello z hello Azure CLI w wersji 1.0
Witaj domyślny rozmiar wirtualnego dysku twardego systemu operacyjnego hello (systemu operacyjnego) jest zwykle 30 GB na maszynie wirtualnej systemu Linux (VM) na platformie Azure. Możesz [Dodaj dyski danych](add-disk.md) tooprovide dla dodatkowego miejsca, ale możesz również tooexpand dysku hello systemu operacyjnego. W tym artykule szczegółowo sposób hello tooexpand systemu operacyjnego na dysku dla maszyny Wirtualnej systemu Linux przy użyciu niezarządzanych dysków z hello Azure CLI w wersji 1.0.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#prerequisites) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](expand-disks.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="prerequisites"></a>Wymagania wstępne
Należy hello [najnowsze Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowane i zarejestrowane w tooan [konta Azure](https://azure.microsoft.com/pricing/free-trial/) przy użyciu tryb usługi Resource Manager hello w następujący sposób:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup* i *myVM*.

## <a name="expand-os-disk"></a>Rozszerzanie dysku systemu operacyjnego

1. Nie można wykonać operacji na wirtualnych dyskach twardych z hello wirtualna uruchomiona. Witaj poniższy przykład zatrzymuje i zwalnia hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`zwalnia zasoby obliczeniowe hello. toorelease zasoby obliczeniowe, użyj `azure vm deallocate`. Witaj maszyny Wirtualnej można cofnąć przydziału tooexpand hello wirtualnego dysku twardego.

2. Zaktualizuj hello rozmiar dysku systemu operacyjnego hello niezarządzanych za pomocą hello `azure vm set` polecenia. Po aktualizacji przykład Hello hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Uruchom maszyny Wirtualnej w następujący sposób:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. Tooyour SSH maszyny Wirtualnej z hello odpowiednie poświadczenia. Zmieniono rozmiar dysku systemu operacyjnego hello tooverify, użyj `df -h`. następujące przykładowe dane wyjściowe Hello pokazuje hello partycji podstawowej (*/dev/sda1*) jest teraz 50 GB:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz dodatkowego magazynu, możesz również [dodać tooa dysków danych maszyny Wirtualnej systemu Linux](add-disk.md). Aby uzyskać więcej informacji o szyfrowaniu dysków, zobacz [szyfrowania dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI](encrypt-disks.md).
