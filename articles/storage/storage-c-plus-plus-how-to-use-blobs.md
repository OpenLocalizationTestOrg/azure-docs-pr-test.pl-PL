---
title: aaaHow toouse obiektu blob magazynu (obiekt) z C++ | Dokumentacja firmy Microsoft
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="3d4f2-103">Jak toouse magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="3d4f2-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="3d4f2-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3d4f2-104">Overview</span></span>
<span data-ttu-id="3d4f2-105">Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="3d4f2-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="3d4f2-107">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="3d4f2-108">W tym przewodniku przedstawiono sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="3d4f2-109">Hello przykłady są napisane w języku C++ i używają hello [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f2-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="3d4f2-110">Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="3d4f2-111">Cele tego przewodnika hello biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="3d4f2-112">Hello zalecana jest wersja biblioteki klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="3d4f2-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="3d4f2-113">Tworzenie aplikacji C++</span><span class="sxs-lookup"><span data-stu-id="3d4f2-113">Create a C++ application</span></span>
<span data-ttu-id="3d4f2-114">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="3d4f2-115">toodo tak, konieczne będzie tooinstall hello biblioteki klienta magazynu Azure dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="3d4f2-116">Witaj tooinstall biblioteki klienta magazynu Azure dla języka C++, można użyć hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="3d4f2-117">**Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="3d4f2-118">**System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="3d4f2-119">Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="3d4f2-120">Pakiet instalacyjny wastorage</span><span class="sxs-lookup"><span data-stu-id="3d4f2-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="3d4f2-121">Konfigurowanie sieci tooaccess aplikacji magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="3d4f2-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="3d4f2-122">Dodaj wlicza się hello następujące instrukcje toohello górnej części pliku C++ hello miejscu obiekty BLOB tooaccess interfejsów API toouse hello magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="3d4f2-123">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="3d4f2-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="3d4f2-124">Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="3d4f2-125">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, używając hello nazwę konta i hello magazynu klucz dostępu do magazynu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="3d4f2-126">Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f2-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="3d4f2-127">Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="3d4f2-128">tootest aplikacji w lokalnym komputerze z systemem Windows, można użyć hello Microsoft Azure [emulatora magazynu](storage-use-emulator.md) zainstalowane z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3d4f2-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="3d4f2-129">emulator magazynu Hello jest narzędziem, która symuluje hello dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="3d4f2-130">Witaj poniższym przykładzie pokazano, jak można zadeklarować pola statycznego toohold hello połączenia ciąg tooyour lokalnym emulatorze magazynu:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="3d4f2-131">emulatora magazynu Azure hello toostart, wybierz opcję hello **Start** hello przycisk lub naciśnij przycisk **Windows** klucza.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="3d4f2-132">Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z hello listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="3d4f2-133">Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="3d4f2-134">Pobranie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="3d4f2-134">Retrieve your connection string</span></span>
<span data-ttu-id="3d4f2-135">Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="3d4f2-136">tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="3d4f2-137">Następnie Pobierz tooa odwołanie **cloud_blob_client** klasa umożliwia tooretrieve obiektów, które reprezentują kontenery i obiekty BLOB przechowywane w ramach hello usługi magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="3d4f2-138">Witaj poniższy kod tworzy **cloud_blob_client** obiektu przy użyciu obiektu konta magazynu hello możemy pobrać powyżej:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="3d4f2-139">Porady: Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="3d4f2-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="3d4f2-140">W tym przykładzie pokazano sposób toocreate kontenera, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="3d4f2-141">Domyślnie nowy kontener hello jest prywatny i należy określić obiektów blob toodownload klucza dostępu do magazynu z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="3d4f2-142">Jeśli chcesz toomake hello plików (BLOB) w ramach tooeveryone dostępne kontenera hello toobe kontenera hello można ustawić publiczny przy użyciu następującego kodu hello:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="3d4f2-143">Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="3d4f2-144">Porady: przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="3d4f2-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="3d4f2-145">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="3d4f2-146">W większości przypadków hello blokowych obiektów blob jest hello zalecane toouse typu.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="3d4f2-147">tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="3d4f2-148">Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **upload_from_stream** metody.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="3d4f2-149">Ta operacja spowoduje utworzenie obiektu blob hello, jeśli on nie istnieje, lub go zastąpić, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="3d4f2-150">powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="3d4f2-151">Alternatywnie można użyć hello **upload_from_file** tooupload metody tooa pliku blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="3d4f2-152">Porady: wyświetlanie obiektów blob hello w kontenerze</span><span class="sxs-lookup"><span data-stu-id="3d4f2-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="3d4f2-153">toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="3d4f2-154">Można użyć kontenera hello **list_blobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="3d4f2-155">tooaccess hello bogatego zestawu właściwości i metod zwróconego **list_blob_item**, należy wywołać hello **list_blob_item.as_blob** tooget metody **cloud_blob** obiektu lub hello **list_blob.as_directory** tooget metody obiektu cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="3d4f2-156">Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello **Moje kontenera próbki** kontenera:</span><span class="sxs-lookup"><span data-stu-id="3d4f2-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="3d4f2-157">Więcej szczegółów na listę działań, zobacz [listy zasobów magazynu Azure w języku C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f2-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="3d4f2-158">Porady: pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3d4f2-158">How to: Download blobs</span></span>
<span data-ttu-id="3d4f2-159">obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **download_to_stream** metody.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="3d4f2-160">Witaj poniższym przykładzie użyto hello **download_to_stream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="3d4f2-161">Alternatywnie można użyć hello **download_to_file** metody toodownload hello zawartości pliku tooa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="3d4f2-162">Ponadto można również użyć hello **download_text** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="3d4f2-163">Porady: usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3d4f2-163">How to: Delete blobs</span></span>
<span data-ttu-id="3d4f2-164">toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **delete_blob** dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="3d4f2-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d4f2-165">Next steps</span></span>
<span data-ttu-id="3d4f2-166">Teraz, kiedy znasz już podstawy magazynu obiektów blob hello, wykonaj te toolearn łącza więcej informacji na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="3d4f2-167">Jak toouse magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="3d4f2-167">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="3d4f2-168">Jak toouse magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="3d4f2-168">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="3d4f2-169">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="3d4f2-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="3d4f2-170">Biblioteka klienta usługi Storage for C++ — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="3d4f2-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="3d4f2-171">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3d4f2-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="3d4f2-172">Transfer danych za pomocą hello wiersza polecenia azcopy</span><span class="sxs-lookup"><span data-stu-id="3d4f2-172">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

