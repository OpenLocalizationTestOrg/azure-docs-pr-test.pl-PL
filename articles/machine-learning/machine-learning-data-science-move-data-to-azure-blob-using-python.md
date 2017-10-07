---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python
W tym temacie opisano sposób toolist, przekazywanie i pobieranie obiektów blob przy użyciu hello interfejsu API języka Python. Hello udostępniane w zestawie SDK usługi Azure API języka Python możesz:

* Tworzenie kontenera
* Przekazywanie obiektu blob do kontenera
* Pobieranie obiektów blob
* Lista hello BLOB w kontenerze
* Usuwanie obiektu blob

Aby uzyskać więcej informacji o używaniu hello interfejsu API języka Python, zobacz [jak tooUse hello usługi magazynu obiektów Blob w języku Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Jeśli używasz maszyny Wirtualnej, który został skonfigurowany z dostarczonych przez skrypty hello [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie AzCopy jest już zainstalowana na powitania maszyny Wirtualnej.
> 
> [!NOTE]
> Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta. Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.

* tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Przekazywanie danych tooBlob
Dodaj powitania po fragment górze hello dowolnego kodu języka Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure:

    from azure.storage.blob import BlobService

Witaj **BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob. Hello następującego kodu tworzy obiekt BlobService przy użyciu hello magazynu konta nazwy i klucza konta. Zamień na nazwę konta i klucz konta swój rzeczywistych konta i klucz.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Użyj hello następujące metody tooupload danych tooa blob:

1. Umieść\_bloku\_obiektu blob\_z\_ścieżki (przekazuje hello zawartości pliku z określonej ścieżki hello)
2. Umieść\_block_blob\_z\_pliku (przekazuje hello zawartość z otwartego pliku/strumienia)
3. Umieść\_bloku\_obiektu blob\_z\_bajtów (przekazywanie jako tablicę bajtów)
4. Umieść\_bloku\_obiektu blob\_z\_tekst (przekazuje hello określona wartość tekstową przy użyciu hello określonego kodowania)

Witaj następującego przykładowego kodu przekazuje kontenera tooa pliku lokalnego:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Witaj następujący przykładowy kod przekazuje wszystkie pliki hello (z wyjątkiem katalogów) w magazynie tooblob katalogu lokalnego:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Pobierz dane z obiektu Blob
Użyj poniższych metod toodownload danych z obiektu blob hello:

1. Pobierz\_obiektu blob\_do\_ścieżki
2. Pobierz\_obiektu blob\_do\_pliku
3. Pobierz\_obiektu blob\_do\_bajtów
4. Pobierz\_obiektu blob\_do\_tekstu

Te metody, wykonujących hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.

Witaj następujący przykładowy kod pobiera hello zawartość obiektu blob w pliku lokalnym tooa kontenera:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Witaj następujący przykładowy kod pobiera wszystkie obiekty BLOB z kontenera. Używa listy\_obiektów blob tooget hello listę dostępnych obiektów blob w kontenerze hello i pobiera je tooa katalogu lokalnego.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
