---
title: "aaaGet wprowadzenie do magazynu obiektów blob i Visual Studio podłączonych usług (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu obiektów Blob platformy Azure w projektu usługi w chmurze w programie Visual Studio po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Wprowadzenie do usługi Azure Blob Storage i Visual Studio połączone usługi (usług w chmurze projekty)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooget pracę z magazynu obiektów Blob Azure po utworzeniu lub odwołuje się do konta usługi Azure Storage za pomocą programu Visual Studio hello **dodać usług połączonych** projektu usług okna dialogowego w chmurze programu Visual Studio. Poniżej opisano sposób tooaccess i tworzenie kontenerów obiektów blob i jak tooperform typowych zadań, takich jak przekazywanie, wyświetlania i pobieranie obiektów blob. Przykłady Hello są napisane w języku C\# i użyj hello [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. Pojedynczego obiektu blob może być dowolnym rozmiarze. Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów.

Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach. Po utworzeniu magazynu tworzenia kontenerach hello magazynu. Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie hello o nazwie "obrazy" toostore obrazów i innej o nazwie "audio" toostore plików audio. Po utworzeniu hello kontenerów, możesz przekazać toothem plików poszczególnych obiektów blob.

* Aby uzyskać więcej informacji na programowo manipulowanie obiektów blob, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md).
* Aby uzyskać ogólne informacje na temat usługi Azure Storage, zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/).
* Aby uzyskać ogólne informacje o usługach w chmurze Azure, zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/).
* Aby uzyskać więcej informacji na temat programowania aplikacji programu ASP.NET, zobacz [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Dostęp do kontenerów obiektów blob w kodzie
tooprogrammatically dostęp do obiektów blob projekty usługi w chmurze, należy hello tooadd następujące elementy, jeśli nie są one już istnieje.

1. Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello górnej części każdego C# pliku, w którym chcesz tooprogrammatically dostępu do magazynu Azure.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Pobierz **CloudBlobClient** obiekt tooreference istniejącego kontenera na koncie magazynu.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Pobierz **CloudBlobContainer** obiekt tooreference kontenera konkretnego obiektu blob.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Korzystanie ze wszystkich hello kodem przedstawionym w poprzedniej procedurze hello przed hello kodu pokazano hello następujące sekcje.
> 
> 

## <a name="create-a-container-in-code"></a>Tworzenie kontenera w kodzie
> [!NOTE]
> Niektórych interfejsów API służących do wykonywania wywołań wychodzących tooAzure magazynu w ASP.NET są asynchroniczne. Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji. Kod Hello w hello poniższy przykład zakłada, używasz metody programowania asynchronicznego.
> 
> 

toocreate kontenera na koncie magazynu, wszystko, czego potrzebujesz toodo jest Dodaj wywołanie za**CreateIfNotExistsAsync** jak hello następującego kodu:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


pliki hello toomake tooeveryone dostępne hello kontenera, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu odpowiednie hello.

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
Usługa Azure Storage obsługuje blokowe i stronicowe obiekty BLOB. W większości przypadków hello blokowych obiektów blob jest hello zalecane toouse typu.

tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku. Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStream** metody. Ta operacja tworzy hello obiektów blob, jeśli wcześniej nie istnieje lub zastąpiony, jeśli istnieje. powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera. Można użyć kontenera hello **ListBlobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi. bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu. Jeśli typ hello jest nieznany, można użyć toodetermine wyboru typu które toocast jej. Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello **zdjęć** kontenera:

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

Jak pokazano na powitania poprzedniego kodu, usługa blob hello ma koncepcji hello katalogów w kontenerach, jak również. Jest to, dzięki czemu można organizować w strukturze więcej folderu przypominającej obiektów blob. Na przykład, należy wziąć pod uwagę następujące zestaw blokowych obiektów blob w kontenerze o nazwie hello **zdjęć**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Podczas wywoływania **ListBlobs** na powitania kontenera (jak hello powyższego przykładu), zawiera hello kolekcji zwróconej **CloudBlobDirectory** i **CloudBlockBlob** obiektów reprezentujący hello katalogi i obiekty BLOB zawarte na najwyższym poziomie hello. Poniżej przedstawiono dane wyjściowe hello:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Opcjonalnie można ustawić hello **UseFlatBlobListing** parametr hello **ListBlobs** metodę **true**. Powoduje to każdy obiekt blob jest zwracana jako **CloudBlockBlob**, niezależnie od tego katalogu. W tym miejscu jest zbyt wywołania hello**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

a Oto hello wyników:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Aby uzyskać więcej informacji, zobacz [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Pobieranie obiektów blob
obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **DownloadToStream** metody. Witaj poniższym przykładzie użyto hello **DownloadToStream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Można również użyć hello **DownloadToStream** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Usuwanie obiektów blob
toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **usunąć** metody.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Asynchroniczne wyświetlanie obiektów blob na stronach
Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub ma toocontrol hello liczbę wyników zwracanych przez jedną operację wyświetlania listy, można wyświetlić listę obiektów blob na stronach wyników. Ten przykład przedstawia, jak tooreturn wyników na stronach asynchronicznie, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania tooreturn dużych zestawów wyników.

W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również wykonywać listę hierarchiczną, przez ustawienie hello **useFlatBlobListing** parametru hello **ListBlobsSegmentedAsync** metody zbyt **FALSE**.

Ponieważ hello przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem hello **async** — słowo kluczowe, a musi zwracać **zadań** obiektu. określona dla hello — słowo kluczowe await Hello **ListBlobsSegmentedAsync** wstrzymuje wykonywanie hello przykładowej metody do momentu ukończenia zadania wyświetlania listy hello.

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

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

