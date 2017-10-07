---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy
Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone dla przekazywanie, pobieranie i kopiowanie tooand danych z obiektu blob, plików i magazynowania tabeli Microsoft Azure.

Aby uzyskać instrukcje na temat instalowania programów AzCopy i dodatkowe informacje o użyciu hello platformy Azure, zobacz [wprowadzenie hello wiersza polecenia Azcopy](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Jeśli używasz maszyny Wirtualnej, który został skonfigurowany z dostarczonych przez skrypty hello [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie AzCopy jest już zainstalowana na powitania maszyny Wirtualnej.
> 
> [!NOTE]
> Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Ten dokument założono, że masz subskrypcji platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta. Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.

* tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Uruchom polecenia AzCopy
polecenia narzędzia AzCopy toorun, Otwórz okno polecenia i przejdź katalog instalacyjny AzCopy toohello na komputerze, w którym znajduje się plik wykonywalny AzCopy.exe hello. 

Podstawowa składnia polecenia AzCopy Hello jest:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Możesz dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy i następnie uruchom polecenia hello z dowolnego katalogu. Domyślnie program AzCopy jest zainstalowany za*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* lub *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Przekazywanie plików tooan obiektów blob platformy Azure
tooupload pliku hello Użyj następującego polecenia:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Pobierz pliki z obiektów blob platformy Azure
toodownload pliku z obiektów blob platformy Azure, hello Użyj następującego polecenia:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Transferowania obiektów blob Azure kontenerów
obiekty BLOB tootransfer między Azure kontenery, użyj hello następujące polecenie:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Porady dotyczące używania narzędzia AzCopy
> [!TIP]
> 1. Gdy **przekazywania** pliki, */S* przekazuje rekursywnie plików. Bez tego parametru nie są przekazywane pliki w podkatalogach.  
> 2. Gdy **pobierania** pliku, */S* wyszukiwania hello rekursywnie kontenera, dopóki wszystkie pliki w określonym katalogu hello i jego podkatalogach lub wszystkich plików spełniających hello określony wzorzec w hello podane pobierane są katalogu i jego podkatalogach.  
> 3. Nie można określić **pliku konkretnego obiektu blob** toodownload przy użyciu hello */Source* parametru. toodownload określonego pliku, określ za pomocą hello hello blob pliku nazwę toodownload */wzorca* parametru. **/S** parametr może być używane toohave AzCopy poszukaj rekursywnie wzorzec nazwy pliku. Bez parametru wzorzec hello AzCopy pobiera wszystkie pliki w tym katalogu.
> 
> 

