---
title: "aaaDynamic przyspieszenie lokacji za pomocą usługi Azure CDN"
description: "Dynamiczne witryny przyspieszenie nowości"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Akceleracja dynamiczne witryny za pomocą usługi Azure CDN

Z rozłożenie hello mediów społecznościowych, handlu elektronicznego i hello hyper spersonalizowanych w sieci web szybko rośnie procent hello zawartości obsługiwanej tooend użytkowników jest generowany w czasie rzeczywistym. Użytkownicy oczekują aplikacje sieci web szybkie, niezawodne i spersonalizowane, niezależnie od przeglądarki, lokalizacji, urządzenia lub sieci. Jednak hello bardzo i innowacje dotyczące wchodzące w tych środowisk, dlatego współpraca również powolna strona pliki do pobrania zagrożenie hello jakości obsługi klienta hello. 

Standardowa możliwość CDN obejmuje hello możliwości toocache pliki bliżej tooend użytkowników toospeed dostarczenia plików statycznych. Jednak z dynamicznych aplikacji sieci web, buforowanie tej zawartości w lokalizacjach edge nie jest możliwe, ponieważ serwer hello generuje zawartość hello w zachowaniu toouser odpowiedzi. Przyspieszenie hello dostarczania zawartości, takich jest bardziej złożone niż tradycyjne krawędzi buforowanie i wymaga precyzyjne Dostraja każdego elementu w ścieżce danych powitania od chwili rozpoczęcia toodelivery rozwiązanie end-to-end. Z usługi Azure CDN dynamiczne lokacji Acceleration (DSA), widoczny zwiększona wydajność hello stron sieci web z zawartością dynamiczną.

Azure CDN from Akamai i Verizon oferuje DSA optymalizacji za pośrednictwem hello **zoptymalizowane pod kątem** menu podczas tworzenia punktu końcowego.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Konfigurowanie dostarczania tooaccelerate punktu końcowego CDN plików dynamicznych

Można skonfigurować dostarczania toooptimize punkt końcowy sieci CDN dynamicznych plików za pośrednictwem portalu Azure, wybierając hello **przyspieszenie dynamiczne witryny** opcję w obszarze hello **zoptymalizowane pod kątem** wybór właściwości podczas utworzenie punktu końcowego Hello. Można również użyć naszych interfejsów API REST lub samo żadnego powitania klienta zestawów SDK toodo hello programowo. 

### <a name="probe-path"></a>Ścieżka sondy
Ścieżka sondy jest funkcja tooDynamic określonych przyspieszenie lokacji i prawidłowego jest wymagana do utworzenia. DSA używa małą *ścieżki sondowania* plik umieszczony na powitania pochodzenia toooptimize routingu konfigurację sieci dla hello CDN. Można pobierać i przekaż witryny przykładowy plik tooyour lub użyć istniejącego zasobu DS, który jest około 10 KB dla ścieżki sondowania hello zamiast hello zasobów istnieje.

> [!Note]
> DSA wiąże się z dodatkowych opłat. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/cdn/) Aby uzyskać więcej informacji.

powitania po zrzuty ekranu przedstawiają procesu hello za pośrednictwem portalu Azure.
 
