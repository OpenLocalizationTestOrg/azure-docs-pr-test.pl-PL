---
title: "Ochrona zawartości z Microsoft PlayReady lub Apple FairPlay - Azure HLS | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i pokazuje, jak używać usługi Azure Media Services do dynamicznego szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu FairPlay firmy Apple. Ponadto sposobu korzystania z usługi dostarczania licencji Media Services dostarczać licencje FairPlay do klientów."
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Ochrona programu HLS zawartości z FairPlay firmy Apple lub Microsoft PlayReady
Usługa Azure Media Services umożliwia dynamicznego szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu następujących formatów:  

* **Koperty AES-128, klucz niezaszyfrowany**

    Cały fragmentów są szyfrowane przy użyciu **CBC AES-128** tryb. Odszyfrowywanie strumień jest obsługiwany natywnie przez systemów iOS i OS X player. Aby uzyskać więcej informacji, zobacz [dynamicznego szyfrowania przy użyciu standardu AES-128 i usługi dostarczania klucza](media-services-protect-with-aes128.md).
* **FairPlay firmy Apple**

    Poszczególne próbki audio i wideo są szyfrowane przy użyciu **CBC AES-128** tryb. **Przesyłanie strumieniowe FairPlay** (kl. / s) jest zintegrowany z systemów operacyjnych urządzeń macierzystą obsługę w systemach iOS i Apple TV. Przeglądarka Safari w OS X umożliwia klatek na Sekundę przy użyciu funkcji obsługi interfejsu szyfrowane nośnika rozszerzenia (EME).
* **Microsoft PlayReady**

Poniższy obraz przedstawia **HLS + FairPlay lub PlayReady szyfrowania dynamicznego** przepływu pracy.

