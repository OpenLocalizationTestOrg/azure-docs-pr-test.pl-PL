---
title: "Korzystanie z usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumieni strumieniowych aaaLive | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób tooset kanału, który odbiera pojedynczej szybkości transmisji bitów na żywo strumienia z kodera lokalnie, a następnie wykonuje strumień na żywo kodowania tooadaptive szybkości transmisji bitów z usługi Media Services. Hello strumienia mogą następnie zostać dostarczone tooclient odtwarzanie aplikacji za pośrednictwem jednego lub więcej punkty końcowe przesyłania strumieniowego, przy użyciu jednej z powitania po protokołów przesyłania strumieniowego z adaptacyjną: HLS, Smooth Stream, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Transmisja strumieniowa przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie na żywo
## <a name="overview"></a>Omówienie
W konsoli usługi Azure Media Services (AMS) **kanału** reprezentuje potok przetwarzania zawartości transmisji strumieniowej na żywo. A **kanału** odbiera na żywo wejściowych strumieni w jeden z dwóch sposobów:

* Na lokalny koder na żywo wysyła o pojedynczej szybkości transmisji bitów toohello kanału, który jest włączone tooperform live encoding w usłudze Media Services w jednym z następujących formatów hello: RTP (MPEG-TS), protokołu RTMP lub Smooth Streaming (pofragmentowany MP4). Witaj kanał wykonuje następnie kodowanie na żywo przychodzącego hello pojedynczej szybkości transmisji bitów strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej) strumienia wideo. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.
* Na lokalny koder na żywo wysyła różnych szybkościach transmisji bitów **RTMP** lub **Smooth Streaming** kanału toohello (pofragmentowany MP4), który nie jest włączone tooperform na żywo, kodowanie przy użyciu usługi AMS. Witaj pozyskanych strumienie są przekazywane za pośrednictwem **kanału**s bez dalszego przetwarzania. Ta metoda jest wywoływana **przekazywanego**. Można użyć następujących koderów na żywo, które udostępniają wielokrotnej szybkości transmisji bitów Smooth Streaming hello: MediaExcel, Ateme, Wyobraź sobie komunikacji, Envivio, Cisco i Elemental. Witaj następujące kodery na żywo wysyłają pliki RTMP: Adobe Flash Media na żywo kodera (FMLE), Telestream Wirecast, Haivision, Teradek i Tricaster koderów.  Koder na żywo może także wysłać pojedynczej szybkości transmisji bitów strumienia tooa kanał nie jest włączona kodowanie na żywo, ale nie jest zalecane. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.
  
  > [!NOTE]
  > Metoda przekazywania jest najbardziej ekonomiczne rozwiązanie hello toodo transmisji strumieniowej na żywo.
  > 
  > 

Począwszy od hello Media Services 2.10 wersji, podczas tworzenia kanału, możesz określić, w jaki sposób chcesz strumienia wejściowego hello tooreceive kanału i czy ma hello tooperform kanału na żywo kodowanie strumienia. Dostępne są dwie opcje:

* **Brak** — podać tę wartość, jeśli planujesz toouse na lokalny koder na żywo, którego dane wyjściowe obejmują wielokrotnej szybkości transmisji bitów stream (strumień przekazującego). W takim przypadku strumienia przychodzącego hello przekazywane toohello output bez żadnych kodowania. Jest to zachowanie hello kanału too2.10 wcześniejszych wersji.  Aby uzyskać szczegółowe informacje na temat pracy z kanałami tego typu, zobacz [transmisję strumieniową na żywo za pomocą koderów lokalnych, które tworzą strumienie o różnych szybkościach transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).
* **Standardowe** — wybierz tę wartość, jeśli planujesz tooencode Media Services toouse strumienia szybkości transmisji bitów toomulti strumień na żywo o pojedynczej szybkości transmisji bitów. Należy pamiętać, że rozliczeń wpływa kodowanie na żywo i należy pamiętać, że pozostawienie kanał kodowania na żywo w stanie "Uruchomiona" hello spowoduje naliczenie opłaty rozliczeń.  Zaleca się natychmiast zatrzymać uruchomione kanałów po zdarzenia transmisji strumieniowej na żywo jest pełną tooavoid opłat bardzo co godzinę.

