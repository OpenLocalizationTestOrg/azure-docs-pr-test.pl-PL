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
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="a7b06-103">Jak toouse magazynu obiektów Blob platformy Azure w języku Python</span><span class="sxs-lookup"><span data-stu-id="a7b06-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a7b06-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a7b06-104">Overview</span></span>
<span data-ttu-id="a7b06-105">Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="a7b06-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7b06-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a7b06-107">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="a7b06-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="a7b06-108">W tym artykule opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="a7b06-109">Witaj przykłady są napisane w języku Python i używają hello [Microsoft Azure magazynu SDK dla języka Python].</span><span class="sxs-lookup"><span data-stu-id="a7b06-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="a7b06-110">omówione scenariusze Hello obejmują przekazywanie, wyświetlanie, pobieranie i usuwanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="a7b06-111">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="a7b06-111">Create a container</span></span>
<span data-ttu-id="a7b06-112">Na podstawie typu hello obiektu blob, na które chcesz toouse, Utwórz **BlockBlobService**, **AppendBlobService**, lub **PageBlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="a7b06-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="a7b06-113">Witaj poniższy kod używa **BlockBlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="a7b06-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="a7b06-114">Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do magazynu obiektów Blob Azure bloku.</span><span class="sxs-lookup"><span data-stu-id="a7b06-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="a7b06-115">Witaj poniższy kod tworzy **BlockBlobService** obiektu przy użyciu hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="a7b06-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="a7b06-116">Zamień "myaccount" i "klucze" Nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="a7b06-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a7b06-117">Poniższy przykład kodu hello, można **BlockBlobService** obiektu toocreate hello kontener, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a7b06-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="a7b06-118">Domyślnie nowy kontener hello jest prywatny, więc (tak samo jak wcześniej), należy określić klucz dostępu do magazynu obiektów blob toodownload z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="a7b06-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="a7b06-119">Jeśli chcesz obiektów blob hello toomake w tooeveryone dostępne kontenera hello, można utworzyć kontenera hello i przekazać poziom dostępu publicznego hello przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="a7b06-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="a7b06-120">Alternatywnie można modyfikować kontenera po utworzeniu go przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="a7b06-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="a7b06-121">Po tej zmianie wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale tylko wtedy można zmodyfikować lub usunąć je.</span><span class="sxs-lookup"><span data-stu-id="a7b06-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a7b06-122">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="a7b06-122">Upload a blob into a container</span></span>
<span data-ttu-id="a7b06-123">toocreate blokowych obiektów blob i przekazywania danych, użyj hello **utworzyć\_obiektu blob\_z\_ścieżki**, **utworzyć\_obiektu blob\_z\_strumienia**, **utworzyć\_obiektu blob\_z\_bajtów** lub **utworzyć\_obiektu blob\_z\_tekst** metody.</span><span class="sxs-lookup"><span data-stu-id="a7b06-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="a7b06-124">Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.</span><span class="sxs-lookup"><span data-stu-id="a7b06-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a7b06-125">**Tworzenie\_obiektu blob\_z\_ścieżki** przekazywania hello zawartość pliku z hello określona ścieżka, i **utworzyć\_obiektu blob\_z\_strumienia** przekazywania hello zawartość z otwartego pliku/strumienia.</span><span class="sxs-lookup"><span data-stu-id="a7b06-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="a7b06-126">**Utwórz\_obiektu blob\_z\_bajtów** przekazuje tablicę bajtów, i **utworzyć\_obiektu blob\_z\_tekst** przekazuje hello określony wartość tekstu przy użyciu hello określić kodowania (domyślne ustawienia tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="a7b06-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="a7b06-127">Witaj poniższy przykład przekazuje zawartość hello hello **sunset.png** pliku do hello **mojblob** obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="a7b06-128">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="a7b06-128">List hello blobs in a container</span></span>
<span data-ttu-id="a7b06-129">toolist hello BLOB w kontenerze, użyj hello **listy\_obiekty BLOB** metody.</span><span class="sxs-lookup"><span data-stu-id="a7b06-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="a7b06-130">Ta metoda zwraca generator.</span><span class="sxs-lookup"><span data-stu-id="a7b06-130">This method returns a generator.</span></span> <span data-ttu-id="a7b06-131">Witaj poniższy kod wyświetla hello **nazwa** każdego obiektu blob w kontenerze toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="a7b06-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="a7b06-132">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a7b06-132">Download blobs</span></span>
<span data-ttu-id="a7b06-133">toodownload danych z obiektu blob, użyj **uzyskać\_obiektu blob\_do\_ścieżki**, **uzyskać\_obiektu blob\_do\_strumienia**, **pobrać\_obiektu blob\_do\_bajtów**, lub **uzyskać\_obiektu blob\_do\_tekstu**.</span><span class="sxs-lookup"><span data-stu-id="a7b06-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="a7b06-134">Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.</span><span class="sxs-lookup"><span data-stu-id="a7b06-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a7b06-135">Hello poniższym przykładzie pokazano przy użyciu **uzyskać\_obiektu blob\_do\_ścieżki** toodownload zawartość hello hello **mojblob** obiektu blob i zapisz go w toohello **sunset.png poza** pliku.</span><span class="sxs-lookup"><span data-stu-id="a7b06-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="a7b06-136">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="a7b06-136">Delete a blob</span></span>
<span data-ttu-id="a7b06-137">Na koniec wywołania toodelete obiektu blob **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="a7b06-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="a7b06-138">Zapisywanie tooan Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a7b06-138">Writing tooan append blob</span></span>
<span data-ttu-id="a7b06-139">Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="a7b06-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="a7b06-140">Podobnie jak blokowy obiekt blob uzupełnialny obiekt blob jest złożony z bloków, ale po dodaniu nowego bloku tooan uzupełnialny obiekt blob jest zawsze toohello dołączany na końcu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="a7b06-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="a7b06-141">Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="a7b06-142">Witaj identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="a7b06-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="a7b06-143">Każdy blok w uzupełnialnym obiekcie blob może być inny rozmiar się tooa maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać maksymalnie 50 000 bloków.</span><span class="sxs-lookup"><span data-stu-id="a7b06-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="a7b06-144">Maksymalny rozmiar uzupełnialnego obiektu blob Hello w związku z tym jest nieco przekraczać 195 GB (4 MB X 50 000 bloków).</span><span class="sxs-lookup"><span data-stu-id="a7b06-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="a7b06-145">w poniższym przykładzie Hello tworzy nowy uzupełnialny obiekt blob i dołącza tooit niektóre dane, symulując prostą operację rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="a7b06-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7b06-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7b06-146">Next steps</span></span>
<span data-ttu-id="a7b06-147">Teraz, kiedy znasz już podstawy magazynu obiektów Blob hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="a7b06-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="a7b06-148">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="a7b06-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="a7b06-149">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a7b06-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a7b06-150">[Blog zespołu odpowiedzialnego za usługę Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="a7b06-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="a7b06-151">[Microsoft Azure magazynu SDK dla języka Python]</span><span class="sxs-lookup"><span data-stu-id="a7b06-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python
