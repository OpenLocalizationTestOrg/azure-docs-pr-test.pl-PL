---
title: "aaaStorSimple wirtualnego tablicy awaryjnego odzyskiwania i urządzenia trybu failover | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat toofailover tablica wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Awaryjnego odzyskiwania i urządzenia w trybie failover tablica wirtualnego StorSimple za pośrednictwem portalu Azure

## <a name="overview"></a>Omówienie
W tym artykule opisano hello odzyskiwania po awarii dla programu Microsoft Azure StorSimple wirtualnej tablicy w tym hello szczegółowe kroki toofail za pośrednictwem tooanother wirtualnego tablicy. Trybu failover umożliwia toomove danych z *źródła* urządzenia w hello datacenter tooa *docelowej* urządzenia. Witaj urządzeniem docelowym może być znajduje się w hello tej samej lub innej lokalizacji geograficznej. Witaj urządzenia z trybu failover jest hello wszystkich danych z urządzenia. Podczas pracy w trybie failover hello danych w chmurze dla urządzenia źródłowego hello zmienia toothat własność hello urządzenia docelowego.

W tym artykule jest tooStorSimple dotyczy tylko tablice wirtualnego. toofail za pośrednictwem urządzenia serii 8000 Przejdź zbyt[urządzenia trybu failover i odzyskiwania po awarii urządzenia StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>Co to jest tryb failover odzyskiwania i urządzenia po awarii?

W przypadku odzyskiwanie po awarii urządzenie podstawowe hello przestanie działać. W tym scenariuszu można przenieść hello skojarzone z urządzeniem tooanother urządzenia nie powiodło się hello danych w chmurze. Urządzenie podstawowe hello można użyć jako hello *źródła* i określ inne urządzenie jako hello *docelowej*. Ten proces jest hello określonego tooas *pracy awaryjnej*. Podczas pracy w trybie failover hello wszystkie woluminy lub udziały hello z urządzenia źródłowego hello zmienić własności i zostały przeniesione toohello urządzenia docelowego. Bez filtrowania danych hello jest dozwolone.

DR ma formę przywracania pełne urządzenia przy użyciu cieplna hello mapy opartych na warstwy i śledzenia. Mapa cieplna jest zdefiniowany przez przypisanie toohello wartość cieplna dane na podstawie odczytu i zapisu wzorce. Ta cieplna mapy, a następnie warstw hello najniższy chmury toohello fragmentów danych cieplna najpierw przy zachowaniu fragmentów danych hello wysokiej cieplna (najczęściej używane) w warstwie lokalne powitania. Podczas odzyskiwania po awarii StorSimple używa toorestore Mapa cieplna hello i rehydrate hello danych z chmury hello. urządzenie Hello pobiera wszystkie hello woluminów/udziały w ostatnim ostatniej kopii zapasowej hello (jak określono wewnętrznie) i przeprowadza Przywracanie z kopii zapasowej. Tablica wirtualnego Hello organizuje hello cały proces odzyskiwania po awarii.

> [!IMPORTANT]
> Usuwanie urządzenia źródłowego Hello na końcu hello urządzenia trybu failover i dlatego powrotu po awarii nie jest obsługiwany.
> 
> 

Odzyskiwanie po awarii jest zorkiestrowana za pomocą funkcji trybu failover urządzenia hello i zainicjowano hello **urządzeń** bloku. Ten blok rejestruje wszystkie usługi Menedżera urządzeń StorSimple tooyour podłączonego urządzenia hello StorSimple. Dla każdego urządzenia można wyświetlić hello przyjaznej nazwy, stanu elastycznie i maksymalną pojemność, typ i modelu.

## <a name="prerequisites-for-device-failover"></a>Wymagania wstępne dotyczące urządzeń w pracy awaryjnej

### <a name="prerequisites"></a>Wymagania wstępne

Failover urządzenia upewnij się, że hello następujące wymagania wstępne są spełnione:

* urządzenia źródłowego Hello musi toobe w **dezaktywowane** stanu.
* Witaj urządzenia docelowego musi tooshow się jako **gotowe tooset się** w hello portalu Azure. Udostępnianie wirtualnych tablicy docelowej hello pojemności tego samego lub wyższego. Użyj tooconfigure interfejsu użytkownika sieci web lokalnego hello i pomyślnie zarejestrować hello docelowej tablicy wirtualnego.
  
  > [!IMPORTANT]
  > Nie należy podejmować hello tooconfigure zarejestrowanego urządzenia wirtualnego za pośrednictwem usługi hello. Konfiguracja urządzenia nie powinny być wykonywane za pośrednictwem usługi hello.
  > 
  > 
* urządzenie docelowe Hello nie może mieć takie same nazwy jako urządzenia źródłowego hello hello.
* Witaj źródłowe i docelowe urządzenie ma toobe hello tego samego typu. Możesz tylko w trybie Failover wirtualnego tablicy, skonfigurowany jako serwer plików tooanother serwera plików. Witaj dotyczy to także serwera iSCSI.
* Dla serwera plików odzyskiwania po awarii, firma Microsoft zaleca, Dołącz do toohello urządzenia docelowego hello tej samej domenie co hello źródła. Ta konfiguracja zapewnia, że uprawnienia udziału hello są automatycznie rozwiązane. Tylko hello trybu failover tooa urządzenie hello tej samej domenie.
* Hello dostępnych urządzeń do odzyskiwania po awarii są urządzenia, które mają hello takie same lub większą pojemność porównaniu toohello urządzenia źródłowego. Witaj urządzenia, które są połączone tooyour usługi, ale nie spełniają hello kryteria wystarczającą ilość miejsca nie są dostępne jako urządzenia docelowe.

### <a name="other-considerations"></a>Inne zagadnienia

* Dla planowanego trybu failover 
  
  * Zaleca się wykonanie wszystkich hello woluminy lub udziały na powitania urządzenia źródłowego w trybie offline.
  * Zalecamy tworzenie kopii zapasowej urządzenia hello, a następnie kontynuować utraty danych toominimize pracy awaryjnej hello. 
* W przypadku nieplanowanego trybu failover urządzenia hello używa hello najnowszych danych hello toorestore kopii zapasowej.

### <a name="device-failover-prechecks"></a>Urządzenie prechecks trybu failover

Przed hello DR rozpoczyna się od urządzenia hello przeprowadza prechecks. Te sprawdzenia pomocy, upewnij się, że nie występują błędy podczas odzyskiwania po awarii rozpocznie się. Witaj prechecks obejmują:

* Sprawdzanie poprawności hello konta magazynu.
* Sprawdzanie, czy tooAzure łączności chmury hello.
* Sprawdzanie miejsca na urządzeniu docelowym hello.
* Sprawdzanie, czy wolumin urządzenia iSCSI serwer źródłowy ma
  
  * Prawidłowe nazwy ACR.
  * Prawidłowe nazwy IQN (nie przekracza 220 znaków).
  * Nieprawidłowy protokół CHAP hasła (maksymalnie 12-16 znaków).

W przypadku awarii dowolnego hello poprzedzających prechecks, nie można kontynuować hello odzyskiwania po awarii. Rozwiąż te problemy, a następnie ponów próbę odzyskiwania po awarii.

Po pomyślnym zakończeniu hello odzyskiwania po awarii, własność hello hello danych w chmurze na powitania urządzenia źródłowego jest przeniesione toohello urządzenia docelowego. urządzenia źródłowego Hello następnie nie jest już dostępne w portalu hello. Dostęp tooall hello woluminów/udziałów na powitania urządzenia źródłowego jest zablokowany i urządzenie docelowe hello staje się aktywny.

> [!IMPORTANT]
> Chociaż hello urządzenie nie jest już dostępna, hello maszyny wirtualnej, która udostępniane w systemie hosta hello nadal korzysta z zasobów. Po zakończeniu hello DR pomyślnie, można usunąć tej maszyny wirtualnej z systemu hosta.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Tryb failover tooa wirtualnego tablicy

Zaleca się udostępniania, skonfigurować i zarejestrować innej tablicy wirtualnych StorSimple z usługą Menedżera urządzeń StorSimple, przed rozpoczęciem tej procedury.

> [!IMPORTANT]
> 
> * Nie można przełączyć się z StorSimple 8000 serii urządzenia tooa 1200 urządzenia wirtualnego.
> * Można przełączyć się z przetwarzania Standard FIPS (Federal Information) włączone urządzenia wirtualnego tooanother FIPS włączone urządzenie lub urządzenia z systemem innym niż FIPS tooa wdrożone w portalu dla instytucji rządowych hello.


Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia wirtualnego StorSimple hello.

1. Udostępniania i konfigurowania urządzenia docelowego, który spełnia hello [wymagania wstępne dotyczące urządzeń w pracy awaryjnej](#prerequisites). Zakończ konfigurację urządzenia hello za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i zarejestrowanie go za tooyour usługi Menedżer urządzeń StorSimple. W przypadku tworzenia serwera plików, przejdź toostep 1 z [skonfigurowany jako serwer plików](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Jeśli tworzenie serwera iSCSI, przejdź toostep 1 z [skonfigurowany jako serwer iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Przełączyć woluminy/udziałów w trybie offline na powitania hosta. tootake hello woluminów/udziałów w trybie offline, można znaleźć instrukcje specyficzne dla systemu operacyjnego toohello hello hosta. Jeśli nie już w trybie offline, należy tootake wszystkich hello woluminów/udziałów w tryb offline na urządzeniu hello następujący hello.
   
    1. Przejdź za**urządzeń** bloku i wybrać urządzenie.
   
    2. Przejdź za**Ustawienia > Zarządzaj > udziałów** (lub **Ustawienia > Zarządzaj > woluminów**). 
   
    3. Wybierz udział/wolumin, kliknij prawym przyciskiem myszy i wybierz **przełączyć do trybu offline**. 
   
    4. Po wyświetleniu monitu o potwierdzenie, sprawdź **rozumiem wpływ hello przełączania w tryb offline tego udziału.** 
   
    5. Kliknij przycisk **przełączyć do trybu offline**.

3. W usłudze Menedżer StorSimple urządzeniu Przejdź zbyt**zarządzania > urządzenia**. W hello **urządzeń** bloku, wybierz i kliknij przycisk urządzenia źródłowego.

4. W Twojej **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **Dezaktywuj**.

5. W hello **Dezaktywuj** bloku, zostanie wyświetlony monit o potwierdzenie. Dezaktywacja urządzenia jest *stałe* procesu, którego nie można cofnąć. Możesz są również przypomnienie tootake udziałów/woluminów w tryb offline na hoście hello. Wpisz tooconfirm nazwy urządzenia hello i kliknij przycisk **Dezaktywuj**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. Dezaktywacja Hello uruchamia. Po pomyślnym zakończeniu dezaktywacji hello, otrzymasz powiadomienie.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Na stronie urządzenia hello, stan urządzenia hello teraz zmieni się zbyt**dezaktywowane**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. W hello **urządzeń** bloku, a kliknij przycisk urządzenia źródłowego dezaktywowane hello w trybie failover. 
9. W hello **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **awaryjnie**. 
10. W hello **w tryb failover urządzeń** bloku hello następujące:
    
    1. Witaj źródła urządzenia pole jest wypełniane automatycznie. Należy pamiętać, rozmiar całkowitą danych hello hello urządzenia źródłowego. rozmiar danych Hello powinna być wcześniejsza niż hello dostępnej pojemności na urządzeniu docelowym hello. Przejrzyj szczegóły hello skojarzone z urządzenia źródłowego hello, takie jak nazwa urządzenia, łączna pojemność i nazwy hello hello akcji, które są przejścia w tryb failover.

    2. Z listy rozwijanej hello dostępne urządzenia, wybierz **urządzenie docelowe**. Hello tylko te urządzenia, które mają wystarczającą pojemność są wyświetlane na liście rozwijanej hello.

    3. Sprawdź, czy **rozumiem, że ta operacja zakończy się niepowodzeniem na urządzeniu docelowym toohello danych**. 

    4. Kliknij przycisk **awaryjnie**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Inicjuje zadania trybu failover i zostanie wyświetlone powiadomienie. Przejdź za**urządzenia > zadań** toomonitor hello w tryb failover.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. W hello **zadania** bloku, zobacz utworzone dla urządzenia źródłowego hello zadanie trybu failover. To zadanie przeprowadza hello prechecks odzyskiwania po awarii.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Po pomyślnym prechecks hello DR hello zadanie trybu failover zostanie zduplikować zadania przywracania dla każdego udziału/woluminu, która istnieje na urządzeniu źródła.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Po pracy awaryjnej hello toohello pełną, przejdź do pozycji **urządzeń** bloku.
    
    1. Wybierz i kliknij urządzenie StorSimple hello została użyta jako urządzenie docelowe hello hello procesu pracy awaryjnej.
    2. Przejdź za**Ustawienia > zarządzania > udziałów** (lub **woluminów** Jeśli serwer iSCSI). W hello **udziałów** bloku można wyświetlić wszystkie udziały hello (woluminy) ze starym urządzeniem hello.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Konieczne będzie zbyt[utworzyć DNS alias](https://support.microsoft.com/kb/168322) tak, aby wszystkie hello aplikacji, które próbujesz tooconnect można uzyskać przekierowanego toohello nowe urządzenie.

## <a name="errors-during-dr"></a>Błędy podczas odzyskiwania po awarii

**Awaria łączności chmurze podczas odzyskiwania po awarii**

Jeśli łączności chmury hello jest zakłócona po DR została uruchomiona przed zakończeniem przywracania urządzenia hello hello DR zakończy się niepowodzeniem. Zostanie wyświetlone powiadomienie failore. Witaj urządzenie docelowe do odzyskiwania po awarii jest oznaczony jako *korzystanie z niej.* Nie można użyć hello urządzenia docelowego dla przyszłych rejestracji urządzeń.

**Nie urządzeń docelowych zgodne**

Jeśli hello dostępnych urządzeń nie ma wystarczającej ilości miejsca, zobaczysz efektu toohello błąd, że nie ma żadnych urządzeń docelowych zgodne.

**Sprawdź błędy**

Jeśli jeden z hello prechecks nie zostanie spełnione, zostanie wyświetlony precheck błędów.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Odzyskiwanie po awarii ciągłości biznesowej (BCDR)

Scenariusz odzyskiwania (BCDR) po awarii ciągłości biznesowej występuje, gdy centrum danych Azure całego hello przestanie działać. Może to mieć wpływ na usługi Menedżer StorSimple urządzenia i hello skojarzone urządzenia StorSimple.

W przypadku urządzeń StorSimple, które zostały zarejestrowane bezpośrednio przed zamknięciem wystąpił awarii, te urządzenia StorSimple może wymagać toobe usunięte. Po awarii hello możesz ponownie utworzyć i skonfigurować te urządzenia.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o tym, jak za[administrowania tablica wirtualnego StorSimple przy użyciu lokalne powitania interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md).

