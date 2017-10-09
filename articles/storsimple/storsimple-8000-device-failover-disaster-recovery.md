---
title: "tryb failover aaaStorSimple, odzyskiwania po awarii dla urządzeń z serii 8000 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem sieci tooitself urządzenia StorSimple, inne fizyczne urządzenie lub urządzenia chmury."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Tryb failover i odzyskiwania po awarii dla danego urządzenia z serii StorSimple 8000

## <a name="overview"></a>Omówienie

W tym artykule opisano hello urządzenia funkcji i trybu failover dla urządzeń z serii StorSimple 8000 hello jak tę funkcję można urządzenia StorSimple toorecover używanych w przypadku awarii. StorSimple używa urządzenia trybu failover toomigrate hello danych z urządzenia źródłowego w urządzeniu docelowym tooanother hello w centrum danych. wskazówki Hello w tym artykule dotyczy urządzeń fizycznych serii tooStorSimple 8000 oraz chmury urządzenia z wersjami oprogramowania aktualizacji, 3 lub nowszym.

StorSimple używa hello **urządzeń** bloku toostart hello urządzenia funkcja trybu failover w przypadku hello awarii. Ten blok zawiera listę wszystkich usługi Menedżera urządzeń StorSimple tooyour podłączonego urządzenia hello StorSimple.

