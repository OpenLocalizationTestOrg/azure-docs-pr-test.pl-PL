---
title: aaaUsing PlayReady i Widevine dynamicznego szyfrowania common encryption | Dokumentacja firmy Microsoft
description: "Microsoft Azure Media Services umożliwia możesz toodeliver MPEG-DASH, Smooth Streaming i Http-Live-Streaming (HLS) strumieni chronionych z Microsoft PlayReady DRM. Można również toodelivery strumienia DASH szyfrowanego przy Widevine DRM. W tym temacie przedstawiono sposób toodynamically szyfrowanie PlayReady i Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Używanie dynamicznego szyfrowania Common Encryption w usługach PlayReady i Widevine

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Microsoft Azure Media Services umożliwia toodeliver MPEG-DASH, Smooth Streaming i strumieni HTTP-Live-Streaming (HLS) chronionych przy [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Można również toodeliver zaszyfrowanych strumienie DASH korzystających z licencji Widevine DRM. Zarówno PlayReady i Widevine są szyfrowane na powitania specyfikacją Common Encryption (ISO/IEC CENC 23001-7). Można użyć [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (począwszy od wersji hello 3.5.1) lub REST API tooconfigure Twojego toouse AssetDeliveryConfiguration Widevine.

Usługa Media Services udostępnia usługę dostarczania licencji PlayReady i Widevine DRM. Media Services dostarcza również interfejsy API, które umożliwiają skonfigurowanie hello prawa i ograniczenia, które mają hello PlayReady lub Widevine DRM środowiska uruchomieniowego tooenforce, gdy użytkownik odtwarza chronioną zawartość. Gdy użytkownik zażąda zawartości chronione DRM, hello aplikacja odtwarzacza zażąda licencji z hello AMS licencji usługi. Usługa licencjonowania AMS Hello będzie wystawiać player toohello licencji, jeśli jest on autoryzowany. Licencja PlayReady lub Widevine zawiera klucz odszyfrowujący hello używanego przez powitania klienta player toodecrypt i strumienia hello zawartości.

Można również użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Aby uzyskać więcej informacji, zobacz: integracja z [Axinom](media-services-axinom-integration.md) i [castLabs](media-services-castlabs-integration.md).

Usługa Media Services obsługuje wiele sposobów autoryzacji użytkowników, którzy tworzą żądania klucza. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w hello [proste tokenów sieci Web](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formatu (SWT) i [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formatu (JWT). Aby uzyskać więcej informacji zobacz Konfigurowanie hello zawartości zasady autoryzacji klucza.

tootake korzystać z szyfrowania dynamicznego, należy toohave element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów. Należy również zasady dostarczania hello tooconfigure dla elementu hello zawartości (opisane w dalszej części tego tematu). Następnie na podstawie hello formatu określonego w hello URL przesyłania strumieniowego, serwer przesyłania strumieniowego na żądanie hello będzie upewnij się, że strumieniu hello jest dostarczany w protokole hello, wybrana. W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź HTTP hello, na podstawie żądań klienta.

Ten temat powinien być przydatny toodevelopers, które działają w przypadku aplikacji, które dostarczają zawartość chronioną przy użyciu wielu protokołów DRM, takich jak PlayReady i Widevine. Witaj temacie pokazano, jak tooconfigure hello usługi dostarczania licencji PlayReady przy użyciu zasad autoryzacji, tak aby tylko autoryzowani klienci mogli odbierać licencje PlayReady lub Widevine. Zawiera także sposób toouse szyfrowania PlayReady lub Widevine DRM strumienia DASH.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

## <a name="download-sample"></a>Pobieranie przykładu
Możesz pobrać przykładowy hello opisane w tym artykule [tutaj](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Konfigurowanie dynamicznego szyfrowania Common Encryption i usług dostarczania licencji DRM

Witaj poniżej przedstawiono ogólne kroki, że będzie potrzebny tooperform podczas ochrony swoich elementów zawartości za pomocą PlayReady, za pomocą usługi dostarczania licencji Media Services hello, a także za pomocą szyfrowania dynamicznego.

1. Utworzenie elementu zawartości i przekazywanie plików do zawartości hello.
2. Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4.
3. Utwórz klucz zawartości i skojarz go z algorytmem hello zawartości. W usłudze Media Services klucz zawartości hello zawiera klucz szyfrowania hello zasobów.
4. Skonfiguruj zasady autoryzacji klucza zawartości hello. zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta hello w kolejności hello zawartości toobe klucza dostarczonego toohello klienta.

    Podczas tworzenia zasady autoryzacji klucza zawartości hello, potrzebujesz następujących hello toospecify: dostarczania — metoda (PlayReady lub Widevine), ograniczenia (otwarte lub tokenu) i typu klucza dostawy toohello określonych informacji, który definiuje sposób dostawy klucza hello Klient toohello ([PlayReady](media-services-playready-license-template-overview.md) lub [Widevine](media-services-widevine-license-template-overview.md) szablon licencji).

5. Skonfiguruj zasady dostarczania hello zasobu. Konfiguracja zasady dostarczania Hello obejmuje: Protokół dostarczania (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie), hello typ szyfrowania dynamicznego (na przykład Common Encryption) PlayReady lub Widevine adres URL pozyskiwania licencji.

    Protokół tooeach różnych zasad można zastosować na powitania elementu zawartości. Na przykład można zastosować szyfrowanie PlayReady tooSmooth/DASH i tooHLS szyfrowanie AES Envelope. Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego. toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości. Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.

6. Utwórz Lokalizator OnDemand w kolejności tooget adresu URL przesyłania strumieniowego.

Znajduje się pełny przykład .NET na końcu hello hello tematu.

powitania po obraz pokazuje opisany wyżej przepływ pracy hello. W tym miejscu hello token jest używany do uwierzytelniania.

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

Witaj pozostałej części tego tematu zawiera szczegółowe wyjaśnienia, przykłady kodu i tootopics łącza, które pokazują, jak tooachieve hello zadania opisane powyżej.

## <a name="current-limitations"></a>Bieżące ograniczenia
Jeśli w przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości, należy usunąć hello skojarzony Lokalizator (jeśli istnieje) i utworzyć nowy.

Ograniczenie w przypadku szyfrowania przy użyciu metody Widevine dla usługi Azure Media Services: obecnie nie jest obsługiwanych wiele kluczy zawartości.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Utworzenie elementu zawartości i przekazywanie plików do zawartości hello
W kolejności toomanage, kodowania i przesyłania strumieniowego filmów, należy najpierw przekazać zawartość do usługi Microsoft Azure Media Services. Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.

Aby uzyskać szczegółowe informacje, zobacz artykuł [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Przekazywanie plików na konto usługi Media Services).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4
W przypadku szyfrowania dynamicznego wystarczy jest toocreate element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów. Następnie na podstawie hello formatu określonego w manifeście hello fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana. W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta. Aby uzyskać więcej informacji, zobacz hello [omówienie tworzenia pakietów dynamicznych](media-services-dynamic-packaging-overview.md) tematu.

Aby uzyskać instrukcje dotyczące tooencode, zobacz [jak tooencode zasobów przy użyciu standardu Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Utwórz klucz zawartości i powiązać ją z hello zakodowane zasobów
W usłudze Media Services klucz zawartości hello zawiera klucz hello, które mają tooencrypt zasób z.

Aby uzyskać szczegółowe informacje, zobacz artykuł [Create content key](media-services-dotnet-create-contentkey.md) (Tworzenie klucza zawartości).

## <a id="configure_key_auth_policy"></a>Skonfiguruj zasady autoryzacji klucza zawartości hello
Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza. zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełniać powitania klienta (odtwarzacz), aby hello toobe klucza dostarczyć toohello klienta. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu.

Aby uzyskać więcej informacji, zobacz artykuł [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption) (Konfigurowanie zasad autoryzacji klucza zawartości).

## <a id="configure_asset_delivery_policy"></a>Konfigurowanie zasad dostarczania elementów zawartości
Skonfiguruj zasady dostarczania powitania dla zawartości. Obejmuje kilka rzeczy, które hello Konfiguracja zasady dostarczania zasobów:

* Witaj URL pozyskiwania licencji DRM.
* Witaj Protokół dostarczania elementów zawartości (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie).
* Witaj typ szyfrowania dynamicznego (w tym przypadku Common Encryption).

Aby uzyskać szczegółowe informacje, zobacz artykuł [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) (Konfigurowanie zasad dostarczania elementów zawartości).

## <a id="create_locator"></a>Utwórz Lokalizator OnDemand przesyłania strumieniowego w kolejności tooget adresu URL przesyłania strumieniowego
Konieczne będzie tooprovide użytkownika z hello przesyłania strumieniowego adres URL dla Smooth, DASH lub HLS.

> [!NOTE]
> W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.
>
>

Aby uzyskać instrukcje dotyczące sposobu toopublish zasobów i kompilacji adresu URL przesyłania strumieniowego, zobacz [zbudować adresu URL przesyłania strumieniowego](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Pobieranie tokenu testowego
Pobierz token testowy, oparte na powitania ograniczenia tokenu użytego do hello zasady autoryzacji klucza.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Można użyć hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest strumienia.

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 
2. Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Przykład

Witaj poniższym przykładzie pokazano funkcje wprowadzone w programie Azure Media Services SDK dla platformy .net — wersja 3.5.2 (w szczególności hello możliwości toodefine Widevine licencji szablonu i żądania licencji Widevine z usługi Azure Media Services).

Zastąp hello kodu w pliku Program.cs kodem hello przedstawionym w tej sekcji.

>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

Upewnij się, że zmienne tooupdate toopoint toofolders gdzie znajdują się pliki danych wejściowych.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Szyfrowanie CENC przy użyciu technologii Multi-DRM i kontroli dostępu](media-services-cenc-with-multidrm-access-control.md)

[Konfigurowanie tworzenia pakietów Widevine przy użyciu usługi AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Powiadomienie o usługach dostarczania licencji Google Widevine w usłudze Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
