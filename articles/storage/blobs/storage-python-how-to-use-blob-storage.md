---
title: "Jak używać magazynu obiektów Blob platformy Azure (obiekt magazynu) w języku Python | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
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
ms.openlocfilehash: 1cab8407be6fc8932b68e50d0c301e8ea37ea3ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="f152c-103">Jak używać magazynu obiektów Blob platformy Azure w języku Python</span><span class="sxs-lookup"><span data-stu-id="f152c-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="f152c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f152c-104">Overview</span></span>
<span data-ttu-id="f152c-105">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="f152c-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f152c-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f152c-107">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="f152c-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="f152c-108">W tym artykule opisano sposób wykonywania typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="f152c-109">Próbki są napisane w języku Python i użyj [Microsoft Azure magazynu SDK dla języka Python].</span><span class="sxs-lookup"><span data-stu-id="f152c-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="f152c-110">Omówione scenariusze obejmują przekazywanie, wyświetlanie, pobieranie i usuwanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="f152c-111">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="f152c-111">Create a container</span></span>
<span data-ttu-id="f152c-112">Utwórz na podstawie typu obiektu blob, które chcesz użyć, **BlockBlobService**, **AppendBlobService**, lub **PageBlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f152c-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="f152c-113">Poniższy kod używa **BlockBlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f152c-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="f152c-114">Dodaj następujący kod w górnej części każdego pliku Python, w którym chcesz uzyskania programowego dostępu do magazynu obiektów Blob Azure bloku.</span><span class="sxs-lookup"><span data-stu-id="f152c-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="f152c-115">Poniższy kod tworzy **BlockBlobService** przy użyciu klucza nazwy i konta konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f152c-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="f152c-116">Zamień "myaccount" i "klucze" Nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="f152c-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f152c-117">W poniższym przykładzie kodu, można użyć **BlockBlobService** obiekt, aby utworzyć kontener, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f152c-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="f152c-118">Domyślnie nowy kontener jest prywatny, dlatego należy określić klucz dostępu do magazynu (tak samo jak wcześniej) aby pobierać obiekty BLOB z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="f152c-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="f152c-119">Jeśli chcesz udostępnić wszystkim obiekty BLOB w kontenerze, można utworzyć kontenera i przekazać poziom dostępu publicznego, używając następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="f152c-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="f152c-120">Alternatywnie można modyfikować kontenera po utworzeniu go przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="f152c-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="f152c-121">Po tej zmianie wszyscy użytkownicy Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale tylko wtedy można zmodyfikować lub usunąć je.</span><span class="sxs-lookup"><span data-stu-id="f152c-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f152c-122">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="f152c-122">Upload a blob into a container</span></span>
<span data-ttu-id="f152c-123">Aby utworzyć blokowych obiektów blob i przekazywanie danych, użyj **utworzyć\_obiektów blob\_z\_ścieżki**, **utworzyć\_obiektów blob\_z\_strumienia**, **utworzyć\_obiektu blob\_z\_bajtów** lub **utworzyć\_obiektu blob\_z\_tekst** metody.</span><span class="sxs-lookup"><span data-stu-id="f152c-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="f152c-124">Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.</span><span class="sxs-lookup"><span data-stu-id="f152c-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="f152c-125">**Utwórz\_obiektu blob\_z\_ścieżki** wysyła zawartość pliku z określonej ścieżki i **utworzyć\_obiektu blob\_z\_strumienia** przekazuje zawartość z otwartego pliku/strumienia.</span><span class="sxs-lookup"><span data-stu-id="f152c-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="f152c-126">**Utwórz\_obiektu blob\_z\_bajtów** przekazuje tablicę bajtów, i **utworzyć\_obiektu blob\_z\_tekst** przekazuje wartość określony tekst przy użyciu określonego kodowania (wartość domyślna to UTF-8).</span><span class="sxs-lookup"><span data-stu-id="f152c-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="f152c-127">Poniższy przykład przekazuje zawartość **sunset.png** pliku do **mojblob** obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f152c-128">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="f152c-128">List the blobs in a container</span></span>
<span data-ttu-id="f152c-129">Aby wyświetlić listę obiektów blob w kontenerze, należy użyć **listy\_obiekty BLOB** metody.</span><span class="sxs-lookup"><span data-stu-id="f152c-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="f152c-130">Ta metoda zwraca generator.</span><span class="sxs-lookup"><span data-stu-id="f152c-130">This method returns a generator.</span></span> <span data-ttu-id="f152c-131">Poniższy kod wyjścia **nazwa** każdego obiektu blob w kontenerze do konsoli.</span><span class="sxs-lookup"><span data-stu-id="f152c-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="f152c-132">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f152c-132">Download blobs</span></span>
<span data-ttu-id="f152c-133">Podczas pobierania danych z obiektu blob, użyj **uzyskać\_obiektów blob\_do\_ścieżki**, **uzyskać\_obiektów blob\_do\_strumienia**, **uzyskać\_obiektu blob\_do\_bajtów**, lub **uzyskać\_obiektu blob\_do\_tekstu**.</span><span class="sxs-lookup"><span data-stu-id="f152c-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="f152c-134">Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.</span><span class="sxs-lookup"><span data-stu-id="f152c-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="f152c-135">W poniższym przykładzie pokazano, za pomocą **uzyskać\_obiektu blob\_do\_ścieżki** do pobrania zawartości **mojblob** obiektu blob i zapisze go do **sunset.png poza** pliku.</span><span class="sxs-lookup"><span data-stu-id="f152c-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="f152c-136">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f152c-136">Delete a blob</span></span>
<span data-ttu-id="f152c-137">Na koniec można usunąć obiektu blob, należy wywołać **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="f152c-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="f152c-138">Zapisywanie do uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f152c-138">Writing to an append blob</span></span>
<span data-ttu-id="f152c-139">Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="f152c-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="f152c-140">Podobnie jak blokowy obiekt blob, uzupełnialny obiekt blob jest złożony z bloków, ale nowy blok dodany do uzupełnialnego obiektu blob jest zawsze dołączany na końcu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="f152c-141">Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="f152c-142">Identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f152c-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="f152c-143">Każdy blok w uzupełnialnym obiekcie blob może różnić się rozmiarem, który może wynosić maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać do 50 000 bloków.</span><span class="sxs-lookup"><span data-stu-id="f152c-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="f152c-144">Z tego względu maksymalny rozmiar uzupełnialnego obiektu blob nieznacznie przekracza 195 GB (4 MB X 50 000 bloków).</span><span class="sxs-lookup"><span data-stu-id="f152c-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="f152c-145">W poniższym przykładzie utworzono nowy uzupełnialny obiekt blob i dołączono do niego określone dane, symulując prostą operację rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="f152c-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="f152c-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f152c-146">Next steps</span></span>
<span data-ttu-id="f152c-147">Teraz, kiedy znasz już podstawy usługi Blob Storage, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="f152c-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="f152c-148">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="f152c-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="f152c-149">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f152c-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="f152c-150">[Blog zespołu odpowiedzialnego za usługę Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="f152c-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="f152c-151">[Microsoft Azure magazynu SDK dla języka Python]</span><span class="sxs-lookup"><span data-stu-id="f152c-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python
