---
title: aaaStorSimple trybu failover i odzyskiwania po awarii | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toofail za pośrednictwem sieci tooitself urządzenia StorSimple, inne fizyczne urządzenie lub urządzenia wirtualnego."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Tryb failover i odzyskiwania po awarii dla urządzenia StorSimple
## <a name="overview"></a>Omówienie
W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem urządzenia StorSimple w razie awarii hello. Tryb failover umożliwi toomigrate danych z urządzenia źródła w tooanother datacenter hello fizycznego lub wirtualnego urządzenia znajdujące się w hello tej samej lub innej lokalizacji geograficznej. 

Odzyskiwania awaryjnego (DR) jest zorkiestrowana za pomocą funkcji trybu failover urządzenia hello i zainicjowano hello **urządzeń** strony. Ta strona rejestruje wszystkie usługi Menedżer StorSimple tooyour podłączonego urządzenia hello StorSimple. Dla każdego urządzenia hello przyjazna nazwa, stan, elastycznie i maksymalną pojemność typ i model są wyświetlane.

![Strona urządzenia](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych i wirtualnych tooStorSimple przez wszystkie wersje oprogramowania.

## <a name="disaster-recovery-dr-and-device-failover"></a>Odzyskiwania awaryjnego (DR) i urządzenia trybu failover
W przypadku odzyskiwanie po awarii urządzenie podstawowe hello przestanie działać. W takiej sytuacji można przenieść danych w chmurze hello skojarzone z hello urządzenia nie powiodło się tooanother urządzenia przy użyciu urządzenie podstawowe hello hello *źródła* i określając inne urządzenie jako hello *docelowej*. Można wybrać co najmniej jeden wolumin kontenerów toomigrate toohello urządzenia docelowego. Ten proces jest hello określonego tooas *pracy awaryjnej*. 

Podczas pracy awaryjnej hello hello kontenery woluminów z urządzenia źródłowego hello zmienić własności i zostały przeniesione toohello urządzenia docelowego. Po kontenery woluminów hello zmienić własność, te są usuwane z urządzenia źródłowego hello. Po zakończeniu usuwania hello urządzenie docelowe hello następnie można ponownie nie.

Zwykle po odzyskiwania po awarii, hello najnowszej kopii zapasowej jest używane toorestore hello danych toohello urządzenia. Jednak w przypadku wielu zasad tworzenia kopii zapasowych hello tego samego woluminu, następnie pobiera pobrania hello zasad tworzenia kopii zapasowej z największą liczbą woluminów hello i hello najnowszej kopii zapasowej z tej zasady jest używane toorestore hello danych na urządzeniu docelowym hello.

Na przykład jeśli istnieją dwie zasady tworzenia kopii zapasowej (jeden domyślny i jeden niestandardowy) *defaultPol*, *customPol* z hello poniższe informacje:

* *defaultPol* : jeden wolumin *vol1*, jest uruchamiany codziennie, zaczynając od 22:30:00.
* *customPol* : cztery woluminy *vol1*, *vol2*, *vol3*, *vol4*, jest uruchamiany codziennie, zaczynając od 10:00 PM.

W takim przypadku *customPol* będzie służyć jako ma więcej woluminów i z różnym priorytetem, spójności awarii. Hello najnowszej kopii zapasowej z tych zasad jest używane toorestore danych.

## <a name="considerations-for-device-failover"></a>Zagadnienia dotyczące urządzenia trybu failover
W przypadku hello awarii może wybrać toofail za pośrednictwem urządzenia StorSimple:

* tooa urządzenia fizycznego 
* tooitself
* Urządzenie wirtualne tooa

Dla dowolnego urządzenia trybu failover należy uwzględnić następujące hello:

* Witaj wymagania wstępne dla odzyskiwania po awarii są wszystkie woluminy hello w kontenery woluminów hello są w trybie offline, a hello kontenery woluminów ma skojarzoną migawkę w chmurze. 
* Witaj dostępnych urządzeń do odzyskiwania po awarii są urządzenia, które ma wystarczające tooaccommodate miejsca hello kontenery wybranego woluminu. 
* Witaj urządzenia, które są połączone tooyour usługi, ale nie spełniają kryteria hello wystarczające miejsce nie będą dostępne jako urządzenia docelowe.
* Następujące odzyskiwania po awarii na czas hello danych dostępu może mieć wpływ na wydajność znacznie, jako urządzenie hello będzie konieczne tooaccess hello danych z chmury hello i przechowywane lokalnie.

#### <a name="device-failover-across-software-versions"></a>Tryb failover urządzeń między wersjami oprogramowania
W ramach wdrożenia usługi Menedżer StorSimple może mieć wielu urządzeń fizycznych i wirtualnych, wszystkie wersje uruchamianie innego oprogramowania. W zależności od wersji oprogramowania hello hello typy woluminu na urządzeniach hello mogą być również inny. Na przykład urządzenie z uruchomioną Update 2 lub nowszego lokalnie przypięty i woluminami warstwowymi (z archiwizacji jest podzbiorem warstwowa). Urządzenia przed aktualizacją 2 na powitania ma warstwy drugiej oraz archiwalne woluminów. 

Użyj powitania po toodetermine tabeli, możesz w trybie Failover urządzenie tooanother, na którym uruchomiono zachowanie oprogramowania innej wersji i hello typów woluminu podczas odzyskiwania po awarii.

| Tryb failover z | Dozwolone w przypadku urządzenia fizycznego | Dozwolony dla urządzenia wirtualnego |
| --- | --- | --- |
| Aktualizacja 2 toopre aktualizacja 1 (wersja, 0.1, 0.2, 0.3) |Nie |Nie |
| Aktualizacja 2 tooUpdate 1 (1, 1.1, 1.2) |Tak <br></br>Jeśli przy użyciu przypięty lokalnie lub woluminami warstwowymi lub mieszane powitalne dwa woluminy są zawsze awaryjnie jako warstwy. |Tak<br></br>Za pomocą lokalnie przypięty woluminów, te są nie ponad warstwy. |
| Aktualizacja 2 tooUpdate 2 (późniejsza wersja) |Tak<br></br>Używania woluminów lokalnie przypiętych lub warstwowych lub dwóch różnych, woluminy hello są zawsze nie powiodło się za pośrednictwem jako hello uruchamianie typ woluminu; warstwowej jako warstwowych i przypięty lokalnie, przypięty lokalnie. |Tak<br></br>Za pomocą lokalnie przypięty woluminów, te są nie ponad warstwy. |

#### <a name="partial-failover-across-software-versions"></a>Częściowe trybu failover między wersjami oprogramowania
Wykonaj tę wskazówkę zamierzając tooperform częściowe trybu failover przy użyciu urządzenia StorSimple źródła systemem docelowym przed aktualizacją tooa 1 z aktualizacji 1 lub nowszą. 

| Częściowe przejściu w tryb failover | Dozwolone w przypadku urządzenia fizycznego | Dozwolony dla urządzenia wirtualnego |
| --- | --- | --- |
| Przed wprowadzeniem aktualizacji Update 1 (wersja, 0.1, 0.2, 0.3) tooUpdate 1 lub nowszy |Tak, wymienione poniżej hello najlepsze praktyki poradę. |Tak, wymienione poniżej hello najlepsze praktyki poradę. |

> [!TIP]
> Wystąpił chmury metadane i dane formatu zmiany w aktualizacji 1 lub nowszy. W związku z tym nie zaleca się częściowe trybu failover z tooUpdate 1 przed aktualizacją 1 lub nowszy. Tooperform częściowe trybu failover, należy Zalecamy najpierw zastosować Update 1 lub nowszy na obu hello urządzeń (źródłowy i docelowy), a następnie kontynuować hello trybu failover. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Tryb failover tooanother urządzenia fizycznego
Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia fizycznego.

1. Sprawdź, czy ten kontener woluminów hello żądane toofail za pośrednictwem skojarzone migawki w chmurze.
2. Na powitania **urządzeń** kliknij przycisk hello **kontenery woluminów** kartę.
3. Wybierz kontener woluminów za pośrednictwem urządzenia tooanother chcesz toofail. Kliknij przycisk Lista kontenera woluminów hello hello toodisplay woluminów, w tym kontenerze. Wybierz wolumin, a następnie kliknij przycisk **Przełącz do trybu Offline** tootake hello woluminu w trybie offline. Powtórz ten proces dla wszystkich woluminów hello w hello kontenera woluminów.
4. Hello Powtórz poprzedni krok dla wszystkich hello kontenery woluminów chcesz toofail za pośrednictwem tooanother urządzenia.
5. Na powitania **urządzeń** kliknij przycisk **pracy awaryjnej**.
6. W Kreatorze hello, który zostaje otwarty, w obszarze **wybierz toofail kontenera woluminu za pośrednictwem**:
   
   1. Na liście hello kontenery woluminów wybierz kontenery woluminów hello, którą chcesz toofail za pośrednictwem.
      **Tylko hello kontenery woluminów z migawkami skojarzonej chmury i woluminy w trybie offline są wyświetlane.**
   2. W obszarze **wybierz urządzenie docelowe** woluminów hello w kontenerach hello wybrana, wybierz urządzenie docelowe z listy rozwijanej hello dostępnych urządzeń. Witaj tylko te urządzenia, które mają hello dostępnej pojemności są wyświetlane na liście rozwijanej hello.
   3. Na koniec przejrzeć wszystkie ustawienia trybu failover hello w **potwierdzić trybu failover**. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Utworzono zadanie trybu failover, które można monitorować za pomocą hello **zadania** strony. Jeśli kontenera woluminów hello zakończonych niepowodzeniem na woluminach lokalnych, zostanie wyświetlona indywidualnych zadań przywracania dla każdego woluminu lokalnego (a nie dla woluminów warstwowych) w kontenerze hello. Przywracania zadania może potrwać jakiś czas toocomplete. Prawdopodobnie hello zadania trybu failover może zakończyć się wcześniej. Należy zauważyć, że woluminy te będą lokalnych gwarancji dopiero po zakończeniu zadania przywracania hello. Po zakończeniu pracy awaryjnej hello Przejdź toohello **urządzeń** strony.                                            
   
   1. Wybierz urządzenie hello, które zostało użyte jako urządzenie docelowe hello hello procesu pracy awaryjnej.
   2. Przejdź toohello **kontenery woluminów** strony. Wszystkie kontenery woluminów hello, wraz z woluminów hello ze starym urządzeniem hello, powinien być wyświetlany.

## <a name="failover-using-a-single-device"></a>Tryb failover przy użyciu jednego urządzenia
Wykonaj następujące kroki, jeśli masz tylko jeden tooperform urządzenia i potrzeb trybu failover hello.

1. Twórz migawki chmurze wszystkie woluminy hello w urządzeniu.
2. Zresetowanie urządzenia toofactory domyślnych. Wykonaj hello szczegółowe instrukcje w [jak tooreset toofactory urządzenia StorSimple domyślne ustawienia](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Konfigurowanie urządzenia i zarejestrować go ponownie przy użyciu usługi Menedżer StorSimple.
4. Na powitania **urządzeń** stronie powitania starym urządzeniem powinny być widoczne jako **Offline**. Witaj nowo zarejestrowane urządzenia powinny być widoczne jako **Online**.
5. Dla hello nowe urządzenie wykonaj najpierw hello minimalnej konfiguracji urządzenia hello. 
   
   > [!IMPORTANT]
   > **Konfiguracja minimalna hello najpierw nie zostało ukończone, programu DR zakończy się niepowodzeniem w wyniku błędu w hello bieżąca implementacja. Ten problem zostanie rozwiązany w nowszej wersji.**
   > 
   > 
6. Wybierz urządzenie starego hello (stan w trybie offline), a następnie kliknij przycisk **pracy awaryjnej**. W Kreatorze hello, które są prezentowane w tryb failover to urządzenie i określ urządzenie docelowe hello jako hello nowo zarejestrowanym urządzeniem. Aby uzyskać szczegółowe instrukcje, zobacz zbyt[awaryjnie urządzenie fizyczne tooanother](#fail-over-to-another-physical-device).
7. Zadanie przywracania urządzenie zostanie utworzony, można monitorować z hello **zadania** strony.
8. Po pomyślnym ukończeniu zadania hello dostępu hello nowe urządzenie i przejdź toohello **kontenery woluminów** strony. Wszystkie kontenery woluminów hello ze starym urządzeniem hello powinno być teraz migrowanych toohello nowe urządzenie.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Tryb failover tooa urządzenia wirtualnego StorSimple
Musi mieć StorSimple, urządzenie wirtualne utworzone i skonfigurowane wcześniejsze toorunning tej procedury. Jeśli z aktualizacją Update 2, rozważ użycie urządzenie wirtualne 8020 dla hello DR, który ma 64 TB i używa magazynu w warstwie Premium. 

Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia wirtualnego StorSimple hello.

1. Sprawdź, czy ten kontener woluminów hello żądane toofail za pośrednictwem skojarzone migawki w chmurze.
2. Na powitania **urządzeń** kliknij przycisk hello **kontenery woluminów** kartę.
3. Wybierz kontener woluminów za pośrednictwem urządzenia tooanother chcesz toofail. Kliknij przycisk Lista kontenera woluminów hello hello toodisplay woluminów, w tym kontenerze. Wybierz wolumin, a następnie kliknij przycisk **Przełącz do trybu Offline** tootake hello woluminu w trybie offline. Powtórz ten proces dla wszystkich woluminów hello w hello kontenera woluminów.
4. Hello Powtórz poprzedni krok dla wszystkich hello kontenery woluminów chcesz toofail za pośrednictwem tooanother urządzenia.
5. Na powitania **urządzeń** kliknij przycisk **pracy awaryjnej**.
6. W Kreatorze hello, który zostaje otwarty, w obszarze **Wybierz wolumin kontenera toofailover**, wykonaj następujące czynności hello:
   
    a. Na liście hello kontenery woluminów wybierz kontenery woluminów hello, którą chcesz toofail za pośrednictwem.
   
    **Tylko hello kontenery woluminów z migawkami skojarzonej chmury i woluminy w trybie offline są wyświetlane.**
   
    b. W obszarze **wybierz urządzenie docelowe dla woluminów hello w kontenerach hello wybrane**, wybierz hello urządzenia wirtualnego StorSimple z listy rozwijanej hello dostępnych urządzeń. **Witaj tylko te urządzenia, które ma wystarczającej wydajności, są wyświetlane na liście rozwijanej hello.**  
7. Na koniec przejrzeć wszystkie ustawienia trybu failover hello w **potwierdzić trybu failover**. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Po zakończeniu pracy awaryjnej hello Przejdź toohello **urządzeń** strony.
   
    a. Wybierz hello urządzenia wirtualnego StorSimple, która została użyta jako urządzenie docelowe hello hello procesu pracy awaryjnej.
   
    b. Przejdź toohello **kontenery woluminów** strony. Teraz wszystkie kontenery woluminów hello, wraz z woluminów hello ze starym urządzeniem hello powinien być wyświetlany.

![Zobacz film](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **Zobacz film**

Kliknij toowatch film wideo przedstawiający sposób można przywrócić nieudanej przez urządzenie fizyczne urządzenia wirtualnego tooa w chmurze hello [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Powrót po awarii
Update 3 i nowszych StorSimple obsługuje powrót po awarii. Po zakończeniu pracy awaryjnej hello hello są wykonywane następujące akcje:

* kontenery woluminów Hello pracujących w są czyszczone z urządzenia źródłowego hello.
* Zadanie w tle na kontenera woluminów (failover) jest inicjowana na powitania urządzenia źródłowego. Jeśli toofailback podczas hello zadania w toku, otrzymasz efekt toothat powiadomień. Konieczne będzie toowait do czasu ukończenia toostart hello powrotu po awarii hello zadania. 
  
    Hello czasu toocomplete hello usuwania kontenerów woluminu zależy od różnych czynników, takich jak ilość danych, wieku hello danych, liczba kopii zapasowych i hello przepustowość sieci dostępną dla operacji hello. Jeśli planujesz praca awaryjna testu powrotu po awarii, zaleca się przetestowanie kontenery woluminów o mniejszej ilości danych (GB). W większości przypadków można uruchomić hello powrotu po awarii po 24 godzinach od hello przejścia w tryb failover. 

## <a name="frequently-asked-questions"></a>Często zadawane pytania
Q. **Co się stanie, jeśli hello odzyskiwania po awarii nie powiodło się lub ma częściowe Powodzenie?**

A. Jeśli hello odzyskiwania po awarii nie powiedzie się, zaleca się, spróbuj ponownie. Witaj drugim razem, odzyskiwania po awarii wie, jaki wszystkie były generowane i podczas procesu hello wstrzymany powitania po raz pierwszy. Hello procesu odzyskiwania po awarii rozpoczyna się od tego momentu i jego nowszych wersjach. 

Q. **Urządzenie można usunąć w trakcie pracy awaryjnej urządzenia hello?**

A. Nie można usunąć urządzenia w trakcie odzyskiwania po awarii. Urządzenie można usunąć tylko po zakończeniu hello odzyskiwania po awarii.

Q.    **Gdy hello wyrzucanie elementów bezużytecznych rozpoczyna się na powitania urządzenia źródłowego, aby dane lokalne powitania na urządzenia źródłowego jest usuwane?**

A. Wyrzucanie elementów bezużytecznych zostaną włączone na urządzeniu źródła hello tylko wtedy, gdy urządzenie hello jest całkowicie wyczyścić. Oczyszczanie Hello obejmuje czyszczenia obiektów, które nie powiodły się za pośrednictwem z urządzenia źródłowego hello, takich jak woluminy, liczby obiektów kopii zapasowej (a nie dane), kontenery woluminów i zasady.

Q. **Co się stanie w przypadku hello usunąć zadanie skojarzone z kontenery woluminów hello w hello urządzenia źródłowego nie powiedzie się?**

A.  Hello usunięcie zadania nie powiodło się, będzie konieczne usunięcie hello wyzwalacza toomanually hello kontenery woluminów. W hello **urządzeń** wybierz urządzenia źródłowego i kliknij przycisk **kontenery woluminów**. Kliknij przycisk Wybierz hello kontenery woluminów, których nie powiodła się nad oraz na powitania u dołu strony hello, **usunąć**. Po usunięciu wszystkich hello przejścia w tryb failover kontenery woluminów na powitania urządzenia źródłowego, można uruchomić hello powrotu po awarii.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Odzyskiwanie po awarii ciągłości biznesowej (BCDR)
Scenariusz odzyskiwania (BCDR) po awarii ciągłości biznesowej występuje, gdy centrum danych Azure całego hello przestanie działać. Może to mieć wpływ na usługi Menedżer StorSimple i hello skojarzone urządzenia StorSimple.

W przypadku urządzeń StorSimple, które zostały zarejestrowane bezpośrednio przed zamknięciem wystąpił awarii, te urządzenia StorSimple może wymagać tooundergo stanu fabrycznego. Po awarii hello urządzenia StorSimple hello będą wyświetlane w trybie offline. urządzenia StorSimple Hello muszą zostać usunięte z portalu hello i resetowania do ustawień fabrycznych należy zrobić, następuje świeże rejestracji.

## <a name="next-steps"></a>Następne kroki
* Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-deactivate-and-delete-device.md).
* Informacje o sposobie toouse hello Menedżer StorSimple usługi, należy przejść za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

