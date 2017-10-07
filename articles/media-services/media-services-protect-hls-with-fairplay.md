---
title: "aaaProtect HLS zawartości z Microsoft PlayReady lub Apple FairPlay - Azure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i pokazuje, jak toodynamically usługi Azure Media Services toouse szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu FairPlay firmy Apple. Pokazuje też, jak hello toouse Media Services licencji toodeliver usługi dostarczania tooclients licencje FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Ochrona programu HLS zawartości z FairPlay firmy Apple lub Microsoft PlayReady
Azure Media Services umożliwia toodynamically można zaszyfrować zawartość HTTP Live Streaming (HLS) przy użyciu hello następujących formatów:  

* **Koperty AES-128, klucz niezaszyfrowany**

    Hello całego fragmentów są szyfrowane przy użyciu hello **CBC AES-128** tryb. odszyfrowywanie Hello strumienia hello jest obsługiwany natywnie przez systemów iOS i OS X player. Aby uzyskać więcej informacji, zobacz [dynamicznego szyfrowania przy użyciu standardu AES-128 i usługi dostarczania klucza](media-services-protect-with-aes128.md).
* **FairPlay firmy Apple**

    Witaj poszczególnych wideo i audio próbki są szyfrowane przy użyciu hello **CBC AES-128** tryb. **Przesyłanie strumieniowe FairPlay** (kl. / s) jest zintegrowany z systemów operacyjnych urządzeń hello, macierzystą obsługę w systemach iOS i Apple TV. Przeglądarka Safari w OS X umożliwia klatek na Sekundę przy użyciu Obsługa interfejsu hello szyfrowane nośnika rozszerzenia (EME).
* **Microsoft PlayReady**

Witaj poniższy obraz przedstawia hello **HLS + FairPlay lub PlayReady szyfrowania dynamicznego** przepływu pracy.

