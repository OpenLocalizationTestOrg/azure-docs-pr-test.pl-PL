---
title: Tworzenie funkcji platformy Azure z programem Media Services
description: "W tym temacie pokazano, jak rozpocząć tworzenie usługi Azure Functions w usłudze Media Services przy użyciu portalu Azure."
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
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Tworzenie funkcji platformy Azure z programem Media Services

W tym temacie przedstawiono, jak rozpocząć pracę z tworzeniem usługi Azure Functions, używanego przez usługi Media Services. Funkcja Azure zdefiniowane w tym temacie monitoruje kontenera konta magazynu o nazwie **wejściowych** dla nowych plików MP4. Gdy plik zostanie upuszczony do kontenera magazynu, wyzwalacza obiektu blob wykona funkcji.

Jeśli chcesz Eksploruj i wdrożyć istniejącej usługi Azure Functions, używanego przez usługi Azure Media Services, zapoznaj się [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). To repozytorium zawiera przykłady, które za pomocą usługi Media Services można wyświetlić przepływów pracy związanych z wprowadzania zawartości bezpośrednio z magazynu obiektów blob, kodowanie i zapisywania zawartości z powrotem do magazynu obiektów blob. Zawiera również przykłady monitorować powiadomienia zadania za pomocą elementów Webhook i kolejek Azure. Można również zaprojektować funkcji w oparciu o przykłady w [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repozytorium. Aby wdrożyć funkcje, naciśnij klawisz **wdrażanie na platformie Azure** przycisku.

## <a name="prerequisites"></a>Wymagania wstępne

- Przed utworzeniem pierwszej funkcji musisz mieć aktywne konto platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, [dostępne są konta bezpłatne](https://azure.microsoft.com/free/).
- Jeśli zamierzasz utworzyć usługi Azure Functions, wykonywać działania na Twoim koncie usługi Azure Media Services (AMS) lub nasłuchiwania zdarzeń wysłanych przez usługę Media Services, należy utworzyć konta usługi AMS zgodnie z opisem [tutaj](media-services-portal-create-account.md).
- Opis elementu [sposób użycia funkcji Azure](../azure-functions/functions-overview.md). Sprawdź również:
    - [Środowisko Azure functions powiązania protokołu HTTP i elementu webhook](../azure-functions/functions-triggers-bindings.md)
    - [Jak skonfigurować ustawienia aplikacji Azure — funkcja](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Zagadnienia do rozważenia

-  Środowisko Azure Functions do uruchamiania planu zużycie ma limit czasu 5 minut.

## <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

1. Przejdź do [witryny Azure Portal](http://portal.azure.com) i zaloguj się przy użyciu konta Azure.
2. Tworzenie aplikacji funkcji, zgodnie z opisem [tutaj](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Konto magazynu, którą można określić w **StorageConnection** zmiennej środowiskowej (patrz następny krok) powinna być w tym samym regionie co aplikacja.

## <a name="configure-function-app-settings"></a>Konfiguruj ustawienia aplikacji — funkcja

Podczas tworzenia usługi Media Services funkcje, warto dodać zmiennych środowiskowych, które będą używane w całej funkcji. Aby skonfigurować ustawienia aplikacji, kliknij łącze Konfiguruj ustawienia aplikacji. Aby uzyskać więcej informacji, zobacz [sposób konfigurowania ustawień aplikacji funkcji platformy Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Na przykład:

![Ustawienia](./media/media-services-azure-functions/media-services-azure-functions001.png)

Funkcja zdefiniowana w tym artykule przyjęto założenie, że masz następujące zmienne środowiskowe w ustawieniach aplikacji:

**AMSAccount** : *nazwa konta usługi AMS* (np. testams)

**AMSKey** : *klucz konta usługi AMS* (np. IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *nazwy konta magazynu* (np. testamsstorage)

**MediaServicesStorageAccountKey** : *klucz konta magazynu* (np. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *połączenia z magazynem* (np. DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)

## <a name="create-a-function"></a>Tworzenie funkcji

Po wdrożeniu aplikacji funkcji można znaleźć wśród **usługi aplikacji** usługi Azure Functions.

1. Wybierz aplikację funkcji, a następnie kliknij przycisk **nową funkcję**.
2. Wybierz **C#** języka i **przetwarzania danych** scenariusza.
3. Wybierz **BlobTrigger** szablonu. Ta funkcja zostanie wyzwolone przy każdym obiektu blob jest przekazywany do **wejściowych** kontenera. **Wejściowych** nazwa została określona w **ścieżki**, w następnym kroku.

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Po wybraniu **BlobTrigger**, niektóre formanty więcej będą wyświetlane na stronie.

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Kliknij przycisk **Utwórz**. 


## <a name="files"></a>Pliki

Funkcja Azure jest skojarzony z plików kodu i innych plików, które zostały opisane w tej sekcji. Domyślnie funkcja jest skojarzony z **function.json** i **run.csx** plików (C#). Należy dodać **project.json** pliku. Pozostałej części tej sekcji przedstawiono definicje tych plików.

![Pliki](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Plik function.json definiuje, powiązania funkcji i innych ustawień konfiguracyjnych. Środowisko uruchomieniowe korzysta z tego pliku, aby określić zdarzenia do monitorowania oraz sposób przekazywania danych do i zwracać dane z wykonywania funkcji. Aby uzyskać więcej informacji, zobacz [Azure functions powiązania protokołu HTTP i webhook](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Ustaw **wyłączone** właściwości **true** aby zapobiec wykonywana przez funkcję. 


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

Plik project.json zawiera zależności. Oto przykład **project.json** plik zawierający wymagane pakiety platformy .NET usługi Azure Media Services z pakietu Nuget. Należy pamiętać, że numery wersji ulegnie zmianie z najnowszymi aktualizacjami do pakietów, dlatego należy upewnić się, najnowsze wersje. 

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

To jest kod C# dla funkcji.  Funkcja zdefiniowana poniżej monitorów kontenera konta magazynu o nazwie **wejściowych** (tzn. jak określono w ścieżce) dla nowych plików MP4. Gdy plik zostanie upuszczony do kontenera magazynu, wyzwalacza obiektu blob wykona funkcji.
    
W przykładzie zdefiniowano w tej sekcji pokazano 

1. jak pozyskiwania zasób do konta usługi Media Services (przez kopiowanie obiektu blob do elementu zawartości AMS) i 
2. w jaki sposób można przesłać zadania kodowania, która używa Media Encoder Standard "Adaptacyjne przesyłanie strumieniowe" wstępnie.

W tym scenariuszu rzeczywistych prawdopodobnie chcesz śledzić postęp zadania, a następnie opublikować z zakodowanym elementem zawartości. Aby uzyskać więcej informacji, zobacz [elementów Webhook Azure używana do monitorowania usługi Media Services zadania powiadomienia](media-services-dotnet-check-job-progress-with-webhooks.md). Aby uzyskać więcej przykładów, zobacz [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

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
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
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

        // Get the destination asset container reference
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

        // Get hold of the destination blob
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

Aby przetestować funkcję, należy przekazać plik MP4 do **wejściowych** kontenera konta magazynu, który określono w parametrach połączenia.  

## <a name="next-step"></a>Następny krok

W tym momencie można przystąpić do rozpocząć tworzenie aplikacji usługi Media Services. 
 
Bardziej szczegółowe informacje i kompletnych rozwiązań/przykłady korzystania z usługi Azure Functions i Logic Apps usłudze Azure Media Services do tworzenia przepływów pracy niestandardowe tworzenie zawartości, zobacz [Media Services .NET funkcje Integraiton przykładem w witrynie GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Zobacz też [elementów Webhook Azure używana do monitorowania usługi Media Services zadania powiadomienia z platformą .NET](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

