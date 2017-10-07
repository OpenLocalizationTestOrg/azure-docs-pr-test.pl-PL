---
title: "wskaźniki monitorowania aaaStorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje hello światła — elektroluminescencyjne (LED) i stan hello toomonitor alarm dźwiękowy używany hello urządzenia StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Korzystać z urządzenia StorSimple monitorowania toomanage wskaźników
## <a name="overview"></a>Omówienie
Urządzenia StorSimple zawiera światła — elektroluminescencyjne (LED) i alarmy, których można używać toomonitor hello moduły i ogólny stan hello urządzenia StorSimple. Witaj wskaźników monitorowania można znaleźć w składniki sprzętowe hello obudowa głównej hello urządzenia i obudowy EBOD hello. Hello wskaźników monitorowania może być LED lub dźwiękowe alarmy.

Istnieją trzy LED stanów używane tooindicate hello stan modułu: zielony miga zielony żółtą toored, lub żółtą czerwony.  

* Zielony LED reprezentują prawidłowego stanu operacyjnego.  
* Miga zielony żółtą toored LED reprezentują obecności hello niekrytyczne warunków, które mogą wymagać interwencji użytkownika.  
* LED żółtą czerwony oznacza, że obecne w hello module błąd krytyczny.  

Witaj dalszej części tego artykułu opisano hello różnych monitorowania LED wskaźnika, ich lokalizacji na urządzeniu StorSimple hello, stan urządzenia hello oparty na powitania stanów LED, wraz ze wszystkimi skojarzonymi dźwiękowe alarmy.

## <a name="front-panel-indicator-leds"></a>Wskaźnik panelu przedniego LED
panelu przedniego Hello, nazywany również hello *panelu Operacje* lub *panelu ops*, wyświetla zagregowany stan wszystkich modułów hello hello w systemie hello. panelu przedniego Hello jest identyczne na powitania StorSimple podstawowego i hello obudowa EBOD i poniżej przedstawiono.  

   ![Urządzenie panelu przedniego][1]

panelu przedniego Hello zawiera następujące wskaźniki hello:  