![Dodawanie nowego punktu końcowego CDN](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Rysunek 1: Dodawanie nowy punkt końcowy CDN z hello profilu CDN*
 
![Tworzenie nowego punktu końcowego CDN za pomocą algorytmu DSA](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Rysunek 2: Tworzenie punktu końcowego usługi CDN za pomocą przyspieszenie lokacji dynamicznej optymalizacji wybrane*

Po utworzeniu punktu końcowego CDN hello stosuje hello DSA optymalizacji dla wszystkich plików spełniających określone kryteria. powitania po sekcji opisano optymalizacji DSA szczegółowo.

## <a name="dsa-optimization-using-azure-cdn"></a>Optymalizacja DSA za pomocą usługi Azure CDN

Dynamiczne przyspieszenie witryny na platformie Azure CDN przyspiesza dostarczania dynamicznych zasobów przy użyciu hello następujące techniki:

-   Optymalizacja trasy
-   Optymalizacje TCP
-   Pobieranie z wyprzedzeniem obiektów (tylko Akamai)
-   Kompresja obrazu przenośnych (tylko Akamai)

### <a name="route-optimization"></a>Optymalizacja trasy

Optymalizacja trasy jest ważne, ponieważ hello Internet jest dynamiczne miejsce, w którym ruch i tymczasowo awarie są ciągle zmieniana hello topologii sieci. Hello protokołu BGP (Border Gateway) jest protokół routingu hello hello internetowych, ale może to być szybsze tras za pomocą pośredniczącej serwerów punktu obecności (PoP). 

Optymalizacja trasy wybiera hello optymalny ścieżki toohello pochodzenia tak, aby witryna jest stale dostępny i dynamicznej zawartości jest dostarczany tooend użytkowników za pośrednictwem hello najszybsze i najbardziej niezawodnym możliwe trasy. 

Witaj Akamai sieci używa danych w czasie rzeczywistym toocollect technik i porównanie różnych ścieżek za pomocą różnych węzłach w hello Akamai serwera, a także trasy protokołu BGP domyślnej hello różnych hello Otwórz Internet toodetermine hello najszybszym trasy między hello pochodzenia i hello Krawędź CDN. Te techniki uniknąć internetowych punktów przeciążenia i długi trasy. 

Podobnie używa sieci Verizon hello kombinację emisji DNS, dużej pojemności obsługuje POP i kontroli kondycji toodetermine hello najlepsze bram toobest trasy danych z hello pochodzenia toohello klienta.
 
W związku z tym dostarczania zawartości w pełni dynamiczne i transakcyjnych szybciej i bardziej niezawodnie tooend użytkowników, nawet wtedy, gdy jest uncacheable. 

### <a name="tcp-optimizations"></a>Optymalizacje TCP

Transmission Control Protocol (TCP) to standard hello zestawu protokołów internetowych hello używane toodeliver informacji między aplikacjami sieci IP.  Domyślnie istnieje kilka kopii i określonymi żądań wymagane tooset się połączenia TCP, jak również limity tooavoid sieci congestions, które powodują wydajność na dużą skalę. Ten problem dotyczy usługi Azure CDN from Akamai optymalizując w trzech obszarach: 

 - Wyeliminowanie start powolne
 - Korzystanie z usług połączeń trwałych
 - dostrajanie parametrów pakietów TCP (tylko Akamai)

#### <a name="eliminating-slow-start"></a>Wyeliminowanie start powolne

*Powolna start* jest częścią hello protokołu TCP, który uniemożliwia przeciążenie sieci, ograniczając hello ilość danych przesyłanych przez sieć hello. Rozpoczyna się od przeciążenia mały rozmiar okna między nadawcą i odbiorcą dopóki nie zostanie osiągnięta maksymalna hello lub wykrycia utraty pakietów.

Azure CDN from Akamai i Verizon eliminuje powolne rozpocznie się za trzy kroki:

1.  Zarówno Akamai i Verizon w sieci za pomocą kondycji i przepustowości monitorowania toomeasure hello przepustowości połączeń między serwerami PoP krawędzi.
2. metryki Hello są współużytkowane serwery krawędzi PoP, aby każdy serwer zna hello się warunków sieciowych i innych POP wokół nich hello kondycję serwera.  
3. serwery krawędzi CDN Hello są teraz możliwe toomake założenia dotyczące niektórych parametrów transmisji, takich jak jakie hello optymalnego rozmiaru okna powinna być podczas komunikowania się z innymi serwerami krawędzi sieci CDN w jego pobliżu. Ten krok oznacza, że rozmiar okna początkowej przeciążenia hello można zwiększyć, jeśli kondycji hello hello połączenia między serwerami krawędzi CDN hello jest w stanie wyższej transferów danych pakietu.  

#### <a name="leveraging-persistent-connections"></a>Korzystanie z usług połączeń trwałych

Za pomocą CDN mniejszej liczby unikatowych maszyn podłączyć serwer pochodzenia tooyour bezpośrednio w porównaniu z użytkowników łączących się bezpośrednio ze źródła — wersja tooyour. Mniejszą liczbę połączeń z pochodzenia hello Azure CDN from Akamai i Verizon również pul tooestablish razem żądania użytkownika.

Jak wspomniano wcześniej, połączeń TCP zająć wiele żądań i z powrotem w tooestablish uzgadniania nowego połączenia. Połączenia trwałe, znanej także jako "HTTP Keep-Alive," ponowne użycie istniejących połączeń TCP dla protokołu HTTP żądania toosave obustronne wielokrotnie i przyspieszenia dostarczania. 

sieci Verizon Hello wysyła również okresowe pakiety utrzymywania aktywności przez tooprevent połączenia TCP hello Otwieranie połączenia z zamknięte.

#### <a name="tuning-tcp-packet-parameters"></a>Dostrajanie parametrów pakietów TCP

Azure CDN from Akamai również Dostraja hello parametry połączenia do serwera i zmniejsza hello ilość długi zasięg round tooretrieve wymaganą zawartości osadzone w witrynie hello przy użyciu hello następujące techniki:

1.  Zwiększanie hello początkowej przeciążenia okna tak, aby więcej pakietów mogą być wysyłane bez oczekiwania na potwierdzenie.
2.  Zmniejszenie limitu czasu początkowej retransmisji hello wykrycia straty, a retransmisji występuje szybciej.
3.  Malejącej hello minimalną i maksymalną przesłania czas oczekiwania hello tooreduce limitu czasu przed przy założeniu, że pakiety zostały utracone podczas transmisji.

### <a name="object-prefetch-akamai-only"></a>Pobieranie z wyprzedzeniem obiektów (tylko Akamai)

Większość witryn sieci Web składają się z strony HTML, który odwołuje się do różnych zasobów takich jak obrazy czy skrypty. Zazwyczaj, gdy klient zażąda strony sieci Web, przeglądarki hello najpierw pobiera analizuje hello obiektu HTML i następnie sprawia, że dodatkowe zasoby toolinked, które są wymagane toofully załadowania strony hello żądań. 

*Pobieranie z wyprzedzeniem* to technika tooretrieve obrazów i skrypty osadzone w hello strony HTML podczas hello HTML obsługiwanej przeglądarki toohello, a przed hello przeglądarki nawet sprawia, że te żądania obiektu. 

Z hello **pobrana z wyprzedzeniem** opcja jest włączona w czasie powitania po hello CDN służy przeglądarki klienta hello HTML strony podstawowej toohello hello CDN analizuje plik hello HTML i dodatkowych żądania dla wszystkich połączonych zasobów i zapisać ją w pamięci podręcznej. Gdy hello klient wysyła żądania hello hello połączonych zasobów, serwer graniczny CDN hello już ma hello żądane obiekty i może obsługiwać je bezpośrednio bez źródła toohello obiegu. Optymalizacja przynosi korzyści zarówno buforowalnej, jak i buforowalnej zawartości.

### <a name="adaptive-image-compression-akamai-only"></a>Kompresja adaptacyjną obrazu (tylko Akamai)

Niektóre urządzenia, szczególnie przenośnych te wystąpić niższych szybkościach sieci z tootime czasu. W tych scenariuszach więcej przydatne dla mniejszych obrazów tooreceive hello użytkownika w ich strony sieci Web jest szybsze, zamiast czekać zbyt długo dla obrazów pełnej rozdzielczości.

Funkcja ta automatycznie monitoruje jakości sieci i wykorzystuje standardowe metody kompresji JPEG, gdy szybkości sieci są wolniejszej czas dostawy tooimprove.

Kompresja adaptacyjną obrazu | Rozszerzenia plików  
--- | ---  
Kompresja JPEG | jpg, JPEG, jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Buforowanie

Z DSA buforowanie jest domyślnie wyłączona na powitania CDN, nawet wtedy, gdy pochodzenia hello zawiera nagłówki pamięci podręcznej formant/wygasa w hello odpowiedzi. To ustawienie domyślne jest wyłączona, ponieważ DSA jest zazwyczaj używana w przypadku dynamicznych zasoby, które nie mają być buforowane, ponieważ są one unikatowe tooeach klienta i włączenie buforowania domyślnie mogą być dzielone to zachowanie.

Jeśli masz witrynę z różnymi statycznych i dynamicznych zasobów, jest najlepszym tootake hybrydowego podejście tooget hello najlepszą wydajność. 

Jeśli używasz sieci ADN z Verizon Premium, możesz włączyć buforowanie ponownie dla określonych przypadków przy użyciu hello aparat reguł.  

Alternatywą jest toouse dwa punkty końcowe usługi CDN. Z zasobów dynamicznej toodeliver DSA, a inny punkt końcowy z optymalizacją statycznych typu, na przykład ogólne dostarczania sieci web toodelivery buforowalnej zasoby. W tym alternatywnych tooaccomplish kolejności należy zmodyfikować z toolink adresów URL strony sieci Web bezpośrednio toohello zasobów na hello planujesz toouse punktu końcowego CDN. 

Na przykład: `mydynamic.azureedge.net/index.html` stronę dynamicznego i jest załadowany z punktu końcowego DSA hello.  Witaj strony html odwołuje się do wielu zasobów statycznych, takich jak biblioteki języka JavaScript lub obrazów, które są ładowane z hello statycznego punktu końcowego CDN, takich jak `mystatic.azureedge.net/banner.jpg` i `mystatic.azureedge.net/scripts.js`. 

Przykład można znaleźć [tutaj](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) na jak toouse kontrolerów w programie ASP.NET web zawartość tooserve aplikacji przy użyciu określonego adresu URL usługi CDN.




