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
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="1e879-103">Tworzenie dla usługi Magazyn plików Azure języka Python</span><span class="sxs-lookup"><span data-stu-id="1e879-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="1e879-104">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="1e879-104">About this tutorial</span></span>
<span data-ttu-id="1e879-105">W tym samouczku przedstawiono podstawy hello przy użyciu języka Python toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="1e879-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="1e879-106">W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem Python i plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="1e879-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="1e879-107">Tworzenie udziałów plików Azure</span><span class="sxs-lookup"><span data-stu-id="1e879-107">Create Azure File shares</span></span>
* <span data-ttu-id="1e879-108">Tworzenie katalogów</span><span class="sxs-lookup"><span data-stu-id="1e879-108">Create directories</span></span>
* <span data-ttu-id="1e879-109">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="1e879-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="1e879-110">Przekazywanie, pobieranie i usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="1e879-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="1e879-111">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików Azure hello przy użyciu hello standardowe we/wy Python klasy i funkcje.</span><span class="sxs-lookup"><span data-stu-id="1e879-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="1e879-112">W tym artykule opisano, jak toowrite aplikacji, które używają hello SDK Python magazynu Azure, która używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="1e879-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="1e879-113">Konfigurowanie sieci toouse aplikacji usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="1e879-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="1e879-114">Dodaj następujące hello górze hello dowolnego pliku źródłowego Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e879-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="1e879-115">Konfigurowanie połączenia tooAzure magazyn plików</span><span class="sxs-lookup"><span data-stu-id="1e879-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="1e879-116">Witaj `FileService` obiektu umożliwia pracę z udziałów, katalogów i plików.</span><span class="sxs-lookup"><span data-stu-id="1e879-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="1e879-117">Witaj poniższy kod tworzy `FileService` obiektu przy użyciu hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="1e879-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="1e879-118">Zastąp `<myaccount>` i `<mykey>` z nazwą konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="1e879-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="1e879-119">Tworzenie udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1e879-119">Create an Azure File share</span></span>
<span data-ttu-id="1e879-120">Poniższy przykład kodu hello, można `FileService` obiektu toocreate hello udziału Jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1e879-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="1e879-121">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="1e879-121">Create a directory</span></span>
<span data-ttu-id="1e879-122">Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="1e879-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="1e879-123">Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów jako Twoje konto zostanie.</span><span class="sxs-lookup"><span data-stu-id="1e879-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="1e879-124">Poniższy kod Hello utworzy podkatalogu o nazwie **sampledir** w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="1e879-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="1e879-125">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="1e879-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="1e879-126">toolist hello plików i katalogów w udziale, użyj hello **listy\_katalogów\_i\_pliki** metody.</span><span class="sxs-lookup"><span data-stu-id="1e879-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="1e879-127">Ta metoda zwraca generator.</span><span class="sxs-lookup"><span data-stu-id="1e879-127">This method returns a generator.</span></span> <span data-ttu-id="1e879-128">Witaj poniższy kod wyświetla hello **nazwa** z poszczególnych plików i katalogów w konsoli toohello udziału.</span><span class="sxs-lookup"><span data-stu-id="1e879-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="1e879-129">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="1e879-129">Upload a file</span></span> 
<span data-ttu-id="1e879-130">Azure plik, który zawiera na powitania bardzo najmniej udziału, katalog główny, w którym mogą znajdować się pliki.</span><span class="sxs-lookup"><span data-stu-id="1e879-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="1e879-131">W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.</span><span class="sxs-lookup"><span data-stu-id="1e879-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="1e879-132">toocreate pliku i przekazywania danych, użyj hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` lub `create_file_from_text` metody.</span><span class="sxs-lookup"><span data-stu-id="1e879-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="1e879-133">Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.</span><span class="sxs-lookup"><span data-stu-id="1e879-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="1e879-134">`create_file_from_path`przekazywanie hello zawartość pliku z określonej ścieżki hello i `create_file_from_stream` przekazywania hello zawartość z otwartego pliku/strumienia.</span><span class="sxs-lookup"><span data-stu-id="1e879-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="1e879-135">`create_file_from_bytes`przekazuje tablicę bajtów, i `create_file_from_text` hello przekazywania podać wartość tekstową przy użyciu hello kodowania (domyślne ustawienia tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="1e879-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="1e879-136">Witaj poniższy przykład przekazuje zawartość hello hello **sunset.png** pliku do hello **mój_plik** pliku.</span><span class="sxs-lookup"><span data-stu-id="1e879-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="1e879-137">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="1e879-137">Download a file</span></span>
<span data-ttu-id="1e879-138">toodownload danych z pliku, użyj `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, lub `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="1e879-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="1e879-139">Są one wysokiego poziomu metodach hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.</span><span class="sxs-lookup"><span data-stu-id="1e879-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="1e879-140">Hello poniższym przykładzie pokazano przy użyciu `get_file_to_path` toodownload zawartość hello hello **mój_plik** pliku i zapisz go w toohello **sunset.png poza** pliku.</span><span class="sxs-lookup"><span data-stu-id="1e879-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="1e879-141">Usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="1e879-141">Delete a file</span></span>
<span data-ttu-id="1e879-142">Na koniec toodelete pliku, wywołaj `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="1e879-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="1e879-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e879-143">Next steps</span></span>
<span data-ttu-id="1e879-144">Teraz, kiedy znasz już jak toomanipulate magazyn plików Azure języka Python, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="1e879-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="1e879-145">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="1e879-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="1e879-146">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1e879-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="1e879-147">Magazyn Microsoft Azure SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="1e879-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)