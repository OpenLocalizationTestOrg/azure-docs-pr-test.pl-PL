---
title: "aaaStream na żywo za pomocą koderów lokalnych, które tworzą strumienie wielokrotnej szybkości transmisji bitów - Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak tooset kanału, który odbiera różnych szybkościach transmisji bitów na żywo strumienia z kodera lokalnymi. Hello strumienia mogą następnie zostać dostarczone tooclient odtwarzanie aplikacji za pośrednictwem jednego lub więcej punktów końcowych przesyłania strumieniowego przy użyciu jednej z powitania po protokołów przesyłania strumieniowego z adaptacyjną: DASH HLS, Smooth Streaming."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Transmisja strumieniowa za pomocą koderów lokalnych, które tworzą strumienie o różnych szybkościach transmisji bitów na żywo
## <a name="overview"></a>Omówienie
W usłudze Azure Media Services *kanału* reprezentuje potok przetwarzania zawartości transmisji strumieniowej na żywo. Kanał otrzymuje na żywo wejściowych strumieni w jeden z dwóch sposobów:

* Na lokalny koder na żywo wysyła RTMP wielokrotnej szybkości transmisji bitów lub Smooth Streaming (pofragmentowany MP4) strumienia toohello kanału, który nie jest włączone tooperform live kodowania w usłudze Media Services. Witaj pozyskanych strumieni przekazywania kanałów bez dalszego przetwarzania. Ta metoda jest wywoływana *przekazywanego*. Można użyć następujących koderów na żywo, które mają wielokrotnej szybkości transmisji bitów Smooth Streaming jako dane wyjściowe hello: nośników w programie Excel, Ateme Wyobraź sobie komunikacji, Envivio, Cisco i Elemental. następujące kodery na żywo Hello ma RTMP jako dane wyjściowe: Adobe Flash Media na żywo koder Telestream Wirecast, Haivision, Teradek i TriCaster. Koder na żywo może także wysłać kanału tooa pojedynczej szybkości transmisji bitów strumienia, który nie jest włączona dla kodowanie na żywo, ale nie jest to zalecane. Usługi Media Services dostarcza hello toocustomers strumienia, który go zażądać.

  > [!NOTE]
  > Metoda przekazywania jest najbardziej ekonomiczne rozwiązanie hello toodo transmisji strumieniowej na żywo.


* Na lokalny koder na żywo wysyła kanału toohello pojedynczej szybkości transmisji bitów strumienia, który jest włączone tooperform live encoding w usłudze Media Services w jednym z następujących formatów hello: RTP (MPEG-TS), protokołu RTMP lub Smooth Streaming (pofragmentowany MP4). Witaj kanał wykonuje następnie kodowanie na żywo hello pojedynczej szybkości transmisji bitów strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej) wideo strumienia przychodzącego. Usługi Media Services dostarcza hello toocustomers strumienia, który go zażądać.

Począwszy od hello Media Services 2.10 wersji, podczas tworzenia kanału, można określić sposób strumienia wejściowego hello tooreceive kanału. Można również określić, czy program hello tooperform kanału na żywo, kodowanie strumienia. Dostępne są dwie opcje:

* **Przekazuj**: podać tę wartość, jeśli planujesz toouse na lokalny koder na żywo, mające strumienia wielokrotnej szybkości transmisji bitów (strumień przekazujące) jako dane wyjściowe. W takim przypadku strumienia przychodzącego hello przechodzi przez toohello output bez żadnych kodowania. Jest to zachowanie hello kanału przed wprowadzeniem hello 2.10. Ten temat zawiera szczegółowe informacje o pracy z kanałami tego typu.
* **Kodowanie na żywo**: Wybierz tę wartość, jeśli planujesz tooencode Media Services toouse strumienia wielokrotnej szybkości transmisji bitów tooa strumień na żywo o pojedynczej szybkości transmisji bitów. Należy pamiętać, który pozostawienie kodowanie na żywo kanału **systemem** stanu będą naliczane opłaty rozliczeń. Zaleca się natychmiast zatrzymać uruchomione kanałów po zdarzenie transmisji strumieniowej na żywo jest pełną tooavoid opłat bardzo co godzinę. Usługi Media Services dostarcza hello toocustomers strumienia, który go zażądać.