1. Przycisk wyciszenia
2. Wskaźnik zasilania LED (zielony czerwony żółtą)
3. Wskaźnik błędów modułu DOPROWADZIŁY (na czerwono żółtą/wyłączona)
4. Wskaźnik błędów logicznych DOPROWADZIŁY (na czerwono żółtą/wyłączona
5. Wyświetlanie Identyfikatora jednostki  

Witaj główna różnica między panelu przedniego hello LED hello urządzenia oraz na powitania obudowa EBOD jest hello **numeru identyfikacyjnego jednostki systemu** wyświetlane na ekranie powitania LED. jednostki domyślne Hello jest wyświetlana na urządzeniu hello identyfikator **00**, a identyfikator jednostki domyślne hello wyświetlany na powitania obudowa EBOD **01**. Dzięki temu można tooquickly rozróżniania hello urządzenia oraz obudowy EBOD powitania po włączeniu urządzenia hello. Jeśli urządzenie jest wyłączone, użyj hello informacji dostępnych w [włączyć nowe urządzenie](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) toodifferentiate hello urządzenia z hello EBOD obudowy.  

## <a name="front-panel-led-status"></a>Stan LED panelu przedniego
Użyj powitania po stan hello tooidentify tabeli wskazywany przez hello LED na panelu przednim hello hello urządzenia lub hello EBOD obudowy.  

| Zasilania systemu | Błąd modułu | Błąd logiczny | Alarm | Stan |
| --- | --- | --- | --- | --- |
| Żółtą czerwony |WYŁĄCZANIE |WYŁĄCZANIE |Nie dotyczy |Utraty zasilacza korzysta z kopii zapasowej zasilania lub zasilacz i hello kontrolera modułów zostały usunięte. |
| Zielony |ON |ON |Nie dotyczy |Stan testu OPS panelu Włącz (5s) |
| Zielony |WYŁĄCZANIE |WYŁĄCZANIE |Nie dotyczy |Włącz wszystkie funkcje dobra |
| Zielony |ON |Nie dotyczy |Błędów PCM LED, błędów wentylator LED |Żadnych błędów PCM, wentylator usterka, powyżej lub poniżej temperatury |
| Zielony |ON |Nie dotyczy |We/Wy modułu LED |Błąd modułu dowolnego kontrolera |
| Zielony |ON |Nie dotyczy |Nie dotyczy |Obudowa logiki błędów |
| Zielony |Flash |Nie dotyczy |Stan modułu PRZEPROWADZONY w module kontrolera. Błędów PCM LED, błędów wentylator LED |Zainstalowany kontroler nieznany typ modułu, I2C magistrali błąd, błąd konfiguracji kontrolera modułu niezbędne produktu danych (VPD) |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Chłodzenia modułu (PCM) wskaźnik LED zasilania
Wskaźnik modułu (PCM) chłodzenia zasilania LED znajduje się na hello obu obudowa głównej hello lub obudowa EBOD dla każdego modułu PCM. W tym temacie omówiono sposób hello toouse po LED toomonitor hello stan urządzenia StorSimple.  

* LED PCM dla podstawowego obudowa hello
* Wskaźniki LED PCM hello obudowa EBOD

## <a name="pcm-leds-for-hello-primary-enclosure"></a>LED PCM dla podstawowego obudowa hello
urządzenie StorSimple Hello ma Moduł PCM 764W o dodatkowe baterii. Witaj poniższej ilustracji przedstawiono panelu LED hello hello urządzenia.  

   ![PCM LED hello obudowa podstawowego][2]

Legenda LED:

1. Ak awarii zasilania
2. Wentylator awarii
3. Uszkodzenia
4. PCM OK
5. Błąd kontrolera domeny
6. Dobrym baterii  

Stan Hello hello PCM jest umieszczona na powitania PRZEPROWADZONY panelu. panel PCM LED urządzenia Hello ma sześć LED. Cztery te LED wyświetlany stan hello hello zasilania i wentylator hello. pozostałe dwie LED Hello wskazują stan hello hello modułu baterii kopii zapasowej w hello PCM. Można użyć następujących tabel toodetermine hello stan hello PCM hello.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Wskaźnik PCM LED zasilania i wentylatora
| Stan | PCM OK (zielony) | Niepowodzenie AC (żółte) | Wentylator kończyć się niepowodzeniem (żółte) | Niepowodzenie kontrolera domeny (żółte) |
| --- | --- | --- | --- | --- |
| Nie zasilacza (tooenclosure) |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Nie zasilacza (tego PCM tylko) |WYŁĄCZANIE |ON |WYŁĄCZANIE |ON |
| Ak przedstawia PCM ON - OK |ON |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Błędów PCM (niepowodzenie wentylator) |WYŁĄCZANIE |WYŁĄCZANIE |ON |Nie dotyczy |
| Błędów PCM (za pośrednictwem amp za pośrednictwem napięcia przez bieżący) |WYŁĄCZANIE |ON |ON |ON |
| PCM (wentylator poza okresem tolerancji) |ON |WYŁĄCZANIE |WYŁĄCZANIE |ON |
| Tryb wstrzymania |Miga |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Pobranie oprogramowania układowego PCM |WYŁĄCZANIE |Miga |Miga |Miga |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Wskaźnik PCM LED hello kopii zapasowej baterii
| Stan | Baterii dobrą (zielony) | Uszkodzenia (żółtą) |
| --- | --- | --- |
| Brak baterii |WYŁĄCZANIE |WYŁĄCZANIE |
| Baterii obecne i obciążona |ON |WYŁĄCZANIE |
| Procedury ładowania lub konserwacji baterii |Miga |WYŁĄCZANIE |
| "Ciąg soft" uszkodzenia (możliwe do odzyskania) |WYŁĄCZANIE |Miga |
| Błąd "sprzętowy" baterii (nieodwracalny) |WYŁĄCZANIE |ON |
| Pozbawionych baterii |Miga |WYŁĄCZANIE |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>Wskaźniki LED PCM hello obudowa EBOD
Witaj obudowa EBOD ma 580W PCM i nie dodatkowe baterii. panel PCM Hello hello obudowa EBOD ma wskaźnik LED tylko w przypadku hello zasilacze i wentylator hello. Witaj poniższej ilustracji przedstawiono te LED.

   ![PCM LED hello obudowa EBOD][3] 

Można użyć następującej tabeli toodetermine hello stan hello PCM hello.  

| Stan | PCM OK (zielony) | Niepowodzenie AC (żółte) | Wentylator kończyć się niepowodzeniem (żółte) | Niepowodzenie kontrolera domeny (żółte) |
| --- | --- | --- | --- | --- |
| Nie zasilacza (tooenclosure) |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Nie zasilacza (tego PCM tylko) |WYŁĄCZANIE |ON |WYŁĄCZANIE |ON |
| Ak przedstawia ON PCM — OK |ON |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Błędów PCM (niepowodzenie wentylator) |WYŁĄCZANIE |WYŁĄCZANIE |ON |X |
| Błędów PCM (za pośrednictwem amp za pośrednictwem napięcia za pośrednictwem bieżącego |WYŁĄCZANIE |ON |ON |ON |
| PCM (wentylator poza okresem tolerancji) |ON |WYŁĄCZANIE |WYŁĄCZANIE |ON |
| Rezerwy modelu |Miga |WYŁĄCZANIE |WYŁĄCZANIE |WYŁĄCZANIE |
| Pobranie oprogramowania układowego PCM |WYŁĄCZANIE |Miga |Miga |Miga |

## <a name="controller-module-indicator-leds"></a>Kontroler modułu wskaźnik LED
urządzenia StorSimple Hello zawiera LED hello podstawowego kontrolera i hello EBOD kontrolera modułów.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>Monitorowanie LED hello podstawowego kontrolera
Witaj ilustracji pomaga zidentyfikować hello LED hello podstawowego kontrolera. (Wszystkie składniki hello są wymienione tooaid w orientacji).  

   ![Monitorowanie LED - podstawowego kontrolera][4]

Użyj następujących hello tabeli toodetermine, czy moduł kontrolera hello działa prawidłowo.  

### <a name="controller-indicator-leds"></a>Wskaźnik kontrolera LED
| LED | Opis |
| --- | --- |
| Identyfikator LED (niebieski) |Wskazuje, że określono ten moduł hello. Jeśli hello niebieski LED jest migający na działającego kontrolera, następnie hello kontroler jest hello active oraz hello innego hello rezerwy kontroler. Aby uzyskać więcej informacji, zobacz [Identyfikuj hello aktywnym kontrolerze na urządzeniu](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| Błąd LED (żółtą) |Wskazuje błąd hello kontrolera. |
| LED OK (zielony) |Stałej zielony oznacza, że ten kontroler hello jest OK. Miga zielony oznacza kontroler VPD błąd konfiguracji. |
| Działanie SAS LED (zielony) |Stałej zielony oznacza nie bieżącego działania z nim połączenia. Miga zielony oznacza, że połączenia hello jest bieżące działanie. |
| Stan Ethernet LED |Po prawej stronie wskazuje działania łącza i sieci: link (zielony stałej) active (miga zielony) działań w sieci. Po lewej stronie wskazuje szybkość sieci: (żółty) 1000 Mb/s (zielony) 100 Mb/s i (OFF) 10 Mb/s. W zależności od modelu składnika hello powyższe może blink, nawet jeśli nie włączono hello interfejsu sieciowego. |
| LED POST |Wskazuje postęp rozruchu powitania po włączeniu hello kontrolera. W przypadku niepowodzenia tooboot urządzenia StorSimple hello tego LED pomoże zidentyfikować punkt hello w hello proces rozruchu, w którym wystąpił błąd hello Support firmy Microsoft. |

> [!IMPORTANT]
> Jeśli błąd hello LED jest włączone, występuje problem z modułem kontrolera hello, którego może rozwiązać przez ponowne uruchomienie kontrolera hello. Jeśli ponownie uruchomić kontrolera hello nie rozwiązuje ten problem, skontaktuj się Support firmy Microsoft.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Monitorowanie LED hello EBOD (EBOD obudowa)
Każdy z hello 6 Gb/s kontrolery SAS EBOD ma LED, które wskazać jej stan, jak pokazano na następującej ilustracji hello.  

  ![Monitorowanie LED - obudowa EBOD][5]

Użyj powitania po toodetermine tabeli, czy moduł kontrolera EBOD hello działa normalnie.  

### <a name="ebod-controller-module-indicator-leds"></a>Wskaźnik modułu kontrolera EBOD LED
| Stan | We/Wy modułu OK (zielony) | Błąd modułu we/wy (żółtą) | Aktywność port hosta (zielony) |
| --- | --- | --- | --- |
| Moduł kontrolera OK |ON |WYŁĄCZANIE |- |
| Błąd modułu kontrolera |WYŁĄCZANIE |ON |- |
| Brak połączenia portu zewnętrznego hosta |- |- |WYŁĄCZANIE |
| Hoście zewnętrznym portu połączenia — Brak działania |- |- |ON |
| Połączenie z portu zewnętrznego hosta — działania |- |- |Miga |
| Błąd metadanych modułu kontrolera |Miga |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Wskaźnik dysku LED hello obudowy podstawowego i obudowy EBOD
urządzenie StorSimple Hello ma dysków znajduje się w zarówno hello obudowa podstawowego, jak i obudowy EBOD hello. Każdy dysk zawiera monitorowania LED wskaźnika, zgodnie z opisem w tej sekcji. 

Hello dysków, stan dysku hello jest określane przez zielona LED i LED żółtą red zainstalowanym na powitania na początku każdego modułu operatora dysku. Witaj poniższej ilustracji przedstawiono te LED.

  ![LED dysku][6]

Użyj powitania po tabeli toodetermine hello stan każdego dysku twardego, który z kolei ma wpływ na powitania panelu przedniego ogólne LED stanu.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Dysk wskaźnik LED hello obudowa EBOD
| Stan | Działanie LED OK (zielony) | Błąd LED (czerwony żółtą) | Skojarzone panelu ops LED |
| --- | --- | --- | --- |
| Dysk nie jest zainstalowany |WYŁĄCZANIE |WYŁĄCZANIE |Brak |
| Dysk zainstalowany i działa |Miga/wyłączone z działania |X |Brak |
| Zestaw tożsamości urządzenia SCSI usług obudowy (SES) |ON |Miga 1 sekundę na/1 sekundę poza |Brak |
| Ustawiony bit błędów urządzenia SES |ON |ON |Błąd logiczny (czerwony) |
| Obwód sterowania zasilaniu |WYŁĄCZANIE |ON |Błąd modułu (czerwony) |

## <a name="audible-alarms"></a>Alarm dźwiękowy
Urządzenie StorSimple zawiera dźwiękowe alarmy związane z zarówno hello obudowa podstawowego i obudowy EBOD hello. Alarm dźwiękowy znajduje się na panelu przednim hello (znanej także jako panel ops hello) zarówno obudów. alarmu Hello wskazuje, kiedy warunek błędu jest obecna. Witaj następujące warunki uaktywni hello alarmu:  

* Wentylator błędów lub niepowodzenie
* Napięcia poza zakresem
* Powyżej lub poniżej temperatury warunku
* Przepełnienie cieplna
* Błąd systemowy
* Błąd logiczny
* Awarii zasilania zasilania
* Usunięcie mocy chłodzenia modułu (PCM)  

Witaj poniższej tabeli opisano hello alarm różne stany.  

### <a name="alarm-states"></a>Alarm stanów
| Alarm stanu | Akcja | Działania przyciskiem wyciszenia naciśnięty |
| --- | --- | --- |
| S0 |Tryb normalny: dyskretnej |Dwa razy dźwiękowego |
| S1 |Tryb błędów: 1 sekundę na/1 sekundę poza |Przejście tooS2 lub S3 (zobacz Uwagi) |
| S2 |Przypomnij tryb: Sporadyczne dźwiękowego |Brak |
| S3 |Tryb stonowane: dyskretnej |Brak |
| S4 |Tryb błędów krytycznych: alarm ciągłej |Nie jest dostępna: wyciszanie nie jest aktywny |

> [!NOTE]
> * W stanie alarm S1 Jeśli nie zostanie naciśnięty wyciszenia w ciągu 2 minut stanu hello automatycznie zostanie przekazana tooS2 lub S3.  
> * Stany alarm S1 tooS4 zwracać tooS0 po awarii hello jest wyczyszczone.  
> * Stan krytyczny błąd S4 można wpisać w inny stan.  


Wyciszanie z hello alarmu, naciskając przycisk wyciszenia hello na powitania ops panelu. Automatyczne wyciszanie nastąpi po dwóch minut, jeśli przełącznik wyciszenia hello ręcznie jest nieobsługiwanymi. Gdy wygaszonego hello alarm będzie toosound z tooindicate krótkich dźwięków sporadyczne, czy problem nadal istnieje. Hello alarm będzie dyskretnej, gdy wszystkie problemy hello zostały wyczyszczone.

Witaj poniższej tabeli opisano hello alarm różnych warunków.

### <a name="alarm-conditions"></a>Alarm warunków
| Stan | Ważność | Alarm | OPS panelu LED |
| --- | --- | --- | --- |
| Alert PCM — utraty zasilania kontrolera domeny z jednym PCM |Błąd — nie utraty redundancji |S1 |Błąd modułu |
| Alert PCM — utraty zasilania kontrolera domeny z jednym PCM |Błąd — Utrata redundancji |S1 |Błąd modułu |
| Wentylator PCM kończyć się niepowodzeniem |Błąd — Utrata redundancji |S1 |Błąd modułu |
| Wykryto moduł SBB błędów PCM |Błąd |S1 |Błąd modułu |
| Usunięte PCM |Błąd konfiguracji |Brak |Błąd modułu |
| Błąd konfiguracji obudowy |Błąd — krytyczne |S1 |Błąd modułu |
| Niski alert temperatury ostrzeżenia |Ostrzeżenie |S1 |Błąd modułu |
| Wysoka alert temperatury ostrzeżenia |Ostrzeżenie |S1 |Błąd modułu |
| Za pośrednictwem alarm temperatury |Błąd — krytyczne |S1 |Błąd modułu |
| Błąd magistrali I2C |Błąd — Utrata redundancji |S1 |Błąd modułu |
| Błąd komunikacji (I2C) panelu OPS |Błąd — krytyczne |S1 |Błąd modułu |
| Błąd kontrolera |Błąd — krytyczne |S1 |Błąd modułu |
| Błąd modułu interfejsu SBB |Błąd — krytyczne |S1 |Błąd modułu |
| Błąd modułu interfejsu SBB — nie działa modułów pozostałych |Błąd — krytyczne |S4 |Błąd modułu |
| Moduł interfejsu SBB usunięte |Ostrzeżenie |Brak |Błąd modułu |
| Dysk awarii zasilania formantu |Ostrzeżenie — bez utraty zasilania dysku |S1 |Błąd modułu |
| Dysk awarii zasilania formantu |Błąd — krytyczne; utraty zasilania dysku |S1 |Błąd modułu |
| Usunięto dysk |Ostrzeżenie |Brak |Błąd modułu |
| Za mało dostępnych zasilania |Ostrzeżenie |Brak |Błąd modułu |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [StorSimple składniki sprzętowe i stan](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


