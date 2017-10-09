---
title: "pliki aaaUpload do konta usługi Media Services przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nośnika tooget zawartości do usługi Media Services za tworzenie i przekazywanie zasoby."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Przekazywanie plików do konta usługi Media Services przy użyciu platformy .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

Za pomocą usługi Media Services można przekazać (lub pozyskać) pliki cyfrowe do elementu zawartości. Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.)  Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.

pliki Hello w hello zasobów są nazywane **plików zasobów**. Witaj **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty. wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.

> [!NOTE]
> Zastosuj Hello następujące zagadnienia:
> 
> * Usługi Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone. Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #". Ponadto może istnieć tylko jeden "." hello rozszerzenie.
> * Długość Hello hello nazwy nie może być większa niż 260 znaków.
> * Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services. Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.
> * Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.
> 

Podczas tworzenia zasobów, można określić hello następujące opcje szyfrowania. 

* **None** — szyfrowanie nie jest stosowane. Jest to wartość domyślna hello. Należy pamiętać, że podczas korzystania z tej opcji zawartość nie jest chroniony w trakcie przesyłania lub przechowywania w magazynie.
  Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji. 
* **CommonEncryption** — ta opcja umożliwia przekazanie zawartości, który został już szyfrowane i chronione za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione za pomocą technologii PlayReady DRM).
* **EnvelopeEncrypted** — Użyj tej opcji, Jeśli przesyłasz HLS zaszyfrowanych z użyciem standardu AES. Należy pamiętać, że pliki hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.
* **StorageEncrypted** — szyfruje zawartości lokalnie, przy użyciu standardu AES 256-bitowego, a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku.
  
    Usługa Media Services udostępnia szyfrowanie magazynu na dysku dla zasobów, nie w locie podobnie jak Menedżer prawami cyfrowymi (DRM).
  
    Jeśli element zawartości jest szyfrowany w magazynie, należy skonfigurować zasady dostarczania elementu zawartości. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md).

Jeśli określisz dla Twojego toobe zasobów zaszyfrowane za pomocą **CommonEncrypted** opcji lub **EnvelopeEncypted** opcji, konieczne będzie tooassociate zawartości z **ContentKey**. Aby uzyskać więcej informacji, zobacz [jak toocreate ContentKey](media-services-dotnet-create-contentkey.md). 

Jeśli określisz dla Twojego toobe zasobów zaszyfrowane za pomocą **StorageEncrypted** hello SDK usługi Media Services dla platformy .NET zostanie utworzona, należy **StorateEncrypted** **ContentKey** dla użytkownika zasobów.

W tym temacie pokazano, jak usługi multimediów toouse .NET SDK, a także pliki tooupload rozszerzenia .NET SDK usługi Media Services do zawartości Media Services.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Przekaż pojedynczy plik z zestawu .NET SDK usługi multimediów
Poniższy kod przykładowy Hello korzysta z zestawu .NET SDK tooupload pojedynczy plik. Witaj AccessPolicy i Locator są tworzone i niszczone przez funkcję przekazywania hello. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Przekazywania wielu plików z zestawu .NET SDK usługi multimediów
Witaj następującego kodu pokazuje sposób toocreate zasobów i przekazywania wielu plików.

Kod Hello hello następujące:

* Tworzy pusty zasobów przy użyciu metody CreateEmptyAsset hello zdefiniowanej w poprzednim kroku hello.
* Tworzy **AccessPolicy** wystąpienie definiujące hello uprawnienia i czas trwania dostępu toohello zasobów.
* Tworzy **lokalizatora** wystąpienia, która zapewnia dostęp do zasobów toohello.
* Tworzy **BlobTransferClient** wystąpienia. Ten typ przedstawia klienta, który działa na powitalne obiektów blob Azure. W tym przykładzie używamy powitania klienta toomonitor hello przekazywania postępu. 
* Wylicza pliki w określonym katalogu hello i tworzy **AssetFile** wystąpienia dla każdego pliku.
* Przekazywanie hello plików do usługi Media Services przy użyciu hello **UploadAsync** metody. 

> [!NOTE]
> Użyj hello UploadAsync metody tooensure nie blokują hello wywołań i hello pliki są wysyłane równolegle.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Podczas przekazywania dużej liczby zasobów, należy wziąć pod uwagę następujące hello.

* Utwórz nową **CloudMediaContext** obiektu na wątek. Witaj **CloudMediaContext** klasa nie jest bezpieczne dla wątków.
* Zwiększ NumberOfConcurrentTransfers z hello wartość domyślną 2 tooa wyższa wartość 5. Ustawienie tej właściwości dotyczy wszystkich wystąpień **CloudMediaContext**. 
* Zachowaj ParallelTransferThreadCount na powitania wartość domyślną równą 10.

