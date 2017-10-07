---
title: aaaManage woluminy StorSimple (U2) | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak tooadd, modyfikowanie, monitorowania i usuwanie woluminów StorSimple i jak tootake ich w tryb offline, jeśli jest to konieczne."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Użyj hello woluminy toomanage usługi Menedżer StorSimple (aktualizacja Update 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple i zarządzanie woluminami na powitania urządzenia StorSimple i urządzenia wirtualnego StorSimple z aktualizacji 2.

Witaj usługi Menedżer StorSimple to rozszerzenie w klasycznym portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello. W dodanie toomanaging woluminów można użyć toocreate usługi Menedżer StorSimple hello i zarządzania usługami StorSimple i zarządzanie urządzeniami, wyświetlanie alertów i wyświetlić i zarządzanie zasadami tworzenia kopii zapasowej i hello katalogu kopii zapasowej.

## <a name="volume-types"></a>Typy woluminu
Woluminy StorSimple można:

* **Przypięty lokalnie woluminach**: dane w tych woluminów pozostaną na urządzeniu StorSimple lokalne powitania przez cały czas.
* **Woluminami warstwowymi**: dane w tych woluminów mogą zostaną przeniesione toohello chmury.

Archiwizacja wolumin jest typem woluminu warstwowego. Witaj większy rozmiar fragmentu deduplikacji używana w przypadku woluminów archiwizacji umożliwia hello urządzenia tootransfer większych segmenty toohello danych w chmurze. 