> [!NOTE]
> W tym temacie omówiono atrybuty kanałów, które nie są włączone tooperform kodowanie na żywo. Aby uzyskać informacje na temat pracy z kanałami, które są włączone, tooperform kodowanie na żywo, zobacz [transmisja strumieniowa na żywo przy użyciu usługi Azure Media Services toocreate wielokrotnej szybkości transmisji bitów strumienie](media-services-manage-live-encoder-enabled-channels.md).
>
>

powitania po diagram reprezentuje transmisji strumieniowej na żywo przepływu pracy, który używa lokalnego kodera na żywo toohave RTMP o różnych szybkościach transmisji bitów lub pofragmentowany MP4 (Smooth Streaming) strumieni jako dane wyjściowe.

![Przepływ pracy na żywo][live-overview]

## <a id="scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo
Witaj poniższych krokach opisano zadania związane z tworzeniem typowych aplikacji transmisji strumieniowej na żywo.

1. Połącz komputer tooa kamerę wideo. Uruchom i skonfiguruj koder na żywo lokalnego, który ma RTMP o różnych szybkościach transmisji bitów lub pofragmentowany MP4 (Smooth Streaming) strumień jako dane wyjściowe. Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).

    Ten krok można również wykonywać po utworzeniu kanału.
2. Tworzenie i uruchamianie kanału.

3. Adres URL pozyskiwania kanału hello pobierania.

    Witaj kodera na żywo używa hello pozyskiwania adresu URL toosend hello strumienia toohello kanału.
4. Pobiera adres URL podglądu kanału hello.

    Użyj tego adresu URL tooverify, czy kanał prawidłowo odbiera strumień na żywo hello.
5. Utwórz program.

    Korzystając z hello portalu Azure, tworzenia program tworzy także zasób.

    Gdy używasz hello zestawu .NET SDK lub REST, należy toocreate zasobów i określ toouse ten zasób, podczas tworzenia programu.
6. Publikowanie zawartości hello, który jest skojarzony z programem hello.   

    >[!NOTE]
    >Po utworzeniu konta usługi Azure Media Services **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. Witaj, z którego mają zostać toostream zawartości punktu końcowego przesyłania strumieniowego ma toobe w hello **systemem** stanu.

7. Uruchom hello program, gdy wszystko jest gotowe toostart przesyłania strumieniowego i archiwizacji.

8. Opcjonalnie hello kodera na żywo może być sygnałowego toostart anonsu. Witaj reklama jest wstawiana hello strumienia wyjściowego.

9. Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.

10. Usuń hello program (i opcjonalnie można również usunąć hello zasobów).     

## <a id="channel"></a>Opis kanału i jej powiązane składniki
### <a id="channel_input"></a>Kanał danych wejściowych (pozyskiwania) konfiguracji
#### <a id="ingest_protocols"></a>Pozyskiwania protokołu przesyłania strumieniowego
Usługa Media Services obsługuje wprowadzania źródeł danych na żywo przy użyciu MP4 o różnych szybkościach transmisji bitów fragmentacji i RTMP o różnych szybkościach transmisji bitów jako strumieniowe protokołów. Gdy pozyskiwania hello RTMP przesyłania strumieniowego protokół jest zaznaczone, pozyskiwania dwa punkty końcowe (wejścia) są tworzone dla kanału hello:

* **Podstawowy adres URL**: Określa hello pełni kwalifikowany adres URL z RTMP podstawowego kanału hello pozyskiwania punktu końcowego.
* **Adres URL dodatkowej** (opcjonalnie): Określa hello pełny adres URL kanału hello dodatkowej RTMP pozyskiwania punktu końcowego.

Adres URL dodatkowej hello należy użyć tooimprove hello trwałości i odporność na uszkodzenia sieci pozyskiwania strumienia (a także kodera trybu failover i odporność na uszkodzenia), zwłaszcza w przypadku hello następujące scenariusze:

