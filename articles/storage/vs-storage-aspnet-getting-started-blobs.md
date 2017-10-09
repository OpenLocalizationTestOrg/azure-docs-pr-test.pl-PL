---
title: "aaaGet wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Sposób uruchamiania przy użyciu magazynu obiektów blob platformy Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu tooa konto magazynu przy użyciu programu Visual Studio usług połączonych tooget"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="eded1-103">Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eded1-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="eded1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="eded1-104">Overview</span></span>

<span data-ttu-id="eded1-105">Magazyn obiektów blob platformy Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="eded1-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eded1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="eded1-107">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="eded1-108">Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eded1-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="eded1-109">Scenariusze obejmują tworzenie kontenera obiektów blob i przekazywanie, wyświetlanie, pobieranie i usuwanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="eded1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eded1-110">Prerequisites</span></span>

* [<span data-ttu-id="eded1-111">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eded1-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="eded1-112">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="eded1-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="eded1-113">Tworzenie kontrolera MVC</span><span class="sxs-lookup"><span data-stu-id="eded1-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="eded1-114">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eded1-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="eded1-116">Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eded1-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="eded1-118">Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *BlobsController*i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eded1-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="eded1-120">Dodaj następujące hello *przy użyciu* toohello dyrektywy `BlobsController.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="eded1-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="eded1-121">Tworzenie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eded1-121">Create a blob container</span></span>

<span data-ttu-id="eded1-122">Kontener obiektów blob jest hierarchią zagnieżdżone obiekty BLOB i folderów.</span><span class="sxs-lookup"><span data-stu-id="eded1-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="eded1-123">Witaj poniższe kroki przedstawiają sposób toocreate kontenera obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="eded1-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eded1-124">Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eded1-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eded1-125">Otwórz hello `BlobsController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="eded1-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eded1-126">Dodaj metodę o nazwie **CreateBlobContainer** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eded1-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="eded1-127">W ramach hello **CreateBlobContainer** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eded1-128">Użyj następującego kodu tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="eded1-129">(Zmień  *&lt;nazwy konta magazynu >* toohello nazwę hello uzyskujesz dostęp do konta magazynu platformy Azure.)</span><span class="sxs-lookup"><span data-stu-id="eded1-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eded1-130">Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eded1-131">Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę odwołania toohello żądanego obiektu blob kontenera.</span><span class="sxs-lookup"><span data-stu-id="eded1-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="eded1-132">Witaj **CloudBlobClient.GetContainerReference** — metoda nie powoduje żądań dotyczących magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="eded1-133">czy istnieje hello kontenera obiektów blob, zwracane jest odwołanie Hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eded1-134">Wywołaj hello **CloudBlobContainer.CreateIfNotExists** metody toocreate hello kontener, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eded1-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="eded1-135">Witaj **CloudBlobContainer.CreateIfNotExists** metoda zwraca **true** Jeśli hello kontener nie istnieje i został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="eded1-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="eded1-136">W przeciwnym razie **false** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="eded1-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="eded1-137">Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="eded1-138">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="eded1-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eded1-139">Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateBlobContainer** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eded1-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="eded1-140">Otwórz `CreateBlobContainer.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="eded1-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="eded1-141">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eded1-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eded1-142">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eded1-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="eded1-143">Uruchamianie aplikacji hello, a następnie wybierz **Tworzenie kontenera obiektów Blob** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="eded1-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Tworzenie kontenera obiektów blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="eded1-145">Jak wspomniano wcześniej, hello **CloudBlobContainer.CreateIfNotExists** metoda zwraca **true** tylko, gdy hello kontenera nie istnieje i zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="eded1-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="eded1-146">W związku z tym po uruchomieniu aplikacji hello, gdy kontener hello istnieje, metoda hello zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="eded1-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="eded1-147">Aplikacja hello toorun wielokrotnie, należy usunąć kontener hello przed ponownym uruchomieniem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="eded1-148">Usunięcie kontenera hello może odbywać się za pośrednictwem hello **CloudBlobContainer.Delete** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="eded1-149">Możesz także usunąć kontener hello hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="eded1-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="eded1-150">Przekazywanie obiektu blob do kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eded1-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="eded1-151">Po wprowadzeniu [utworzono kontener obiektów blob](#create-a-blob-container), możesz przekazać pliki do tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="eded1-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="eded1-152">Ta sekcja przeprowadzi Cię przez przekazanie pliku lokalnego tooa kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="eded1-153">Witaj w krokach założono, po utworzeniu kontenera obiektów blob o nazwie *blobcontainer testu*.</span><span class="sxs-lookup"><span data-stu-id="eded1-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="eded1-154">Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eded1-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eded1-155">Otwórz hello `BlobsController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="eded1-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eded1-156">Dodaj metodę o nazwie **uploadblob dla platformy** zwracającą **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="eded1-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="eded1-157">W ramach hello **uploadblob dla platformy** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eded1-158">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="eded1-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eded1-159">Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eded1-160">Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="eded1-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eded1-161">Jak opisano wcześniej, usługa Azure storage obsługuje typy inny obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="eded1-162">tooretrieve odwołanie tooa stronicowy obiekt blob, wywołanie hello **CloudBlobContainer.GetPageBlobReference** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eded1-163">tooretrieve odwołanie tooa blokowego obiektu blob, wywołanie hello **CloudBlobContainer.GetBlockBlobReference** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="eded1-164">Zwykle blokowych obiektów blob jest hello zalecane toouse typu.</span><span class="sxs-lookup"><span data-stu-id="eded1-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="eded1-165">(Zmień < nazwa obiektu blob > * Nazwa toohello ma obiektu blob hello toogive raz przekazany.)</span><span class="sxs-lookup"><span data-stu-id="eded1-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="eded1-166">Po utworzeniu odwołanie do obiektu blob możesz przekazać żadnych tooit strumienia danych przez wywołanie obiektu hello blob odwołania **UploadFromStream** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="eded1-167">Witaj **UploadFromStream** metoda tworzy hello obiektów blob, jeśli nie istnieje lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="eded1-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="eded1-168">(Zmień  *&lt;przekazywania pliku >* tooa w pełni kwalifikowana ścieżka toohello pliku, który chcesz tooupload.)</span><span class="sxs-lookup"><span data-stu-id="eded1-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="eded1-169">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="eded1-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eded1-170">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eded1-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eded1-171">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eded1-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eded1-172">Uruchamianie aplikacji hello, a następnie wybierz **przekazywanie obiektu blob**.</span><span class="sxs-lookup"><span data-stu-id="eded1-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="eded1-173">Witaj sekcji - [listy hello BLOB w kontenerze obiektów blob](#list-the-blobs-in-a-blob-container) -ilustruje sposób toolist hello obiektów blob w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="eded1-174">Lista hello BLOB w kontenerze obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eded1-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="eded1-175">W tej części przedstawiono, jak toolist hello obiektów blob w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="eded1-176">Hello przykładowy kod odwołuje się do hello *testu blobcontainer* utworzony w sekcji hello [Tworzenie kontenera obiektów blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="eded1-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eded1-177">Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eded1-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eded1-178">Otwórz hello `BlobsController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="eded1-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eded1-179">Dodaj metodę o nazwie **ListBlobs** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eded1-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="eded1-180">W ramach hello **ListBlobs** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eded1-181">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="eded1-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eded1-182">Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eded1-183">Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="eded1-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eded1-184">toolist hello BLOB w kontenerze obiektów blob, użyj hello **CloudBlobContainer.ListBlobs** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="eded1-185">Witaj **CloudBlobContainer.ListBlobs** metoda zwraca **IListBlobItem** obiekt czy rzutowania tooa **CloudBlockBlob**, **CloudPageBlob**, lub **CloudBlobDirectory** obiektu.</span><span class="sxs-lookup"><span data-stu-id="eded1-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="eded1-186">Witaj poniższy fragment kodu wylicza wszystkie hello obiekty BLOB w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="eded1-187">Każdy obiekt blob jest rzutowanie toohello odpowiedni obiekt na podstawie typu i jego nazwę (lub identyfikator URI w przypadku hello **CloudBlobDirectory**) jest dodawany do listy tooa.</span><span class="sxs-lookup"><span data-stu-id="eded1-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="eded1-188">W tooblobs dodanie kontenerów obiektów blob może zawierać katalogów.</span><span class="sxs-lookup"><span data-stu-id="eded1-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="eded1-189">Załóżmy, że masz kontenera obiektów blob o nazwie *blobcontainer testu* z powitania po hierarchii:</span><span class="sxs-lookup"><span data-stu-id="eded1-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="eded1-190">Przy użyciu hello poprzedzających przykładowego kodu, hello **obiekty BLOB** ciąg lista zawiera wartości podobnie toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="eded1-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="eded1-191">Jak widać, hello lista zawiera tylko hello najwyższego poziomu jednostki; nie hello zagnieżdżone jedynek (*bar.png* i *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="eded1-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="eded1-192">toolist hello wszystkich jednostek w kontenerze obiektów blob, należy wywołać hello **CloudBlobContainer.ListBlobs** — metoda i przekazać **true** dla hello **useFlatBlobListing** parametr.</span><span class="sxs-lookup"><span data-stu-id="eded1-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="eded1-193">Ustawienie hello **useFlatBlobListing** parametru zbyt**true** zwraca płaska lista wszystkich jednostek w kontenerze obiektów blob hello i daje hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="eded1-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="eded1-194">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="eded1-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eded1-195">Na powitania **Dodaj widok** okna dialogowego, wprowadź **ListBlobs** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eded1-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="eded1-196">Otwórz `ListBlobs.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="eded1-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="eded1-197">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eded1-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eded1-198">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eded1-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="eded1-199">Uruchamianie aplikacji hello, a następnie wybierz **wyświetlanie obiektów blob** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="eded1-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Lista obiektów blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="eded1-201">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eded1-201">Download blobs</span></span>

<span data-ttu-id="eded1-202">W tej części przedstawiono, jak toodownload obiektu blob, a następnie zachować go toolocal magazynu lub odczytu zawartości hello na ciąg.</span><span class="sxs-lookup"><span data-stu-id="eded1-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="eded1-203">Hello przykładowy kod odwołuje się do hello *testu blobcontainer* utworzony w sekcji hello [Tworzenie kontenera obiektów blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="eded1-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="eded1-204">Otwórz hello `BlobsController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="eded1-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eded1-205">Dodaj metodę o nazwie **DownloadBlob** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eded1-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="eded1-206">W ramach hello **DownloadBlob** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eded1-207">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="eded1-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eded1-208">Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eded1-209">Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="eded1-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eded1-210">Pobierz przez wywołanie obiektu blob odwołania **CloudBlobContainer.GetBlockBlobReference** lub **CloudBlobContainer.GetPageBlobReference** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eded1-211">(Zmień  *&lt;nazwa obiektu blob >* toohello nazwa obiektu blob hello pobierasz.)</span><span class="sxs-lookup"><span data-stu-id="eded1-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="eded1-212">toodownload obiektu blob, użyj hello **CloudBlockBlob.DownloadToStream** lub **CloudPageBlob.DownloadToStream** metody, w zależności od typu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="eded1-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="eded1-213">Witaj poniższy fragment kodu używa hello **CloudBlockBlob.DownloadToStream** tootransfer metodę, obiekt strumienia tooa zawartość obiektu blob następnie utrwalone tooa pliku lokalnego: (zmiana  *&lt;nazwy pliku lokalnego >* toohello w pełni kwalifikowana, w którym ma obiektu blob hello pobrane reprezentujący nazwę pliku.)</span><span class="sxs-lookup"><span data-stu-id="eded1-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="eded1-214">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eded1-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eded1-215">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eded1-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eded1-216">Uruchamianie aplikacji hello, a następnie wybierz **pobieranie obiektu blob** toodownload hello blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="eded1-217">określony w hello blob Hello **CloudBlobContainer.GetBlockBlobReference** wywołanie metody pobiera toohello lokalizacji w hello **File.OpenWrite** wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="eded1-218">Usuwanie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eded1-218">Delete blobs</span></span>

<span data-ttu-id="eded1-219">Witaj poniższe kroki przedstawiają sposób toodelete obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="eded1-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eded1-220">Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eded1-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eded1-221">Otwórz hello `BlobsController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="eded1-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eded1-222">Dodaj metodę o nazwie **DeleteBlob** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eded1-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="eded1-223">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="eded1-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eded1-224">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="eded1-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eded1-225">Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.</span><span class="sxs-lookup"><span data-stu-id="eded1-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eded1-226">Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="eded1-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eded1-227">Pobierz przez wywołanie obiektu blob odwołania **CloudBlobContainer.GetBlockBlobReference** lub **CloudBlobContainer.GetPageBlobReference** metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eded1-228">(Zmień  *&lt;nazwa obiektu blob >* toohello nazwa obiektu blob hello usuwasz.)</span><span class="sxs-lookup"><span data-stu-id="eded1-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="eded1-229">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eded1-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eded1-230">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eded1-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eded1-231">Uruchamianie aplikacji hello, a następnie wybierz **usuwania obiektów blob** toodelete hello blob określone w hello **CloudBlobContainer.GetBlockBlobReference** wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="eded1-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eded1-232">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eded1-232">Next steps</span></span>
<span data-ttu-id="eded1-233">Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eded1-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="eded1-234">Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eded1-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="eded1-235">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eded1-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
