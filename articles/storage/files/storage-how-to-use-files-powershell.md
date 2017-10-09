---
title: "aaaHow toouse PowerShell toomanage magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse toomanage środowiska PowerShell usługi Magazyn plików Azure."
services: storage
documentationcenter: 
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Jak toouse toomanage środowiska PowerShell usługi Magazyn plików Azure
Można użyć programu Azure PowerShell toocreate i Zarządzanie udziałami plików.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Zainstaluj hello poleceń cmdlet programu PowerShell dla usługi Azure Storage
toouse tooprepare programu PowerShell, Pobierz i zainstaluj polecenia cmdlet programu Azure PowerShell hello. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) hello zainstalować instrukcje instalacji i punktu.

> [!NOTE]
> Zaleca się pobrać i zainstalować lub uaktualnić toohello najnowsze modułu Azure PowerShell.
> 
> 

Otwórz okno programu Azure PowerShell, klikając przycisk **Start** i wpisując polecenie **Windows PowerShell**. okno programu PowerShell Hello obliczeniowymi hello modułu Azure Powershell.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Tworzenie kontekstu konta magazynu i klucza
Tworzenie kontekstu konta magazynu hello. kontekst Hello hermetyzuje hello magazynu konta nazwy i klucza konta. Aby uzyskać instrukcje dotyczące kopiowania klucza konta z hello [portalu Azure](https://portal.azure.com), zobacz [wyświetlanie i kopiowanie kluczy dostępu do magazynu](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Zastąp `storage-account-name` i `storage-account-key` z nazwy konta magazynu i klucza w hello poniższy przykład.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Tworzenie nowego udziału plików
Utwórz nowy udział hello, o nazwie `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Masz już udział plików w usłudze Magazyn plików. Teraz dodamy katalog i plik.

> [!IMPORTANT]
> Witaj nazwa udziału plików musi być tylko małe litery. Szczegółowe informacje o nazwach plików i udziałów plików można znaleźć w temacie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Nazywanie i odwoływanie się do udziałów, katalogów, plików i metadanych).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Tworzenie katalogu w udziale plików hello
Tworzenie katalogu w udziale hello. W hello poniższy przykład, nosi nazwę katalogu hello `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Przekazywanie pliku lokalnego katalogu toohello
Teraz można przekazać pliku lokalnego katalogu toohello. Witaj poniższym przykładzie plik zostanie przekazany z `C:\temp\Log1.txt`. Edytuj hello ścieżkę pliku tak, aby wskazywało tooa prawidłowy plik na komputerze lokalnym.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Lista plików hello hello katalogu
toosee hello pliku w katalogu hello, możesz wyświetlić listę wszystkich plików z katalogu hello. To polecenie zwraca hello pliki i podkatalogi (jeśli istnieją) w katalogu CustomLogs hello.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Polecenie Get-AzureStorageFile zwraca listę plików i katalogów dla dowolnego przekazanego obiektu katalogu. "Polecenia get-AzureStorageFile-Share $s" zwraca listę plików i katalogów w katalogu głównym hello. tooget listę plików w podkatalogu, masz hello toopass tooGet polecenia podkatalogu-AzureStorageFile. Jest to czego — pierwsza część polecenia hello zapasowej potoku toohello hello Zwraca wystąpienie katalogu hello podkatalogu CustomLogs. Następnie jest ono przekazywane do polecenia Get-AzureStorageFile, która zwraca hello pliki i katalogi w podkatalogu CustomLogs.

## <a name="copy-files"></a>Kopiowanie plików
Począwszy od wersji 0.9.7 programu Azure PowerShell, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob. Poniżej przedstawiamy, jak tooperform je skopiować operacji za pomocą poleceń cmdlet programu PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Rozwiązywanie problemów w systemie Linux](storage-troubleshoot-linux-file-connection-problems.md)    