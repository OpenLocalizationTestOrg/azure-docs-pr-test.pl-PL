---
title: "toocustomers zawartości aaaDelivering | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie co uczestniczy w dostarczaniu zawartości przy użyciu usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Dostarczanie zawartości toocustomers
Gdy programową przesyłania strumieniowego lub wideo na żądanie toocustomers zawartości jest toodeliver toovarious wideo wysokiej jakości urządzeń bez względu na warunki panujące w sieci.

tooachieve w tym celu można wykonywać następujące czynności:

* Kodowanie strumienia wideo strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej szybkości transmisji bitów). To zajmie się jakość i warunki sieciowe.
* Użyj usługi Microsoft Azure Media Services [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md) toodynamically ponownego tworzenia pakietów strumienia w różnych protokołów. To zajmie się przesyłania strumieniowego na różnych urządzeniach. Usługa Media Services obsługuje dostarczanie hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG-DASH.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

Ten artykuł zawiera omówienie założeń ważne dostarczania zawartości.

toocheck znane problemy, zobacz [znane problemy](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Dynamiczne tworzenie pakietów
Dzięki funkcji dynamicznego tworzenia pakietów hello tego Media Services udostępnia, można dostarczyć zawartość o adaptacyjnej szybkości bitowej MP4 lub Smooth Streaming zakodowane w formatach transmisji strumieniowej obsługiwanych przez usługę Media Services (MPEG-DASH, HLS, Smooth Streaming) bez konieczności pakietu toore do formatach przesyłania strumieniowego. Firma Microsoft zaleca dostarczania zawartości z dynamicznego tworzenia pakietów.

tootake korzyści z dynamicznego tworzenia pakietów, należy tooencode (źródłowy) mezzanine do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów.

Dzięki funkcji dynamicznego tworzenia pakietów, można przechowywać i opłacać pliki hello w jednym formacie magazynu. Usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań użytkownika.

Dynamiczne tworzenie pakietów jest dostępna dla standardowa i premium punkty końcowe przesyłania strumieniowego. 

Aby uzyskać więcej informacji, zobacz [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtry i manifestów dynamiczne
Można zdefiniować filtry dla zasobów z usługi Media Services. Te filtry są reguły po stronie serwera, które ułatwiają wykonywanie czynności, takie jak odtwarzanie określonej sekcji wideo lub określić podzestaw wersji audio i wideo, które urządzenia klienta może obsłużyć (a nie wszystkie wersje hello skojarzonych z zasobów hello klientów ). Filtrowanie to odbywa się za pośrednictwem *dynamiczne manifestów* które są tworzone, gdy klient żąda toostream wideo na podstawie jednej lub większej liczby określonych filtrów.

Aby uzyskać więcej informacji, zobacz [filtry i manifestów dynamiczne](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Lokalizatory
tooprovide użytkownikowi adres URL, który może być używane toostream lub pobierania zawartości, należy najpierw toopublish zawartości, tworząc Lokalizator. Lokalizator umożliwia hello tooaccess punktu wejścia plików znajdujących się w zasób. Usługa Media Services obsługuje dwa typy lokalizatorów:

* Lokalizatory OnDemandOrigin. Te są używane toostream nośnika (na przykład MPEG-DASH, HLS lub Smooth Streaming) lub pobrać progresywnie pliki.
* Lokalizatory adres URL sygnatury dostępu Współdzielonego dostępu współdzielonego. Są to komputer lokalny tooyour toodownload używane nośnika plików.

*Zasady dostępu* jest używane toodefine hello uprawnienia (na przykład odczytu, zapisu i listy) i czas trwania, dla których klient ma dostęp do określonego zasobu. Należy pamiętać, że hello listy uprawnień (AccessPermissions.List) nie należy używać podczas tworzenia Lokalizator OrDemandOrigin.

Lokalizatory mają datę wygaśnięcia. Witaj portalu Azure ustawia datę wygaśnięcia 100 lat. w hello przyszłych lokalizatorów.

> [!NOTE]
> Jeśli używasz hello Azure toocreate portalu lokalizatorów przed marcem 2015 r. te lokalizatorów zostały ustawione tooexpire po upływie dwóch lat.
> 
> 

tooupdate Data wygaśnięcia na lokalizatorze użyj [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) lub [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) interfejsów API. Należy pamiętać, że po zaktualizowaniu hello daty wygaśnięcia lokalizatora SAS następuje zmiana adresu URL hello.

Lokalizatory nie są zaprojektowane kontroli dostępu użytkownika toomanage. Dostęp do różnych można umożliwić użytkownikom tooindividual praw przy użyciu rozwiązań zarządzania prawami cyfrowymi (DRM). Aby uzyskać więcej informacji, zobacz [zabezpieczania nośnika](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Tworząc Lokalizator, może być 30-sekundowe opóźnienie powodu toorequired magazynu i propagacji procesów w usłudze Azure Storage.

## <a name="adaptive-streaming"></a>Adaptacyjną przesyłania strumieniowego
Technologie adaptacyjną szybkością transmisji bitów zezwolić aplikacji odtwarzacza wideo toodetermine się warunków sieciowych i wybierz z kilku szybkości transmisji bitów. Podczas komunikacji sieciowej obniża, powitania klienta można wybrać niższe szybkości transmisji bitów tak odtwarzania można kontynuować niższej jakości wideo. Jak zwiększyć się warunków sieciowych, powitania klienta można przełączać tooa wyższej szybkości transmisji bitów z poprawy jakości wideo. Usługa Azure Media Services obsługuje hello następujące technologie adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG-DASH.

tooprovide użytkowników z adresami URL przesyłania strumieniowego, najpierw należy utworzyć Lokalizator OnDemandOrigin. Tworzenie lokalizatora zapewnia hello ścieżki bazowej toohello zawartości, który zawiera zawartość hello hello ma toostream. Jednak toobe stanie toostream ta zawartość, należy toomodify dalsze tej ścieżki. tooconstruct pełne toohello adres URL przesyłania strumieniowego pliku manifestu, musi łączyć hello lokalizatora ścieżki wartość i hello (filename.ism) Nazwa pliku manifestu. Następnie dołącz **/Manifest** i odpowiedni format (w razie potrzeby) toohello lokalizatora ścieżki.

> [!NOTE]
> Można również strumienia zawartości za pośrednictwem połączenia SSL. toodo, upewnij się, że uruchamiania adresy URL przesyłania strumieniowego z protokołu HTTPS. Należy zauważyć, że obecnie AMS nie obsługuje protokołu SSL z domen niestandardowych.  
> 


Można tylko strumienia za pośrednictwem protokołu SSL Jeśli hello, z którego dostarczać zawartość z punktu końcowego przesyłania strumieniowego został utworzony po 10 września 2014 r. Jeśli Twoje adresy URL przesyłania strumieniowego są oparte na powitania utworzone po 10 września 2014 punkty końcowe przesyłania strumieniowego hello adres URL zawiera "streaming.mediaservices.windows.net." Adresy URL przesyłania strumieniowego zawierające "origin.mediaservices.windows.net" (stary format hello) nie obsługują protokołu SSL. Jeśli adres URL jest w starym formacie hello i chcesz toobe toostream mogli za pośrednictwem protokołu SSL, należy utworzyć nowy punkt końcowy przesyłania strumieniowego. Użyj adresów URL na podstawie nowych przesyłania strumieniowego punktu końcowego toostream hello zawartości za pośrednictwem protokołu SSL.

## <a name="streaming-url-formats"></a>Formaty adresu URL przesyłania strumieniowego
### <a name="mpeg-dash-format"></a>Format MPEG-DASH
{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=mpd-Time-CSF)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Format V4 Apple HTTP Live Streaming (HLS)
{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Format V3 Apple HTTP Live Streaming (HLS)
{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Format Apple HTTP Live Streaming (HLS) z filtrem tylko audio
Domyślnie tylko dźwięk ścieżki są uwzględniane w powitalne HLS manifestu. Jest to wymagane do sklepu Apple certyfikacji dla sieci komórkowej. W takim przypadku jeśli klient nie ma wystarczającą przepustowość lub jest połączony za pośrednictwem połączenia 2G, odtwarzania zmienia tylko tooaudio. Dzięki temu przesyłania strumieniowego bez buforowania zawartości tookeep, ale nie ma żadnego obrazu. W niektórych scenariuszach player buforowanie może mieć pierwszeństwo tylko audio. Śledź hello tooremove tylko dźwięk, należy dodać **tylko dźwięk = false** toohello adresu URL.

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=m3u8-aapl-v3,audio-Only=false)

Aby uzyskać więcej informacji, zobacz [wyjściowe dodatkowe funkcje obsługi tworzenia manifestu dynamicznych i HLS](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Smooth Streaming formatu
{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest

Przykład:

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest

### <a id="fmp4_v20"></a>Smooth Streaming 2.0 manifestu (starszej wersji manifestu)
Domyślnie Smooth Streaming format manifestu zawiera tag powtarzania hello (r-tag). Jednak niektóre odtwarzacze nie obsługują hello r-tag. Klienci z te odtwarzacze można użyć formatu, który powoduje wyłączenie hello r-tag:

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=fmp4-v20) przesyłania strumieniowego

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Pobierania progresywnego
Pobierania progresywnego można rozpocząć odtwarzanie multimediów przed hello cały plik został pobrany. Nie można pobrać progresywnie .ism * (ismv isma, ismt pliki lub ismc).

tooprogressively pobieranie zawartości, należy użyć typu OnDemandOrigin hello lokalizatora. Witaj poniższy przykład przedstawia hello adres URL, który jest oparty na powitania OnDemandOrigin Typ lokalizatora:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Należy odszyfrować zasoby magazynu systemu szyfrowania plików, które mają toostream z hello usługi punkt początkowy dla pobierania progresywnego.

## <a name="download"></a>Do pobrania
toodownload tooa zawartości urządzenia klienta, należy utworzyć lokalizatora SAS. zapewnia lokalizatora SAS Hello dostępu toohello kontenera magazynu Azure, gdzie znajduje się plik. adres URL pobierania hello toobuild, masz tooembed nazwę pliku hello między hostem hello i sygnatury SAS.

Witaj poniższy przykład przedstawia hello adres URL, który jest oparty na lokalizatora SAS hello:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

Zastosuj Hello następujące zagadnienia:

* Należy odszyfrować zasoby magazynu systemu szyfrowania plików, które mają toostream z hello usługi punkt początkowy dla pobierania progresywnego.
* Pobieranie, które nie zostało ukończone w ciągu 12 godzin zakończy się niepowodzeniem.

## <a name="streaming-endpoints"></a>Punkty końcowe przesyłania strumieniowego

Punkt końcowy przesyłania strumieniowego reprezentuje przesyłania strumieniowego usługa, która może dostarczać zawartość bezpośrednio tooa klienta player aplikacji lub tooa sieci dostarczania zawartości (CDN) do dalszej dystrybucji. Witaj strumienia wychodzącego z usługą punktu końcowego przesyłania strumieniowego może być strumień na żywo lub zasobów wideo na żądanie, w ramach konta usługi Media Services. Istnieją dwa typy punkty końcowe, przesyłania strumieniowego **standardowe** i **premium**. Aby uzyskać więcej informacji, zobacz [Omówienie punktów końcowych przesyłania strumieniowego](media-services-streaming-endpoints-overview.md).

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

## <a name="known-issues"></a>Znane problemy
### <a name="changes-toosmooth-streaming-manifest-version"></a>Wersja manifestu zmiany tooSmooth przesyłania strumieniowego
Czy zgodne przed zwróceniem hello wersja usługi lipca 2016 — gdy zasoby utworzone przez Media Encoder Standard Media Encoder Premium w przepływie pracy i hello wcześniejszych Azure Media Encoder zostały strumieniowego za pomocą dynamicznego tworzenia pakietów — Witaj Smooth Streaming manifestu tooversion 2.0. W wersji 2.0 czas trwania fragmentu hello nie należy używać hello tagi tak zwane Powtórz (r). Na przykład:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

W hello lipca 2016 r. wersja usługi hello wygenerowany manifest Smooth Streaming zgodne tooversion 2.2, o czasie trwania fragmentu przy użyciu powtarzania tagów. Na przykład:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Niektóre starszych klientów Smooth Streaming hello może nie obsługiwać hello powtarzania tagów i zakończy się niepowodzeniem tooload hello manifestu. toomitigate ten problem, można użyć parametru starszej wersji manifestu format hello **(format = fmp4 v20)** lub zaktualizuj z klienta toohello najnowszej wersji, która obsługuje powtarzania znaczników. Aby uzyskać więcej informacji, zobacz [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Powiązane tematy
[Aktualizacja usługi Media Services lokalizatorów po wycofanie magazynu kluczy](media-services-roll-storage-access-keys.md)

