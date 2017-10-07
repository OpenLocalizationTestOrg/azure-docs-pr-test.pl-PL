---
title: "aaaFilters i manifestów dynamiczne | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toocreate filtry, aby klient mógł ich użyć toostream określonych sekcji strumienia. Usługi Media Services tworzy dynamiczne manifestów tooarchive selektywnego strumienia."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtry i manifestów dynamiczne
Począwszy od wersji 2.11, Media Services umożliwia filtry toodefine trwałych. Te filtry są reguły po stronie serwera, zezwalające klientom toochoose toodo np.: odtwarzanie tylko części klipu wideo (a nie odtwarzane hello całego wideo), lub określ tylko podzestaw audio i wideo wersji obsługi (przez klienta urządzenia zamiast wersji hello wszystkich skojarzonych z hello zasobów). Filtrowania elementów zawartości zostaną zarchiwizowane za pośrednictwem **dynamiczne manifestu**, które są tworzone w chwili toostream żądania klienta wideo oparte na określonej filtry.

Tematy to omówiono typowe scenariusze, w którym za pomocą filtrów będą tootopics klientów i linki tooyour bardzo przydatne, które pokazują, jak programowo toocreate filtry (obecnie można tworzyć filtry z interfejsów API REST tylko).

## <a name="overview"></a>Omówienie
W celu dostarczenia Twojej zawartości toocustomers (wydarzeń transmisji strumieniowej na żywo lub wideo) poznasz jest toodeliver wysokiej jakości wideo toovarious urządzeń bez względu na warunki panujące w sieci. w tym celu hello po tooachieve:

