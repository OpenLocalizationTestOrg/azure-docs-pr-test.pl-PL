---
title: "inspekcję aaaPacket z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak zbierane toouse inspekcję pakietów tooperform obserwatora sieciowego z maszyny Wirtualnej"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Inspekcję pakietów z obserwatora sieciowego Azure

Za pomocą funkcji przechwytywania pakietów hello obserwatora sieciowego, można zainicjować i zarządzanie sesjami przechwytywania na maszynach wirtualnych platformy Azure z hello portalu programu PowerShell, interfejsu wiersza polecenia i programowo przy użyciu hello zestawu SDK i interfejsu API REST. Przechwytywania pakietów umożliwia scenariusze tooaddress, które wymagają danych na poziomie pakietów, zapewniając hello informacji w formacie łatwo można używać. Wykorzystanie danych hello tooinspect bezpłatnych narzędzi, możesz sprawdzić tooand komunikacji z maszyn wirtualnych i uzyskać wgląd w ruchu sieciowego. Niektóre przykładowe zastosowania danych przechwytywania pakietów obejmują: do badania problemów dotyczących sieci lub aplikacji, wykrywanie prób nieprawidłowego użycia i nieautoryzowanego dostępu sieciowego lub utrzymania zgodności z przepisami. W tym artykule zostanie przedstawiony sposób tooopen pliku przechwytywania pakietów udostępniane przez obserwatora sieciowego przy użyciu narzędzia popularnych typu open source. Firma Microsoft udostępni również przykładami przedstawiający sposób zidentyfikować ruch nietypowe toocalculate opóźnienie połączenia i sprawdź statystyki sieci.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przechodzi przez niektóre scenariusze wstępnie skonfigurowane na przechwytywania pakietów, która została wcześniej uruchomiona. Te scenariusze przedstawiono możliwości, które są dostępne, przeglądając przechwytywania pakietów. W tym scenariuszu [WireShark](https://www.wireshark.org/) przechwytywania pakietów hello tooinspect.

W tym scenariuszu przyjęto założenie, że był już uruchamiany przechwytywania pakietów na maszynie wirtualnej. toolearn jak toocreate przechwytywania pakietów, odwiedź [Przechwytywanie pakietów zarządzania za pomocą portalu hello](network-watcher-packet-capture-manage-portal.md) lub REST odwiedzając [z interfejsu API REST zarządzania Przechwytywanie pakietów](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Scenariusz

W tym scenariuszu należy:

* Przejrzyj przechwytywania pakietów

## <a name="calculate-network-latency"></a>Oblicz opóźnienia sieci

W tym scenariuszu zostanie przedstawiony sposób tooview hello początkowej obiegu czasu (RTT) między dwoma punktami końcowymi konwersacji Transmission Control Protocol (TCP).

Po nawiązaniu połączenia TCP hello pierwsze trzy pakiety wysyłane w ramach połączenia hello wykonaj wzorzec często określana tooas hello trójstopniowego. Sprawdzając hello najpierw dwa pakiety przesyłane w tym uzgadniania, żądania początkowego powitania klienta i odpowiedzi z serwera hello możemy obliczyć hello opóźnienia podczas tego połączenia. To opóźnienie jest hello tooas określonego czasu obiegu (RTT). Więcej informacji na temat protokołu TCP hello i uzgadniania trójstopniowego hello można znaleźć toohello następującego zasobu. https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-Handshake-VIA-TCP-IP

### <a name="step-1"></a>Krok 1

Uruchamianie programu WireShark

### <a name="step-2"></a>Krok 2

Witaj obciążenia **CAP** plik z sieci przechwytywania pakietów. Ten plik znajduje się w obiekcie blob hello został zapisany w naszym lokalnie na maszynie wirtualnej hello, w zależności od tego, jak został skonfigurowany.

### <a name="step-3"></a>Krok 3

tooview hello początkowej obiegu czasu (RTT) konwersacji TCP, firma Microsoft będzie tylko patrzeć dwóch pierwszych pakietów hello objętego hello uzgadnianie protokołu TCP. Użyjemy dwóch pierwszych pakietów hello w hello trójstopniowego, które są hello [SYN], [SYN, potwierdzenia] pakietów. Są one nazwane dla flag w nagłówku TCP hello. w tym scenariuszu nie użyjemy ostatnim pakiecie Hello w hello uzgadniania pakietów hello [potwierdzenia]. Pakiet HELLO [SYN] jest wysyłany przez powitania klienta. Po odebraniu hello serwer wysyła pakietów hello [potwierdzenia] jako potwierdzenia otrzymania hello SYN z powitania klienta. Wykorzystanie hello fakt, że odpowiedź serwera hello wymaga bardzo małego obciążenia, możemy obliczyć powitalne RTT przez odjęcie czas hello pakietów hello [SYN, potwierdzenia] otrzymała przez klienta na powitania hello czasu [SYN] pakiet został wysłany przez powitania klienta.

Za pomocą programu WireShark ta wartość jest obliczana firmie Microsoft.

toomore łatwe przeglądanie dwóch pierwszych pakietów hello w hello TCP trójstopniowego, firma Microsoft będzie wykorzystywać hello oferowana przez WireShark możliwość filtrowania.

Filtr hello tooapply w WireShark, rozwiń hello segmentu "Transmission Control Protocol" [SYN] pakietu w Twojej przechwytywania i zbadać flag hello w nagłówku TCP hello.

Ponieważ czekamy toofilter na wszystkich [SYN] i [SYN potwierdzenia] pakiety, w obszarze flagi cofirm ustawiono hello Syn bit too1, a następnie kliknięcie prawym przyciskiem na powitania Syn bit -> Zastosuj jako filtr -> wybrane.

![Rysunek 7][7]

### <a name="step-4"></a>Krok 4

Teraz, gdy zostały przefiltrowane hello okna tooonly Zobacz pakiety z hello [SYN] bitu, można łatwo wybrać konwersacje myślisz tooview hello RTT początkowej. Prosty sposób tooview hello RTT w WireShark wystarczy kliknąć listy rozwijanej hello oznaczone jako "SEQ/potwierdzenia" analizy. Zostanie wtedy wyświetlone powitalne RTT wyświetlane. W takim przypadku hello RTT został 0.0022114 sekund lub 2.211 ms.

![rysunek 8][8]

## <a name="unwanted-protocols"></a>Protokoły niechciane

Może mieć wiele aplikacji uruchomionych w wystąpieniu maszyny wirtualnej wdrożonej na platformie Azure. Wiele z tych aplikacji komunikują się za pośrednictwem sieci hello, być może bez Twojej zgody jawnej. Za pomocą komunikacji sieciowej toostore przechwytywania pakietów, możemy Sprawdź jak mówimy więc na powitania sieci i Wyszukaj problemy w aplikacji.

W tym przykładzie firma Microsoft analizuje poprzedniego uruchomienia przechwytywania pakietów dla niechciane protokołów, które mogą wskazywać nieautoryzowanego komunikacji z aplikacji na komputerze.

### <a name="step-1"></a>Krok 1

Przy użyciu hello tego samego przechwytywania w poprzednim kliknij scenariusz hello **statystyki** > **protokołu hierarchii**

![Protokół hierarchii menu][2]

zostanie wyświetlone okno hierarchii protokołu Hello. Ten widok zawiera listę wszystkich protokołów hello, które były używane podczas sesji przechwytywania hello i hello liczba pakietów wysłanych i odebranych za pomocą protokołów hello. Ten widok może być przydatne do znajdowania niechciane ruchu sieciowego na maszynach wirtualnych lub w sieci.

![Hierarchia elementów protokołu otwarty][3]

Jak widać w powitania po Przechwytywanie ekranu wystąpił ruchu przy użyciu protokołu BitTorrent hello, który jest używany do udostępniania plików toopeer elementu równorzędnego. Jako administrator nie będzie toosee BitTorrent ruchu w przypadku tego konkretnego maszyn wirtualnych. Teraz należy pamiętać o tego rodzaju ruch, usunięciem hello równorzędnej toopeer oprogramowania instalowanego na tej maszynie wirtualnej lub bloku hello ruchu przy użyciu grup zabezpieczeń sieci i zapory. Ponadto może wybrać przechwytywania pakietów toorun zgodnie z harmonogramem, możesz przejrzeć hello Użyj protokołu regularnie na maszynach wirtualnych. Na przykład na jak sieci tooautomate zadania w programie azure odwiedziny [monitorowania zasobów sieciowych przy użyciu usługi Automatyzacja azure](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Znajdowanie Najpopularniejsze miejsca docelowe i porty

Opis typów hello ruchu, hello punktów końcowych i przekazywane za pośrednictwem portów hello jest ważne podczas monitorowania i rozwiązywania problemów z aplikacji i zasobów w sieci. Przy użyciu pliku przechwytywania pakietów z powyższych, firma Microsoft szybko informacje hello Najpopularniejsze miejsca docelowe naszych maszyny Wirtualnej komunikuje się i hello porty jej użycia.

### <a name="step-1"></a>Krok 1

Przy użyciu hello tego samego przechwytywania w poprzednim kliknij scenariusz hello **statystyki** > **statystyki IPv4** > **miejsc docelowych i porty**

![Okno przechwytywania pakietów][4]

### <a name="step-2"></a>Krok 2

Szukamy za pośrednictwem wyników hello oznaczyć linii, było wiele połączeń na porcie 111. został Hello najczęściej używane portu 3389, czyli pulpitu zdalnego, a pozostałe hello są dynamiczne porty RPC.

Podczas tego ruchu może oznaczać nic, jest port, który był używany dla wielu połączeń i jest administratorem toohello nieznany.

![Rysunek 5][5]

### <a name="step-3"></a>Krok 3

Teraz, Ustaliliśmy jest za mało miejsca portu firma Microsoft można filtrować naszych przechwytywania na podstawie hello portu.

Filtr Hello w tym scenariuszu należy:

```
tcp.port == 111
```

Możemy wprowadzić w polu tekstowym filtru hello tekstem filtru hello z powyższych i naciśnij klawisz enter.

![Rysunek 6.][6]

Z wyników hello możemy stwierdzić, cały ruch hello pochodzi z lokalnej maszyny wirtualnej na powitania tej samej podsieci. Jeśli nadal nie Rozumiemy Dlaczego występuje ten ruch, możemy dalsze inspekcję toodetermine pakietów hello dlaczego jest wprowadzenie tych połączeń na porcie 111. Dzięki tym informacjom firma Microsoft może potrwać hello odpowiednią akcję.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o hello inne funkcje diagnostyczne obserwatora sieciowego odwiedzając [omówienie monitorowania sieci platformy Azure](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













