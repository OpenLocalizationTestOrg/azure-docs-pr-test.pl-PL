---
title: aaaManage woluminy StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak tooadd, modyfikowanie, monitorowania i usuwanie woluminów StorSimple i jak tootake ich w tryb offline, jeśli jest to konieczne."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Użycie woluminów toomanage usługi Menedżer StorSimple hello
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple i zarządzanie woluminami na powitania urządzenia StorSimple i urządzenia wirtualnego StorSimple.

Hello usługi Menedżer StorSimple, jest rozszerzenie hello klasycznego portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej. W dodanie toomanaging woluminów można użyć toocreate usługi Menedżer StorSimple hello i zarządzania usługami StorSimple i zarządzanie urządzeniami, wyświetlanie alertów i wyświetlić i zarządzanie zasadami tworzenia kopii zapasowej i hello katalogu kopii zapasowej.

> [!NOTE]
> Azure StorSimple można tworzyć tylko woluminy alokowane elastycznie. Nie można utworzyć w pełni lub częściowo inicjowanych woluminów w systemie Azure StorSimple.
> 
> Alokowanie elastyczne jest technologii wirtualizacji, w której dostępny magazyn pojawia się tooexceed zasobów fizycznych. Zamiast z wyprzedzeniem rezerwowania wystarczającej ilości miejsca, Azure StorSimple używa alokowania tooallocate inicjowania obsługi administracyjnej wystarczającego miejsca toomeet bieżące wymagania. Hello elastycznej rodzaj magazynu w chmurze ułatwia takie podejście, ponieważ Azure StorSimple można zwiększyć lub zmniejszyć chmury magazynu toomeet zmieniających się potrzeb.
> 
> 

