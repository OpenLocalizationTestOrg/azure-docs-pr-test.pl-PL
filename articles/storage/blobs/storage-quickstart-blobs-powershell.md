---
title: "Szybki start platformy Azure — Transferowanie obiektów do usługi Azure Blob Storage i z niej za pomocą programu PowerShell | Microsoft Docs"
description: "Skrócona instrukcja transferowania obiektów do usługi Azure Blob Storage i z niej za pomocą programu PowerShell"
services: storage
documentationcenter: storage
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/19/2017
ms.author: tamram
ms.openlocfilehash: bbc0de7b3a63e8b541a6425e0c7fef9a72dfdffc
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="transfer-objects-tofrom-azure-blob-storage-using-azure-powershell"></a>Transferowanie obiektów do usługi Azure Blob Storage i z niej za pomocą programu Azure PowerShell

Moduł Azure PowerShell umożliwia tworzenie zasobów platformy Azure i zarządzanie nimi za pomocą wiersza polecenia programu PowerShell lub skryptów. Ten przewodnik zawiera informacje na temat wykorzystania programu PowerShell do transferowania plików między dyskiem lokalnym i usługą Azure Blob Storage.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Dla tego przewodnika Szybki start jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej. Uruchom polecenie `Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).

[!INCLUDE [storage-quickstart-tutorial-intro-include-powershell](../../../includes/storage-quickstart-tutorial-intro-include-powershell.md)]

## <a name="create-a-container"></a>Tworzenie kontenera

Obiekty blob są zawsze przesyłane do kontenera. Możesz organizować grupy obiektów blob w sposób podobny do organizowania plików w folderach na komputerze.

Określ nazwę kontenera, a następnie utwórz kontener przy użyciu polecenia [New-AzureStorageContainer](/powershell/module/azure.storage/new-azurestoragecontainer), ustawiając uprawnienia do elementów „blob”, tak aby pozwolić na publiczny dostęp do plików. W tym przykładzie nazwą kontenera jest *quickstartblobs*.

```powershell
$containerName = "quickstartblobs"
New-AzureStorageContainer -Name $containerName -Context $ctx -Permission blob
```

## <a name="upload-blobs-to-the-container"></a>Przekazywanie obiektów blob do kontenera

Usługa Blob Storage obsługuje blokowe, uzupełnialne i stronicowe obiekty blob. Pliki VHD używane do tworzenia kopii maszyn wirtualnych IaaS są stronicowymi obiektami blob. Uzupełnialne obiekty blob są używane do rejestrowania, na przykład w sytuacji, w której konieczny jest zapis do pliku, a następnie dodawanie kolejnych informacji. Większość plików przechowywanych w usłudze Blob Storage to blokowe obiekty blob. 

Aby przekazać plik do blokowego obiektu blob, pobierz odwołanie do kontenera i uzyskaj odwołanie do blokowego obiektu blob w tym kontenerze. Po uzyskaniu odwołania do obiektu blob możesz przekazać do niego dane przy użyciu polecenia [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent). Ta operacja tworzy obiekt blob, jeśli jeszcze nie istnieje, lub zastępuje go, jeśli już istnieje.

Poniższe przykłady umożliwiają przekazanie plików Image001.jpg i Image002.png z folderu D:\\_TestImages na dysku lokalnym do utworzonego kontenera.

```powershell
# upload a file
Set-AzureStorageBlobContent -File "D:\_TestImages\Image001.jpg" `
  -Container $containerName `
  -Blob "Image001.jpg" `
  -Context $ctx 

# upload another file
Set-AzureStorageBlobContent -File "D:\_TestImages\Image002.png" `
  -Container $containerName `
  -Blob "Image002.png" `
  -Context $ctx
```

Przed kontynuowaniem można przesłać dowolną liczbę plików.

## <a name="list-the-blobs-in-a-container"></a>Wyświetlanie listy obiektów blob w kontenerze

Pobierz listę obiektów blob w kontenerze za pomocą polecenia [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob). W tym przykładzie przedstawiono tylko nazwy przekazanych obiektów blob.

```powershell
Get-AzureStorageBlob -Container $ContainerName -Context $ctx | select Name 
```

## <a name="download-blobs"></a>Pobieranie obiektów blob

Pobierz obiekty blob na swój dysk twardy. Dla każdego obiektu blob do pobrania określ nazwę i użyj polecenia [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent), aby pobrać obiekt blob.

W tym przykładzie obiekty blob są pobierane do folderu D:\\_TestImages\Downloads na dysku lokalnym. 

```powershell
# download first blob
Get-AzureStorageBlobContent -Blob "Image001.jpg" `
  -Container $containerName `
  -Destination "D:\_TestImages\Downloads\" `
  -Context $ctx 

# download another blob
Get-AzureStorageBlobContent -Blob "Image002.png" `
  -Container $containerName `
  -Destination "D:\_TestImages\Downloads\" `
  -Context $ctx 
```

## <a name="data-transfer-with-azcopy"></a>Transfer danych przy użyciu narzędzia AzCopy

Narzędzie [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) to kolejna opcja umożliwiająca wydajny transfer danych do usługi Azure Storage z użyciem skryptów. Narzędzia AzCopy można używać do transferu danych do i z magazynu obiektów blob, plików i tabel.

Oto przykładowe polecenie AzCopy umożliwiające przesłanie pliku o nazwie *myfile.txt* do kontenera *mystoragecontainer* w oknie programu PowerShell.

```PowerShell
./AzCopy `
    /Source:C:\myfolder `
    /Dest:https://mystorageaccount.blob.core.windows.net/mystoragecontainer `
    /DestKey:<storage-account-access-key> `
    /Pattern:"myfile.txt"
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Usuń wszystkie utworzone zasoby. Najprostszym sposobem wykonania tego działania jest usunięcie grupy zasobów. Spowoduje to również usunięcie wszystkich zasobów znajdujących się w grupie. W takim przypadku następuje również usunięcie konta magazynu i samej grupy zasobów.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start przedstawiono metodę transferowania plików między dyskiem lokalnym a usługą Azure Blob Storage. Aby dowiedzieć się więcej na temat pracy z usługą Blob Storage, przejdź do instrukcji dotyczących magazynu obiektów blob.

> [!div class="nextstepaction"]
> [Instrukcje: Operacje wykonywane w usłudze Blob Storage](storage-how-to-use-blobs-powershell.md)

### <a name="microsoft-azure-powershell-storage-cmdlets-reference"></a>Dokumentacja poleceń cmdlet programu PowerShell dla usługi Microsoft Azure Storage
* [Polecenia cmdlet programu PowerShell usługi Storage](/powershell/module/azurerm.storage#storage)

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Explorer
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) jest bezpłatną aplikacją autonomiczną oferowaną przez firmę Microsoft, która umożliwia wizualną pracę z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.