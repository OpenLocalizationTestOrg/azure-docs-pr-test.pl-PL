---
title: "aaaGet wprowadzenie do magazynu obiektów blob i Visual Studio podłączonych usług (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu obiektów Blob platformy Azure w projektu usługi w chmurze w programie Visual Studio po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
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
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="40cf4-103">Wprowadzenie do usługi Azure Blob Storage i Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="40cf4-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="40cf4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="40cf4-104">Overview</span></span>
<span data-ttu-id="40cf4-105">W tym artykule opisano, jak tooget pracę z magazynu obiektów Blob Azure po utworzeniu lub odwołuje się do konta usługi Azure Storage za pomocą programu Visual Studio hello **dodać usług połączonych** projektu usług okna dialogowego w chmurze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40cf4-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="40cf4-106">Poniżej opisano sposób tooaccess i tworzenie kontenerów obiektów blob i jak tooperform typowych zadań, takich jak przekazywanie, wyświetlania i pobieranie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="40cf4-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="40cf4-107">Przykłady Hello są napisane w języku C\# i użyj hello [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="40cf4-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="40cf4-108">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="40cf4-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="40cf4-109">Pojedynczego obiektu blob może być dowolnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="40cf4-109">A single blob can be any size.</span></span> <span data-ttu-id="40cf4-110">Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów.</span><span class="sxs-lookup"><span data-stu-id="40cf4-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="40cf4-111">Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="40cf4-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="40cf4-112">Po utworzeniu magazynu tworzenia kontenerach hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="40cf4-113">Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie hello o nazwie "obrazy" toostore obrazów i innej o nazwie "audio" toostore plików audio.</span><span class="sxs-lookup"><span data-stu-id="40cf4-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="40cf4-114">Po utworzeniu hello kontenerów, możesz przekazać toothem plików poszczególnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="40cf4-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="40cf4-115">Aby uzyskać więcej informacji na programowo manipulowanie obiektów blob, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="40cf4-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="40cf4-116">Aby uzyskać ogólne informacje na temat usługi Azure Storage, zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="40cf4-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="40cf4-117">Aby uzyskać ogólne informacje o usługach w chmurze Azure, zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="40cf4-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="40cf4-118">Aby uzyskać więcej informacji na temat programowania aplikacji programu ASP.NET, zobacz [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="40cf4-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="40cf4-119">Dostęp do kontenerów obiektów blob w kodzie</span><span class="sxs-lookup"><span data-stu-id="40cf4-119">Access blob containers in code</span></span>
<span data-ttu-id="40cf4-120">tooprogrammatically dostęp do obiektów blob projekty usługi w chmurze, należy hello tooadd następujące elementy, jeśli nie są one już istnieje.</span><span class="sxs-lookup"><span data-stu-id="40cf4-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="40cf4-121">Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello górnej części każdego C# pliku, w którym chcesz tooprogrammatically dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="40cf4-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="40cf4-122">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="40cf4-123">Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="40cf4-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="40cf4-124">Pobierz **CloudBlobClient** obiekt tooreference istniejącego kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="40cf4-125">Pobierz **CloudBlobContainer** obiekt tooreference kontenera konkretnego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="40cf4-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="40cf4-126">Korzystanie ze wszystkich hello kodem przedstawionym w poprzedniej procedurze hello przed hello kodu pokazano hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="40cf4-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="40cf4-127">Tworzenie kontenera w kodzie</span><span class="sxs-lookup"><span data-stu-id="40cf4-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="40cf4-128">Niektórych interfejsów API służących do wykonywania wywołań wychodzących tooAzure magazynu w ASP.NET są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="40cf4-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="40cf4-129">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="40cf4-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="40cf4-130">Kod Hello w hello poniższy przykład zakłada, używasz metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="40cf4-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="40cf4-131">toocreate kontenera na koncie magazynu, wszystko, czego potrzebujesz toodo jest Dodaj wywołanie za**CreateIfNotExistsAsync** jak hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="40cf4-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="40cf4-132">pliki hello toomake tooeveryone dostępne hello kontenera, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="40cf4-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="40cf4-133">Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="40cf4-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="40cf4-134">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="40cf4-134">Upload a blob into a container</span></span>
<span data-ttu-id="40cf4-135">Usługa Azure Storage obsługuje blokowe i stronicowe obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="40cf4-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="40cf4-136">W większości przypadków hello blokowych obiektów blob jest hello zalecane toouse typu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="40cf4-137">tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku.</span><span class="sxs-lookup"><span data-stu-id="40cf4-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="40cf4-138">Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStream** metody.</span><span class="sxs-lookup"><span data-stu-id="40cf4-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="40cf4-139">Ta operacja tworzy hello obiektów blob, jeśli wcześniej nie istnieje lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="40cf4-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="40cf4-140">powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="40cf4-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="40cf4-141">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="40cf4-141">List hello blobs in a container</span></span>
<span data-ttu-id="40cf4-142">toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera.</span><span class="sxs-lookup"><span data-stu-id="40cf4-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="40cf4-143">Można użyć kontenera hello **ListBlobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi.</span><span class="sxs-lookup"><span data-stu-id="40cf4-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="40cf4-144">bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="40cf4-145">Jeśli typ hello jest nieznany, można użyć toodetermine wyboru typu które toocast jej.</span><span class="sxs-lookup"><span data-stu-id="40cf4-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="40cf4-146">Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello **zdjęć** kontenera:</span><span class="sxs-lookup"><span data-stu-id="40cf4-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="40cf4-147">Jak pokazano na powitania poprzedniego kodu, usługa blob hello ma koncepcji hello katalogów w kontenerach, jak również.</span><span class="sxs-lookup"><span data-stu-id="40cf4-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="40cf4-148">Jest to, dzięki czemu można organizować w strukturze więcej folderu przypominającej obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="40cf4-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="40cf4-149">Na przykład, należy wziąć pod uwagę następujące zestaw blokowych obiektów blob w kontenerze o nazwie hello **zdjęć**:</span><span class="sxs-lookup"><span data-stu-id="40cf4-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="40cf4-150">Podczas wywoływania **ListBlobs** na powitania kontenera (jak hello powyższego przykładu), zawiera hello kolekcji zwróconej **CloudBlobDirectory** i **CloudBlockBlob** obiektów reprezentujący hello katalogi i obiekty BLOB zawarte na najwyższym poziomie hello.</span><span class="sxs-lookup"><span data-stu-id="40cf4-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="40cf4-151">Poniżej przedstawiono dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="40cf4-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="40cf4-152">Opcjonalnie można ustawić hello **UseFlatBlobListing** parametr hello **ListBlobs** metodę **true**.</span><span class="sxs-lookup"><span data-stu-id="40cf4-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="40cf4-153">Powoduje to każdy obiekt blob jest zwracana jako **CloudBlockBlob**, niezależnie od tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="40cf4-154">W tym miejscu jest zbyt wywołania hello**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="40cf4-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="40cf4-155">a Oto hello wyników:</span><span class="sxs-lookup"><span data-stu-id="40cf4-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="40cf4-156">Aby uzyskać więcej informacji, zobacz [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="40cf4-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="40cf4-157">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="40cf4-157">Download blobs</span></span>
<span data-ttu-id="40cf4-158">obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **DownloadToStream** metody.</span><span class="sxs-lookup"><span data-stu-id="40cf4-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="40cf4-159">Witaj poniższym przykładzie użyto hello **DownloadToStream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="40cf4-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="40cf4-160">Można również użyć hello **DownloadToStream** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.</span><span class="sxs-lookup"><span data-stu-id="40cf4-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="40cf4-161">Usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="40cf4-161">Delete blobs</span></span>
<span data-ttu-id="40cf4-162">toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **usunąć** metody.</span><span class="sxs-lookup"><span data-stu-id="40cf4-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="40cf4-163">Asynchroniczne wyświetlanie obiektów blob na stronach</span><span class="sxs-lookup"><span data-stu-id="40cf4-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="40cf4-164">Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub ma toocontrol hello liczbę wyników zwracanych przez jedną operację wyświetlania listy, można wyświetlić listę obiektów blob na stronach wyników.</span><span class="sxs-lookup"><span data-stu-id="40cf4-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="40cf4-165">Ten przykład przedstawia, jak tooreturn wyników na stronach asynchronicznie, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania tooreturn dużych zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="40cf4-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="40cf4-166">W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również wykonywać listę hierarchiczną, przez ustawienie hello **useFlatBlobListing** parametru hello **ListBlobsSegmentedAsync** metody zbyt **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="40cf4-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="40cf4-167">Ponieważ hello przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem hello **async** — słowo kluczowe, a musi zwracać **zadań** obiektu.</span><span class="sxs-lookup"><span data-stu-id="40cf4-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="40cf4-168">określona dla hello — słowo kluczowe await Hello **ListBlobsSegmentedAsync** wstrzymuje wykonywanie hello przykładowej metody do momentu ukończenia zadania wyświetlania listy hello.</span><span class="sxs-lookup"><span data-stu-id="40cf4-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="40cf4-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40cf4-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

