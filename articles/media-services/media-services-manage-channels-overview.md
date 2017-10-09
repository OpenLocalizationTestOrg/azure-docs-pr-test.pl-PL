---
title: "aaaOverview z transmisji strumieniowej na żywo przy użyciu usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie transmisji strumieniowych na żywo przy użyciu usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Omówienie transmisji strumieniowej na żywo przy użyciu usługi Azure Media Services
## <a name="overview"></a>Omówienie
W celu dostarczenia na żywo strumienia zdarzeń w usłudze Azure Media Services hello następujące składniki są zwykle wymagane:

* Kamera, która jest używana toobroadcast zdarzenia.
* Koder wideo na żywo, który konwertuje sygnały z toostreams aparatu hello, które są wysyłane tooa usługi transmisji strumieniowej na żywo.

    Opcjonalnie wiele zsynchronizowanych czasowo koderów na żywo. Krytyczne dla niektórych wydarzeń na żywo czy wymagają bardzo wysokiej dostępności i jakości obsługi, zaleca się aktywny aktywny tooemploy nadmiarowych koderów z czas synchronizacji tooachieve płynnego trybu failover bez utraty danych.
* Na żywo usługi przesyłania strumieniowego umożliwiającej hello toodo następujące:

  * pozyskiwanie zawartości na żywo przy użyciu różnych protokołów transmisji strumieniowej na żywo (np. RTMP lub Smooth Streaming);
  * (opcjonalnie) kodowanie strumienia do strumienia o adaptacyjnej szybkości transmisji bitów;
  * wyświetlanie podglądu transmisji strumieniowej na żywo;
  * rekord i magazynu zawartości hello pozyskanych w kolejności toobe strumieniowo nowszej (wideo)
  * Dostarczanie zawartości hello za pośrednictwem wspólnych protokołów przesyłania strumieniowego (na przykład MPEG DASH, Smooth, HLS) bezpośrednio tooyour klientów lub tooa Content Delivery Network (CDN) w celu dalszej dystrybucji.

**Microsoft Azure Media Services** (AMS) zapewnia hello tooingest możliwości, kodowania, podglądu, przechowywania i dostarczania transmisji strumieniowej na żywo zawartość.

W celu dostarczenia Twojej zawartości toocustomers poznasz jest toodeliver wysokiej jakości wideo toovarious urządzeń bez względu na warunki panujące w sieci. tooachieve, użyj tooencode koderów na żywo strumienia wideo strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej szybkości transmisji bitów).  tootake nad przesyłania strumieniowego na różnych urządzeniach, użyj usługi Media Services [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md) toodynamically ponownego tworzenia pakietów z protokołów toodifferent strumienia. Usługa Media Services obsługuje dostarczanie hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

W usłudze Azure Media Services **kanałów**, **programy**, i **punkty końcowe** dojście wszystkich hello live streaming funkcje, w tym pozyskiwanie, formatowanie DVR, zabezpieczenia, skalowalność i nadmiarowość.

**Kanał** reprezentuje potok przetwarzania zawartości transmisji strumieniowej na żywo. Kanał może odbierać na żywo strumienie w hello następujące sposoby:

* Na lokalny koder na żywo wysyła wielokrotnej szybkości transmisji bitów **RTMP** lub **Smooth Streaming** (pofragmentowany plik MP4) toohello kanału, który jest skonfigurowany dla **przekazywanego** dostarczania. Witaj **przekazywanego** jest dostarczana, gdy hello pozyskanych strumienie są przekazywane za pośrednictwem **kanału**s bez dalszego przetwarzania. Można użyć następujących koderów na żywo, które udostępniają wielokrotnej szybkości transmisji bitów Smooth Streaming hello: MediaExcel, Ateme, Wyobraź sobie komunikacji, Envivio, Cisco i Elemental. Witaj następujące kodery na żywo wysyłają pliki RTMP: Adobe Flash Media na żywo kodera (FMLE), Telestream Wirecast, Haivision, Teradek i transkodery Tricaster.  Koder na żywo może także wysłać pojedynczej szybkości transmisji bitów strumienia tooa kanał nie jest włączona kodowanie na żywo, ale nie jest zalecane. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.

  > [!NOTE]
  > Metoda przekazywania to najbardziej ekonomiczne rozwiązanie hello toodo live przesyłania strumieniowego, gdy są organizowania wielu wydarzeń w długim okresie oraz poczynionych inwestycji w kodery lokalne. Zobacz szczegółowe informacje o [cenach](https://azure.microsoft.com/pricing/details/media-services/).
  > 
  > 
* Na lokalny koder na żywo wysyła o pojedynczej szybkości transmisji bitów toohello kanału, który jest włączone tooperform live encoding w usłudze Media Services w jednym z następujących formatów hello: RTMP lub Smooth Streaming (pofragmentowany MP4). RTP (MPEG-TS) jest również obsługiwany, pod warunkiem, że centrum danych Azure toohello dedykowanego połączenia. następujące kodery na żywo z RTMP Hello dane wyjściowe są znane toowork z kanałami tego typu: Telestream Wirecast, FMLE. Witaj kanał wykonuje następnie kodowanie na żywo przychodzącego hello pojedynczej szybkości transmisji bitów strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej) strumienia wideo. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.

