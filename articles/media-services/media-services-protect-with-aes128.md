---
title: "dynamiczne aaaUsing AES-128 szyfrowania i klucz usługi dostarczania | Dokumentacja firmy Microsoft"
description: "Microsoft Azure Media Services umożliwia toodeliver możesz zawartości zaszyfrowane za pomocą kluczy szyfrowania AES 128-bitowego. Usługa Media Services udostępnia również hello usługi dostarczania klucza, która dostarcza użytkownikom tooauthorized klucze szyfrowania. W tym temacie przedstawiono sposób toodynamically szyfrowania z AES-128 i korzystanie z usługi dostarczania klucza hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>Za pomocą dynamicznego szyfrowania AES-128 i usługi dostarczania klucza
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Omówienie
> [!NOTE]
> Zobacz [to](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) wideo omówienie sposobu tooprotect multimediów zawartości z szyfrowania AES.
> 
> 

Microsoft Azure Media Services umożliwia toodeliver Http-Live-Streaming (HLS) i płynnego przesyłania przesyłane zaszyfrowane z Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowe). Usługa Media Services udostępnia również hello usługi dostarczania klucza, która dostarcza użytkownikom tooauthorized klucze szyfrowania. Jeśli chcesz dla usługi Media Services tooencrypt zasób, muszą tooassociate klucz szyfrowania z zasobów hello i również skonfigurować zasady autoryzacji klucza hello. Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania zawartości przy użyciu szyfrowania AES. toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello. toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.

Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w hello [proste tokenów sieci Web](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formatu (SWT) i [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formatu (JWT). Aby uzyskać więcej informacji, zobacz [Skonfiguruj zasady autoryzacji klucza zawartości hello](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake korzystać z szyfrowania dynamicznego, należy toohave element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów. Należy również zasady dostarczania hello tooconfigure dla elementu hello zawartości (opisane w dalszej części tego tematu). Następnie na podstawie hello formatu określonego w hello URL przesyłania strumieniowego, serwer przesyłania strumieniowego na żądanie hello będzie upewnij się, że strumieniu hello jest dostarczany w protokole hello, wybrana. W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.

Ten temat powinien być przydatny toodevelopers, że działają w przypadku aplikacji dostarczanie multimediów chronionych. Witaj temacie pokazano, jak tooconfigure hello usługi dostarczania klucza przy użyciu zasad autoryzacji, aby tylko autoryzowani klienci mogli odbierać hello kluczy szyfrowania. Zawiera także sposób toouse szyfrowania dynamicznego.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>Przepływ pracy usługi dostarczania klucza i dynamicznego szyfrowania AES-128

Witaj poniżej przedstawiono ogólne kroki, że będzie potrzebny tooperform podczas szyfrowania zasobów z użyciem standardu AES, za pomocą usługi dostawy klucza usługi Media Services hello, a także korzystanie z szyfrowania dynamicznego.

1. [Utworzenie elementu zawartości i przekazywanie plików do zawartości hello](media-services-protect-with-aes128.md#create_asset).
2. [Kodowanie zawartości hello zawierającego hello pliku toohello o adaptacyjnej szybkości bitowej MP4 zestawu](media-services-protect-with-aes128.md#encode_asset).
3. [Utwórz klucz zawartości i powiązać ją z zasobów hello zakodowane](media-services-protect-with-aes128.md#create_contentkey). W usłudze Media Services klucz zawartości hello zawiera klucz szyfrowania hello zasobów.
4. [Skonfiguruj zasady autoryzacji klucza zawartości hello](media-services-protect-with-aes128.md#configure_key_auth_policy). zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta hello w kolejności hello zawartości toobe klucza dostarczonego toohello klienta.
5. [Skonfiguruj zasady dostarczania hello zasobu](media-services-protect-with-aes128.md#configure_asset_delivery_policy). Konfiguracja zasady dostarczania Hello obejmuje: kluczy adres URL pozyskiwania i wektor inicjowania (IV) (AES 128 wymaga hello tego samego toobe IV podane podczas szyfrowania i odszyfrowywania), protokół dostarczania (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie), hello typu szyfrowania dynamicznego (na przykład, koperty lub nie szyfrowania dynamicznego).

    Protokół tooeach różnych zasad można zastosować na powitania elementu zawartości. Na przykład można zastosować szyfrowanie PlayReady tooSmooth/DASH i tooHLS szyfrowanie AES Envelope. Wszystkie protokoły, które nie są zdefiniowane w zasadzie dostarczania (na przykład dodać jedną zasadę, która tylko określa hello protokół HLS), zostanie zablokowany przesyłania strumieniowego. toothis wyjątek Hello jest, jeśli masz nie zdefiniowano zasad dostarczania elementów zawartości. Następnie wszystkie protokoły mogą być przesyłane hello Wyczyść.

6. [Utwórz Lokalizator OnDemand](media-services-protect-with-aes128.md#create_locator) w celu tooget adresu URL przesyłania strumieniowego.

przedstawiono również temat Hello [jak aplikacji klienckiej mogą żądać klucza z usługi dostarczania klucza hello](media-services-protect-with-aes128.md#client_request).

Dostępne są kompletne .NET [przykład](media-services-protect-with-aes128.md#example) na końcu hello hello tematu.

powitania po obraz pokazuje opisany wyżej przepływ pracy hello. W tym miejscu hello token jest używany do uwierzytelniania.

![Ochrona z zastosowaniem standardu AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

Witaj pozostałej części tego tematu zawiera szczegółowe wyjaśnienia, przykłady kodu i tootopics łącza, które pokazują, jak tooachieve hello zadania opisane powyżej.

## <a name="current-limitations"></a>Bieżące ograniczenia
W przypadku dodania lub zaktualizowania zasad dostarczania elementów zawartości należy usunąć skojarzony lokalizator (jeśli istnieje) i utworzyć nowy.

## <a id="create_asset"></a>Utworzenie elementu zawartości i przekazywanie plików do zawartości hello
W kolejności toomanage, kodowania i przesyłania strumieniowego filmów, należy najpierw przekazać zawartość do usługi Microsoft Azure Media Services. Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego. 

Aby uzyskać szczegółowe informacje, zobacz artykuł [Upload Files into a Media Services account](media-services-dotnet-upload-files.md) (Przekazywanie plików na konto usługi Media Services).

## <a id="encode_asset"></a>Kodowanie hello zasobu zawierającego hello pliku toohello adaptacyjną szybkością transmisji bitów zestaw MP4
W przypadku szyfrowania dynamicznego wystarczy jest toocreate element zawartości zawierający zestaw plików MP4 wielokrotnej szybkości transmisji bitów lub pliki źródłowe Smooth Streaming wielokrotnej szybkości transmisji bitów. Następnie na podstawie hello formatu określonego w manifeście hello lub fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana. W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta. Aby uzyskać więcej informacji, zobacz hello [omówienie tworzenia pakietów dynamicznych](media-services-dynamic-packaging-overview.md) tematu.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 
>
>Ponadto toobe toouse stanie dynamicznego tworzenia pakietów i dynamicznego szyfrowania zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.

Aby uzyskać instrukcje dotyczące tooencode, zobacz [jak tooencode zasobów przy użyciu standardu Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Utwórz klucz zawartości i powiązać ją z hello zakodowane zasobów
W usłudze Media Services klucz zawartości hello zawiera klucz hello, które mają tooencrypt zasób z.

Aby uzyskać szczegółowe informacje, zobacz artykuł [Create content key](media-services-dotnet-create-contentkey.md) (Tworzenie klucza zawartości).

## <a id="configure_key_auth_policy"></a>Skonfiguruj zasady autoryzacji klucza zawartości hello
Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza. zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełniać powitania klienta (odtwarzacz), aby hello toobe klucza dostarczyć toohello klienta. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: Otwórz, token ograniczenia lub ograniczenia adresów IP.

Aby uzyskać więcej informacji, zobacz artykuł [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md) (Konfigurowanie zasad autoryzacji klucza zawartości).

## <a id="configure_asset_delivery_policy"></a>Konfigurowanie zasad dostarczania elementów zawartości
Skonfiguruj zasady dostarczania powitania dla zawartości. Obejmuje kilka rzeczy, które hello Konfiguracja zasady dostarczania zasobów:

* adres URL pozyskiwania klucza Hello. 
* Witaj toouse wektor inicjowania (IV) hello koperty szyfrowania. AES 128 wymaga hello tego samego toobe IV podane podczas szyfrowania i odszyfrowywania. 
* Witaj Protokół dostarczania elementów zawartości (na przykład MPEG DASH, HLS, Smooth Streaming lub wszystkie).
* Witaj typ szyfrowania dynamicznego (na przykład szyfrowanie AES envelope) lub nie szyfrowania dynamicznego. 

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

## <a id="client_request"></a>Jak klient Zażądaj klucza z usługi dostarczania klucza hello
W poprzednim kroku hello należy konstruować hello adres URL, który wskazuje plik manifestu tooa. Klient musi tooextract hello niezbędne informacje z hello przesyłanie strumieniowe plików manifestu w kolejności toomake usługi klucza dostawy toohello żądania.

### <a name="manifest-files"></a>Pliki manifestu
powitania klienta wymaga adresu URL hello tooextract (zawierającej również identyfikator (Kącik) klucz zawartości) wartość z zakresu od hello pliku manifestu. powitania klienta spróbuj klucza szyfrowania hello tooget z usługi dostarczania klucza hello. Witaj klienta musi też mieć wartość hello IV tooextract i użyj odszyfrować stream.hello powitania po fragment kodu przedstawia hello <Protection> element hello Smooth Streaming manifestu.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

W przypadku hello HLS hello głównego manifestu jest dzielony na pliki segmentu. 

Na przykład jest hello głównego manifestu: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) zawierający listę nazw plików segmentu.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Jeśli jeden z plików segmentu hello Otwórz w edytorze tekstu (na przykład http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should zawiera #EXT-X-klucza, który wskazuje, że ten plik hello jest zaszyfrowany.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Jeśli planujesz tooplay AES szyfrowane HLS w programie Safari, zobacz [ten blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Żądaj hello klucza z usługi dostarczania klucza hello

Witaj poniższy kod przedstawia sposób toosend toohello żądania usługi Media Services klucz usługi dostarczania przy użyciu klucza dostawy identyfikatora Uri (który został wyodrębniony z manifestu hello) i tokenu (w tym temacie nie opisano sposobu tooget prostego tokeny zabezpieczenia usługi tokenu).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>Ochrona zawartości przy użyciu standardu AES-128 przy użyciu platformy .NET

### <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 
2. Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Przykład

Zastąp hello kodu w pliku Program.cs kodem hello przedstawionym w tej sekcji.
 
>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

Upewnij się, że zmienne tooupdate toopoint toofolders gdzie znajdują się pliki danych wejściowych.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

