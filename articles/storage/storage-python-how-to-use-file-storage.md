---
title: aaaDevelop Azure File Storage z Python | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dane plików toodevelop Python aplikacji i usług, które używają toostore magazyn plików Azure."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Tworzenie dla usługi Magazyn plików Azure języka Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku przedstawiono podstawy hello przy użyciu języka Python toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure. W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem Python i plików platformy Azure:

* Tworzenie udziałów plików Azure
* Tworzenie katalogów
* Wyliczanie plików i katalogów w udziale plików Azure
* Przekazywanie, pobieranie i usuwanie pliku

> [!Note]  
> Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików Azure hello przy użyciu hello standardowe we/wy Python klasy i funkcje. W tym artykule opisano, jak toowrite aplikacji, które używają hello SDK Python magazynu Azure, która używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Konfigurowanie sieci toouse aplikacji usługi Magazyn plików Azure
Dodaj następujące hello górze hello dowolnego pliku źródłowego Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Konfigurowanie połączenia tooAzure magazyn plików 
Witaj `FileService` obiektu umożliwia pracę z udziałów, katalogów i plików. Witaj poniższy kod tworzy `FileService` obiektu przy użyciu hello magazynu konta nazwy i klucza konta. Zastąp `<myaccount>` i `<mykey>` z nazwą konta i klucz.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Tworzenie udziału plików platformy Azure
Poniższy przykład kodu hello, można `FileService` obiektu toocreate hello udziału Jeśli nie istnieje.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Tworzenie katalogu
Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym hello. Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów jako Twoje konto zostanie. Poniższy kod Hello utworzy podkatalogu o nazwie **sampledir** w katalogu głównym hello.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Wyliczanie plików i katalogów w udziale plików Azure
toolist hello plików i katalogów w udziale, użyj hello **listy\_katalogów\_i\_pliki** metody. Ta metoda zwraca generator. Witaj poniższy kod wyświetla hello **nazwa** z poszczególnych plików i katalogów w konsoli toohello udziału.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Przekazywanie pliku 
Azure plik, który zawiera na powitania bardzo najmniej udziału, katalog główny, w którym mogą znajdować się pliki. W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.

toocreate pliku i przekazywania danych, użyj hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` lub `create_file_from_text` metody. Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.

`create_file_from_path`przekazywanie hello zawartość pliku z określonej ścieżki hello i `create_file_from_stream` przekazywania hello zawartość z otwartego pliku/strumienia. `create_file_from_bytes`przekazuje tablicę bajtów, i `create_file_from_text` hello przekazywania podać wartość tekstową przy użyciu hello kodowania (domyślne ustawienia tooUTF-8).

Witaj poniższy przykład przekazuje zawartość hello hello **sunset.png** pliku do hello **mój_plik** pliku.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Pobieranie pliku
toodownload danych z pliku, użyj `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, lub `get_file_to_text`. Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.

Hello poniższym przykładzie pokazano przy użyciu `get_file_to_path` toodownload zawartość hello hello **mój_plik** pliku i zapisz go w toohello **sunset.png poza** pliku.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Usuwanie pliku
Na koniec toodelete pliku, wywołaj `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już jak toomanipulate magazyn plików Azure języka Python, wykonaj te więcej toolearn łącza.

* [Centrum deweloperów języka Python](/develop/python/)
* [Interfejs API REST usług Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Magazyn Microsoft Azure SDK dla języka Python](https://github.com/Azure/azure-storage-python)