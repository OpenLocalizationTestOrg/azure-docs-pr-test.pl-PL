---
title: "aaaMonitor urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello wydajność We/Wy toomonitor usługi Menedżer StorSimple, wykorzystanie pojemności, przepływność sieci i wydajność urządzenia."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Użyj toomonitor usługi Menedżer StorSimple hello urządzenia StorSimple
## <a name="overview"></a>Omówienie
Urządzenia określonego toomonitor usługi Menedżer StorSimple hello można użyć w rozwiązaniu StorSimple. Można tworzyć niestandardowe wykresy na podstawie wydajności operacji We/Wy, wykorzystanie pojemności, przepływność sieci i metryki wydajności urządzenia. 

Witaj tooview monitorowania informacje dotyczące określonego urządzenia w hello klasycznego portalu Azure, wybierz hello usługi Menedżer StorSimple. Kliknij przycisk hello **Monitor** , a następnie wybierz z listy hello urządzeń. Witaj **Monitor** strona zawiera hello następujących informacji.

## <a name="io-performance"></a>Wydajność We/Wy
**Wydajność We/Wy** metryki śledzi powiązany numer toohello odczytu i zapisu między albo iSCSI hello interfejsy inicjatora na powitania serwera hosta i hello urządzenie lub urządzenia hello i w chmurze hello. To wydajność może być zmierzony dla określonego woluminu, określony wolumin kontenera lub wszystkie kontenery woluminów.

Wykres Hello poniżej przedstawia hello we/wy dla urządzenia tooyour inicjatora hello wszystkie woluminy hello urządzenia produkcji. metryki Hello wykreślić są do odczytu i zapisu bajtów na sekundę, odczytu i operacji We/Wy na sekundę, zapisu i odczytu i zapisu opóźnienia.

