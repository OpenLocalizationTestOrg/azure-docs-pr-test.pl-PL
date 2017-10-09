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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="c8e2a-104">Przy użyciu Axinom toodeliver Widevine licencji tooAzure Media Services</span><span class="sxs-lookup"><span data-stu-id="c8e2a-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8e2a-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="c8e2a-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="c8e2a-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="c8e2a-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c8e2a-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c8e2a-107">Overview</span></span>
<span data-ttu-id="c8e2a-108">Azure Media Services (AMS) został dodany Google Widevine dynamiczną ochronę (zobacz [Mingfei w blogu](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="c8e2a-109">Ponadto usługi Azure Media Player (AMP) również została dodana obsługa Widevine (zobacz [dokumentu AMP](http://amp.azure.net/libs/amp/latest/docs/) szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="c8e2a-110">W nowoczesnych przeglądarkach wyposażony MSE i EME jest głównych zakończenia w strumienia DASH zawartość chroniona przez CENC z kilku-native DRM (PlayReady i Widevine).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="c8e2a-111">Począwszy od hello SDK .NET usługi Media Services wersja 3.5.2 Media Services umożliwia możesz tooconfigure szablonu licencji Widevine i uzyskać licencji Widevine.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="c8e2a-112">Można również użyć powitania po dostarczania licencji Widevine toohelp partnerów AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="c8e2a-113">W tym artykule opisano, jak toointegrate i testowania Widevine licencję na serwerze zarządzanym przez Axinom.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="c8e2a-114">W szczególności obejmuje:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="c8e2a-115">Konfigurowanie dynamicznego szyfrowania Common Encryption z wieloma DRM (PlayReady i Widevine) z odpowiednie adresy URL pozyskiwania licencji;</span><span class="sxs-lookup"><span data-stu-id="c8e2a-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="c8e2a-116">Generowanie tokenu JWT w kolejności toomeet powitania serwera wymagań dotyczących licencji;</span><span class="sxs-lookup"><span data-stu-id="c8e2a-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="c8e2a-117">Tworzenie aplikacji usługi Azure Media Player, która obsługuje nabycie licencji przy użyciu uwierzytelniania tokenu JWT;</span><span class="sxs-lookup"><span data-stu-id="c8e2a-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="c8e2a-118">Witaj całego systemu i hello przepływu zawartość, którą kluczy, kluczy identyfikator klucza inicjatora, JTW token i jego oświadczeń można najlepiej opisać za pomocą powitania po diagramu.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![KRESKA i CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="c8e2a-120">Ochrona zawartości</span><span class="sxs-lookup"><span data-stu-id="c8e2a-120">Content Protection</span></span>
<span data-ttu-id="c8e2a-121">Do konfigurowania ochrony dynamiczne i zasady dostarczania klucza, zobacz Mingfei w blogu: [sposób tworzenia pakietów Widevine tooconfigure w usłudze Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="c8e2a-122">Można skonfigurować dynamiczne ochrony CENC z wieloma DRM DASH przesyłania strumieniowego posiadające obie następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="c8e2a-123">Ochrona PlayReady MS Edge i IE11, mające ograniczenia tokenu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="c8e2a-124">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS), takich jak Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="c8e2a-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="c8e2a-125">Widevine ochrony dla programu Chrome, ich wymaga tokenu uwierzytelniania z token wystawiony przez inną usługę STS.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="c8e2a-126">Zobacz [generowania tokenów JWT](media-services-axinom-integration.md#jwt-token-generation) sekcji dlaczego usługi Azure Active Directory nie można użyć jako tokenu Zabezpieczającego serwera licencji Widevine przez Axinom.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="c8e2a-127">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="c8e2a-127">Considerations</span></span>
1. <span data-ttu-id="c8e2a-128">Należy użyć hello określone Axinom klucza inicjatora (8888000000000000000000000000000000000000) i wygenerowanych lub wybranego klucza identyfikator toogenerate hello zawartość klucza do konfigurowania usługi dostarczania klucza.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="c8e2a-129">Serwer licencji Axinom wystawi wszystkie licencje zawierający klucze zawartości na podstawie na powitania klucza inicjatora, która jest prawidłowa dla testowania i produkcji.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="c8e2a-130">adres URL pozyskiwania licencji Widevine Hello do testowania: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="c8e2a-131">Protokół HTTP ani HTTS są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="c8e2a-132">Przygotowanie odtwarzacz multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="c8e2a-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="c8e2a-133">AMP v1.4.0 obsługuje odtwarzanie AMS spakowanego dynamicznie z PlayReady i Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="c8e2a-134">Jeśli serwer licencji Widevine nie wymaga uwierzytelniania tokenu, nie ma dodatkowych należy tootest toodo kreska zawartość chroniona przez Widevine.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="c8e2a-135">Na przykład zespołu hello AMP udostępnia prostą [próbki](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), w którym można obejrzeć go do pracy w Edge i IE11 za pomocą PlayReady i Chrome przy użyciu metody Widevine.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="c8e2a-136">serwer licencji Widevine Hello podał Axinom wymaga uwierzytelnienia tokenu JWT.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="c8e2a-137">Hello JWT token musi toobe przesłane z żądaniem licencji za pośrednictwem nagłówka HTTP "X-AxDRM-komunikat".</span><span class="sxs-lookup"><span data-stu-id="c8e2a-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="c8e2a-138">W tym celu należy hello tooadd javascript na stronie sieci web hello hosting AMP przed ustawienie hello źródła po:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="c8e2a-139">pozostałe Hello kodzie AMP jest standardowe API AMP jak dokument AMP [tutaj](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="c8e2a-140">Należy pamiętać, że hello powyżej javascript dla ustawienia, które nagłówek autoryzacji niestandardowej nadal jest podejście krótkoterminowa przed oficjalne hello, wydania długoterminowej podejścia AMP.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="c8e2a-141">Generowanie tokenów JWT</span><span class="sxs-lookup"><span data-stu-id="c8e2a-141">JWT Token Generation</span></span>
<span data-ttu-id="c8e2a-142">Serwer licencji Axinom Widevine testowania wymaga uwierzytelnienia tokenu JWT.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="c8e2a-143">Ponadto jednym z oświadczeń hello w hello JWT token jest typu obiekt złożony zamiast typu danych pierwotnych.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="c8e2a-144">Niestety usługi Azure AD może wystawiać tokeny JWT z typami pierwotnymi.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="c8e2a-145">Podobnie interfejsu API dla platformy .NET Framework (Klasa System.IdentityModel.Tokens.SecurityTokenHandler i JwtPayload) zezwala tylko tooinput obiekt złożony typu jako oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="c8e2a-146">Jednak oświadczeń hello nadal są serializowane jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="c8e2a-147">W związku z tym nie można użyć dowolnego hello dwa do generowania tokenu JWT hello żądania licencji Widevine.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="c8e2a-148">Jan Sheehan [pakietu JWT Nuget](https://www.nuget.org/packages/JWT) spełnia potrzeby Witaj, więc zamierzamy toouse tego pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="c8e2a-149">Poniżej znajduje się kod hello generowania tokenu JWT z hello wymaganych oświadczeń, co jest wymagane przez serwer licencji Axinom Widevine do testowania:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

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

<span data-ttu-id="c8e2a-150">Serwer licencji Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="c8e2a-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="c8e2a-151">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="c8e2a-151">Considerations</span></span>
1. <span data-ttu-id="c8e2a-152">Mimo że wymaga usługi dostarczania licencji AMS PlayReady "Bearer =" kolejnych tokenu uwierzytelniania serwera licencji Axinom Widevine nie używa ich.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="c8e2a-153">klucz komunikacji Axinom Hello jest używany jako klucza podpisywania.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="c8e2a-154">Należy zauważyć, że klucz hello jest ciąg znaków szesnastkowych, jednak ją muszą być traktowane jako serię bajtów nie ciągu podczas kodowania.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="c8e2a-155">Jest to osiągane przez metodę hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="c8e2a-156">Pobieranie Identyfikatora klucza</span><span class="sxs-lookup"><span data-stu-id="c8e2a-156">Retrieving Key ID</span></span>
<span data-ttu-id="c8e2a-157">Można zauważyć, że w kodzie hello generowania token JWT identyfikator tokenu, klucza jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="c8e2a-158">Ponieważ tokenu JWT hello musi toobe gotowe przed załadowaniem AMP player, klucza potrzeb ID pobierane toobe w kolejności toogenerate tokenu JWT.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="c8e2a-159">Oczywiście, który istnieje wiele sposobów tooget przechowywania klucza identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="c8e2a-160">Na przykład, co może przechowywać Identyfikatora klucza wraz z zawartością metadanych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="c8e2a-161">Lub może pobrać Identyfikatora z MPD DASH (opis prezentacji nośnika) pliku klucza.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="c8e2a-162">Poniższy kod Hello dotyczy hello później.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-162">hello code below is for hello latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="c8e2a-163">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c8e2a-163">Summary</span></span>
<span data-ttu-id="c8e2a-164">Z najnowszy dodatek Widevine obsługi zarówno w przypadku ochrony zawartości Azure Media Services, jak i usługi Azure Media Player, możemy tooimplement przesyłania strumieniowego z DASH + kilku native DRM (PlayReady i Widevine) z usługą licencji PlayReady, zarówno w licencji AMS i Widevine Serwer z Axinom powitania po nowoczesnymi przeglądarkami:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="c8e2a-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="c8e2a-165">Chrome</span></span>
* <span data-ttu-id="c8e2a-166">Przeglądarka Microsoft Edge w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="c8e2a-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="c8e2a-167">IE 11 na Windows 8.1 i Windows 10</span><span class="sxs-lookup"><span data-stu-id="c8e2a-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="c8e2a-168">Zarówno Firefox (Desktop) Safari dla komputerów Mac (nie iOS) również są obsługiwane za pośrednictwem programu Silverlight i hello tego samego adresu URL przy użyciu usługi Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="c8e2a-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="c8e2a-169">Witaj następujące parametry są wymagane w hello mini rozwiązania korzystanie z usług serwera licencji Axinom Widevine.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="c8e2a-170">Z wyjątkiem klucza Identyfikatora hello pozostałe parametry są dostarczane przez Axinom na podstawie ich Widevine konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="c8e2a-171">Parametr</span><span class="sxs-lookup"><span data-stu-id="c8e2a-171">Parameter</span></span> | <span data-ttu-id="c8e2a-172">Jak jest używany</span><span class="sxs-lookup"><span data-stu-id="c8e2a-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="c8e2a-173">Identyfikator klucza komunikacji</span><span class="sxs-lookup"><span data-stu-id="c8e2a-173">Communication key ID</span></span> |<span data-ttu-id="c8e2a-174">Musi być uwzględniony jako wartość oświadczenia hello "com_key_id" w JWT token (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c8e2a-175">Klucz komunikacji</span><span class="sxs-lookup"><span data-stu-id="c8e2a-175">Communication key</span></span> |<span data-ttu-id="c8e2a-176">Musi być używany jako hello klucza podpisywania tokenu JWT (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c8e2a-177">Klucza inicjatora</span><span class="sxs-lookup"><span data-stu-id="c8e2a-177">Key seed</span></span> |<span data-ttu-id="c8e2a-178">Muszą być używane toogenerate klucz zawartości ze wszystkimi podane zawartości Identyfikatora klucza (zobacz [to](media-services-axinom-integration.md#content-protection) sekcji).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="c8e2a-179">Adres URL pozyskiwania licencji Widevine</span><span class="sxs-lookup"><span data-stu-id="c8e2a-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="c8e2a-180">Musi być używany w Konfigurowanie zasad dostarczania elementów zawartości dla strumienia DASH (zobacz [to](media-services-axinom-integration.md#content-protection) sekcji).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="c8e2a-181">Identyfikator klucza zawartości</span><span class="sxs-lookup"><span data-stu-id="c8e2a-181">Content Key ID</span></span> |<span data-ttu-id="c8e2a-182">Musi być uwzględniony hello wartości oświadczenia komunikatów dotyczących tokenu JWT (zobacz [to](media-services-axinom-integration.md#jwt-token-generation) sekcji).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="c8e2a-183">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="c8e2a-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8e2a-184">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="c8e2a-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="c8e2a-185">Potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="c8e2a-185">Acknowledgments</span></span>
<span data-ttu-id="c8e2a-186">Chcielibyśmy hello tooacknowledge od osób, które przyczyniły się do tworzenia tego dokumentu: Kristjan Jõgi z Axinom, Mingfei Yan i Rajput Amitowi.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

