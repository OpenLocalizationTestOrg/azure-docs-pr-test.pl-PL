---
title: "Magazyn plików Azure na maszynach wirtualnych systemu Linux za pomocą protokołu SMB aaaMount | Dokumentacja firmy Microsoft"
description: "Jak toomount na maszynach wirtualnych systemu Linux za pomocą protokołu SMB z usługi Magazyn plików Azure hello Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Magazyn plików Azure instalacji na maszynach wirtualnych systemu Linux za pomocą protokołu SMB

W tym artykule opisano, jak zainstalować hello tooutilize Usługa Magazyn plików Azure na maszynie Wirtualnej systemu Linux za pomocą protokołu SMB z hello Azure CLI 2.0. Magazyn plików Azure oferuje udziały plików w chmurze hello przy użyciu standardowego protokołu SMB hello. Można również wykonać te kroki hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). wymagania dotyczące Hello są:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Szybkie polecenia

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
toodo tak, Dodaj powitania po wierszu toohello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Magazyn plików oferuje udziały plików w chmurze hello używających standardowego protokołu SMB hello. Witaj najnowszej wersji z pliku magazynu można również zainstalować udział plików z dowolnego systemu operacyjnego, który obsługuje protokół SMB 3.0. Użycie instalacji SMB w systemie Linux, otrzymasz łatwe tworzenie kopii zapasowych tooa niezawodne, stała archiwizacji lokalizacji magazynu, która jest obsługiwana przez umowy dotyczącej poziomu usług.

Przenoszenie plików z instalacji SMB tooan maszyny Wirtualnej znajdującej się na magazyn plików jest toodebug doskonałym sposobem logowania. Wynika to z faktu hello udziału SMB tego samego mogą być instalowane lokalnie tooyour Mac, Linux lub Windows stacji roboczej. SMB nie jest najlepszym rozwiązaniem hello do przesyłania strumieniowego Linux lub dzienniki aplikacji w czasie rzeczywistym, ponieważ hello protokołu SMB nie jest skompilowany toohandle tych obowiązków duże rejestrowania. Narzędzia rejestrowania dedykowanych, ujednoliconej warstwy, takiego jak Fluentd będzie lepszym rozwiązaniem niż SMB zbierania systemu Linux i aplikacji, rejestrowania danych wyjściowych.

Aby to szczegółowe wskazówki utworzymy hello wymagania wstępne niezbędne toofirst utworzyć udział magazynu plików hello, a następnie zainstalować go za pośrednictwem protokołu SMB na maszynie Wirtualnej systemu Linux.

1. Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) udziału plików hello toohold.

    Grupa zasobów o nazwie toocreate `myResourceGroup` w lokalizacji "Zachodnie stany USA" hello, użyj hello poniższy przykład:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Utwórz konto magazynu platformy Azure z [Tworzenie konta magazynu az](/cli/azure/storage/account#create) toostore hello rzeczywistymi plikami.

    toocreate konto magazynu o nazwie mojekontomagazynu przy użyciu magazynu Standard_LRS hello jednostka SKU, użyj hello poniższy przykład:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Pokaż klucze konta magazynu hello.

    Podczas tworzenia konta magazynu, klucze konta hello są tworzone w parach, dzięki czemu można obracać bez przerw w działaniu usługi. Po przełączeniu toohello drugi klucz w parze hello, możesz utworzyć nową parę kluczy. Nowe klucze konta magazynu zawsze są tworzone w parach, sprawdzając, czy zawsze jest co najmniej jeden magazyn nieużywane konta klucza gotowe tooswitch do.

    Wyświetl klucze konta magazynu hello hello [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list). Witaj klucze konta magazynu dla hello o nazwie `mystorageaccount` są wymienione w hello poniższy przykład:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract jednego klucza, użyj hello `--query` flagi. Witaj poniższy przykład wyodrębnia hello pierwszego klucza (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Utwórz udział magazynu plików hello.

    udział magazynu plików Hello zawiera hello udziału SMB z [utworzyć udział magazynu az](/cli/azure/storage/share#create). przydział Hello jest zawsze wyrażona w gigabajtów (GB). Podaj jeden z kluczy hello z poprzednim hello `az storage account keys list` polecenia. Utwórz udział o nazwie mystorageshare z przydziału 10 GB, za pomocą hello poniższy przykład:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Utwórz katalog punktu instalacji.

    Utwórz katalog lokalny w hello Linux pliku system toomount hello do udziału SMB. Cokolwiek zapisu lub odczytu z katalogu instalacji lokalnej hello są przesyłane dalej toohello udziału SMB, który znajduje się w pliku magazynu. toocreate katalogu lokalnego na/mnt/mymountdirectory, użyj hello poniższy przykład:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Zainstaluj katalogu lokalnego udziału toohello hello SMB.

    Podaj własne nazwy użytkownika konta magazynu i klucza konta magazynu dla poświadczenia instalacji hello:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Utrwalanie hello SMB instalacji podczas ponownych rozruchów.

    Po ponownym uruchomieniu maszyny Wirtualnej systemu Linux hello hello zainstalowany udział SMB jest odinstalowane podczas zamykania. hello tooremount udziale SMB podczas rozruchu, Dodaj wiersz toohello /etc/fstab systemu Linux. Linux używa hello fstab pliku toolist hello systemów plików wymaga toomount, podczas procesu rozruchu hello. Dodawanie udziału SMB hello gwarantuje, że ten udział magazynu plików hello jest trwale zainstalowany system plików dla hello maszyny Wirtualnej systemu Linux. Dodawanie hello pliku magazynu SMB udziału tooa nowej maszyny Wirtualnej jest możliwe, gdy używasz init chmury.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Następne kroki

- [Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Dodaj tooa dysku maszyny Wirtualnej systemu Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
