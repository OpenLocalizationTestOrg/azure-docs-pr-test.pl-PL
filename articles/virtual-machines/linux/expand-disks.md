---
title: "wirtualne dyski twarde aaaExpand na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wirtualne dyski twarde tooexpand na Maszynę wirtualną systemu Linux z hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Jak wirtualne dyski twarde tooexpand na Maszynę wirtualną systemu Linux z hello wiersza polecenia platformy Azure
Witaj domyślny rozmiar wirtualnego dysku twardego systemu operacyjnego hello (systemu operacyjnego) jest zwykle 30 GB na maszynie wirtualnej systemu Linux (VM) na platformie Azure. Możesz [Dodaj dyski danych](add-disk.md) tooprovide dla dodatkowego miejsca, ale może również określić tooexpand istniejącego dysku danych. Ten artykuł zawiera szczegóły dotyczące sposobu zarządzania tooexpand dysków maszyny wirtualnej systemu Linux z hello Azure CLI 2.0. Można również rozszerzać dysk systemu operacyjnego hello niezarządzanych z hello [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Zawsze upewnij się, utworzono kopię zapasową danych przed wykonaniem dysku zmienić rozmiar operacji. Aby uzyskać więcej informacji, zobacz [kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Zwiększ rozmiar dysku
Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

W tym artykule wymaga istniejącej maszyny Wirtualnej na platformie Azure z co najmniej jeden dysk danych dołączona i przygotowane. Jeśli nie masz już maszyny Wirtualnej, który można użyć, zobacz [tworzenie i przygotowywanie maszyny Wirtualnej z dyskami danych](tutorial-manage-disks.md#create-and-attach-disks).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup* i *myVM*.

1. Nie można wykonać operacji na wirtualnych dyskach twardych z hello wirtualna uruchomiona. Cofnięcie przydziału maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`zwalnia zasoby obliczeniowe hello. toorelease zasoby obliczeniowe, użyj `az vm deallocate`. Witaj maszyny Wirtualnej można cofnąć przydziału tooexpand hello wirtualnego dysku twardego.

2. Wyświetl listę dysków zarządzanych w grupie zasobów o [Lista dysków az](/cli/azure/disk#list). Hello poniższym przykładzie zostanie wyświetlona lista dysków zarządzanych w grupie zasobów hello o nazwie *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Zwiększ rozmiar dysku wymagana hello z [aktualizacja dysku az](/cli/azure/disk#update). Witaj poniższy przykład rozszerza hello dysków zarządzanych o nazwie *myDataDisk* toobe *200*rozmiar Gb:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Po rozwinięciu dysków zarządzanych hello zaktualizowano rozmiar jest mapowane toohello najbliższego rozmiaru dysków zarządzanych. Dla tabeli hello dysków zarządzanych w dostępne rozmiary i warstw, zobacz [Azure zarządzanych dysków Przegląd — cennik i rozliczenia](../windows/managed-disks-overview.md#pricing-and-billing).

3. Uruchom maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start). Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. Tooyour SSH maszyny Wirtualnej z hello odpowiednie poświadczenia. Możesz uzyskać hello publicznego adresu IP maszyny Wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. toouse hello rozwinięty dysku, należy partycji podstawowej hello tooexpand i systemu plików.

    a. Jeśli już zainstalowane, odinstaluj hello dysku:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Użyj `parted` tooview informacje o dysku i rozmiar partycji hello:

    ```bash
    sudo parted /dev/sdc
    ```

    Wyświetl informacje o hello istniejący układ partycji z `print`. Witaj danych wyjściowych jest podobne toohello poniższy przykład, który zawiera informacje o dysku hello 215 Gb ma rozmiar:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Rozwiń węzeł hello partycji o `resizepart`. Wprowadź numer partycji hello, *1*i rozmiaru dla nowej partycji hello:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, wprowadź`quit`

5. Z partycją hello zmiany rozmiaru, należy sprawdzić spójność partycji hello z `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Teraz Zmień rozmiar filesystem hello z `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Toohello partycji hello instalacji konieczne lokalizacji, takich jak `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. Zmieniono rozmiar dysku systemu operacyjnego hello tooverify, użyj `df -h`. następujące przykładowe dane wyjściowe Hello pokazuje hello dysk danych, */dev/sdc1*, jest teraz 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz dodatkowego magazynu, możesz również [dodać tooa dysków danych maszyny Wirtualnej systemu Linux](add-disk.md). Aby uzyskać więcej informacji o szyfrowaniu dysków, zobacz [szyfrowania dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI](encrypt-disks.md).
