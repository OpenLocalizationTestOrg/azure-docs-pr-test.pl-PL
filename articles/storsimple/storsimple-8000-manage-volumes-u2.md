---
title: "aaaManage woluminów StorSimple (aktualizacja Update 3) | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd, modyfikowanie, monitorowania i usuwanie woluminów StorSimple i jak tootake ich w tryb offline, jeśli jest to konieczne."
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
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Użyj hello woluminy toomanage usługi Menedżer urządzenia StorSimple (Aktualizacja 3 lub nowszym)

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać woluminach urządzeń z serii StorSimple 8000 hello uruchomioną aktualizacją 3 lub nowszym.

Witaj usługi Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello. Użycie woluminów toomanage portalu Azure hello na wszystkich urządzeniach. Można również utworzyć i zarządzać usługami StorSimple, zarządzania urządzeniami, zasady tworzenia kopii zapasowej i kopii zapasowej wykazu i wyświetlać alerty.

## <a name="volume-types"></a>Typy woluminu

Woluminy StorSimple można:

* **Przypięty lokalnie woluminach**: dane w tych woluminów pozostaną na urządzeniu StorSimple lokalne powitania przez cały czas.
* **Woluminami warstwowymi**: dane w tych woluminów mogą zostaną przeniesione toohello chmury.

Archiwizacja wolumin jest typem woluminu warstwowego. Witaj większy rozmiar fragmentu deduplikacji używana w przypadku woluminów archiwizacji umożliwia hello urządzenia tootransfer większych segmenty toohello danych w chmurze.