- Koder pojedynczego o podwójnej precyzji wypychanie tooboth głównych i dodatkowych adresów URL:

    głównym celem tego scenariusza Hello jest tooprovide większej odporności toonetwork fluktuacji i tłumienie. Niektóre kodery RTMP nie obsługują również zakończy połączenie sieci. W przypadku rozłączenia sieciowej kodera może zatrzymać kodowanie i następnie wysyłają hello buforowane dane w przypadku ponownego połączenia. Powoduje to przerw i utraty danych. Odłącza sieci może się zdarzyć z powodu nieprawidłowych sieci lub konserwacji na powitania po stronie platformy Azure. Adresy URL podstawowe i pomocnicze pozwalają ograniczyć problemy z siecią hello i kontrolowany przez proces uaktualniania. Zawsze rozłączenia zaplanowane sieci sytuacji usługi Media Services zarządza hello podstawowy i pomocniczy rozłącza oraz zapewnia opóźnione rozłączyć między hello dwa. Następnie koderów ma tookeep czas przesyłania danych i ponownie. odłączy Hello kolejność hello może być losowych, ale zawsze będzie opóźnienia między podstawowe i pomocnicze lub pomocniczym/podstawowych adresów URL. W tym scenariuszu kodera hello jest nadal hello pojedynczy punkt awarii.

- Wiele koderów, za pomocą kodera każdego wypychanie tooa dedykowanego punktu:

    W tym scenariuszu zawiera zarówno koder i pozyskiwania nadmiarowości. W tym scenariuszu encoder1 wypchnięcia toohello podstawowy adres URL, a encoder2 wypchnięcia toohello dodatkowej adresu URL. W przypadku awarii kodera hello innych kodera można zachować wysyłanie danych. Nadmiarowość danych mogą być obsługiwane, ponieważ usługi Media Services nie rozłączy głównych i dodatkowych adresów URL na powitania tym samym czasie. W tym scenariuszu przyjęto założenie, że koderów są synchronizowane czasu i dokładnie hello tych samych danych.  

- Wiele koderów o podwójnej precyzji wypychanie tooboth głównych i dodatkowych adresów URL:

    W tym scenariuszu oba koderów wypychania danych tooboth głównych i dodatkowych adresów URL. Zapewnia to hello najlepsze niezawodność i odporność na uszkodzenia, a także nadmiarowość danych. W tym scenariuszu może tolerować zarówno awariami kodera i rozłącza, nawet wtedy, gdy jeden koder przestanie działać. Przyjęto założenie, że koderów są synchronizowane czasu i dokładnie hello tych samych danych.  

Informacje o RTMP koderów na żywo, zobacz [Obsługa protokołu RTMP usługi multimediów Azure i kodery na żywo](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>Pozyskiwania adresów URL (punkty końcowe)
Kanał zawiera ono wejściowy punkt końcowy (adres URL pozyskiwania) określenie w hello kodera na żywo, więc wypchnąć kodera hello strumieni tooyour kanałów.   

Możesz uzyskać hello adresy URL pozyskiwania, podczas tworzenia kanału hello. Dla tooget możesz tych adresów URL kanału hello nie ma toobe w hello **systemem** stanu. Jeśli wszystko jest gotowe toostart wypychanie danych toohello kanału, kanał hello musi być w hello **systemem** stanu. Po uruchomieniu kanału hello wprowadzania danych można wyświetlić podgląd strumienia za pośrednictwem hello URL podglądu.

Istnieje opcja wprowadzania pofragmentowane MP4 (Smooth Streaming) strumień na żywo za pośrednictwem połączenia SSL. tooingest za pośrednictwem protokołu SSL, upewnij się, że hello tooupdate pozyskiwania tooHTTPS adres URL. Nie można obecnie pozyskiwania RTMP, za pośrednictwem protokołu SSL.

#### <a id="keyframe_interval"></a>Interwał klatki kluczowej
Podczas korzystania z lokalnymi kodera na żywo toogenerate wielokrotnej szybkości transmisji bitów strumienia, interwał klatki kluczowej powitania określa czas trwania hello hello grupy obrazów (GOP) używany przez tego kodera. Gdy kanał hello otrzyma tego strumienia przychodzącego, można dostarczyć transmisji strumieniowej na żywo tooclient odtwarzanie aplikacji w jednym z następujących formatów hello: Smooth Streaming, dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH) i HTTP Live Streaming (HLS). Podczas prowadzenia transmisji strumieniowych na żywo, HLS zawsze jest dostarczana dynamicznie. Domyślnie usługi Media Services automatycznie oblicza oparte na interwał klatki kluczowej powitania odebrane z kodera na żywo hello hello HLS segmentu pakowania stosunek (fragmenty według segmentu).

