---
title: "Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu programu .NET | Microsoft Docs"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 70c7d6a5e1b9aa9a13481893e0baa56538be097c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="05140-103">Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="05140-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="05140-104">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="05140-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="05140-105">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05140-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="05140-106">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="05140-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="05140-107">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="05140-107">About this tutorial</span></span>
<span data-ttu-id="05140-108">W tym samouczku pokazano, jak napisać kod .NET dla niektórych typowych scenariuszy przy użyciu Magazynu obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="05140-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="05140-109">Przedstawione scenariusze obejmują przekazywanie, pobieranie i usuwanie obiektów blob oraz wyświetlanie ich listy.</span><span class="sxs-lookup"><span data-stu-id="05140-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="05140-110">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="05140-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="05140-111">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05140-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="05140-112">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="05140-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="05140-113">Menedżer konfiguracji Azure dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="05140-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="05140-114">[konto usługi Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="05140-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="05140-115">Więcej przykładów</span><span class="sxs-lookup"><span data-stu-id="05140-115">More samples</span></span>
<span data-ttu-id="05140-116">Dodatkowe przykłady użycia usługi Blob Storage znajdziesz w temacie [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Blob Storage w programie .NET).</span><span class="sxs-lookup"><span data-stu-id="05140-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="05140-117">Możesz pobrać przykładową aplikację i uruchomić ją lub przejrzeć kod w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="05140-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="05140-118">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="05140-118">Add using directives</span></span>
<span data-ttu-id="05140-119">Dodaj następujące dyrektywy **using** na początku pliku `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="05140-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="05140-120">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="05140-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="05140-121">Tworzenie klienta usługi Blob</span><span class="sxs-lookup"><span data-stu-id="05140-121">Create the Blob service client</span></span>
<span data-ttu-id="05140-122">Klasa **CloudBlobClient** umożliwia pobieranie kontenerów i obiektów blob przechowywanych w usłudze Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="05140-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="05140-123">Oto jeden ze sposobów tworzenia klienta usługi:</span><span class="sxs-lookup"><span data-stu-id="05140-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="05140-124">Teraz możesz przystąpić do pisania kodu, który będzie odczytywać dane z Magazynu obiektów blob i zapisywać je w nim.</span><span class="sxs-lookup"><span data-stu-id="05140-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="05140-125">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="05140-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="05140-126">W tym przykładzie pokazano, jak utworzyć kontener, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="05140-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="05140-127">Domyślnie nowy kontener jest prywatny, co oznacza, że musisz podać klucz dostępu do magazynu, aby pobierać obiekty blob z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="05140-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="05140-128">Jeśli chcesz, aby pliki w kontenerze były dostępne dla wszystkich, możesz ustawić kontener jako publiczny przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="05140-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="05140-129">Wszyscy w Internecie będą mogli uzyskiwać dostęp do obiektów blob w kontenerze publicznym.</span><span class="sxs-lookup"><span data-stu-id="05140-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="05140-130">Jednak modyfikować lub usuwać je można tylko przy użyciu odpowiedniego klucza dostępu do konta lub sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="05140-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="05140-131">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="05140-131">Upload a blob into a container</span></span>
<span data-ttu-id="05140-132">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="05140-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="05140-133">W większości przypadków zalecane jest użycie blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="05140-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="05140-134">Aby przekazać plik do blokowego obiektu blob, pobierz odwołanie do kontenera i uzyskaj za jego pomocą odwołanie do blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05140-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="05140-135">Po uzyskaniu odwołania do obiektu blob możesz przekazać do niego dowolny strumień danych, wywołując metodę **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="05140-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="05140-136">Ta operacja tworzy obiekt blob, jeśli jeszcze nie istniał, lub go zastępuje, jeśli już istniał.</span><span class="sxs-lookup"><span data-stu-id="05140-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="05140-137">W poniższym przykładzie przedstawiono, jak przekazać obiekt blob do kontenera, zakładając, że kontener został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="05140-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="05140-138">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="05140-138">List the blobs in a container</span></span>
<span data-ttu-id="05140-139">Aby wyświetlić listę obiektów blob w kontenerze, należy najpierw uzyskać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="05140-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="05140-140">Następnie można użyć metody **ListBlobs** kontenera, aby pobrać obiekty blob i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="05140-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="05140-141">Aby uzyskać dostęp do bogatego zestawu właściwości i metod zwróconego obiektu **IListBlobItem**, należy rzutować go na obiekt **CloudBlockBlob**, **CloudPageBlob** lub **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="05140-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="05140-142">Jeśli typ jest nieznany, można zastosować sprawdzanie typu, aby określić, do którego obiektu rzutować obiekt.</span><span class="sxs-lookup"><span data-stu-id="05140-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="05140-143">Poniższy kod przedstawia sposób pobierania i zwracania identyfikatora URI poszczególnych elementów w kontenerze _photos_:</span><span class="sxs-lookup"><span data-stu-id="05140-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="05140-144">Uwzględniając informacje o ścieżce w nazwach obiektów blob, można utworzyć wirtualną strukturę katalogów, które można organizować i przechodzić między nimi tak jak w przypadku tradycyjnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="05140-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="05140-145">Struktura katalogów jest wyłącznie wirtualna — jedyne zasoby dostępne w magazynie Blob Storage to kontenery i obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="05140-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="05140-146">Jednak biblioteka klienta magazynu zapewnia obiekt **CloudBlobDirectory** służący do odwoływania się do katalogów wirtualnych i ułatwiający pracę z obiektami blob zorganizowanymi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="05140-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="05140-147">Rozważmy na przykład następujący zestaw blokowych obiektów blob w kontenerze o nazwie *photos*:</span><span class="sxs-lookup"><span data-stu-id="05140-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="05140-148">Wywołanie metody **ListBlobs** w kontenerze *photos* (jak we wcześniejszym fragmencie kodu) powoduje zwrócenie listy hierarchicznej.</span><span class="sxs-lookup"><span data-stu-id="05140-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="05140-149">Zawiera ona obiekty **CloudBlobDirectory** i **CloudBlockBlob** reprezentujące odpowiednio katalogi i obiekty blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="05140-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="05140-150">Dane wyjściowe wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="05140-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="05140-151">Opcjonalnie można ustawić parametr **UseFlatBlobListing** metody **ListBlobs** na wartość **true**.</span><span class="sxs-lookup"><span data-stu-id="05140-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="05140-152">W takim przypadku każdy obiekt blob w kontenerze będzie zwracany jako obiekt **CloudBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="05140-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="05140-153">Wywołanie metody **ListBlobs** w celu zwrócenia listy niezhierarchizowanej wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="05140-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="05140-154">Wyniki wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="05140-154">and the results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="05140-155">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05140-155">Download blobs</span></span>
<span data-ttu-id="05140-156">Aby pobrać obiekty blob, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać metodę **DownloadToStream**.</span><span class="sxs-lookup"><span data-stu-id="05140-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="05140-157">W poniższym przykładzie użyto metody **DownloadToStream**, aby przesłać zawartość obiektu blob do obiektu strumienia, który można następnie zachować w pliku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="05140-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="05140-158">Można również użyć metody **DownloadToStream**, aby pobrać zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="05140-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="05140-159">Usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05140-159">Delete blobs</span></span>
<span data-ttu-id="05140-160">Aby usunąć obiekt blob, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać dla niego metodę **Delete**.</span><span class="sxs-lookup"><span data-stu-id="05140-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="05140-161">Asynchroniczne wyświetlanie obiektów blob na stronach</span><span class="sxs-lookup"><span data-stu-id="05140-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="05140-162">Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub kontrolować liczbę wyników zwracanych przez jedną operację wyświetlania listy, możesz wyświetlić obiekty blob na stronach wyników.</span><span class="sxs-lookup"><span data-stu-id="05140-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="05140-163">W tym przykładzie przedstawiono sposób asynchronicznego zwracania wyników na stronach, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania na zwrócenie dużych zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="05140-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="05140-164">W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również uzyskać listę hierarchiczną, ustawiając parametr _useFlatBlobListing_ metody **ListBlobsSegmentedAsync** na wartość _false_.</span><span class="sxs-lookup"><span data-stu-id="05140-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="05140-165">Ze względu na to, że przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem kluczowym _async_ i zwracać obiekt **Task**.</span><span class="sxs-lookup"><span data-stu-id="05140-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="05140-166">Słowo kluczowe await określone dla metody **ListBlobsSegmentedAsync** wstrzymuje wykonywanie przykładowej metody do momentu ukończenia zadania wyświetlania listy.</span><span class="sxs-lookup"><span data-stu-id="05140-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="05140-167">Zapisywanie do uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="05140-167">Writing to an append blob</span></span>
<span data-ttu-id="05140-168">Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="05140-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="05140-169">Podobnie jak blokowy obiekt blob, uzupełnialny obiekt blob jest złożony z bloków, ale nowy blok dodany do uzupełnialnego obiektu blob jest zawsze dołączany na końcu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05140-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="05140-170">Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="05140-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="05140-171">Identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="05140-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="05140-172">Każdy blok w uzupełnialnym obiekcie blob może różnić się rozmiarem, który może wynosić maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać do 50 000 bloków.</span><span class="sxs-lookup"><span data-stu-id="05140-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="05140-173">Z tego względu maksymalny rozmiar uzupełnialnego obiektu blob nieznacznie przekracza 195 GB (4 MB X 50 000 bloków).</span><span class="sxs-lookup"><span data-stu-id="05140-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="05140-174">W poniższym przykładzie utworzono nowy uzupełnialny obiekt blob i dołączono do niego określone dane, symulując prostą operację rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="05140-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="05140-175">Aby uzyskać więcej informacji o różnicach między tymi trzema typami obiektów blob, zobacz [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) (Omówienie blokowych i stronicowych obiektów blob oraz uzupełnialnych obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="05140-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="05140-176">Zarządzanie zabezpieczeniami obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05140-176">Managing security for blobs</span></span>
<span data-ttu-id="05140-177">Domyślnie usługa Azure Storage chroni dane, umożliwiając dostęp wyłącznie właścicielowi konta, który ma klucze dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="05140-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="05140-178">W przypadku potrzeby udostępnienia danych obiektów blob na koncie magazynu ważne jest, aby zrobić to bez uszczerbku dla bezpieczeństwa kluczy dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="05140-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="05140-179">Dodatkowo można zaszyfrować dane obiektu blob, aby zapewnić ich bezpieczeństwo podczas przesyłania przez sieć oraz w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="05140-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="05140-180">Kontrolowanie dostępu do danych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05140-180">Controlling access to blob data</span></span>
<span data-ttu-id="05140-181">Domyślnie dane obiektów blob na koncie magazynu są dostępne tylko dla właściciela konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="05140-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="05140-182">Domyślnie do uwierzytelniania żądań dotyczących Magazynu obiektów blob jest wymagany klucz dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="05140-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="05140-183">Możesz jednak udostępnić określone dane obiektów blob innym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="05140-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="05140-184">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="05140-184">You have two options:</span></span>

* <span data-ttu-id="05140-185">**Dostęp anonimowy:** możesz ustawić kontener lub zawarte w nim obiekty blob jako dostępne publicznie, aby umożliwić dostęp anonimowy.</span><span class="sxs-lookup"><span data-stu-id="05140-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="05140-186">Aby uzyskać więcej informacji, zobacz [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) (Zarządzanie dostępem anonimowym do kontenerów i obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="05140-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="05140-187">**Sygnatury dostępu współdzielonego:** możesz zapewnić klientom sygnatury dostępu współdzielonego (SAS), które umożliwiają dostęp delegowany do zasobu na koncie magazynu z uprawnieniami i w przedziale czasu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="05140-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="05140-188">Zobacz [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="05140-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="05140-189">Szyfrowanie danych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="05140-189">Encrypting blob data</span></span>
<span data-ttu-id="05140-190">Usługa Azure Storage obsługuje szyfrowanie danych obiektów blob na kliencie i na serwerze:</span><span class="sxs-lookup"><span data-stu-id="05140-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="05140-191">**Szyfrowanie po stronie klienta:** biblioteka klienta usługi Storage dla programu .NET obsługuje szyfrowanie danych w aplikacjach klienckich przed ich przekazaniem do usługi Azure Storage oraz odszyfrowywanie danych przed pobraniem do klienta.</span><span class="sxs-lookup"><span data-stu-id="05140-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="05140-192">Biblioteka obsługuje również integrację z magazynem kluczy Azure do zarządzania kluczami konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="05140-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="05140-193">Aby uzyskać więcej informacji, zobacz [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Szyfrowanie po stronie klienta przy użyciu programu .NET dla usługi Microsoft Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="05140-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="05140-194">Zobacz również [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md) (Samouczek: szyfrowanie i odszyfrowywanie obiektów blob w usłudze Microsoft Azure Storage przy użyciu usługi Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="05140-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="05140-195">**Szyfrowanie po stronie serwera**: usługa Azure Storage obsługuje teraz szyfrowanie po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="05140-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="05140-196">Zobacz [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Szyfrowanie usługi Azure Storage dla danych magazynowanych (wersja zapoznawcza)).</span><span class="sxs-lookup"><span data-stu-id="05140-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05140-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05140-197">Next steps</span></span>
<span data-ttu-id="05140-198">Teraz, kiedy znasz już podstawy usługi Blob Storage, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="05140-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="05140-199">Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="05140-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="05140-200">[Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) jest darmową aplikacją autonomiczną oferowaną przez firmę Microsoft, która umożliwia pracę poglądową z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="05140-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="05140-201">Przykłady użycia usługi Blob Storage</span><span class="sxs-lookup"><span data-stu-id="05140-201">Blob storage samples</span></span>
* [<span data-ttu-id="05140-202">Rozpoczynanie pracy z usługą Azure Blob Storage na platformie .NET</span><span class="sxs-lookup"><span data-stu-id="05140-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="05140-203">Informacje o usłudze Blob Storage</span><span class="sxs-lookup"><span data-stu-id="05140-203">Blob storage reference</span></span>
* [<span data-ttu-id="05140-204">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="05140-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="05140-205">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="05140-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="05140-206">Przewodniki koncepcyjne</span><span class="sxs-lookup"><span data-stu-id="05140-206">Conceptual guides</span></span>
* [<span data-ttu-id="05140-207">Transfer danych za pomocą narzędzia wiersza polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="05140-207">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="05140-208">Wprowadzenie do usługi File Storage dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="05140-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="05140-209">Korzystanie z usługi Azure Blob Storage z zestawem SDK WebJobs</span><span class="sxs-lookup"><span data-stu-id="05140-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
