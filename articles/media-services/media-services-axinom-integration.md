---
title: aaaUsing Axinom toodeliver Widevine licencje tooAzure Media Services | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak używasz usługi Azure Media Services (AMS) toodeliver dynamicznie szyfrowanych przez AMS z PlayReady i Widevine DRMs strumienia. licencji PlayReady Hello pochodzi z serwera licencji Media Services PlayReady i licencji Widevine jest dostarczany przez serwer licencji Axinom."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Przy użyciu Axinom toodeliver Widevine licencji tooAzure Media Services
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Omówienie
Azure Media Services (AMS) został dodany Google Widevine dynamiczną ochronę (zobacz [Mingfei w blogu](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) szczegółowe informacje). Ponadto usługi Azure Media Player (AMP) również została dodana obsługa Widevine (zobacz [dokumentu AMP](http://amp.azure.net/libs/amp/latest/docs/) szczegółowe informacje). W nowoczesnych przeglądarkach wyposażony MSE i EME jest głównych zakończenia w strumienia DASH zawartość chroniona przez CENC z kilku-native DRM (PlayReady i Widevine).

Począwszy od hello SDK .NET usługi Media Services wersja 3.5.2 Media Services umożliwia możesz tooconfigure szablonu licencji Widevine i uzyskać licencji Widevine. Można również użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

W tym artykule opisano, jak toointegrate i testowania Widevine licencję na serwerze zarządzanym przez Axinom. W szczególności obejmuje:  

* Konfigurowanie dynamicznego szyfrowania Common Encryption z wieloma DRM (PlayReady i Widevine) z odpowiednie adresy URL pozyskiwania licencji;
* Generowanie tokenu JWT w kolejności toomeet powitania serwera wymagań dotyczących licencji;
* Tworzenie aplikacji usługi Azure Media Player, która obsługuje nabycie licencji przy użyciu uwierzytelniania tokenu JWT;

Witaj całego systemu i hello przepływu zawartość, którą kluczy, kluczy identyfikator klucza inicjatora, JTW token i jego oświadczeń można najlepiej opisać za pomocą powitania po diagramu.

![KRESKA i CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Ochrona zawartości
Do konfigurowania ochrony dynamiczne i zasady dostarczania klucza, zobacz Mingfei w blogu: [sposób tworzenia pakietów Widevine tooconfigure w usłudze Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Można skonfigurować dynamiczne ochrony CENC z wieloma DRM DASH przesyłania strumieniowego posiadające obie następujące hello:

1. Ochrona PlayReady MS Edge i IE11, mające ograniczenia tokenu autoryzacji. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS), takich jak Azure Active Directory;
2. Widevine ochrony dla programu Chrome, ich wymaga tokenu uwierzytelniania z token wystawiony przez inną usługę STS. 

Zobacz [generowania tokenów JWT](media-services-axinom-integration.md#jwt-token-generation) sekcji dlaczego usługi Azure Active Directory nie można użyć jako tokenu Zabezpieczającego serwera licencji Widevine przez Axinom.

### <a name="considerations"></a>Zagadnienia do rozważenia
1. Należy użyć hello określone Axinom klucza inicjatora (8888000000000000000000000000000000000000) i wygenerowanych lub wybranego klucza identyfikator toogenerate hello zawartość klucza do konfigurowania usługi dostarczania klucza. Serwer licencji Axinom wystawi wszystkie licencje zawierający klucze zawartości na podstawie na powitania klucza inicjatora, która jest prawidłowa dla testowania i produkcji.
2. adres URL pozyskiwania licencji Widevine Hello do testowania: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). Protokół HTTP ani HTTS są dozwolone.

## <a name="azure-media-player-preparation"></a>Przygotowanie odtwarzacz multimediów Azure
AMP v1.4.0 obsługuje odtwarzanie AMS spakowanego dynamicznie z PlayReady i Widevine DRM.
Jeśli serwer licencji Widevine nie wymaga uwierzytelniania tokenu, nie ma dodatkowych należy tootest toodo kreska zawartość chroniona przez Widevine. Na przykład zespołu hello AMP udostępnia prostą [próbki](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), w którym można obejrzeć go do pracy w Edge i IE11 za pomocą PlayReady i Chrome przy użyciu metody Widevine.
serwer licencji Widevine Hello podał Axinom wymaga uwierzytelnienia tokenu JWT. Hello JWT token musi toobe przesłane z żądaniem licencji za pośrednictwem nagłówka HTTP "X-AxDRM-komunikat". W tym celu należy hello tooadd javascript na stronie sieci web hello hosting AMP przed ustawienie hello źródła po:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

pozostałe Hello kodzie AMP jest standardowe API AMP jak dokument AMP [tutaj](http://amp.azure.net/libs/amp/latest/docs/).

Należy pamiętać, że hello powyżej javascript dla ustawienia, które nagłówek autoryzacji niestandardowej nadal jest podejście krótkoterminowa przed oficjalne hello, wydania długoterminowej podejścia AMP.

## <a name="jwt-token-generation"></a>Generowanie tokenów JWT
Serwer licencji Axinom Widevine testowania wymaga uwierzytelnienia tokenu JWT. Ponadto jednym z oświadczeń hello w hello JWT token jest typu obiekt złożony zamiast typu danych pierwotnych.

Niestety usługi Azure AD może wystawiać tokeny JWT z typami pierwotnymi. Podobnie interfejsu API dla platformy .NET Framework (Klasa System.IdentityModel.Tokens.SecurityTokenHandler i JwtPayload) zezwala tylko tooinput obiekt złożony typu jako oświadczenia. Jednak oświadczeń hello nadal są serializowane jako ciąg. W związku z tym nie można użyć dowolnego hello dwa do generowania tokenu JWT hello żądania licencji Widevine.

Jan Sheehan [pakietu JWT Nuget](https://www.nuget.org/packages/JWT) spełnia potrzeby Witaj, więc zamierzamy toouse tego pakietu Nuget.

Poniżej znajduje się kod hello generowania tokenu JWT z hello wymaganych oświadczeń, co jest wymagane przez serwer licencji Axinom Widevine do testowania:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

Serwer licencji Axinom Widevine

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Zagadnienia do rozważenia
1. Mimo że wymaga usługi dostarczania licencji AMS PlayReady "Bearer =" kolejnych tokenu uwierzytelniania serwera licencji Axinom Widevine nie używa ich.
2. klucz komunikacji Axinom Hello jest używany jako klucza podpisywania. Należy zauważyć, że klucz hello jest ciąg znaków szesnastkowych, jednak ją muszą być traktowane jako serię bajtów nie ciągu podczas kodowania. Jest to osiągane przez metodę hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Pobieranie Identyfikatora klucza
Można zauważyć, że w kodzie hello generowania token JWT identyfikator tokenu, klucza jest wymagana. Ponieważ tokenu JWT hello musi toobe gotowe przed załadowaniem AMP player, klucza potrzeb ID pobierane toobe w kolejności toogenerate tokenu JWT.

Oczywiście, który istnieje wiele sposobów tooget przechowywania klucza identyfikatora. Na przykład, co może przechowywać Identyfikatora klucza wraz z zawartością metadanych w bazie danych. Lub może pobrać Identyfikatora z MPD DASH (opis prezentacji nośnika) pliku klucza. Poniższy kod Hello dotyczy hello później.

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a>Podsumowanie
Z najnowszy dodatek Widevine obsługi zarówno w przypadku ochrony zawartości Azure Media Services, jak i usługi Azure Media Player, możemy tooimplement przesyłania strumieniowego z DASH + kilku native DRM (PlayReady i Widevine) z usługą licencji PlayReady, zarówno w licencji AMS i Widevine Serwer z Axinom powitania po nowoczesnymi przeglądarkami:

* Chrome
* Przeglądarka Microsoft Edge w systemie Windows 10
* IE 11 na Windows 8.1 i Windows 10
* Zarówno Firefox (Desktop) Safari dla komputerów Mac (nie iOS) również są obsługiwane za pośrednictwem programu Silverlight i hello tego samego adresu URL przy użyciu usługi Azure Media Player

Witaj następujące parametry są wymagane w hello mini rozwiązania korzystanie z usług serwera licencji Axinom Widevine. Z wyjątkiem klucza Identyfikatora hello pozostałe parametry są dostarczane przez Axinom na podstawie ich Widevine konfiguracji serwera.

| Parametr | Jak jest używany |
| --- | --- |
| Identyfikator klucza komunikacji |Musi być uwzględniony jako wartość oświadczenia hello "com_key_id" w JWT token (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji). |
| Klucz komunikacji |Musi być używany jako hello klucza podpisywania tokenu JWT (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji). |
| Klucza inicjatora |Muszą być używane toogenerate klucz zawartości ze wszystkimi podane zawartości Identyfikatora klucza (zobacz [to](media-services-axinom-integration.md#content-protection) sekcji). |
| Adres URL pozyskiwania licencji Widevine |Musi być używany w Konfigurowanie zasad dostarczania elementów zawartości dla strumienia DASH (zobacz [to](media-services-axinom-integration.md#content-protection) sekcji). |
| Identyfikator klucza zawartości |Musi być uwzględniony hello wartości oświadczenia komunikatów dotyczących tokenu JWT (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji). |

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Potwierdzenia
Chcielibyśmy hello tooacknowledge od osób, które przyczyniły się do tworzenia tego dokumentu: Kristjan Jõgi z Axinom, Mingfei Yan i Rajput Amitowi.

