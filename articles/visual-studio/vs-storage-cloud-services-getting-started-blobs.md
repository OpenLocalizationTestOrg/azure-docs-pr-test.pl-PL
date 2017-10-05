---
title: "Rozpoczynanie pracy z obiektu blob magazynu i Visual Studio połączone usługi (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę przy użyciu magazynu obiektów Blob platformy Azure w projektu usługi w chmurze w programie Visual Studio po połączeniu z kontem magazynu za pomocą programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: cf14880c70f90b01c5dffbfe434150581c2ec33b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="f61ca-103">Wprowadzenie do usługi Azure Blob Storage i Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="f61ca-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="f61ca-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f61ca-104">Overview</span></span>
<span data-ttu-id="f61ca-105">W tym artykule opisano, jak rozpocząć pracę z magazynu obiektów Blob Azure, po utworzeniu lub odwołuje się do konta usługi Azure Storage za pomocą programu Visual Studio **dodać usług połączonych** projektu usług okna dialogowego w chmurze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f61ca-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="f61ca-106">Poniżej opisano sposób dostępu i tworzenie kontenerów obiektów blob oraz sposób wykonywania typowych zadań, takich jak przekazywanie, wyświetlania i pobieranie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f61ca-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="f61ca-107">Przykłady są napisane w języku C\# i użyj [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="f61ca-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="f61ca-108">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f61ca-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f61ca-109">Pojedynczego obiektu blob może być dowolnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="f61ca-109">A single blob can be any size.</span></span> <span data-ttu-id="f61ca-110">Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów.</span><span class="sxs-lookup"><span data-stu-id="f61ca-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="f61ca-111">Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="f61ca-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="f61ca-112">Po utworzeniu magazynu należy utworzyć kontenerach w magazynie.</span><span class="sxs-lookup"><span data-stu-id="f61ca-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="f61ca-113">Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie o nazwie "obrazy" do przechowywania obrazów i innej o nazwie "audio" do przechowywania plików audio.</span><span class="sxs-lookup"><span data-stu-id="f61ca-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="f61ca-114">Po utworzeniu kontenerów, możesz przekazać pliki poszczególnych obiektów blob do nich.</span><span class="sxs-lookup"><span data-stu-id="f61ca-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="f61ca-115">Aby uzyskać więcej informacji na programowo manipulowanie obiektów blob, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f61ca-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="f61ca-116">Aby uzyskać ogólne informacje na temat usługi Azure Storage, zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="f61ca-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="f61ca-117">Aby uzyskać ogólne informacje o usługach w chmurze Azure, zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="f61ca-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="f61ca-118">Aby uzyskać więcej informacji na temat programowania aplikacji programu ASP.NET, zobacz [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="f61ca-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="f61ca-119">Dostęp do kontenerów obiektów blob w kodzie</span><span class="sxs-lookup"><span data-stu-id="f61ca-119">Access blob containers in code</span></span>
<span data-ttu-id="f61ca-120">Do uzyskania programowego dostępu do obiektów blob w projekty usługi w chmurze, należy dodać następujące elementy, jeśli nie są one już istnieje.</span><span class="sxs-lookup"><span data-stu-id="f61ca-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="f61ca-121">Dodaj następujące deklaracje przestrzeni nazw kod na początku każdego pliku C# w którym chcesz uzyskania programowego dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="f61ca-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="f61ca-122">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f61ca-123">Użyj następującego kodu można pobrać parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="f61ca-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="f61ca-124">Pobierz **CloudBlobClient** obiekt, aby odwołać istniejącego kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="f61ca-125">Pobierz **CloudBlobContainer** obiekt, aby odwołać kontenera konkretnego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f61ca-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="f61ca-126">Korzystanie ze wszystkich kodem przedstawionym w poprzedniej procedurze przed kodu pokazano w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="f61ca-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="f61ca-127">Tworzenie kontenera w kodzie</span><span class="sxs-lookup"><span data-stu-id="f61ca-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="f61ca-128">Niektórych interfejsów API służących do wykonywania wywołań wychodzących do magazynu Azure w ASP.NET są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="f61ca-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="f61ca-129">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f61ca-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="f61ca-130">Kod w poniższym przykładzie przyjęto założenie, że używasz metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="f61ca-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="f61ca-131">Aby utworzyć kontener na koncie magazynu, jest wszystko co należy zrobić, dodaj wywołanie do **CreateIfNotExistsAsync** zgodnie z poniższym kodem:</span><span class="sxs-lookup"><span data-stu-id="f61ca-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="f61ca-132">Aby udostępnić pliki w kontenerze dla wszystkich użytkowników, można ustawić kontener jako publiczny przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="f61ca-133">Wszyscy użytkownicy Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f61ca-134">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="f61ca-134">Upload a blob into a container</span></span>
<span data-ttu-id="f61ca-135">Usługa Azure Storage obsługuje blokowe i stronicowe obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="f61ca-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f61ca-136">W większości przypadków zalecane jest użycie blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f61ca-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="f61ca-137">Aby przekazać plik do blokowego obiektu blob, pobierz odwołanie do kontenera i uzyskaj za jego pomocą odwołanie do blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f61ca-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="f61ca-138">Po uzyskaniu odwołania do obiektu blob możesz przekazać do niego dowolny strumień danych, wywołując metodę **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="f61ca-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="f61ca-139">Ta operacja tworzy obiekt blob, jeśli jeszcze nie istniał, lub go zastępuje, jeśli już istniał.</span><span class="sxs-lookup"><span data-stu-id="f61ca-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="f61ca-140">W poniższym przykładzie przedstawiono, jak przekazać obiekt blob do kontenera, zakładając, że kontener został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="f61ca-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f61ca-141">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="f61ca-141">List the blobs in a container</span></span>
<span data-ttu-id="f61ca-142">Aby wyświetlić listę obiektów blob w kontenerze, należy najpierw uzyskać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="f61ca-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="f61ca-143">Następnie można użyć metody **ListBlobs** kontenera, aby pobrać obiekty blob i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="f61ca-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="f61ca-144">Aby dostęp do bogatego zestawu właściwości i metod zwróconego **IListBlobItem**, należy rzutować go do **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="f61ca-145">Jeśli typ jest nieznany, można zastosować sprawdzanie typu, aby określić, do którego obiektu rzutować obiekt.</span><span class="sxs-lookup"><span data-stu-id="f61ca-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="f61ca-146">Poniższy kod przedstawia sposób pobierania i zwracania identyfikatora URI poszczególnych elementów w kontenerze **photos**:</span><span class="sxs-lookup"><span data-stu-id="f61ca-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

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

