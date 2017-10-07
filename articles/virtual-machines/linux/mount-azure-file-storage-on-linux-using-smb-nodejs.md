---
title: "aaaMount magazyn plików Azure na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak toomount magazyn plików Azure na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Magazyn plików Azure instalacji na maszynach wirtualnych systemu Linux przy użyciu protokołu SMB 1.0 interfejsu wiersza polecenia platformy Azure

W tym artykule opisano, jak toomount magazyn plików Azure na maszynie Wirtualnej systemu Linux przy użyciu hello protokołu bloku komunikatów serwera (SMB). Magazyn plików oferuje udziały plików w chmurze hello za pośrednictwem hello standardowego protokołu SMB. wymagania dotyczące Hello są:

* [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Secure Shell (SSH) publicznego i prywatnego klucza plików](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>Toouse wersje interfejsu wiersza polecenia
Hello zadanie można wykonać za pomocą jednego z hello następujące wersje interfejsu wiersza polecenia (CLI):

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia
zadanie hello tooaccomplish szybkie, wykonaj kroki hello w tej sekcji. Aby uzyskać szczegółowe informacje i kontekstu, rozpoczęcie hello ["Szczegółowy przewodnik"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sekcji.

### <a name="prerequisites"></a>Wymagania wstępne
* Grupy zasobów
* Sieć wirtualna platformy Azure
* Grupa zabezpieczeń sieci przy użyciu protokołu SSH dla ruchu przychodzącego
* Podsieci
* Konto magazynu platformy Azure
* Klucze konta magazynu platformy Azure
* Udział magazynu plików Azure
* Maszynę wirtualną systemu Linux

Przykładami należy zastąpić własnymi ustawieniami.

### <a name="create-a-directory-for-hello-local-mount"></a>Utwórz katalog instalacji lokalne powitania

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Zainstaluj punkt instalacji toohello udziału SMB hello pliku magazynu

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Utrwalanie hello instalacji po ponownym uruchomieniu
Dodaj powitania po wierszu zbyt`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Magazyn plików oferuje udziały plików w chmurze hello używających standardowego protokołu SMB hello. Witaj najnowszej wersji z pliku magazynu można również zainstalować udział plików z dowolnego systemu operacyjnego, który obsługuje protokół SMB 3.0. Użycie instalacji SMB w systemie Linux, otrzymasz łatwe tworzenie kopii zapasowych tooa niezawodne, stała archiwizacji lokalizacji magazynu, która jest obsługiwana przez umowy dotyczącej poziomu usług.

Przenoszenie plików z instalacji SMB tooan maszyny Wirtualnej znajdującej się na magazyn plików jest toodebug doskonałym sposobem logowania. Wynika to z faktu hello udziału SMB tego samego mogą być instalowane lokalnie tooyour Mac, Linux lub Windows stacji roboczej. SMB nie jest najlepszym rozwiązaniem hello do przesyłania strumieniowego Linux lub dzienniki aplikacji w czasie rzeczywistym, ponieważ hello protokołu SMB nie jest skompilowany toohandle tych obowiązków duże rejestrowania. Narzędzia rejestrowania dedykowanych, ujednoliconej warstwy, takiego jak Fluentd będzie lepszym rozwiązaniem niż SMB zbierania systemu Linux i aplikacji, rejestrowania danych wyjściowych.

Aby to szczegółowe wskazówki utworzymy hello wymagania wstępne niezbędne toofirst utworzyć udział magazynu plików hello, a następnie zainstalować go za pośrednictwem protokołu SMB na maszynie Wirtualnej systemu Linux.

1. Utwórz konto magazynu platformy Azure przy użyciu hello następującego kodu:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Pokaż klucze konta magazynu hello.

    Podczas tworzenia konta magazynu, klucze konta hello są tworzone w parach, dzięki czemu można obracać bez przerw w działaniu usługi. Po przełączeniu toohello drugi klucz w parze hello, możesz utworzyć nową parę kluczy. Nowe klucze konta magazynu zawsze są tworzone w parach, sprawdzając, czy zawsze jest co najmniej jeden nieużywane magazynu kluczy gotowe tooswitch do. tooshow hello klucze konta magazynu, należy użyć hello następującego kodu:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Utwórz udział magazynu plików hello.

    udział magazynu plików Hello zawiera hello udziału SMB. przydział Hello jest zawsze wyrażona w gigabajtów (GB). toocreate hello udział magazynu plików, użyj następującego kodu hello:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Utwórz katalog punktu instalacji hello.

    Należy utworzyć w hello Linux pliku system toomount hello udziału SMB do katalogu lokalnego. Cokolwiek zapisu lub odczytu z katalogu instalacji lokalnej hello są przesyłane dalej toohello udziału SMB, który znajduje się w pliku magazynu. toocreate hello katalog hello Użyj następującego kodu:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Zainstaluj hello udziału SMB przy użyciu hello następującego kodu:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Utrwalanie hello SMB instalacji podczas ponownych rozruchów.

    Po ponownym uruchomieniu maszyny Wirtualnej systemu Linux hello hello zainstalowany udział SMB jest odinstalowane podczas zamykania. tooremount hello udziale SMB podczas rozruchu, należy dodać toohello wiersza /etc/fstab systemu Linux. Linux używa hello fstab pliku toolist hello systemów plików wymaga toomount, podczas procesu rozruchu hello. Dodawanie udziału SMB hello gwarantuje, że ten udział magazynu plików hello jest trwale zainstalowany system plików dla hello maszyny Wirtualnej systemu Linux. Dodawanie hello pliku magazynu SMB udziału tooa nowej maszyny Wirtualnej jest możliwe, gdy używasz init chmury.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Następne kroki

- [Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Dodaj tooa dysku maszyny Wirtualnej systemu Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
