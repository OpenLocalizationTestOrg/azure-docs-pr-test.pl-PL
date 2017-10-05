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
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="da94c-103">Tworzenie dla usługi Magazyn plików Azure języka Python</span><span class="sxs-lookup"><span data-stu-id="da94c-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="da94c-104">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="da94c-104">About this tutorial</span></span>
<span data-ttu-id="da94c-105">W tym samouczku przedstawiono podstawy do tworzenia aplikacji lub usługi, które korzystają z usługi Magazyn plików Azure do przechowywania danych plików za pomocą języka Python.</span><span class="sxs-lookup"><span data-stu-id="da94c-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="da94c-106">W tym samouczku utworzymy prostej aplikacji konsolowej ją i pokazują, jak wykonywać podstawowe działania z magazynem Python i plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="da94c-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="da94c-107">Tworzenie udziałów plików Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-107">Create Azure File shares</span></span>
* <span data-ttu-id="da94c-108">Tworzenie katalogów</span><span class="sxs-lookup"><span data-stu-id="da94c-108">Create directories</span></span>
* <span data-ttu-id="da94c-109">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="da94c-110">Przekazywanie, pobieranie i usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="da94c-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="da94c-111">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, istnieje możliwość zapisu proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure przy użyciu standardowych operacji We/Wy Python klasy i funkcje.</span><span class="sxs-lookup"><span data-stu-id="da94c-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="da94c-112">W tym artykule opisano sposób pisania aplikacji, które używają usługi Azure SDK Python magazynu, która używa [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) aby komunikował się z usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="da94c-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="da94c-113">Konfigurowanie aplikacji do używania usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="da94c-114">Dodaj następujący kod w górnej części dowolnego pliku źródłowego Python mają do uzyskania programowego dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="da94c-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="da94c-115">Konfigurowanie połączenia z magazynem plików Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="da94c-116">`FileService` Obiektu umożliwia pracę z udziałów, katalogów i plików.</span><span class="sxs-lookup"><span data-stu-id="da94c-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="da94c-117">Poniższy kod tworzy `FileService` przy użyciu klucza nazwy i konta konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="da94c-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="da94c-118">Zastąp `<myaccount>` i `<mykey>` z nazwą konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="da94c-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="da94c-119">Tworzenie udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-119">Create an Azure File share</span></span>
<span data-ttu-id="da94c-120">W poniższym przykładzie kodu, można użyć `FileService` obiekt, aby utworzyć udział, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="da94c-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="da94c-121">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="da94c-121">Create a directory</span></span>
<span data-ttu-id="da94c-122">Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="da94c-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="da94c-123">Magazyn plików Azure umożliwia tworzenie katalogów tyle dopuszcza Twoje konto.</span><span class="sxs-lookup"><span data-stu-id="da94c-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="da94c-124">Poniższy kod będzie utworzyć podkatalogu o nazwie **sampledir** w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="da94c-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="da94c-125">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="da94c-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="da94c-126">Aby wyświetlić listę plików i katalogów w udziale, użyj **listy\_katalogów\_i\_pliki** metody.</span><span class="sxs-lookup"><span data-stu-id="da94c-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="da94c-127">Ta metoda zwraca generator.</span><span class="sxs-lookup"><span data-stu-id="da94c-127">This method returns a generator.</span></span> <span data-ttu-id="da94c-128">Poniższy kod wyjścia **nazwa** z poszczególnych plików i katalogów w udziale, do konsoli.</span><span class="sxs-lookup"><span data-stu-id="da94c-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="da94c-129">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="da94c-129">Upload a file</span></span> 
<span data-ttu-id="da94c-130">Plik Azure udział zawiera co najmniej, katalog główny, w którym mogą znajdować się pliki.</span><span class="sxs-lookup"><span data-stu-id="da94c-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="da94c-131">W tej sekcji dowiesz się, jak można przekazać pliku z magazynu lokalnego do katalogu głównego udziału.</span><span class="sxs-lookup"><span data-stu-id="da94c-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="da94c-132">Aby utworzyć plik i przekazywanie danych, użyj `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` lub `create_file_from_text` metody.</span><span class="sxs-lookup"><span data-stu-id="da94c-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="da94c-133">Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.</span><span class="sxs-lookup"><span data-stu-id="da94c-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="da94c-134">`create_file_from_path`wysyła zawartość pliku z określonej ścieżki i `create_file_from_stream` przekazuje zawartość z otwartego pliku/strumienia.</span><span class="sxs-lookup"><span data-stu-id="da94c-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="da94c-135">`create_file_from_bytes`przekazuje tablicę bajtów, i `create_file_from_text` przekazuje wartość określony tekst przy użyciu określonego kodowania (wartość domyślna to UTF-8).</span><span class="sxs-lookup"><span data-stu-id="da94c-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="da94c-136">Poniższy przykład przekazuje zawartość **sunset.png** pliku do **mój_plik** pliku.</span><span class="sxs-lookup"><span data-stu-id="da94c-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="da94c-137">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="da94c-137">Download a file</span></span>
<span data-ttu-id="da94c-138">Aby pobrać dane z pliku, należy użyć `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, lub `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="da94c-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="da94c-139">Są one wysokiego poziomu metodach podziału niezbędne, gdy rozmiar danych przekroczy 64 MB.</span><span class="sxs-lookup"><span data-stu-id="da94c-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="da94c-140">W poniższym przykładzie pokazano, za pomocą `get_file_to_path` do pobrania zawartości **mój_plik** plik i zapisać go do **sunset.png poza** pliku.</span><span class="sxs-lookup"><span data-stu-id="da94c-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="da94c-141">Usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="da94c-141">Delete a file</span></span>
<span data-ttu-id="da94c-142">Na koniec, aby usunąć plik, należy wywołać `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="da94c-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="da94c-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da94c-143">Next steps</span></span>
<span data-ttu-id="da94c-144">Teraz, kiedy znasz już sposobu modyfikowania magazyn plików Azure języka Python, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="da94c-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="da94c-145">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="da94c-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="da94c-146">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="da94c-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="da94c-147">Magazyn Microsoft Azure SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="da94c-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)