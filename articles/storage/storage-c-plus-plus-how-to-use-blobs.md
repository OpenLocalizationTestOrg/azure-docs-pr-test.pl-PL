---
title: "Jak używać magazynu obiektów blob (magazyn obiektu) z C++ | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
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
ms.openlocfilehash: 3f28fbee4e267ab6962e2f73af5af6461cc16448
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="254d8-103">Jak używać magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="254d8-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="254d8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="254d8-104">Overview</span></span>
<span data-ttu-id="254d8-105">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="254d8-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="254d8-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="254d8-107">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="254d8-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="254d8-108">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="254d8-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="254d8-109">Przykłady są napisane w C++ i użyj [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="254d8-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="254d8-110">Omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="254d8-111">Ten przewodnik jest przeznaczony dla biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="254d8-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="254d8-112">Zalecana wersja jest biblioteka klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="254d8-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="254d8-113">Tworzenie aplikacji C++</span><span class="sxs-lookup"><span data-stu-id="254d8-113">Create a C++ application</span></span>
<span data-ttu-id="254d8-114">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.</span><span class="sxs-lookup"><span data-stu-id="254d8-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="254d8-115">Aby to zrobić, należy zainstalować bibliotekę klienta usługi Azure Storage dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="254d8-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="254d8-116">Aby zainstalować bibliotekę klienta usługi Azure Storage dla języka C++, można użyć następujących metod:</span><span class="sxs-lookup"><span data-stu-id="254d8-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="254d8-117">**Linux:** postępuj zgodnie z instrukcjami [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.</span><span class="sxs-lookup"><span data-stu-id="254d8-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="254d8-118">**System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="254d8-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="254d8-119">Wpisz następujące polecenie w [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="254d8-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="254d8-120">Pakiet instalacyjny wastorage</span><span class="sxs-lookup"><span data-stu-id="254d8-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="254d8-121">Konfigurowanie aplikacji dostęp do magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="254d8-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="254d8-122">Dodaj następujące instrukcje na początku pliku C++, której chcesz używać interfejsów API magazynu Azure na dostęp do obiektów blob obejmują:</span><span class="sxs-lookup"><span data-stu-id="254d8-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="254d8-123">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="254d8-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="254d8-124">Klienta usługi Azure storage używa parametrów połączenia magazynu do przechowywania punktów końcowych i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="254d8-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="254d8-125">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu w następującym formacie, przy użyciu nazwy konta magazynu i klucz dostępu do magazynu dla konta magazynu na liście [Azure Portal](https://portal.azure.com) dla *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="254d8-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="254d8-126">Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="254d8-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="254d8-127">Ten przykład przedstawia, jak można zadeklarować pola statycznego do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="254d8-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="254d8-128">Aby przetestować aplikację w lokalnym komputerze z systemem Windows, można użyć Microsoft Azure [emulatora magazynu](storage-use-emulator.md) zainstalowane z [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="254d8-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="254d8-129">Emulator magazynu jest narzędziem, która symuluje dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="254d8-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="254d8-130">W poniższym przykładzie pokazano, jak można zadeklarować pole statyczne, aby mógł pomieścić parametry połączenia z lokalnym emulatorze magazynu:</span><span class="sxs-lookup"><span data-stu-id="254d8-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="254d8-131">Aby uruchomić emulatora magazynu Azure, wybierz **Start** przycisk lub naciśnij przycisk **Windows** klucza.</span><span class="sxs-lookup"><span data-stu-id="254d8-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="254d8-132">Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="254d8-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="254d8-133">Poniższe przykłady założono użycie jednej z tych dwóch metod można pobrać parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="254d8-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="254d8-134">Pobranie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="254d8-134">Retrieve your connection string</span></span>
<span data-ttu-id="254d8-135">Można użyć **cloud_storage_account** klasy do reprezentowania informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="254d8-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="254d8-136">Aby uzyskać informacje o koncie magazynu z parametrów połączenia magazynu, można użyć **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="254d8-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="254d8-137">Następnie należy pobrać odwołanie do **cloud_blob_client** klasa umożliwia pobieranie obiektów, które reprezentują kontenery i obiekty BLOB przechowywane w ramach usługi magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="254d8-138">Poniższy kod tworzy **cloud_blob_client** przy użyciu obiektu konta magazynu, możemy pobrać powyżej:</span><span class="sxs-lookup"><span data-stu-id="254d8-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="254d8-139">Porady: Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="254d8-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="254d8-140">W tym przykładzie pokazano, jak utworzyć kontener, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="254d8-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="254d8-141">Domyślnie nowy kontener jest prywatny i należy określić klucz dostępu do magazynu, aby pobierać obiekty BLOB z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="254d8-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="254d8-142">Jeśli chcesz udostępnić pliki (BLOB) w kontenerze wszystkim użytkownikom, możesz ustawić kontener jako publiczny przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="254d8-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="254d8-143">Wszyscy użytkownicy Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="254d8-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="254d8-144">Porady: przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="254d8-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="254d8-145">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="254d8-146">W większości przypadków zalecane jest użycie blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="254d8-147">Aby przekazać plik do blokowego obiektu blob, pobierz odwołanie do kontenera i uzyskaj za jego pomocą odwołanie do blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="254d8-148">Po utworzeniu odwołanie do obiektu blob, dowolny strumień danych można przekazać do niej przez wywołanie metody **upload_from_stream** metody.</span><span class="sxs-lookup"><span data-stu-id="254d8-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="254d8-149">Ta operacja spowoduje utworzenie obiektu blob, jeśli jeszcze nie istnieje, lub jego zastąpienie, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="254d8-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="254d8-150">W poniższym przykładzie przedstawiono, jak przekazać obiekt blob do kontenera, zakładając, że kontener został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="254d8-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="254d8-151">Alternatywnie można użyć **upload_from_file** metody, aby przekazać plik do blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="254d8-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="254d8-152">Porady: wyświetlanie obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="254d8-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="254d8-153">Aby wyświetlić listę obiektów blob w kontenerze, należy najpierw uzyskać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="254d8-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="254d8-154">Następnie można użyć kontenera **list_blobs** metodę, aby pobrać obiekty BLOB i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="254d8-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="254d8-155">Aby dostęp do bogatego zestawu właściwości i metod zwróconego **list_blob_item**, należy wywołać **list_blob_item.as_blob** metodę, aby pobrać **cloud_blob** obiekt, lub **list_blob.as_directory** metody pobierania obiektu cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="254d8-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="254d8-156">Poniższy kod przedstawia sposób pobierania i zwracania identyfikatora URI poszczególnych elementów w **Moje kontenera próbki** kontenera:</span><span class="sxs-lookup"><span data-stu-id="254d8-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
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

<span data-ttu-id="254d8-157">Więcej szczegółów na listę działań, zobacz [listy zasobów magazynu Azure w języku C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="254d8-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="254d8-158">Porady: pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="254d8-158">How to: Download blobs</span></span>
<span data-ttu-id="254d8-159">Aby pobrać obiekty BLOB, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **download_to_stream** metody.</span><span class="sxs-lookup"><span data-stu-id="254d8-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="254d8-160">W poniższym przykładzie użyto **download_to_stream** metodę, aby przesłać zawartość obiektu blob do obiektu strumienia, który można następnie zachować do pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="254d8-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="254d8-161">Alternatywnie można użyć **download_to_file** metodę, aby pobrać zawartość obiektu blob do pliku.</span><span class="sxs-lookup"><span data-stu-id="254d8-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="254d8-162">Ponadto umożliwia także **download_text** metodę, aby pobrać zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="254d8-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="254d8-163">Porady: usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="254d8-163">How to: Delete blobs</span></span>
<span data-ttu-id="254d8-164">Aby usunąć obiekt blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **delete_blob** dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="254d8-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="254d8-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="254d8-165">Next steps</span></span>
<span data-ttu-id="254d8-166">Teraz, kiedy znasz już podstawy magazynu obiektów blob, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="254d8-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="254d8-167">Jak używać magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="254d8-167">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="254d8-168">Jak używać magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="254d8-168">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="254d8-169">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="254d8-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="254d8-170">Biblioteka klienta usługi Storage for C++ — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="254d8-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="254d8-171">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="254d8-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="254d8-172">Transfer danych za pomocą narzędzia wiersza polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="254d8-172">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

