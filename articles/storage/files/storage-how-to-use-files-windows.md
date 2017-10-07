---
title: "aaaMount udziału plików platformy Azure i hello dostępu do udziału w systemie Windows | Dokumentacja firmy Microsoft"
description: "Instalowanie udziału plików platformy Azure i udziału hello dostępu w systemie Windows."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Instalowanie udziału plików platformy Azure i udziału hello dostępu w systemie Windows
[Magazyn plików Azure](../storage-dotnet-how-to-use-files.md) jest system plików w chmurze łatwe toouse firmy Microsoft. Udziały plików platformy Azure można instalować w systemie Windows i Windows Server. W tym artykule przedstawiono trzy różne sposoby toomount udział plików Azure w systemie Windows: z hello Interfejsu Eksploratora plików, za pomocą programu PowerShell i za pośrednictwem hello wiersza polecenia. 

W kolejności toomount udział plików Azure poza hello region platformy Azure, który jest obsługiwany w, takich jak lokalnie lub w innym regionie Azure hello systemu operacyjnego musi obsługiwać protokół SMB 3.0. 

Udział plików platformy Azure można zainstalować na maszynie z systemem Windows w środowisku lokalnym lub na maszynie wirtualnej platformy Azure, w zależności od wersji systemu operacyjnego. Poniższej tabeli przedstawiono hello 

| Wersja systemu Windows        | Wersja protokołu SMB |Instalacja na maszynie wirtualnej platformy Azure|Instalacja w środowisku lokalnym|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Tak                 | Nie                  |
| Windows Server 2008 R2 | SMB 2.1     | Tak                 | Nie                  |
| Windows 8              | SMB 3.0     | Tak                 | Tak                 |
| Windows Server 2012    | SMB 3.0     | Tak                 | Tak                 |
| Windows Server 2012 R2 | SMB 3.0     | Tak                 | Tak                 |
| Windows 10             | SMB 3.0     | Tak                 | Tak                 |

> [!Note]  
> Zawsze zalecamy z argumentami hello KB najnowszej wersji systemu Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie Windows 
* **Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.

* **Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu. Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.

* **Otwarty port 445**: Usługa Azure File Storage korzysta z protokołu SMB. SMB komunikuje się za pośrednictwem portu TCP 445 - Sprawdź toosee, czy Zapora nie blokuje porty TCP 445 z komputera klienta.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Instalowanie udziału plików Azure hello z Eksploratora plików
> [!Note]  
> Należy pamiętać, że Witaj, postępując zgodnie z instrukcjami są wyświetlane w systemie Windows 10 i może różnić się nieznacznie w starszych wersjach. 

1. **Otwórz okno Eksploratora plików**: można to zrobić przez otwarcie z hello Start Menu lub naciskając klawisz skrótu Win + E.

2. **Przejdź element "Ten komputer" toohello na powitania po lewej stronie powitania okna. Spowoduje to zmianę menu hello hello Wstążce. W obszarze hello komputera menu, wybierz "Mapuj dysk sieciowy"**.
    
    ![Zrzut ekranu przedstawiający menu rozwijanego "Mapuj dysk sieciowy" hello](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Ścieżka UNC hello kopiowania z okienka "Połącz" hello w portalu Azure hello**: szczegółowy opis sposobu toofind te informacje można znaleźć [tutaj](storage-how-to-use-files-portal.md#connect-to-file-share).

    ![ścieżka UNC Hello w okienku Połącz magazyn plików Azure hello](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. **Wybierz hello literę dysku, a następnie wprowadź ścieżkę UNC hello.** 
    
    ![Zrzut ekranu okna dialogowego powitania "Mapuj dysk sieciowy"](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Użyj hello nazwy konta magazynu poprzedzony przez `Azure\` jako hello nazwy użytkownika i klucz konta magazynu, jako hello hasła.**
    
    ![Zrzut ekranu okna dialogowego poświadczeń sieciowych hello](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Użyj udziału plików platformy Azure zgodnie z potrzebami**.
    
    ![Udział plików platformy Azure jest teraz zainstalowany](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Gdy są gotowe toodismount (lub odłączyć) hello udziału plików platformy Azure możesz to zrobić przez kliknięcie prawym przyciskiem myszy na zapis hello hello udziału w obszarze hello "lokalizacje sieciowe" w Eksploratorze plików i wybierając polecenie "Rozłącz"**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Instalowanie udziału plików Azure hello przy użyciu programu PowerShell
1. **Użyj hello następujące polecenie udział plików Azure hello toomount**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello odpowiednie informacje.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Użyj udziału plików platformy Azure hello zgodnie z potrzebami**.

3. **Gdy skończysz, należy odinstalować hello udziału plików platformy Azure przy użyciu następującego polecenia hello**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Można użyć hello `-Persist` parametru `New-PSDrive` hello toomake pozostałe toohello widoczne udział plików Azure hello systemu operacyjnego, gdy jest zainstalowany.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Instalowanie udziału plików Azure hello z wiersza polecenia
1. **Użyj hello następujące polecenie udział plików Azure hello toomount**: Pamiętaj tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello odpowiednie informacje.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Użyj udziału plików platformy Azure hello zgodnie z potrzebami**.

3. **Gdy skończysz, należy odinstalować hello udziału plików platformy Azure przy użyciu następującego polecenia hello**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Witaj ponownie tooautomatically udział plików Azure można skonfigurować na ponowne uruchomienie komputera przez utrwalanie poświadczeń hello w systemie Windows. następujące polecenie Hello zostanie utrzymana hello poświadczeń:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)
* [Jak toouse magazyn plików Azure z systemem Linux](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Narzędzia dostępne dla usługi Azure File Storage
* [Jak toouse AzCopy z usługi Magazyn Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Rozwiązywanie problemów z usługą Azure File Storage — Windows](storage-troubleshoot-windows-file-connection-problems.md)
* [Rozwiązywanie problemów z usługą Azure File Storage — Linux](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Migrowanie danych tooAzure pliku](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
