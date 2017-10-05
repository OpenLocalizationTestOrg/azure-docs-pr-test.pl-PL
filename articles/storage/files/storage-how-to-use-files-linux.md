---
title: "Magazyn plików Azure za pomocą systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować udział plików Azure za pośrednictwem protokołu SMB w systemie Linux."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: d8987082c559a374b8d19fd69e20cf5e81cb25ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Użyj usługi Magazyn plików Azure z systemem Linux
[Azure File Storage](../storage-dotnet-how-to-use-files.md) to łatwy w użyciu system plików w chmurze firmy Microsoft. Udziały plików platformy Azure można zainstalować w dystrybucje systemu Linux przy użyciu [pakietu cifs witryny](https://wiki.samba.org/index.php/LinuxCIFS_utils) z [projektu Samba](https://www.samba.org/). W tym artykule przedstawiono dwie metody, aby zainstalować udział plików Azure: na żądanie z `mount` polecenia i na rozruchu, tworząc wpis w `/etc/fstab`.

> [!NOTE]  
> Aby zainstalować udział plików Azure poza Azure region, który jest obsługiwany, takich jak lokalnie lub w innym regionie Azure, system operacyjny musi obsługiwać funkcje szyfrowania protokołu SMB 3.0. Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra. Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure. Podczas publikowania ta funkcja została backported do Ubuntu z 16.04 i powyżej.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a>Konfigurator służący do instalowania plików Azure udostępniać Linux oraz pakiet cifs witryny
* **Wybierz dystrybucji systemu Linux, który może mieć zainstalowanym pakietem cifs witryny**: Firma Microsoft zaleca następujące dystrybucje systemu Linux w galerii Azure obrazu:

    * Ubuntu Server 14.04 +
    * RHEL 7 +
    * CentOS 7 +
    * Debian 8
    * openSUSE 13.2 +
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Zainstalowano pakiet cifs witryny**: witryny cifs można zainstalować za pomocą Menedżera pakietu na dystrybucji systemu Linux wybranych przez użytkownika. 

    Na **Ubuntu** i **na podstawie Debian** dystrybucji, użyj `apt-get` Menedżera pakietów:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Na **RHEL** i **CentOS**, użyj `yum` Menedżera pakietów:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Na **openSUSE**, użyj `zypper` Menedżera pakietów:

    ```
    sudo zypper install samba*
    ```

    W innych dystrybucji przy użyciu Menedżera odpowiedniego pakietu lub [Kompiluj ze źródła](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Podejmowanie decyzji o uprawnienia pliku lub katalogu zainstalowany udział**: W poniższym przykładzie używamy 0777, aby dać odczytu, zapisu i wykonywania uprawnienia do wszystkich użytkowników. Można zastąpić go z innymi [uprawnienia chmod](https://en.wikipedia.org/wiki/Chmod) pożądane. 

* **Nazwa konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie podanie nazwy konta magazynu.

* **Klucz konta magazynu**: Aby zainstalować udział plików platformy Azure, konieczne będzie posiadanie podstawowego (lub dodatkowego) klucza magazynu. Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.

* **Upewnij się, jest otwarty port 445**: SMB komunikuje się za pośrednictwem portu TCP 445 — Sprawdź, czy Zapora nie blokuje TCP, porty 445 z komputera klienta.

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a>Instalacji plików Azure udostępniania na żądanie za pomocą`mount`
1. **[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji**: można to zrobić dowolne miejsce w systemie plików.

    ```
    mkdir mymountpoint
    ```

3. **Aby zainstalować udział plików Azure za pomocą polecenia instalacji**: Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` przy użyciu odpowiednich informacji.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Po zakończeniu korzystania z udziału plików platformy Azure, możesz użyć `sudo umount ./mymountpoint` odinstalował udziału.

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a>Utwórz punkt trwałej dla udziału plików platformy Azure z`/etc/fstab`
1. **[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji**: można to zrobić dowolne miejsce w systemie plików, ale należy pamiętać, bezwzględną ścieżkę do folderu. Poniższy przykład tworzy folder w katalogu głównym.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Użyj następującego polecenia, aby dołączyć następujący wiersz do `/etc/fstab`** : Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` przy użyciu odpowiednich informacji.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Można użyć `sudo mount -a` Aby zainstalować udział plików Azure po zakończeniu edycji `/etc/fstab` zamiast ponownego uruchamiania.

## <a name="feedback"></a>Opinia
Użytkownicy systemu Linux, chcemy poznać Twoją opinię!

Magazyn plików Azure dla grupy Użytkownicy systemu Linux udostępnia forum można udostępnić opinii, oceny i przyjęcie magazynu plików w systemie Linux. Wiadomości e-mail [magazyn plików Azure użytkowników systemu Linux](mailto:azurefileslinuxusers@microsoft.com) dołączenia do grupy użytkowników.

## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Jak używać narzędzia AzCopy z magazynu Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Przy użyciu wiersza polecenia platformy Azure z usługą Azure storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów](storage-troubleshoot-linux-file-connection-problems.md)