Hello w poniższej tabeli przedstawiono sposób obliczania czas trwania segmentu hello:

| Interwał klatki kluczowej | Współczynnik opakowania segment HLS (FragmentsPerSegment) | Przykład |
| --- | --- | --- |
| Mniejsze niż lub równa too3 sekund |3:1 |W przypadku KeyFrameInterval (lub GOP) 2 sekundy, hello domyślne HLS segmentu pakowania stosunek jest 3 too1. Spowoduje to utworzenie segment HLS 6 sekundę. |
| 3 too5 sekundy |2:1 |W przypadku KeyFrameInterval (lub GOP) 4 sekundy, hello domyślne HLS segmentu pakowania stosunek jest 2 too1. Spowoduje to utworzenie segmentu HLS 8 sekundy. |
| Większa niż 5 sekund |1:1 |W przypadku KeyFrameInterval (lub GOP) sekund 6, hello domyślne HLS segmentu pakowania stosunek jest 1 too1. Spowoduje to utworzenie segment HLS 6 sekundę. |

Współczynnik fragmenty na segment hello przez dane wyjściowe i ustawienie FragmentsPerSegment na ChannelOutputHls Konfigurowanie kanału hello, można zmienić.

Możesz również zmienić wartość interwału klatki kluczowej hello, ustawiając właściwość KeyFrameInterval hello na ChanneInput. Jeśli ustawisz jawnie KeyFrameInterval, hello HLS segmentu pakowania stosunek obliczonego FragmentsPerSegment za pomocą reguł hello opisanych powyżej.  

Jeśli musisz jawnie ustawić KeyFrameInterval i FragmentsPerSegment, Media Services użyje hello wartości, które można ustawić.

#### <a name="allowed-ip-addresses"></a>Dozwolonych adresów IP
Można zdefiniować hello adresy IP, które są dozwolone toopublish toothis wideo kanału. Dozwolonych adresów IP można określić jako jedną z następujących hello:

* Pojedynczy adres IP (np. 10.0.0.1)
* Zakres IP, który korzysta z adresu IP i maski podsieci CIDR (na przykład 10.0.0.1/22)
* Zakres IP, który korzysta z adresu IP i maski podsieci dziesiętną kropkami (na przykład 10.0.0.1(255.255.252.0))

Adresy IP nie są określone, jeśli nie ma żadnych definicji reguły, żaden adres IP będzie dozwolona. tooallow dowolnego adresu IP, Utwórz regułę i ustaw wartość 0.0.0.0/0.

### <a name="channel-preview"></a>Podgląd kanału
#### <a name="preview-urls"></a>Adresy URL w wersji zapoznawczej
Kanały zapewniają punktu końcowego podglądu (adres URL w wersji zapoznawczej) Użyj toopreview, a następnie sprawdź strumienia, zanim dalszego przetwarzania i dostarczania.

Po utworzeniu kanału hello można uzyskać adres URL podglądu hello. Możesz tooget hello adresu URL, hello kanału nie ma toobe w hello **systemem** stanu. Po uruchomieniu kanału hello wprowadzania danych można wyświetlić podgląd strumienia.

