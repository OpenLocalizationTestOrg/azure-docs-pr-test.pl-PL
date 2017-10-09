---
title: "urządzenie serii StorSimple 8000 aaaUse podsumowania | Dokumentacja firmy Microsoft"
description: "Opisuje urządzenie usługi Menedżer StorSimple urządzenia hello podsumowania i w jaki sposób toouse on tooview magazynu metryki i inicjatorów połączonych i Znajdź hello numer seryjny i IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Używanie urządzenia hello podsumowania w usłudze Menedżer StorSimple urządzenia

## <a name="overview"></a>Omówienie
Blok podsumowania urządzenia StorSimple Hello zawiera przegląd informacji dla określonego urządzenia StorSimple, natomiast toohello usługi podsumowania bloku, który zawiera informacje o wszystkich urządzeniach hello zawarte w rozwiązaniu Microsoft Azure StorSimple.

Podsumowanie bloku urządzenia Hello zawiera widok podsumowania urządzenia serii StorSimple 8000, który jest zarejestrowany z danym urządzeniem Menedżer StorSimple, wyróżnianie tych problemów z urządzeniami, które wymagają uwagi administratora systemu. W tym samouczku wprowadza hello urządzenia podsumowania bloku, opisano hello zawartości i funkcji oraz opisano hello zadania, które można wykonać z poziomu tego bloku.

Podsumowanie bloku urządzenia Hello Wyświetla hello następujących informacji:

![Podsumowanie bloku urządzenia](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Pasek poleceń zarządzania

W bloku urządzenia StorSimple hello zobacz temat hello opcje służące do zarządzania urządzeniem StorSimple. Widzisz polecenia zarządzania hello hello górze bloku hello i po lewej stronie powitania. Użyj tych opcji tooadd udziały lub woluminy lub urządzenie w tryb failover.

![Pasek poleceń zarządzania](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Podstawy

obszar essentials Hello przechwytuje niektórych hello ważne właściwości, takie jak, stan hello, modelu, docelowy IQN i hello wersji oprogramowania. 

![Podstawowe informacje dotyczące urządzeń](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Monitorowanie

* Witaj **alerty** kafelka zawiera migawkę wszystkich hello aktywne alerty dla danego urządzenia, pogrupowane według ważności alertu.

    ![Kafelek alertu](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Kliknij przycisk hello kafelka tooopen hello **alerty** bloku, a następnie kliknij przycisk indywidualnym alertów tooview dodatkowe szczegóły dotyczące alertu, wraz ze wszystkimi zalecane akcje. Można także wyczyścić hello alert, jeśli hello problem został rozwiązany.

    ![Kliknij Kafelek alertu](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Witaj **stanu i kondycji** kafelka zapewnia wgląd w kondycja składnika hello sprzętu dla urządzeń, w tym stan urządzenia hello. Stan urządzenia Hello może być w trybie offline, online, dezaktywować lub gotowe tooset aktywne.

    ![Kafelek stanu i kondycji](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Witaj **woluminów** kafelka zawiera podsumowanie liczby hello woluminów w urządzeniu pogrupowane według stanu.

    ![Kafelka woluminy](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Kliknij przycisk hello kafelka tooopen hello **woluminów** listy bloku, a następnie kliknij na tooview poszczególnych woluminów lub zmodyfikować jego właściwości.
    
    ![Kliknij Kafelek woluminów](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Aby uzyskać więcej informacji, zobacz temat jak zbyt[Zarządzanie woluminami](storsimple-8000-manage-volumes-u2.md).

* W hello **użycia** wykresu, można wyświetlić hello magazynu podstawowy używany przez urządzenia i magazynu w chmurze hello używane za pośrednictwem hello ostatnich 7 dni, hello domyślny okres czasu.

     ![Kafelek użycie](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose przedział czasu różnych Użyj hello **Edytuj** opcji w hello prawym górnym rogu wykresu hello.

     ![Edytuj wykres użycia](./media/storsimple-8000-device-dashboard/device-summary12.png)

     Na tym wykresie można wyświetlać metryki dla hello głównej pamięci masowej (hello ilość danych zapisanych przez urządzenie tooyour hostów) i hello całkowita liczba zużywane przez urządzenie w danym okresie czasu magazynu w chmurze.
  
     W tym kontekście *magazynu głównego* odwołuje się toohello łączną ilość danych zapisanych przez hosta hello i mogą być podzielone przez typ woluminu: *podstawowego do warstwy magazynu* obejmuje zarówno lokalnie przechowywanych danych i danych Chmura toohello warstwowego. *Podstawowy przypięty lokalnie magazynu* zawiera tylko dane przechowywane lokalnie. *Magazyn w chmurze*, na hello drugiej, to miara hello łączną ilość danych przechowywanych w chmurze hello. Ten magazyn zawiera warstwowych danych i tworzenie kopii zapasowych. Witaj danych przechowywanych w chmurze hello jest deduplikowany i skompresowane magazynu podstawowego wskazuje ilość hello Magazyn używany przed danych hello jest deduplikowany i skompresowane. (Możesz porównać tych dwóch liczb tooget pomysł szybkość kompresji hello). Dla obu lokacji podstawowej i magazynu, hello kwotach są oparte na powitania śledzenia częstotliwości należy skonfigurować w chmurze. Na przykład jeśli częstotliwość tydzień, hello wykresu zawiera dane dla poszczególnych dni w hello poprzedniego tygodnia.

     toosee hello ilość magazynu w chmurze używane w czasie, wybierz hello **używany Magazyn w CHMURZE** opcji. toosee hello całkowita ilość miejsca, która została zapisana przez hosta hello, wybierz hello **podstawowego do warstwy MAGAZYNU używane** i **głównej LOKALNIE PRZYPIĘTY Magazyn używany** opcje. 
     Aby uzyskać więcej informacji, zobacz [Użyj hello toomonitor usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-monitor-device.md).


* Witaj **pojemności** kafelka Wyświetla hello podstawowego magazynu, który zostanie zainicjowana i pozostałych między hello urządzenia względną toohello całkowita ilość miejsca dostępne dla hello takie same. **Zainicjowano obsługę administracyjną** odwołuje się toohello ilość miejsca w magazynie, który jest przygotowany i przydzielona do użycia, **pozostała** odwołuje się toohello pozostałych pojemności, które można udostępnić w tym urządzeniu. 

    ![Kafelek użycie](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Kliknij ten tooview kafelka jak pojemności hello zostanie zainicjowana na woluminach warstwowych i przypiętych lokalnie. Hello **pozostałych do warstwy** pojemność to hello dostępnej pojemności, który można udostępnić, łącznie z chmury, podczas hello **pozostałych lokalnego** jest pojemność hello pozostały na dyskach hello dołączonego urządzenia toothis.

    ![Kliknij wykres użycia](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [bloku podsumowania usługi StorSimple](storsimple-8000-service-dashboard.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

