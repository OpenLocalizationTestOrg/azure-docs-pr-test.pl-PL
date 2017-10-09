---
title: "aaaAzure Media Services na żywo pofragmentowane MP4 pozyskiwania specyfikacji | Dokumentacja firmy Microsoft"
description: "Określenie tej wartości opisano hello protokołu i format pofragmentowane na podstawie MP4 na żywo przesyłania strumieniowego wprowadzanie do usługi Azure Media Services. Można użyć usługi Azure Media Services toostream wydarzeń na żywo i emisji zawartości w czasie rzeczywistym za pomocą jako hello chmury platformy Azure. W tym dokumencie omówiono również najlepsze rozwiązania dotyczące tworzenia wysoce nadmiarowe i niezawodne na żywo pozyskiwania mechanizmów."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Specyfikacja pozyskiwania Azure Media Services MP4 pofragmentowane na żywo
Określenie tej wartości opisano hello protokołu i format pofragmentowane na podstawie MP4 na żywo przesyłania strumieniowego wprowadzanie do usługi Azure Media Services. Usługa Media Services udostępnia usługi transmisji strumieniowej na żywo klientów może używać toostream wydarzeń na żywo i emisji zawartości w czasie rzeczywistym za pomocą jako hello chmury platformy Azure. W tym dokumencie omówiono również najlepsze rozwiązania dotyczące tworzenia wysoce nadmiarowe i niezawodne na żywo pozyskiwania mechanizmów.

## <a name="1-conformance-notation"></a>1. Notacja zgodność
Hello słów kluczowych "musi," ",""Wymagane", "SHALL", "są nie może," "SHOULD", "Nie powinien," "Zalecane", "Może" i "OPTIONAL", w tym dokumencie są toobe interpretowany jako opisano w dokumencie RFC 2119.

## <a name="2-service-diagram"></a>2. Diagram usługi
Witaj Poniższy diagram przedstawia hello Architektura wysokiego poziomu hello na żywo, przesyłania strumieniowego usługi Media Services:

1. Koder na żywo wypycha toochannels źródeł danych na żywo, które są tworzone i udostępniane za pośrednictwem hello Azure Media Services SDK.
2. Kanały, programów i punktów końcowych przesyłania strumieniowego w dojścia usługi Media Services wszystkie hello live streaming funkcje, w tym pozyskiwanie, formatowanie, chmury DVR, zabezpieczenia, skalowalność i nadmiarowość.
3. Opcjonalnie klienci mogą wybrać toodeploy warstwa Azure Content Delivery Network między hello punktu końcowego i powitania klienta z punktów końcowych przesyłania strumieniowego.
4. Strumień punktów końcowych klienta z punktu końcowego przesyłania strumieniowego przy użyciu protokołów HTTP adaptacyjne przesyłanie strumieniowe hello. Przykładami Microsoft Smooth Streaming, dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH lub MPEG-DASH) i Apple HTTP Live Streaming (HLS).