![Diagram przepływu pracy szyfrowania dynamicznego](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

W tym temacie przedstawiono sposób korzystania z usługi Media Services do dynamicznego szyfrowania zawartości HLS przy użyciu FairPlay firmy Apple. Ponadto sposobu korzystania z usługi dostarczania licencji Media Services dostarczać licencje FairPlay do klientów.

> [!NOTE]
> Jeśli chcesz także do szyfrowania treści HLS za pomocą PlayReady, należy utworzyć wspólny klucz zawartości i powiązać ją z zawartości. Należy również skonfigurować zasady autoryzacji klucza zawartości, zgodnie z opisem w [za pomocą PlayReady, dynamicznego szyfrowania common encryption](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Wymagania i uwagi

Poniżej są wymagane w przypadku przy użyciu usługi Media Services, aby dostarczać HLS zaszyfrowanych z FairPlay i dostarczać licencje FairPlay:

  * Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Konto usługi Media Services. Aby go utworzyć, zobacz [utworzyć konto usługi Azure Media Services przy użyciu portalu Azure](media-services-portal-create-account.md).
  * Logowanie się przy [Program firmy Apple Development](https://developer.apple.com/).
  * Firma Apple wymaga właściciela zawartości uzyskać [pakietu wdrożeniowego](https://developer.apple.com/contact/fps/). Stan już zaimplementowany klucza modułu zabezpieczeń (KSM) z usługi Media Services, a następnie żądają końcowego pakietu kl. / s. Nie ma instrukcji w pakiecie końcowego kl. / s do generowania certyfikacji i uzyskać klucz tajny aplikacji (poproś). Poproś są używane do konfigurowania FairPlay.
  * Wersja Azure .NET SDK usługi Media Services **3.6.0** lub nowszym.

Po stronie klucza dostawy Media Services musi być ustawione następujące czynności:

  * **Aplikacja certyfikatu (AC)**: jest to plik PFX zawierający klucz prywatny. Utwórz ten plik i szyfrowania za pomocą hasła.

       Po skonfigurowaniu zasad klucza dostawy, musisz podać to hasło, a plik pfx w formacie Base64.

      W poniższych krokach opisano sposób generowania pliku certyfikatu PFX dla FairPlay:

    1. Zainstaluj biblioteki OpenSSL z https://slproweb.com/products/Win32OpenSSL.html.

        Przejdź do folderu, w których są certyfikatu FairPlay i inne pliki dostarczane przez firmę Apple.
    2. W wierszu polecenia uruchom następujące polecenie. Plik .cer to konwertuje plik PEM.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509-informuje der — w fairplay.cer-out fairplay out.pem
    3. W wierszu polecenia uruchom następujące polecenie. Plik PEM to konwertuje do pliku .pfx z kluczem prywatnym. Biblioteki OpenSSL następnie o hasło pliku pfx.

        Pkcs12 "C:\OpenSSL-Win32\bin\openssl.exe"-Eksportowanie — limit fairplay out.pfx-inkey privatekey.pem — w file:privatekey-pem-pass.txt - passin fairplay out.pem
  * **Hasło certyfikatu aplikacji**: hasło do utworzenia pliku .pfx.
  * **Identyfikator hasła aplikacji Cert**: musisz przekazać hasła, podobnie jak ich przekazać kluczy usługi Media Services. Użyj **ContentKeyType.FairPlayPfxPassword** wartości wyliczenia, aby uzyskać nazwę usługi multimediów. Jest to, muszą zostać użyty w opcji zasad klucza dostawy.
  * **IV**: jest to wartość losowe 16 bajtów. Musi on być zgodny z iv w zasad dostarczania elementów zawartości. Generowanie iv i umieszcza je w obu miejscach: zasady dostarczania elementu zawartości i opcji zasad klucza dostawy.
  * **Poproś**: ten klucz jest odebrane podczas generowania certyfikacji za pomocą portalu dla deweloperów firmy Apple. Każdy zespół deweloperów otrzyma unikatowy poproś. Zapisz kopię ZADAJ i przechowuj go w bezpiecznym miejscu. Należy skonfigurować poproś jako FairPlayAsk usługą Media Services.
  * **Poproś identyfikator**: ten identyfikator jest uzyskiwany podczas przekazywania poproś do usługi Media Services. Należy przekazać poproś przy użyciu **ContentKeyType.FairPlayAsk** wartości wyliczenia. W rezultacie identyfikator usług Media jest zwracane, a jest przeznaczenia, ustawiając opcję zasady dostarczania klucza.

Po stronie klienta kl. / s musi być ustawione następujące czynności:

  * **Aplikacja certyfikatu (AC)**: jest to plik.cer/.der, który zawiera klucz prywatny, który używa systemu operacyjnego do szyfrowania niektórych ładunku. Usługa Media Services musi wiedzieć o on, ponieważ jest to wymagane przez odtwarzacz. Usługi dostarczania klucza odszyfrowuje ją przy użyciu odpowiedniego klucza prywatnego.

Aby odtworzyć strumienia zaszyfrowanych FairPlay uzyskać rzeczywiste Poproś pierwszy, a następnie wygeneruj rzeczywistych certyfikatu. Ten proces tworzy wszystkich trzech części:

  * pliku der
  * plik PFX
  * hasło dla pliku pfx

Następujący klienci obsługuje HLS z **CBC AES-128** szyfrowania: Safari w systemie iOS Apple TV, OS X.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Konfigurowanie FairPlay dynamicznego szyfrowania i licencji dostarczania usług
Poniżej przedstawiono ogólne kroki do ochrony zasobów z FairPlay przy użyciu usługi dostarczania licencji Media Services, a także za pomocą szyfrowania dynamicznego.

1. Utworzenie elementu zawartości i przekazywanie plików do zawartości.
2. Kodowanie zawartości, który zawiera plik o adaptacyjnej szybkości bitowej MP4 ustawiona.
3. Utwórz klucz zawartości i skojarzyć go z zakodowanym elementem zawartości.  
4. Skonfiguruj zasady autoryzacji klucza zawartości. Określ następujące ustawienia:

   * Metoda dostarczania (w tym przypadku FairPlay).
   * FairPlay konfiguracji opcje zasad. Aby uzyskać więcej informacji na temat konfigurowania FairPlay, zobacz **ConfigureFairPlayPolicyOptions()** metody w poniższym przykładzie.

     > [!NOTE]
     > Zwykle czy chcesz skonfigurować opcje zasad FairPlay tylko raz, ponieważ będzie mieć tylko jeden zestaw certyfikacji i poproś.
     >
     >
   * Ograniczenia (otwarte lub tokenu).
   * Informacje specyficzne dla typu klucza dostawy, który definiuje sposób dostawy klucza do klienta.
5. Skonfiguruj zasady dostarczania elementu zawartości. Konfiguracja zasady dostarczania obejmuje:

   * Protokół dostarczania (HLS).
   * Typ szyfrowania dynamicznego (typowe szyfrowanie CBC).
   * Adres URL pozyskiwania licencji.

     > [!NOTE]
     > Jeśli chcesz dostarczyć strumienia, który jest szyfrowana za FairPlay i innego systemu zarządzania prawami cyfrowymi (DRM), należy skonfigurować zasady dostarczania oddzielne:
     >
     > * Jeden IAssetDeliveryPolicy, aby skonfigurować dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH) z wspólnego szyfrowania (CENC) (PlayReady i Widevine) i Smooth za pomocą PlayReady
     > * Inny IAssetDeliveryPolicy, aby skonfigurować FairPlay dla protokołu HLS
     >
     >
6. Utwórz Lokalizator OnDemand w celu uzyskania adresu URL przesyłania strumieniowego.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Aby użyć klucza dostawy FairPlay aplikacji odtwarzacza
Można programować aplikacje player przy użyciu zestawu SDK dla systemu iOS. Możliwość odtwarzania zawartości FairPlay, należy zaimplementować protokół wymiany licencji. Ten protokół nie jest określony przez firmę Apple. Jest każda aplikacja sposób wysyłania żądań klucza dostawy. Usługi Media Services FairPlay klucza dostawy oczekuje SPC znaleziona jako www-form-url post zakodowany komunikat w następującym formacie:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player nie obsługuje odtwarzania FairPlay poza pole. Uzyskanie odtwarzania FairPlay w systemie MAC OS X, uzyskać player próbki z konta dewelopera firmy Apple.
>
>

## <a name="streaming-urls"></a>Adresy URL przesyłania strumieniowego
Jeśli zawartości została zaszyfrowana z więcej niż jeden DRM, należy użyć tag szyfrowania w adresie URL przesyłania strumieniowego: (format = "m3u8-aapl, szyfrowanie = 'xxx').

Następujące kwestie:

* Można określić tylko zero lub jeden typ szyfrowania.
* Typ szyfrowania nie ma określonego w adresie URL, jeśli tylko jeden szyfrowania została zastosowana do zasobu.
* Typ szyfrowania jest uwzględniana wielkość liter.
* Można określić następujące typy szyfrowania:  
  * **cenc**: szyfrowania Common encryption (PlayReady lub Widevine)
  * **cbcs-aapl**: FairPlay
  * **CBC**: szyfrowanie AES envelope

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio

1. Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md). 
2. Dodaj następujące elementy do węzła **appSettings** zdefiniowanego w pliku app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Przykład

W poniższym przykładzie pokazano możliwość używania usługi Media Services do dostarczania zawartości zaszyfrowane za pomocą FairPlay. Ta funkcja została wprowadzona w Azure Media Services SDK dla platformy .NET w wersji 3.6.0. 

Zastąp kod w pliku Program.cs kodem przedstawionym w tej sekcji.

>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

Upewnij się, że zaktualizowano zmienne, tak aby wskazywały foldery, w których znajdują się pliki danych wejściowych.

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
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
