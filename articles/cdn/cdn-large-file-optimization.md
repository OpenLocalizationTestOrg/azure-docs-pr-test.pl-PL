---
title: "Optymalizacja pobierania pliku aaaLarge za pośrednictwem hello Azure Content Delivery Network"
description: "Optymalizacja wyjaśniono szczegółowo pobieranie dużych plików"
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
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Optymalizacja pobierania plików o dużym za pośrednictwem hello Azure Content Delivery Network

Rozmiary plików zawartości dostarczane za pośrednictwem Internetu hello nadal toogrow płatności funkcji tooenhanced, ulepszonemu i zawartość multimedialną. Wzrostu jest wymuszany przez wiele czynników: penetracji komórkowej łączności szerokopasmowej, większe urządzeń niedrogich magazynów, powszechnie zwiększenia wysokiej rozdzielczości wideo i podłączonej do Internetu urządzeń (IoT). Mechanizm dostarczania szybkich i wydajnych dużych plików jest krytyczne tooensure środowisko płynne i jest przyjemne konsumenta.

Dostarczanie dużych plików ma kilka problemów. Najpierw hello Średni czas toodownload dużego pliku może być istotne, ponieważ aplikacje nie może pobrać wszystkie dane sekwencyjnie. W niektórych przypadkach aplikacje mogą pobierać hello ostatnia część pliku przed hello pierwszej części. Wymagany jest mała ilość pliku lub zatrzymaniu pobieranie, pobierania hello może zakończyć się niepowodzeniem. pobierania Hello również może być opóźnione aż po hello sieci dostarczania zawartości (CDN) pobiera hello całego pliku z serwera źródłowego hello. 

Po drugie hello opóźnienia między komputerem użytkownika i plików hello określa szybkość hello jaką mogą wyświetlać zawartość. Ponadto sieci przeciążona i pojemności problemów miały wpływ na przepustowość. Większej odległości między serwerami i użytkownicy utworzyć dodatkowe możliwości toooccur utraty pakietów, co zmniejsza jakości. Witaj obniżenie jakości spowodowane ograniczonej przepustowości i utraty pakietów zwiększona wydłużyć czas oczekiwania hello toofinish pobierania pliku. 

Trzecie wielu dużych plików nie są dostarczane w całości. Użytkownicy mogą anulować pobieranie w połowie lub Obejrzyj tylko hello pierwszych kilku minut długi wideo MP4. W związku z tym oprogramowania oraz nośnika dostarczania firmach toodeliver tylko części hello żądanego pliku. Skutecznej dystrybucji hello żądanej części zmniejsza ruch wychodzący hello z serwera źródłowego hello. Efektywne dystrybucji zmniejsza hello pamięci i wykorzystanie we/wy na powitania serwera źródłowego. 

Hello Azure Content Delivery Network from Akamai oferuje teraz funkcja, która dostarcza dużych plików wydajnie toousers między Witaj świecie na dużą skalę. Funkcja Hello zmniejsza opóźnienia, ponieważ redukuje hello obciążenia hello pochodzenia serwerów. Ta funkcja jest dostępna z warstwy cenowej standardowa Akamai hello.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Konfigurowanie dostarczania toooptimize punktu końcowego CDN dużych plików

Można skonfigurować dostarczania toooptimize punkt końcowy sieci CDN dla dużych plików za pomocą hello portalu Azure. Można również użyć naszych interfejsów API REST lub dowolną z hello klienta toodo zestawów SDK to. Hello następujących krokach przedstawiono proces hello za pośrednictwem hello portalu Azure.

