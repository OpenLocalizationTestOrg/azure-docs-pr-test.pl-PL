---
title: "aaaMonitor Twojego urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak hello toouse Menedżera urządzeń StorSimple usługi użycia toomonitor, wydajności we/wy i wykorzystanie pojemności."
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Użyj toomonitor usługi Menedżer StorSimple urządzenia hello urządzenia StorSimple
## <a name="overview"></a>Omówienie
Hello Menedżera urządzeń StorSimple usługi toomonitor określonych urządzeń można użyć w rozwiązaniu StorSimple. Można tworzyć niestandardowe wykresy na podstawie wydajności operacji We/Wy, wykorzystanie pojemności, przepływność sieci i metryki wydajności urządzenia i Przypnij do pulpitu nawigacyjnego tych toohello. Aby uzyskać więcej informacji, przejdź zbyt[dostosowanie pulpitu nawigacyjnego portalu](/articles/azure-portal/azure-portal-dashboards.md).

tooview hello informacji o monitorowaniu dla określonego urządzenia, w hello portalu Azure, wybierz usługę Menedżer StorSimple urządzenia hello. Z listy hello urządzeń wybierz urządzenia, a następnie przejdź zbyt**Monitor**. Możesz sprawdzić hello **pojemności**, **użycia**, i **wydajności** wykresy hello wybranego urządzenia.

## <a name="capacity"></a>Pojemność
**Pojemność** śledzi hello elastycznie i miejsca hello na powitania urządzenia. następnie jest wyświetlany Hello pozostałych pojemności, jak przypięty lokalnie lub do warstwy.

Hello zainicjowano obsługę administracyjną i pozostałych pojemności jest dalsze rozbiciu woluminów warstwowych i przypiętych lokalnie. Dla każdego woluminu hello alokować pojemności i hello pozostałych pojemności na urządzeniu hello jest wyświetlany.

