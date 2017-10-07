---
title: "aaaView StorSimple alerty i zarządzaj nimi | Dokumentacja firmy Microsoft"
description: "Opisuje StorSimple warunków alertów i ważność, jak powiadomieniami o alertach tooconfigure i jak hello toouse Menedżer StorSimple Usługa alertów toomanage."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bee49253-9ac7-4131-95f6-6bf0e72b8438
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: anbacker
ms.openlocfilehash: d322c88b565606538a3acb61ff939ec1fbe2f3cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-alerts"></a>Użyj tooview usługi Menedżer StorSimple hello alerty i zarządzaj nimi StorSimple
## <a name="overview"></a>Omówienie
Witaj **alerty** kartę w hello usługi Menedżer StorSimple umożliwia możesz tooreview i wyczyść alerty związane z urządzenia StorSimple na podstawie w czasie rzeczywistym. Na tej karcie można centralnie monitorować problemy dotyczące kondycji hello urządzenia StorSimple i hello ogólnego rozwiązania Microsoft Azure StorSimple.

W tym samouczku opisano typowe warunki alertu, poziomy ważności alertów i jak tooconfigure alertów powiadomienia. Ponadto zawiera alertu krótkimi opisami tabel, które umożliwiają tooquickly można zlokalizować określony alert i reagowania.

![Strona alertów](./media/storsimple-manage-alerts/HCS_AlertsPage.png)

## <a name="common-alert-conditions"></a>Typowe warunki alertu
Urządzenia StorSimple generuje alerty w odpowiedzi tooa różnych warunków. Oto Hello hello najbardziej typowych alertów warunki:

* **Problemy ze sprzętem** — te alerty informujące o kondycji hello sprzętu. Umożliwiają one Cię o tym, czy aktualizacje oprogramowania są wymagane, jeśli interfejs sieciowy ma problemy w przypadku problemu z jednym z dysków z danymi.
* **Problemy z łącznością** — te alerty występują w przypadku trudności podczas transferu danych. Problemy z komunikacją mogą wystąpić podczas transferu danych tooand z kontem magazynu platformy Azure hello lub termin toolack łączność między urządzeniami hello i hello usługi Menedżer StorSimple. Problemy z komunikacją przedstawiono niektóre toofix najtrudniejsze hello, ponieważ istnieje wiele punktów awarii. Należy zawsze najpierw sprawdź, czy połączenie sieciowe oraz dostęp do Internetu są dostępne przed kontynuowaniem na toomore zaawansowanego rozwiązywania problemów. Aby uzyskać pomoc dotyczącą rozwiązywania problemów, przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Test-Connection hello](storsimple-troubleshoot-deployment.md).
* **Problemy z wydajnością** — te alerty są powodowane przeprowadzania systemu nie jest optymalnie, np. gdy jest mocno obciążony.

Ponadto można napotkać, toosecurity powiązanych alertów, aktualizacji lub niepowodzenia zadań.

## <a name="alert-severity-levels"></a>Poziomy ważności alertów
Alerty mają różne poziomy ważności, w zależności od wpływu hello, który hello alertu sytuacji będzie mieć i hello potrzebę alert toohello odpowiedzi. dostępne są następujące poziomy ważności Hello:

* **Krytyczne** — alert jest w stanie tooa odpowiedzi, który ma wpływ na powitania pomyślnego działania systemu. Akcja jest wymagana tooensure usługi StorSimple hello nie zostało przerwane.
* **Ostrzeżenie** — ten stan może stać się krytyczny, jeśli nie uda się rozwiązać. Należy zbadać sytuację hello i wykonać wszystkie czynności tooclear hello problem.
* **Informacje o** — tego alertu zawiera informacje, które mogą być przydatne w śledzenia i zarządzanie systemem.

## <a name="configure-alert-settings"></a>Konfigurowanie ustawień alertów
Można wybrać, czy ma toobe powiadomienie e-mail alertów warunki dla każdego urządzenia StorSimple. Ponadto można zidentyfikować innych odbiorców powiadomień o alertach, wprowadzając ich adresów e-mail w hello **innych adresatów wiadomości e-mail** okno, oddzielając je średnikami.

> [!NOTE]
> Możesz wprowadzić maksymalnie 20 adresy e-mail na urządzeniu.
> 
> 