W razie potrzeby można zmienić typ woluminu hello z lokalnym tootiered lub toolocal warstwowego. Aby uzyskać więcej informacji, przejdź zbyt[zmienić typ woluminu hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Woluminów przypiętych lokalnie
Woluminów przypiętych lokalnie są w pełni woluminów, które nie warstwy toohello danych w chmurze, zapewniając lokalnego gwarantuje dla danych podstawowych, niezależnie od łączności chmury. Dane dotyczące woluminów przypiętych lokalnie nie jest deduplikowany i skompresowane; jednak migawek woluminów przypiętych lokalnie są deduplikowane. 

Woluminów przypiętych lokalnie są w pełni zaaprowizowanym; w związku z tym musi mieć wystarczającą ilość miejsca na urządzeniu, podczas ich tworzenia. Umożliwia obsługę woluminów przypiętych lokalnie tooa maksymalnym rozmiarze 8 TB na urządzeniu StorSimple 8100 hello i 20 TB na urządzeniu 8600 hello. StorSimple rezerwuje pozostałego miejsca lokalne powitania na urządzeniu hello migawek, metadane i przetwarzania danych. Można zwiększyć rozmiar hello woluminu przypiętego lokalnie toohello maksymalną dostępnego miejsca, ale nie można zmniejszyć rozmiar woluminu utworzonej hello.

Podczas tworzenia woluminu przypiętego lokalnie hello dostępnego miejsca na potrzeby tworzenia woluminów warstwowych zostanie zmniejszona. Witaj odwrotnej również ma wartość true: Jeśli masz istniejące woluminy warstwowe hello miejsca dla tworzenia lokalnie przypięty woluminów będzie niższa niż maksymalnych hello podanych powyżej. Aby uzyskać więcej informacji na woluminach lokalnych, zobacz toohello [— często zadawane pytania na woluminów przypiętych lokalnie](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Woluminy warstwowe
Woluminy warstwowe są woluminy alokowane elastycznie, w których hello często używanych danych pozostaje lokalne powitania urządzenia i mniej często używanych danych jest automatycznie do warstwy toohello chmury. Alokowanie elastyczne jest technologii wirtualizacji, w której dostępny magazyn pojawia się tooexceed zasobów fizycznych. Zamiast z wyprzedzeniem rezerwowania wystarczającej ilości miejsca, StorSimple używa alokowania tooallocate inicjowania obsługi administracyjnej wystarczającego miejsca toomeet bieżące wymagania. Hello elastycznej rodzaj magazynu w chmurze ułatwia takie podejście, ponieważ StorSimple można zwiększyć lub zmniejszyć chmury magazynu toomeet zmieniających się potrzeb.

Jeśli używasz woluminu warstwowego na potrzeby danych archiwalnych, wybranie hello hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pola wyboru zmienia hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli nie zaznaczysz tej opcji, hello odpowiedni wolumin warstwowy użyje rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury.

> [!NOTE]
> Archiwizacja woluminów utworzonych przy użyciu wersji 2 przed aktualizacją StorSimple będzie zaimportowany jako warstwowy z hello archiwizacji zaznaczone jest pole wyboru.
> 
> 

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

## <a name="hello-volumes-page"></a>Witaj strony woluminów
Witaj **woluminów** strony można toomanage hello magazynu woluminy, które są udostępniane na urządzeniu Microsoft Azure StorSimple hello Twojej inicjatorów (serwerów). Wyświetla hello listę woluminów na urządzeniu StorSimple.

 ![Strony woluminów](./media/storsimple-manage-volumes-u2/VolumePage.png)

Wolumin składa się z szeregu atrybuty:

* **Nazwa woluminu** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello woluminu. Ta nazwa jest również używana do monitorowania raportów podczas filtrowania w określonym woluminie.
* **Stan** — może być w trybie online lub offline. Jeśli wolumin jest w trybie offline, nie jest widoczne tooinitiators (serwery) dozwoloną dostępu toouse hello woluminu.
* **Pojemność** — określa hello łączna ilość danych, które mogą być przechowywane przez inicjatora hello (serwer). Przypięty lokalnie woluminy są w pełni zaaprowizowanym i znajdują się na urządzeniu StorSimple hello. Woluminy warstwowe są alokowane elastycznie i danych hello jest deduplikowany. Z woluminy alokowane elastycznie urządzenia nie wstępnie przydzielić pojemności magazynu fizycznego wewnętrznych lub w chmurze hello zgodnie z tooconfigured pojemność woluminu. pojemność woluminu Hello jest przydzielone i używane na żądanie.
* **Typ** — wskazuje, czy wolumin hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.
* **Kopia zapasowa** — wskazuje, czy domyślne zasady tworzenia kopii zapasowej istnieje hello woluminu.
* **Dostęp** — określa hello inicjatorów (serwerów), które mają prawo dostępu toothis woluminu. Inicjatory, względem których nie są elementami członkowskimi rekord kontroli dostępu (ACR) skojarzony z woluminu hello nie będą widzieć hello woluminu.
* **Monitorowanie** — Określa, czy jest monitorowany wolumin. Wolumin ma monitorowania włączona domyślnie po jego utworzeniu. Monitorowanie będzie, jednak, można wyłączyć dla Klonowanie woluminów. tooenable monitorowania dla woluminu, postępuj zgodnie z instrukcjami hello [monitorować woluminu](#monitor-a-volume). 

Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:

* Dodawanie woluminu 
* Modyfikowanie woluminu 
* Zmień typ woluminu hello
* Usuwanie woluminu 
* Przełącz do trybu offline woluminu 
* Monitor woluminu 

## <a name="add-a-volume"></a>Dodawanie woluminu
Możesz [utworzony wolumin](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) podczas wdrażania rozwiązania StorSimple. Dodawanie woluminu jest podobnej procedury.

#### <a name="tooadd-a-volume"></a>tooadd woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów z hello listy i kliknij ją dwukrotnie tooaccess hello skojarzone z hello kontenera woluminów.
3. Kliknij przycisk **Dodaj** u dołu hello hello strony. Uruchamia powitania w Kreatorze dodawania woluminu.
   
     ![Kreator dodawania woluminem ustawienia podstawowe](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. W hello Dodaj kreatora woluminów, w obszarze **podstawowe ustawienia**, hello następujące:
   
   1. Wypełnij pole **Nazwa** dla woluminu.
   2. Wybierz **typ użycia** z listy rozwijanej hello. W przypadku obciążeń, które wymagają toobe danych dostępne lokalnie na urządzeniu hello przez cały czas, wybrać **przypięty lokalnie**. Dla wszystkich innych typów danych, wybierz **warstwowego**. (**Warstwowego** jest domyślnym hello.)
   3. W przypadku wybrania **warstwowego** w kroku 2, można wybrać hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** tooconfigure pole wyboru archiwizacji woluminu.
   4. Wprowadź hello **alokowana pojemność** dla woluminu w GB lub TB. Zobacz [elastycznie pojemności](#provisioned-capacity) dla maksymalne rozmiary dla każdego typu urządzenia i woluminu. Przyjrzyj się hello **dostępnej pojemności** toodetermine ile miejsca do magazynowania rzeczywiście znajduje się na urządzeniu.
5. Kliknij ikonę strzałki hello![Ikona strzałki](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Jeśli konfigurujesz woluminu przypiętego lokalnie, zostanie wyświetlony po wiadomość hello.
   
    ![Komunikat typu woluminu zmiany](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Kliknij ikonę strzałki hello ![ikonę strzałki](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)ponownie toogo toohello **dodatkowe ustawienia** strony.
   
    ![Dodaj dodatkowe ustawienia kreatora woluminu](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. W obszarze **dodatkowe ustawienia**, Dodaj nowy rekord kontroli dostępu (ACR):
   
   1. Wybierz rekord kontroli dostępu (ACR) z listy rozwijanej hello. Alternatywnie możesz dodać nowe ACR. ACRs określić hosty, które mogą uzyskiwać dostęp do woluminów przez hello zgodnego hosta IQN o znajdującego się w rekordzie hello. Jeśli nie określisz ACR, zostanie wyświetlony następującą wiadomości powitania.
      
        ![Określ ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Zaleca się, że wybrano hello **włączyć domyślnego tworzenia kopii zapasowej dla tego woluminu** wyboru.
   3. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) wolumin hello toocreate z hello określonych ustawień.

Nowy wolumin jest teraz gotowy toouse.

> [!NOTE]
> Jeśli Tworzenie woluminu przypiętego lokalnie, a następnie utworzyć inną lokalnie przypięty woluminu natychmiast po zadania tworzenia woluminu hello są wykonywane sekwencyjnie. zadanie tworzenia woluminu pierwszy Hello musi zakończyć się przed rozpoczęciem hello następne zadanie tworzenia woluminu.
> 
> 

## <a name="modify-a-volume"></a>Modyfikowanie woluminu
Zmodyfikuj woluminu, gdy będziesz potrzebować tooexpand lub zmień hello hosty, które uzyskują dostęp do woluminu hello.

> [!IMPORTANT]
> * Jeśli zmodyfikujesz hello rozmiar woluminu na urządzeniu hello hello rozmiar woluminu musi toobe zmienione na powitania hosta oraz. 
> * powitania po stronie hosta opisane w tym miejscu są przeznaczone dla systemu Windows Server 2012 (2012 R2). Procedury dla systemu Linux lub z innymi systemami operacyjnymi hosta może się różnić. Podczas modyfikowania hello woluminu na hoście z innym systemem operacyjnym, można znaleźć instrukcje systemu operacyjnego hosta tooyour. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów z hello listy i kliknij ją dwukrotnie wolumin hello tooview skojarzony z hello kontenera.
3. Wybierz wolumin, a u dołu hello hello strony, kliknij przycisk **Modyfikuj**. zostanie uruchomiony Kreator woluminu Modyfikuj Hello.
4. Hello zmodyfikuj Kreator woluminu w obszarze **podstawowe ustawienia**, można wykonać następujące hello:
   
   * Edytuj hello **nazwa**.
   * Konwertuj hello **typ użycia** z tootiered przypiętych lokalnie lub warstwowych toolocally przypięty (zobacz [zmienić typ woluminu hello](#change-the-volume-type) Aby uzyskać więcej informacji).
   * Zwiększ hello **alokowana pojemność**. Witaj **alokowana pojemność** zwiększyć. Nie można zmniejszyć wolumin, po jego utworzeniu.
5. W obszarze **dodatkowe ustawienia**, można zmodyfikować hello ACR, pod warunkiem, że wolumin hello jest w trybie offline. Jeśli wolumin hello jest w trybie online, konieczne będzie tootake go najpierw w trybie offline. Zobacz kroki toohello w [woluminu Przełącz do trybu offline](#take-a-volume-offline) hello wcześniejsze toomodifying ACR.
   
   > [!NOTE]
   > Nie można zmienić hello **włączyć domyślnego tworzenia kopii zapasowej** opcji hello woluminu.
   > 
   > 
6. Zapisz zmiany, klikając ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Witaj klasycznego portalu Azure wyświetli komunikat aktualizowania woluminu. Go zostanie wyświetlony komunikat Powodzenie hello woluminu została zaktualizowana pomyślnie.
7. Jeśli rozszerzasz wolumin, wykonaj następujące kroki na komputerze hosta z systemem Windows hello:
   
   1. Przejdź za**Zarządzanie komputerem** ->**Zarządzanie dyskami**.
   2. Kliknij prawym przyciskiem myszy **Zarządzanie dyskami** i wybierz **Skanuj dyski**.
   3. Hello listy dysków, wybierz wolumin hello, które zostało zaktualizowane, kliknij prawym przyciskiem myszy, a następnie wybierz **Rozszerz wolumin**. zostanie uruchomiony Kreator rozszerzania woluminów Hello. Kliknij przycisk **Dalej**.
   4. Ukończ Kreatora hello, akceptując wartości domyślne hello. Po zakończeniu pracy Kreatora hello hello woluminu powinien być wyświetlony hello zwiększyć rozmiar.
      
      > [!NOTE]
      > Jeśli Rozszerz wolumin przypięty lokalnie, a następnie rozwiń węzeł przypięty lokalnie inny wolumin natychmiast po hello woluminu rozszerzenia zadania są wykonywane sekwencyjnie. Witaj pierwszego zadania rozszerzenia woluminu musi zakończyć się przed rozpoczęciem następnego zadania rozszerzania woluminów hello.
      > 
      > 

![Zobacz film](./media/storsimple-manage-volumes-u2/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób tooexpand wolumin, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Zmień typ woluminu hello
Można zmienić typ woluminu hello z warstwową toolocally przypięty lub tootiered przypiętych lokalnie. Jednak ta konwersja nie powinien być częste wystąpienie. Konwertowanie woluminu z warstwową toolocally przypięty niektórych przyczyn należą:

* Lokalnych gwarancji dotyczących wydajności i dostępności danych
* Eliminacja chmury opóźnienia i problemy z łącznością chmury.

Zazwyczaj są to mały istniejące woluminy często mają tooaccess. Wolumin przypięty lokalnie jest w pełni zaaprowizowanym podczas jego tworzenia. Jeśli zmieniasz wolumin przypięty lokalnie tooa wolumin warstwowy StorSimple sprawdza, czy mają wystarczającą ilość miejsca na urządzeniu, przed rozpoczęciem powitalne konwersji. Jeśli masz za mało miejsca, zostanie zwrócony błąd i hello operacja zostanie anulowana. 

> [!NOTE]
> Przed rozpoczęciem konwersji warstwowych toolocally przypięty, upewnij się, rozważ hello wymagania dotyczące miejsca na innych obciążeń. 
> 
> 

Możesz się, że toochange tooa woluminu przypiętego lokalnie do warstwy woluminu Jeśli potrzebujesz dodatkowego miejsca tooprovision inne woluminy. Podczas konwertowania tootiered wolumin przypięty lokalnie hello hello dostępnej pojemności na urządzeniu hello zwiększa się rozmiar hello hello wydane pojemności. Jeśli problemy z łącznością hello konwersji woluminu z toohello typ lokalne powitania warstwowej typu, hello woluminu lokalnego będzie mieć właściwości woluminu warstwowego ukończenie hello konwersji. Jest to spowodowane część danych może rozrzucone toohello chmury. Te dane rozlanej będzie toooccupy lokalne miejsce na urządzeniu hello, który nie jest możliwe, dopóki operacja hello jest uruchomiona ponownie oraz zostać zakończona.

> [!NOTE]
> Konwertowanie woluminu może zająć trochę czasu i nie można anulować konwersji po jego uruchomieniu. Podczas konwersji hello Hello wolumin pozostaje w trybie online i korzystać z kopii zapasowych, ale nie można rozwinąć lub Przywróć hello woluminu, podczas konwersji hello odbywa się.  
> 
> 

Konwersja z woluminu warstwowego tooa przypięty lokalnie może niekorzystnie wpłynąć na wydajność urządzenia. Ponadto hello następujące czynniki mogą zwiększyć hello czas toocomplete hello konwersji:

* Jest za mała przepustowość.
* Nie istnieje żadne obecnie wykonać kopii zapasowej.

toominimize hello efekty, których może mieć następujące czynniki:

* Zapoznaj się z przepustowości zasad i upewnij się, że dedykowany 40 MB/s przepustowości jest dostępny.
* Planowanie hello konwersji poza godzinami szczytu.
* Przed rozpoczęciem powitalne konwersji, należy utworzyć migawkę chmury.

Są konwersji wielu woluminów (obsługi różnych obciążeń), następnie użytkownik powinien priorytet konwersji woluminu hello tak, aby wyższy priorytet woluminy są konwertowane najpierw. Na przykład należy przekonwertować woluminy, które obsługi maszyn wirtualnych (VM) lub z obciążeniami SQL przed dokonaniem konwersji woluminy z obciążeniami udziału plików.

#### <a name="toochange-hello-volume-type"></a>Typ woluminu hello toochange
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów z hello listy i kliknij ją dwukrotnie wolumin hello tooview skojarzony z hello kontenera.
3. Wybierz wolumin, a u dołu hello hello strony, kliknij przycisk **Modyfikuj**. zostanie uruchomiony Kreator woluminu Modyfikuj Hello.
4. Na powitania **podstawowe ustawienia** Zmień typ użycia hello, wybierając hello nowy typ z hello **typ użycia** listy rozwijanej.
   
   * W przypadku zmiany typu hello zbyt**przypięty lokalnie**, StorSimple sprawdzi toosee, czy pojemność sieci jest wystarczająca.
   * W przypadku zmiany typu hello zbyt**warstwowego** i ten wolumin, które będą używane na potrzeby danych archiwalnych, wybierz hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru.
     
       ![Pole wyboru archiwum](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Kliknij ikonę strzałki hello ![ikonę strzałki](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **dodatkowe ustawienia** strony. Jeśli konfigurujesz woluminu przypiętego lokalnie hello zostanie wyświetlony następujący komunikat.
   
    ![Komunikat typu woluminu zmiany](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Kliknij ikonę strzałki hello ![ikona strzałki](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) ponownie toocontinue.
7. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) proces konwersji hello toostart. Witaj portalu Azure wyświetli komunikat aktualizowania woluminu. Go zostanie wyświetlony komunikat Powodzenie hello woluminu została zaktualizowana pomyślnie.

## <a name="take-a-volume-offline"></a>Przełącz do trybu offline woluminu
Może być konieczne tootake woluminu w trybie offline podczas planowania toomodify albo go usunąć go. Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu. Konieczne będzie tootake hello woluminu w trybie offline na hoście hello, a także na urządzeniu hello. 

#### <a name="tootake-a-volume-offline"></a>tootake woluminu w trybie offline
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

#### <a name="toodelete-a-volume"></a>toodelete woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów hello zawierający wolumin hello ma toodelete. Kliknij przycisk hello tooaccess kontenera woluminu hello **woluminów** strony.
3. Wszystkie woluminy hello skojarzone z tym kontenerem są wyświetlane w formacie tabelarycznym. Sprawdź stan hello woluminu hello ma toodelete. Jeśli wolumin hello ma toodelete nie jest w trybie offline, przełączyć go w trybie offline hello pierwszą, następujące kroki [Przełącz do trybu offline wolumin](#take-a-volume-offline).
4. Po wolumin hello jest w trybie offline, kliknij przycisk **usunąć** u dołu hello hello strony.
5. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. Witaj wolumin zostanie usunięte i hello **woluminów** strony zostaną wyświetlone listy hello zaktualizowane woluminy w kontenerze hello.
   
   > [!NOTE]
   > Jeśli usuniesz woluminu przypiętego lokalnie hello miejsca dla nowych woluminów mogły nie zostać zaktualizowane od razu. Witaj usługi Menedżer StorSimple okresowo aktualizuje hello lokalne miejsce dostępne. Sugerujemy, zaczekaj kilka minut przed podjęciem próby toocreate hello nowego woluminu.<br> Ponadto jeśli Usuń wolumin przypięty lokalnie, a następnie usuń innego lokalnie przypięty woluminu, natychmiast po hello woluminu usunięcia zadania są wykonywane sekwencyjnie. Witaj pierwszego zadania usuwania woluminu musi zakończyć się przed rozpoczęciem następnego zadania usuwania woluminu hello.
   > 
   > 

## <a name="monitor-a-volume"></a>Monitor woluminu
Monitorowanie woluminów umożliwia toocollect I/E-statystyki związane z woluminu. Monitorowanie jest domyślnie włączona dla hello najpierw 32 woluminów, które można utworzyć. Monitorowanie z dodatkowych woluminów jest domyślnie wyłączone. Monitorowanie woluminów sklonowany jest również domyślnie wyłączone.

Wykonaj następujące kroki tooenable hello lub Wyłącz monitorowanie w woluminie.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable lub wyłączania monitorowania woluminu
1. Na powitania **urządzeń** , wybierz hello urządzenie, kliknij go dwukrotnie, a następnie kliknij przycisk hello **kontenery woluminów** kartę.
2. Wybierz kontener woluminów hello, w których hello znajduje się wolumin, a następnie kliknij hello tooaccess kontenera woluminu hello **woluminów** strony.
3. Wszystkie woluminy hello skojarzone z tym kontenerem są wyświetlane w hello tabelaryczny widok. Kliknij i zaznacz hello woluminu lub Klonowanie woluminów.
4. U dołu hello hello strony, kliknij przycisk **Modyfikuj**.
5. W Kreatorze modyfikowania woluminu hello w obszarze **podstawowe ustawienia**, wybierz pozycję **włączyć** lub **wyłączyć** z hello **monitorowanie** listy rozwijanej.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[sklonować woluminu StorSimple](storsimple-clone-volume.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