## <a name="hello-volumes-page"></a>Witaj strony woluminów
Witaj **woluminów** strony można toomanage hello magazynu woluminy, które są udostępniane na urządzeniu Microsoft Azure StorSimple hello Twojej inicjatorów (serwerów). Wyświetla hello listę woluminów na urządzeniu StorSimple.

 ![Strony woluminów](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Wolumin składa się z szeregu atrybuty:

* **Nazwa** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello woluminu. Ta nazwa jest również używana do monitorowania raportów podczas filtrowania w określonym woluminie.
* **Stan** — może być w trybie online lub offline. Jeśli wolumin, jeśli jest w trybie offline, nie jest widoczne tooinitiators (serwery) dozwoloną dostępu toouse hello woluminu.
* **Pojemność** — określa sposób dużą hello jest jako postrzegane przez inicjatora hello (serwer). Pojemność określa hello łączna ilość danych, które mogą być przechowywane przez inicjatora hello (serwer). Woluminy alokowane są udostępniane, a następnie jest deduplikowany danych. Oznacza to, że urządzenie nie wstępnie przydzielić pojemności magazynu fizycznego, wewnętrznych lub w chmurze hello zgodnie z tooconfigured pojemność woluminu. pojemność woluminu Hello jest przydzielone i używane na żądanie.
* **Typ** — typ woluminu hello może być warstwowych lub archiwizacji (podtyp o warstwowa)
* **Dostęp** — określa hello inicjatorów (serwerów), które mają prawo dostępu toothis woluminu. Inicjatory, względem których nie są elementami członkowskimi rekord kontroli dostępu (ACR) skojarzony z woluminu hello nie będą widzieć hello woluminu.
* **Monitorowanie** — Określa, czy jest monitorowany wolumin. Wolumin ma monitorowania włączona domyślnie po jego utworzeniu. Monitorowanie będzie, jednak, można wyłączyć dla Klonowanie woluminów. tooenable monitorowania dla woluminu, wykonaj instrukcje hello w monitorze woluminu.

Witaj najbardziej typowych zadań związanych z woluminu są:

* Dodawanie woluminu
* Modyfikowanie woluminu
* Usuwanie woluminu
* Przełącz do trybu offline woluminu
* Monitor woluminu

## <a name="add-a-volume"></a>Dodawanie woluminu
Możesz [utworzony wolumin](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) podczas wdrażania rozwiązania StorSimple. Dodawanie woluminu jest podobnej procedury.

### <a name="tooadd-a-volume"></a>tooadd woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów, a następnie kliknij strzałkę hello w hello odpowiedni wiersz tooaccess hello woluminy skojarzone z kontenera hello.
3. Kliknij przycisk **Dodaj** u dołu hello hello strony. Uruchamia powitania w Kreatorze dodawania woluminu.
   
     ![Kreator dodawania woluminem ustawienia podstawowe](./media/storsimple-manage-volumes/AddVolume1.png)
4. W hello Dodaj kreatora woluminów, w obszarze **podstawowe ustawienia**, hello następujące:
   
   1. Wypełnij pole **Nazwa** dla woluminu.
   2. Określ hello **alokowana pojemność** dla woluminu w GB lub TB. pojemność Hello musi wynosić od 1 GB do 64 TB dla urządzenia fizycznego. Hello maksymalną pojemność, które można udostępnić dla woluminu na urządzeniu wirtualnym StorSimple wynosi 30 TB.
   3. Wybierz hello **typ użycia** dla woluminu. Jeśli używasz woluminu warstwowego na potrzeby danych archiwalnych, wybranie hello hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pola wyboru zmienia hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli nie zaznaczysz tej opcji, hello odpowiedni wolumin warstwowy użyje rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury. (Woluminy warstwowe były dawniej nazywane woluminami głównymi.)
   4. Kliknij ikonę strzałki hello ![ikonę strzałki](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **dodatkowe ustawienia** strony.
      
        ![Dodaj dodatkowe ustawienia kreatora woluminu](./media/storsimple-manage-volumes/AddVolume2.png)
5. W obszarze **dodatkowe ustawienia**, Dodaj nowy rekord kontroli dostępu (ACR):
   
   1. Wybierz rekord kontroli dostępu (ACR) z listy rozwijanej hello. Alternatywnie możesz dodać nowe ACR. ACRs określić hosty, które mogą uzyskiwać dostęp do woluminów przez hello zgodnego hosta IQN o znajdującego się w rekordzie hello.
   2. Zaleca się włączenie domyślnego tworzenia kopii zapasowej przez zaznaczenie hello **włączyć domyślnego tworzenia kopii zapasowej dla tego woluminu** pole wyboru.
   3. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-volumes/HCS_CheckIcon.png) wolumin hello toocreate z hello określonych ustawień.

Nowy wolumin jest teraz gotowy toouse.

## <a name="modify-a-volume"></a>Modyfikowanie woluminu
Zmodyfikuj woluminu, gdy będziesz potrzebować tooexpand lub zmień hello hosty, które uzyskują dostęp do woluminu hello.

> [!IMPORTANT]
> * Jeśli zmodyfikujesz hello rozmiar woluminu na urządzeniu hello hello rozmiar woluminu musi toobe zmienione na powitania hosta oraz.
> * powitania po stronie hosta opisane w tym miejscu są przeznaczone dla systemu Windows Server 2012 (2012 R2). Procedury dla systemu Linux lub z innymi systemami operacyjnymi hosta może się różnić. Podczas modyfikowania hello woluminu na hoście z innym systemem operacyjnym, można znaleźć instrukcje systemu operacyjnego hosta tooyour.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenera woluminów** kartę. Ta strona zawiera listę w formacie tabelarycznym wszystkie kontenery woluminów hello, które są skojarzone z urządzeniem hello.
2. Wybierz kontener woluminów i kliknij ją toodisplay hello listę wszystkich woluminów hello w kontenerze hello.
3. Na powitania **woluminów** , wybierz wolumin i kliknij przycisk **Modyfikuj**.
4. Hello zmodyfikuj Kreator woluminu w obszarze **podstawowe ustawienia**, można wykonać następujące hello:
   
   * Edytuj hello **nazwa** i **typu** Jeśli chcesz toomodify woluminu archiwizacji tooan wolumin warstwowy, wybierając hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru toochange hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB.
   * Zwiększ hello **alokowana pojemność**. Witaj **alokowana pojemność** zwiększyć. Nie można zmniejszyć wolumin, po jego utworzeniu.
     
     > [!NOTE]
     > Kontener woluminów hello nie można zmienić po przypisaniu tooa woluminu.
     > 
     > 
5. W obszarze **dodatkowe ustawienia**, można wykonać następujące hello:
   
   * Zmodyfikuj hello ACRs, pod warunkiem, że wolumin hello jest w trybie offline. Jeśli wolumin hello jest w trybie online, konieczne będzie tootake go najpierw w trybie offline. Zobacz kroki toohello w [woluminu Przełącz do trybu offline](#take-a-volume-offline) hello wcześniejsze toomodifying ACR.
   * Zmodyfikuj hello lista ACRs po wolumin hello jest w trybie offline.
     
     > [!NOTE]
     > Nie można zmienić hello **włączyć domyślnego tworzenia kopii zapasowej dla tego woluminu** opcji hello woluminu.
     > 
     > 
6. Zapisz zmiany, klikając ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Witaj klasycznego portalu Azure wyświetli komunikat aktualizowania woluminu. Go zostanie wyświetlony komunikat Powodzenie hello woluminu została zaktualizowana pomyślnie.
7. Jeśli rozszerzasz wolumin, wykonaj następujące kroki na komputerze hosta z systemem Windows hello:
   
   1. Przejdź za**Zarządzanie komputerem** ->**Zarządzanie dyskami**.
   2. Kliknij prawym przyciskiem myszy **Zarządzanie dyskami** i wybierz **Skanuj dyski**.
   3. Hello listy dysków, wybierz wolumin hello, które zostało zaktualizowane, kliknij prawym przyciskiem myszy, a następnie wybierz **Rozszerz wolumin**. zostanie uruchomiony Kreator rozszerzania woluminów Hello. Kliknij przycisk **Dalej**.
   4. Ukończ Kreatora hello, akceptując wartości domyślne hello. Po zakończeniu pracy Kreatora hello hello woluminu powinien być wyświetlony hello zwiększyć rozmiar.

![Zobacz film](./media/storsimple-manage-volumes/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób tooexpand wolumin, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Przełącz do trybu offline woluminu
Może być konieczne tootake woluminu w trybie offline podczas planowania toomodify albo go usunąć go. Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu. Konieczne będzie tootake hello woluminu w trybie offline na hoście hello, a także na urządzeniu hello. Wykonaj hello następujące kroki tootake woluminu w trybie offline.

### <a name="tootake-a-volume-offline"></a>tootake woluminu w trybie offline
1. Upewnij się, że w woluminie hello nie jest używany przed przełączeniem do trybu offline.
2. Zająć hello woluminu w trybie offline na hoście hello pierwszy. Eliminuje to potencjalne ryzyko uszkodzeniem danych na woluminie hello. Określone kroki można znaleźć toohello instrukcje dotyczące systemu operacyjnego hosta.
3. Po hello host jest w trybie offline, należy wykonać hello woluminu na urządzeniu hello w trybie offline, wykonując następujące kroki hello:
   
   1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** hello kartę **kontenery woluminów** karcie listy w formacie tabelarycznym wszystkie Witaj kontenery woluminów, które są skojarzone z urządzeniem hello.
   2. Wybierz kontener woluminów i kliknij ją toodisplay hello listę wszystkich woluminów hello w kontenerze hello.
   3. Wybierz wolumin, a następnie kliknij przycisk **przełączyć do trybu offline**.
   4. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. wolumin Hello powinno być teraz w trybie offline.
      
      Gdy wolumin jest w trybie offline, hello **przejdź do trybu Online** opcja staje się dostępna.

> [!NOTE]
> Witaj **Przełącz do trybu Offline** polecenie wysyła żądanie toohello urządzenia tootake hello woluminu w trybie offline. Jeśli hosty w dalszym ciągu używają hello woluminu, powoduje to zerwane połączenia, ale przełączania w tryb offline wolumin hello nie powiedzie się.
> 
> 

## <a name="delete-a-volume"></a>Usuwanie woluminu
> [!IMPORTANT]
> Wolumin można usunąć tylko wtedy, gdy jest w trybie offline.
> 
> 

Wykonaj następujące kroki toodelete woluminu hello.

### <a name="toodelete-a-volume"></a>toodelete woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów hello zawierający wolumin hello ma toodelete. Kliknij przycisk hello tooaccess kontenera woluminu hello **woluminów** strony.
3. Wszystkie woluminy hello skojarzone z tym kontenerem są wyświetlane w formacie tabelarycznym. Sprawdź stan hello woluminu hello ma toodelete. Jeśli wolumin hello ma toodelete nie jest w trybie offline, przełączyć go w trybie offline hello pierwszą, następujące kroki [Przełącz do trybu offline wolumin](#take-a-volume-offline).
4. Po wolumin hello jest w trybie offline, kliknij przycisk **usunąć** u dołu hello hello strony.
5. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. Witaj wolumin zostanie usunięte i hello **woluminów** strony zostaną wyświetlone listy hello zaktualizowane woluminy w kontenerze hello.

## <a name="monitor-a-volume"></a>Monitor woluminu
Monitorowanie woluminów umożliwia toocollect I/E-statystyki związane z woluminu. Monitorowanie jest domyślnie włączona dla hello najpierw 32 woluminów, które można utworzyć. Monitorowanie z dodatkowych woluminów jest domyślnie wyłączone. Monitorowanie woluminów sklonowany jest również domyślnie wyłączone.

Wykonaj następujące kroki tooenable hello lub Wyłącz monitorowanie w woluminie.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable lub wyłączania monitorowania woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów hello, w których hello znajduje się wolumin, a następnie kliknij hello tooaccess kontenera woluminu hello **woluminów** strony.
3. Wszystkie woluminy hello skojarzone z tym kontenerem są wyświetlane w hello tabelaryczny widok. Kliknij i zaznacz hello woluminu lub Klonowanie woluminów.
4. U dołu hello hello strony, kliknij przycisk **Modyfikuj**.
5. W Kreatorze modyfikowania woluminu hello w obszarze **podstawowe ustawienia**, wybierz pozycję **włączyć** lub **wyłączyć** z hello **monitorowanie** listy rozwijanej.
   
    ![Zmodyfikuj ustawienia podstawowe woluminu](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[sklonować woluminu StorSimple](storsimple-clone-volume.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