Po włączeniu powiadomień e-mail dla urządzeń członków listy powiadomień hello otrzymają wiadomość e-mail z każdym alert krytyczny wystąpieniu. będą wysyłane wiadomości powitania  *storsimple-alerts-noreply@mail.windowsazure.com*  i opisano hello warunku alertu. Kliknąć adresatów **Unsubscribe** tooremove się z listy powiadomień e-mail hello.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>tooenable powiadomienia e-mail o alertach dla urządzenia
1. Przejdź za**urządzeń** > **Konfiguruj** hello urządzenia.
2. W obszarze **ustawienia alertu**, ustaw następujące hello:
   
   1. W hello **wysyłania powiadomień e-mail** pól, zaznacz **tak**.
   2. W hello **poczty E-mail Administratorzy usługi** pól, zaznacz **tak** Jeśli chcesz, aby administrator usługi hello toohave i wszyscy administratorzy wspólnej otrzymywać powiadomienia o alertach hello.
   3. W hello **innych adresatów wiadomości e-mail** wprowadź adresy e-mail wszystkich adresatów, którzy mają otrzymywać powiadomienia o alertach hello hello. Wprowadź nazwy w formacie hello  *someone@somewhere.com* . Użyj adresów e-mail hello tooseparate średnikami. Można skonfigurować maksymalnie 20 adresy e-mail na urządzeniu. 
      
       ![Konfiguracja powiadomień alertów](./media/storsimple-manage-alerts/AlertNotify.png)
3. toosend testowe powiadomienie e-mail, kliknij ikonę strzałki hello obok zbyt**Wyślij testową wiadomość e-mail**. Hello usługi Menedżer StorSimple zostaną wyświetlone komunikaty o stanie zgodnie z przesyła powiadomienie testowe hello. 
4. Gdy hello zostanie wyświetlony następujący komunikat, kliknij przycisk **OK**. 
   
    ![Alerty przetestować powiadomienia e-mail wysyłanego](./media/storsimple-manage-alerts/HCS_AlertNotificationConfig3.png)
   
   > [!NOTE]
   > W przypadku hello powiadomienia nie można wysłać wiadomości testowej, hello usługi Menedżer StorSimple wyświetli odpowiedni komunikat. Kliknij przycisk **OK**, zaczekaj kilka minut, a następnie ponownie spróbuj toosend komunikatu powiadomienia testu. 
   > 
   > 

## <a name="view-and-track-alerts"></a>Wyświetlanie i śledzenie alertów
pulpit nawigacyjny usługi Menedżer StorSimple Hello zapewnia szybkiego dostępu na powitania liczbę alertów na urządzeniach, aby uporządkowane według poziomu ważności.

![Pulpit nawigacyjny alertów](./media/storsimple-manage-alerts/admin_alerts_dashboard.png)

Kliknięcie poziom ważności hello otwiera hello **alerty** kartę hello wyniki zawierają tylko alerty hello spełniające ten poziom ważności.

![Raport o alertach zakres tooalert typu](./media/storsimple-manage-alerts/admin_alerts_scoped.png)

Kliknięcie alertu na liście hello zapewnia dodatkowe szczegóły alertu hello, takie jak hello ostatni czas hello alert został zgłoszony, hello liczbę wystąpień alertu hello na powitania urządzenia i hello Zalecana akcja tooresolve hello alertu. Jeśli jest to alert sprzętu, również zidentyfikuje hello składników sprzętowych.

![Przykład alertu sprzętu](./media/storsimple-manage-alerts/admin_alerts_hardware.png)

Jeśli potrzebujesz toosend hello informacji tooMicrosoft pomocy technicznej można skopiować pliku tekstowego tooa szczegóły alertu hello. Po po Zalecenie hello i rozpoznać hello warunku alertu lokalnymi, należy wyczyścić hello alert z urządzenia hello wybierając hello alert hello **alerty** kartę i klikając **wyczyść**. tooclear wiele alertów, zaznacz każdy alert, kliknij przycisk wszystkich kolumn z wyjątkiem hello **Alert** kolumny, a następnie kliknij przycisk **wyczyść** po wybraniu wszystkich hello toobe alerty wyczyszczone. Należy zwrócić uwagę na to, czy niektóre alerty są automatycznie czyszczone po rozwiązaniu problemu hello, lub gdy hello system aktualizuje hello alert o nowe informacje.