Począwszy od hello Media Services 2.10 wersji, podczas tworzenia kanału, możesz określić, w jaki sposób chcesz strumienia wejściowego hello tooreceive kanału i czy ma hello tooperform kanału na żywo kodowanie strumienia. Dostępne są dwie opcje:

* **Brak** (przekazujących) — podać tę wartość, jeśli planujesz toouse na lokalny koder na żywo, którego dane wyjściowe obejmują wielokrotnej szybkości transmisji bitów stream (strumień przekazującego). W takim przypadku strumienia przychodzącego hello przekazywane toohello output bez żadnych kodowania. Jest to zachowanie hello kanału too2.10 wcześniejszych wersji.  
* **Standardowe** — wybierz tę wartość, jeśli planujesz tooencode Media Services toouse strumienia szybkości transmisji bitów toomulti strumień na żywo o pojedynczej szybkości transmisji bitów. Ta metoda jest bardziej ekonomiczne skalowania szybko rzadkim zdarzeń. Należy pamiętać, że rozliczeń wpływa kodowanie na żywo i należy pamiętać, że pozostawienie kanał kodowania na żywo w stanie "Uruchomiona" hello spowoduje naliczenie opłaty rozliczeń.  Zaleca się natychmiast zatrzymać uruchomione kanałów po zdarzenia transmisji strumieniowej na żywo jest pełną tooavoid opłat bardzo co godzinę.

## <a name="comparison-of-channel-types"></a>Porównanie typów kanałów
Poniższa tabela zawiera przewodnik toocomparing hello dwóch typów kanałów obsługiwane w usłudze Media Services

| Funkcja | Kanał przekazywania | Wzorzec kanał |
| --- | --- | --- |
| Dane wejściowe pojedynczej szybkości transmisji bitów jest kodowane do wielokrotnych szybkości transmisji bitów w chmurze hello |Nie |Tak |
| Rozdzielczość maksymalna, liczba warstw |1080p, 8 warstwy 60 + kl. / s |720p 6 warstwy 30 klatek na sekundę |
| Protokoły wejściowych |RTMP, Smooth Streaming |RTMP, Smooth Streaming i RTP |
| Cena |Zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/media-services/) i kliknij kartę "Wideo na żywo" |Zobacz hello [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/media-services/) |
| Maksymalny czas wykonywania |24 x 7 |8 godzin |
| Obsługa Wstawianie typu |Nie |Tak |
| Obsługa sygnalizowania ad |Nie |Tak |
| Podpisy CEA 608/708 przekazywania |Tak |Tak |
| Możliwość toorecover z krótki wstrzymania w udziale źródła danych |Tak |Nie (kanał rozpocznie slating sekund 6 + bez wprowadzania danych) |
| Obsługa niejednolitego GOPs wejściowych |Tak |Nie — dane wejściowe muszą być ustalone 2 s GOPs |
| Obsługa danych wejściowych szybkość zmiennej ramki |Tak |Nie — dane wejściowe muszą być ustalane szybkość klatek.<br/>Niewielkich zmian są dopuszczalne, na przykład podczas ruchu wysokiej sceny. Ale koder nie można porzucić too10 klatek na sekundę. |
| Auto bliskie kanałów podczas wprowadzania źródła danych zostaną utracone |Nie |Po 12 godzinach, jeśli żaden Program uruchomiony |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych (przekazujących)
Witaj Poniższy diagram przedstawia hello główne elementy platformy hello AMS, które są związane z hello **przekazywanego** przepływu pracy.