Obecnie hello podglądu strumienia mogą być dostarczane tylko w pofragmentowane MP4 (Smooth Streaming) format, niezależnie od hello określony typ danych wejściowych. Można użyć hello [Smooth Streaming Monitor kondycji](http://smf.cloudapp.net/healthmonitor) player tootest hello smooth stream. Umożliwia także odtwarzacza Hosted w hello Azure tooview portalu strumienia.

#### <a name="allowed-ip-addresses"></a>Dozwolonych adresów IP
Można zdefiniować adresy IP hello, które są dozwolone punktu końcowego podglądu toohello tooconnect. Jeżeli nie określono żadnych adresów IP, mogą być dowolnego adresu IP. Dozwolonych adresów IP można określić jako jedną z następujących hello:

* Pojedynczy adres IP (np. 10.0.0.1)
* Zakres IP, który korzysta z adresu IP i maski podsieci CIDR (na przykład 10.0.0.1/22)
* Zakres IP, który korzysta z adresu IP i maski podsieci dziesiętną kropkami (na przykład 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>Kanał danych wyjściowych
Informacje dla kanału danych wyjściowych, zobacz hello [interwał klatki kluczowej](#keyframe_interval) sekcji.

### <a name="channel-managed-programs"></a>Programy zarządzane przez kanał
Kanał jest skojarzony z programami, której można toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają programami. Witaj relacja kanału i programu jest bardzo podobne tootraditional nośnik, gdzie kanał ma stały strumień zawartości, a program zdarzeń zakresie toosome upłynął, w tym kanale.

Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **okno archiwum** długości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin. Długość okna archiwum określa również dostępny hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Programy mogą być transmitowane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każdy program jest skojarzony z zasobu, który przechowuje hello strumieniowo zawartość. Zasób jest kontenera obiektów blob bloku tooa mapowane na koncie magazynu Azure hello i pliki hello w hello zasobów są przechowywane jako obiekty BLOB w tym kontenerze. program hello toopublish tak klientów można wyświetlić hello strumienia, należy utworzyć Lokalizator OnDemand dla hello skojarzonych zasobów. Można użyć tego toobuild lokalizatora adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree jednocześnie uruchomione programy, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Można publikowanie i archiwizację różnych części wydarzenia, zgodnie z potrzebami. Na przykład załóżmy, że konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast hello tylko ostatnich 10 minut. tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy. Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Hello inny program jest zestaw tooarchive przez 10 minut, a ten program zostanie opublikowany.

Nie należy używać ponownie istniejących programów dla nowych zdarzeń. Zamiast tego należy utworzyć nowy program dla każdego zdarzenia. Uruchom hello program, gdy wszystko jest gotowe toostart przesyłania strumieniowego i archiwizacji. Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.

toodelete zarchiwizowane zawartość, Zatrzymaj i Usuń hello program, a następnie usuń hello skojarzonego elementu zawartości. Nie można usunąć elementu zawartości, jeśli program używa jej. Najpierw należy usunąć Hello program.

Nawet po zatrzymaniu i usunięciu hello program, użytkownicy mogą strumieniowo zarchiwizowaną zawartość wideo na żądanie, do momentu usunięcia hello zasobów. Jeśli tooretain hello zarchiwizowane zawartość, ale nie jest dostępny do przesyłania strumieniowego, Usuń hello przesyłania strumieniowego lokalizatora.

## <a id="states"></a>Stany kanału i rozliczeń
Możliwe wartości dla bieżącego stanu hello kanału:

* **Zatrzymano**: jest to stan początkowy hello hello kanału po jego utworzeniu. W tym stanie można zaktualizować właściwości kanału hello, ale przesyłania strumieniowego nie jest dozwolone.
* **Uruchamianie**: kanał hello jest uruchamiana. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa. Jeśli wystąpi błąd, kanał hello zwraca toohello **zatrzymane** stanu.
* **Uruchomiona**: hello kanału może przetwarzać strumienie na żywo.
* **Zatrzymywanie**: kanał hello jest zatrzymywana. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.
* **Usuwanie**: kanał hello jest usuwany. W tym stanie nie są dozwolone ani aktualizacje, ani transmisja strumieniowa.

Witaj poniższej tabeli przedstawiono sposób kanału stany trybu rozliczeń toohello mapy.

| Stan kanału | Wskaźniki interfejsu użytkownika portalu | Naliczanie opłat? |
| --- | --- | --- | --- |
| **Uruchamianie** |**Uruchamianie** |Nie (stan przejściowy) |
| **Uruchomiona** |**Gotowe** (nie uruchomione programy)<p><p>lub<p>**Przesyłanie strumieniowe** (co najmniej jeden uruchomiony program) |Tak |
| **Zatrzymywanie** |**Zatrzymywanie** |Nie (stan przejściowy) |
| **Zatrzymana** |**Zatrzymana** |Nie |

## <a id="cc_and_ads"></a>Zamknięte wstawiania podpisów i usługi ad
Witaj w poniższej tabeli przedstawiono obsługiwane standardy kodowane i wstawiania reklam.

| Standardowa | Uwagi |
| --- | --- |
| CEA 708 i EIA 608 (708/608) |CEA 708 i EIA 608 są kodowane standardy hello Stanów Zjednoczonych i Kanady.<p><p>Obecnie podpisów jest obsługiwana tylko wtedy, gdy w hello zakodowanego strumienia wejściowego. Należy toouse kodera na żywo nośnika, który można wstawić 608 lub 708 podpisów hello zakodowanego strumienia, który wysłał tooMedia usług. Usługa Media Services dostarcza zawartość hello z przeglądarki tooyour wstawionego podpisów. |
| TTML wewnątrz .ismt (Smooth Streaming ścieżek tekstu) |Dynamiczne tworzenie pakietów usługi Media Services umożliwia zawartości toostream klientów w jednym z następujących formatów hello: DASH, HLS lub Smooth Streaming. Jednak jeśli użytkownik pozyskiwania pofragmentowany plik MP4 (Smooth Streaming) z napisami wewnątrz .ismt (Smooth Streaming ścieżek tekstu), można dostarczyć tooonly strumienia hello Smooth Streaming klientów. |
| SCTE 35 |SCTE 35 to cyfrowe sygnalizowania system, który został użyty toocue wstawiania reklam. Podrzędny odbiornikami używać hello sygnału toosplice reklamy w strumieniu hello hello wyznaczony czas. SCTE 35 należy wysłać jako rozrzedzony śledzenie w hello strumień wejściowy.<p><p>Obecnie jest pofragmentowana hello obsługiwane tylko strumień wejściowy formatu, który prowadzi sygnały ad MP4 (Smooth Streaming). format danych wyjściowych Hello tylko obsługiwane jest również Smooth Streaming. |

## <a id="considerations"></a>Zagadnienia dotyczące
Podczas korzystania z lokalnymi kodera na żywo toosend kanał tooa strumienia wielokrotnej szybkości transmisji bitów, zastosuj hello następujące ograniczenia:

* Upewnij się, że masz wystarczające wolne Internet łączności toosend danych toohello pozyskiwania punktów.
* Adres URL pozyskiwania, przy użyciu dodatkowej wymaga dodatkowe ograniczenie użycia przepustowości.
* przychodzący strumień wielokrotnej szybkości transmisji bitów Hello może mieć maksymalnie 10 poziomy jakości wideo (warstwy) i maksymalnie 5 ścieżki audio.
* Hello najwyższej średniej szybkości transmisji bitów do dowolnego poziomu jakości wideo hello powinno być niższe niż 10 MB/s.
* Witaj agregacji hello średniej szybkości transmisji bitów dla wszystkich strumieni audio i wideo hello powinno być niższe niż 25 MB/s.
* Nie można zmienić hello protokołu wejściowego, gdy hello kanał lub skojarzone z nim programy są uruchomione. Jeśli potrzebujesz różnych protokołów, utwórz osobny kanał dla każdego protokołu wejściowego.
* Może obsługiwać pojedynczej szybkości transmisji bitów w kanału. Ale ponieważ hello kanału nie przetwarza strumień hello, aplikacje klienckie hello również otrzymają strumień o pojedynczej szybkości transmisji bitów. (Nie zaleca się tę opcję.)

Inne zagadnienia dotyczące tooworking powiązane z kanałów i powiązane składniki są następujące:

* Za każdym razem, gdy skonfigurujesz hello kodera na żywo, wywołaj hello **zresetować** metody w kanale hello. Zanim je zresetujesz kanału hello masz toostop hello program. Po zresetowaniu hello kanału, uruchom ponownie hello program.
* Kanał można zatrzymać tylko wtedy, gdy jest on hello **systemem** stanu i wszystkie programy na kanale hello zostały zatrzymane.
* Domyślnie można dodać konta usługi Media Services tooyour tylko 5 kanałów. Aby uzyskać więcej informacji, zobacz [przydziały i ograniczenia](media-services-quotas-and-limitations.md).
* Są rozliczane tylko wtedy, gdy kanał w hello **systemem** stanu. Aby uzyskać więcej informacji, zobacz toohello [kanału stanów i rozliczeń](media-services-live-streaming-with-onprem-encoders.md#states) sekcji.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Opinia
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Powiązane tematy
[Specyfikacja pozyskiwania Azure Media Services MP4 pofragmentowane na żywo](media-services-fmp4-live-ingest-overview.md)

[Omówienie usługi Azure Media Services i typowe scenariusze](media-services-overview.md)

[Pojęcia dotyczące usługi Media Services](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
