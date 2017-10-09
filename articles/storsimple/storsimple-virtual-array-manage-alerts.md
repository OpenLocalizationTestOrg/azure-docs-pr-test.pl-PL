---
title: "aaaView tablicy wirtualne Microsoft Azure StorSimple alerty i zarządzaj nimi | Dokumentacja firmy Microsoft"
description: "Opisuje warunki alertu tablicy wirtualnego StorSimple i ważność i jak hello toouse Menedżer StorSimple Usługa alertów toomanage."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Użyj Menedżera urządzeń StorSimple toomanage alertów dla hello tablicy wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Funkcja Alerty Hello hello usługi Menedżer StorSimple urządzenia umożliwia możesz tooreview i wyczyść alerty powiązane tooStorSimple tablice wirtualnego na podstawie w czasie rzeczywistym. Witaj alerty mogą być używane na powitania **Podsumowanie usługi** toocentrally bloku monitorować problemy dotyczące kondycji hello tablic wirtualnego StorSimple i hello ogólnego rozwiązania Microsoft Azure StorSimple.

W tym samouczku opisano, jak tooconfigure powiadomień o alertach, typowe warunki alertu, poziomy ważności alertów i jak alerty tooview i śledzenia. Ponadto zawiera alertu krótkimi opisami tabel, które umożliwiają tooquickly można zlokalizować określony alert i reagowania.

