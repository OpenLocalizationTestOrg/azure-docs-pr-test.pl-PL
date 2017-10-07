---
title: aaaAzure Media Services Telemetrii | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie telemetrii usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Telemetrii usługi Azure Media Services

Azure Media Services (AMS) umożliwia tooaccess danych telemetrii/metryki dla swoich usług. Bieżąca wersja AMS Hello pozwala na żywo zbierania danych telemetrycznych dla **kanału**, **StreamingEndpoint**i na żywo **archiwum** jednostek. 

Dane telemetryczne są zapisywane tabeli magazynu tooa w konta usługi Azure Storage, który określisz (zazwyczaj używasz konta magazynu hello skojarzonych z Twoim kontem AMS). 

Witaj telemetrii systemu nie zarządza przechowywania danych. Można usunąć stare dane telemetryczne hello, usuwając hello magazynu tabel.

W tym temacie omówiono sposób tooconfigure i zużywać telemetrii hello AMS.

## <a name="configuring-telemetry"></a>Konfigurowanie telemetrii

Dane telemetryczne można skonfigurować na poziom szczegółowości na poziomie składnika. Istnieją dwa poziomy szczegółowości "Normal" i "Pełne". Obecnie obu poziomach zwracać hello tych samych informacji. Zalecane jest toouse "Normalny. 

Witaj, jak następujące tematy Pokaż dane telemetryczne tooenable:

[Włączanie danych telemetrycznych z platformą .NET](media-services-dotnet-telemetry.md) 

