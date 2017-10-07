---
title: "wprowadzenie do dostarczania zawartości na żądanie przy użyciu platformy .NET aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello wdrażania aplikacji dostarczania zawartości na żądanie usłudze Azure Media Services przy użyciu platformy .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Wprowadzenie do dostarczania zawartości na żądanie przy użyciu zestawu .NET SDK
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu zestawu .NET SDK usługi Azure Media Services hello hello.

## <a name="prerequisites"></a>Wymagania wstępne

Samouczek hello toocomplete wymagane są następujące Hello:

* Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Konto usługi Media Services. Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).
* .NET Framework 4.0 lub nowszy.
* Program Visual Studio.

W tym samouczku opisano hello następujące zadania:

1. Początek (przy użyciu portalu Azure hello) punktu końcowego przesyłania strumieniowego.
2. Tworzenie i konfigurowanie projektu programu Visual Studio.
3. Połącz toohello konta usługi Media Services.
2. Ładowanie pliku wideo.
3. Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.
4. Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresów URL.  
5. Odtwarzanie zawartości.

## <a name="overview"></a>Omówienie
Ten samouczek przedstawia kroki hello wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu usługi Azure Media Services (AMS) zestawu SDK dla platformy .NET.

Samouczek Hello wprowadza hello podstawowy przepływ pracy usług Media Services i hello najczęściej obiekty i zadania programowania wymagane do tworzenia usługi Media Services. Po ukończeniu hello samouczka hello będzie toostream może być lub pobrać progresywnie przykładowy plik nośnika, który przekazany, zakodowany i pobierane.

### <a name="ams-model"></a>Model AMS

Witaj poniższej ilustracji przedstawiono niektóre obiekty hello najczęściej używane podczas tworzenia aplikacji VoD hello Media Services OData modelu.

