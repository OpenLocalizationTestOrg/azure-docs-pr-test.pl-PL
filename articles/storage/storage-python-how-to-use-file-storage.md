---
title: "Tworzenie dla języka Python usługi Magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrażać aplikacje Python i usług korzystających z usługi Magazyn plików Azure do przechowywania plików danych."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Tworzenie dla usługi Magazyn plików Azure języka Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku przedstawiono podstawy do tworzenia aplikacji lub usługi, które korzystają z usługi Magazyn plików Azure do przechowywania danych plików za pomocą języka Python. W tym samouczku utworzymy prostej aplikacji konsolowej ją i pokazują, jak wykonywać podstawowe działania z magazynem Python i plików platformy Azure:

* Tworzenie udziałów plików Azure
* Tworzenie katalogów
* Wyliczanie plików i katalogów w udziale plików Azure
* Przekazywanie, pobieranie i usuwanie pliku

> [!Note]  
> Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, istnieje możliwość zapisu proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure przy użyciu standardowych operacji We/Wy Python klasy i funkcje. W tym artykule opisano sposób pisania aplikacji, które używają usługi Azure SDK Python magazynu, która używa [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) aby komunikował się z usługi Magazyn plików Azure.

### <a name="set-up-your-application-to-use-azure-file-storage"></a>Konfigurowanie aplikacji do używania usługi Magazyn plików Azure
Dodaj następujący kod w górnej części dowolnego pliku źródłowego Python mają do uzyskania programowego dostępu do magazynu Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>Konfigurowanie połączenia z magazynem plików Azure 
`FileService` Obiektu umożliwia pracę z udziałów, katalogów i plików. Poniższy kod tworzy `FileService` przy użyciu klucza nazwy i konta konta magazynu. Zastąp `<myaccount>` i `<mykey>` z nazwą konta i klucz.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Tworzenie udziału plików platformy Azure
W poniższym przykładzie kodu, można użyć `FileService` obiekt, aby utworzyć udział, jeśli nie istnieje.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Tworzenie katalogu
Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym. Magazyn plików Azure umożliwia tworzenie katalogów tyle dopuszcza Twoje konto. Poniższy kod będzie utworzyć podkatalogu o nazwie **sampledir** w katalogu głównym.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Wyliczanie plików i katalogów w udziale plików Azure
Aby wyświetlić listę plików i katalogów w udziale, użyj **listy\_katalogów\_i\_pliki** metody. Ta metoda zwraca generator. Poniższy kod wyjścia **nazwa** z poszczególnych plików i katalogów w udziale, do konsoli.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Przekazywanie pliku 
Plik Azure udział zawiera co najmniej, katalog główny, w którym mogą znajdować się pliki. W tej sekcji dowiesz się, jak można przekazać pliku z magazynu lokalnego do katalogu głównego udziału.

Aby utworzyć plik i przekazywanie danych, użyj `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` lub `create_file_from_text` metody. Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.

`create_file_from_path`wysyła zawartość pliku z określonej ścieżki i `create_file_from_stream` przekazuje zawartość z otwartego pliku/strumienia. `create_file_from_bytes`przekazuje tablicę bajtów, i `create_file_from_text` przekazuje wartość określony tekst przy użyciu określonego kodowania (wartość domyślna to UTF-8).

Poniższy przykład przekazuje zawartość **sunset.png** pliku do **mój_plik** pliku.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Pobieranie pliku
Aby pobrać dane z pliku, należy użyć `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, lub `get_file_to_text`. Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.

W poniższym przykładzie pokazano, za pomocą `get_file_to_path` do pobrania zawartości **mój_plik** plik i zapisać go do **sunset.png poza** pliku.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Usuwanie pliku
Na koniec, aby usunąć plik, należy wywołać `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już sposobu modyfikowania magazyn plików Azure języka Python, skorzystaj z poniższych linków, aby dowiedzieć się więcej.

* [Centrum deweloperów języka Python](/develop/python/)
* [Interfejs API REST usług Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Magazyn Microsoft Azure SDK dla języka Python](https://github.com/Azure/azure-storage-python)