![Wydajność We/Wy](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Sposób użycia
**Użycie** śledzi metryk powiązanych toohello ilość miejsca do magazynowania danych, używany przez hello woluminów, kontenery woluminów lub urządzenia. Możesz utworzyć raporty na podstawie wykorzystania pojemności hello podstawowego magazynu, magazynu w chmurze lub magazynie urządzenia. Wykorzystanie pojemności może być zmierzony przy określonego woluminu, określony wolumin kontenera lub wszystkie kontenery woluminów.
Domyślnie jest zgłaszana hello użycie w ciągu ostatnich 24 godzin. Można edytować za pośrednictwem których hello użycia jest zgłaszany, wybierając z hello wykresu toochange hello czas:
* Po 24 godzinach
* Ostatnie 7 dni
* Ostatnie 30 dni
* Ostatnie 90 dni
* Ciągu ostatniego roku


Witaj podstawowego, chmury i lokalny magazyn używany można przedstawić w następujący sposób:

### <a name="primary-storage-usage"></a>Użycie magazynu głównego
Te na wykresach hello ilość danych zapisane woluminów tooStorSimple przed danych hello jest deduplikowany i skompresowane. Można wyświetlić hello magazyn podstawowy używany przez wszystkie woluminy w kontenerze woluminów lub jednego woluminu. Witaj magazyn podstawowy używany jest dalsze rozbiciu podstawowego magazynu warstwowego używane i podstawowy używany Magazyn przypiętych lokalnie.

Witaj następujące na wykresach hello magazynu podstawowy używany dla urządzenia StorSimple przed i po migawki chmury. Jak jest to po prostu danych woluminu, migawka w chmurze nie należy zmieniać hello podstawowego magazynu. Jak widać, hello wykres przedstawia różnicy w hello głównej warstwowych lub przypięty lokalnie Magazyn używany wyniku migawki chmury. Migawka w chmurze Hello rozpoczęty o godzinie około 11:50 pm na tym urządzeniu.

![Wykorzystanie pojemności głównej po migawka w chmurze](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Jeśli teraz uruchomić we/wy na urządzeniu StorSimple tooyour hosta połączony hello, zobaczysz wzrost podstawowego magazynu warstwowego lub przypięty lokalnie podstawowy magazyn używany w zależności od woluminów (warstwowa lub przypięty lokalnie) można zapisywać hello danych. Poniżej przedstawiono wykresy użycia magazynu głównego powitania dla urządzenia StorSimple. Na tym urządzeniu hosta StorSimple hello uruchomiona obsługująca zapisuje na około 2:30 będzie na wolumin warstwowy na urządzeniu hello. Szczytowa hello w hello zapisu bajtów/s odpowiadającego we/wy toohello uruchomiona na hoście hello jest widoczny.

![Wydajność We/Wy z woluminami warstwowymi](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Jeśli przyjrzymy się hello podstawowego magazynu warstwowego używane, która wykroczyła się konieczne użycie hello głównej przypięty lokalnie pozostaje niezmieniony są nie zapisy zrealizować woluminów toohello przypięty lokalnie na urządzeniu hello.

![Wykorzystanie pojemności głównej uruchomionej we/wy na woluminach warstwowych](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Jeśli używasz aktualizacją 3 lub wyższym, można przerwać w dół hello głównej wykorzystanie pojemności poszczególnych woluminów, wszystkie woluminy, wszystkie woluminy warstwowe i wszystkich woluminów przypiętych lokalnie jak pokazano poniżej. Dzielenie przez wszystkie lokalnie woluminów przypiętych pozwoli tooquickly upewnić się, ile warstwy lokalne powitania zużycia.

![Wykorzystanie pojemności głównej dla wszystkich woluminów warstwowych](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Wykorzystanie pojemności głównej dla wszystkich woluminów przypiętych lokalnie](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Pozwala dodatkowo kliknij na każdym woluminie hello liście hello i zobacz Użycie odpowiednich hello.

![Wykorzystanie pojemności głównej dla wszystkich woluminów przypiętych lokalnie](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Użycie magazynu w chmurze
Te na wykresach hello ilość używane magazynu w chmurze. Te dane są deduplikowane i skompresowane. Ta wartość obejmuje migawki w chmurze, które mogą zawierać dane, które nie jest uwzględniana w głównej woluminami i jest przechowywana na potrzeby przechowywania starszych lub wymagane. Można porównać hello podstawowego i chmury magazynu zużycie rysunki tooget pomysł hello danych zmniejszenie szybkości, mimo że numer hello nie będą dokładne.

Witaj następujące na wykresach wykorzystanie magazynu chmury hello urządzenia StorSimple podczas migawki chmury.

* Migawka w chmurze Hello rozpoczęty o godzinie około 11:50:00 na tym urządzeniu i można stwierdzić, że przed hello migawka w chmurze, nie było żadnych magazynu w chmurze używane. 
* Raz migawka w chmurze hello ukończone, wykorzystanie magazynu w chmurze hello zrzut zapasowej 0,89 GB. 
* Podczas hello migawka w chmurze jest w toku, dostępna jest również odpowiedniego szczytu w hello We/Wy z toocloud urządzenia.

    ![Wykorzystanie magazynu w chmurze przed migawka w chmurze](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Wykorzystanie magazynu w chmurze po migawka w chmurze](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![We/Wy z urządzenia toocloud podczas migawka w chmurze](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Użycie lokalnego magazynu
Te na wykresach hello łączne użycie hello urządzenia, którego będzie więcej niż użycie magazynu podstawowego, ponieważ zawiera on liniowej warstwy dysków SSD hello. Ta warstwa zawiera ilość danych, które istnieje także w hello urządzenia innej warstwy. pojemność Hello w liniowej warstwy dysków SSD hello ponownym włączeniu tak, aby po nadejściu nowych danych starych danych hello jest warstwy dysków HDD przeniesionego toohello (po tym czasie jest deduplikowany i skompresowane), a następnie toohello chmury.

Wraz z upływem czasu podstawowego magazynu używane i lokalny magazyn używany najprawdopodobniej spowoduje zwiększenie razem do momentu rozpoczęcia toobe hello danych warstwowej toohello chmury. W tym momencie magazyn lokalne powitania używany prawdopodobnie rozpocznie się tooplateau, ale będzie większa hello magazyn podstawowy używany, gdy zapisywanych jest więcej danych.

Witaj następujące na wykresach hello magazynu podstawowy używany dla urządzenia StorSimple, gdy migawki chmury. Migawka w chmurze Hello zaczęła na 11:50:00, a Magazyn lokalny hello zmniejszenie o tej godzinie. lokalny magazyn Hello używane zakończył działanie z too1.09 1.445 GB GB. To wskazuje, że prawdopodobnie hello nieskompresowanych danych w liniowej warstwy dysków SSD hello został deduplikowane, skompresowane i przeniesione do warstwy dysków HDD hello. Należy pamiętać, że jeśli urządzenie hello już dużą ilość danych zarówno hello dysków SSD i warstwy dysków HDD, mogą nie być widoczne to zmniejszenie. W tym przykładzie hello urządzenie ma niewielką ilość danych.

![Użycie magazynu lokalnego po migawka w chmurze](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Wydajność
**Wydajność** metryki śledzi powiązany numer toohello odczytu i zapisu między albo iSCSI hello interfejsy inicjatora na powitania serwera hosta i hello urządzenie lub urządzenia hello i w chmurze hello. To wydajność może być zmierzony dla określonego woluminu, określony wolumin kontenera lub wszystkie kontenery woluminów. Wydajność obejmuje także wykorzystanie procesora CPU i przepływności sieci dla hello różnych interfejsów sieciowych na urządzeniu.

### <a name="io-performance-for-initiator-toodevice"></a>Wydajność We/Wy toodevice inicjatora
Wykres Hello poniżej przedstawia hello we/wy dla urządzenia tooyour inicjatora hello wszystkie woluminy hello urządzenia produkcji. metryki Hello wykreślić są odczytu i zapisu bajtów na sekundę. Można również wykresu odczytu, zapisu i oczekujących operacji We/Wy lub odczytu i zapisu opóźnienia.

![Wydajność We/Wy toodevice inicjatora](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Wydajność We/Wy toocloud urządzenia
Dla hello jednym urządzeniu, operacje We/Wy hello są kreślone hello danych z hello urządzenia toohello chmury dla wszystkich hello kontenery woluminów. Na tym urządzeniu hello danych jest tylko w warstwie liniowej hello i nic nie ma rozrzucone toohello chmury. Nie ma żadnych wykonywane z chmury toohello urządzenia operacje odczytu i zapisu. W związku z tym hello szczytów wykresu hello są z interwałem wynoszącym 5 minut odpowiadający częstotliwość toohello jaką pulsu hello zaznaczono między hello urządzeń i usług hello.

Dla hello jednym urządzeniu, migawkę chmury została wykonana dla danych woluminu, zaczynając od 11:50:00. To sprawia, że dane przepływające z hello urządzenia toohello chmury. Zapisy zostały obsłużone toohello chmury w ten czas trwania. Wykres we/wy Hello pokazuje szczytu hello zapisu bajtów/s odpowiedniego toohello czas po hello migawki.

![We/Wy z urządzenia toocloud podczas migawka w chmurze](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Przepustowość sieci dla interfejsów sieciowych urządzenia
**Przepustowość sieci** śledzi metryk powiązanych toohello ilość danych przetransferowanych z hello iSCSI initiator interfejsów sieciowych na serwerze hosta hello i hello urządzenia oraz między hello urządzenia i w chmurze hello. Ta metryka dla poszczególnych interfejsów sieciowych iSCSI hello można monitorować na urządzeniu.

Witaj następujących przepływność sieci hello Pokaż wykresów dla hello dane 0, 1, 1 GbE sieci na swoim urządzeniu, która była zarówno włączoną obsługę chmury (ustawienie domyślne) i włączono interfejs iSCSI. Na tym urządzeniu 14 czerwca na około 21: 00 do danych został warstwy do chmury hello (bez chmury, którego wykonano migawek w tym czasie, które są tootiering punktów hello mechanizm toomove hello danych w chmurze hello), co spowodowało obsługiwanej chmury toohello we/wy. Wykres przepustowość sieci hello jest odpowiedni szczytu, hello tym samym czasie i większość ruchu sieciowego hello jest wychodzący toohello chmury.

![Przepustowość sieci dla interfejsu dane 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Jeśli przyjrzymy hello danych 1 interfejs przepływności wykresu sieciowe innego 1 GbE interfejs, który był tylko włączono interfejs iSCSI, a następnie nie było praktycznie ruchu sieciowego w ten czas trwania.

![Przepustowość sieci dla danych 1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Użycie procesora CPU dla urządzenia
**Użycie procesora CPU** śledzi metryki dotyczące toohello procesora CPU wykorzystana na urządzeniu. Witaj poniższym wykresie przedstawiono Statystyka wykorzystania procesora CPU hello urządzenia w środowisku produkcyjnym.

![Użycie procesora CPU dla urządzenia](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[pulpit nawigacyjny urządzenia usługi Menedżer StorSimple urządzenia hello](storsimple-device-dashboard.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

