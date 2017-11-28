---
title: "Rozpoczynanie pracy z obiektu blob magazynu i Visual Studio połączone usługi (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę przy użyciu magazynu obiektów Blob platformy Azure w projekcie programu Visual Studio platformy ASP.NET Core, po utworzeniu konta magazynu przy użyciu programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e725015c8be7ecfa908f0ae75986b73f218fa3ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="9456b-103">Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (platformy ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="9456b-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="9456b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9456b-104">Overview</span></span>
<span data-ttu-id="9456b-105">W tym artykule opisano, jak rozpocząć pracę przy użyciu magazynu obiektów Blob platformy Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą okna dialogowego programu Visual Studio Dodaj połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="9456b-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="9456b-106">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9456b-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="9456b-107">Pojedynczego obiektu blob może być dowolnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="9456b-107">A single blob can be any size.</span></span> <span data-ttu-id="9456b-108">Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów.</span><span class="sxs-lookup"><span data-stu-id="9456b-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="9456b-109">W tym artykule opisano, jak rozpocząć pracę z magazynu obiektów blob, po utworzeniu konta magazynu platformy Azure przy użyciu programu Visual Studio **dodać usług połączonych** okna dialogowego w projekcie platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9456b-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="9456b-110">Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="9456b-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="9456b-111">Po utworzeniu magazynu należy utworzyć kontenerach w magazynie.</span><span class="sxs-lookup"><span data-stu-id="9456b-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="9456b-112">Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie o nazwie "obrazy" do przechowywania obrazów i innej o nazwie "audio" do przechowywania plików audio.</span><span class="sxs-lookup"><span data-stu-id="9456b-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="9456b-113">Po utworzeniu kontenerów, możesz przekazać pliki poszczególnych obiektów blob do nich.</span><span class="sxs-lookup"><span data-stu-id="9456b-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="9456b-114">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) uzyskać więcej informacji o programowo manipulowanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9456b-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="9456b-115">Dostęp do kontenerów obiektów blob w kodzie</span><span class="sxs-lookup"><span data-stu-id="9456b-115">Access blob containers in code</span></span>
<span data-ttu-id="9456b-116">Do uzyskania programowego dostępu do obiektów blob w projektów platformy ASP.NET Core, należy dodać następujące elementy, jeśli nie są one już istnieje.</span><span class="sxs-lookup"><span data-stu-id="9456b-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="9456b-117">Dodaj następujące deklaracje przestrzeni nazw kod na początku dowolnego pliku C# ma do uzyskania programowego dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9456b-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="9456b-118">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9456b-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9456b-119">Poniższy kod umożliwia pobieranie parametrów połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="9456b-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="9456b-120">**Uwaga:** korzystać ze wszystkich powyższych kodu przed kod w następujących sekcjach.</span><span class="sxs-lookup"><span data-stu-id="9456b-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="9456b-121">Użyj **CloudBlobClient** obiekt, aby pobrać **CloudBlobContainer** odwołania do istniejącego kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9456b-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="9456b-122">Tworzenie kontenera w kodzie</span><span class="sxs-lookup"><span data-stu-id="9456b-122">Create a container in code</span></span>
<span data-ttu-id="9456b-123">Można również użyć **CloudBlobClient** do utworzenia kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9456b-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="9456b-124">Wszystko co należy zrobić to dodanie wywołanie **CreateIfNotExistsAsync** zgodnie z poniższym kodem:</span><span class="sxs-lookup"><span data-stu-id="9456b-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="9456b-125">**Uwaga:** interfejsów API służących do wykonywania wywołań do magazynu Azure w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="9456b-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="9456b-126">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9456b-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="9456b-127">Poniższy kod przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="9456b-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="9456b-128">Aby udostępnić pliki w kontenerze dla wszystkich użytkowników, można ustawić kontener jako publiczny przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="9456b-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="9456b-129">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="9456b-129">Upload a blob into a container</span></span>
<span data-ttu-id="9456b-130">Aby przekazać plik obiektu blob do kontenera, Pobierz odwołanie do kontenera i użyj go, aby pobrać odwołanie do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="9456b-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="9456b-131">Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych do niej przez wywołanie metody **UploadFromStreamAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="9456b-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="9456b-132">Ta operacja tworzy obiektu blob, jeśli nie jest jeszcze określony lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="9456b-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="9456b-133">W poniższym przykładzie przedstawiono, jak przekazać obiekt blob do kontenera, zakładając, że kontener został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="9456b-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="9456b-134">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="9456b-134">List the blobs in a container</span></span>
<span data-ttu-id="9456b-135">Aby wyświetlić listę obiektów blob w kontenerze, należy najpierw uzyskać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="9456b-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="9456b-136">Następnie można wywołać kontenera **ListBlobsSegmentedAsync** metodę, aby pobrać obiekty BLOB i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="9456b-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="9456b-137">Aby uzyskać dostęp do bogatego zestawu właściwości i metod zwróconego obiektu **IListBlobItem**, należy rzutować go na obiekt **CloudBlockBlob**, **CloudPageBlob** lub **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="9456b-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="9456b-138">Jeśli nie znasz typu obiektu blob służy sprawdzanie typu umożliwia określenie, które rzutować obiekt.</span><span class="sxs-lookup"><span data-stu-id="9456b-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="9456b-139">Poniższy kod przedstawia sposób pobierania i zwracania identyfikatora URI poszczególnych elementów w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="9456b-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="9456b-140">Istnieją inne sposoby na wyświetlanie zawartości kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9456b-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="9456b-141">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9456b-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="9456b-142">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="9456b-142">Download a blob</span></span>
<span data-ttu-id="9456b-143">Aby pobrać obiektu blob, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **DownloadToStreamAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="9456b-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="9456b-144">W poniższym przykładzie użyto **DownloadToStreamAsync** metodę, aby przesłać zawartość obiektu blob do obiektu strumienia, który można zapisać jako plik lokalny.</span><span class="sxs-lookup"><span data-stu-id="9456b-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="9456b-145">Istnieją inne sposoby zapisywania obiektów blob jako plików.</span><span class="sxs-lookup"><span data-stu-id="9456b-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="9456b-146">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9456b-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="9456b-147">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="9456b-147">Delete a blob</span></span>
<span data-ttu-id="9456b-148">Aby usunąć obiekt blob, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **DeleteAsync** dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="9456b-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="9456b-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9456b-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