![Przepływ pracy na żywo](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Praca z kanałami, które są włączone tooperform live encoding w usłudze Azure Media Services
Witaj Poniższy diagram przedstawia hello główne elementy platformy AMS hello związanych z transmisji strumieniowej na żywo przepływu pracy gdzie kanał jest włączony tooperform live encoding w usłudze Media Services.

![Przepływ pracy na żywo](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Opis kanału i jej powiązane składniki
### <a name="channel"></a>Kanał
W usłudze Media Services [kanału](https://docs.microsoft.com/rest/api/media/operations/channel)s są zobowiązani do przetwarzania zawartości transmisji strumieniowej na żywo. Kanał zawiera ono wejściowy punkt końcowy (adres URL pozyskiwania) następnie podaj tooa transcoder na żywo. kanał Hello odbiera strumienie na żywo wejściowe z hello transcoder na żywo i udostępnia go do przesyłania strumieniowego za pośrednictwem jednego lub więcej punkty końcowe. Kanały udostępniają punktu końcowego podglądu (adres URL w wersji zapoznawczej) Użyj toopreview, a następnie sprawdź strumienia, zanim dalszego przetwarzania i dostarczania.

Możesz uzyskać hello pozyskiwania adresu URL i adresu URL w wersji zapoznawczej hello podczas tworzenia kanału hello. tooget tych adresów URL kanału hello nie ma toobe w stanie hello uruchomiona. Gdy wszystko jest gotowe toostart przekazywanie danych z transcoder na żywo do kanału hello, hello kanału musi być uruchomiona. Po uruchomieniu hello na żywo transcoder wprowadzania danych można wyświetlić podgląd strumienia.

Każde konto usługi Media Services może zawierać wiele kanałów, wiele programów i wielu punkty końcowe. W zależności od potrzeb przepustowości i zabezpieczeń hello StreamingEndpoint usługi może być dedykowany tooone lub więcej kanałów. Wszelkie StreamingEndpoint można ściąganie danych z dowolnego kanału.

### <a name="program"></a>Program
A [Program](https://docs.microsoft.com/rest/api/media/operations/program) pozwala toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają programami. Witaj relacja kanału i programu jest bardzo podobne nośnika tootraditional, gdzie kanał ma stały strumień zawartości, a program zdarzeń zakresie toosome upłynął, w tym kanale.
Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **ArchiveWindowLength** właściwości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin.

ArchiveWindowLength decyduje również hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Programy mogą być transmitowane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każdy program jest skojarzony z zasobem. program hello toopublish należy utworzyć Lokalizator dla hello skojarzonych zasobów. Lokalizator umożliwi toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree jednocześnie uruchomione programy, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami. Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast ostatnich 10 minut. tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy. Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Hello inny program jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.

## <a name="billing-implications"></a>Implikacje rozliczeń
Kanał rozpoczyna rozliczeń zaraz po jego stan przejścia zbyt "uruchomiona" za pośrednictwem hello interfejsu API.  

Witaj poniższej tabeli przedstawiono sposób stanów kanału mapowania stanów toobilling w hello interfejsu API i portalu Azure. Należy zauważyć, że stanów hello różni się między hello interfejsu API i Portal UX. Jak najszybciej kanał jest w stanie "Uruchomiona" do hello za pośrednictwem interfejsu API hello, lub w hello "Gotowe" lub "Przesyłania strumieniowego" stan w portalu Azure hello rozliczeń będzie aktywny.

Kanał hello toostop z rozliczeniami można dodatkowo, masz tooStop hello kanału za pomocą interfejsu API hello lub hello portalu Azure.
Jest odpowiedzialny za zatrzymywanie kanałów po zakończeniu hello kanału. Błąd toostop hello kanału spowoduje dalsze rozliczeń.

> [!NOTE]
> Podczas pracy z kanałami standardowe, AMS automatycznie bliskie żadnych kanału, który jest nadal w stanie "Uruchomiona" 12 godzin po hello wejściowych źródła strumieniowego zostaną utracone i nie ma żadnych programów uruchomiony. Jednak możesz będą nadal naliczane za powitalne czasu hello kanału był w stanie "Uruchomiona".
>
>

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

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Powiązane tematy
[Specyfikacja pozyskiwania MP4 pofragmentowane na żywo w usłudze Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)

[Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych](media-services-live-streaming-with-onprem-encoders.md)

[Przydziały i ograniczenia](media-services-quotas-and-limitations.md).  

[Pojęcia dotyczące usługi Media Services](media-services-concepts.md)