[Włączanie telemetrii REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Wykorzystywanie informacji telemetrii

Dane telemetryczne są zapisywane tooan tabeli magazynu Azure na koncie magazynu hello określoną podczas konfigurowania dane telemetryczne dotyczące hello konta usługi Media Services. W tej sekcji opisano hello tabel do przechowywania hello metryki.

Będzie można korzystać z danych telemetrycznych w jednym z hello następujące sposoby:

- Odczytywanie danych bezpośrednio z magazynem tabel Azure (np. przy użyciu hello zestawu SDK usługi Magazyn). Opis hello tabel do przechowywania danych telemetrii, zobacz hello **wykorzystywanie informacji telemetrii** w [to](https://msdn.microsoft.com/library/mt742089.aspx) tematu.

Lub

- Używać funkcji hello w hello .NET SDK usługi Media Services do odczytywania danych z magazynu, zgodnie z opisem w [to](media-services-dotnet-telemetry.md) tematu. 


Schemat danych telemetrycznych Hello opisanych poniżej jest zaprojektowana toogive dobrą wydajność w ramach limitów hello Azure Table Storage:

- Partycjonowanego konta identyfikator i identyfikator usługi danych telemetrii tooallow z każdego toobe usługi proszeni niezależnie.
- Partycje zawierają hello Data toogive uzasadnione górna granica na powitania rozmiar partycji.
- Wiersz klucze będą proszeni w czasu odwrotnej kolejności tooallow hello najnowsze dane telemetryczne elementów toobe dla danej usługi.

Powinno to umożliwić wielu typowych toobe zapytania hello wydajne:

- Równoległe, niezależne pobieranie danych dla poszczególnych usług.
- Pobieranie wszystkich danych dla danej usługi w zakresie daty.
- Pobieranie najnowszych danych hello usługi.

### <a name="telemetry-table-storage-output-schema"></a>Schemat danych wyjściowych magazynu tabeli telemetrii

Dane telemetryczne są przechowywane w agregacji w jednej tabeli, "TelemetryMetrics20160321", gdzie "20160321" jest data hello utworzone tabeli. Dane telemetryczne system tworzy osobnej tabeli dla każdego dnia nowy, oparty na 00:00 czasu UTC. Tabela Hello jest używana toostore cyklicznego wartości pozyskiwania, takich jak szybkości transmisji bitów w ramach danego okna czasu wysłane bajty, itp. 

Właściwość|Wartość|Przykłady/notes
---|---|---
PartitionKey|{Identyfikator konta} _ {identyfikator jednostki}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66 < br /<br/>Witaj konta identyfikator jest uwzględniona w przepływ toosimplify klucza partycji hello gdzie wiele kont usługi Media Services pisania toohello tego samego konta magazynu.
RowKey|{sekund toomidnight} _ {losowych wartości}|01688_00199<br/><br/>klucz wiersza Hello rozpoczyna się od hello liczbę sekund toomidnight tooallow top n styl zawartych w partycji. Aby uzyskać więcej informacji, zobacz [to](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) artykułu. 
Znacznik czasu|Data i godzina|Automatycznie sygnatury czasowej z hello Azure tabeli 2016-09-09T22:43:42.241Z
Typ|Typ Hello hello podmiotów świadczących dla nich dane telemetryczne|Kanał/StreamingEndpoint/archiwum<br/><br/>Typ zdarzenia jest tylko wartość ciągu.
Nazwa|Nazwa Hello hello dane telemetryczne zdarzenia|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|zdarzenia telemetrii hello czasu Hello wystąpił (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Witaj obserwowanych czasu został podany przez hello jednostki wysyłania hello telemetrii (na przykład kanał). Może to być problemy z synchronizacją między składnikami, dlatego ta wartość jest w przybliżeniu czas
ServiceID|{Identyfikator usługi}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Właściwości jednostki|Zgodnie z definicją zdarzenia hello|StreamName: stream1, szybkości transmisji bitów 10123...<br/><br/>pozostałe właściwości Hello są definiowane dla hello danego typu zdarzenia. Zawartości tabeli platformy Azure jest pary wartości klucza.  (to znaczy różne wiersze w tabeli hello mają różne zestawy właściwości).

### <a name="entity-specific-schema"></a>Schemat specyficzne dla jednostki

Istnieją trzy typy wpisów telemetrycznego dane specyficzne dla jednostki, które wypychana każdego z powitania po częstotliwość:

- Punkty końcowe przesyłania strumieniowego: co 30 sekund
- Na żywo kanałów: co minutę
- Na żywo archiwum: co minutę

**Punkt końcowy przesyłania strumieniowego**

Właściwość|Wartość|Przykłady
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Znacznik czasu|Znacznik czasu|Automatycznie sygnatury czasowej z Azure tabeli 2016-09-09T22:43:42.241Z
Typ|Typ|StreamingEndpoint
Nazwa|Nazwa|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identyfikator usługi|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Nazwa hosta|Nazwa hosta punktu końcowego hello|builddemoserver.Origin.mediaservices.Windows.NET
statusCode|Stan rekordów HTTP|200
resultCode|Szczegóły kod wyniku|S_OK
RequestCount|Całkowita liczba żądania w hello agregacji|3
Żądania|Wysłane bajty zagregowane|2987358
ServerLatency|Server Średni czas oczekiwania (łącznie z magazynem)|129
E2ELatency|Średnie opóźnienie end-to-end|250

**Kanału na żywo**

Właściwość|Wartość|Przykłady/notes
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Znacznik czasu|Znacznik czasu|Automatycznie sygnatury czasowej z hello Azure tabeli 2016-09-09T22:43:42.241Z
Typ|Typ|Kanał
Nazwa|Nazwa|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identyfikator usługi|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Typ ścieżki nr audio/wideo/tekstu|audio/wideo
TrackName|Nazwa ścieżki hello|wideo/audio_1
Szybkość transmisji bitów|Śledź szybkości transmisji bitów|785000
Customattributes —||   
IncomingBitrate|Rzeczywista szybkość transmisji bitów przychodzących|784548
OverlapCount|Zakładki na powitania pozyskiwania|0
DiscontinuityCount|Brak ciągłości dla ścieżki|0
LastTimestamp|Sygnatura czasowa ostatniego pozyskiwane danych|1800488800
NonincreasingCount|Liczba fragmentów usunięte z powodu zwiększenie toonon sygnatury czasowej|2
UnalignedKeyFrames|Gdzie klucza ramek nie jest wyrównana czy odebrano fragment(s) (za pośrednictwem poziomy jakości) |True
UnalignedPresentationTime|Określa, czy odebrano fragment(s) (za pośrednictwem poziomy jakości/ścieżek), gdzie czas prezentacji nie jest wyrównany|True
UnexpectedBitrate|Wartość PRAWDA Jeśli jest obliczana rzeczywista szybkość transmisji bitów audio/wideo śledzenia > 40 000/s i IncomingBitrate == lub IncomingBitrate i actualBitrate różnią się 50% 0 |True
W dobrej kondycji|Wartość true, jeśli <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> są wszystkie 0|True<br/><br/>Złożonych funkcji, która zwraca wartość FAŁSZ, gdy dowolne hello następujące warunki blokady jest kondycja:<br/><br/>-OverlapCount > 0.<br/>-DiscontinuityCount > 0.<br/>-NonincreasingCount > 0.<br/>-UnalignedKeyFrames == True<br/>-UnalignedPresentationTime == True<br/>-UnexpectedBitrate == True

**Archiwum na żywo**

Właściwość|Wartość|Przykłady/notes
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Znacznik czasu|Znacznik czasu|Automatycznie sygnatury czasowej z hello Azure tabeli 2016-09-09T22:43:42.241Z
Typ|Typ|Archiwum
Nazwa|Nazwa|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identyfikator usługi|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|Adres url programu|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ISM
TrackName|Nazwa ścieżki hello|audio_1
TrackType|Typ ścieżki hello|Audio i wideo
Element CustomAttribute|Liczba szesnastkowa ciąg, który rozróżnia między inną ścieżkę o tej samej nazwie i szybkości transmisji bitów (multi aparatu kąt)|
Szybkość transmisji bitów|Śledź szybkości transmisji bitów|785000
W dobrej kondycji|Wartość true, jeśli FragmentDiscardedCount == 0 & & ArchiveAcquisitionError == False|Wartość true (te dwie wartości nie są obecne w hello metryki, ale są obecne w zdarzeniu źródła hello)<br/><br/>Złożonych funkcji, która zwraca wartość FAŁSZ, gdy dowolne hello następujące warunki blokady jest kondycja:<br/><br/>-FragmentDiscardedCount > 0.<br/>-ArchiveAcquisitionError == True

## <a name="general-qa"></a>Ogólne pytań i odpowiedzi

### <a name="how-tooconsume-metrics-data"></a>Jak tooconsume metryki danych?

Metryki dane są przechowywane w postaci serii tabel Azure na koncie magazynu powitania klienta. Te dane mogą być używane, za pomocą hello następujące narzędzia:

- AMS SDK
- Eksplorator usługi Storage Azure firmy Microsoft (obsługuje format wartości rozdzielane toocomma eksportu i przetworzonych w programie Excel)
- Interfejs API REST

### <a name="how-toofind-average-bandwidth-consumption"></a>Jak toofind Średnie zużycie przepustowości?

Witaj średniej przepustowości jest średnią hello żądania w danym okresie czasu.

### <a name="how-toodefine-streaming-unit-count"></a>Jak liczba toodefine jednostkę przesyłania strumieniowego?

Witaj przesyłania strumieniowego liczby jednostek można zdefiniować jako przepływności szczytu hello z rozdzielonych przepływność szczytu hello jeden punkt końcowy przesyłania strumieniowego punktów końcowych przesyłania strumieniowego hello usługi. Witaj szczytowego można używać przepływność jeden punkt końcowy przesyłania strumieniowego to 160 MB/s.
Na przykład załóżmy, że przepływność szczytu powitania od klienta usługi jest 40 MB/s (hello maksymalną wartość BytesSent w danym okresie czasu). Następnie hello przesyłania strumieniowego liczba jednostek jest równy too(40 MBps) * /(160 Mbps) (w 8 bitów na bajt) = 2 jednostki przesyłania strumieniowego.

### <a name="how-toofind-average-requestssecond"></a>Jak średnia toofind żądań na sekundę?

toofind hello średnia liczba żądań/sekundę obliczeniowe hello średnia liczba żądań (RequestCount) w danym okresie czasu.

### <a name="how-toodefine-channel-health"></a>Jak toodefine kanału kondycji?

Kanał kondycji można zdefiniować jako złożone funkcja logiczna taki sposób, że ma wartość false, gdy przechowywania dowolnej hello następujące warunki:

- OverlapCount > 0.
- DiscontinuityCount > 0.
- NonincreasingCount > 0.
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>Jak przerw toodetect?

Brak ciągłości toodetect, Znajdź wszystkie wpisy danych kanału gdzie DiscontinuityCount > 0. Sygnatura czasowa Hello odpowiedniego ObservedTime wskazuje razy hello, w których wystąpił brak ciągłości hello.

### <a name="how-toodetect-timestamp-overlaps"></a>Jak sygnatury czasowej toodetect nakłada?

toodetect sygnatury czasowej nakładania się, Znajdź wszystkie wpisy danych kanału gdzie OverlapCount > 0. sygnatury czasowej Hello odpowiedniego ObservedTime wskazuje hello wystąpił razy, na które hello nakłada sygnatury czasowej.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Jak toofind przesyłanie strumieniowe żądania awarie i przyczyny?

toofind przesyłania strumieniowego błędów żądań i ze względu na wyszukiwanie wszystkie wpisy danych punktu końcowego przesyłania strumieniowego, gdy ResultCode nie jest równy tooS_OK. odpowiednie pole StatusCode Hello wskazuje hello przyczyny niepowodzenia żądania hello.

### <a name="how-tooconsume-data-with-external-tools"></a>Jak tooconsume danych za pomocą narzędzi zewnętrznych?

Telemetrycznego danych mogą być przetwarzane i wizualizowane z hello następujące narzędzia:

- Usługa PowerBI
- Application Insights
- Monitor Azure (dawniej Shoebox)
- Pulpit nawigacyjny na żywo usług AMS
- Portalu Azure (oczekiwanie wersji)

### <a name="how-toomanage-data-retention"></a>Sposób przechowywania danych toomanage?

system telemetrii Hello nie zapewnia zarządzania przechowywania danych ani automatycznego usuwania starych rekordów. W związku z tym należy toomanage i ręcznie usuń stare rekordy z tabeli magazynu hello. Może się odwoływać toostorage zestawu SDK dotyczące toodo go.

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
