---
title: "aaaGet wprowadzenie do magazynu obiektów blob i Visual Studio podłączonych usług (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Sposób uruchamiania przy użyciu magazynu obiektów Blob platformy Azure w projekcie programu Visual Studio platformy ASP.NET Core, po utworzeniu konta magazynu przy użyciu programu Visual Studio tooget połączone usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="2a0ae-103">Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (platformy ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="2a0ae-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2a0ae-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2a0ae-104">Overview</span></span>
<span data-ttu-id="2a0ae-105">W tym artykule opisano sposób uruchamiania przy użyciu magazynu obiektów Blob platformy Azure w programie Visual Studio po utworzony lub odwołuje się do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą okna dialogowego programu Visual Studio Dodaj połączone usługi hello tooget.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="2a0ae-106">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="2a0ae-107">Pojedynczego obiektu blob może być dowolnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-107">A single blob can be any size.</span></span> <span data-ttu-id="2a0ae-108">Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="2a0ae-109">W tym artykule opisano, jak tooget pracę z magazynu obiektów blob, po utworzeniu konta magazynu platformy Azure przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego w projekcie platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="2a0ae-110">Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="2a0ae-111">Po utworzeniu magazynu tworzenia kontenerach hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="2a0ae-112">Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie hello o nazwie "obrazy" toostore obrazów i innej o nazwie "audio" toostore plików audio.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="2a0ae-113">Po utworzeniu hello kontenerów, możesz przekazać toothem plików poszczególnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="2a0ae-114">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) uzyskać więcej informacji o programowo manipulowanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="2a0ae-115">Dostęp do kontenerów obiektów blob w kodzie</span><span class="sxs-lookup"><span data-stu-id="2a0ae-115">Access blob containers in code</span></span>
<span data-ttu-id="2a0ae-116">tooprogrammatically dostęp do obiektów blob platformy ASP.NET Core projektów, należy hello tooadd następujące elementy, jeśli nie są one już istnieje.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="2a0ae-117">Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello górnej części każdego C# pliku, w której ma zostać tooprogrammatically dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="2a0ae-118">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a0ae-119">Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="2a0ae-120">**Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="2a0ae-121">Użyj **CloudBlobClient** obiekt tooget **CloudBlobContainer** odwołania tooan istniejącego kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="2a0ae-122">Tworzenie kontenera w kodzie</span><span class="sxs-lookup"><span data-stu-id="2a0ae-122">Create a container in code</span></span>
<span data-ttu-id="2a0ae-123">Można również użyć hello **CloudBlobClient** toocreate kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="2a0ae-124">Toodo wystarczy tooadd wywołanie za**CreateIfNotExistsAsync** jak hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="2a0ae-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="2a0ae-125">**Uwaga:** hello interfejsów API, które wykonywania wywołań tooAzure magazynu w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="2a0ae-126">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="2a0ae-127">Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="2a0ae-128">pliki hello toomake tooeveryone dostępne hello kontenera, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2a0ae-129">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="2a0ae-129">Upload a blob into a container</span></span>
<span data-ttu-id="2a0ae-130">tooupload pliku blob do kontenera, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="2a0ae-131">Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStreamAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="2a0ae-132">Tej operacji tworzy hello obiektów blob, jeśli nie jest jeszcze określony lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="2a0ae-133">powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="2a0ae-134">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="2a0ae-134">List hello blobs in a container</span></span>
<span data-ttu-id="2a0ae-135">toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="2a0ae-136">Kontener hello może wywoływać **ListBlobsSegmentedAsync** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="2a0ae-137">bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="2a0ae-138">Jeśli nie znasz typu blob hello, możesz użyć toodetermine wyboru typu które toocast jej.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="2a0ae-139">Witaj następującego kodu pokazano, jak tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="2a0ae-140">Istnieją inne sposoby toolist hello zawartość kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="2a0ae-141">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="2a0ae-142">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2a0ae-142">Download a blob</span></span>
<span data-ttu-id="2a0ae-143">toodownload obiektu blob, najpierw pobrać odwołanie do obiektu blob toohello, a następnie wywołać hello **DownloadToStreamAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="2a0ae-144">Witaj poniższym przykładzie użyto hello **DownloadToStreamAsync** metody tootransfer hello blob zawartość tooa obiektu strumienia, który można zapisać jako plik lokalny.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="2a0ae-145">Istnieją inne sposoby toosave obiekty BLOB jako plików.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="2a0ae-146">Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="2a0ae-147">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2a0ae-147">Delete a blob</span></span>
<span data-ttu-id="2a0ae-148">toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob toohello, a następnie wywołać hello **DeleteAsync** dla niego metodę.</span><span class="sxs-lookup"><span data-stu-id="2a0ae-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="2a0ae-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2a0ae-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