Po kliknięciu **wyczyść**, konieczne będzie hello możliwości tooprovide komentarze dotyczące alertu hello i kroki hello przez trwała tooresolve hello problem. Niektóre zdarzenia zostaną usunięte przez hello system, jeśli inny zdarzenie zostanie wyzwolone przy użyciu nowych informacji. W takim przypadku zostanie wyświetlone następujące wiadomość hello.

![Komunikat alertu czyszczenia.](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Sortowanie i przegląd alertów
Może być bardziej efektywne raporty toorun alertów dzięki czemu można przejrzeć, a następnie je wyczyść w grupach. Ponadto hello **alerty** kartę można wyświetlać alerty too250. Po przekroczeniu tej liczby alertów, nie wszystkie alerty będą wyświetlane w hello widok domyślny. Możesz połączyć ze sobą hello toocustomize pola, które alerty są wyświetlane następujące:

* **Stan** — można wyświetlić **Active** lub **wyczyszczone** alertów. Aktywne alerty nadal są inicjowane w systemie, gdy alerty wyczyszczone zostały albo ręcznie usunięte przez administratora lub programistycznie wyczyścić, ponieważ hello system zaktualizowany stan alertu hello nowymi informacjami.
* **Ważność** — można wyświetlać alerty wszystkie poziomy ważności (krytyczny, ostrzeżenie, informacje o) lub tylko niektórych ważność, takich jak alerty tylko krytyczne.
* **Źródło** — wyświetlania alertów ze wszystkich źródeł lub ograniczyć hello toothose alerty, które pochodzą z usługi hello lub jedno lub wszystkie hello urządzeń.
* **Zakres czasu** — określając hello **z** i **do** dat i sygnatury czasowe, można zapoznać się z alertami, podczas hello okres czasu, który chcesz.

## <a name="alerts-quick-reference"></a>Krótki przewodnik alertów
następujące tabele Hello listę niektórych hello Microsoft Azure StorSimple alerty, które można napotkać, a także dodatkowe informacje i zalecenia w przypadku, gdy dostępna. Alerty urządzenia StorSimple dzielą się na powitania następujące kategorie:

* [Alerty łączności chmury](#cloud-connectivity-alerts)
* [Alerty klastra](#cluster-alerts)
* [Alerty odzyskiwania po awarii](#disaster-recovery-alerts)
* [Alerty sprzętu](#hardware-alerts)
* [Alerty błędów zadania](#job-failure-alerts)
* [Alerty woluminu przypiętego lokalnie](#locally-pinned-volume-alerts)
* [Alerty sieci](#networking-alerts)
* [Alerty wydajności](#performance-alerts)
* [Alerty zabezpieczeń](#security-alerts)
* [Obsługa alertów pakietu](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Alerty łączności chmury
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Łączność zbyt <*nazwa poświadczeń w chmurze*> nie powiodło się. |Nie można połączyć toohello konta magazynu. |Wygląda na to, może być problem z łącznością z urządzeniem. Uruchom hello `Test-HcsmConnection` polecenia cmdlet hello interfejsu programu Windows PowerShell dla StorSimple na tooidentify Twojego urządzenia i rozwiązać problem hello. Jeśli ustawienia hello są poprawne, hello problem może być przy użyciu poświadczeń hello hello konta magazynu, dla którego hello alertu. W takim przypadku należy użyć hello `Test-HcsStorageAccountCredential` toodetermine polecenia cmdlet, jeśli występują problemy, które można rozwiązać.<ul><li>Sprawdź ustawienia sieciowe.</li><li>Sprawdź poświadczenia konta magazynu.</li></ul> |
| Nie Otrzymaliśmy pulsu z Twojego urządzenia pod kątem hello ostatnio <*numer*> minut. |Nie można połączyć toodevice. |Prawdopodobnie istnieje problem z łącznością z urządzeniem. Użyj hello `Test-HcsmConnection` polecenia cmdlet hello interfejsu programu Windows PowerShell dla StorSimple na tooidentify Twojego urządzenia i rozwiązać problem hello lub skontaktuj się z administratorem sieci. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>Zachowanie StorSimple, gdy łączność chmury nie powiodło się.
Co się stanie, jeśli łączność chmury nie powiedzie się dla urządzenia StorSimple w środowisku produkcyjnym?

Jeśli chmury połączenie nie powiedzie się na urządzeniu StorSimple w środowisku produkcyjnym, następnie w zależności od stanu hello urządzenia, hello poniżej może wystąpić: 

* **Dla danych lokalnych hello na urządzeniu**: przez pewien czas nie będą bez przerw w działaniu i odczytów będzie toobe obsłużone. Jednak hello liczba oczekujących zwiększa i przekracza limit, odczyty hello można uruchomić toofail. 
  
    W zależności od hello ilości danych na urządzeniu zapisy hello również będzie toooccur dla hello pierwszy kilka godzin po przerwaniu hello w hello chmury łączności. zapisy Hello zostanie następnie spowolnić i ostatecznie Uruchom toofail, jeśli łączność chmury hello jest zakłócona przez kilka godzin. (Brak magazyn tymczasowy na urządzeniu hello dane toobe wypychana toohello chmury. Ten obszar jest opróżniany po wysłaniu danych hello. Jeśli połączenie nie powiedzie się, dane w tym obszarze magazynu nie zostanie naciśnięty toohello chmury, a nie powiedzie się we/wy.)   
* **Witaj danych w chmurze hello**: większość błędów łączności chmury, zwracany jest błąd. Po przywróceniu łączności hello, hello IOs zostaną wznowione bez hello użytkownika o objętości hello toobring online. W rzadkich przypadkach interwencji użytkownika może być wymagane toobring wstecz hello wolumin do trybu online z hello klasycznego portalu Azure. 
* **Dla migawki w chmurze w toku**: operacja hello jest ponowiona kilka razy w ciągu 4 do 5 godzin i jeśli hello połączenie nie zostanie przywrócona, migawki w chmurze hello zakończy się niepowodzeniem.

### <a name="cluster-alerts"></a>Alerty klastra
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Urządzenie jest w trybie konserwacji. |Urządzenia nie powiodła się za pośrednictwem tooentering lub istniejącym trybu konserwacji. Jest to normalne i nie jest potrzebne nie działanie. Po zostały potwierdzone ten alert, należy go wyczyścić ze strony alerty hello. |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Oprogramowanie układowe urządzenia lub oprogramowania został zaktualizowany. |Wystąpił klastra pracy awaryjnej powodu tooan aktualizacji. Jest to normalne i nie jest potrzebne nie działanie. Po zostały potwierdzone ten alert, należy go wyczyścić ze strony alerty hello. |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Kontroler został wyłączony lub ponownie uruchomiony. |Urządzenie nie za pośrednictwem, ponieważ kontroler active hello został wyłączony lub ponownie uruchomiony przez administratora. Nie jest potrzebne nie działanie. Po zostały potwierdzone ten alert, należy go wyczyścić ze strony alerty hello. |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Planowany tryb failover. |Sprawdź, czy to planowanego trybu failover. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello. |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Nieplanowane przełączenie awaryjne. |StorSimple jest wbudowana Odzyskaj tooautomatically z nieplanowanej pracy w trybie Failover. Jeśli widzisz dużą liczbę alertów, skontaktuj się z Microsoft Support. |
| Urządzenia nie powiodło się za pośrednictwem zbyt <*nazwa urządzenia*>. |Inne/Nieznana przyczyna. |Jeśli widzisz dużą liczbę alertów, skontaktuj się z Microsoft Support. Po hello problem został rozwiązany, wyczyść ten alert z hello strony alertów. |
| Stan raporty o usługach urządzeń krytycznych jako zakończony niepowodzeniem. |Awaria usługi ścieżki danych. |Aby uzyskać pomoc, skontaktuj się z Microsoft Support. |
| Wirtualny adres IP interfejsu sieciowego <*danych #*> zgłasza stan jako zakończony niepowodzeniem. |Inne/Nieznana przyczyna. |Czasami tymczasowych warunków może spowodować te alerty. Jeśli w przypadku hello następnie ten alert zostanie automatycznie usunięty po pewnym czasie. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |
| Wirtualny adres IP interfejsu sieciowego <*danych #*> zgłasza stan jako zakończony niepowodzeniem. |Nazwa interfejsu: <*danych #*> adresu IP <IP address> nie można przełączyć do trybu online, ponieważ na powitania sieci wykryto zduplikowany adres IP. |Upewnij się, że hello zduplikowany adres IP został usunięty z sieci hello lub ponownie skonfiguruj interfejs hello za pomocą innego adresu IP. |

### <a name="disaster-recovery-alerts"></a>Alerty odzyskiwania po awarii
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Operacje odzyskiwania nie może przywrócić wszystkie ustawienia powitania dla tej usługi. Dane konfiguracji urządzenia jest niespójna dla niektórych urządzeń. |Niezgodność danych po awarii. |Zaszyfrowane dane na powitania usługi nie jest zsynchronizowany z tym na urządzeniu hello. Zezwolić urządzeniu hello <*nazwa urządzenia*> z procesu synchronizacji hello toostart Menedżer StorSimple. Użyj hello interfejsu programu Windows PowerShell dla StorSimple toorun hello `Restore-HcsmEncryptedServiceData` na urządzeniu <*nazwa urządzenia*> polecenia cmdlet, zapewniając hello stare hasło jako toothis wejściowy profil zabezpieczeń hello toorestore polecenia cmdlet. Następnie uruchom hello `Invoke-HcsmServiceDataEncryptionKeyChange` klucza szyfrowania danych usługi hello tooupdate polecenia cmdlet. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello. |

### <a name="hardware-alerts"></a>Alerty sprzętu
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Składnik sprzętowy <*identyfikator składnika*> zgłasza stan jako <*stan*>. | |Czasami tymczasowych warunków może spowodować te alerty. Jeśli tak, ten alert zostanie automatycznie usunięty po pewnym czasie. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |
| Kontroler pasywnym działa poprawnie. |Witaj pasywnym (informacje pomocnicze) nie działa. |Urządzenie działa, ale jeden z kontrolerów działa poprawnie. Spróbuj ponownie uruchomić tego kontrolera. Jeśli hello problem nie zniknie, skontaktuj się z Microsoft Support. |
| Wykryto awarię dysku zbliżającym się. | Wykryto awarię dysku zbliżającym się. |Wykryto błąd zbliżającym się dysku dla składników sprzętowych hello "dysków w gnieździe <*gniazdo identyfikator*>, obudowa <*identyfikator obudowy*>". Należy wziąć pod uwagę, zastępując dysk. <br> Przed rozpoczęciem powitalne wymiana dysku, przejrzyj hello następujących informacji.<br><br>Jeśli urządzenie ma więcej niż jednego dysku nie powiodło się, nie należy usuwać więcej niż jeden dysków SSD i HDD w dowolnym momencie. W ten sposób może spowodować utratę danych.<br><br>Upewnij się, umieść zastępczy dysków SSD w miejscu, które wcześniej zawierało dysków SSD. Witaj dotyczy to dysk twardy.<br><br>Gniazda są ponumerowane od 0 too11. Uszkodzony dysk w gnieździe 2 mapuje tooa uszkodzony dysk w gnieździe 3 hello urządzenia (od góry powitania po lewej).<br><br>Aby uzyskać więcej informacji na temat wymiana dysku Przejdź toohttps://go.microsoft.com/fwlink/?linkid=838653. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft za pośrednictwem https://go.microsoft.com/fwlink/?linkid=838654. |

### <a name="job-failure-alerts"></a>Alerty błędów zadania
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Tworzenie kopii zapasowych <*identyfikator grupy woluminu źródłowego*> nie powiodło się. |Zadanie tworzenia kopii zapasowej nie powiodło się. |Problemy z łącznością może uniemożliwiać hello operacji tworzenia kopii zapasowej z pomyślne wykonanie. Jeśli nie ma problemów z połączeniem, możliwe, że osiągnięto hello maksymalną liczbę kopii zapasowych. Usuń wszystkie kopie zapasowe, które nie są już potrzebne i ponów próbę wykonania operacji hello. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello. |
| Klon <*źródła identyfikatory elementów kopii zapasowych*> zbyt <*numery seryjne wolumin docelowy*> nie powiodło się. |Zadanie klonowania nie powiodło się. |Odświeżanie hello listy kopii zapasowych tooverify, który hello kopii zapasowej jest nadal ważny. Jeśli kopia zapasowa hello jest poprawna, istnieje możliwość, że problemy z łącznością chmury uniemożliwiają pomyślnie ukończenie operacji klonowania hello. Jeśli nie ma problemów z połączeniem, możliwe, że osiągnięto limit magazynu hello. Usuń wszystkie kopie zapasowe, które nie są już potrzebne i ponów próbę wykonania operacji hello. Po wykonaniu problem hello tooresolve odpowiednią akcję, usuń zaznaczenie tego alertu na stronie Alerty hello. |
| Przywracanie <*źródła identyfikatory elementów kopii zapasowych*> nie powiodło się. |Przywróć zadanie nie powiodło się. |Odświeżanie hello listy kopii zapasowych tooverify, który hello kopii zapasowej jest nadal ważny. Jeśli kopia zapasowa hello jest poprawna, istnieje możliwość, że problemy z łącznością chmury uniemożliwiają pomyślne wykonanie operacji przywracania hello. Jeśli nie ma problemów z połączeniem, możliwe, że osiągnięto limit magazynu hello. Usuń wszystkie kopie zapasowe, które nie są już potrzebne i ponów próbę wykonania operacji hello. Po wykonaniu problem hello tooresolve odpowiednią akcję, usuń zaznaczenie tego alertu na stronie Alerty hello. |

### <a name="locally-pinned-volume-alerts"></a>Alerty woluminu przypiętego lokalnie
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Tworzenie woluminu lokalnego <*nazwa woluminu*> nie powiodło się. |zadanie tworzenia woluminu Hello nie powiodło się. <*Toohello odpowiedni komunikat błędu nie powiodło się, kod błędu:*>. |Problemy z łącznością może uniemożliwiać hello miejsca tworzenia pomyślnie ukończenie operacji. Woluminów przypiętych lokalnie jest alokowany nieelastycznie i proces tworzenia miejsca hello obejmuje przechodzeniu woluminy warstwowe toohello chmury. Jeśli nie ma problemów z połączeniem, może wykorzystał hello lokalne miejsce na powitania urządzenia. Określ, czy miejsce istnieje na urządzeniu hello, przed ponowną próbą wykonania tej operacji. |
| Rozszerzanie woluminu lokalnego <*nazwa woluminu*> nie powiodło się. |Hello woluminu modyfikacji zadanie nie powiodło się ze względu zbyt <*toohello odpowiedni komunikat błędu nie powiodło się, kod błędu:*>. |Problemy z łącznością może uniemożliwiać hello woluminu rozszerzenia pomyślnie ukończenie operacji. Woluminów przypiętych lokalnie jest alokowany nieelastycznie i proces hello rozszerzenia istniejącej przestrzeni hello obejmuje przechodzeniu woluminy warstwowe toohello chmury. Jeśli nie ma problemów z połączeniem, może wykorzystał hello lokalne miejsce na powitania urządzenia. Określ, czy miejsce istnieje na urządzeniu hello, przed ponowną próbą wykonania tej operacji. |
| Konwersja woluminu <*nazwa woluminu*> nie powiodło się. |Hello konwersji zadania tooconvert hello woluminu typ woluminu z tootiered przypiętych lokalnie nie powiodło się. |Nie można wykonać konwersji hello woluminu z tootiered typu przypięty lokalnie. Upewnij się, że nie ma problemów z połączeniem uniemożliwia operację hello pomyślne zakończenie działania. Do rozwiązywania problemów z łącznością problemów Przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>wolumin przypięty lokalnie Hello oryginalnego teraz została oznaczona jako wolumin warstwowy, ponieważ część danych hello z woluminu przypiętego lokalnie hello ma rozrzucone chmury toohello podczas konwersji hello. Wynikowe wolumin warstwowy Hello nadal zajmuje lokalne miejsce na urządzeniu hello, którego nie można odzyskać przyszłych woluminów lokalnych.<br>Rozwiąż wszelkie problemy dotyczące łączności, wyczyść hello alert i konwertowanie tego woluminu wstecz toohello oryginalnego woluminu przypiętego lokalnie typu tooensure wszystkie dane hello jest udostępniana lokalnie ponownie. |
| Konwersja woluminu <*nazwa woluminu*> nie powiodło się. |Hello konwersji zadania tooconvert hello woluminu typ woluminu z warstwową toolocally przypięty nie powiodło się. |Nie można wykonać konwersji hello woluminu z typu, który przypięty toolocally warstwowego. Upewnij się, że nie ma problemów z połączeniem uniemożliwia operację hello pomyślne zakończenie działania. Do rozwiązywania problemów z łącznością problemów Przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>Hello oryginalnego woluminu warstwowego teraz oznaczona jako wolumin przypięty lokalnie, jako część procesu konwersji hello nadal toohave danych znajdującej się w chmurze hello podczas hello alokowany nieelastycznie miejsca na urządzeniu powitania dla tego woluminu nie będzie można odzyskać do przyszłych lokalnej woluminy.<br>Rozwiąż wszelkie problemy z łącznością, hello wyczyść alert i przekonwertować tego woluminu wstecz toohello oryginalnego woluminu warstwowego typu tooensure lokalne miejsce alokowany nieelastycznie na urządzeniu hello można odzyskać. |
| Niedługo lokalne miejsce zużycie inaczej lokalnymi migawkami <*Nazwa grupy woluminu*> |Migawki lokalne powitania zasad tworzenia kopii zapasowej może być wkrótce zabraknie miejsca i być nieważne tooavoid błędy zapisu hosta. |Częste migawki lokalne obok danych z dużą ilość danych churn w skojarzonych z tą grupą zasad tworzenia kopii zapasowych woluminów hello powodują lokalne miejsce na powitania toobe urządzenia używane szybko. Usuń wszystkie migawki lokalne, które nie są już potrzebne. Również zaktualizować planów migawka lokalna dla tej zasady tworzenia kopii zapasowej tootake mniej częste migawki lokalne i zapewnić regularnie podjęcie migawki w chmurze. Te akcje nie są brane, lokalne miejsce dla migawek wkrótce może wyczerpane i hello system zostanie automatycznie usunąć tooensure, który zapisuje hosta kontynuować toobe przetworzone pomyślnie. |
| Migawki lokalne dla <*Nazwa grupy woluminu*> zostały unieważnione. |Witaj migawki lokalne dla <*Nazwa grupy woluminu*> unieważniona, a następnie usunąć, ponieważ zostały one przekraczającej hello lokalne miejsce na urządzeniu hello. |tooensure to nie powtarzać w przyszłości hello, przejrzyj hello migawka lokalna harmonogramy dla tych zasad tworzenia kopii zapasowej i usuń wszelkie migawki lokalne, które nie są już potrzebne. Częste migawki lokalne obok danych z dużą ilość danych churn w woluminach hello skojarzonych z tą grupą zasad tworzenia kopii zapasowej może spowodować lokalne miejsce na powitania toobe urządzenia używane szybko. |
| Przywracanie <*źródła identyfikatory elementów kopii zapasowych*> nie powiodło się. |Zadanie przywracania Hello nie powiodło się. |Jeśli przypięty lokalnie lub mieszane woluminów warstwowych i przypiętych lokalnie w tych zasad tworzenia kopii zapasowej tooverify listy kopii zapasowych hello odświeżania, który hello kopii zapasowej jest nadal ważny. Jeśli kopia zapasowa hello jest poprawna, istnieje możliwość, że problemy z łącznością chmury uniemożliwiają pomyślne wykonanie operacji przywracania hello. lokalne powitania przypięty woluminów, które zostały przywracana jako część tej grupy migawki nie ma wszystkich swoich urządzeń toohello pobrane dane, a jeśli masz kombinację woluminów warstwowych i przypiętych lokalnie w tej grupie migawki, nie będzie on zsynchronizowany ze sobą. toosuccessfully ukończyć powitalnych operacji przywracania, wykonać woluminów hello w tej grupie w tryb offline na hoście hello i ponów próbę wykonania operacji przywracania hello. Uwaga w procesie przywracania danych woluminu toohello zmiany wykonane podczas hello zostaną utracone. |

### <a name="networking-alerts"></a>Alerty sieci
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Nie można uruchomić usług StorSimple. |Błąd ścieżki danych |Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |
| "Data0" Wykryto zduplikowany adres IP. | |Witaj system wykrył konflikt adresu IP "10.0.0.1". Witaj zasobu sieciowego "Data0" na urządzeniu hello  *<device1>*  jest w trybie offline. Upewnij się, że ten adres IP nie jest używany przez inne jednostki w tej sieci. problemy z siecią tootroubleshoot, przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Aby uzyskać pomoc w rozwiązaniu tego problemu, skontaktuj się z administratorem sieci. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |
| Adres IPv4 (lub IPv6) dla "Data0" jest w trybie offline. | |zasobu sieciowego Hello "Data0" o adresie IP "10.0.0.1". i długość "22" prefiksu na urządzeniu hello  *<device1>*  jest w trybie offline. Upewnij się, że hello toowhich portów przełącznika, ten interfejs jest podłączony są operacyjną. problemy z siecią tootroubleshoot, przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |

### <a name="performance-alerts"></a>Alerty wydajności
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Witaj obciążenia urządzenia przekroczyła <*próg*>. |Wolniej niż oczekiwany czas odpowiedzi. |Urządzenie raportuje użycie bardzo duże obciążenie wejścia/wyjścia. Może to spowodować pracy toonot urządzenia, a także powinno. Przejrzyj obciążeń hello podłączone urządzenie toohello i ustalić, jeśli istnieją jakieś, który może być przeniesiony tooanother urządzenia lub które nie są już wymagane.<br>toounderstand hello bieżący stan, odwiedź zbyt[Użyj hello toomonitor usługi Menedżer StorSimple, urządzenia](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Alerty zabezpieczeń
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Microsoft Support sesji zostało uruchomione. |Innych firm dostęp do sesji pomocy technicznej. |Potwierdź, że taki dostęp jest autoryzowany. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello. |
| Hasło dla <*elementu*> wygaśnie za <*czas*>. |Zbliża się do wygaśnięcia hasła. |Zmień hasło przed jego wygaśnięciem. |
| Brak informacji o konfiguracji zabezpieczeń <*identyfikator elementu*>. | |Witaj woluminy skojarzone z tym kontenerem woluminu nie może być używane tooreplicate konfiguracji StorSimple. tooensure bezpiecznie przechowywane dane, zaleca się usunięcie kontenera woluminów hello zaś wszelkie woluminy skojarzone z hello kontenera woluminów. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello. |
| <*numer*> prób logowania nie powiodła się dla <*identyfikator elementu*>. |Wiele nieudane próby logowania. |Urządzenie może zostać zaatakowany lub uwierzytelniony użytkownik próbuje tooconnect przy użyciu niepoprawnego hasła.<ul><li>Skontaktuj się z autoryzowanych użytkowników i sprawdź, czy te próby zostały z wiarygodnego źródła. Jeśli będziesz kontynuować toosee dużej liczby nieudanych prób logowania, należy wziąć pod uwagę wyłączanie zdalnego zarządzania i skontaktować się z administratorem sieci. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello.</li><li>Sprawdź, czy swoich wystąpień Snapshot Manager zostały skonfigurowane z hello poprawne hasło. Po wykonaniu odpowiednich działań, usuń zaznaczenie tego alertu na stronie Alerty hello.</li></ul>Aby uzyskać więcej informacji, przejdź zbyt[zmienić hasło urządzenia wygasłe](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Podczas zmiany klucza szyfrowania danych usługi hello wystąpił jeden lub więcej błędów. | |Wystąpiły błędy podczas zmieniania klucza szyfrowania danych usługi hello. Po usunąć czynniki powodujące błędy hello, uruchom hello `Invoke-HcsmServiceDataEncryptionKeyChange` polecenia cmdlet z hello interfejsu systemu Windows PowerShell dla urządzenia StorSimple w usłudze hello tooupdate urządzenia. Jeśli ten problem będzie nadal występować, skontaktuj się z pomocą techniczną firmy Microsoft. Po rozwiązaniu problemu hello wyczyść ten alert z hello strony alertów. |

### <a name="support-package-alerts"></a>Obsługa alertów pakietu
| Tekst alertu | Wydarzenie | Więcej informacji / zalecane akcje |
|:--- |:--- |:--- |
| Nie można utworzyć pakietu obsługi. |StorSimple nie może wygenerować hello pakietu. |Ponów tę operację. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. Po rozwiązaniu problemu hello, usuń zaznaczenie tego alertu na stronie Alerty hello. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [StorSimple błędy i rozwiązywanie problemów z działającego urządzenia](storsimple-troubleshoot-operational-device.md).