![Wydajność We/Wy z toodevice inicjatora](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Dla hello jednym urządzeniu, operacje We/Wy hello są kreślone hello danych z hello urządzenia toohello chmury dla wszystkich hello kontenery woluminów. Na tym urządzeniu hello danych jest tylko w warstwie liniowej hello i nic nie ma rozrzucone toohello chmury. Nie ma żadnych wykonywane z chmury toohello urządzenia operacje odczytu i zapisu. W związku z tym hello szczytów wykresu hello są z interwałem wynoszącym 5 minut odpowiadający częstotliwość toohello jaką pulsu hello zaznaczono między hello urządzeń i usług hello. 

![Wydajność We/Wy z toocloud urządzenia](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Dla hello jednym urządzeniu, migawkę chmury została wykonana dla danych woluminu, zaczynając od 2:00 pm. To sprawia, że dane przepływające z hello urządzenia toohello chmury. Odczytuje i zapisuje zostały obsłużone chmury toohello tego czasu trwania. Witaj we/wy wykres pokazuje szczytu hello różnych metryk odpowiadającego toohello czas, kiedy hello migawki. 

![Wydajność We/Wy urządzenia toocloud po migawka w chmurze](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Użycie wydajności
**Użycie wydajności** śledzi metryk powiązanych toohello ilość miejsca do magazynowania danych, używany przez hello woluminów, kontenery woluminów lub urządzenia. Możesz utworzyć raporty na podstawie wykorzystania pojemności hello podstawowego magazynu, magazynu w chmurze lub magazynie urządzenia. Wykorzystanie pojemności może być zmierzony przy określonego woluminu, określony wolumin kontenera lub wszystkie kontenery woluminów.

Hello podstawowego, chmury i pojemności magazynu urządzenia można przedstawić w następujący sposób:

### <a name="primary-storage-capacity-utilization"></a>Podstawowe wykorzystanie pojemności
Te na wykresach hello ilość danych zapisane woluminów tooStorSimple przed danych hello jest deduplikowany i skompresowane. Wykorzystanie magazynu podstawowego hello można wyświetlić wszystkich woluminów lub jednego woluminu.

Po wyświetleniu hello magazynu głównego woluminu pojemności wykorzystania wykresy wszystkie woluminy w porównaniu z każdego hello poszczególnych woluminów i podsumowania danych podstawowych hello w obu przypadkach może być niezgodność między dwiema liczbami hello. Całkowita danych podstawowych Hello we wszystkich woluminach może nie sumują łączną sumę toohello hello danych podstawowych hello poszczególnych woluminów. Może to być spowodowane tooone hello następujące czynności:

* **Dane uwzględnione dla wszystkich woluminów migawek**: ten problem występuje tylko wtedy, gdy używasz wersji wcześniejszych niż aktualizacja Update 3. Hello danych podstawowych pokazano wszystkie woluminy hello jest suma hello hello migawki danych i hello danych pierwotnych dla każdego woluminu. Hello danych podstawowych wyświetlany dla danego woluminu odpowiada tooonly hello ilość danych przydzielone w woluminie hello (i nie ma hello odpowiednie dane migawki woluminu).
  
    Ten można również wyjaśnić hello następujące równanie:
  
    *Danych podstawowych (wszystkich woluminów) = Suma (danych podstawowych (woluminu i) + rozmiar danych migawki (woluminu i))*
  
    *w przypadku gdy podstawowy danych (woluminu i) = rozmiar danych podstawowych przydzielone toovolume i*
  
    Usunięcie migawki hello za pośrednictwem usługi hello usunięcia hello odbywa się asynchronicznie w tle hello. Może upłynąć trochę czasu, zanim hello wolumin danych rozmiar toobe uaktualnić po hello usunięcia migawki. 
  
    Jeśli uruchomioną aktualizacją 3 lub nowszym, dane migawki hello nie jest uwzględniony w hello woluminów danych. I użycie głównej hello jest obliczana w następujący sposób:
  
    * Głównej danych (wszystkich woluminów) = Suma (danych podstawowych (woluminu i)
  
    *w przypadku gdy podstawowy danych (woluminu i) = rozmiar danych podstawowych przydzielone toovolume i*
* **Woluminy z monitorowaniem wyłączone objęte wszystkie woluminy**: Jeśli masz woluminów na urządzeniu, dla których monitorowanie jest wyłączone, hello danych monitorowania dla tych woluminów poszczególnych nie będą dostępne na wykresach hello. Jednak dane hello wszystkie woluminy na wykresie hello obejmują hello woluminów, których monitorowanie jest wyłączone. 
* **Usunięte z uwzględnione wszystkie woluminy na żywo skojarzonych kopii zapasowych woluminów**: Jeśli woluminy zawierające dane migawki są usuwane, ale nadal istnieją migawki hello skojarzony, a następnie niezgodność może zostać wyświetlony.
* **Usunięte woluminy uwzględnione dla wszystkich woluminów**: W niektórych przypadkach mogą istnieć starszych woluminów, nawet jeśli te zostały usunięte. efekt Hello usunięcia nie jest widoczny i hello urządzenia mogą być wyświetlane niższe dostępnej pojemności. Należy tooremove Microsoft Support toocontact tych woluminów.

Witaj następujące na wykresach hello głównej wykorzystanie pojemności urządzenia StorSimple przed i po migawki chmury. Jak jest to po prostu danych woluminu, migawka w chmurze nie należy zmieniać hello podstawowego magazynu. Jak widać, hello wykres przedstawia różnicy w wykorzystanie pojemności głównej hello wyniku migawki chmury. Migawka w chmurze Hello rozpoczęty o godzinie około 2:00 pm na tym urządzeniu.

![Wykorzystanie pojemności głównej przed migawka w chmurze](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Wykorzystanie pojemności głównej po migawka w chmurze](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Jeśli używasz Update 2 lub nowszy, można przerwać dół hello głównej wykorzystanie pojemności poszczególnych woluminów, wszystkie woluminy, wszystkie woluminy warstwowe i wszystkich woluminów przypiętych lokalnie jak pokazano poniżej. Dzielenie przez wszystkie lokalnie woluminów przypiętych pozwoli tooquickly upewnić się, ile warstwy lokalne powitania zużycia.

![Wykorzystanie pojemności głównej dla wszystkich woluminów przypiętych lokalnie](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Wykorzystanie pojemność magazynu w chmurze
Te na wykresach hello ilość używane magazynu w chmurze. Te dane są deduplikowane i skompresowane. Ta wartość obejmuje migawki w chmurze, które mogą zawierać dane, które nie jest uwzględniana w głównej woluminami i jest przechowywana na potrzeby przechowywania starszych lub wymagane. Można porównać hello podstawowego i chmury magazynu zużycie rysunki tooget pomysł hello danych zmniejszenie szybkości, mimo że numer hello nie będą dokładne. Witaj następujące na wykresach hello chmury wykorzystanie pojemności urządzenia StorSimple przed i po migawki chmury. Witaj migawka w chmurze rozpoczęty o godzinie około 2:00 pm na tym urządzeniu, aby zobaczyć wykorzystanie pojemności chmury hello zrzut na powitania sam czas zwiększenia z too4.04 5.73 MB, GB.

![Wykorzystanie pojemności chmury przed migawka w chmurze](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Wykorzystanie pojemności chmury po migawka w chmurze](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Wykorzystanie pojemności urządzenia
Te na wykresach hello łączne użycie hello urządzenia, które będzie większa niż wartość użycia magazynu podstawowego, ponieważ zawiera on liniowej warstwy dysków SSD hello. Ta warstwa zawiera ilość danych, które istnieje także w hello urządzenia innej warstwy. pojemność Hello w liniowej warstwy dysków SSD hello ponownym włączeniu tak, aby po nadejściu nowych danych starych danych hello jest warstwy dysków HDD przeniesionego toohello (po tym czasie jest deduplikowany i skompresowane), a następnie toohello chmury.

Wraz z upływem czasu użycia głównej pojemności i wykorzystania pojemności urządzenia najprawdopodobniej zwiększy razem do momentu rozpoczęcia toobe hello danych warstwowej toohello chmury. W tym momencie wykorzystanie pojemności urządzenia hello prawdopodobnie rozpocznie się tooplateau, ale wykorzystanie pojemności głównej hello zwiększy miarę zapisywanych jest więcej danych.

Witaj następujące na wykresach hello głównej wykorzystanie pojemności urządzenia StorSimple przed i po migawki chmury. Migawka w chmurze Hello rozpoczęty o godzinie 2:00 pm i wykorzystanie pojemności urządzenia hello uruchomiona, zmniejszając w tym czasie. wykorzystanie pojemności urządzenia Hello zakończył działanie z too7.48 11.58 GB GB. To wskazuje, że prawdopodobnie hello nieskompresowanych danych w liniowej warstwy dysków SSD hello został deduplikowane, skompresowane i przeniesione do warstwy dysków HDD hello. Należy pamiętać, że jeśli urządzenie hello już dużą ilość danych zarówno hello dysków SSD i warstwy dysków HDD, mogą nie być widoczne to zmniejszenie. W tym przykładzie hello urządzenie ma niewielką ilość danych.

![Wykorzystanie pojemności urządzenia przed migawka w chmurze](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Wykorzystanie pojemności urządzenia po migawka w chmurze](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Przepustowość sieci
**Przepustowość sieci** śledzi metryk powiązanych toohello ilość danych przetransferowanych z hello iSCSI initiator interfejsów sieciowych na serwerze hosta hello i hello urządzenia oraz między hello urządzenia i w chmurze hello. Ta metryka dla poszczególnych interfejsów sieciowych iSCSI hello można monitorować na urządzeniu.

powitania po przepływność sieci hello Pokaż wykresy hello dane 0 a 4 danych, obu 1 GbE interfejsów na urządzeniu. W tym przypadku Data 0 został włączoną obsługę chmury 4 danych został włączony iSCSI. Widać zarówno hello ruchu przychodzącego i hello ruchu wychodzącego dla urządzenia StorSimple. Hello płaskiej wiersza na wykresie powitania od 15:24:00 jest ze względu na fakt toohello firma Microsoft zbiera dane o co 5 minut i należy ją ignorować. 

![Przepustowość sieci dla Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Przepustowość sieci dla Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Wydajność urządzenia
**Wydajność urządzenia** śledzi metryki dotyczące wydajności toohello urządzenia. Witaj poniższym wykresie przedstawiono Statystyka wykorzystania procesora CPU hello urządzenia w środowisku produkcyjnym.

![Użycie procesora CPU dla urządzenia](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[pulpit nawigacyjny urządzenia usługi Menedżer StorSimple hello](storsimple-device-dashboard.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