W razie potrzeby można zmienić typ woluminu hello z lokalnym tootiered lub toolocal warstwowego. Aby uzyskać więcej informacji, przejdź zbyt[zmienić typ woluminu hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Woluminów przypiętych lokalnie

Woluminów przypiętych lokalnie są w pełni woluminów, które nie warstwy toohello danych w chmurze, zapewniając lokalnego gwarantuje dla danych podstawowych, niezależnie od łączności chmury. Dane dotyczące woluminów przypiętych lokalnie nie jest deduplikowany i skompresowane; jednak migawek woluminów przypiętych lokalnie są deduplikowane. 

Woluminów przypiętych lokalnie są w pełni zaaprowizowanym; w związku z tym musi mieć wystarczającą ilość miejsca na urządzeniu, podczas ich tworzenia. Umożliwia obsługę woluminów przypiętych lokalnie tooa maksymalnym rozmiarze 8 TB na urządzeniu StorSimple 8100 hello i 20 TB na urządzeniu 8600 hello. StorSimple rezerwuje pozostałego miejsca lokalne powitania na urządzeniu hello migawek, metadane i przetwarzania danych. Można zwiększyć rozmiar hello woluminu przypiętego lokalnie toohello maksymalną dostępnego miejsca, ale nie można zmniejszyć rozmiar woluminu utworzonej hello.

Podczas tworzenia woluminu przypiętego lokalnie hello dostępnego miejsca na potrzeby tworzenia woluminów warstwowych zostanie zmniejszona. Witaj odwrotnej również ma wartość true: Jeśli masz istniejące woluminy warstwowe hello miejsca dla tworzenia lokalnie przypięty woluminów będzie niższa niż maksymalnych hello podanych powyżej. Aby uzyskać więcej informacji na woluminach lokalnych, zobacz toohello [— często zadawane pytania na woluminów przypiętych lokalnie](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Woluminy warstwowe

Woluminy warstwowe są woluminy alokowane elastycznie, w których hello często używanych danych pozostaje lokalne powitania urządzenia i mniej często używanych danych jest automatycznie do warstwy toohello chmury. Alokowanie elastyczne jest technologii wirtualizacji, w której dostępny magazyn pojawia się tooexceed zasobów fizycznych. Zamiast z wyprzedzeniem rezerwowania wystarczającej ilości miejsca, StorSimple używa alokowania tooallocate inicjowania obsługi administracyjnej wystarczającego miejsca toomeet bieżące wymagania. Hello elastycznej rodzaj magazynu w chmurze ułatwia takie podejście, ponieważ StorSimple można zwiększyć lub zmniejszyć chmury magazynu toomeet zmieniających się potrzeb.

Jeśli używasz woluminu warstwowego na potrzeby danych archiwalnych, wybierz hello hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru toochange hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli nie zaznaczysz tej opcji, hello odpowiedni wolumin warstwowy użyje rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury.


### <a name="provisioned-capacity"></a>Udostępnione pojemności

Można znaleźć w poniższej tabeli dla maksymalnej pojemności udostępnione dla każdego typu urządzenia i woluminu toohello. (Należy pamiętać, że woluminy przypięte lokalnie nie są dostępne na urządzeniu wirtualnym).

|  | Rozmiar maksymalny wolumin warstwowy | Rozmiar woluminu przypiętego lokalnie maksymalna |
| --- | --- | --- |
| **Fizyczne urządzenia** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Urządzenia wirtualne** | | |
| 8010 |30 TB |Nie dotyczy |
| 8020 |64 TB |Nie dotyczy |

## <a name="hello-volumes-blade"></a>Witaj woluminów bloku

Witaj **woluminów** bloku umożliwia toomanage hello magazynu woluminy, które są udostępniane na urządzeniu Microsoft Azure StorSimple hello Twojej inicjatorów (serwerów). Wyświetla listę woluminów hello na usługi tooyour podłączonego urządzenia StorSimple hello.

 ![Strony woluminów](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Wolumin składa się z szeregu atrybuty:

* **Nazwa woluminu** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello woluminu. Ta nazwa jest również używana do monitorowania raportów podczas filtrowania w określonym woluminie. Po utworzeniu hello woluminu, nie można zmienić nazwy.
* **Stan** — może być w trybie online lub offline. Jeśli wolumin jest w trybie offline, nie jest widoczne tooinitiators (serwery) dozwoloną dostępu toouse hello woluminu.
* **Pojemność** — określa hello łączna ilość danych, które mogą być przechowywane przez inicjatora hello (serwer). Przypięty lokalnie woluminy są w pełni zaaprowizowanym i znajdują się na urządzeniu StorSimple hello. Woluminy warstwowe są alokowane elastycznie i danych hello jest deduplikowany. Z woluminy alokowane elastycznie urządzenia nie wstępnie przydzielić pojemności magazynu fizycznego wewnętrznych lub w chmurze hello zgodnie z tooconfigured pojemność woluminu. pojemność woluminu Hello jest przydzielone i używane na żądanie.
* **Typ** — wskazuje, czy wolumin hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.

Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:

* Dodawanie woluminu 
* Modyfikowanie woluminu 
* Zmień typ woluminu hello
* Usuwanie woluminu 
* Przełącz do trybu offline woluminu 
* Monitor woluminu 

## <a name="add-a-volume"></a>Dodawanie woluminu

Możesz [utworzony wolumin](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) podczas wdrażania urządzenia StorSimple 8000 serii. Dodawanie woluminu jest podobnej procedury.

#### <a name="tooadd-a-volume"></a>tooadd woluminu

1. Z hello Tabelaryczny spis urządzeń hello w hello **urządzeń** bloku, wybierz swoje urządzenie. Kliknij pozycję **+ Dodaj wolumin**.

    ![Dodawanie nowego woluminu](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. W hello **Dodaj wolumin** bloku:
   
    1. Witaj **wybierz urządzenie** pole jest wypełniane automatycznie z bieżącego urządzenia.

    2. Z listy rozwijanej hello Wybierz kontener woluminów hello wymagających tooadd woluminu.

    3.  Wpisz wartość pola **Nazwa** dla woluminu. Po utworzeniu hello woluminu, nie można zmienić nazwy woluminów hello.

    4. Na liście rozwijanej hello, wybierz hello **typu** dla woluminu. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz wolumin typu **Przypięty lokalnie**. W przypadku wszystkich innych danych wybierz wolumin typu **Warstwowy**. Jeśli używasz tego woluminu na potrzeby danych archiwalnych, wybierz opcję **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych**.
      
       Wolumin warstwowy jest alokowany elastycznie i można go szybko utworzyć. Wybieranie **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** dla woluminu warstwowego celem danych archiwalnych zmiany hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli to pole nie jest zaznaczone, odpowiedni wolumin warstwowy hello używa rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury.
       
       Wolumin przypięty lokalnie jest alokowany nieelastycznie i gwarantuje, że hello główne dane na woluminie hello pozostaje toohello lokalne urządzenia i nie zostaną przeniesione toohello chmury.  Jeśli tworzysz wolumin przypięty lokalnie, urządzenia hello wyszukuje dostępne miejsce w warstwach lokalne powitania tooprovision hello ilość hello żądany rozmiar. Witaj operacji tworzenia woluminu przypiętego lokalnie może obejmować przenoszenie istniejących danych z chmury toohello urządzenia hello i czas hello toocreate hello woluminu może trwać długo. Łączny czas Hello zależy od rozmiaru hello hello elastycznie woluminu, dostępnej przepustowości sieci i danych hello na urządzeniu.

    5. Określ hello **alokowana pojemność** dla woluminu. Zanotuj hello pojemności dostępnej w oparciu wybrany typ woluminu hello. Witaj określony rozmiar woluminu nie może przekraczać hello dostępnego miejsca.
      
       Można alokować woluminy przypięte lokalnie w górę too8.5 TB lub woluminy warstwowe się too200 TB na urządzeniu 8100 hello. Na urządzeniu 8600 większych hello można udostępnić woluminów przypiętych lokalnie too22.5 TB lub woluminy warstwowe się too500 TB. Lokalne miejsce na urządzeniu hello jest hello wymagane toohost pracy zestaw woluminów warstwowych, tworzenie woluminów przypiętych lokalnie ma wpływ na powitania miejsce dostępne do alokowania na woluminach warstwowych. Dlatego jeśli tworzysz wolumin przypięty lokalnie, miejsce dostępne na potrzeby tworzenia woluminów warstwowych zmniejsza się. Podobnie jeśli został utworzony wolumin warstwowy, zostanie zmniejszona hello dostępnego miejsca na potrzeby tworzenia woluminów przypiętych lokalnie.
      
       Jeśli dostarczasz woluminu przypiętego lokalnie 8,5 TB (maksymalny dozwolony rozmiar) na urządzeniu 8100 zostały wyczerpane wszystkich hello lokalne miejsce dostępne na urządzeniu hello. Nie można tworzyć woluminów warstwowych od tego momentu i jego nowszych wersjach, ponieważ nie ma już miejsca lokalnego na powitania urządzenia toohost hello zestaw roboczy hello warstwowej woluminu. Istniejące woluminy warstwowe również wpływają na dostępne miejsce hello. Jeśli na przykład masz urządzenie 8100 z woluminami warstwowymi o wielkości około 106 TB, tylko 4 TB są dostępne dla woluminów przypiętych lokalnie.

    6. W hello **połączone hosty** kliknij strzałkę hello. 

        ![Połączone hosty](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. W hello **połączone hosty** bloku, wybierz istniejący ACR lub Dodaj nowe ACR. Jeśli nowy ACR, następnie podaj **nazwa** dla rekordu ACR, podaj hello **iSCSI Qualified Name** (IQN) hosta z systemem Windows. Jeśli nie masz hello IQN, przejdź zbyt[hello Get IQN hosta z systemem Windows Server](#get-the-iqn-of-a-windows-server-host). Kliknij przycisk **Utwórz**. Wolumin zostanie utworzona z hello określone ustawienia.

        ![Kliknięcie pozycji Utwórz](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Nowy wolumin jest teraz gotowy toouse.

> [!NOTE]
> Jeśli Tworzenie woluminu przypiętego lokalnie, a następnie utworzyć inną lokalnie przypięty woluminu natychmiast po zadania tworzenia woluminu hello są wykonywane sekwencyjnie. zadanie tworzenia woluminu pierwszy Hello musi zakończyć się przed rozpoczęciem hello następne zadanie tworzenia woluminu.

## <a name="modify-a-volume"></a>Modyfikowanie woluminu

Zmodyfikuj woluminu, gdy będziesz potrzebować tooexpand lub zmień hello hosty, które uzyskują dostęp do woluminu hello.

> [!IMPORTANT]
> * Jeśli zmodyfikujesz hello rozmiar woluminu na urządzeniu hello hello rozmiar woluminu musi toobe zmienione na powitania hosta oraz.
> * powitania po stronie hosta opisane w tym miejscu są przeznaczone dla systemu Windows Server 2012 (2012 R2). Procedury dla systemu Linux lub z innymi systemami operacyjnymi hosta może się różnić. Podczas modyfikowania hello woluminu na hoście z innym systemem operacyjnym, można znaleźć instrukcje systemu operacyjnego hosta tooyour.

#### <a name="toomodify-a-volume"></a>toomodify woluminu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. Hello Tabelaryczny spis urządzeń hello, zaznacz urządzenie hello woluminu hello czy zamierzasz toomodify. Kliknij przycisk **Ustawienia > woluminów**.

    ![Przejdź do bloku tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. Z hello tabelarycznej listę woluminów wybrać wolumin hello i kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke. Wybierz **przełączyć do trybu offline** tootake hello woluminu, należy zmodyfikować w trybie offline.

    ![Wybierz, a następnie przełącz wolumin do trybu offline](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. W hello **przełączyć do trybu offline** bloku, przejrzyj wpływ hello przełączania w tryb offline hello woluminu i zaznacz odpowiednie pole wyboru hello. Upewnij się, że hello odpowiednich woluminów na hoście hello jest najpierw w trybie offline. Informacji na temat sposobu tootake woluminu w trybie offline na serwerze hosta połączenia tooStorSimple można znaleźć toooperating systemu szczegółowych instrukcji. Kliknij przycisk **przełączyć do trybu offline**.

    ![Przejrzyj wpływ przełączania w tryb offline woluminu](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Po wolumin hello jest w trybie offline (jak to przedstawiono stan woluminu hello), wybierz wolumin hello i kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke. Wybierz **zmodyfikować woluminu**.

    ![Wybierz Modyfikuj woluminu](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. W hello **zmodyfikować woluminu** bloku, możesz wprowadzić hello następujące zmiany:
   
   1. Witaj woluminu **nazwa** nie może być edytowany.
   2. Konwertuj hello **typu** z tootiered przypiętych lokalnie lub warstwowych toolocally przypięty (zobacz [zmienić typ woluminu hello](#change-the-volume-type) Aby uzyskać więcej informacji).
   3. Zwiększ hello **alokowana pojemność**. Witaj **alokowana pojemność** zwiększyć. Nie można zmniejszyć wolumin, po jego utworzeniu.
   4. W obszarze **połączone hosty**, można zmodyfikować hello ACR. toomodify ACR wolumin hello musi być w trybie offline.

       ![Przejrzyj wpływ przełączania w tryb offline woluminu](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Kliknij przycisk **zapisać** toosave zmiany. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. Witaj portalu Azure wyświetli komunikat aktualizowania woluminu. Go zostanie wyświetlony komunikat Powodzenie hello woluminu została zaktualizowana pomyślnie.

    ![Przejrzyj wpływ przełączania w tryb offline woluminu](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Jeśli rozszerzasz wolumin, wykonaj następujące kroki na komputerze hosta z systemem Windows hello:
   
   1. Przejdź za**Zarządzanie komputerem** ->**Zarządzanie dyskami**.
   2. Kliknij prawym przyciskiem myszy **Zarządzanie dyskami** i wybierz **Skanuj dyski**.
   3. Hello listy dysków, wybierz wolumin hello, które zostało zaktualizowane, kliknij prawym przyciskiem myszy, a następnie wybierz **Rozszerz wolumin**. zostanie uruchomiony Kreator rozszerzania woluminów Hello. Kliknij przycisk **Dalej**.
   4. Ukończ Kreatora hello, akceptując wartości domyślne hello. Po zakończeniu pracy Kreatora hello hello woluminu powinien być wyświetlony hello zwiększyć rozmiar.
      
      > [!NOTE]
      > Jeśli Rozszerz wolumin przypięty lokalnie, a następnie rozwiń węzeł przypięty lokalnie inny wolumin natychmiast po hello woluminu rozszerzenia zadania są wykonywane sekwencyjnie. Witaj pierwszego zadania rozszerzenia woluminu musi zakończyć się przed rozpoczęciem następnego zadania rozszerzania woluminów hello.
      

## <a name="change-hello-volume-type"></a>Zmień typ woluminu hello

Można zmienić typ woluminu hello z warstwową toolocally przypięty lub tootiered przypiętych lokalnie. Jednak ta konwersja nie powinien być częste wystąpienie.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Zagadnienia dotyczące konwersji woluminu warstwowego toolocal

Konwertowanie woluminu z warstwową toolocally przypięty niektórych przyczyn należą:

* Lokalnych gwarancji dotyczących wydajności i dostępności danych
* Eliminacja chmury opóźnienia i problemy z łącznością chmury.

Zazwyczaj są to mały istniejące woluminy często mają tooaccess. Wolumin przypięty lokalnie jest w pełni zaaprowizowanym podczas jego tworzenia. 

Jeśli zmieniasz wolumin przypięty lokalnie tooa wolumin warstwowy StorSimple sprawdza, czy mają wystarczającą ilość miejsca na urządzeniu, przed rozpoczęciem powitalne konwersji. Jeśli masz za mało miejsca, zostanie zwrócony błąd i hello operacja zostanie anulowana. 

> [!NOTE]
> Przed rozpoczęciem konwersji warstwowych toolocally przypięty, upewnij się, rozważ hello wymagania dotyczące miejsca na innych obciążeń. 

Konwersja z woluminu warstwowego tooa przypięty lokalnie może niekorzystnie wpłynąć na wydajność urządzenia. Ponadto hello następujące czynniki mogą zwiększyć hello czas toocomplete hello konwersji:

* Jest za mała przepustowość.
* Nie istnieje żadne obecnie wykonać kopii zapasowej.

toominimize hello efekty, których może mieć następujące czynniki:

* Zapoznaj się z przepustowości zasad i upewnij się, że dedykowany 40 MB/s przepustowości jest dostępny.
* Planowanie hello konwersji poza godzinami szczytu.
* Przed rozpoczęciem powitalne konwersji, należy utworzyć migawkę chmury.

Są konwersji wielu woluminów (obsługi różnych obciążeń), następnie użytkownik powinien priorytet konwersji woluminu hello tak, aby wyższy priorytet woluminy są konwertowane najpierw. Na przykład należy przekonwertować woluminy, które obsługi maszyn wirtualnych (VM) lub z obciążeniami SQL przed dokonaniem konwersji woluminy z obciążeniami udziału plików.

### <a name="local-tootiered-volume-conversion-considerations"></a>Zagadnienia dotyczące konwersji woluminu lokalnego tootiered

Możesz się, że toochange tooa woluminu przypiętego lokalnie do warstwy woluminu Jeśli potrzebujesz dodatkowego miejsca tooprovision inne woluminy. Podczas konwertowania tootiered wolumin przypięty lokalnie hello hello dostępnej pojemności na urządzeniu hello zwiększa się rozmiar hello hello wydane pojemności. Jeśli problemy z łącznością hello konwersji woluminu z toohello typ lokalne powitania warstwowej typu, hello woluminu lokalnego będzie mieć właściwości woluminu warstwowego do czasu ukończenia hello konwersji. Jest to spowodowane część danych może rozrzucone toohello chmury. Te dane rozlanej nadal toooccupy lokalne miejsce na urządzeniu hello, który nie jest możliwe, dopóki operacja hello jest uruchomiona ponownie oraz zostać zakończona.

> [!NOTE]
> Konwertowanie woluminu może zająć trochę czasu i nie można anulować konwersji po jego uruchomieniu. Podczas konwersji hello Hello wolumin pozostaje w trybie online i korzystać z kopii zapasowych, ale nie można rozwinąć lub Przywróć hello woluminu, podczas konwersji hello odbywa się.


#### <a name="toochange-hello-volume-type"></a>Typ woluminu hello toochange

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. Hello Tabelaryczny spis urządzeń hello, zaznacz urządzenie hello woluminu hello czy zamierzasz toomodify. Kliknij przycisk **Ustawienia > woluminów**.

    ![Przejdź do bloku tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Z hello tabelarycznej listę woluminów wybrać wolumin hello i kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke. Wybierz **zmodyfikować**.

    ![Modyfikowanie wybierz z menu kontekstowego](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Na powitania **zmodyfikować woluminu** bloku, Zmień typ woluminu hello, wybierając hello nowy typ z hello **typu** listy rozwijanej.
   
   * W przypadku zmiany typu hello zbyt**przypięty lokalnie**, StorSimple sprawdzi toosee, czy pojemność sieci jest wystarczająca.
   * W przypadku zmiany typu hello zbyt**warstwowego** i ten wolumin, które będą używane na potrzeby danych archiwalnych, wybierz hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru.
   * Jeśli konfigurujesz woluminu przypiętego lokalnie, jak warstwowej lub _odwrotnie_, hello zostanie wyświetlony następujący komunikat.
   
    ![Komunikat typu woluminu zmiany](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Kliknij przycisk **zapisać** toosave hello zmiany. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toostart hello w procesie konwersji. 

    ![Zapisz i Potwierdź](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Witaj portalu Azure wyświetli powiadomienie do utworzenia zadania hello, że będzie aktualizował hello woluminu. Polecenie hello powiadomień toomonitor hello stan zadania konwersji woluminu hello.

    ![Zadania dla konwersji woluminu](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Przełącz do trybu offline woluminu

Podczas planowania toomodify lub Usuń wolumin hello tootake woluminu w trybie offline może być konieczne. Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu. Należy wykonać hello wolumin do trybu offline na hoście hello i hello urządzenia.

#### <a name="tootake-a-volume-offline"></a>tootake woluminu w trybie offline

1. Upewnij się, że w woluminie hello nie jest używany przed przełączeniem do trybu offline.
2. Zająć hello woluminu w trybie offline na hoście hello pierwszy. Eliminuje to potencjalne ryzyko uszkodzeniem danych na woluminie hello. Określone kroki można znaleźć toohello instrukcje dotyczące systemu operacyjnego hosta.
3. Po hello host jest w trybie offline, należy wykonać hello woluminu na urządzeniu hello w trybie offline, wykonując następujące kroki hello:
   
    1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. Hello Tabelaryczny spis urządzeń hello, zaznacz urządzenie hello woluminu hello czy zamierzasz toomodify. Kliknij przycisk **Ustawienia > woluminów**.

        ![Przejdź do bloku tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. Z hello tabelarycznej listę woluminów wybrać wolumin hello i kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke. Wybierz **przełączyć do trybu offline** tootake hello woluminu, należy zmodyfikować w trybie offline.

        ![Wybierz, a następnie przełącz wolumin do trybu offline](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. W hello **przełączyć do trybu offline** bloku, przejrzyj wpływ hello przełączania w tryb offline hello woluminu i zaznacz odpowiednie pole wyboru hello. Kliknij przycisk **przełączyć do trybu offline**. 

    ![Przejrzyj wpływ przełączania w tryb offline woluminu](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Użytkownik jest powiadamiany o wolumin hello jest w trybie offline. Stan woluminu Hello aktualizuje również tooOffline.
      
4. Gdy wolumin jest w trybie offline, w przypadku wybrania hello wolumin i kliknij prawym przyciskiem myszy, **przejdź do trybu Online** opcja staje się dostępna w menu kontekstowym hello.

> [!NOTE]
> Witaj **Przełącz do trybu Offline** polecenie wysyła żądanie toohello urządzenia tootake hello woluminu w trybie offline. Jeśli hosty w dalszym ciągu używają hello woluminu, powoduje to zerwane połączenia, ale przełączania w tryb offline wolumin hello nie powiedzie się.

## <a name="delete-a-volume"></a>Usuwanie woluminu

> [!IMPORTANT]
> Wolumin można usunąć tylko wtedy, gdy jest w trybie offline.

Wykonaj następujące kroki toodelete woluminu hello.

#### <a name="toodelete-a-volume"></a>toodelete woluminu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. Hello Tabelaryczny spis urządzeń hello, zaznacz urządzenie hello woluminu hello czy zamierzasz toomodify. Kliknij przycisk **Ustawienia > woluminów**.

    ![Przejdź do bloku tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Sprawdź stan hello woluminu hello ma toodelete. Jeśli wolumin hello toodelete nie jest w trybie offline, przejść do trybu offline najpierw. Wykonaj kroki hello w [Przełącz do trybu offline wolumin](#take-a-volume-offline).
4. Po wolumin hello jest w trybie offline, wybierz wolumin hello, kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke, a następnie wybierz **usunąć**.

    ![Wybierz opcję usunięcia z menu kontekstowego](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. W hello **usunąć** bloku, przejrzyj i wybierz hello wyboru przed wpływ hello Usunięcie woluminu. Po usunięciu woluminu wszystkie dane hello, które znajduje się na woluminie hello zostaną utracone. 

    ![Zapisz i potwierdzenie zmian](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Po usunięciu woluminu hello hello tabelarycznej listę woluminów aktualizuje tooindicate hello usunięcia.

    ![Lista zaktualizowanych woluminów](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Jeśli usuniesz woluminu przypiętego lokalnie hello miejsca dla nowych woluminów mogły nie zostać zaktualizowane od razu. Witaj usługi Menedżer StorSimple urządzenia okresowo aktualizuje hello lokalne miejsce dostępne. Sugerujemy, zaczekaj kilka minut przed podjęciem próby toocreate hello nowego woluminu.
   >
   > Ponadto jeśli Usuń wolumin przypięty lokalnie, a następnie usuń innego lokalnie przypięty woluminu, natychmiast po hello woluminu usunięcia zadania są wykonywane sekwencyjnie. Witaj pierwszego zadania usuwania woluminu musi zakończyć się przed rozpoczęciem następnego zadania usuwania woluminu hello.

## <a name="monitor-a-volume"></a>Monitor woluminu

Monitorowanie woluminów umożliwia toocollect I/E-statystyki związane z woluminu. Monitorowanie jest domyślnie włączona dla hello najpierw 32 woluminów, które można utworzyć. Monitorowanie z dodatkowych woluminów jest domyślnie wyłączone. 

> [!NOTE]
> Monitorowanie woluminów sklonowany jest domyślnie wyłączone.


Wykonaj następujące kroki tooenable hello lub Wyłącz monitorowanie w woluminie.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable lub wyłączania monitorowania woluminu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. Hello Tabelaryczny spis urządzeń hello, zaznacz urządzenie hello woluminu hello czy zamierzasz toomodify. Kliknij przycisk **Ustawienia > woluminów**.
2. Z hello tabelarycznej listę woluminów wybrać wolumin hello i kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke. Wybierz **zmodyfikować**.
3. W hello **zmodyfikować woluminu** bloku dla **monitorowanie** wybierz **włączyć** lub **wyłączyć** tooenable lub Wyłącz monitorowanie.

    ![Wyłącz monitorowanie](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak**. Witaj portalu Azure wyświetla powiadomienie o aktualizacji hello woluminu, a następnie komunikat z potwierdzeniem po pomyślnej aktualizacji hello woluminu.

## <a name="next-steps"></a>Następne kroki

* Dowiedz się, jak za[sklonować woluminu StorSimple](storsimple-8000-clone-volume-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