![Blok urządzeń](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Odzyskiwania awaryjnego (DR) i urządzenia trybu failover

W przypadku odzyskiwanie po awarii urządzenie podstawowe hello przestanie działać. StorSimple używa hello urządzenie podstawowe jako _źródła_ i przenosi tooanother danych chmury hello skojarzone _docelowej_ urządzenia. Ten proces jest hello określonego tooas *pracy awaryjnej*. powitania po ilustracja przedstawia proces hello pracy awaryjnej.

![Co się stanie w tryb failover urządzeń?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

urządzenie docelowe Hello Failover może być urządzenie fizyczne lub nawet urządzenia do chmury. Witaj urządzeniem docelowym może być znajduje się w hello tej samej lub innej lokalizacji geograficznej niż hello urządzenia źródłowego.

Podczas pracy awaryjnej hello można wybrać kontenery woluminów do migracji. StorSimple następnie zmienia hello własność kontenery woluminów z urządzenia docelowego toohello hello źródła urządzenia. Po właścicielem hello kontenery woluminów StorSimple usuwa kontenery z hello urządzenia źródłowego. Po zakończeniu usuwania hello może zakończyć się niepowodzeniem wstecz hello urządzenia docelowego. _Powrót po awarii_ transferów hello własność wstecz toohello oryginalnego urządzenia źródłowego.

### <a name="cloud-snapshot-used-during-device-failover"></a>Migawka w chmurze używane podczas pracy awaryjnej urządzenia

Po DR hello najnowszej kopii zapasowej chmury jest używane toorestore hello danych toohello urządzenia. Aby uzyskać więcej informacji dotyczących migawki w chmurze, zobacz [Użyj tootake usługi Menedżer StorSimple urządzenia hello ręcznego tworzenia kopii zapasowej](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

W serii StorSimple 8000 zasad tworzenia kopii zapasowych są skojarzone z kopii zapasowych. Jeśli istnieje wiele zasad tworzenia kopii zapasowych dla hello tego samego woluminu, a następnie wybiera StorSimple hello zasad tworzenia kopii zapasowej z hello największą liczbę woluminów. StorSimple na urządzeniu docelowym hello używa hello najnowszej kopii zapasowej z hello wybrane zasady tworzenia kopii zapasowej toorestore hello danych.

Załóżmy, że istnieją dwie zasady tworzenia kopii zapasowej, *defaultPol* i *customPol*:

* *defaultPol*: jeden wolumin *vol1*, jest uruchamiany codziennie, zaczynając od 22:30:00.
* *customPol*: cztery woluminy *vol1*, *vol2*, *vol3*, *vol4*, jest uruchamiany codziennie, zaczynając od 10:00 PM.

W takim przypadku StorSimple priorytetem spójności awarii i używa *customPol* została ona więcej woluminów. Hello najnowszej kopii zapasowej z tych zasad jest używane toorestore danych. Aby uzyskać więcej informacji na temat toocreate i zarządzanie zasadami tworzenia kopii zapasowej, należy przejść za[przy użyciu zasad tworzenia kopii zapasowej toomanage usługi Menedżer StorSimple urządzenia hello](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Typowe kwestie dotyczące pracy w trybie failover urządzenia

Przed przejścia w tryb failover urządzenia, przejrzyj hello następujących informacji:

* Przed rozpoczęciem pracy awaryjnej urządzenia, wszystkie woluminy hello w kontenery woluminów hello musi być w trybie offline. W przypadku nieplanowanego trybu failover woluminy StotSimple nastąpi automatyczne przejście w trybie offline. Jednak jeśli przeprowadzasz planowanego trybu failover (tootest DR), wszystkie woluminy hello należy wykonać w trybie offline.
* Tylko hello kontenery woluminów, które mają skojarzone migawka w chmurze są wyświetlane dla odzyskiwania po awarii. Musi istnieć co najmniej jeden kontener woluminów z danymi toorecover migawki skojarzonej chmury.
* W przypadku migawki w chmurze, obejmujące między wieloma kontenery woluminów StorSimple nie powiedzie się w tych kontenerach woluminu jako zestaw. W rzadkich wystąpienia Jeśli istnieją migawki lokalne, obejmujące między wieloma kontenery woluminów, ale migawki skojarzonej chmury nie StorSimple w tryb failover migawki lokalne powitania i dane lokalne powitania zostaną utracone po odzyskiwania po awarii.
* Witaj dostępnych urządzeń do odzyskiwania po awarii są urządzenia, które ma wystarczające tooaccommodate miejsca hello kontenery wybranego woluminu. Urządzenia, które nie mają wystarczająco dużo miejsca, nie są wyświetlane jako urządzenia docelowe.
* Po DR (na czas) hello danych dostępu może mieć wpływ na wydajność znacznie, jako urządzenie hello musi tooaccess hello danych z chmury hello i przechowywane lokalnie.

#### <a name="device-failover-across-software-versions"></a>Tryb failover urządzeń między wersjami oprogramowania

Usługa Menedżer urządzenia StorSimple w ramach wdrożenia może mieć wielu urządzeń, zarówno fizyczne i w chmurze, wszystkie wersje uruchamianie innego oprogramowania.

Użyj powitania po toodetermine tabeli może funkcjonować w trybie awaryjnym lub niepowodzeniem urządzenie tooanother Wstecz, na którym uruchomiono wersję innego oprogramowania i zachowanie typy woluminu hello podczas odzyskiwania po awarii.

#### <a name="failover-and-failback-across-software-versions"></a>Tryb failover i powrotu po awarii między wersjami oprogramowania

| Tryb failover / się nie powieść z kopii | Urządzenie fizyczne | Urządzenie w chmurze |
| --- | --- | --- |
| Aktualizacja 3 tooUpdate 4 |Woluminy warstwowe ponad warstwowej zakończyć się niepowodzeniem. <br></br>Woluminów przypiętych lokalnie w trybie Failover przypięty lokalnie. <br></br> Po przejściu w tryb failover podczas wykonywania migawki na urządzeniu hello aktualizacji 4 [śledzenia na podstawie heatmap](storsimple-update4-release-notes.md#whats-new-in-update-4) jest uruchamiane. |Przypięty lokalnie woluminach działających w trybie Failover jako warstwowego. |
| Aktualizacja 4 tooUpdate 3 |Woluminy warstwowe ponad warstwowej zakończyć się niepowodzeniem. <br></br>Woluminów przypiętych lokalnie w trybie Failover przypięty lokalnie. <br></br> Używane kopie zapasowe toorestore zachować heatmap metadanych. <br></br>Na podstawie Heatmap śledzenia nie jest dostępne w wersji Update 3 po powrotu po awarii. |Przypięty lokalnie woluminach działających w trybie Failover jako warstwowego. |


## <a name="device-failover-scenarios"></a>Scenariusze trybu failover urządzenia

W przypadku awarii, można wybrać toofail za pośrednictwem urządzenia StorSimple:

* [urządzenie fizyczne tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [urządzenia chmury tooa](storsimple-8000-device-failover-cloud-appliance.md).

Hello poprzedniego artykuły zawierają szczegółowe kroki dla każdego hello powyżej przypadków trybu failover.


## <a name="failback"></a>Powrót po awarii

Update 3 i nowszych StorSimple obsługuje powrót po awarii. Powrót po awarii jest tylko hello wstecznego pracy awaryjnej, hello docelowej staje się hello źródła i hello oryginalnego urządzenia źródłowego podczas awarii hello teraz staje się urządzeniem docelowym hello. 

Podczas powrotu po awarii StorSimple ponownie synchronizuje lokalizacji głównej hello danych toohello Wstecz, zatrzymuje hello We/Wy i działanie aplikacji i przechodzi wstecz toohello oryginalnej lokalizacji.

Po zakończeniu pracy w trybie failover StorSimple wykonuje hello następujące akcje:

* StorSimple czyści kontenery woluminów hello pracujących w z hello urządzenia źródłowego.
* StorSimple inicjuje zadania tła na kontenera woluminów (failover) na powitania urządzenia źródłowego. Jeśli toofail w trakcie hello zadanie jest w toku, pojawi się efekt toothat powiadomień. Poczekaj, aż zadanie hello jest pełną toostart hello powrotu po awarii.
* czas Hello toocomplete hello usuwania kontenerów woluminu zależy od różnych czynników, takich jak ilość danych, wieku hello danych, liczba kopii zapasowych i hello przepustowość sieci dostępną dla operacji hello.

Jeśli planowania testowy tryb failover, lub test powrotu po awarii, zaleca się przetestowanie kontenery woluminów o mniejszej ilości danych (GB). Zazwyczaj można uruchomić hello powrotu po awarii po 24 godzinach od hello przejścia w tryb failover.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

Q. **Co się stanie, jeśli hello odzyskiwania po awarii nie powiodło się lub ma częściowe Powodzenie?**

A. Jeśli hello odzyskiwania po awarii nie powiedzie się, zaleca się, spróbuj ponownie. Hello drugiego urządzenia trybu failover zadania zna hello postęp zadania pierwszy hello i rozpoczyna się od tego momentu i jego nowszych wersjach.

Q. **Urządzenie można usunąć w trakcie pracy awaryjnej urządzenia hello?**

A. Nie można usunąć urządzenia w trakcie odzyskiwania po awarii. Urządzenie można usunąć tylko po zakończeniu hello odzyskiwania po awarii. Możesz monitorować postęp zadania hello urządzenia trybu failover w hello **zadania** bloku.

Q. **Gdy hello wyrzucanie elementów bezużytecznych rozpoczyna się na powitania urządzenia źródłowego, aby dane lokalne powitania na urządzenia źródłowego jest usuwane?**

A. Wyrzucanie elementów bezużytecznych jest włączona na urządzenia źródłowego hello tylko wtedy, gdy urządzenie hello jest całkowicie oczyszczone. Oczyszczanie Hello obejmuje czyszczenia obiektów, które nie powiodły się za pośrednictwem z urządzenia źródłowego hello, takich jak woluminy, liczby obiektów kopii zapasowej (a nie dane), kontenery woluminów i zasady.

Q. **Co się stanie w przypadku hello usunąć zadanie skojarzone z kontenery woluminów hello w hello urządzenia źródłowego nie powiedzie się?**

A.  Jeśli hello usunięcie zadania nie powiodło się, można ręcznie usunąć hello kontenery woluminów. W hello **urządzeń** bloku, wybierz urządzenia źródłowego i kliknij przycisk **kontenery woluminów**. Kliknij przycisk Wybierz hello kontenery woluminów, których nie powiodła się nad oraz na powitania dolnej części bloku hello **usunąć**. Po usunięciu wszystkich hello przejścia w tryb failover kontenery woluminów na powitania urządzenia źródłowego, można uruchomić hello powrotu po awarii. Aby uzyskać więcej informacji, przejdź zbyt[usunąć kontener woluminów](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>Odzyskiwanie po awarii ciągłości biznesowej (BCDR)

Scenariusz odzyskiwania (BCDR) po awarii ciągłości biznesowej występuje, gdy centrum danych Azure całego hello przestanie działać. Ten scenariusz może mieć wpływ na usługi Menedżer StorSimple urządzenia i hello skojarzone urządzenia StorSimple.

Jeśli urządzenia StorSimple zarejestrowano tuż przed wystąpił awarii, to urządzenie może wymagać tooundergo stanu fabrycznego. Po awarii hello urządzenia StorSimple hello zostaną wyświetlone w hello portalu Azure jako w trybie offline. Urządzenia muszą zostać usunięte z portalu hello. Resetuj hello urządzenia toofactory domyślne, a następnie zarejestruj go ponownie hello usługi.

## <a name="next-steps"></a>Następne kroki

Jeśli wszystko jest gotowe tooperform urządzenia trybu failover, należy wybrać jedną z hello następujące scenariusze, aby uzyskać szczegółowe instrukcje:

- [Tryb failover tooanother urządzenia fizycznego](storsimple-8000-device-failover-physical-device.md)
- [Tryb failover toohello takie same urządzenia](storsimple-8000-device-failover-same-device.md)
- [Tryb failover tooStorSimple urządzenia chmury](storsimple-8000-device-failover-cloud-appliance.md)

Jeśli nie powiodło przez urządzenie, wybierz jedną z hello następujące opcje:

* [Dezaktywuj lub usuń urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* [Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

