---
title: "Usługa pliki Azure za pomocą systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować udział plików na platformę Azure przy użyciu protokołu SMB w systemie Linux."
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
ms.date: 12/20/2017
ms.author: renash
ms.openlocfilehash: cca0d315a815faca5db07099b8e8e451ef55fad5
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="use-azure-files-with-linux"></a>Użyj plików platformy Azure z systemem Linux
[Azure Files](storage-files-introduction.md) to łatwy w użyciu system plików w chmurze firmy Microsoft. Udziały plików platformy Azure można zainstalować w dystrybucje systemu Linux przy użyciu [CIFS jądra klienta](https://wiki.samba.org/index.php/LinuxCIFS). W tym artykule przedstawiono dwie metody, aby zainstalować udział plików na platformę Azure: na żądanie z `mount` polecenia i na rozruchu, tworząc wpis w `/etc/fstab`.

> [!NOTE]  
> Aby zainstalować udział plików na platformę Azure poza region platformy Azure, który jest obsługiwany w, takich jak lokalnie lub w innym regionie Azure, system operacyjny musi obsługiwać funkcje szyfrowania protokołu SMB 3.0.

## <a name="prerequisites-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a>Wymagania wstępne dotyczące instalowania udziału plików na platformę Azure z systemem Linux i pakietu cifs witryny
* **Wybierz dystrybucji systemu Linux, który może mieć zainstalowanym pakietem cifs witryny.**  
    Następujące dystrybucje systemu Linux są dostępne do użycia w galerii platformy Azure:

    * Ubuntu Server 14.04+
    * RHEL 7 +
    * CentOS 7+
    * Debian 8 +
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Zainstalowano pakiet cifs witryny.**  
    Pakiet cifs witryny można zainstalować za pomocą Menedżera pakietu na dystrybucji systemu Linux wybranych przez użytkownika. 

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

* <a id="smb-client-reqs"></a>**Zrozumienie wymagań dotyczących klientów SMB.**  
    Usługa pliki Azure można zainstalować za pośrednictwem protokołu SMB 2.1 i 3.0 protokołu SMB. W przypadku połączeń pochodzącego z klientami lokalnymi lub z innych regionów platformy Azure pliki Azure spowoduje odrzucenie protokół SMB 2.1 (lub SMB 3.0 bez szyfrowania). Jeśli *bezpieczny transfer wymagane* jest włączona dla konta magazynu plików Azure będzie Zezwalaj na połączenia tylko z szyfrowaniem przy użyciu protokołu SMB 3.0.
    
    Obsługa szyfrowania protokołu SMB 3.0 została wprowadzona w systemie Linux wersji jądra 4.11 i została backported do starszych wersji jądra dla popularnych dystrybucje systemu Linux. W chwili opublikowania tego dokumentu następujące dystrybucji z poziomu galerii Azure obsługuje tę funkcję:

    - Ubuntu Server 16.04+
    - openSUSE 42.3+
    - SUSE Linux Enterprise Server 12 SP3+
    
    Jeśli dystrybucji systemu Linux nie ma na liście, można sprawdzić, aby wyświetlić wersję jądra systemu Linux przy użyciu następującego polecenia:

    ```
    uname -r
    ```

* **Podejmowanie decyzji o uprawnienia pliku lub katalogu zainstalowany udział**: W przykładzie poniżej uprawnienie `0777` jest używać, aby zapewnić odczytu, zapisu i wykonywania uprawnienia do wszystkich użytkowników. Można zastąpić go z innymi [uprawnienia chmod](https://en.wikipedia.org/wiki/Chmod) pożądane. 

* **Nazwa konta magazynu**: Aby zainstalować udział plików na platformę Azure, potrzebna jest nazwa konta magazynu.

* **Klucz konta magazynu**: Aby zainstalować udział plików na platformę Azure, potrzebny jest klucz podstawowy (lub dodatkowej) magazynu. Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.

* **Upewnij się, jest otwarty port 445**: SMB komunikuje się za pośrednictwem portu TCP 445 — Sprawdź, czy Zapora nie blokuje TCP, porty 445 z komputera klienta.

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a>Instalowanie plików na platformę Azure udziału na żądanie z`mount`
1. **[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji**: folder punkt instalacji można utworzyć dowolne miejsce w systemie plików, ale jest typowe Konwencji, aby je utworzyć w obszarze `/mnt` folderu. Na przykład:

    ```
    mkdir /mnt/MyAzureFileShare
    ```

3. **Aby zainstalować udział plików na platformę Azure za pomocą polecenia instalacji**: Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, `<smb-version>`, `<storage-account-key>`, i `<mount-point>` odpowiednie informacje dla danego środowiska. W przypadku dystrybucji systemu Linux obsługuje protokół SMB 3.0 przy użyciu szyfrowania (zobacz [wymagania dotyczące klienta SMB zrozumieć](#smb-client-reqs) Aby uzyskać więcej informacji), użyj `3.0` dla `<smb-version>`. Dystrybucje systemu Linux, które nie obsługują protokołu SMB 3.0 z szyfrowaniem, można użyć `2.1` dla `<smb-version>`. Należy pamiętać, że udział plików na platformę Azure może być instalowany tylko poza region platformy Azure (łącznie z lokalnymi lub w innym regionie Azure) z protokołem SMB 3.0. 

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> <mount-point> -o vers=<smb-version>,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Po zakończeniu korzystania z udziału plików na platformę Azure, możesz użyć `sudo umount <mount-point>` odinstalował udziału.

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a>Utwórz punkt trwałej z udziału plików na platformę Azure`/etc/fstab`
1. **[Zainstaluj pakiet cifs witryny dla dystrybucji systemu Linux](#install-cifs-utils)**.

2. **Utwórz folder na potrzeby punktu instalacji**: folder punkt instalacji można utworzyć dowolne miejsce w systemie plików, ale jest typowe Konwencji, aby je utworzyć w obszarze `/mnt` folderu. Wszędzie tam, gdzie można utworzyć, należy zwrócić uwagę na bezwzględną ścieżkę do folderu. Na przykład następujące polecenie tworzy nowy folder na `/mnt` (ścieżka jest ścieżką bezwzględną).

    ```
    sudo mkdir /mnt/MyAzureFileShare
    ```

3. **Użyj następującego polecenia, aby dołączyć następujący wiersz do `/etc/fstab`** : Pamiętaj, aby zastąpić `<storage-account-name>`, `<share-name>`, `<smb-version>`, `<storage-account-key>`, i `<mount-point>` odpowiednie informacje dla użytkownika środowisko. W przypadku dystrybucji systemu Linux obsługuje protokół SMB 3.0 przy użyciu szyfrowania (zobacz [wymagania dotyczące klienta SMB zrozumieć](#smb-client-reqs) Aby uzyskać więcej informacji), użyj `3.0` dla `<smb-version>`. Dystrybucje systemu Linux, które nie obsługują protokołu SMB 3.0 z szyfrowaniem, można użyć `2.1` dla `<smb-version>`. Należy pamiętać, że udział plików na platformę Azure może być instalowany tylko poza region platformy Azure (łącznie z lokalnymi lub w innym regionie Azure) z protokołem SMB 3.0. 

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> <mount-point> cifs nofail,vers=<smb-version>,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Można użyć `sudo mount -a` Aby zainstalować udział plików na platformę Azure po zakończeniu edycji `/etc/fstab` zamiast ponownego uruchamiania.

## <a name="feedback"></a>Opinia
Użytkownicy systemu Linux, chcemy poznać Twoją opinię!

Pliki Azure dla grupy Użytkownicy systemu Linux udostępnia forum można udostępnić opinii, oceny i przyjęcie magazynu plików w systemie Linux. Wiadomości e-mail [użytkowników systemu Linux plików Azure](mailto:azurefileslinuxusers@microsoft.com) dołączenia do grupy użytkowników.

## <a name="next-steps"></a>Kolejne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Azure Files.
* [Wprowadzenie do platformy Azure pliki](storage-files-introduction.md)
* [Planowanie wdrożenia usługi pliki Azure](storage-files-planning.md)
* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów](storage-troubleshoot-linux-file-connection-problems.md)