1. nowy punkt końcowy na powitania tooadd **profilu CDN** wybierz pozycję **punktu końcowego**.

    ![Nowy punkt końcowy](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. W hello **zoptymalizowane pod kątem** listy rozwijanej wybierz **pobierania plików o dużym**.

    ![Wybrane optymalizacji dużych plików](./media/cdn-large-file-optimization/02_Creating.png)


Po utworzeniu punktu końcowego CDN hello stosuje hello optymalizacje dużych plików dla wszystkich plików spełniających określone kryteria. powitania po sekcji opisano tego procesu.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Optymalizuj pod kątem dostarczania dużych plików z hello Azure Content Delivery Network from Akamai

Funkcja typu optymalizacji plików o dużym Hello włącza optymalizacje i konfiguracje toodeliver dużych plików sieciowych szybciej i bardziej responsively. Dostarczania ogólne sieci web z Akamai przechowuje pliki tylko poniżej 1,8 GB i można tunelu (nie pamięci podręcznej) pliki zapasowej too150 GB. Optymalizacja plików o dużym buforuje pliki zapasowej too150 GB.

Optymalizacja dużych plików ma zastosowanie, gdy są spełnione określone warunki. Warunki uwzględnić sposób działania serwera źródłowego hello hello rozmiarów i typów plików hello, które są wymagane. Aby uzyskać szczegółowe informacje na następujące tematy, uzyskujemy zapoznaj się działania hello optymalizacji. 

### <a name="object-chunking"></a>Obiekt podziału 

Hello Azure Content Delivery Network from Akamai stosowana jest metoda o nazwie obiektu podziału. Po zażądaniu dużego pliku hello CDN pobiera mniejsze części pliku hello pochodzenia hello. Po hello CDN krawędzi/serwer protokołu POP odbiera żądanie pliku full lub zakresu bajtów, sprawdza, czy typ pliku hello jest obsługiwana dla tego rodzaju optymalizacji. Sprawdza również, czy typ pliku hello spełnia wymagania dotyczące rozmiaru pliku hello. Jeśli rozmiar pliku hello jest większa niż 10 MB, serwer graniczny CDN hello żąda pliku hello pochodzenia hello w fragmentów 2 MB. 

Po fragmentu hello dociera hello krawędzi CDN, ma ona w pamięci podręcznej i natychmiast obsłużone toohello użytkownika. następnie prefetches hello dalej fragmentu równolegle Hello CDN. To pobieranie z wyprzedzeniem gwarantuje, że zawartość hello jest jednym fragmencie wcześniejsze hello użytkownika, co zmniejsza opóźnienia. Ten proces jest kontynuowany do momentu hello cały plik jest pobierany (jeśli jest to wymagane), wszystkich zakresów bajtów dostępnych (jeśli jest to wymagane), lub powitania klienta kończy hello połączenia. 

Aby uzyskać więcej informacji na powitania żądania zakresu bajtów, zobacz [RFC 7233](https://tools.ietf.org/html/rfc7233).

Witaj CDN buforuje wszelkie fragmenty po odebraniu. Witaj cały plik nie ma toobe buforowane w pamięci podręcznej CDN hello. Kolejne żądania dla zakresów pliku lub byte hello są udostępniane z hello CDN pamięci podręcznej. Jeśli nie wszystkie fragmenty hello są buforowane na powitania CDN, pobieranie z wyprzedzeniem to toorequest używanych fragmentów hello pochodzenia. Tego rodzaju optymalizacji, zależy od możliwości hello hello pochodzenia serwera toosupport zakresu bajtów żądań. _Jeśli serwer pochodzenia hello nie obsługuje żądania zakresu bajtów, optymalizacja nie jest skuteczne._ 

### <a name="caching"></a>Buforowanie
Optymalizacja dużych plików używa czas buforowania wygaśnięcia różne domyślne od dostarczania ogólne sieci web. Program rozróżnia buforowanie dodatnią i ujemną buforowanie na podstawie kodów odpowiedzi HTTP. Jeśli serwer pochodzenia hello określa czas wygaśnięcia za pośrednictwem nagłówka cache-control lub nagłówek odpowiedzi hello wygaśnięcia, hello CDN honoruje tej wartości. Gdy nie określono źródła hello i plik hello zgodny hello typ i rozmiar warunki dla tego typu optymalizacji, hello CDN używane wartości domyślne hello optymalizacji dużych plików. W przeciwnym razie hello CDN używa ustawień domyślnych w celu dostarczania ogólne sieci web.


|    | Ogólne sieci web | Optymalizacja dużych plików 
--- | --- | --- 
Buforowanie: dodatnią <br> HTTP 200, 203, 300, <br> 301, 302 i 410 | 7 dni |1 dzień  
Buforowanie: ujemna <br> HTTP 204, 305, 404, <br> i 405 | Brak | 1 sekunda 

### <a name="deal-with-origin-failure"></a>Postępowania w przypadku niepowodzenia źródła

Długość limitu czasu odczytu pochodzenia Hello zwiększa się z dwóch sekund minut tootwo dostarczania ogólne sieci web dla typu optymalizacji plików o dużym hello. Liczbę kont hello większy plik rozmiary tooavoid przedwczesny limit czasu połączenia.

Jeśli upłynie limit czasu połączenia, hello CDN ponowi próbę wiele razy przed wysłaniem klienta toohello błąd "504 — Limit czasu bramy". 

### <a name="conditions-for-large-file-optimization"></a>Warunki dla optymalizacji dużych plików

Hello w poniższej tabeli wymieniono hello zestaw kryteriów toobe spełnić w celu optymalizacji dużych plików:

Warunek | Wartości 
--- | --- 
Obsługiwane typy plików | 3g, 2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> GZ, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> MPEG, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Minimalny rozmiar pliku | 10 MB 
Maksymalny rozmiar pliku | 150 GB 
Właściwości serwera pochodzenia | Musi obsługiwać żądania zakresu bajtów 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Optymalizuj pod kątem dostarczania dużych plików z hello Azure Content Delivery Network from Verizon

Hello Azure Content Delivery Network from Verizon oferuje duże pliki bez ograniczenie rozmiaru pliku. Dodatkowe funkcje są włączone przez domyślnego dostarczania toomake dużych plików szybciej.

### <a name="complete-cache-fill"></a>Wypełnienie pamięci podręcznej ukończone

Funkcja wypełnienia pamięci podręcznej pełną domyślnych Hello umożliwia hello CDN toopull pliku do pamięci podręcznej hello podczas żądania początkowego jest porzucone lub utraty. 

Najbardziej przydatny w przypadku dużych zasobów jest wypełnienie pamięci podręcznej ukończone. Zwykle użytkownicy nie pobrać je z start toofinish. Używają pobierania progresywnego. zachowanie domyślne Hello wymusza hello krawędzi serwera tooinitiate pobieranie w tle trwałego hello z serwera źródłowego hello. W efekcie hello zasobów jest w lokalnej pamięci podręcznej serwera granicznego hello. Po pełnej obiekt hello znajduje się w pamięci podręcznej hello, serwer graniczny hello spełnia toohello żądania zakresu bajtów CDN dla hello obiektu w pamięci podręcznej.

Witaj domyślne zachowanie można wyłączyć za pomocą hello aparatu reguł w hello warstwy Verizon Premium.

### <a name="peer-cache-fill-hot-filing"></a>Równorzędna pamięć podręczna wypełnienia hot zgłoszenia

Hello domyślne równorzędnej pamięci podręcznej wypełnienia hot zgłoszenia funkcji używa zaawansowane algorytmu. Używa dodatkowe krawędzi buforowanie serwery oparte na przepustowość i agregacji żądania żądania klienta toofulfill metryki dla dużych, bardzo popularny obiektów. Ta funkcja zapobiega sytuacji, w którym dużej liczby dodatkowych żądań są wysyłane na serwer pochodzenia tooa użytkownika. 

### <a name="conditions-for-large-file-optimization"></a>Warunki dla optymalizacji dużych plików

funkcje optymalizacji Hello Verizon jest domyślnie włączona. Na maksymalny rozmiar pliku nie ma żadnych ograniczeń. 

## <a name="additional-considerations"></a>Dodatkowe zagadnienia

Należy wziąć pod uwagę następujące dodatkowe aspekty dla tego typu optymalizacji hello.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Usługa Azure Content Delivery Network from Akamai

- Witaj podziału procesu generuje serwera pochodzenia toohello dodatkowych żądań. Jednak hello ogólne dostarczane z hello źródła danych jest znacznie mniejszy. Powoduje segmentu lepsze buforowania charakterystyce hello CDN.

- Pamięć i wykorzystanie we/wy zostały zredukowane pochodzenia hello, ponieważ mniejsze części pliku hello są dostarczane.

- Dla fragmentów w pamięci podręcznej na powitania CDN nie ma żadnych dodatkowych żądań pochodzenia toohello do momentu wygaśnięcia zawartości hello lub zostanie usunięty z pamięci podręcznej hello.

- Użytkownicy mogą wprowadzać zakresu żądań toohello CDN i traktowane jak normalne pliki. Optymalizacja ma zastosowanie tylko wtedy, gdy jest prawidłowy typ pliku i zakres bajtów hello jest od 10 MB do 150 GB. Jeśli żądany rozmiar pliku średni hello jest mniejsza niż 10 MB, zamiast tego może być toouse dostarczania ogólne sieci web.

### <a name="azure-content-delivery-network-from-verizon"></a>Usługa Azure Content Delivery Network from Verizon

Typ optymalizacji dostarczania ogólne web Hello zapewnia dużych plików.