<span data-ttu-id="f61ca-147">Jak pokazano w poprzednim przykładzie kodu, usługa blob korzysta z koncepcji katalogów w kontenerach, jak również.</span><span class="sxs-lookup"><span data-stu-id="f61ca-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="f61ca-148">Jest to, dzięki czemu można organizować w strukturze więcej folderu przypominającej obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f61ca-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="f61ca-149">Rozważmy na przykład następujący zestaw blokowych obiektów blob w kontenerze o nazwie **photos**:</span><span class="sxs-lookup"><span data-stu-id="f61ca-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="f61ca-150">Podczas wywoływania **ListBlobs** w kontenerze (jak powyższego przykładu) zawiera kolekcji zwróconej **CloudBlobDirectory** i **CloudBlockBlob** obiektów reprezentujący katalogi i obiekty BLOB, zawarty na najwyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="f61ca-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="f61ca-151">Poniżej przedstawiono dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f61ca-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="f61ca-152">Opcjonalnie można ustawić parametr **UseFlatBlobListing** metody **ListBlobs** na wartość **true**.</span><span class="sxs-lookup"><span data-stu-id="f61ca-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="f61ca-153">Powoduje to każdy obiekt blob jest zwracana jako **CloudBlockBlob**, niezależnie od tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="f61ca-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="f61ca-154">Oto wywołanie **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="f61ca-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="f61ca-155">i poniżej przedstawiono wyniki:</span><span class="sxs-lookup"><span data-stu-id="f61ca-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="f61ca-156">Aby uzyskać więcej informacji, zobacz [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="f61ca-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="f61ca-157">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f61ca-157">Download blobs</span></span>
<span data-ttu-id="f61ca-158">Aby pobrać obiekty blob, należy najpierw pobrać odwołanie do obiektu blob, a następnie wywołać metodę **DownloadToStream**.</span><span class="sxs-lookup"><span data-stu-id="f61ca-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="f61ca-159">W poniższym przykładzie użyto metody **DownloadToStream**, aby przesłać zawartość obiektu blob do obiektu strumienia, który można następnie zachować w pliku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f61ca-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="f61ca-160">Można również użyć metody **DownloadToStream**, aby pobrać zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="f61ca-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="f61ca-161">Usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f61ca-161">Delete blobs</span></span>
<span data-ttu-id="f61ca-162">Aby usunąć obiekt blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **usunąć** metody.</span><span class="sxs-lookup"><span data-stu-id="f61ca-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="f61ca-163">Asynchroniczne wyświetlanie obiektów blob na stronach</span><span class="sxs-lookup"><span data-stu-id="f61ca-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="f61ca-164">Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub kontrolować liczbę wyników zwracanych przez jedną operację wyświetlania listy, możesz wyświetlić obiekty blob na stronach wyników.</span><span class="sxs-lookup"><span data-stu-id="f61ca-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="f61ca-165">W tym przykładzie przedstawiono sposób asynchronicznego zwracania wyników na stronach, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania na zwrócenie dużych zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="f61ca-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="f61ca-166">W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również uzyskać listę hierarchiczną, ustawiając parametr **useFlatBlobListing** metody **ListBlobsSegmentedAsync** na wartość **false**.</span><span class="sxs-lookup"><span data-stu-id="f61ca-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="f61ca-167">Ze względu na to, że przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem kluczowym **async** i zwracać obiekt **Task**.</span><span class="sxs-lookup"><span data-stu-id="f61ca-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="f61ca-168">Słowo kluczowe await określone dla metody **ListBlobsSegmentedAsync** wstrzymuje wykonywanie przykładowej metody do momentu ukończenia zadania wyświetlania listy.</span><span class="sxs-lookup"><span data-stu-id="f61ca-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="f61ca-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f61ca-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