## <a id="ingest_in_bulk"></a>Pozyskaniu elementów zawartości zbiorczo przy użyciu zestawu .NET SDK usługi multimediów
Przekazywanie zawartości dużych plików może być wąskie gardło podczas tworzenia zasobu. Pozyskaniu elementów zawartości w zbiorczej lub "Zbiorczego wprowadzania", polega na rozdzieleniu tworzenie zasobów za pomocą hello procesu przekazywania. toouse podejście ingesting zbiorczego tworzenie manifestu (IngestManifest) dotyczące zasobów hello i skojarzone z nią pliki. Następnie należy użyć metody przekazywania hello kontenera obiektów blob z wybranym tooupload hello skojarzone pliki toohello manifestu. Microsoft Azure Media Services Obserwujący kontenera obiektów blob hello skojarzonego z hello manifestu. Gdy plik jest przekazany toohello kontenera obiektów blob, Microsoft Azure Media Services kończy tworzenie zasobów hello na podstawie konfiguracji hello hello zasobów w manifeście hello (IngestManifestAsset).

toocreate nowe IngestManifest wywołać metodę tworzenia hello udostępnianych przez hello kolekcji IngestManifests na powitania CloudMediaContext. Ta metoda spowoduje utworzenie nowej IngestManifest z hello manifestu o podanej nazwie.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Utwórz hello zasobów, które będą skojarzone z zbiorczego hello IngestManifest. Skonfiguruj opcje szyfrowania hello żądanego na powitania zasobów służy do wprowadzania zbiorczego.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

IngestManifestAsset kojarzy zasób z zbiorczego IngestManifest służy do wprowadzania zbiorczego. Powoduje również skojarzenie hello AssetFiles tworzącej każdego zasobu. toocreate IngestManifestAsset, użyj metody tworzenia hello hello kontekstu serwera.

Witaj poniższym przykładzie pokazano dodawania dwóch IngestManifestAssets nowe kojarzące hello zasoby dwóch wcześniej utworzony zbiorczego toohello pozyskiwania manifestu. Każdy IngestManifestAsset powoduje również skojarzenie zestaw plików, które zostaną przekazane za każdy zasób podczas wprowadzania zbiorczego.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Można użyć dowolnej aplikacji klienta szybkich możliwość przekazywania hello zasobów plików toohello kontenera magazynu obiektów blob identyfikatora URI podał hello **IIngestManifest.BlobStorageUriForUpload** właściwości hello IngestManifest. Co Usługa przekazywania zauważalne szybkich [Aspera na żądanie dla aplikacji Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). Można również napisać kod plików zasobów hello tooupload pokazane na powitania poniższy przykład kodu.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

Kod Hello przekazywania hello plików zasobów dla przykładu hello używane w tym temacie przedstawiono hello poniższy przykład kodu.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


Można określić postęp hello hello zbiorczego wprowadzania dla wszystkich zasobów skojarzonych z **IngestManifest** przez sondowanie właściwość statystyki hello hello **IngestManifest**. W kolejności informacje o postępie tooupdate, należy użyć nowego **CloudMediaContext** zawsze sondowania hello statystyki właściwości.

Witaj poniższym przykładzie pokazano sondowania IngestManifest przez jego **identyfikator**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Przekazywanie plików przy użyciu rozszerzenia zestawu .NET SDK
w poniższym przykładzie Hello pokazuje, jak tooupload w jednym pliku przy użyciu rozszerzenia zestawu .NET SDK. W takim przypadku hello **CreateFromFile** metoda jest używana, ale jest również dostępna wersja asynchroniczne hello (**CreateFromFileAsync**). Witaj **CreateFromFile** — metoda pozwala na określenie nazwy pliku hello, opcja szyfrowania i wywołanie zwrotne w kolejności tooreport hello postęp pliku hello przekazywania.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Witaj poniższy przykład wywołuje funkcję UploadFile i określa szyfrowanie magazynu jako opcję tworzenia zasobów hello.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Następne kroki

Teraz możesz zakodować przekazane elementy zawartości. Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).

Umożliwia także tootrigger usługi Azure Functions zadania kodowania, na podstawie pliku odbieranych w kontenerze hello skonfigurowane. Aby uzyskać więcej informacji, zobacz [ten przykład](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Następny krok
Teraz, gdy zostały przekazane zasób usługi tooMedia Przejdź toohello [jak tooGet procesor multimediów] [ How tooGet a Media Processor] tematu.

[How tooGet a Media Processor]: media-services-get-media-processor.md