![Diagram przepływu pracy szyfrowania dynamicznego](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

W tym temacie przedstawiono, jak toodynamically Media Services toouse zaszyfrować HLS zawartości przy użyciu FairPlay firmy Apple. Pokazuje też, jak hello toouse Media Services licencji toodeliver usługi dostarczania tooclients licencje FairPlay.

> [!NOTE]
> Chcąc również tooencrypt Twojego HLS zawartości za pomocą PlayReady, należy toocreate wspólny klucz zawartości i skojarzyć go z zawartości. Należy również tooconfigure hello zawartości zasady autoryzacji klucza, zgodnie z opisem w [za pomocą PlayReady, dynamicznego szyfrowania common encryption](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Wymagania i uwagi

następujące Hello są wymagane, gdy przy użyciu toodeliver Media Services, który HLS zaszyfrowanych z FairPlay i licencje FairPlay toodeliver:

  * Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Konto usługi Media Services. Zobacz toocreate, [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).
  * Logowanie się przy [Program firmy Apple Development](https://developer.apple.com/).
  * Firma Apple wymaga hello właściciela zawartości tooobtain hello [pakietu wdrożeniowego](https://developer.apple.com/contact/fps/). Stan już zaimplementowany klucza modułu zabezpieczeń (KSM) z usługi Media Services, a następnie żądają hello pakiet klatek na Sekundę. Istnieją instrukcje hello końcowego kl. / s pakietu toogenerate certyfikacji i uzyskiwanie hello klucz tajny aplikacji (poproś). Możesz użyć poproś tooconfigure FairPlay.
  * Wersja Azure .NET SDK usługi Media Services **3.6.0** lub nowszym.

po stronie klucza dostawy Media Services musi być ustawione hello następujące czynności:

  * **Aplikacja certyfikatu (AC)**: jest to plik PFX zawierający klucz prywatny hello. Utwórz ten plik i szyfrowania za pomocą hasła.

       Po skonfigurowaniu zasad klucza dostawy, należy podać ten plik PFX hasło i hello w formacie Base64.

      Witaj następujące kroki opisano, jak plik FairPlay toogenerate certyfikatu PFX:

    1. Zainstaluj biblioteki OpenSSL z https://slproweb.com/products/Win32OpenSSL.html.

        Przejdź toohello folder zawierający certyfikat FairPlay hello i inne pliki dostarczane przez firmę Apple.
    2. Uruchom następujące polecenie z wiersza polecenia hello hello. Konwertuje to plik PEM tooa pliku .cer hello.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509-informuje der — w fairplay.cer-out fairplay out.pem
    3. Uruchom następujące polecenie z wiersza polecenia hello hello. Plik PFX tooa pliku PEM hello to konwertuje hello kluczem prywatnym. następnie o Hello hasło pliku PFX hello biblioteki OpenSSL.

        Pkcs12 "C:\OpenSSL-Win32\bin\openssl.exe"-Eksportowanie — limit fairplay out.pfx-inkey privatekey.pem — w file:privatekey-pem-pass.txt - passin fairplay out.pem
  * **Hasło certyfikatu aplikacji**: hello hasło do utworzenia pliku PFX hello.
  * **Identyfikator hasła aplikacji Cert**: musisz przekazać hello hasła, podobne toohow one przekazać kluczy usługi Media Services. Użyj hello **ContentKeyType.FairPlayPfxPassword** hello tooget wartość enum nośnika identyfikatora usługi. Jest to, co potrzebne toouse wewnątrz opcji zasad hello klucza dostawy.
  * **IV**: jest to wartość losowe 16 bajtów. Musi on być zgodny hello iv w zasad dostarczania elementów zawartości hello. Możesz wygenerować hello iv i umieszcza je w obu miejscach: zasady dostarczania elementu zawartości hello i opcji zasad hello klucza dostawy.
  * **Poproś**: podczas generowania hello certyfikacji za pomocą portalu dla deweloperów firmy Apple hello otrzymania tego klucza. Każdy zespół deweloperów otrzyma unikatowy poproś. Zapisz kopię hello poproś i przechowuj go w bezpiecznym miejscu. Konieczne będzie tooconfigure poproś jako FairPlayAsk tooMedia usługi później.
  * **Poproś identyfikator**: ten identyfikator jest uzyskiwany podczas przekazywania poproś do usługi Media Services. Należy przekazać poproś przy użyciu hello **ContentKeyType.FairPlayAsk** wartości wyliczenia. W wyniku hello hello Media Services ID jest zwracany, co jest przeznaczenia, ustawiając opcję zasad klucza dostawy hello.

Witaj następujących czynności należy ustawić hello kl. / s po stronie klienta:

  * **Aplikacja certyfikatu (AC)**: jest to plik.cer/.der, który zawiera klucz publiczny hello, korzysta z systemu operacyjnego hello tooencrypt niektórych ładunku. Usługi Media Services musi tooknow informacji na ten temat, ponieważ jest to wymagane przez odtwarzacz hello. usługi dostarczania klucza Hello odszyfrowuje ją przy użyciu odpowiedniego klucza prywatnego hello.

tooplay kopii FairPlay strumienia zaszyfrowane, uzyskać pierwszy rzeczywistych poproś i następnie wygenerować rzeczywistych certyfikatu. Ten proces tworzy wszystkich trzech części:

  * pliku der
  * plik PFX
  * hasło dla pliku PFX hello

Witaj następujący klienci obsługuje HLS z **CBC AES-128** szyfrowania: Safari w systemie iOS Apple TV, OS X.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Konfigurowanie FairPlay dynamicznego szyfrowania i licencji dostarczania usług
Witaj poniżej przedstawiono ogólne kroki do ochrony zasobów z FairPlay przy użyciu usługi dostarczania licencji Media Services hello, a także za pomocą szyfrowania dynamicznego.

1. Utworzenie elementu zawartości i przekazywanie plików do zawartości hello.
2. Kodowanie zawartości hello, który zawiera hello pliku toohello o adaptacyjnej szybkości bitowej MP4 ustawiona.
3. Utwórz klucz zawartości i skojarzyć go z zasobów hello zakodowany.  
4. Skonfiguruj zasady autoryzacji klucza zawartości hello. Określ następujące hello:

   * Metoda dostarczania Hello (w tym przypadku FairPlay).
   * FairPlay konfiguracji opcje zasad. Aby uzyskać więcej informacji na temat tooconfigure FairPlay, zobacz hello **ConfigureFairPlayPolicyOptions()** w poniższym przykładzie hello metody.

     > [!NOTE]
     > Zwykle czy chcesz tooconfigure zasad FairPlay opcje tylko raz, ponieważ będzie mieć tylko jeden zestaw certyfikacji i poproś.
     >
     >
   * Ograniczenia (otwarte lub tokenu).
   * Informacje typu klucza dostawy określonych toohello, który definiuje sposób dostawy klucza powitania klienta toohello.
5. Skonfiguruj zasady dostarczania elementu zawartości hello. Konfiguracja zasady dostarczania Hello obejmuje:

   * Protokół dostarczania Hello (HLS).
   * Witaj typ szyfrowania dynamicznego (typowe szyfrowanie CBC).
   * adres URL pozyskiwania licencji Hello.

     > [!NOTE]
     > Jeśli chcesz toodeliver strumienia, który jest szyfrowana za FairPlay i innego systemu zarządzania prawami cyfrowymi (DRM), masz zasady dostarczania oddzielnych tooconfigure:
     >
     > * Jeden tooconfigure IAssetDeliveryPolicy dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH) z wspólnego szyfrowania (CENC) (PlayReady i Widevine) i Smooth za pomocą PlayReady
     > * Inny tooconfigure IAssetDeliveryPolicy FairPlay dla protokołu HLS
     >
     >
6. Utwórz tooget lokalizatora OnDemand adresu URL przesyłania strumieniowego.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Aby użyć klucza dostawy FairPlay aplikacji odtwarzacza
Aplikacji odtwarzacza można programować za pomocą hello iOS SDK. toobe stanie tooplay FairPlay zawartości, masz tooimplement hello licencji exchange protokołu. Ten protokół nie jest określony przez firmę Apple. Jest zapasowej aplikacji tooeach sposób dostawy klucza toosend żądań. Hello Media Services FairPlay klucza dostawy usług oczekuje hello SPC toocome jako www-form-url post zakodowany komunikat w hello następującej postaci:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player nie obsługuje odtwarzania FairPlay fabrycznej hello. odtwarzanie FairPlay tooget w systemie MAC OS X, uzyskać player próbki hello hello konta dewelopera firmy Apple.
>
>

## <a name="streaming-urls"></a>Adresy URL przesyłania strumieniowego
Jeśli zawartości została zaszyfrowana z więcej niż jeden DRM, należy użyć tag szyfrowania w hello URL przesyłania strumieniowego: (format = "m3u8-aapl, szyfrowanie = 'xxx').

Zastosuj Hello następujące zagadnienia:

* Można określić tylko zero lub jeden typ szyfrowania.
* Typ szyfrowania Hello nie ma toobe określona w adresie URL hello, jeśli tylko jeden szyfrowania został zastosowany toohello zasobów.
* Typ szyfrowania Hello jest uwzględniana wielkość liter.
* można określić Hello następujące typy szyfrowania:  
  * **cenc**: szyfrowania Common encryption (PlayReady lub Widevine)
  * **cbcs-aapl**: FairPlay
  * **CBC**: szyfrowanie AES envelope

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 
2. Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Przykład

Hello następujące przykładowe pokazuje hello możliwości toouse toodeliver Media Services zaszyfrowane za pomocą FairPlay zawartości. Ta funkcja została wprowadzona w hello Azure Media Services SDK dla platformy .NET w wersji 3.6.0. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