* kodowanie z strumienia toomulti szybkości transmisji bitów ([adaptacyjną szybkością transmisji bitów](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) strumienia wideo (to zajmie się jakość i warunki sieciowe) i 
* Użyj usługi Media Services [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md) toodynamically ponownego tworzenia pakietów strumienia w różnych protokołów (to zajmie się przesyłania strumieniowego na różnych urządzeniach). Usługa Media Services obsługuje dostarczanie hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH. 

### <a name="manifest-files"></a>Pliki manifestu
Podczas kodowania zawartości do przesyłania strumieniowego o adaptacyjnej szybkości bitowej, **manifestu** (odtwarzania) jest tworzony (plik hello jest tekstowy lub opartych na języku XML). Witaj **manifestu** plik zawiera przesyłania strumieniowego metadane, takie jak: śledzenie typu (audio, wideo lub tekst) oraz śledzenie nazwę, godzina rozpoczęcia i zakończenia, szybkości transmisji bitów (właściwości), Śledź języków, okna prezentacji (czas określony na metodzie przesuwanego okna), wideo Koder-dekoder (FourCC). Nakazuje również hello player tooretrieve hello dalej fragmentu, podając informacje o hello dalej rozgrywane wideo fragmenty dostępne i ich lokalizacji. Fragmenty (lub segmentów) są hello rzeczywiste "fragmentów" o zawartości wideo.

Oto przykład pliku manifestu: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Dynamiczne manifestów
Brak [scenariusze](media-services-dynamic-manifest-overview.md#scenarios) gdy klient potrzebuje większą elastyczność niż opisany w pliku manifestu hello domyślne zasobów. Na przykład:

* Urządzenie: dostarczać tylko hello określonych wersji woluminu, określony język ścieżek, które są obsługiwane przez urządzenie hello jest używany tooplayback hello zawartości ("wersji filtrowanie"). 
* Zmniejsz hello manifestu tooshow klipem podrzędne wydarzenia na żywo ("filtrowanie obiekty podrzędne").
* Początek przycięcia hello wideo ("Przycinanie wideo").
* Dostosuj prezentacji okna (DVR) w kolejności tooprovide ograniczona długość okna DVR hello player hello ("Dostosowywanie okna prezentacji").

tooachieve to elastyczność, oferty usługi Media Services **dynamiczne manifesty** oparte na wstępnie zdefiniowane [filtry](media-services-dynamic-manifest-overview.md#filters).  Po zdefiniowaniu filtrów hello klientów można używać ich toostream określonej wersji lub podrzędne klipy wideo. Czy określają filtry w hello URL przesyłania strumieniowego. Filtry mogą być zastosowane tooadaptive szybkości transmisji bitów przesyłania strumieniowego protokołów obsługiwanych przez [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md): HLS, MPEG DASH i Smooth Streaming. Na przykład:

MPEG DASH URL z filtrem

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

Smooth Streaming URL z filtrem

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Aby uzyskać więcej informacji o tym, jak toodeliver zawartość i kompilacji przesyłania strumieniowego adresów URL, zobacz [dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).

> [!NOTE]
> Należy pamiętać, że manifesty dynamiczne nie zmieniaj hello zasobów i hello manifest domyślny dla tego zasobu. Klienta można wybrać toorequest strumienia z lub bez filtrów. 
> 
> 

### <a id="filters"></a>Filtry
Istnieją dwa typy filtrów zasobów: 

* Filtry globalne (może być zastosowane tooany zasobów w hello konta usługi Azure Media Services, okres istnienia hello konta) oraz 
* Filtry lokalnego (może być tylko zastosowany tooan zasobów z hello, który został skojarzony po utworzeniu filtru, okres istnienia hello zasobów). 

Typy filtrów globalne i lokalne ma dokładnie takie same właściwości hello. Witaj podstawowa różnica między hello dwa jest w scenariuszach, które jest bardziej odpowiedni typ plików. Filtry globalne są zazwyczaj odpowiednie profile urządzeń (filtrowanie wersji) gdzie lokalnego filtry mogą być używane tootrim określonych zasobów.

## <a id="scenarios"></a>Typowe scenariusze
Jak wspomniano wcześniej, po dostarczanie Twojej zawartości toocustomers (wydarzeń transmisji strumieniowej na żywo lub wideo) poznasz toodeliver wysokiej jakości wideo toovarious urządzeń w różnych sieci warunków. Ponadto sieci może mają inne wymagania, które obejmują filtrowanie zasobów i korzystanie z **dynamiczne manifestu**s. następujące sekcje Hello podać krótki przegląd informacji o różnych scenariuszy filtrowania.

* Określ podzestaw wersji audio i wideo, które może obsłużyć niektórych urządzeń, (a nie wszystkie wersje hello skojarzonych z zasobów hello). 
* Odtwarzanie do tyłu tylko części klipu wideo (zamiast hello odtwarzanie całego wideo).
* Dostosuj DVR okna prezentacji.

## <a name="rendition-filtering"></a>Filtrowanie wersji
Możesz wybrać tooencode toomultiple zasobów kodowania profile (H.264 linii bazowej, H.264 wysoki, AACL, AACH, Dolby Digital Plus) i wielokrotnych szybkości transmisji bitów jakości. Jednak nie wszystkie urządzenia klienta zostanie obsługują, profile wszystkich elementów zawartości i szybkości transmisji bitów. Starsze urządzenia z systemem Android obsługuje tylko H.264 linii bazowej + AACL. Wysyła wyższej szybkości transmisji bitów tooa urządzenia, co nie można pobrać hello korzyści, marnuje obliczeń przepustowości i urządzeń. Takie urządzenia muszą dekodowania wszystkie hello podany informacji, tylko tooscale go w dół do wyświetlenia.

Manifest dynamiczne umożliwia tworzenie profilów urządzeń takich jak telefon komórkowy, konsoli HD/SD itp. i zawierać ścieżek hello i właściwości, które mają toobe część każdego profilu.

![Przykład filtrowania wersji][renditions2]

W hello poniższy przykład kodera było używane tooencode zasób mezzanine do siedmiu ISO MP4s wersji wideo (od too1080p 180p). Hello zakodowanym elementem zawartości można dynamicznie umieszczone w każdym hello następujących protokołów: MPEG DASH, HLS i Smooth.  U góry hello hello diagramu, jest wyświetlany hello HLS manifestu dla zasobu hello bez filtrów (zawiera wszystkie wersje siedem).  W lewym dolnym hello HLS manifestu toowhich zastosowaniu filtru o nazwie "ott" hello jest wyświetlana. Filtr "ott" Hello określa tooremove wszystkie szybkości transmisji bitów poniżej 1 MB/s, co spowodowało hello dolnej dwa poziomy jakości trwa odłączany hello odpowiedzi.  W prawej, dolnej hello hello HLS toowhich manifestu, zastosowaniu filtru o nazwie "przenośnych" jest wyświetlana. Filtr "przenośnych" Hello określa wersje tooremove gdzie hello rozpoznawania jest większy niż 720p, co spowodowało Witaj dwie wersje 1080p jest odłączony.

![Filtrowanie wersji][renditions1]

## <a name="removing-language-tracks"></a>Usuwanie wersji językowych
Zasobów może zawierać wiele języków audio, takie jak angielski, hiszpański, francuski,... itd. Zwykle menedżerów Player SDK hello ścieżki audio wybór domyślny i śledzi audio dostępne dla określonego użytkownika. Utrudnione jest toodevelop takich zestawów SDK Player, wymaga różnych implementacji między struktur odtwarzaczy specyficzne dla urządzenia. Ponadto na niektórych platformach interfejsów API Player są ograniczone i nie dołączaj funkcji wyboru audio, gdzie użytkownicy nie mogą wybierz ani zmienić ścieżkę audio hello domyślne. Za pomocą filtrów zasobów można kontrolować zachowanie hello tworząc filtry, które obejmują tylko żądane języki audio.

![Filtrowanie wersji językowych][language_filter]

## <a name="trimming-start-of-an-asset"></a>Przycinanie początkowy środka trwałego
W większości wydarzeń transmisji strumieniowej na żywo Operatorzy uruchomić niektórych testów przed hello rzeczywistego zdarzenia. Na przykład może obejmować łupków takie przed rozpoczęciem powitalne zdarzenia hello: "Program rozpocznie się na chwilę". Jeśli archiwizacji hello program testu hello łupków danych również są archiwizowane i mają być uwzględnieni w hello prezentacji. Jednak te informacje należy nie można wyświetlić toohello klientów. Z dynamicznego manifestu można utworzyć filtr czasu rozpoczęcia i usuwanie danych hello niechciane z manifestu hello.

![Przycinanie start][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Tworzenie podrzędnego klipów (widoki) z archiwum na żywo
Wiele wydarzeń na żywo są długotrwałe i na żywo archiwum może obejmować wiele zdarzeń. Po nadawców zakończenia zdarzenia na żywo hello może być toobreak się hello do logicznego program będzie uruchamiany na żywo archiwum i Zatrzymaj sekwencji. Następnie opublikować te programy wirtualnego oddzielnie bez post przetwarzania hello archiwum na żywo i nie są tworzone oddzielne zasobów (nie otrzyma korzyści z istniejącej pamięci podręcznej fragmentów hello w hello CDN). Przykładami takich wirtualnego programów (podrzędne klipy) są kwartałów hello football lub koszykówki grę, innings hello w baseball lub pojedynczych zdarzeń popołudnie Olimpiada program.

Z manifestu dynamicznej można tworzyć filtry przy użyciu godziny rozpoczęcia i zakończenia i tworzyć widoki wirtualnych za pośrednictwem hello początku archiwum na żywo. 

![Filtr subclip][subclip_filter]

Filtrowane zasobów:

![Nart][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Dostosowywanie okna prezentacji (DVR)
Obecnie usługi Azure Media Services udostępnia archiwum cykliczne, których czas trwania hello można skonfigurować między 5 minut - 25 godzin. Filtrowanie manifestu można używane toocreate stopniowego okna DVR przez hello początku archiwum hello, bez usuwania nośnika. Istnieje wiele scenariuszy, w którym nadawców mają tooprovide ograniczone okna DVR, które przenoszona razem z hello edge na żywo i na powitania jednocześnie zachować większy okien archiwizacji. Nadawca może być toouse hello dane, które są poza hello DVR okna toohighlight klipy he\she może tooprovide różnych DVR system windows lub dla różnych urządzeń. Na przykład większość hello urządzenia przenośne nie obsługują big DVR systemu windows (dla klientów pulpitu może mieć okno DVR 2 minuty dla urządzeń przenośnych i 1 godzina).

![Okno DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Dopasowywanie LiveBackoff (pozycji na żywo)
Filtrowanie manifestu mogą być używane tooremove kilka sekund od hello na żywo krawędzi program na żywo. Dzięki temu nadawców prezentacji hello toowatch hello Podgląd publikacji punktu i utworzyć anons punkty wstawienia przed podglądy hello odbierania hello strumienia (zazwyczaj kopii — wyłączone przez 30 sekund). Nadawców można następnie Wypchnij tych platform klienta tootheir anonsów w czasie ich tooreceived i procesu informacje hello przed hello anonsu możliwości.

Oprócz obsługi toohello anonsu, LiveBackoff może służyć do dostosowania pozycji na żywo pobierania klienta tak, kiedy klienci rozchodzenia i trafień hello edge na żywo z serwera zamiast występują błędy HTTP 404 lub 412 fragmenty nadal może uzyskać.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Łączenie wielu reguł w jeden filtr
Można połączyć wiele reguł filtrowania w jeden filtr. Na przykład można zdefiniować zakres reguły tooremove łupków z archiwum na żywo i także filtrować dostępne szybkości transmisji bitów. Dla wielu end hello reguły filtrowania wyników jest kompozycją hello (tylko część wspólną) tych zasad.

![wiele reguł][multiple-rules]

## <a name="create-filters-programmatically"></a>Programowe tworzenie filtrów
powitania po temacie omówiono jednostki usługi Media Services, które są powiązane toofilters. Hello temacie przedstawiono również sposób tooprogrammatically tworzenie filtrów.  

[Tworzenie filtrów z interfejsów API REST](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Łączenie wielu filtrów (filtru kompozycji)
Można także połączyć wiele filtrów w jeden adres URL. 

Witaj następujący scenariusz przedstawiono Dlaczego warto toocombine filtrów:

1. Należy toofilter Twojego jakości wideo dla urządzeń przenośnych, takich jak Android i iPAD (w kolejności toolimit jakości wideo). tooremove hello niechciane właściwości, należy utworzyć filtr globalny, który jest odpowiedni dla profilów urządzeń. Jak wspomniano powyżej, można filtry globalne dla wszystkich zasobów w obszarze hello konto bez żadnych dalszych skojarzenia usług tego samego nośnika. 
2. Również mają tootrim hello rozpoczęcia i zakończenia czasu zasobu. tooachieve to, czy utworzyć filtr lokalnych i ustawić czas rozpoczęcia i zakończenia hello. 
3. Ma toocombine obu tych filtrów (bez kombinacja będzie potrzebny tooadd jakości filtrowania toohello przycinanie filtr, co spowoduje, że użycie filtru trudne).

filtry toocombine należy tooset hello filtr nazw toohello manifest/odtwarzania adres URL z rozdzielanych średnikami. Załóżmy, że masz filtru o nazwie *MyMobileDevice* który filtry właściwości i inny o nazwie *MyStartTime* tooset określony czas rozpoczęcia. Można je połączyć następująco:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Możesz łączyć too3 filtrów. 

Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.

## <a name="know-issues-and-limitations"></a>Wiedzieć, problemy i ograniczenia
* Dynamiczne manifest działa w GOP granic (klucz ramki), dlatego przycinanie ma GOP dokładności. 
* Można użyć tej samej nazwy filtru dla lokalne i globalne filtry. Należy pamiętać, że filtr lokalny mają wyższy priorytet i zastąpi filtrów globalnych.
* Po zaktualizowaniu filtru może potrwać too2 minut do przesyłania strumieniowego punktu końcowego toorefresh hello reguły. Jeśli zawartość hello zostało obsłużone przy użyciu niektóre filtry (i w pamięci podręcznej serwerów proxy i sieci CDN pamięci podręcznych), aktualizowanie tych filtrów może powodować błędy player. Jest zalecane tooclear hello w pamięci podręcznej po zaktualizowaniu hello filtru. Jeśli ta opcja nie jest możliwe, należy rozważyć użycie inny filtr.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Dostarczanie zawartości tooCustomers — omówienie](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
