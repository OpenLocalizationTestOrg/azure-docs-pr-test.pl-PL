---
title: "aaaGet pracy z magazynem obiektów Blob platformy Azure (obiekt magazynu), przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
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
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="51938-103">Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="51938-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="51938-104">Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="51938-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="51938-105">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51938-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="51938-106">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="51938-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="51938-107">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="51938-107">About this tutorial</span></span>
<span data-ttu-id="51938-108">Ten samouczek pokazuje, jak kod toowrite .NET dla niektórych typowych scenariuszy przy użyciu magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51938-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="51938-109">Przedstawione scenariusze obejmują przekazywanie, pobieranie i usuwanie obiektów blob oraz wyświetlanie ich listy.</span><span class="sxs-lookup"><span data-stu-id="51938-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="51938-110">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="51938-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="51938-111">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51938-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="51938-112">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="51938-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="51938-113">Menedżer konfiguracji Azure dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="51938-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="51938-114">[konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="51938-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="51938-115">Więcej przykładów</span><span class="sxs-lookup"><span data-stu-id="51938-115">More samples</span></span>
<span data-ttu-id="51938-116">Dodatkowe przykłady użycia usługi Blob Storage znajdziesz w temacie [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Blob Storage w programie .NET).</span><span class="sxs-lookup"><span data-stu-id="51938-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="51938-117">Możesz pobrać hello przykładowej aplikacji i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="51938-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="51938-118">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="51938-118">Add using directives</span></span>
<span data-ttu-id="51938-119">Dodaj następujące hello **przy użyciu** dyrektywy toohello początku hello `Program.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="51938-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="51938-120">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="51938-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="51938-121">Tworzenie klienta usługi Blob hello</span><span class="sxs-lookup"><span data-stu-id="51938-121">Create hello Blob service client</span></span>
<span data-ttu-id="51938-122">Witaj **CloudBlobClient** klasy pozwala tooretrieve kontenery i obiekty BLOB przechowywane w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="51938-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="51938-123">Klient usługi jednokierunkowej toocreate hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="51938-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="51938-124">Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooBlob pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="51938-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="51938-125">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="51938-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="51938-126">W tym przykładzie pokazano sposób toocreate kontenera, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="51938-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="51938-127">Domyślnie program hello nowy kontener jest prywatny, co oznacza, że obiektów blob toodownload klucza dostępu do magazynu z tego kontenera należy określić.</span><span class="sxs-lookup"><span data-stu-id="51938-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="51938-128">Jeśli chcesz, aby pliki hello toomake tooeveryone dostępne kontenera hello, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello:</span><span class="sxs-lookup"><span data-stu-id="51938-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="51938-129">Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym.</span><span class="sxs-lookup"><span data-stu-id="51938-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="51938-130">Jednak można zmodyfikować lub usunąć je tylko wtedy, gdy masz hello odpowiednie konto dostępu do klucza lub sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="51938-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="51938-131">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="51938-131">Upload a blob into a container</span></span>
<span data-ttu-id="51938-132">Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="51938-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="51938-133">W większości przypadków blokowych obiektów blob jest hello zalecane toouse typu.</span><span class="sxs-lookup"><span data-stu-id="51938-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="51938-134">tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku.</span><span class="sxs-lookup"><span data-stu-id="51938-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="51938-135">Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStream** metody.</span><span class="sxs-lookup"><span data-stu-id="51938-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="51938-136">Ta operacja tworzy hello obiektów blob, jeśli wcześniej nie istnieje lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="51938-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="51938-137">powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="51938-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="51938-138">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="51938-138">List hello blobs in a container</span></span>
<span data-ttu-id="51938-139">toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="51938-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="51938-140">Można użyć kontenera hello **ListBlobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="51938-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="51938-141">bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="51938-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="51938-142">Jeśli typ hello jest nieznany, można użyć toodetermine wyboru typu które toocast jej.</span><span class="sxs-lookup"><span data-stu-id="51938-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="51938-143">Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello _zdjęć_ kontenera:</span><span class="sxs-lookup"><span data-stu-id="51938-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
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

<span data-ttu-id="51938-144">Uwzględniając informacje o ścieżce w nazwach obiektów blob, można utworzyć wirtualną strukturę katalogów, które można organizować i przechodzić między nimi tak jak w przypadku tradycyjnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="51938-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="51938-145">Struktura katalogów Hello jest wirtualna tylko — Witaj tylko zasoby dostępne w magazynie obiektów Blob to kontenery i obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="51938-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="51938-146">Jednak biblioteka klienta magazynu hello zapewnia **CloudBlobDirectory** obiektu katalogu wirtualnego tooa toorefer i uprościć proces hello Praca z obiektami blob zorganizowanymi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="51938-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="51938-147">Na przykład, należy wziąć pod uwagę następujące zestaw blokowych obiektów blob w kontenerze o nazwie hello *zdjęć*:</span><span class="sxs-lookup"><span data-stu-id="51938-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="51938-148">Podczas wywoływania **ListBlobs** na powitania *zdjęć* kontenera (jak hello poprzedzających fragment kodu), zwrócenie listy hierarchicznej.</span><span class="sxs-lookup"><span data-stu-id="51938-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="51938-149">Zawiera **CloudBlobDirectory** i **CloudBlockBlob** obiekty reprezentujące odpowiednio hello katalogi i obiekty BLOB w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="51938-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="51938-150">Witaj dane wyjściowe wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="51938-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="51938-151">Opcjonalnie można ustawić hello **UseFlatBlobListing** parametru hello **ListBlobs** metodę **true**.</span><span class="sxs-lookup"><span data-stu-id="51938-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="51938-152">W takim przypadku każdy obiekt blob w kontenerze hello jest zwracana jako **CloudBlockBlob** obiektu.</span><span class="sxs-lookup"><span data-stu-id="51938-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="51938-153">Witaj wywołanie za**ListBlobs** tooreturn listy niezhierarchizowanej wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="51938-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="51938-154">i hello wyniki wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="51938-154">and hello results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="51938-155">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51938-155">Download blobs</span></span>
<span data-ttu-id="51938-156">obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **DownloadToStream** metody.</span><span class="sxs-lookup"><span data-stu-id="51938-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="51938-157">Witaj poniższym przykładzie użyto hello **DownloadToStream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="51938-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="51938-158">Można również użyć hello **DownloadToStream** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="51938-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="51938-159">Usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51938-159">Delete blobs</span></span>
<span data-ttu-id="51938-160">toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **usunąć** dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="51938-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="51938-161">Asynchroniczne wyświetlanie obiektów blob na stronach</span><span class="sxs-lookup"><span data-stu-id="51938-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="51938-162">Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub ma toocontrol hello liczbę wyników zwracanych przez jedną operację wyświetlania listy, można wyświetlić listę obiektów blob na stronach wyników.</span><span class="sxs-lookup"><span data-stu-id="51938-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="51938-163">Ten przykład przedstawia, jak tooreturn wyników na stronach asynchronicznie, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania tooreturn dużych zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="51938-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="51938-164">W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również wykonywać listę hierarchiczną, przez ustawienie hello _useFlatBlobListing_ parametru hello **ListBlobsSegmentedAsync** too_false_ metody.</span><span class="sxs-lookup"><span data-stu-id="51938-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="51938-165">Ponieważ hello przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem hello _async_ — słowo kluczowe, a musi zwracać **zadań** obiektu.</span><span class="sxs-lookup"><span data-stu-id="51938-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="51938-166">określona dla hello — słowo kluczowe await Hello **ListBlobsSegmentedAsync** wstrzymuje wykonywanie hello przykładowej metody do momentu ukończenia zadania wyświetlania listy hello.</span><span class="sxs-lookup"><span data-stu-id="51938-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="51938-167">Zapisywanie tooan Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51938-167">Writing tooan append blob</span></span>
<span data-ttu-id="51938-168">Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="51938-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="51938-169">Podobnie jak blokowy obiekt blob uzupełnialny obiekt blob jest złożony z bloków, ale po dodaniu nowego bloku tooan uzupełnialny obiekt blob jest zawsze toohello dołączany na końcu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="51938-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="51938-170">Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="51938-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="51938-171">Witaj identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="51938-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="51938-172">Każdy blok w uzupełnialnym obiekcie blob może być inny rozmiar się tooa maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać maksymalnie 50 000 bloków.</span><span class="sxs-lookup"><span data-stu-id="51938-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="51938-173">Maksymalny rozmiar uzupełnialnego obiektu blob Hello w związku z tym jest nieco przekraczać 195 GB (4 MB X 50 000 bloków).</span><span class="sxs-lookup"><span data-stu-id="51938-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="51938-174">w poniższym przykładzie Hello tworzy nowy uzupełnialny obiekt blob i dołącza tooit niektóre dane, symulując prostą operację rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="51938-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="51938-175">Zobacz [opis blokowe, stronicowe obiekty BLOB i Dołącz obiektów blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) Aby uzyskać więcej informacji o różnicach hello hello trzy typy obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="51938-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="51938-176">Zarządzanie zabezpieczeniami obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51938-176">Managing security for blobs</span></span>
<span data-ttu-id="51938-177">Domyślnie usługi Azure Storage chroni dane, ograniczając toohello właściciela konta dostępu, który znajduje się w posiadaniu klucze dostępu do konta hello.</span><span class="sxs-lookup"><span data-stu-id="51938-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="51938-178">Jeśli potrzebujesz tooshare danych obiektów blob na koncie magazynu jest ważne toodo tak bez naruszania zabezpieczeń hello kluczy dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="51938-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="51938-179">Ponadto można zaszyfrować tooensure danych obiektów blob, który jest bezpieczne, przejdź na powitania przewodowy i w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="51938-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="51938-180">Kontrolowanie dostępu do danych tooblob</span><span class="sxs-lookup"><span data-stu-id="51938-180">Controlling access tooblob data</span></span>
<span data-ttu-id="51938-181">Domyślnie program hello danych obiektów blob na koncie magazynu jest dostępny tylko właściciel konta toostorage.</span><span class="sxs-lookup"><span data-stu-id="51938-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="51938-182">Uwierzytelniania żądań dotyczących magazynu obiektów Blob wymaga klucz dostępu do konta hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="51938-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="51938-183">Jednak możesz toomake niektórych użytkowników tooother dostępnych danych obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="51938-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="51938-184">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="51938-184">You have two options:</span></span>

* <span data-ttu-id="51938-185">**Dostęp anonimowy:** możesz ustawić kontener lub zawarte w nim obiekty blob jako dostępne publicznie, aby umożliwić dostęp anonimowy.</span><span class="sxs-lookup"><span data-stu-id="51938-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="51938-186">Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](storage-manage-access-to-resources.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="51938-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="51938-187">**Sygnatury dostępu współdzielonego:** możesz zapewnić klientom sygnatury dostępu współdzielonego (SAS), która zapewnia dostęp delegowany tooa zasobów na koncie magazynu z uprawnieniami, które określisz i interwału, który określisz.</span><span class="sxs-lookup"><span data-stu-id="51938-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="51938-188">Zobacz [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="51938-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="51938-189">Szyfrowanie danych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51938-189">Encrypting blob data</span></span>
<span data-ttu-id="51938-190">Usługa Azure Storage obsługuje szyfrowanie danych obiektów blob, zarówno na powitania klienta, jak i na serwerze hello:</span><span class="sxs-lookup"><span data-stu-id="51938-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="51938-191">**Szyfrowanie po stronie klienta:** hello biblioteki klienta usługi Storage dla platformy .NET obsługuje szyfrowania danych w aplikacjach klienckich przed przekazaniem tooAzure magazynu i odszyfrowywania danych podczas pobierania toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="51938-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="51938-192">Biblioteka Hello obsługuje również integrację z usługą Azure Key Vault do zarządzania kluczami konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="51938-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="51938-193">Aby uzyskać więcej informacji, zobacz [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) (Szyfrowanie po stronie klienta przy użyciu programu .NET dla usługi Microsoft Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="51938-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="51938-194">Zobacz również [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md) (Samouczek: szyfrowanie i odszyfrowywanie obiektów blob w usłudze Microsoft Azure Storage przy użyciu usługi Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="51938-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="51938-195">**Szyfrowanie po stronie serwera**: usługa Azure Storage obsługuje teraz szyfrowanie po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="51938-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="51938-196">Zobacz [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md) (Szyfrowanie usługi Azure Storage dla danych magazynowanych (wersja zapoznawcza)).</span><span class="sxs-lookup"><span data-stu-id="51938-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51938-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51938-197">Next steps</span></span>
<span data-ttu-id="51938-198">Teraz, kiedy znasz już podstawy magazynu obiektów Blob hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="51938-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="51938-199">Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="51938-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="51938-200">[Microsoft Azure magazynu Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="51938-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="51938-201">Przykłady użycia usługi Blob Storage</span><span class="sxs-lookup"><span data-stu-id="51938-201">Blob storage samples</span></span>
* [<span data-ttu-id="51938-202">Rozpoczynanie pracy z usługą Azure Blob Storage na platformie .NET</span><span class="sxs-lookup"><span data-stu-id="51938-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="51938-203">Informacje o usłudze Blob Storage</span><span class="sxs-lookup"><span data-stu-id="51938-203">Blob storage reference</span></span>
* [<span data-ttu-id="51938-204">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="51938-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="51938-205">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="51938-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="51938-206">Przewodniki koncepcyjne</span><span class="sxs-lookup"><span data-stu-id="51938-206">Conceptual guides</span></span>
* [<span data-ttu-id="51938-207">Transfer danych za pomocą hello wiersza polecenia azcopy</span><span class="sxs-lookup"><span data-stu-id="51938-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="51938-208">Wprowadzenie do usługi File Storage dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="51938-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="51938-209">Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="51938-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
