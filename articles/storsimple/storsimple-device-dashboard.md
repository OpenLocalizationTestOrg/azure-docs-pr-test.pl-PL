---
title: "aaaUse hello Menedżer StorSimple urządzenia w pulpicie nawigacyjnym | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano nawigacyjnym urządzenia usługi Menedżer StorSimple hello i w jaki sposób toouse go tooview magazynu metryki i inicjatorów połączonych i Znajdź hello numer seryjny i IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Pulpit nawigacyjny urządzenia hello w usłudze Menedżer StorSimple  

## <a name="overview"></a>Omówienie
pulpit nawigacyjny urządzenia StorSimple Manager Hello zawiera przegląd informacji dla określonego urządzenia StorSimple, natomiast toohello usługi Pulpit nawigacyjny, który zawiera informacje o wszystkich urządzeniach hello zawarte w rozwiązaniu Microsoft Azure StorSimple.

![Strona pulpitu nawigacyjnego urządzenia](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

pulpit nawigacyjny Hello zawiera hello następujących informacji:

* **Obszar wykresu** — widać hello odpowiedniego magazynu metryki w obszarze wykresu hello u góry hello hello pulpitu nawigacyjnego. Na tym wykresie można wyświetlać metryki dla hello głównej pamięci masowej (hello ilość danych zapisanych przez urządzenie tooyour hostów) i hello całkowita liczba zużywane przez urządzenie w danym okresie czasu magazynu w chmurze.
  
     W tym kontekście *magazynu głównego* odwołuje się toohello łączną ilość danych zapisanych przez hosta hello i mogą być podzielone przez typ woluminu: *podstawowego do warstwy magazynu* obejmuje zarówno lokalnie przechowywanych danych i danych Chmura warstwowych toohello; *głównej przypięty lokalnie magazynu* zawiera tylko dane przechowywane lokalnie. *Magazyn w chmurze*, na hello drugiej, to miara hello łączną ilość danych przechowywanych w chmurze hello. W tym warstwowych danych i tworzenie kopii zapasowych. Należy pamiętać, że dane przechowywane w chmurze hello jest deduplikowany i kompresji magazynu podstawowego wskazuje ilość hello Magazyn używany przed danych hello jest deduplikowany i skompresowane. (Możesz porównać tych dwóch liczb tooget pomysł szybkość kompresji hello). Dla obu lokacji podstawowej i magazynu, hello kwotach będą oparte na powitania śledzenia częstotliwości należy skonfigurować w chmurze. Na przykład jeśli częstotliwość tydzień, następnie wykresu hello spowodują wyświetlenie danych dla poszczególnych dni w hello poprzedniego tygodnia.
  
     Wykres hello można skonfigurować w następujący sposób:
  
  * toosee hello ilość magazynu w chmurze używane w czasie, wybierz hello **używany Magazyn w CHMURZE** opcji. toosee hello całkowita ilość miejsca, która została zapisana przez hosta hello, wybierz hello **podstawowego do warstwy MAGAZYNU używane** i **głównej LOKALNIE PRZYPIĘTY Magazyn używany** opcje. Na ilustracji hello są zaznaczone obie opcje; w związku z tym hello wykres przedstawia kwoty magazynu dla chmurą i z magazynu głównego. Należy pamiętać, że dowolny magazyn podstawowy używane wcześniejsze tooinstalling Update 2 jest reprezentowana przez hello **podstawowego do warstwy MAGAZYNU używane** wiersza.
  * Użyj menu rozwijanego hello hello prawym górnym rogu toospecify wykresu hello przez pewien czas 1 tygodnia, miesiąca 1, 3-miesięczna lub 1 rok. Należy pamiętać, że hello najwyższego poziomu wykresu zostanie odświeżony tylko jeden raz dziennie, a w związku z tym będzie odzwierciedlać hello sumy poprzedniego dnia.
    
    Aby uzyskać więcej informacji, zobacz [Użyj hello toomonitor usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-monitor-device.md).
* **Przegląd wykorzystania** — Witaj **przegląd wykorzystania** obszarze widać hello ilość miejsca w magazynie podstawowy używany ilość hello zainicjowanego magazynu i hello maksymalna pojemność magazynu dla danego urządzenia. Porównując te użycia numery toohello maksymalną ilość pamięci, która jest dostępna, można wyświetlić w skrócie należy tooobtain dodatkowego magazynu. Warto zauważyć, że w tym omówieniu jest aktualizowany co 15 minut, z powodu różnicy hello częstotliwość aktualizacji, mogą być wyświetlane różne numery niż wyświetlanych w hello obszaru wykresu powyżej, która jest aktualizowana raz dziennie. Aby uzyskać więcej informacji, zobacz [Użyj hello toomonitor usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-monitor-device.md).
* **Alerty** — Witaj **alerty** obszaru zawiera omówienie hello alerty dla danego urządzenia. Alerty są pogrupowane według ważności, a licznik podano hello liczby alertów na każdym poziomie ważność. Kliknięcie przycisku alertów hello ważność spowoduje otwarcie widoku zakresami hello alerty tooshow kartę tylko hello alerty ten poziom ważności, dla tego urządzenia.
* **Zadania** — Witaj **zadania** pokazuje obszaru hello wyników ostatnią aktywność zadania. To należy zapewnić że hello system działa zgodnie z oczekiwaniami, lub umożliwić użytkownika, należy tootake działań naprawczych. Kliknij przycisk więcej informacji o zadaniach ostatnio wykonanych toosee **zadań pomyślnie hello ostatnich 24 godzinach**.
* Witaj **szybkiego dostępu** obszar na powitania rogu hello pulpit nawigacyjny zawiera przydatne informacje, takie jak model urządzenia, numer seryjny, stan, opisu i liczby woluminów.

Można również skonfigurować trybu failover i wyświetlić inicjatorów połączonych z poziomu pulpitu nawigacyjnego hello urządzenia.

Witaj typowych zadań, które mogą być wykonywane na tej stronie są:

* Wyświetl połączone inicjatorów
* Znaleźć numer seryjny urządzenia hello
* Znajdź hello urządzenia docelowego IQN

## <a name="view-connected-initiators"></a>Wyświetl połączone inicjatorów
Możesz wyświetlić hello inicjatorów iSCSI, które są tooyour podłączonego urządzenia, klikając hello **wyświetlanie połączonych inicjatorów** łącza w hello **szybkiego dostępu** części pulpitu nawigacyjnego urządzenia. Ta strona zawiera listę tabelarycznym inicjatorów hello, które pomyślnie nawiązano połączenie tooyour urządzenia. Dla każdego inicjatora można wyświetlić:

* Witaj iSCSI kwalifikowana nazwa (IQN) z hello połączone inicjatora.
* Nazwa Hello hello rekord kontroli dostępu (ACR) umożliwiający tego inicjatora połączonych.
* adres IP Hello hello połączone inicjatora.
* Witaj interfejsy sieciowe tego inicjatora hello jest tooon podłączonego urządzenia pamięci masowej. Te mogą należeć do zakresu od danych 0 tooDATA 5.
* Wszystkie woluminy hello, które hello połączonych inicjatora jest dozwolone tooaccess zgodnie z bieżącą konfigurację ACR toohello.

Jeśli Zobacz nieoczekiwany inicjatorów na tej liście lub nie ma się, że hello oczekiwano te, należy przejrzeć konfigurację ACR. Urządzenie tooyour można podłączyć maksymalnie 512 inicjatorów.

## <a name="find-hello-device-serial-number"></a>Znaleźć numer seryjny urządzenia hello
Po skonfigurowaniu wielościeżkowego We/Wy (MPIO) firmy Microsoft na urządzeniu hello numer seryjny urządzenia hello może być konieczne. Wykonaj hello następującego numeru seryjnego urządzenia hello toofind czynności.

#### <a name="toofind-hello-device-serial-number"></a>numer seryjny urządzenia hello toofind
1. Przejdź za**urządzeń** > **pulpitu nawigacyjnego**.
2. W prawym okienku hello hello pulpitu nawigacyjnego, Znajdź hello **szybkiego dostępu** obszaru.
3. Przewiń w dół, a następnie zlokalizuj hello numeru seryjnego.

## <a name="find-hello-device-target-iqn"></a>Znajdź hello urządzenia docelowego IQN
Witaj urządzenia docelowego IQN może być konieczne po skonfigurowaniu hello protokół uwierzytelniania typu Challenge Handshake (CHAP) na urządzeniu StorSimple. Wykonaj następujące kroki toofind hello urządzenia docelowego IQN hello.

### <a name="toofind-hello-device-target-iqn"></a>toofind hello urządzenia docelowego IQN
1. Przejdź za**urządzeń** > **pulpitu nawigacyjnego**.
2. W prawym okienku hello hello pulpitu nawigacyjnego, Znajdź hello **szybkiego dostępu** obszaru.
3. Przewiń w dół, a następnie zlokalizuj docelowy hello IQN.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [pulpit nawigacyjny usługi Menedżer StorSimple](storsimple-service-dashboard.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