Kliknij przycisk tooview obraz powitania pełny jego rozmiar.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Możesz wyświetlić hello całego modelu [tutaj](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Uruchom przy użyciu portalu Azure hello punkty końcowe przesyłania strumieniowego

Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów. Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.

toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:

1. Zaloguj się w hello [portalu Azure](https://portal.azure.com/).
2. W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego.
3. Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego.

    zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.

4. Kliknij ikonę Start hello.
5. Kliknij przycisk toosave przycisk Zapisz hello zmiany.

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 
2. Utwórz nowy folder (folder może być dowolnym miejscu na dysku lokalnym) i skopiuj plik plik MP4 tooencode i strumienia, lub pobrać progresywnie. W tym przykładzie ścieżki "C:\VideoFiles" hello jest używany.

## <a name="connect-toohello-media-services-account"></a>Połącz toohello konta usługi Media Services

Korzystając z usługi Media Services z platformą .NET, należy użyć hello **CloudMediaContext** klasy dla większości zadań programowania Media Services: Łączenie konta usług tooMedia; tworzenia, aktualizowania, uzyskiwanie dostępu do i usuwanie następujących hello obiekty: zasoby, pliki zasobów, zadań, zasad dostępu, lokalizatorów itp.

Zastąp domyślną klasę Program hello hello następującego kodu. Witaj kod pokazuje, jak połączenia hello tooread wartości z pliku App.config hello i jak toocreate hello **CloudMediaContext** obiektu w kolejności tooconnect tooMedia usług. Aby uzyskać więcej informacji, zobacz [łączenie toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).

Upewnij się, że tooupdate hello pliku nazwa i ścieżka toowhere posiadanego pliku nośnika.

Witaj **Main** funkcja wywołuje metody, które będą zdefiniowane dalszej części tej sekcji.

> [!NOTE]
> Możesz będą występować błędy kompilacji do momentu dodania definicje dla wszystkich funkcji hello.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Tworzenie nowego elementu zawartości i przekazywanie pliku wideo

Za pomocą usługi Media Services można przekazać (lub pozyskać) pliki cyfrowe do elementu zawartości. Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżki i napisów plików (i hello metadane dotyczące tych plików.)  Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego. pliki Hello w hello zasobów są nazywane **plików zasobów**.

Witaj **UploadFile** określonych poniżej wywołania metody **CreateFromFile** (określone w rozszerzenia zestawu .NET SDK). **CreateFromFile** powoduje utworzenie nowego elementu zawartości, do których hello jest przekazywany określony plik źródłowy.

Witaj **CreateFromFile** ma metodę **AssetCreationOptions** które pozwalają określić jedną z hello następujące opcje tworzenia zasobów:

* **None** — szyfrowanie nie jest stosowane. Jest to wartość domyślna hello. Należy pamiętać, że w przypadku korzystania z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.
  Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.
* **StorageEncrypted** — Użyj tej opcji tooencrypt zawartości lokalnie, przy użyciu szyfrowania 256-bitowego szyfrowania AES (Advanced Standard), a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych z silne szyfrowanie przechowywanych na dysku.
* **CommonEncryptionProtected** — za pomocą tej opcji można przekazać zawartość, która jest już zaszyfrowana i chroniona za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (np. pliki Smooth Streaming chronione za pomocą technologii PlayReady DRM).
* **EnvelopeEncryptionProtected** — ta opcja umożliwia przekazanie plików w formacie HLS zaszyfrowanych z użyciem standardu AES. Należy pamiętać, że pliki hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.

Witaj **CreateFromFile** metoda pozwala także określić wywołanie zwrotne w kolejności tooreport hello postępu przekazywania pliku hello.

Poniższy przykład hello, możemy określić **Brak** hello opcji zasobów.

Dodaj hello następujące metody toohello Program klasy.

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów
Po pozyskaniu elementów zawartości do usługi Media Services, nośnik, mogą zostać zakodowane, poddane transmultipleksacji, oznaczone znakiem wodnym i tak dalej, przed przekazaniem tooclients. Te działania są zaplanowane i uruchomienia wielu tła roli wystąpień tooensure wysokiej wydajności i dostępności. Te działania są nazywane zadaniami, a każde zadanie składa się z niepodzielnych zadań, które hello rzeczywistą pracę w pliku trwałego hello.

Jak wspomniano wcześniej, podczas pracy z usługą Azure Media Services, jest jednym z najbardziej typowych scenariuszy hello dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów. Usługi Media Services można dynamicznie pakietu do jednego z następujących formatów hello zestaw plików MP4 z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH.

tootake korzyści z dynamicznego tworzenia pakietów, potrzebujesz tooencode lub transkoduj plik (źródłowy) mezzanine do zestawu plików MP4 lub Smooth Streaming plików.  

Witaj następującego kodu pokazuje, jak zadania toosubmit kodowania. Witaj zadanie zawiera jedno zadanie, które określa plik mezzanine hello tootranscode do zestawu z adaptacyjną szybkością transmisji bitów MP4s przy użyciu **Media Encoder Standard**. Hello kod przesyła zadanie hello i czeka, dopóki zostanie zakończona.

Po zakończeniu zadania hello może być możliwe toostream zawartości lub pobrać progresywnie pliki MP4, które zostały utworzone w wyniku transkodowania.

Dodaj hello następujące metody toohello Program klasy.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Publikowanie hello zawartości i uzyskiwanie adresów URL do przesyłania strumieniowego i pobierania progresywnego

toostream lub pobierania zawartości, należy najpierw należy zbyt opublikować, przez utworzenie lokalizatora. Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów. Usługa Media Services obsługuje dwa typy lokalizatorów: OnDemandOrigin lokalizatory nośniki używane toostream (na przykład MPEG DASH, HLS lub Smooth Streaming) i lokalizatorów podpis dostępu (SAS) używane pliki multimedialne toodownload (Aby uzyskać więcej informacji o lokalizatory sygnatury dostępu Współdzielonego, zobacz [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu).

### <a name="some-details-about-url-formats"></a>Informacje na temat formatów adresów URL

Po utworzeniu lokalizatorów hello można tworzyć adresy URL hello, które może być używane toostream lub pobierania plików. Przykładowe Hello w tym samouczku dane wyjściowe obejmują adresów URL, które można wkleić w odpowiednich przeglądarkach. W tej sekcji przedstawiono jedynie krótkie przykłady różnych formatów.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Adres URL przesyłania strumieniowego MPEG DASH ma hello następującego formatu:

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Adres URL dla protokołu HLS ma hello następującego formatu:

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Adres URL dla protokołu Smooth Streaming ma hello następującego formatu:

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Pliki toodownload adres URL SAS używany ma hello następującego formatu:

{nazwa kontenera obiektów blob}/{nazwa elementu zawartości}/{nazwa pliku}/{sygnatura dostępu współdzielonego}

Rozszerzenia .NET SDK usługi Media Services zapewniają wygodne metody pomocnicze czy powrotu sformatowane adresy URL dla hello opublikowanych zasobów.

Hello poniższym kodzie użyto rozszerzeń zestawu .NET SDK toocreate lokalizatory i tooget przesyłania strumieniowego i pobierania progresywnego adresów URL. Kod Hello przedstawiono również sposób tooa lokalny folder plików toodownload.

Dodaj hello następujące metody toohello Program klasy.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Testowanie przez odtwarzanie zawartości

Po uruchomieniu program hello zdefiniowane w poprzedniej sekcji hello hello podobne następujące toohello będą wyświetlane w oknie konsoli hello adresów URL.

Adresy URL przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

Adresy URL pobierania progresywnego (audio i wideo):

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream wideo, wklej adres URL w polu tekstowym adres URL hello w hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progresywnego pobierania, wklej adres URL do przeglądarki (na przykład program Internet Explorer, Chrome lub Safari).

Aby uzyskać więcej informacji zobacz następujące tematy hello:

- [Odtwarzanie zawartości w istniejących odtwarzaczach](media-services-playback-content-with-existing-players.md)
- [Opracowywanie aplikacji odtwarzacza wideo](media-services-develop-video-players.md)
- [Osadzanie plików wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z implementacją DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Pobieranie przykładu
Witaj Poniższy przykładowy kod zawiera hello kod, który został utworzony w tym samouczku: [próbki](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
