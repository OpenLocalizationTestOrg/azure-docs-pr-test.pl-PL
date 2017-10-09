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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (platformy ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uruchamiania przy użyciu magazynu obiektów Blob platformy Azure w programie Visual Studio po utworzony lub odwołuje się do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą okna dialogowego programu Visual Studio Dodaj połączone usługi hello tooget.

Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, którego mogą uzyskać dostęp z dowolnego miejsca Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. Pojedynczego obiektu blob może być dowolnym rozmiarze. Obiekty BLOB można np. obrazów, plików audio i wideo, nieprzetworzone dane i pliki dokumentów. W tym artykule opisano, jak tooget pracę z magazynu obiektów blob, po utworzeniu konta magazynu platformy Azure przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego w projekcie platformy ASP.NET Core.

Tak samo, jak żywe plików w folderach, na żywo magazynu obiektów blob w kontenerach. Po utworzeniu magazynu tworzenia kontenerach hello magazynu. Na przykład magazynu o nazwie "Pamiętnik", można tworzyć kontenery w magazynie hello o nazwie "obrazy" toostore obrazów i innej o nazwie "audio" toostore plików audio. Po utworzeniu hello kontenerów, możesz przekazać toothem plików poszczególnych obiektów blob. Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) uzyskać więcej informacji o programowo manipulowanie obiektów blob.

## <a name="access-blob-containers-in-code"></a>Dostęp do kontenerów obiektów blob w kodzie
tooprogrammatically dostęp do obiektów blob platformy ASP.NET Core projektów, należy hello tooadd następujące elementy, jeśli nie są one już istnieje.

1. Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello górnej części każdego C# pliku, w której ma zostać tooprogrammatically dostępu do magazynu Azure.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące sekcje.
3. Użyj **CloudBlobClient** obiekt tooget **CloudBlobContainer** odwołania tooan istniejącego kontenera na koncie magazynu.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Tworzenie kontenera w kodzie
Można również użyć hello **CloudBlobClient** toocreate kontenera na koncie magazynu. Toodo wystarczy tooadd wywołanie za**CreateIfNotExistsAsync** jak hello następującego kodu:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Uwaga:** hello interfejsów API, które wykonywania wywołań tooAzure magazynu w ASP.NET Core są asynchroniczne. Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji. Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.

pliki hello toomake tooeveryone dostępne hello kontenera, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
tooupload pliku blob do kontenera, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob. Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStreamAsync** metody. Tej operacji tworzy hello obiektów blob, jeśli nie jest jeszcze określony lub zastąpiony, jeśli istnieje. powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera. Kontener hello może wywoływać **ListBlobsSegmentedAsync** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi. bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu. Jeśli nie znasz typu blob hello, możesz użyć toodetermine wyboru typu które toocast jej. Witaj następującego kodu pokazano, jak tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w kontenerze.

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

Istnieją inne sposoby toolist hello zawartość kontenera obiektów blob. Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) Aby uzyskać więcej informacji.

## <a name="download-a-blob"></a>Pobieranie obiektu blob
toodownload obiektu blob, najpierw pobrać odwołanie do obiektu blob toohello, a następnie wywołać hello **DownloadToStreamAsync** metody. Witaj poniższym przykładzie użyto hello **DownloadToStreamAsync** metody tootransfer hello blob zawartość tooa obiektu strumienia, który można zapisać jako plik lokalny.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Istnieją inne sposoby toosave obiekty BLOB jako plików. Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) Aby uzyskać więcej informacji.

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob toohello, a następnie wywołać hello **DeleteAsync** dla niego metodę.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

