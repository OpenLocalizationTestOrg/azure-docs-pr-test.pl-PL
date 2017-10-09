---
title: "aaaDevelop funkcje Azure za pomocą usługi Media Services"
description: "W tym temacie przedstawiono sposób tworzenia funkcje platformy Azure za pomocą usługi Media Services przy użyciu toostart hello portalu Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Tworzenie funkcji platformy Azure z programem Media Services

W tym temacie pokazano, jak tooget pracę z tworzenia usługi Azure Functions, używanego przez usługi Media Services. Witaj funkcji platformy Azure, zdefiniowane w tym temacie monitoruje kontenera konta magazynu o nazwie **wejściowych** dla nowych plików MP4. Gdy plik zostanie upuszczony do kontenera magazynu hello, wyzwalacza obiektu blob hello wykona hello funkcji.

Jeśli chcesz tooexplore i wdrażanie istniejących funkcji platformy Azure korzystające z usługi Azure Media Services, zapoznaj się [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). To repozytorium zawiera przykłady korzystających z usługi Media Services tooshow przepływy pracy pokrewne tooingesting zawartości bezpośrednio z magazynu obiektów blob, kodowanie i zapisywania zawartości ponownie tooblob magazynu. Zawiera również przykłady sposobu toomonitor zadania powiadomienia za pomocą elementów Webhook i kolejek Azure. Można również zaprojektować funkcji oparte na powitania przykłady w hello [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repozytorium. Funkcje hello toodeploy, naciśnij klawisz hello **wdrażanie tooAzure** przycisku.

## <a name="prerequisites"></a>Wymagania wstępne

- Przed utworzeniem pierwszej funkcji, należy toohave aktywne konto platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, [dostępne są konta bezpłatne](https://azure.microsoft.com/free/).
- Jeśli zamierzasz toocreate usługi Azure Functions, wykonywać działania na Twoim koncie usługi Azure Media Services (AMS) lub nasłuchiwania tooevents wysyłane przez usługę Media Services, należy utworzyć konta usługi AMS zgodnie z opisem [tutaj](media-services-portal-create-account.md).
- Opis elementu [jak toouse Azure funkcji](../azure-functions/functions-overview.md). Sprawdź również:
    - [Środowisko Azure functions powiązania protokołu HTTP i elementu webhook](../azure-functions/functions-triggers-bindings.md)
    - [Jak ustawienia aplikacji tooconfigure funkcji platformy Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Zagadnienia do rozważenia

-  Środowisko Azure Functions do uruchamiania planu zużycie hello ma limit czasu 5 minut.

## <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

1. Przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.
2. Tworzenie aplikacji funkcji, zgodnie z opisem [tutaj](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Konto magazynu w hello **StorageConnection** zmiennej środowiskowej (patrz następny krok hello) musi należeć do hello tym samym regionie co aplikacja.

## <a name="configure-function-app-settings"></a>Konfiguruj ustawienia aplikacji — funkcja

Podczas tworzenia usługi Media Services funkcje, jest przydatne tooadd zmiennych środowiskowych, które będą używane w całej funkcji. Ustawienia aplikacji tooconfigure, kliknij łącze Konfiguruj ustawienia aplikacji hello. Aby uzyskać więcej informacji, zobacz [jak ustawienia aplikacji funkcji platformy Azure tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Na przykład:

![Ustawienia](./media/media-services-azure-functions/media-services-azure-functions001.png)

Funkcja Hello, zdefiniowana w tym artykule przyjęto założenie, że masz następujące zmienne środowiskowe w ustawieniach aplikacji hello:

**AMSAccount** : *nazwa konta usługi AMS* (np. testams)

**AMSKey** : *klucz konta usługi AMS* (np. IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *nazwy konta magazynu* (np. testamsstorage)

**MediaServicesStorageAccountKey** : *klucz konta magazynu* (np. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *połączenia z magazynem* (np. DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)

## <a name="create-a-function"></a>Tworzenie funkcji

Po wdrożeniu aplikacji funkcji można znaleźć wśród **usługi aplikacji** usługi Azure Functions.

1. Wybierz aplikację funkcji, a następnie kliknij przycisk **nową funkcję**.
2. Wybierz hello **C#** języka i **przetwarzania danych** scenariusza.
3. Wybierz **BlobTrigger** szablonu. Ta funkcja zostanie wyzwolone przy każdym obiektu blob jest przekazywany do hello **wejściowych** kontenera. Witaj **wejściowych** nazwa została określona w hello **ścieżki**, w następnym kroku hello.

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Po wybraniu **BlobTrigger**, niektóre formanty więcej będą wyświetlane na stronie powitania.

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Kliknij przycisk **Utwórz**. 


## <a name="files"></a>Pliki

Funkcja Azure jest skojarzony z plików kodu i innych plików, które zostały opisane w tej sekcji. Domyślnie funkcja jest skojarzony z **function.json** i **run.csx** plików (C#). Konieczne będzie tooadd **project.json** pliku. Hello pozostałej części tej sekcji przedstawiono definicje hello tych plików.

![Pliki](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Plik function.json Hello definiuje powiązania funkcji hello i innych ustawień konfiguracyjnych. środowiska uruchomieniowego Hello korzysta z tego pliku toodetermine hello zdarzenia toomonitor i sposób wykonywania funkcji toopass dane i zwracanych danych z. Aby uzyskać więcej informacji, zobacz [Azure functions powiązania protokołu HTTP i webhook](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Zestaw hello **wyłączone** właściwości zbyt**true** funkcja hello tooprevent wstrzymywane. 


Oto przykład **function.json** pliku.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>Project.JSON

Plik project.json Hello zawiera zależności. Oto przykład **project.json** plik zawierający hello wymagane .NET Azure Media Services pakietów z pakietu Nuget. Należy pamiętać, że hello numery wersji ulegnie zmianie z najnowszymi aktualizacjami pakiety toohello, należy się upewnić, hello najnowsze wersje. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>Run.csx

Jest to hello C# kod dla funkcji.  Funkcja Hello zdefiniowana poniżej monitorów kontenera konta magazynu o nazwie **wejściowych** (tzn. jak określono w ścieżce hello) dla nowych plików MP4. Gdy plik zostanie upuszczony do kontenera magazynu hello, wyzwalacza obiektu blob hello wykona hello funkcji.
    
przykład Witaj zdefiniowane w tej sekcji przedstawiono 

1. jak tooingest zasób do usługi Media Services konta (przez kopiowanie obiektu blob do elementu zawartości AMS) i 
2. jak toosubmit zadania kodowania, która używa Media Encoder Standard "adaptacyjne przesyłanie strumieniowe" wstępnie.

W scenariuszu Witaj świecie rzeczywistym najprawdopodobniej mają tootrack postęp zadania, a następnie opublikuj z zakodowanym elementem zawartości. Aby uzyskać więcej informacji, zobacz [elementów Webhook Azure Użyj toomonitor Media Services zadania powiadomienia](media-services-dotnet-check-job-progress-with-webhooks.md). Aby uzyskać więcej przykładów, zobacz [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Po zakończeniu definiowania funkcji kliknij **Zapisz i uruchom**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>Testowanie funkcji

tootest funkcji, należy tooupload plik MP4 do hello **wejściowych** kontenera hello konta magazynu, który określono w parametrach połączenia hello.  

## <a name="next-step"></a>Następny krok

W tym momencie wszystko jest gotowe toostart opracowanie aplikacji usługi Media Services. 
 
Aby uzyskać więcej szczegółów i kompletnych rozwiązań/przykłady korzystania z usługi Azure Functions i aplikacje logiki z przepływami pracy niestandardowe tworzenie zawartości toocreate usługi Azure Media Services, zobacz hello [Media Services .NET funkcje Integraiton przykładem w witrynie GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Zobacz też [elementów Webhook Azure Użyj toomonitor Media Services zadania powiadomienia z platformą .NET](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

