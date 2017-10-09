---
title: "toouse aaaHow magazynu obiektów Blob platformy Azure (obiekt magazynu) w języku Python | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Jak toouse magazynu obiektów Blob platformy Azure w języku Python
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

W tym artykule opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob. Witaj przykłady są napisane w języku Python i używają hello [Microsoft Azure magazynu SDK dla języka Python]. omówione scenariusze Hello obejmują przekazywanie, wyświetlanie, pobieranie i usuwanie obiektów blob.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Tworzenie kontenera
Na podstawie typu hello obiektu blob, na które chcesz toouse, Utwórz **BlockBlobService**, **AppendBlobService**, lub **PageBlobService** obiektu. Witaj poniższy kod używa **BlockBlobService** obiektu. Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do magazynu obiektów Blob Azure bloku.

```python
from azure.storage.blob import BlockBlobService
```

Witaj poniższy kod tworzy **BlockBlobService** obiektu przy użyciu hello magazynu konta nazwy i klucza konta.  Zamień "myaccount" i "klucze" Nazwa konta i klucz.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Poniższy przykład kodu hello, można **BlockBlobService** obiektu toocreate hello kontener, jeśli nie istnieje.

```python
block_blob_service.create_container('mycontainer')
```

Domyślnie nowy kontener hello jest prywatny, więc (tak samo jak wcześniej), należy określić klucz dostępu do magazynu obiektów blob toodownload z tego kontenera. Jeśli chcesz obiektów blob hello toomake w tooeveryone dostępne kontenera hello, można utworzyć kontenera hello i przekazać poziom dostępu publicznego hello przy użyciu następującego kodu hello.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Alternatywnie można modyfikować kontenera po utworzeniu go przy użyciu następującego kodu hello.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Po tej zmianie wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale tylko wtedy można zmodyfikować lub usunąć je.

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
toocreate blokowych obiektów blob i przekazywania danych, użyj hello **utworzyć\_obiektu blob\_z\_ścieżki**, **utworzyć\_obiektu blob\_z\_strumienia**, **utworzyć\_obiektu blob\_z\_bajtów** lub **utworzyć\_obiektu blob\_z\_tekst** metody. Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.

**Tworzenie\_obiektu blob\_z\_ścieżki** przekazywania hello zawartość pliku z hello określona ścieżka, i **utworzyć\_obiektu blob\_z\_strumienia** przekazywania hello zawartość z otwartego pliku/strumienia. **Utwórz\_obiektu blob\_z\_bajtów** przekazuje tablicę bajtów, i **utworzyć\_obiektu blob\_z\_tekst** przekazuje hello określony wartość tekstu przy użyciu hello określić kodowania (domyślne ustawienia tooUTF-8).

Witaj poniższy przykład przekazuje zawartość hello hello **sunset.png** pliku do hello **mojblob** obiektu blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, użyj hello **listy\_obiekty BLOB** metody. Ta metoda zwraca generator. Witaj poniższy kod wyświetla hello **nazwa** każdego obiektu blob w kontenerze toohello konsoli.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Pobieranie obiektów blob
toodownload danych z obiektu blob, użyj **uzyskać\_obiektu blob\_do\_ścieżki**, **uzyskać\_obiektu blob\_do\_strumienia**, **pobrać\_obiektu blob\_do\_bajtów**, lub **uzyskać\_obiektu blob\_do\_tekstu**. Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.

Hello poniższym przykładzie pokazano przy użyciu **uzyskać\_obiektu blob\_do\_ścieżki** toodownload zawartość hello hello **mojblob** obiektu blob i zapisz go w toohello **sunset.png poza** pliku.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
Na koniec wywołania toodelete obiektu blob **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Zapisywanie tooan Dołącz obiektów blob
Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie. Podobnie jak blokowy obiekt blob uzupełnialny obiekt blob jest złożony z bloków, ale po dodaniu nowego bloku tooan uzupełnialny obiekt blob jest zawsze toohello dołączany na końcu obiektu blob hello. Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob. Witaj identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.

Każdy blok w uzupełnialnym obiekcie blob może być inny rozmiar się tooa maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać maksymalnie 50 000 bloków. Maksymalny rozmiar uzupełnialnego obiektu blob Hello w związku z tym jest nieco przekraczać 195 GB (4 MB X 50 000 bloków).

w poniższym przykładzie Hello tworzy nowy uzupełnialny obiekt blob i dołącza tooit niektóre dane, symulując prostą operację rejestrowania.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu obiektów Blob hello, wykonaj te więcej toolearn łącza.

* [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/)
* [Interfejs API REST usług Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage]
* [Microsoft Azure magazynu SDK dla języka Python]

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python