![pozyskiwania przepływu][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Format Bitstream — ISO 14496 12 pofragmentowany plik MP4
Hello formatu podczas transmisji na żywo przesyłanie strumieniowe pozyskiwania omówione w tym dokumencie jest oparta na [ISO-14496-12]. Aby uzyskać szczegółowy opis pofragmentowane formacie MP4 i rozszerzeń zarówno dla plików wideo na żądanie i wprowadzanie transmisji strumieniowej na żywo, zobacz [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Na żywo pozyskiwania definicje formatu
Witaj Poniższa lista zawiera opis format specjalnych definicji, które są stosowane toolive pozyskiwania do usługi Azure Media Services:

1. Witaj **ftyp zawiera informacje**, **aktywne okno manifestu serwera**, i **moov** pola muszą być wysyłane z każdym żądaniem (HTTP POST). Te pola muszą być wysyłane na początku hello hello strumienia i pozyskiwania w dowolnym momencie kodera hello należy nawiązać ponownie połączenie tooresume strumienia. Aby uzyskać więcej informacji zobacz sekcja 6 w [1].
2. 3.3.2 części [1] określa opcjonalne pola o nazwie **StreamManifestBox** dla pozyskiwania na żywo. Powodu logiki routingu toohello usługi równoważenia obciążenia Azure hello przy użyciu tego pola jest przestarzały. pole Hello nie powinny znajdować się podczas wprowadzania do usługi Media Services. Jeśli to pole jest obecne, Media Services dyskretnie zignoruje ją.
3. Witaj **TrackFragmentExtendedHeaderBox** pola zdefiniowane w 3.2.3.2 [1] musi być obecny dla każdego fragmentu.
4. W wersji 2 hello **TrackFragmentExtendedHeaderBox** pole powinno być używane toogenerate nośnika segmentów, które mają identyczne adresów URL w wielu centrach danych. Witaj fragmentu indeksu pole jest wymagane w trybie failover między datacenter opartego na indeksie formatów przesyłania strumieniowego, takich jak Apple HLS i MPEG-DASH opartego na indeksie. tooenable centrum danych między przejścia w tryb failover hello fragmentu indeksu musi synchronizowane między wieloma koderów i zwiększyć o 1 dla każdego fragmentu nośnika kolejnych nawet przez koder ponownego uruchomienia lub w przypadku awarii.
5. Pole o nazwie definiuje 3.3.6 części [1] **MovieFragmentRandomAccessBox** (**mfra**) mogą być wysyłane na końcu hello na żywo wprowadzanie tooindicate zakończenia elementu strumienia (EOS) toohello kanału. Z powodu toohello pozyskiwania logiki usługi Media Services przy użyciu EOS jest przestarzałe i hello **mfra** polu dla wprowadzanie na żywo nie mają być wysyłane. Jeśli wysyłane, Media Services dyskretnie zignoruje ją. Stan hello tooreset hello pozyskiwania punktu, firma Microsoft zaleca użycie [Resetowanie kanału](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). Zalecamy również użycie [Zatrzymaj Program](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend prezentacji i strumienia.
6. czas trwania fragmentu Hello MP4 powinna być stała, rozmiar hello tooreduce hello manifesty na kliencie. Stałe czas trwania fragmentu MP4 także usprawnia heurystyki pobierania klienta przy użyciu hello powtarzania tagów. czas trwania Hello mogą ulegać zmianie toocompensate dla szybkości odtwarzania nie jest liczbą całkowitą.
7. czas trwania fragmentu Hello MP4 powinna wynosić około 2 do 6 w sekundach.
8. MP4 fragmentu sygnatury czasowe i indeksów (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` i `fragment_index`) powinna odbierane w kolejności rosnącej. Chociaż usługi Media Services jest odporność tooduplicate fragmenty, ograniczył fragmenty tooreorder możliwości zgodnie z toohello nośnika w osi czasu.

## <a name="4-protocol-format--http"></a>4. Format protokołu — HTTP
ISO fragmentacji na podstawie MP4 na żywo pozyskiwania dla usługi Media Services używa standardowych długotrwałe POST protokołu HTTP żądania tootransmit zakodowane nośnika danych spakowanego pofragmentowane usługi toohello formacie MP4. Każdy HTTP POST wysyła kompletna pofragmentowany bitstream MP4 ("strumień"), zaczynając od początku hello z pola nagłówka (**ftyp zawiera informacje**, **aktywne okno manifestu serwera**, i **moov** pola) i kontynuowanie sekwencję fragmenty (**moof** i **mdat** pól). Aby składni adresu URL dla żądania HTTP POST hello zobacz sekcję 9.2 w [1]. Przykład Witaj adresu URL przesyłania to: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Wymagania
Poniżej przedstawiono hello szczegółowe wymagania:

1. Witaj kodera powinien rozpocząć hello emisji, wysyłając żądanie HTTP POST z pustą "treść" (zerowej długości zawartości) przy użyciu hello samego wprowadzanie adresu URL. Może to ułatwić kodera hello szybko wykryć, czy punkt końcowy na żywo wprowadzanie hello jest prawidłowy, a jeśli ma żadnego uwierzytelniania lub inne warunki wymagane. Dla protokołu HTTP powitania serwera nie odesłania odpowiedzi HTTP do momentu hello całego, w tym treść wpisu hello, zostanie odebrane żądanie. Charakter długotrwałe hello wydarzenia na żywo bez tego kroku kodera hello może nie być toodetect stanie błędu do momentu zakończenia wszystkich danych hello wysyłania.
2. Koder Hello musi obsługiwać żadnych błędów lub wezwań do uwierzytelnienia z powodu (1). Jeśli (1) zakończy się pomyślnie z odpowiedzi 200, będzie kontynuowane.
3. Koder Hello musi rozpoczynać nowe żądanie HTTP POST hello pofragmentowany strumień MP4. ładunek Hello musi rozpoczynać się od pola nagłówka hello, następuje fragmenty. Należy pamiętać, że hello **ftyp zawiera informacje**, **aktywne okno manifestu serwera**, i **moov** pola (w podanej kolejności) muszą być wysyłane z każdym żądaniem, nawet jeśli koder hello należy nawiązać ponownie połączenie, ponieważ hello poprzednie żądanie zostało przerwane przed toohello koniec strumienia hello. 
4. Koder Hello musi używać przekazywania kodowanie transferu pakietowego, ponieważ jest niemożliwe toopredict hello całej zawartości długości hello na żywo zdarzeń.
5. Po zdarzeń hello umieszczeniu po wysłaniu hello ostatniego fragmentu, koder hello bezpiecznie musi kończyć się transfer hello fragmentaryczne Kodowanie komunikatu sekwencji (większość stosy klienta HTTP jego obsługa automatycznie). Koder Hello musi poczekaj hello usługi tooreturn hello ostatecznej odpowiedzi kod, a następnie przerywania połączenia hello. 
6. Koder Hello nie może używać hello `Events()` rzeczownik zgodnie z opisem w 9.2 w [1] na żywo wprowadzanie do usługi Media Services.
7. Jeśli kończy żądanie HTTP POST hello lub razy ze TCP błąd toohello przed końcem strumienia hello kodera hello musi wygenerowanie nowego żądania POST, używając nowego połączenia i wykonaj hello powyższych wymagań. Ponadto kodera hello musi ponownie wysłać hello poprzednich dwóch fragmenty MP4 dla każdej ścieżki w strumieniu hello i wznowienie bez wprowadzania brak ciągłości w osi czasu nośnika hello. Ponowne wysyłanie hello ostatnie dwa fragmenty MP4 dla każdej ścieżki gwarantuje, że jest bez utraty danych. Innymi słowy jeśli zawiera strumień audio i wideo ścieżkę, a nie bieżącego żądania POST hello, koder hello należy nawiązać ponownie połączenie i Wyślij ponownie hello ostatnie dwa fragmenty hello ścieżki audio, które wcześniej zostały pomyślnie wysłane, oraz hello ostatnie dwa fragmenty dla Ścieżka wideo Hello, które wcześniej zostały pomyślnie wysłane tooensure, że nie ma bez utraty danych. Koder Hello muszą zachować "do przodu" bufora fragmentów nośnika, które wysyła go ponownie po wznowieniu połączenia.

## <a name="5-timescale"></a>5. skali czasu
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) opisuje hello użycia skali czasu dla **SmoothStreamingMedia** (sekcja 2.2.2.1) **StreamElement** (sekcja 2.2.2.3) **StreamFragmentElement**(Sekcja 2.2.2.6), a **LiveSMIL** (2.2.7.3.1 sekcji). Jeśli nie ma wartości skali czasu hello, hello wartość domyślna używana jest 10 000 000 (10 MHz). Mimo że hello Smooth Streaming specyfikacji formatu nie blokuje użycia innych wartości skali czasu, większości implementacji kodera użyć to ustawienie domyślne toogenerate wartość (10 MHz), Smooth Streaming pozyskiwania danych. Z powodu toohello [dynamicznego tworzenia pakietów Azure Media](media-services-dynamic-packaging-overview.md) funkcji zalecane użycie 90 KHz Skala czasu dla strumieni wideo i 44,1 KHz lub 48.1 KHz dla strumieni audio. Jeśli wartości różnych skali czasu są używane do różnych strumieni, należy wysłać hello poziomu strumienia w skali czasu. Aby uzyskać więcej informacji, zobacz [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Definicja "strumień"
Strumień jest podstawowa jednostka hello operacji w wprowadzanie na żywo do tworzenia prezentacji na żywo, obsługę przesyłania strumieniowego trybu failover i scenariusze nadmiarowości. Strumień jest zdefiniowany jako jeden unikatowy, pofragmentowane bitstream MP4, który może zawierać pojedynczą ścieżkę lub wiele ścieżek. Prezentacja pełnej na żywo może zawierać jeden lub więcej strumieni, w zależności od konfiguracji hello hello koderów na żywo. Hello następujące przykłady przedstawiają różne opcje użycia toocompose strumieni prezentacji pełnej na żywo.

**Przykład:** 

Odbiorca chce otrzymywać toocreate na żywo prezentacji przesyłania strumieniowego, która obejmuje powitania po audio/wideo szybkości transmisji bitów:

Wideo — 3000 KB/s, 1500 KB/s, 750 Kb/s

Audio – 128 Kb/s

### <a name="option-1-all-tracks-in-one-stream"></a>Opcja 1: Wszystkie ścieżki w jednego strumienia
W przypadku tej opcji jeden koder generuje wszystkie ścieżki audio/wideo i zawiera ich w jednym pofragmentowane bitstream MP4. Witaj pofragmentowany plik MP4, bitstream jest następnie wysyłana za pośrednictwem jednego połączenia HTTP POST. W tym przykładzie jest tylko jeden strumień w tej prezentacji na żywo.

![Śledź strumieni-do-jednego.][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Opcja 2: Każdej ścieżki w oddzielnych strumienia
W przypadku tej opcji kodera hello umieszcza jedną ścieżkę bitstream każdego fragmentu MP4 i zapisuje wszystkie strumienie hello przez oddzielne połączenia HTTP. Można to zrobić za pomocą kodera jednego lub wielu koderów. wprowadzanie na żywo Hello widzi tej prezentacji na żywo, jak składa się z czterech strumieni.

![Śledzi oddzielne strumienie][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Opcja 3: Ścieżka audio pakietu z hello najniższa szybkość transmisji bitów Ścieżka wideo do jednego strumienia
W przypadku tej opcji powitania klienta wybiera ścieżkę toobundle hello audio z hello Ścieżka wideo najniższa szybkość transmisji bitów w jednym fragmencie MP4 bitstream i pozostaw hello innych dwóch ścieżek wideo jako oddzielne strumienie. 

![Śledzi strumieni audio i wideo][image4]

### <a name="summary"></a>Podsumowanie
Nie jest to pełna lista wszystkich opcji wprowadzanie możliwe w ramach tego przykładu. Jak rzeczy zgrupowania ścieżki do strumieni jest obsługiwana przez wprowadzanie na żywo. Klienci i dostawcy kodera można wybrać własne implementacje na podstawie engineering złożoności, pojemność koder i nadmiarowości i zagadnienia dotyczące trybu failover. Jednak w większości przypadków jest tylko jedną ścieżkę audio hello całej prezentacji na żywo. Tak jego ważne tooensure hello healthiness z hello pozyskiwania strumienia, który zawiera hello ścieżki audio. Ta kwestia często powoduje umieszczenie hello ścieżki audio w jego własnej strumienia (jak opcja 2) lub funkcję tworzenia pakietów z hello Ścieżka wideo najniższa szybkość transmisji bitów (jak opcja 3). Ponadto dla lepszej nadmiarowość i odporność na uszkodzenia, wysyłanie hello tej samej ścieżki audio w dwóch różnych strumieni (opcja 2 z nadmiarowe ścieżki audio) lub ścieżkę audio hello powiązanego z co najmniej dwie ścieżki wideo hello najniższa szybkość transmisji bitów (opcja 3 o audio powiązane w w co najmniej dwóch strumieni wideo) zdecydowanie zaleca się na żywo pozyskiwania do usługi Media Services.

## <a name="7-service-failover"></a>7. Usługa trybu failover
Podany charakter hello transmisja strumieniowa na żywo obsługę pracy awaryjnej dobrej jest istotne dla zapewnienia dostępności hello hello usługi. Usługa Media Services jest zaprojektowana toohandle różnego typu awarii, w tym błędy sieci, serwer błędów i problemów z magazynowaniem. Gdy jest używany w połączeniu z logiką prawidłowego trybu failover z hello strony kodera na żywo, klientów można osiągnąć wysoce niezawodne usługa transmisji strumieniowej na żywo z hello chmury.

W tej sekcji omówiono scenariuszach pracy awaryjnej usługi. W takim przypadku niepowodzenia hello sytuacji gdzieś w ramach usługi hello i ujawnia się jako błąd sieciowy. Poniżej przedstawiono kilka zaleceń dla implementacji kodera hello obsługę pracy awaryjnej usługi:

1. Użyj limitu 10 sekundy do nawiązywania połączeń TCP hello. Jeśli próba tooestablish hello połączenia trwa dłużej niż 10 sekund, przerwać hello operację i spróbuj ponownie. 
2. Użyj krótki limit czasu wysyłania fragmentów komunikatu żądania hello HTTP. Jeśli hello docelowy MP4 fragmentu duration N sekund, użyj limit czasu wysyłania, od N do 2 N sekund; na przykład jeśli czas trwania fragmentu MP4 hello 6 sekund, Użyj limitu czasu w sekundach too12 6. Jeśli zostanie przekroczony limit czasu, resetowania hello połączenia, Otwórz nowe połączenie i Wznów strumienia pozyskiwania na powitania nowego połączenia. 
3. Obsługa stopniowego buforu, który ma hello ostatnie dwa fragmenty dla każdej ścieżki wysłanych pomyślnie i całkowicie toohello usługi.  Jeśli hello żądanie HTTP POST dla strumienia zostało zakończone lub upłynął jej czas przed toohello koniec strumienia hello, otworzyć nowe połączenie i rozpocząć kolejnego żądania HTTP POST, wysłania nagłówków strumienia hello Wyślij ponownie hello ostatnie dwa fragmenty dla każdej ścieżki i wznowić strumienia hello bez Prezentacja brak ciągłości w osi czasu nośnika hello. Zmniejsza hello ryzyko utraty danych.
4. Firma Microsoft zaleca tego kodera hello nie Ogranicz liczbę ponownych prób tooestablish połączenie hello lub wznowić przesyłania strumieniowego po wystąpieniu błędu TCP.
5. Po wystąpieniu błędu TCP:
  
    a. bieżące połączenie Hello muszą zostać zamknięte, a nowe połączenie musi zostać utworzony dla nowego żądania HTTP POST.

    b. Witaj nowe HTTP POST adres URL musi być hello tak samo jak hello początkowego adresu URL przesyłania.
  
    c. Hello nowe HTTP POST musi zawierać nagłówki strumienia (**ftyp zawiera informacje**, **aktywne okno manifestu serwera**, i **moov** pól), które są identyczne toohello strumienia nagłówków w hello początkowa POST.
  
    d. ostatnie dwa fragmenty Hello wysłane dla każdej ścieżki, należy ponownie wysłać i przesyłania strumieniowego wznowienia bez wprowadzania brak ciągłości w osi czasu nośnika hello. Hello sygnatury czasowe fragmentu MP4 należy zwiększyć stale, nawet przez żądania HTTP POST.
6. Koder Hello powinien przerwanie hello żądanie HTTP POST, jeśli dane nie są wysyłane z szybkością proporcjonalnie do czasu trwania fragmentu MP4 hello.  Żądanie HTTP POST, który nie będzie przesyłał dane mogą uniemożliwić szybko odłączanie kodera hello w zdarzeniu hello aktualizacji usługi Media Services. Z tego powodu hello HTTP POST do rozrzedzonych ścieżki (sygnał ad) powinna być krótkotrwały i przerywa jak fragmentu rozrzedzonych hello są wysyłane.

## <a name="8-encoder-failover"></a>8. Koder trybu failover
Koder pracy awaryjnej jest hello drugiego typu scenariusz trybu failover, który wymaga toobe skierowane do dostarczania transmisji strumieniowej na żywo na trasie. W tym scenariuszu hello wystąpi błąd po stronie kodera hello. 

![Koder trybu failover][image5]

powitania od oczekiwań się punkt końcowy na żywo wprowadzanie hello w przypadku pracy awaryjnej kodera:

1. Nowe wystąpienie kodera należy utworzyć toocontinue przesyłania strumieniowego, jak pokazano na diagramie hello (strumienia wideo z linii kreskowanej k 3000).
2. Koder nowe Hello musi Użyj hello sam adres URL dla metody POST protokołu HTTP żądania jako hello nie wystąpienia.
3. Hello kodera nowego żądania POST musi zawierać hello sam pofragmentowany pola nagłówka MP4 jako hello wystąpienia nie powiodło się.
4. Koder nowe Hello musi prawidłowo zsynchronizowane z wszystkie inne uruchomione koderów dla hello tego samego toogenerate prezentacji na żywo zsynchronizowane przykłady audio i wideo z granice wyrównany fragmentu.
5. Witaj nowego strumienia musi być semantycznie równoważne z poprzednich strumienia hello i wymienne poziomach hello nagłówka i fragmentu.
6. Koder nowe Hello należy spróbować toominimize utraty danych. Witaj `fragment_absolute_time` i `fragment_index` nośnika fragmenty należy zwiększyć z punktu hello których ostatnio zatrzymano hello kodera. Witaj `fragment_absolute_time` i `fragment_index` należy zwiększyć w sposób ciągły, ale jest dopuszczalna toointroduce brak ciągłości, jeśli to konieczne. Usługi Media Services ignoruje fragmentów, które ma już odbierane i przetwarzane, tak aby lepiej tooerr po stronie powitania ponowne wysyłanie fragmenty niż przerw toointroduce hello osi czasu z nośnika. 

## <a name="9-encoder-redundancy"></a>9. nadmiarowość kodera
Krytyczne dla niektórych wydarzeń na żywo że żądanie nawet wyższej dostępności i jakości obsługi, zaleca się używać nadmiarowych koderów aktywny aktywny tooachieve płynnego trybu failover bez utraty danych.

![nadmiarowość kodera][image6]

Jak pokazano na tym diagramie, dwie grupy koderów wypchnąć dwie kopie każdego strumienia jednocześnie do hello usługi na żywo. Ta konfiguracja jest obsługiwana, ponieważ usługi Media Services można odfiltrować zduplikowane fragmenty oparte na sygnatury czasowej ID i fragment strumienia. Witaj wynikowy strumień na żywo i archiwum jest pojedynczej kopii wszystkich strumieni hello będący hello najlepsze możliwe agregacji z hello dwóch źródeł. Na przykład w przypadku extreme hipotetyczny tak długo, jak istnieje jeden koder (nie ma hello toobe dyskiem) działania na dowolnym etapie w czasie dla każdego strumienia hello wynikowa strumień na żywo z usługi hello jest ciągłe bez utraty danych. 

Hello wymagań dotyczących tego scenariusza są prawie takie same hello jako hello wymagań w przypadku "Kodera trybu failover" hello, z wyjątkiem hello, drugi zestaw koderów hello uruchomionych na powitania sam czas hello koderów podstawowego.

## <a name="10-service-redundancy"></a>10. nadmiarowość usługi
Czasami wysokiej nadmiarowe dystrybucji globalnych, musi mieć regionalnej awarii między region toohandle kopii zapasowej. Rozszerzając topologii "Kodera nadmiarowość" hello, klienci mogą wybrać toohave wdrożenia usługi nadmiarowego w innym regionie, który jest połączony z drugiego zestawu koderów hello. Klienci również może współpracować z toodeploy dostawcy Content Delivery Network globalne Menedżera ruchu przed hello dwa wdrożenia tooseamlessly trasy klienta ruchu w ramach usługi. Hello wymagania dotyczące koderów hello są tak samo jak w przypadku "Kodera nadmiarowość" hello hello. Hello tylko wyjątku jest drugi zestaw hello toobe potrzeb koderów na żywo wskazywana tooa różnych pozyskiwania punktu końcowego. Witaj Poniższy diagram przedstawia Instalatora:

![nadmiarowość usługi][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Specjalne rodzaje wprowadzanie formatów
W tej sekcji omówiono specjalne rodzaje formatów wprowadzanie na żywo, które są zaprojektowane toohandle określonych scenariuszy.

### <a name="sparse-track"></a>Śledź rozrzedzony
W celu dostarczenia prezentacji transmisji strumieniowej na żywo przy użyciu środowiska wzbogaconego klienta, często jest niezbędne tootransmit zsynchronizowany czas zdarzenia lub sygnały wewnątrzpasmowe hello głównym nośnika danych. Na przykład jest wstawiania reklam na żywo dynamicznych. Ten typ zdarzenia sygnalizowania różni się od przesyłania strumieniowego z powodu natury rozrzedzonych regularne audio/wideo. Innymi słowy hello sygnalizowania danych zwykle odbywa się stale i interwał powitania może być toopredict twardych. pojęcie Hello rozrzedzonych Śledź została zaprojektowana tooingest i emisji wewnątrzpasmowe sygnalizowania danych.

Witaj następujące czynności są zalecane implementacji służy do wprowadzania rozrzedzonych Śledź:

1. Utwórz oddzielne bitstream MP4 pofragmentowane zawierający tylko rozrzedzonych ścieżki, bez ścieżki audio i wideo.
2. W hello **aktywne okno manifestu serwera** zgodnie z definicją w sekcji 6 w [1], użyj hello *parentTrackName* nazwa hello toospecify parametru hello ścieżki nadrzędnej. Aby uzyskać więcej informacji zobacz sekcję 4.2.1.2.1.2 w [1].
3. W hello **aktywne okno manifestu serwera**, **manifestOutput** musi być ustawiona zbyt**true**.
4. Podana hello rozrzedzonych rodzaj hello sygnalizowania zdarzenia, zaleca się następujące hello:
   
    a. Na początku hello hello wydarzenia na żywo, koder hello wysyła pola nagłówka początkowej hello toohello usługi, która umożliwia śledzenie rozrzedzonych tooregister hello hello usługi w manifeście klienta hello.
   
    b. Koder Hello powinien z chwilą żądanie HTTP POST hello dane nie są wysyłane. Długotrwałe HTTP POST nie wysyła dane mogą uniemożliwić szybko odłączanie kodera hello w przypadku hello ponowny rozruch update lub usługi Media Services. W takich przypadkach hello serwer multimediów jest tymczasowo zablokowany w operacji odbierania dla gniazda hello.
   
    c. W czasie hello gdy sygnalizowania danych nie jest dostępna koder hello powinna zamykać hello żądanie HTTP POST. Podczas żądania POST hello jest aktywny, koder hello należy wysłać danych.

    d. Podczas wysyłania rozrzedzonych fragmenty, koder hello można ustawić jawne nagłówek content-length, jeśli jest dostępna.

    e. Podczas wysyłania rozrzedzonych fragmenty o nowe połączenie, koder hello należy zacząć wysyłania z pola nagłówka hello, następuje hello nowych fragmentów. To w przypadku sytuacji między w pracą w trybie failover, a nowe połączenie rozrzedzonych hello są ustalonych tooa nowy serwer, który nie otrzymała hello Śledź rozrzedzonych przed.

    f. fragment rozrzedzonych Śledź Hello staje się dostępne toohello klienta podczas hello odpowiedniego nadrzędnego śledzenie fragment, który ma wartość równą lub większą sygnatury czasowej staje się dostępna toohello klienta. Na przykład, jeśli fragmentu rozrzedzonych hello ma sygnaturę czasową t = 1000, oczekuje się, które po powitania klienta widzi "wideo" (przy założeniu nazwa ścieżki nadrzędnej hello "wideo") fragmentu sygnatury czasowej 1000 lub nowszych, można pobrać hello rozrzedzonych fragmentu t = 1000. Należy pamiętać, że hello rzeczywiste sygnału może służyć do inne położenie na osi czasu prezentacji hello wyznaczone z przeznaczeniem. W tym przykładzie tego możliwe, że hello rozrzedzonych fragmentu t = 1000 ma ładunek XML, czyli wstawiania ad w pozycji, która jest kilka sekund później.

    g. ładunek Hello fragmentów Śledź rozrzedzonych może być w różnych formatach (na przykład XML, tekst lub binarny), w zależności od scenariusza hello.

### <a name="redundant-audio-track"></a>Nadmiarowe ścieżki audio
W typowym HTTP adaptacyjnego przesyłania strumieniowego scenariuszu (na przykład, Smooth Streaming lub kreska) często istnieje tylko jedną ścieżkę audio w hello całej prezentacji. W odróżnieniu od wideo ścieżek, które mają wiele poziomy jakości powitania klienta toochoose od w warunkach błędu, ścieżka audio hello może być pojedynczym punktem awarii, jeśli hello wprowadzanie hello strumienia, który zawiera ścieżki audio hello jest uszkodzona. 

Ten problem, usługi Media Services obsługuje toosolve live wprowadzanie nadmiarowe ścieżki audio. pomysł Hello jest hello, tej samej ścieżki audio może być wysyłana wielokrotnie w różnych strumieni. Mimo że hello usługa tylko rejestruje ścieżki audio hello raz w manifeście klienta hello, może używać nadmiarowe ścieżki audio jako zapasowe pobierania audio fragmenty, jeśli hello głównej ścieżki audio występują problemy. nadmiarowe ścieżki audio tooingest, koder hello musi:

1. Utwórz hello ścieżka tego samego audio w wielu fragmentu MP4 bitstreams. nadmiarowe ścieżki audio Hello, należy mieć semantycznie równoważne z hello sam fragmentu sygnatury czasowe i być wymienne na poziomach fragmentu i hello nagłówka.
2. Upewnij się, że wpis "audio" hello w hello aktywnego serwera manifestu (sekcja 6 [1]) jest hello takie same dla wszystkich nadmiarowe ścieżki audio.

nadmiarowe ścieżki audio zaleca się powitania po implementacji:

1. Wyślij każdego unikatową ścieżkę audio w strumieniu samodzielnie. Także wysłać strumień nadmiarowe dla każdego z tych strumieni ścieżki audio, gdy strumień drugi hello różni się od hello najpierw tylko przez identyfikator hello w hello adresu URL HTTP POST: {protokołu} :// {adres serwera} / {publikowanie path}/Streams({identifier}) punktu.
2. Użyj oddzielnych strumienie toosend hello dwóch najniższy wideo szybkości transmisji bitów. Każdy z tych strumieni powinien również zawierać kopię każdego unikatową ścieżkę audio. Na przykład jeśli obsługuje wiele języków, tych strumieni powinien zawierać ścieżek audio dla każdego języka.
3. Użyj tooencode wystąpień oddzielny serwer (koder) i wysłać hello strumieni nadmiarowe wspomnianego (1) i (2). 

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