![Strona alertów](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Konfigurowanie ustawień alertów

Można wybrać, czy ma toobe powiadomienie e-mail hello warunków alertów dla każdego z macierzami wirtualne StorSimple. Ponadto można zidentyfikować innych odbiorców powiadomień o alertach, wprowadzając ich adresów e-mail w hello **adresatów wiadomości e-mail dodatkowych** okno, oddzielając je średnikami.

> [!NOTE]
> Możesz wprowadzić maksymalnie 20 adresy e-mail na tablicę wirtualnego.


Po włączeniu powiadomień e-mail dla tablicy wirtualnego członków listy powiadomień hello otrzymają wiadomość e-mail z każdym alert krytyczny wystąpieniu. będą wysyłane wiadomości powitania  *storsimple-alerts-noreply@mail.windowsazure.com*  i opisano hello warunku alertu. Kliknąć adresatów **Unsubscribe** tooremove się z listy powiadomień e-mail hello.

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable powiadomienia e-mail dla alertów

1. Przejdź tooyour Menedżera urządzeń StorSimple, usługi i w hello **zarządzania** , wybierz i kliknij pozycję **urządzeń**. Z listy hello wyświetlane urządzenia wybierz i kliknij urządzenie.
   
    ![Ustawienia alertów](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Spowoduje to otwarcie zapasowej hello **ustawienia** bloku. W hello **ustawienia urządzenia** zaznacz **ogólne**. Spowoduje to otwarcie zapasowej hello **ustawienia ogólne** bloku.
   
    ![Konfiguracja powiadomień alertów](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. W hello **ustawienia ogólne** bloku Przejdź zbyt**ustawienia alertu** sekcji i ustaw następujące hello:
   
   1. W hello **Włącz powiadomienia e-mail** pól, zaznacz **tak**.
   2. W hello **poczty E-mail Administratorzy usługi** pól, zaznacz **tak** Jeśli chcesz, aby administrator usługi hello toohave i wszyscy administratorzy wspólnej otrzymywać powiadomienia o alertach hello.
   3. W hello **adresatów wiadomości e-mail dodatkowych** wprowadź adresy e-mail wszystkich adresatów, którzy mają otrzymywać powiadomienia o alertach hello hello. Wprowadź nazwy w formacie hello  *someone@somewhere.com* . Użyj adresów e-mail hello tooseparate średnikami. Można skonfigurować maksymalnie 20 adresy e-mail na urządzeniu wirtualnym.
      
       ![Konfiguracja powiadomień alertów](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend testowe powiadomienie e-mail, kliknij przycisk **Wyślij testową wiadomość e-mail**. Hello usługi Menedżer StorSimple urządzenia będą wyświetlane komunikaty o stanie zgodnie z przesyła powiadomienie testowe hello.
      
       ![Alerty przetestować powiadomienia e-mail wysyłanego](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Jeśli hello test powiadomienia nie można wysłać wiadomości, usługa Menedżera urządzeń StorSimple hello wyświetli odpowiedni komunikat. Kliknij przycisk **OK**, zaczekaj kilka minut, a następnie ponownie spróbuj toosend komunikatu powiadomienia testu.
      > 
      > 
   5. U dołu hello hello strony, kliknij przycisk **zapisać** toosave konfiguracji. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.
      
      ![Alerty przetestować powiadomienia e-mail wysyłanego](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Typowe warunki alertu

Tablica wirtualnego StorSimple generuje alerty w odpowiedzi tooa różnych warunków. Oto Hello hello najbardziej typowych alertów warunki:

* **Problemy z łącznością** — te alerty występują w przypadku trudności podczas transferu danych. Problemy z komunikacją mogą wystąpić podczas transferu danych tooand z kontem magazynu platformy Azure hello lub termin toolack łączność między hello urządzenia wirtualne i usługi Menedżer StorSimple urządzenia hello. Problemy z komunikacją przedstawiono niektóre toofix najtrudniejsze hello, ponieważ istnieje wiele punktów awarii. Należy zawsze najpierw sprawdź, czy połączenie sieciowe oraz dostęp do Internetu są dostępne przed kontynuowaniem na toomore zaawansowanego rozwiązywania problemów. Informacje o portach i ustawienia zapory, przejdź zbyt[wymagania systemowe tablicy wirtualnego StorSimple](storsimple-ova-system-requirements.md). Aby uzyskać pomoc dotyczącą rozwiązywania problemów, przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemy z wydajnością** — te alerty są powodowane przeprowadzania systemu nie jest optymalnie, np. gdy jest mocno obciążony.

Ponadto można napotkać, toosecurity powiązanych alertów, aktualizacji lub niepowodzenia zadań.

## <a name="alert-severity-levels"></a>Poziomy ważności alertów

Alerty mają różne poziomy ważności, w zależności od wpływu hello, który hello alertu sytuacji będzie mieć i hello potrzebę alert toohello odpowiedzi. dostępne są następujące poziomy ważności Hello:

* **Krytyczne** — alert jest w stanie tooa odpowiedzi, który ma wpływ na powitania pomyślnego działania systemu. Akcja jest wymagana tooensure usługi StorSimple hello nie zostało przerwane.
* **Ostrzeżenie** — ten stan może stać się krytyczny, jeśli nie uda się rozwiązać. Należy zbadać sytuację hello i wykonać wszystkie czynności tooclear hello problem.
* **Informacje o** — tego alertu zawiera informacje, które mogą być przydatne w śledzenia i zarządzanie systemem.

## <a name="view-and-track-alerts"></a>Wyświetlanie i śledzenie alertów

bloku podsumowania usługi Menedżer StorSimple urządzenia Hello zapewnia szybkiego dostępu hello liczby alertów dla urządzenia wirtualnego uporządkowane według poziomu ważności.

![Pulpit nawigacyjny alertów](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Kliknij przycisk hello tooopen poziomu ważności hello **alerty** bloku. Witaj wyniki zawierają tylko alerty hello spełniające ten poziom ważności.

![Raport o alertach zakres tooalert typu](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Kliknij alert na powitania listy tooget dodatkowych szczegółów alertu hello, w tym hello czasu, gdy został zgłoszony hello alert, hello liczbę wystąpień alertu hello na urządzeniu hello i hello Zalecana akcja tooresolve hello alertu.

![Lista alertów i szczegóły](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Jeśli potrzebujesz toosend hello informacji tooMicrosoft pomocy technicznej można skopiować pliku tekstowego tooa szczegóły alertu hello. Po po Zalecenie hello i rozpoznać hello warunku alertu lokalnymi, należy wyczyścić hello alert z listy hello. Wybierz z listy hello hello alert i kliknij przycisk **wyczyść**. tooclear wiele alertów, zaznacz każdy alert, kliknij przycisk wszystkich kolumn z wyjątkiem hello **Alert** kolumny, a następnie kliknij przycisk **wyczyść** po wybraniu wszystkich hello toobe alerty wyczyszczone.

Po kliknięciu **wyczyść**, konieczne będzie hello możliwości tooprovide komentarze dotyczące alertu hello i kroki hello przez trwała tooresolve hello problem. 

![komentarze alertu](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Niektóre zdarzenia zostaną usunięte przez hello system, jeśli inny zdarzenie zostanie wyzwolone przy użyciu nowych informacji. 

## <a name="sort-and-review-alerts"></a>Sortowanie i przegląd alertów

Witaj **alerty** bloku można wyświetlać alerty too250. Po przekroczeniu tej liczby alertów, nie wszystkie alerty będą wyświetlane w hello widok domyślny. Możesz połączyć ze sobą hello toocustomize pola, które alerty są wyświetlane następujące:

* **Stan** — można wyświetlić **Active** lub **wyczyszczone** alertów. Aktywne alerty nadal są inicjowane w systemie, gdy alerty wyczyszczone zostały albo ręcznie usunięte przez administratora lub programistycznie wyczyścić, ponieważ hello system zaktualizowany stan alertu hello nowymi informacjami.
* **Ważność** — można wyświetlać alerty wszystkie poziomy ważności (krytyczny, ostrzeżenie, informacje o) lub tylko niektórych ważność, takich jak alerty tylko krytyczne.
* **Źródło** — wyświetlania alertów ze wszystkich źródeł lub ograniczyć hello toothose alerty, które pochodzą z usługi hello lub jednego lub wszystkich hello urządzenia wirtualnego.
* **Zakres czasu** — określając hello **z** i **do** dat i sygnatury czasowe, można zapoznać się z alertami, podczas hello okres czasu, który chcesz.

## <a name="alerts-quick-reference"></a>Krótki przewodnik alertów

następujące tabele Hello listę niektórych hello StorSimple alerty, które można napotkać, a także dodatkowe informacje i zalecenia w przypadku, gdy dostępna. Alerty tablicy wirtualnego StorSimple dzielą się na powitania następujące kategorie:

* [Alerty łączności chmury](#cloud-connectivity-alerts)
* [Alerty konfiguracji](#configuration-alerts)
* [Alerty błędów zadania](#job-failure-alerts)
* [Alerty wydajności](#performance-alerts)
* [Alerty zabezpieczeń](#security-alerts)
* [Aktualizowanie alertów](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Alerty łączności chmury

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Urządzenie  *<device name>*  jest niepodłączony toohello chmury. |Witaj o nazwie urządzenia nie można połączyć toohello chmury. |Nie można połączyć toohello chmury. Może to być spowodowane tooone hello następujące czynności:<ul><li>Może to być problem z ustawieniami sieci hello na urządzeniu.</li><li>Może to być problem z poświadczeniami konta magazynu hello.</li></ul>Aby uzyskać więcej informacji na temat rozwiązywania problemów z łącznością, przejdź toohello [lokalnego interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md) hello urządzenia. |

### <a name="configuration-alerts"></a>Alerty konfiguracji

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Konfiguracja urządzenia wirtualnego lokalnymi nieobsługiwany. |Niska wydajność. |Bieżąca konfiguracja Hello może spowodować obniżenie wydajności. Upewnij się, że serwer spełnia wymagania dotyczące minimalnej konfiguracji hello. Aby uzyskać więcej informacji, przejdź zbyt[wymagania dotyczące urządzenia StorSimple wirtualnego tablicy](storsimple-ova-system-requirements.md). |
| Kończy się miejsce na dysku elastycznie <*nazwa urządzenia*>. |Ostrzeżenie miejsca na dysku. |Masz mało miejsca na dysku elastycznie. toofree miejsca, należy wziąć pod uwagę przeniesienie obciążeń tooanother woluminu lub udziału lub usunięcie danych. |

### <a name="job-failure-alerts"></a>Alerty błędów zadania

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Tworzenie kopii zapasowych <*nazwa urządzenia*> nie można ukończyć. |Niepowodzenie zadania tworzenia kopii zapasowej. |Nie można utworzyć kopii zapasowej. Należy wziąć pod uwagę jedną z następujących hello:<ul><li>Problemy z łącznością może uniemożliwiać hello operacji tworzenia kopii zapasowej z pomyślne wykonanie. Upewnij się, że nie ma problemów z połączeniem. Aby uzyskać więcej informacji na temat rozwiązywania problemów z łącznością, przejdź toohello [lokalnego interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md) dla urządzenia wirtualnego.</li><li>Osiągnięto limit dostępny magazyn hello. toofree miejsca, należy rozważyć usunięcie wszelkich kopii zapasowych, które nie są już potrzebne.</li></ul> Rozwiązywanie problemów dotyczących hello, wyczyść hello alert, a następnie ponów operację hello. |
| Klon <*nazwa urządzenia*> nie można ukończyć. |Klonowanie niepowodzenie zadania. |Nie można utworzyć klonu. Należy wziąć pod uwagę jedną z następujących hello:<ul><li>Z listy kopii zapasowych jest nieprawidłowy. Odśwież tooverify listy hello jest nadal ważny.</li><li>Problemy z łącznością może uniemożliwiać pomyślne wykonanie operacji klonowania hello. Upewnij się, że nie ma problemów z połączeniem.</li><li>Osiągnięto limit dostępny magazyn hello. toofree miejsca, należy rozważyć usunięcie wszelkich kopii zapasowych, które nie są już potrzebne.</li></ul>Rozwiązywanie problemów dotyczących hello, wyczyść hello alert, a następnie ponów operację hello. |

### <a name="performance-alerts"></a>Alerty wydajności

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Występują nieoczekiwane opóźnienia transferu danych. |Transfer danych powolne. |Ograniczenia przepustowości błędy występują w przypadku przekroczenia wartości docelowe skalowalności hello usługi magazynu. Usługa Magazyn Hello jest to tooensure nie jednego klienta lub dzierżawcy, można użyć usługi hello na powitania koszt innych osób. Aby uzyskać więcej informacji na temat usuwania konta magazynu Azure, przejdź zbyt[monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Możesz zaczyna brakować miejsca na dysku lokalnym rezerwacji <*nazwa urządzenia*>. |Długi czas odpowiedzi. |10% hello całkowity rozmiar udostępnione dla <*nazwa urządzenia*> jest zarezerwowana na powitania urządzenie lokalne i są teraz zaczyna brakować hello Zarezerwowana przestrzeń. Obciążenie Hello <*nazwa urządzenia*> generuje wyższa szybkość zmian lub może mieć ostatnio zmigrowany dużej ilości danych. To może spowodować zmniejszenie wydajności. Należy wziąć pod uwagę jedną z hello następujące akcje tooresolve to:<ul><li>Zwiększ hello chmury przepustowości toothis urządzenia.</li><li>Zmniejsz lub przenoszenia obciążeń tooanother woluminu lub udziału.</li></ul> |

### <a name="security-alerts"></a>Alerty zabezpieczeń

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Hasło dla <*nazwa urządzenia*> wygaśnie za <*numer*> dni. |Ostrzeżenie o hasło. |Twoje hasło wygaśnie w < numer < dni. Rozważ zmianę hasła. Aby uzyskać więcej informacji, przejdź zbyt[hasło administratora urządzenia StorSimple wirtualnego tablicy hello zmiany](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Aktualizowanie alertów

| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Nowe aktualizacje są dostępne dla danego urządzenia. |Dostępne są aktualizacje toohello tablicy wirtualne StorSimple. |Nowe aktualizacje można zainstalować z hello **konserwacji** strony. |
| Nie można skanować pod kątem nowych aktualizacji na <*nazwa urządzenia*>. |Zaktualizuj awarii. |Wystąpił błąd podczas instalowania nowych aktualizacji. Możesz ręcznie zainstalować aktualizacje hello. Jeśli hello problem będzie się powtarzać, skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej o hello tablicy wirtualnego StorSimple](storsimple-ova-overview.md).