> [!NOTE]
> W tym temacie omówiono atrybuty kanałami obsługującymi kodowanie na żywo tooperform (**standardowe** typ kodowania). Aby uzyskać informacje na temat pracy z kanałami, które nie są włączone, tooperform kodowanie na żywo, zobacz [transmisję strumieniową na żywo za pomocą koderów lokalnych, które tworzą strumienie o różnych szybkościach transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).
> 
> Upewnij się, że hello tooreview [zagadnienia](media-services-manage-live-encoder-enabled-channels.md#Considerations) sekcji.
> 
> 

## <a name="billing-implications"></a>Implikacje rozliczeń
Kanał kodowania na żywo rozpoczyna rozliczeń zaraz po jego stan przejścia zbyt "uruchomiona" za pośrednictwem hello interfejsu API.   Można również wyświetlić stan hello w hello portalu Azure lub w narzędziu Azure Media Services Explorer hello (http://aka.ms/amse).

Witaj poniższej tabeli przedstawiono sposób stanów kanału mapowania stanów toobilling w hello interfejsu API i portalu Azure. Należy zauważyć, że stanów hello różni się między hello interfejsu API i Portal UX. Jak najszybciej kanał jest w stanie "Uruchomiona" do hello za pośrednictwem interfejsu API hello, lub w hello "Gotowe" lub "Przesyłania strumieniowego" stan w portalu Azure hello rozliczeń będzie aktywny.
Kanał hello toostop z rozliczeniami można dodatkowo, masz tooStop hello kanału za pomocą interfejsu API hello lub hello portalu Azure.
Jest odpowiedzialny za zatrzymywanie kanałów po zakończeniu hello kanału kodowania na żywo.  Błąd toostop kanał kodowania spowoduje dalsze rozliczeń.

### <a id="states"></a>Stany kanału oraz sposobu mapowania ich toohello tryb rozliczeń
bieżący stan Hello kanału. Możliwe wartości obejmują:

* **Zatrzymano**. Jest to hello początkowy stan hello kanału po jego utworzeniu (chyba że automatyczne uruchamianie zostało wybrane w portalu hello). Karta nie występuje w tym stanie. W tym stanie można zaktualizować właściwości kanału hello, ale przesyłania strumieniowego nie jest dozwolone.
* **Uruchamianie**. Kanał Hello jest uruchamiana. Karta nie występuje w tym stanie. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa. Jeśli wystąpi błąd, hello kanału zwraca toohello zatrzymana.
* **Uruchomiona**. Witaj kanał jest w stanie przetwarzania strumieni na żywo. Jest on teraz rozliczeń użycia. Musisz zatrzymać tooprevent kanału hello dalsze rozliczeń. 
* **Zatrzymywanie**. Kanał Hello jest zatrzymywana. Karta nie występuje w tym stan przejściowy. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.
* **Usuwanie**. Kanał Hello jest usuwany. Karta nie występuje w tym stan przejściowy. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.

Witaj poniższej tabeli przedstawiono sposób kanału stany trybu rozliczeń toohello mapy. 

| Stan kanału | Wskaźniki w interfejsie użytkownika portalu | Jest to karta? |
| --- | --- | --- |
| Uruchamianie |Uruchamianie |Nie (stan przejściowy) |
| Działanie |Gotowy (brak uruchomionych programów)<br/>lub<br/>Transmisja strumieniowa (co najmniej jeden uruchomiony program) |TAK |
| Zatrzymywanie |Zatrzymywanie |Nie (stan przejściowy) |
| Zatrzymane |Zatrzymane |Nie |

### <a name="automatic-shut-off-for-unused-channels"></a>Automatyczne wyłączania nieużywanych kanałów
Począwszy od 25 stycznia 2016 Media Services wprowadzanie aktualizacji, która automatycznie zatrzyma kanał (kodowanie na żywo włączone) po jego działaniu w stanie nieużywane przez dłuższy okres. Dotyczy to tooChannels, która nie ma żadnych aktywnych programów i nie uzyskały wejściowych wkład źródła danych przez dłuższy czas.

Próg Hello na okres nieużywane nominalnie jest 12 godzin, ale jest toochange podmiotu.

## <a name="live-encoding-workflow"></a>Przepływ pracy kodowania na żywo
Witaj Poniższy diagram przedstawia na żywo przepływ pracy transmisji strumieniowej, gdzie kanał odbiera strumień o pojedynczej szybkości transmisji bitów w jednym z hello następujące protokoły: RTMP, Smooth Streaming lub RTP (MPEG-TS); koduje go następnie hello strumienia tooa wielokrotnej szybkości transmisji bitów strumienia. 

![Przepływ pracy na żywo][live-overview]

## <a id="scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo
Witaj poniżej przedstawiono ogólne etapy tworzenia typowych aplikacji transmisji strumieniowej na żywo.

> [!NOTE]
> Obecnie hello maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin. Skontaktuj się pod adresem amslived@Microsoft.com, jeśli potrzebujesz toorun kanał na dłuższe okresy. Należy pamiętać, że ma rozliczeń wpływu kodowanie na żywo i należy pamiętać, że pozostawienie kanał kodowania na żywo w stanie "Uruchomiona" hello będą naliczane co godzinę opłat rozliczeń.  Zaleca się natychmiast zatrzymać uruchomione kanałów po zdarzenia transmisji strumieniowej na żywo jest pełną tooavoid opłat bardzo co godzinę. 
> 
> 

1. Połącz komputer tooa kamerę wideo. Uruchom i skonfiguruj na lokalny koder na żywo, który wysyła strumień **pojedynczego** szybkości transmisji bitów w jednym z hello następujących protokołów: RTMP, Smooth Streaming lub RTP (MPEG-TS). 
   
    Ten krok można również wykonać po utworzeniu kanału.
2. Utwórz i uruchom kanał. 
3. Adres URL pozyskiwania, Pobierz hello kanału. 
   
    adres URL pozyskiwania Hello jest używany przez hello kodera na żywo toosend hello strumienia toohello kanału.
4. Pobiera adres URL podglądu kanału hello. 
   
    Użyj tego adresu URL tooverify, czy kanał prawidłowo odbiera strumień na żywo hello.
5. Utwórz program. 
   
    Przy użyciu hello portalu Azure, tworzenia program tworzy także zasób. 
   
    Podczas korzystania z zestawu .NET SDK lub REST muszą toocreate zasób i określ ten zasób toouse podczas tworzenia programu. 
6. Publikowanie zawartości hello skojarzony z programem hello.   
   
    >[!NOTE]
    >Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. Witaj, z którego mają zostać toostream zawartości punktu końcowego przesyłania strumieniowego ma toobe w hello **systemem** stanu. 
    
7. Uruchom hello program, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji.
8. Opcjonalnie hello kodera na żywo może być sygnałowego toostart anonsu. Witaj reklama jest wstawiana hello strumienia wyjściowego.
9. Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.
10. Usuń hello Program (i opcjonalnie można również usunąć hello zasobów).   

> [!NOTE]
> Bardzo ważne jest, nie tooforget tooStop kanału kodowanie na żywo. Należy pamiętać, że istnieje co godzinę rozliczeń wpływ kodowanie na żywo i należy pamiętać, że pozostawienie kanał kodowania na żywo w stanie "Uruchomiona" hello spowoduje naliczenie opłaty rozliczeń.  Zaleca się natychmiast zatrzymać uruchomione kanałów po zdarzenia transmisji strumieniowej na żywo jest pełną tooavoid opłat bardzo co godzinę. 
> 
> 

## <a id="channel"></a>Kanał danych wejściowych (pozyskiwania) konfiguracji
### <a id="Ingest_Protocols"></a>Pozyskiwania protokołu przesyłania strumieniowego
Jeśli hello **typu kodera** ustawiono zbyt**standardowe**, prawidłowe opcje to:

* **RTP** (MPEG-TS): strumień transportu MPEG-2 przy użyciu protokołu RTP.  
* Pojedynczej szybkości transmisji bitów **RTMP**
* Pojedynczej szybkości transmisji bitów **pofragmentowany MP4** (Smooth Streaming)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) - strumień transportu MPEG-2 przy użyciu protokołu RTP.
Typowy przypadek użycia: 

Professional nadawców zwykle współdziałają z koderów na żywo lokalny wysokiej klasy od dostawców, takich jak toosend stanie wolnym technologii Ericsson, Ateme imprezie Imagine albo Envivio strumienia. Często używane w połączeniu z działu informatycznego i sieciach prywatnych.

Kwestie do rozważenia:

* Zdecydowanie zalecane jest użycie Hello strumień transportowy jednego programu (SPTS) danych wejściowych. 
* Można wprowadzić się too8 strumieni audio przy użyciu usług terminalowych MPEG-2 przy użyciu protokołu RTP. 
* strumienia wideo o Hello powinny mieć średniej szybkości transmisji bitów poniżej 15 MB/s
* Hello agregacji średniej szybkości transmisji bitów strumieni audio hello powinno być niższe niż 1 MB/s
* Poniżej są hello koderów-dekoderów obsługiwanych:
  
  * MPEG-2 / H.262 wideo 
    
    * Główny profil (4:2:0)
    * Profil wysokiej (4:2:0, 4:2:2)
    * Profil 422 (4:2:0, 4:2:2)
  * MPEG-4 AVC / wideo H.264  
    
    * Linii bazowej, Main, wysokiej profilu (8-bitową 4:2:0)
    * Wysoka profilu 10 (10-bitowy 4:2:0)
    * Wysoka 422 profilu (10-bitowy 4:2:2)
  * Audio AAC-LC MPEG-2 
    
    * Mono, Stereo, przestrzennego (5.1, 7.1)
    * OPAKOWYWANIE ADTS styl MPEG-2
  * Dolby Audio cyfrowy (AC-3) 
    
    * Mono, Stereo, przestrzennego (5.1, 7.1)
  * MPEG Audio (warstwy II i III) 
    
    * Mono, Stereo
* Zalecane emisji koderów to:
  
  * Wyobraź sobie ENC Selenio komunikacji 1
  * Wyobraź sobie ENC Selenio komunikacji 2
  * Elemental na żywo

#### <a id="single_bitrate_RTMP"></a>Pojedyncza szybkość transmisji bitów RTMP
Kwestie do rozważenia:

* strumień przychodzący Hello nie może zawierać wideo o różnych szybkościach transmisji bitów
* strumienia wideo o Hello powinny mieć średniej szybkości transmisji bitów poniżej 15 MB/s
* strumień audio Hello powinny mieć średniej szybkości transmisji bitów poniżej 1 MB/s
* Poniżej są hello koderów-dekoderów obsługiwanych:
* MPEG-4 AVC / wideo H.264
* Linii bazowej, Main, wysokiej profilu (8-bitową 4:2:0)
* Wysoka profilu 10 (10-bitowy 4:2:0)
* Wysoka 422 profilu (10-bitowy 4:2:2)
* Audio AAC-LC MPEG-2
* Mono, Stereo, przestrzennego (5.1, 7.1)
* częstotliwość próbkowania 44,1 kHz
* OPAKOWYWANIE ADTS styl MPEG-2
* Następujące kodery zalecane:
* Telestream Wirecast
* Koder na żywo Flash nośnika

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>Pojedyncza szybkość transmisji bitów podzielonej zawartości w formacie MP4 (Smooth Streaming)
Typowy przypadek użycia:

Wykorzystanie lokalnych koderów na żywo z dostawców takich jak stanie wolnym technologii Ericsson Ateme, strumień wejściowy hello toosend Envivio za pośrednictwem hello Otwórz internet tooa w pobliżu centrum danych Azure.

Kwestie do rozważenia:

Sam jak w przypadku [pojedyncza szybkość transmisji bitów RTMP](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Inne zagadnienia
* Nie można zmienić hello protokołu wejściowego, gdy hello kanał lub skojarzone z nim programy są uruchomione. Jeśli potrzebujesz różnych protokołów, utwórz osobny kanał dla każdego protokołu wejściowego.
* Maksymalna rozdzielczość dla przychodzących strumienia wideo hello wynosi 1920 x 1080 pikseli i co najwyżej 60 pola/sekundę Jeśli naprzemiennych lub 30 klatek na sekundę Jeśli progresywnego.

### <a name="ingest-urls-endpoints"></a>Pozyskiwania adresów URL (punkty końcowe)
Kanał zawiera ono wejściowy punkt końcowy (adres URL pozyskiwania) określenie w hello kodera na żywo, więc wypchnąć kodera hello strumieni tooyour kanałów.

Możesz uzyskać hello adresy URL pozyskiwania, po utworzeniu kanału. tooget tych adresów URL hello kanału nie ma toobe w hello **systemem** stanu. Gdy wszystko jest gotowe toostart przekazywanie danych do hello kanału, który musi być w hello **systemem** stanu. Po uruchomieniu kanału hello wprowadzania danych można wyświetlić podgląd strumienia za pośrednictwem hello URL podglądu.

Istnieje opcja wprowadzania pofragmentowany MP4 (Smooth Streaming) strumień na żywo za pośrednictwem połączenia SSL. tooingest za pośrednictwem protokołu SSL, upewnij się, że hello tooupdate pozyskiwania tooHTTPS adres URL. Należy zauważyć, że obecnie AMS nie obsługuje protokołu SSL z domen niestandardowych.  

### <a name="allowed-ip-addresses"></a>Dozwolonych adresów IP
Można zdefiniować hello adresy IP, które są dozwolone toopublish toothis wideo kanału. Dozwolone adresy IP można określić jako pojedynczy adres IP (np. „10.0.0.1”), zakres adresów IP przy użyciu adresu IP i maski podsieci CIDR (np. „10.0.0.1/22”) lub zakres adresów IP przy użyciu adresu IP i maski podsieci w zapisie kropkowo-cyfrowym (np. „10.0.0.1(255.255.252.0)”).

Jeśli adresy IP nie zostaną określone i brakuje definicji reguły, to żaden adres IP nie będzie dozwolony. tooallow dowolnego adresu IP, Utwórz regułę i ustaw wartość 0.0.0.0/0.

## <a name="channel-preview"></a>Podgląd kanału
### <a name="preview-urls"></a>Adresy URL w wersji zapoznawczej
Kanały zapewniają punktu końcowego podglądu (adres URL w wersji zapoznawczej) Użyj toopreview, a następnie sprawdź strumienia, zanim dalszego przetwarzania i dostarczania.

Po utworzeniu kanału hello można uzyskać adres URL podglądu hello. adres URL hello tooget, hello kanału nie ma toobe w hello **systemem** stanu.

Po uruchomieniu kanału hello wprowadzania danych można wyświetlić podgląd strumienia.

> [!NOTE]
> Obecnie hello podglądu strumienia tylko mogą być dostarczane w pofragmentowany MP4 (Smooth Streaming) format niezależnie od hello określony typ danych wejściowych. Można użyć hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest hello Smooth Stream. Można również użyć odtwarzacza hostowanych w hello Azure tooview portalu strumienia.
> 
> 

### <a name="allowed-ip-addresses"></a>Dozwolone adresy IP
Można zdefiniować adresy IP hello, które są dozwolone punktu końcowego podglądu toohello tooconnect. Jeśli nie zawiera adresów IP nie zostaną określone może być dowolny adres IP. Dozwolone adresy IP można określić jako pojedynczy adres IP (np. „10.0.0.1”), zakres adresów IP przy użyciu adresu IP i maski podsieci CIDR (np. „10.0.0.1/22”) lub zakres adresów IP przy użyciu adresu IP i maski podsieci w zapisie kropkowo-cyfrowym (np. „10.0.0.1(255.255.252.0)”).

## <a name="live-encoding-settings"></a>Ustawienia kodowania na żywo
W tej sekcji opisano, jak można hello ustawienia hello kodera na żywo w ramach hello kanału dostosowana, gdy hello **typu kodowania** kanału ustawiono zbyt**standardowe**.

> [!NOTE]
> Gdy wprowadzanie wielu wersji językowych i wykonywania, kodowanie na żywo przy użyciu platformy Azure, tylko RTP jest obsługiwane dla wielu języków w danych wejściowych. Można zdefiniować się too8 strumieni audio przy użyciu usług terminalowych MPEG-2 przy użyciu protokołu RTP. Wprowadzania wielu ścieżek audio RTMP lub Smooth streaming nie jest obecnie obsługiwane. Twoją kodowanie na żywo z [live lokalnymi koduje](media-services-live-streaming-with-onprem-encoders.md), jest nie takiego ograniczenia, ponieważ niezależnie od wysłaniu tooAMS przechodzi przez kanał bez dalszego przetwarzania.
> 
> 

### <a name="ad-marker-source"></a>Źródło znacznika usługi AD
Można określić hello źródło sygnałów znaczników reklamowych. Wartość domyślna to **interfejsu Api**, co oznacza tego hello kodera na żywo w ramach hello kanału będą wysyłane tooan asynchroniczne **interfejsu API znacznika reklamy**.

Witaj innych prawidłową opcją jest **Scte35** (dozwolone tylko wtedy, gdy pozyskiwania hello przesyłania strumieniowego protokołu ustawiono tooRTP (MPEG-TS). W przypadku Scte35 hello kodera na żywo będzie analizować sygnały SCTE 35 ze strumienia wejściowego RTP (MPEG-TS) hello.

### <a name="cea-708-closed-captions"></a>CEA 708 zamknięte podpisy
Opcjonalna Flaga, która informuje tooignore kodera na żywo hello żadnych danych podpisy CEA 708 osadzony w hello przychodzące wideo. Gdy hello flagę toofalse (ustawienie domyślne), koder hello wykryje i ponownie włóż CEA 708 danych do wideo strumienie wyjściowe hello.

### <a name="video-stream"></a>Strumienia wideo
Opcjonalny. W tym artykule opisano hello wejściowego strumienia wideo. Jeśli to pole nie zostanie określony, wartością domyślną hello jest używany. To ustawienie jest dozwolone tylko wtedy, gdy hello wejściowej protokołu przesyłania strumieniowego ustawiono tooRTP (MPEG-TS).

#### <a name="index"></a>Indeks
Liczony od zera indeks, który określa, które wejściowego strumienia wideo powinny być przetwarzane przez hello kodera na żywo w ramach hello kanału. To ustawienie ma zastosowanie tylko wtedy, gdy pozyskiwania przesyłania strumieniowego protokół jest RTP (MPEG-TS).

Wartość domyślna wynosi zero. Zalecane jest toosend w jednym programie strumień transportowy (SPTS). Jeśli hello strumień wejściowy zawiera wiele programów, hello kodera na żywo analizuje hello Program mapy tabeli (rata) w danych wejściowych hello identyfikuje hello danych wejściowych, które mają nazwę typu strumienia wideo MPEG-2 lub H.264 i rozmieszcza je w kolejności hello w hello konto liczony od zera indeks Hello jest następnie używany toopick hello n-ty percentyl wpis w takie rozwiązanie.

### <a name="audio-stream"></a>Strumień audio
Opcjonalny. W tym artykule opisano hello wejściowych strumieni audio. Jeśli to pole nie zostanie określony, mają zastosowanie określone wartości domyślne hello. To ustawienie jest dozwolone tylko wtedy, gdy hello wejściowej protokołu przesyłania strumieniowego ustawiono tooRTP (MPEG-TS).

#### <a name="index"></a>Indeks
Zalecane jest toosend w jednym programie strumień transportowy (SPTS). Jeśli hello strumień wejściowy zawiera wiele programów, hello kodera na żywo w ramach hello kanału analizuje hello Program mapy tabeli (rata) w danych wejściowych hello, który identyfikuje hello danych wejściowych, które mają nazwę typu strumienia ADTS AAC MPEG-2 lub AC-3, System A lub System AC 3-B lub prywatnej MPEG-2 PES lub Audio MPEG-1 lub Audio MPEG-2 i rozmieszcza je w kolejności hello w hello konto liczony od zera indeks Hello jest następnie używany toopick hello n-ty percentyl wpis w takie rozwiązanie.

#### <a name="language"></a>Język
Witaj identyfikator języka hello strumieniem audio, zgodnych tooISO 639-2, takich jak ENG. Jeśli nie istnieje domyślny hello jest i (niezdefiniowanej).

Można się too8 strumieniem audio określone zestawy kanału toohello dane wejściowe hello jest MPEG-2 TS przy użyciu protokołu RTP. Jednak może być brak dwóch wpisów z hello tę samą wartość indeksu.

### <a id="preset"></a>Ustawienie systemu
Określa, że hello ustawienia wstępnego toobe używane przez hello kodera na żywo w ramach tego kanału. Obecnie hello Jedyne dozwolone wartości to **Default720p** (ustawienie domyślne).

Należy pamiętać, że jeśli potrzebujesz predefiniowanych, należy skontaktować się pod adresem amslived@Microsoft.com.

**Default720p** będzie kodowanie wideo hello do powitania po warstwy 7.

#### <a name="output-video-stream"></a>Wideo strumienia wyjściowego.
| Szybkość transmisji bitów | Szerokość | Wysokość | MaxFPS | Profil | Nazwa strumienia wyjściowego |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Wysoka |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Main |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Main |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Main |Video_512x288_850kbps |
| 550 |384 |216 |30 |Main |Video_384x216_550kbps |
| 350 |340 |192 |30 |Linii bazowej |Video_340x192_350kbps |
| 200 |340 |192 |30 |Linii bazowej |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Audio strumienia wyjściowego.
Dźwięk jest zakodowany toostereo AAC-LC na 64 KB, współczynnik 44,1 kHz pobierania próbek.

## <a name="signaling-advertisements"></a>Reklamy sygnalizowania
Kanał ma Live Encoding włączone, ma składnika w Twojej potok, który ma przetwarzania obrazu, a można manipulować go. Może sygnalizować, dla typu tooinsert kanału hello i/lub anonsów do hello wychodzących adaptacyjnej szybkości transmisji bitów. Typu są nadal obrazów, w której w niektórych przypadkach można toocover się hello źródła danych na żywo wejściowych (na przykład podczas podziału komercyjnych). Anonsowanie sygnałów, są sygnały zsynchronizowany czas, który osadzić w hello wychodzących strumienia tootell hello odtwarzacza wideo tootake specjalnych działań — takie jak anons tooan tooswitch w czasie odpowiednie hello. Zobacz to [blogu](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) Omówienie mechanizmu sygnalizowania hello SCTE 35 do tego celu. Oto typowy scenariusz, które można zaimplementować w zdarzenia na żywo.

1. Ma widzów pobrać obrazu zdarzenie wstępne, przed rozpoczęciem powitalne zdarzeń.
2. Ma widzów Pobierz obraz po zdarzeń po zakończeniu hello zdarzeń.
3. Ma widzów Pobierz obraz zdarzenie błędu, jeśli występuje problem podczas zdarzenia hello (na przykład awarii zasilania w hello stadium).
4. Wyślij AD-BREAK obrazu toohide hello wydarzenia na żywo źródła danych podczas podziału komercyjnych.

Oto Hello hello właściwości, które można ustawić podczas reklamy sygnalizowania. 

### <a name="duration"></a>Czas trwania
Hello czas w sekundach hello komercyjnych podziału. Toobe to ma wartość dodatnią zera w kolejności toostart hello komercyjnych podziału. Podczas podziału komercyjnych jest w toku i czas trwania hello jest toozero zestawu z hello CueId pasującego hello w toku komercyjnych podziału anulowania tego podziału, a następnie.

### <a name="cueid"></a>CueId
Unikatowy identyfikator dla hello komercyjnych końca toobe używane przez akcje odpowiednie tootake aplikacji. Wymaga toobe dodatnią liczbą całkowitą. Można ustawić tej wartości tooany losowe dodatnią liczbą całkowitą lub użyć hello tootrack nadrzędnego systemu sygnalizacji identyfikatorów. Należy niektórych toonormalize liczb całkowitych wszystkie identyfikatory toopositive przed przesłaniem za pośrednictwem hello interfejsu API.

### <a name="show-slate"></a>Pokaż łupków
Opcjonalny. Sygnały hello kodera na żywo tooswitch toohello [domyślne łupków](media-services-manage-live-encoder-enabled-channels.md#default_slate) obrazu podczas podziału handlowych i Ukryj hello przychodzące źródła wideo. Podczas łupków również wyciszeniu dźwięku. Domyślnie jest **false**. 

Obraz powitania używany będzie hello określona za pomocą zasobów domyślne łupków hello właściwość identyfikatora w czasie hello hello tworzenia kanału. łupków Hello będzie rozciągany rozmiar obrazu wyświetlanego hello toofit. 

## <a name="insert-slate--images"></a>Wstawianie obrazów łupków
Witaj kodera na żywo w ramach hello kanału może być sygnałowego tooswitch tooa łupków obrazu. Można też sygnałowego tooend łupków w toku. 

Hello kodera na żywo można skonfigurowanego tooswitch tooa łupków obrazu i Ukryj hello przychodzącego sygnału wideo w niektórych sytuacjach — na przykład podczas podziału ad. Jeśli nie skonfigurowano takie łupków, wejściowy plik wideo nie jest maskowane podczas tego podziału ad.

### <a name="duration"></a>Czas trwania
czas Hello łupków hello w sekundach. Toobe to ma wartość dodatnią zera w kolejności toostart hello łupków. Jeśli istnieje łupków w toku, a czas trwania zero jest określony, że łupków w toku zostanie zakończona.

### <a name="insert-slate-on-ad-marker"></a>Wstaw planszę w miejscu znacznika reklamy
Gdy zestaw tootrue, to ustawienie konfiguruje hello kodera na żywo tooinsert obrazu łupków podczas podziału ad. Witaj wartość domyślna to true. 

### <a id="default_slate"></a>Identyfikator zasobu domyślny łupków

Opcjonalny. Określa identyfikator zasobu hello zasobów usługi nośnika, który zawiera obraz powitania łupków hello. Domyślna ma wartość null. 


>[!NOTE] 
>Przed utworzeniem hello kanału, hello łupków obrazu o hello następujące ograniczenia należy przesłać jako zasób dedykowanych (żadne inne pliki powinna być w tym zasobów). Ten obraz jest używana tylko podczas hello kodera na żywo jest wstawianie łupków powodu podziału ad tooan lub została jawnie sygnalizowane tooinsert łupków. Hello kodera na żywo można także przejść do trybu łupków podczas niektórych warunków błędów — na przykład jeśli sygnału wejściowego hello zostaną utracone. Nie ma obecnie nie toouse opcja niestandardowego obrazu po kodera na żywo hello przejściu takich "sygnału wejściowego utraty" stan. Dla tej funkcji, można głosować [tutaj](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Co najwyżej 1920 x 1080 pikseli rozdzielczość.
* Co najwyżej 3 (MB) rozmiar.
* Witaj, nazwa pliku musi mieć rozszerzenie *.jpg.
* Obraz powitania należy przekazać do elementu zawartości w formie powitalne AssetFile tylko w tym zasobów i AssetFile ten powinien być oznaczony jako plik podstawowy hello. Witaj zasobów nie może być szyfrowany w magazynie.

Jeśli hello **domyślne łupków identyfikator zasobu** nie zostanie określona, i **Wstaw łupków na znacznika ad** ustawiono zbyt**true**, domyślnego obrazu usługi Azure Media Services będą używane toohide hello danych wejściowych strumienia wideo. Podczas łupków również wyciszeniu dźwięku. 

## <a name="channels-programs"></a>Programy kanału
Kanał jest skojarzony z programami, które pozwalają toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają programami. Witaj relacja kanału i programu jest bardzo podobne nośnika tootraditional, gdzie kanał ma stały strumień zawartości, a program zdarzeń zakresie toosome upłynął, w tym kanale.

Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **okno archiwum** długości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin. Długość okna archiwum określa również dostępny hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Programy mogą być transmitowane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każdy program jest skojarzony z zasobem służący do przechowywania zawartości hello strumieniowo. Zasób jest kontenera obiektów blob bloku tooa mapowane na koncie magazynu Azure hello i pliki hello w hello zasobów są przechowywane jako obiekty BLOB w tym kontenerze. program hello toopublish tak klientów można wyświetlić strumienia hello należy utworzyć Lokalizator OnDemand dla hello skojarzonych zasobów. Lokalizator umożliwi toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree jednocześnie uruchomione programy, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami. Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast ostatnich 10 minut. tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy. Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Hello inny program jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.

Nie należy używać ponownie istniejących programów dla nowych zdarzeń. Zamiast tego należy utworzyć i uruchomić nowy program dla każdego zdarzenia, zgodnie z opisem w sekcji programowania aplikacji przesyłania strumieniowego na żywo hello.

Uruchom hello program, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji. Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello. 

toodelete zarchiwizowane zawartość, Zatrzymaj i Usuń hello program, a następnie usuń hello skojarzonego elementu zawartości. Nie można usunąć elementu zawartości, jeśli jest on używany przez program; Najpierw należy usunąć Hello program. 

Nawet po zatrzymaniu i usunięciu hello program, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte.

Jeśli chcesz zarchiwizować hello tooretain zawartości, ale nie jest dostępny do przesyłania strumieniowego, Usuń hello przesyłania strumieniowego lokalizatora.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Pobieranie miniatury podglądu źródła na żywo
Jeśli kodowanie na żywo jest włączona, teraz można uzyskać podgląd źródła danych na żywo hello jako osiągnie hello kanału. Może to być toocheck przydatnym narzędziem, czy Twoje źródło na żywo faktycznie wkrótce osiągnie hello kanału. 

## <a id="states"></a>Stany kanału oraz sposobu stanów mapowania toohello tryb rozliczeń
bieżący stan Hello kanału. Możliwe wartości obejmują:

* **Zatrzymano**. Jest to hello początkowy stan hello kanału po jego utworzeniu. W tym stanie można zaktualizować właściwości kanału hello, ale przesyłania strumieniowego nie jest dozwolone.
* **Uruchamianie**. Kanał Hello jest uruchamiana. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa. Jeśli wystąpi błąd, hello kanału zwraca toohello zatrzymana.
* **Uruchomiona**. Witaj kanał jest w stanie przetwarzania strumieni na żywo.
* **Zatrzymywanie**. Kanał Hello jest zatrzymywana. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.
* **Usuwanie**. Kanał Hello jest usuwany. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.

Witaj poniższej tabeli przedstawiono sposób kanału stany trybu rozliczeń toohello mapy. 

| Stan kanału | Wskaźniki w interfejsie użytkownika portalu | Naliczanie opłat? |
| --- | --- | --- |
| Uruchamianie |Uruchamianie |Nie (stan przejściowy) |
| Działanie |Gotowy (brak uruchomionych programów)<br/>lub<br/>Transmisja strumieniowa (co najmniej jeden uruchomiony program) |Tak |
| Zatrzymywanie |Zatrzymywanie |Nie (stan przejściowy) |
| Zatrzymane |Zatrzymane |Nie |

> [!NOTE]
> Obecnie hello kanału start średnia jest około 2 minuty, ale niekiedy może potrwać too20 + minut. Resetowanie kanału może potrwać too5 minut.
> 
> 

## <a id="Considerations"></a>Zagadnienia dotyczące
* Gdy kanałem **standardowe** typ kodowania napotyka utracie źródła danych wejściowych źródło/udział, jego kompensuje go przez zamianę audio/wideo źródła hello łupków błąd i wyciszenia. Hello kanału będzie tooemit łupków, dopóki nie wznawia strumieniowego źródła danych wejściowych hello swoim ważonym udziale. Zaleca się, że kanału na żywo nie należy pozostawiać w stanie przez czas dłuższy niż 2 godziny. Zachowanie hello hello kanału po ponownym nawiązaniu połączenia wejściowy nie jest gwarantowana poza ten punkt, nie jest jego zachowanie w odpowiedzi tooa polecenie resetowania. Zostanie toostop hello kanału, usuń ją i Utwórz nową.
* Nie można zmienić hello protokołu wejściowego, gdy hello kanał lub skojarzone z nim programy są uruchomione. Jeśli potrzebujesz różnych protokołów, utwórz osobny kanał dla każdego protokołu wejściowego.
* Za każdym razem, gdy skonfigurujesz hello kodera na żywo, wywołaj hello **zresetować** metody w kanale hello. Zanim je zresetujesz kanału hello masz toostop hello program. Po zresetowaniu hello kanału, uruchom ponownie hello program.
* Kanał można zatrzymać tylko wtedy, gdy jest w stanie uruchomiona hello i wszystkie programy na kanale hello zostały zatrzymane.
* Domyślnie można dodawać tylko 5 tooyour kanały konta usługi Media Services. Jest to przydziału elastycznego na wszystkich nowych kont. Aby uzyskać więcej informacji, zobacz [przydziały i ograniczenia](media-services-quotas-and-limitations.md).
* Nie można zmienić hello protokołu wejściowego, gdy hello kanał lub skojarzone z nim programy są uruchomione. Jeśli potrzebujesz różnych protokołów, utwórz osobny kanał dla każdego protokołu wejściowego.
* Rozliczenie jest przeprowadzane tylko gdy kanał hello **systemem** stanu. Aby uzyskać więcej informacji, zobacz zbyt[to](media-services-manage-live-encoder-enabled-channels.md#states) sekcji.
* Obecnie hello maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin. Skontaktuj się pod adresem amslived@Microsoft.com, jeśli potrzebujesz toorun kanał na dłuższe okresy.
* Upewnij się, że toohave hello punktu końcowego przesyłania strumieniowego, z którego ma zawartość toostream hello **systemem** stanu.
* Gdy wprowadzanie wielu wersji językowych i wykonywania, kodowanie na żywo przy użyciu platformy Azure, tylko RTP jest obsługiwane dla wielu języków w danych wejściowych. Można zdefiniować się too8 strumieni audio przy użyciu usług terminalowych MPEG-2 przy użyciu protokołu RTP. Wprowadzania wielu ścieżek audio RTMP lub Smooth streaming nie jest obecnie obsługiwane. Twoją kodowanie na żywo z [live lokalnymi koduje](media-services-live-streaming-with-onprem-encoders.md), jest nie takiego ograniczenia, ponieważ niezależnie od wysłaniu tooAMS przechodzi przez kanał bez dalszego przetwarzania.
* Witaj kodowanie predefiniowanych używa hello pojęcie "maksymalną szybkość" 30 klatek na sekundę. Jeśli więc hello wprowadzania 60 klatek na sekundę / 59.97i, klatek hello są porzucony/dezaktywuje-interlaced too30/29,97 kl. / s. Jeśli dane wejściowe hello jest 50 klatek na sekundę/50i, klatek hello są klatek na sekundę porzuconych/dezaktywuje-interlaced too25. Jeśli dane wejściowe hello jest 25 kl. / s, dane wyjściowe pozostaje w 25 kl. / s.
* Nie zapomnij tooSTOP YOUR kanały po zakończeniu. Jeśli nie, będą nadal rozliczeń.

## <a name="known-issues"></a>Znane problemy
* Udoskonalono czas uruchamiania kanału średnia tooan 2 minuty, ale w czasie zwiększone zapotrzebowanie, nadal może potrwać too20 + minut.
* Obsługa RTP jest stacji nadawanych kierunku nadawców professional. Zapoznaj się z tematem hello uwagi o RTP w [to](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blogu.
* Obrazy łupków powinna być zgodna toorestrictions opisane [tutaj](media-services-manage-live-encoder-enabled-channels.md#default_slate). Przy próbie utworzenia kanału z powodu błędu domyślna łupków, która jest większa niż 1920 x 1080 pikseli, hello żądanie zostanie wychodzących.
* Ponownie... nie zapomnij tooSTOP YOUR kanały, po zakończeniu przesyłania strumieniowego. Jeśli nie, będą nadal rozliczeń.

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Powiązane tematy
[Dostarczanie wydarzeń na żywo przesyłania strumieniowego w usłudze Azure Media Services](media-services-overview.md)

[Tworzenia kanałów wykonujących kodowanie na żywo z o wystąpieniu szybkości transmisji bitów tooadaptive szybkości transmisji bitów z portalu](media-services-portal-creating-live-encoder-enabled-channel.md)

[Tworzenia kanałów wykonujących kodowanie na żywo z o wystąpieniu szybkości transmisji bitów tooadaptive szybkości transmisji bitów przy użyciu zestawu .NET SDK](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Zarządzanie kanałami z interfejsu API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Pojęcia dotyczące usługi Media Services](media-services-concepts.md)

[Specyfikacja pozyskiwania MP4 pofragmentowane na żywo w usłudze Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

