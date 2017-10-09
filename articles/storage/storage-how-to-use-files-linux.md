---
title: "Magazyn plików Azure z systemem Linux aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić toomount plików Azure za pośrednictwem protokołu SMB w systemie Linux."
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
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Użyj usługi Magazyn plików Azure z systemem Linux
[Magazyn plików Azure](storage-dotnet-how-to-use-files.md) jest system plików w chmurze łatwe toouse firmy Microsoft. Udziały plików platformy Azure można zainstalować w dystrybucje systemu Linux przy użyciu hello [pakietu cifs witryny](https://wiki.samba.org/index.php/LinuxCIFS_utils) z hello [projektu Samba](https://www.samba.org/). W tym artykule opisano dwa sposoby toomount udziału plików platformy Azure: na żądanie z hello `mount` polecenia i na rozruchu, tworząc wpis w `/etc/fstab`.

> [!NOTE]  
> W kolejności toomount udział plików Azure poza hello region platformy Azure, który jest obsługiwany, takich jak lokalnie lub w innym regionie Azure, hello systemu operacyjnego musi obsługiwać hello funkcji szyfrowania protokołu SMB 3.0. Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra. Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure. W czasie hello publikowania ta funkcja została tooUbuntu backported z 16.04 i nowszych.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Wymagania wstępne dla instalowanie udziału plików platformy Azure z systemem Linux i hello pakietem cifs witryny
* **Wybierz dystrybucji systemu Linux, którą może mieć zainstalowany pakiet witryny cifs hello**: Firma Microsoft zaleca hello dystrybucje systemu Linux w galerii Azure obraz powitania po:

    * Ubuntu Server 14.04 +
    * RHEL 7 +
    * CentOS 7 +
    * Debian 8
    * openSUSE 13.2 +
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Witaj witryny cifs zainstalowano pakietu**: hello cifs witryny można zainstalować za pomocą Menedżera pakietów hello na dystrybucji systemu Linux hello wybranych przez użytkownika. 

    Na **Ubuntu** i **na podstawie Debian** dystrybucji, użyj hello `apt-get` Menedżera pakietów:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Na **RHEL** i **CentOS**, użyj hello `yum` Menedżera pakietów:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Na **openSUSE**, użyj hello `zypper` Menedżera pakietów:

    ```
    sudo zypper install samba*
    ```

    W innych dystrybucji przy użyciu Menedżera odpowiedniego pakietu hello lub [Kompiluj ze źródła](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Podejmowanie decyzji o uprawnienia pliku lub katalogu hello hello zainstalowany udział**: W poniższych przykładach hello, używamy 0777, toogive odczytu, zapisu i wykonywania uprawnienia tooall użytkowników. Można zastąpić go z innymi [uprawnienia chmod](https://en.wikipedia.org/wiki/Chmod) pożądane. 

* **Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.

* **Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu. Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.

* **Upewnij się, jest otwarty port 445**: SMB komunikuje się za pośrednictwem portu TCP 445 - Sprawdź toosee, czy Zapora nie blokuje TCP porty 445 z komputera klienta.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Zainstaluj hello na żądanie z udziału plików platformy Azure`mount`
1. **[Zainstalować hello cifs witryny pakietu dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji hello**: można to zrobić dowolne miejsce w systemie plików hello.

    ```
    mkdir mymountpoint
    ```

3. **Udział plików Azure hello toomount polecenia użyj hello instalacji**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` hello odpowiednie informacje.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Gdy wszystko będzie gotowe za pomocą hello udziału plików na platformę Azure, możesz użyć `sudo umount ./mymountpoint` toounmount hello udziału.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Tworzenie punktu instalacji trwałe hello udział plików Azure`/etc/fstab`
1. **[Zainstalować hello cifs witryny pakietu dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji hello**: można to zrobić dowolne miejsce w systemie plików hello, ale należy toonote hello ścieżka bezwzględna hello folderu. Witaj poniższy przykład tworzy folder w katalogu głównym.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Użyj hello następujące polecenie hello tooappend po wierszu zbyt`/etc/fstab`**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, i `<storage-account-key>` hello odpowiednie informacje.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Można użyć `sudo mount -a` udział plików Azure hello toomount po edycji `/etc/fstab` zamiast ponownego uruchamiania.

## <a name="feedback"></a>Opinia
Użytkownicy systemu Linux, chcemy toohear od Ciebie!

Hello magazyn plików Azure do grupy użytkowników systemu Linux udostępnia forum dla Ciebie tooshare opinii ocenić i przyjęcie magazynu plików w systemie Linux. Wiadomości e-mail [magazyn plików Azure użytkowników systemu Linux](mailto:azurefileslinuxusers@microsoft.com) grupy Użytkownicy hello toojoin.

## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Przy użyciu programu Azure PowerShell z usługą Azure storage](storage-powershell-guide-full.md)
* [Jak toouse AzCopy z magazynu Microsoft Azure](storage-use-azcopy.md)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure storage](storage-azure-cli.md#create-and-manage-file-shares)
* [Często zadawane pytania](storage-files-faq.md)
* [Rozwiązywanie problemów](storage-troubleshoot-file-connection-problems.md)
