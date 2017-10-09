---
title: aaaDevelop Azure File Storage z C++ | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dane plików toodevelop C++ aplikacji i usług, które używają toostore magazyn plików Azure."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="d5129-103">Tworzenie dla usługi Magazyn plików Azure z C++</span><span class="sxs-lookup"><span data-stu-id="d5129-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="d5129-104">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="d5129-104">About this tutorial</span></span>

<span data-ttu-id="d5129-105">W przypadku tego samouczka, dowiesz się, jak tooperform podstawowe operacje na magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d5129-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="d5129-106">Za pomocą przykłady w języku C++, dowiesz się, jak toocreate udziałów i katalogi, przekazywanie, listy i Usuń pliki.</span><span class="sxs-lookup"><span data-stu-id="d5129-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="d5129-107">W przypadku nowego magazynu plików tooAzure pośrednictwa koncepcje hello w kolejnych sekcjach hello będzie zrozumieć przykłady hello przydatne.</span><span class="sxs-lookup"><span data-stu-id="d5129-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="d5129-108">Tworzenie i usuwanie udziałów plików Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="d5129-109">Tworzenie i usuwanie katalogów</span><span class="sxs-lookup"><span data-stu-id="d5129-109">Create and delete directories</span></span>
* <span data-ttu-id="d5129-110">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="d5129-111">Przekazywanie, pobieranie i usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="d5129-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="d5129-112">Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="d5129-113">Utwórz sygnaturę dostępu współdzielonego (SAS klucza) dla pliku, która używa zasad dostępu współdzielonego zdefiniowanych w udziale hello.</span><span class="sxs-lookup"><span data-stu-id="d5129-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="d5129-114">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików Azure hello przy użyciu hello standard C++ we/wy klasy i funkcje.</span><span class="sxs-lookup"><span data-stu-id="d5129-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="d5129-115">W tym artykule opisano, jak toowrite aplikacji, które używają hello Azure C++ zestawu SDK usługi Magazyn, który używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="d5129-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="d5129-116">Tworzenie aplikacji C++</span><span class="sxs-lookup"><span data-stu-id="d5129-116">Create a C++ application</span></span>
<span data-ttu-id="d5129-117">Przykłady hello toobuild, konieczne będzie hello tooinstall 2.4.0 biblioteki klienta magazynu Azure dla języka C++.</span><span class="sxs-lookup"><span data-stu-id="d5129-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="d5129-118">Należy również utworzono konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5129-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="d5129-119">tooinstall powitania klienta magazynu Azure 2.4.0 dla języka C++, można użyć jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="d5129-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="d5129-120">**Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.</span><span class="sxs-lookup"><span data-stu-id="d5129-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="d5129-121">**System Windows:** w programie Visual Studio, kliknij przycisk **narzędzia &gt; Menedżera pakietów NuGet &gt; Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="d5129-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="d5129-122">Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="d5129-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="d5129-123">Konfigurowanie sieci toouse aplikacji usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="d5129-124">Dodaj następujące hello wlicza się toohello instrukcje na początku pliku źródłowego C++ hello miejscu toomanipulate usługi Magazyn plików Azure:</span><span class="sxs-lookup"><span data-stu-id="d5129-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d5129-125">Konfigurowanie parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="d5129-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="d5129-126">toouse pliku magazynu, musisz mieć konto magazynu Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d5129-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="d5129-127">Witaj pierwszym krokiem będzie tooconfigure parametry połączenia, które będą używane konto magazynu tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d5129-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="d5129-128">Umożliwia definiowanie statycznego toodo zmiennej który.</span><span class="sxs-lookup"><span data-stu-id="d5129-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="d5129-129">Łączenie z kontem magazynu platformy Azure tooan</span><span class="sxs-lookup"><span data-stu-id="d5129-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="d5129-130">Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d5129-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="d5129-131">tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="d5129-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="d5129-132">Tworzenie udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-132">Create an Azure File share</span></span>
<span data-ttu-id="d5129-133">Wszystkich plików i katalogów w usłudze magazyn plików Azure znajdują się w kontenerze o nazwie **udziału**.</span><span class="sxs-lookup"><span data-stu-id="d5129-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="d5129-134">Twoje konto magazynu może mieć dowolną liczbę akcji zezwala pojemności Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="d5129-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="d5129-135">tooobtain dostępu tooa udziału i jego zawartość, należy toouse klienta magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d5129-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="d5129-136">Za pomocą klienta magazyn plików Azure hello można następnie uzyskać udziału tooa odwołania.</span><span class="sxs-lookup"><span data-stu-id="d5129-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="d5129-137">toocreate hello udziału, użyj hello **create_if_not_exists** metody hello **cloud_file_share** obiektu.</span><span class="sxs-lookup"><span data-stu-id="d5129-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="d5129-138">W tym momencie **udostępnianie** posiada udział tooa odwołania o nazwie **Moje udziału próbki**.</span><span class="sxs-lookup"><span data-stu-id="d5129-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="d5129-139">Usuń udział plików Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-139">Delete an Azure File share</span></span>
<span data-ttu-id="d5129-140">Usuwanie udziału jest realizowane przez wywołanie hello **delete_if_exists** metody dla obiekt cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="d5129-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="d5129-141">Oto przykładowy kod, który robi to.</span><span class="sxs-lookup"><span data-stu-id="d5129-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="d5129-142">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="d5129-142">Create a directory</span></span>
<span data-ttu-id="d5129-143">Magazyn można organizować przez umieszczenie plików w podkatalogach zamiast wszystkich z nich w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="d5129-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="d5129-144">Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów jako Twoje konto zostanie.</span><span class="sxs-lookup"><span data-stu-id="d5129-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="d5129-145">Poniższy kod Hello utworzy katalog o nazwie **Moje katalog przykładu** w obszarze katalogu głównego hello, a także podkatalogu o nazwie **Moje podkatalogu próbki**.</span><span class="sxs-lookup"><span data-stu-id="d5129-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="d5129-146">Usuwanie katalogu</span><span class="sxs-lookup"><span data-stu-id="d5129-146">Delete a directory</span></span>
<span data-ttu-id="d5129-147">Usunięcie katalogu jest prostym zadaniem, chociaż należy zauważyć, że nie można usunąć katalogu, w którym nadal zawiera pliki lub katalogi innych.</span><span class="sxs-lookup"><span data-stu-id="d5129-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="d5129-148">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="d5129-149">Uzyskiwanie listy plików i katalogów w udziale łatwo odbywa się przez wywołanie metody **list_files_and_directories** na **cloud_file_directory** odwołania.</span><span class="sxs-lookup"><span data-stu-id="d5129-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="d5129-150">bogaty zestaw właściwości i metod zwróconego hello tooaccess **list_file_and_directory_item**, należy wywołać hello **list_file_and_directory_item.as_file** tooget metody **cloud_ plik** obiektu lub hello **list_file_and_directory_item.as_directory** tooget metody **cloud_file_directory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="d5129-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="d5129-151">Witaj następującego kodu pokazano, jak tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w katalogu głównym hello hello udziału.</span><span class="sxs-lookup"><span data-stu-id="d5129-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="d5129-152">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="d5129-152">Upload a file</span></span>
<span data-ttu-id="d5129-153">W bardzo hello najmniej udział plików Azure zawiera katalog główny, w którym mogą znajdować się pliki.</span><span class="sxs-lookup"><span data-stu-id="d5129-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="d5129-154">W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.</span><span class="sxs-lookup"><span data-stu-id="d5129-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="d5129-155">pierwszym krokiem Hello przekazywania pliku jest tooobtain katalogu toohello odwołania, gdzie powinien znajdować się.</span><span class="sxs-lookup"><span data-stu-id="d5129-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="d5129-156">W tym celu wywoływania hello **get_root_directory_reference** metody hello udziału obiektu.</span><span class="sxs-lookup"><span data-stu-id="d5129-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="d5129-157">Teraz, gdy masz katalog główny odwołania toohello hello udziału, możesz przekazać plik na niego.</span><span class="sxs-lookup"><span data-stu-id="d5129-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="d5129-158">W tym przykładzie zostanie przesłany z pliku, tekst i ze strumienia.</span><span class="sxs-lookup"><span data-stu-id="d5129-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="d5129-159">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="d5129-159">Download a file</span></span>
<span data-ttu-id="d5129-160">pliki toodownload najpierw pobrać odwołanie do pliku, a następnie wywołać hello **download_to_stream** metody tootransfer hello pliku zawartość tooa strumienia obiektu, który można następnie zachować tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="d5129-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="d5129-161">Alternatywnie można użyć hello **download_to_file** metody toodownload hello zawartości pliku lokalnego tooa pliku.</span><span class="sxs-lookup"><span data-stu-id="d5129-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="d5129-162">Można użyć hello **download_text** metody toodownload hello zawartość pliku jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="d5129-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="d5129-163">Witaj poniższym przykładzie użyto hello **download_to_stream** i **download_text** toodemonstrate metod pobierania hello pliki, które zostały utworzone w poprzednich sekcjach.</span><span class="sxs-lookup"><span data-stu-id="d5129-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="d5129-164">Usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="d5129-164">Delete a file</span></span>
<span data-ttu-id="d5129-165">Inna operacja magazynu plików Azure wspólnej jest usuwanie plików.</span><span class="sxs-lookup"><span data-stu-id="d5129-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="d5129-166">Witaj następujący kod usuwa plik o nazwie my próbki pliku-3 przechowywane w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="d5129-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="d5129-167">Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5129-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="d5129-168">Można ustawić przydziału hello (lub maksymalny rozmiar) udziału plików w gigabajtach.</span><span class="sxs-lookup"><span data-stu-id="d5129-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="d5129-169">Można również sprawdzić, jak dużo danych jest obecnie przechowywanych w udziale hello toosee.</span><span class="sxs-lookup"><span data-stu-id="d5129-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="d5129-170">Przez ustawienie hello limitu przydziału dla udziału można ograniczyć całkowity rozmiar plików hello przechowywanych w udziale hello hello.</span><span class="sxs-lookup"><span data-stu-id="d5129-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="d5129-171">Jeśli całkowity rozmiar plików w udziale hello hello przekracza przydział hello ustawiony na powitania udziału, a następnie klienci będą tooincrease hello rozmiaru istniejących plików lub tworzenia nowych plików, chyba że te pliki są puste.</span><span class="sxs-lookup"><span data-stu-id="d5129-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="d5129-172">w poniższym przykładzie Hello pokazuje, jak toocheck hello bieżące użycie udziału oraz jak tooset hello przydziału udziału hello.</span><span class="sxs-lookup"><span data-stu-id="d5129-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="d5129-173">Generowanie sygnatury dostępu współdzielonego dla pliku lub udziału plików</span><span class="sxs-lookup"><span data-stu-id="d5129-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="d5129-174">Możesz wygenerować sygnaturę dostępu współdzielonego (SAS) dla udziału plików lub dla pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="d5129-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="d5129-175">Można również tworzyć zasady dostępu współużytkowanego na dostęp do udostępnionych toomanage udziału plików podpisy.</span><span class="sxs-lookup"><span data-stu-id="d5129-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="d5129-176">Tworzenie zasad dostępu współdzielonego jest zalecane, ponieważ umożliwia cofnięcie hello SAS, jeśli powinien być zagrożone.</span><span class="sxs-lookup"><span data-stu-id="d5129-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="d5129-177">Hello poniższy przykład tworzy zasady dostępu współdzielonego w udziale, a następnie używa, że zasady tooprovide hello ograniczenia na sygnatury dostępu Współdzielonego w pliku w hello udostępniać.</span><span class="sxs-lookup"><span data-stu-id="d5129-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="d5129-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5129-178">Next steps</span></span>
<span data-ttu-id="d5129-179">toolearn więcej informacji na temat usługi Azure Storage, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="d5129-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="d5129-180">Biblioteka klienta usługi Storage dla języka C++</span><span class="sxs-lookup"><span data-stu-id="d5129-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="d5129-181">[Magazynu azure pliku usługi przykłady w języku C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="d5129-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="d5129-182">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="d5129-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="d5129-183">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d5129-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)