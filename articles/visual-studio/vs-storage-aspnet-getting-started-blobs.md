---
title: "aaaGet wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Sposób uruchamiania przy użyciu magazynu obiektów blob platformy Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu tooa konto magazynu przy użyciu programu Visual Studio usług połączonych tooget"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie

Magazyn obiektów blob platformy Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu magazynu obiektów blob platformy Azure. Scenariusze obejmują tworzenie kontenera obiektów blob i przekazywanie, wyświetlanie, pobieranie i usuwanie obiektów blob.

##<a name="prerequisites"></a>Wymagania wstępne

* [Program Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Konto usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Tworzenie kontrolera MVC 

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *BlobsController*i wybierz **Dodaj**.

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Dodaj następujące hello *przy użyciu* toohello dyrektywy `BlobsController.cs` pliku:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Tworzenie kontenera obiektów blob

Kontener obiektów blob jest hierarchią zagnieżdżone obiekty BLOB i folderów. Witaj poniższe kroki przedstawiają sposób toocreate kontenera obiektów blob:

> [!NOTE]
> 
> Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `BlobsController.cs` pliku.

1. Dodaj metodę o nazwie **CreateBlobContainer** zwracającą **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **CreateBlobContainer** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj następującego kodu tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello hello. (Zmień  *&lt;nazwy konta magazynu >* toohello nazwę hello uzyskujesz dostęp do konta magazynu platformy Azure.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę odwołania toohello żądanego obiektu blob kontenera. Witaj **CloudBlobClient.GetContainerReference** — metoda nie powoduje żądań dotyczących magazynu obiektów blob. czy istnieje hello kontenera obiektów blob, zwracane jest odwołanie Hello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Wywołaj hello **CloudBlobContainer.CreateIfNotExists** metody toocreate hello kontener, jeśli jeszcze nie istnieje. Witaj **CloudBlobContainer.CreateIfNotExists** metoda zwraca **true** Jeśli hello kontener nie istnieje i został utworzony pomyślnie. W przeciwnym razie **false** jest zwracany.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kontenera obiektów blob.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateBlobContainer** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `CreateBlobContainer.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **Tworzenie kontenera obiektów Blob** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Tworzenie kontenera obiektów blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Jak wspomniano wcześniej, hello **CloudBlobContainer.CreateIfNotExists** metoda zwraca **true** tylko, gdy hello kontenera nie istnieje i zostanie utworzony. W związku z tym po uruchomieniu aplikacji hello, gdy kontener hello istnieje, metoda hello zwraca **false**. Aplikacja hello toorun wielokrotnie, należy usunąć kontener hello przed ponownym uruchomieniem aplikacji hello. Usunięcie kontenera hello może odbywać się za pośrednictwem hello **CloudBlobContainer.Delete** metody. Możesz także usunąć kontener hello hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Przekazywanie obiektu blob do kontenera obiektów blob

Po wprowadzeniu [utworzono kontener obiektów blob](#create-a-blob-container), możesz przekazać pliki do tego kontenera. Ta sekcja przeprowadzi Cię przez przekazanie pliku lokalnego tooa kontenera obiektów blob. Witaj w krokach założono, po utworzeniu kontenera obiektów blob o nazwie *blobcontainer testu*. 

> [!NOTE]
> 
> Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `BlobsController.cs` pliku.

1. Dodaj metodę o nazwie **uploadblob dla platformy** zwracającą **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. W ramach hello **uploadblob dla platformy** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Jak opisano wcześniej, usługa Azure storage obsługuje typy inny obiektu blob. tooretrieve odwołanie tooa stronicowy obiekt blob, wywołanie hello **CloudBlobContainer.GetPageBlobReference** metody. tooretrieve odwołanie tooa blokowego obiektu blob, wywołanie hello **CloudBlobContainer.GetBlockBlobReference** metody. Zwykle blokowych obiektów blob jest hello zalecane toouse typu. (Zmień < nazwa obiektu blob > * Nazwa toohello ma obiektu blob hello toogive raz przekazany.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Po utworzeniu odwołanie do obiektu blob możesz przekazać żadnych tooit strumienia danych przez wywołanie obiektu hello blob odwołania **UploadFromStream** metody. Witaj **UploadFromStream** metoda tworzy hello obiektów blob, jeśli nie istnieje lub zastąpiony, jeśli istnieje. (Zmień  *&lt;przekazywania pliku >* tooa w pełni kwalifikowana ścieżka toohello pliku, który chcesz tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **przekazywanie obiektu blob**.  
  
Witaj sekcji - [listy hello BLOB w kontenerze obiektów blob](#list-the-blobs-in-a-blob-container) -ilustruje sposób toolist hello obiektów blob w kontenerze obiektów blob.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Lista hello BLOB w kontenerze obiektów blob

W tej części przedstawiono, jak toolist hello obiektów blob w kontenerze obiektów blob. Hello przykładowy kod odwołuje się do hello *testu blobcontainer* utworzony w sekcji hello [Tworzenie kontenera obiektów blob](#create-a-blob-container).

> [!NOTE]
> 
> Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `BlobsController.cs` pliku.

1. Dodaj metodę o nazwie **ListBlobs** zwracającą **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **ListBlobs** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. toolist hello BLOB w kontenerze obiektów blob, użyj hello **CloudBlobContainer.ListBlobs** metody. Witaj **CloudBlobContainer.ListBlobs** metoda zwraca **IListBlobItem** obiekt czy rzutowania tooa **CloudBlockBlob**, **CloudPageBlob**, lub **CloudBlobDirectory** obiektu. Witaj poniższy fragment kodu wylicza wszystkie hello obiekty BLOB w kontenerze obiektów blob. Każdy obiekt blob jest rzutowanie toohello odpowiedni obiekt na podstawie typu i jego nazwę (lub identyfikator URI w przypadku hello **CloudBlobDirectory**) jest dodawany do listy tooa.

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

    W tooblobs dodanie kontenerów obiektów blob może zawierać katalogów. Załóżmy, że masz kontenera obiektów blob o nazwie *blobcontainer testu* z powitania po hierarchii:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Przy użyciu hello poprzedzających przykładowego kodu, hello **obiekty BLOB** ciąg lista zawiera wartości podobnie toohello poniżej:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Jak widać, hello lista zawiera tylko hello najwyższego poziomu jednostki; nie hello zagnieżdżone jedynek (*bar.png* i *baz.png*). toolist hello wszystkich jednostek w kontenerze obiektów blob, należy wywołać hello **CloudBlobContainer.ListBlobs** — metoda i przekazać **true** dla hello **useFlatBlobListing** parametr.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Ustawienie hello **useFlatBlobListing** parametru zbyt**true** zwraca płaska lista wszystkich jednostek w kontenerze obiektów blob hello i daje hello następujące wyniki:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **obiekty BLOB**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **ListBlobs** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `ListBlobs.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

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

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **wyświetlanie obiektów blob** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Lista obiektów blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Pobieranie obiektów blob

W tej części przedstawiono, jak toodownload obiektu blob, a następnie zachować go toolocal magazynu lub odczytu zawartości hello na ciąg. Hello przykładowy kod odwołuje się do hello *testu blobcontainer* utworzony w sekcji hello [Tworzenie kontenera obiektów blob](#create-a-blob-container).

1. Otwórz hello `BlobsController.cs` pliku.

1. Dodaj metodę o nazwie **DownloadBlob** zwracającą **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. W ramach hello **DownloadBlob** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Pobierz przez wywołanie obiektu blob odwołania **CloudBlobContainer.GetBlockBlobReference** lub **CloudBlobContainer.GetPageBlobReference** metody. (Zmień  *&lt;nazwa obiektu blob >* toohello nazwa obiektu blob hello pobierasz.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload obiektu blob, użyj hello **CloudBlockBlob.DownloadToStream** lub **CloudPageBlob.DownloadToStream** metody, w zależności od typu obiektu blob hello. Witaj poniższy fragment kodu używa hello **CloudBlockBlob.DownloadToStream** tootransfer metodę, obiekt strumienia tooa zawartość obiektu blob następnie utrwalone tooa pliku lokalnego: (zmiana  *&lt;nazwy pliku lokalnego >* toohello w pełni kwalifikowana, w którym ma obiektu blob hello pobrane reprezentujący nazwę pliku.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **pobieranie obiektu blob** toodownload hello blob. określony w hello blob Hello **CloudBlobContainer.GetBlockBlobReference** wywołanie metody pobiera toohello lokalizacji w hello **File.OpenWrite** wywołania metody. 

## <a name="delete-blobs"></a>Usuwanie obiektów blob

Witaj poniższe kroki przedstawiają sposób toodelete obiektu blob:

> [!NOTE]
> 
> Witaj kodu w tej sekcji założono, że zostały wykonane kroki hello w sekcji hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `BlobsController.cs` pliku.

1. Dodaj metodę o nazwie **DeleteBlob** zwracającą **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudBlobClient** obiekt reprezentuje klienta usługi blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Pobierz **CloudBlobContainer** obiekt, który reprezentuje nazwę kontenera obiektów blob toohello odwołania. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Pobierz przez wywołanie obiektu blob odwołania **CloudBlobContainer.GetBlockBlobReference** lub **CloudBlobContainer.GetPageBlobReference** metody. (Zmień  *&lt;nazwa obiektu blob >* toohello nazwa obiektu blob hello usuwasz.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **usuwania obiektów blob** toodelete hello blob określone w hello **CloudBlobContainer.GetBlockBlobReference** wywołania metody. 

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.

  * [Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
