---
title: "aaaStart/zatrzymywania maszyn wirtualnych podczas rozwiązania poza godzinami szczytu [Podgląd] | Dokumentacja firmy Microsoft"
description: "rozwiązania do zarządzania maszyny Wirtualnej Hello uruchamia i zatrzymuje maszyn wirtualnych platformy Azure Resource Manager zgodnie z harmonogramem i aktywnego monitorowania z analizy dzienników."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Rozwiązanie umożliwiające uruchamianie/zatrzymywanie maszyn wirtualnych poza godzinami szczytu [wersja zapoznawcza] w usłudze Automation

Hello uruchamiania/zatrzymywania maszyn wirtualnych podczas rozwiązania poza godzinami szczytu [Podgląd] uruchamia i zatrzymuje maszynach wirtualnych Azure Resource Manager zgodnie z harmonogramem zdefiniowane przez użytkownika i zapewnia wgląd w hello Powodzenie hello automatyzacji zadań, które uruchamianie i zatrzymywanie maszyn wirtualnych z usługą OMS Analiza dzienników.  

## <a name="prerequisites"></a>Wymagania wstępne

- elementy runbook Hello pracować z [konta Uruchom jako platformy Azure](automation-offering-get-started.md#authentication-methods).  Witaj konta Uruchom jako jest hello preferowana metoda uwierzytelniania, ponieważ zamiast hasła, który może wygaśnie lub zmienić często używa certyfikatu uwierzytelniania.  

- To rozwiązanie może zarządzać tylko maszyn wirtualnych, które znajdują się w hello tej samej subskrypcji co gdzie znajduje się hello konta automatyzacji.  

- To rozwiązanie obejmuje jedynie toohello następujące regiony platformy Azure - Australia Południowo-Wschodnia, wschodnie stany USA, Azja południowo-wschodnia i Europa Zachodnia.  elementów runbook Hello zarządzania hello harmonogramem maszyny Wirtualnej można kierować maszyn wirtualnych w dowolnym regionie.  

- powiadomienia e-mail toosend, gdy hello uruchamianie i zatrzymywanie elementów runbook wirtualna pełną, subskrypcję usługi Office 365 klasy biznesowej jest wymagana.  

## <a name="solution-components"></a>Składniki rozwiązania

To rozwiązanie składa się z następujących zasobów, które zostaną zaimportowane i dodać konto automatyzacji tooyour hello.

### <a name="runbooks"></a>Elementy Runbook

Element Runbook | Opis|
--------|------------|
CleanSolution-MS-Mgmt-VM | Ten element runbook spowoduje usunięcie wszystkich zawartych w niej zasobów i harmonogramy po przejściu toodelete hello rozwiązania z subskrypcji.|  
SendMailO365-MS-Mgmt | Ten element Runbook wysyła wiadomość e-mail za pośrednictwem programu Exchange w usłudze Office 365.|
StartByResourceGroup-MS-Mgmt-VM | Ten element runbook jest zamierzone toostart maszyn wirtualnych (zarówno classic i maszyn wirtualnych na podstawie ARM) który znajduje się w danej listy grup zasobów platformy Azure.
StopByResourceGroup-MS-Mgmt-VM | Ten element runbook jest zamierzone toostop maszyn wirtualnych (zarówno classic i maszyn wirtualnych na podstawie ARM) który znajduje się w danej listy grup zasobów platformy Azure.|
<br>

### <a name="variables"></a>Zmienne

Zmienna | Opis|
---------|------------|
Element Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Określa, czy elementy Runbook StartByResourceGroup-MS-Mgmt-VM i StopByResourceGroup-MS-Mgmt-VM mogą wysyłać powiadomienia e-mail po zakończeniu działania.  Wybierz **True** tooenable i **False** toodisable poczty e-mail alertów. Wartość domyślna to **False**.| 
Element Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Wprowadź wykluczone z zarządzania operację; toobe nazwy maszyny Wirtualnej Rozdziel nazwy przy użyciu semi-colon(;) nie może zawierać spacji. W wartościach jest rozróżniana wielkość liter. Dopuszcza się użycie symbolu wieloznacznego (gwiazdki).|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Tekst, który może być dołączane toohello początku treść wiadomości e-mail hello.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Określa nazwę hello hello konto automatyzacji zawierające hello runbook wiadomości E-mail.  **Nie należy modyfikować tej zmiennej.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Określa nazwę hello hello runbook wiadomości e-mail.  To jest używany przez hello StartByResourceGroup-MS-Mgmt-VM i StopByResourceGroup-MS-Mgmt-VM elementów runbook toosend w wiadomości e-mail.  **Nie należy modyfikować tej zmiennej.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Określa nazwę hello hello grupę zasobów, która zawiera hello runbook wiadomości E-mail.  **Nie należy modyfikować tej zmiennej.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Określa tekst hello hello wiersz tematu wiadomości e-mail hello.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Określa adresaci hello hello poczty e-mail.  Wprowadź inne nazwy przy użyciu semi-colon(;) nie może zawierać spacji.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Wprowadź wykluczone z zarządzania operację; toobe nazwy maszyny Wirtualnej Rozdziel nazwy przy użyciu semi-colon(;) nie może zawierać spacji. W wartościach jest rozróżniana wielkość liter. Dopuszcza się użycie symbolu wieloznacznego (gwiazdki).  Wartość domyślna (gwiazdkę) będzie zawierać wszystkich grup zasobów w subskrypcji hello.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Określa hello subskrypcji, która zawiera toobe maszyn wirtualnych zarządzanych przez tego rozwiązania.  Musi to być hello tej samej subskrypcji, w którym znajduje się hello konta automatyzacji tego rozwiązania.|
Element Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Wprowadź wykluczone z zarządzania operację; toobe nazwy maszyny Wirtualnej Rozdziel nazwy przy użyciu semi-colon(;) nie może zawierać spacji. W wartościach jest rozróżniana wielkość liter. Dopuszcza się użycie symbolu wieloznacznego (gwiazdki).|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Tekst, który może być dołączane toohello początku treść wiadomości e-mail hello.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Określa nazwę hello hello konto automatyzacji zawierające hello runbook wiadomości E-mail.  **Nie należy modyfikować tej zmiennej.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Określa nazwę hello hello grupę zasobów, która zawiera hello runbook wiadomości E-mail.  **Nie należy modyfikować tej zmiennej.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Określa tekst hello hello wiersz tematu wiadomości e-mail hello.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Określa adresaci hello hello poczty e-mail.  Wprowadź inne nazwy przy użyciu semi-colon(;) nie może zawierać spacji.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Wprowadź wykluczone z zarządzania operację; toobe nazwy maszyny Wirtualnej Rozdziel nazwy przy użyciu semi-colon(;) nie może zawierać spacji. W wartościach jest rozróżniana wielkość liter. Dopuszcza się użycie symbolu wieloznacznego (gwiazdki).  Wartość domyślna (gwiazdkę) będzie zawierać wszystkich grup zasobów w subskrypcji hello.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Określa hello subskrypcji, która zawiera toobe maszyn wirtualnych zarządzanych przez tego rozwiązania.  Musi to być hello tej samej subskrypcji, w którym znajduje się hello konta automatyzacji tego rozwiązania.|  
<br>

### <a name="schedules"></a>Harmonogramy

Harmonogram | Opis|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Harmonogram StartByResourceGroup elementu runbook, który przeprowadza hello uruchamiania maszyn wirtualnych zarządzanych przez tego rozwiązania. Podczas tworzenia, domyślnie tooUTC strefy czasowej.|
StopByResourceGroup-Schedule-MS-Mgmt | Harmonogram StopByResourceGroup elementu runbook, który przeprowadza hello zamykania maszyn wirtualnych zarządzanych przez tego rozwiązania. Podczas tworzenia, domyślnie tooUTC strefy czasowej.|

### <a name="credentials"></a>Poświadczenia

Poświadczenie | Opis|
-----------|------------|
O365Credential | Określa nieprawidłowy e-mail toosend konta użytkownika usługi Office 365.  Wymagany tylko wtedy, gdy zmienna SendMailO365-IsSendEmail-MS-Mgmt ustawiono zbyt**True**.

## <a name="configuration"></a>Konfiguracja

Wykonaj powitania po hello tooadd kroki uruchamiania/zatrzymywania maszyn wirtualnych w tooyour rozwiązania poza godzinami szczytu [Podgląd] konta automatyzacji, a następnie skonfiguruj hello zmienne toocustomize hello rozwiązania.

1. Z hello głównej ekranu w hello portalu Azure, wybierz hello **Marketplace** kafelka.  Wybierz Kafelek hello jest już przypięty tooyour głównej ekranu, w okienku nawigacji po lewej stronie powitania **nowy**.  
2. W bloku portalu Marketplace hello wpisz **uruchamianie maszyny Wirtualnej** w polu wyszukiwania hello a rozwiązanie a następnie wybierz pozycję hello **uruchamiania/zatrzymywania maszyn wirtualnych w godzinach [Podgląd]** hello wyników wyszukiwania.  
3. W hello **uruchamiania/zatrzymywania maszyn wirtualnych w godzinach [Podgląd]** bloku hello wybrane rozwiązanie, Przejrzyj podsumowanie hello, a następnie kliknij przycisk **Utwórz**.  
4. Witaj **Dodaj rozwiązanie** zostanie wyświetlony blok gdzie zostanie wyświetlony monit o tooconfigure hello rozwiązania są przed zaimportowaniem go w ramach subskrypcji automatyzacji.<br><br> ![Zarządzanie maszynami wirtualnymi — blok Dodawanie rozwiązania](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Na powitania **Dodaj rozwiązanie** bloku, wybierz opcję **obszaru roboczego** i tutaj wybierz obszar roboczy OMS, który jest połączony toohello znajduje się w tej samej subskrypcji Azure, która hello konta automatyzacji lub Utwórz nowy obszar roboczy OMS.  Jeśli nie masz obszar roboczy OMS, możesz wybrać **Utwórz nowy obszar roboczy** i na powitania **obszarem roboczym pakietu OMS** blok, wykonaj następujące hello: 
   - Określ nazwę nowej hello **obszarem roboczym pakietu OMS**.
   - Wybierz **subskrypcji** toolink tooby wybierając z listy rozwijanej hello Jeśli hello domyślne nie jest odpowiedni.
   - W pozycji **Grupa zasobów** możesz utworzyć nową grupę zasobów lub wybrać istniejącą grupę zasobów.  
   - Wybierz **lokalizację**.  Obecnie są jedynymi lokalizacjami hello przewidzianych wybór **południowo-wschodnia Australia**, **wschodnie stany USA**, **Azja południowo-wschodnia**, i **Europa**.
   - Wybierz **warstwę cenową**.  rozwiązanie Hello jest oferowany dwóch warstw: Zwolnij i OMS płatnej warstwy.  Witaj warstwa bezpłatna ma ograniczenie na powitania ilość danych zbieranych dziennie, okres przechowywania i minut czasu wykonywania zadania elementu runbook.  Witaj OMS płatnej warstwy nie ma limit na powitania ilość danych zbieranych dziennie.  

        > [!NOTE]
        > Podczas wyświetlania hello autonomiczny płatnej warstwy jako opcja, nie ma zastosowania.  Zaznacz go i kontynuować tworzenie hello tego rozwiązania, w ramach subskrypcji, jego zakończy się niepowodzeniem.  Ten problem zostanie rozwiązany po oficjalnym wydaniu tego rozwiązania.<br>Jeśli używasz tego rozwiązania, będzie ono używać wyłącznie minut zadania automatyzacji oraz pozyskiwania dziennika.  rozwiązanie Hello nie dodać dodatkowe środowiska tooyour węzłów OMS.  

6. Po podaniu informacji hello wymagane na powitania **obszarem roboczym pakietu OMS** bloku, kliknij przycisk **Utwórz**.  Informacje hello jest weryfikowany i utworzeniu hello obszaru roboczego, można śledzić postęp w obszarze **powiadomienia** hello menu.  Zostanie zwrócony toohello **Dodaj rozwiązanie** bloku.  
7. Na powitania **Dodaj rozwiązanie** bloku, wybierz opcję **konto automatyzacji**.  Jeśli tworzysz nowy obszar roboczy OMS, konieczna będzie tooalso Utwórz nowe konto automatyzacji, która zostanie skojarzona z hello nowy obszar roboczy OMS określony wcześniej, łącznie z Twojej subskrypcji platformy Azure, grupy zasobów i region.  Możesz wybrać **utworzyć konto usługi automatyzacja** i na powitania **konto automatyzacji dodać** bloku, podaj poniżej hello: 
  - W hello **nazwa** wprowadź nazwę hello hello konta automatyzacji.

    Wszystkie inne opcje są wypełniane automatycznie na podstawie na wybrany obszar roboczy OMS hello i nie można zmodyfikować te opcje.  Konto Uruchom jako platformy Azure jest hello domyślną metodą uwierzytelniania dla elementów runbook hello zawartych w tym rozwiązaniu.  Po kliknięciu **OK**, opcje konfiguracji hello są weryfikowane i utworzeniu hello konta automatyzacji.  Można śledzić postęp w obszarze **powiadomienia** hello menu. 

    W przeciwnym razie możesz wybrać istniejące konto Uruchom jako usługi Automation.  Należy pamiętać, że konto hello, którą wybierzesz już nie może być połączone tooanother obszarem roboczym pakietu OMS inaczej wiadomości będą wyświetlane w tooinform bloku hello należy.  Jeśli jest już połączony, będzie konieczne tooselect innego konta Uruchom jako automatyzacji lub Utwórz nową.<br><br> ![Konto już połączone tooOMS automatyzacji obszaru roboczego](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Na koniec na powitania **Dodaj rozwiązanie** bloku, wybierz opcję **konfiguracji** i hello **parametry** zostanie wyświetlony blok.  Na powitania **parametry** bloku, zostanie wyświetlony monit:  
   - Określ hello **nazw grupa zasobów docelowych**, czyli nazwy grupy zasobów, która zawiera toobe maszyn wirtualnych zarządzanych przez tego rozwiązania.  Wprowadzić możesz kilka nazw i oddzielić je przy użyciu średnika (w wartościach jest rozróżniana wielkość liter).  Przy użyciu symboli wieloznacznych jest obsługiwana, jeśli chcesz, aby tootarget maszyn wirtualnych we wszystkich grupach zasobów w subskrypcji hello.
   - Wybierz **harmonogram** czyli cyklicznego datę i godzinę dla uruchamiania i zatrzymywania hello maszyny Wirtualnej w hello docelowego grup zasobów.  Domyślnie harmonogram hello jest skonfigurowany toohello UTC strefy czasowej, i wybrać inny region nie jest dostępna.  Jeśli chcesz tooconfigure hello harmonogram tooyour określonej strefy czasowej po skonfigurowaniu hello rozwiązania, zobacz [hello modyfikowanie harmonogramu uruchamiania i wyłączania](#modifying-the-startup-and-shutdown-schedule) poniżej.    

10. Po zakończeniu konfigurowania ustawień początkowej hello wymagane przez rozwiązanie hello wybierz **Utwórz**.  Wszystkie ustawienia zostaną zweryfikowane, a następnie próbuje toodeploy hello rozwiązania w ramach subskrypcji.  Ten proces może potrwać kilka sekund toocomplete i można śledzić postęp w obszarze **powiadomienia** hello menu. 

## <a name="collection-frequency"></a>Częstotliwość zbierania

Automatyzacja zadania dziennika i zadania strumienia danych jest pozyskanych w repozytorium OMS hello co pięć minut.  

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po dodaniu hello rozwiązania do zarządzania maszyny Wirtualnej w Twojej hello obszar roboczy OMS **widoku StartStopVM** kafelka zostanie dodany tooyour OMS z pulpitu nawigacyjnego.  Ten Kafelek Wyświetla graficzną reprezentację zadania elementów runbook hello hello rozwiązania, które zostały uruchomione i została ukończona pomyślnie i liczba.<br><br> ![Zarządzanie maszynami wirtualnymi — kafelek Widok StartStopVM](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Na koncie automatyzacji można uzyskać dostęp i zarządzać nimi rozwiązania hello wybierając hello **rozwiązań** Kafelek, a następnie z hello **rozwiązań** bloku, wybierając rozwiązania hello **[Start-Stop-VM Obszar roboczy]** z listy hello.<br><br> ![Lista rozwiązań usługi Automation](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Wybranie rozwiązania hello spowoduje wyświetlenie hello **Start-Stop-VM [obszaru roboczego]** bloku rozwiązania, w którym można przejrzeć ważne informacje, takie jak hello **StartStopVM** Kafelek tak samo, jak w obszarze roboczym pakietu OMS, które przedstawia liczbę i graficzną reprezentację zadania elementów runbook hello hello rozwiązania, które zostały uruchomione i zostały ukończone pomyślnie.<br><br> ![Blok rozwiązania maszyny wirtualnej w usłudze Automation](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

W tym miejscu możesz także Otwórz obszar roboczy OMS i podczas dalszej analizy hello rekordów zadań.  Po prostu kliknij **wszystkie ustawienia**w hello **ustawienia** bloku, wybierz opcję **Szybki Start** , a następnie w hello **Szybki Start** wybierz bloku  **Portalu OMS**.   To spowoduje otwarcie nowej karty lub nowej sesji przeglądarki i wyświetlenie obszaru roboczego OMS skojarzonego z Twoim kontem i subskrypcją usługi Automation.  


### <a name="configuring-e-mail-notifications"></a>Konfigurowanie powiadomień e-mail

tooenable powiadomienia e-mail, gdy hello uruchamianie i zatrzymywanie elementów runbook wirtualna pełną, konieczne będzie toomodify hello **O365Credential** poświadczeń i co najmniej hello następujących zmiennych:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

Witaj tooconfigure **O365Credential** poświadczeń, wykonaj następujące kroki hello:

1. Twoje konto usługi Automatyzacja kliknij **wszystkie ustawienia** u góry hello hello okna. 
2. Na powitania **ustawienia** bloku sekcji hello **zasobów automatyzacji**, wybierz pozycję **zasoby**. 
3. Na powitania **zasoby** bloku, wybierz hello **poświadczeń** Kafelek i z hello **poświadczeń** bloku, wybierz hello **O365Credential**.  
4. Wprowadź prawidłową nazwę użytkownika usługi Office 365 i hasło, a następnie kliknij przycisk **zapisać** toosave zmiany.  

zmienne hello tooconfigure wyróżnione wcześniej, wykonaj hello następujące kroki:

1. Twoje konto usługi Automatyzacja kliknij **wszystkie ustawienia** u góry hello hello okna. 
2. Na powitania **ustawienia** bloku sekcji hello **zasobów automatyzacji**, wybierz pozycję **zasoby**. 
3. Na powitania **zasoby** bloku, wybierz hello **zmienne** Kafelek i z hello **zmienne** bloku, wybierz zmienną hello wymienionych powyżej, a następnie zmodyfikuj jego wartość hello Opis dla niego określone w hello [zmiennej](##variables) wcześniejszej sekcji.  
4. Kliknij przycisk **zapisać** toosave hello zmiany toohello zmiennej.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Modyfikowanie harmonogramu uruchamiania i wyłączania hello

Zarządzanie hello uruchamiania i wyłączania harmonogramu w tym rozwiązaniu następuje hello same kroki opisane w [Planowanie elementu runbook automatyzacji Azure](automation-schedules.md).  Należy pamiętać, że nie można zmodyfikować hello konfiguracji harmonogramu.  Konieczne będzie toodisable hello istniejący harmonogram, a następnie utwórz nowy, a następnie połącz toohello **StartByResourceGroup-MS-Mgmt-VM** lub **StopByResourceGroup-MS-Mgmt-VM** elementu runbook, które mają hello Planowanie tooapply do.   

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics

Automatyzacja tworzy dwa typy rekordów w repozytorium OMS hello.

### <a name="job-logs"></a>Dzienniki zadań

Właściwość | Opis|
----------|----------|
Obiekt wywołujący |  Kto zainicjował operację hello.  Możliwe wartości to adres e-mail lub system w przypadku zaplanowanych zadań.|
Kategoria | Klasyfikacja hello typu danych.  Do automatyzacji wartość hello jest JobLogs.|
CorrelationId | Identyfikator GUID jest hello identyfikator korelacji hello zadania elementu runbook.|
JobId | Identyfikator GUID jest hello identyfikator hello zadania elementu runbook.|
operationName | Określa typ hello operacje wykonywane na platformie Azure.  Do automatyzacji hello wartość będzie zadania.|
resourceId | Określa typ zasobu hello na platformie Azure.  Do automatyzacji wartość hello jest skojarzony z elementem runbook hello konta automatyzacji hello.|
ResourceGroup | Określa nazwę grupy zasobów hello hello zadanie elementu runbook.|
ResourceProvider | Określa hello Azure usługa, która dostarcza hello zasobów można wdrażać i zarządzać nimi.  Do automatyzacji wartość hello jest automatyzacji Azure.|
ResourceType | Określa typ zasobu hello na platformie Azure.  Do automatyzacji wartość hello jest skojarzony z elementem runbook hello konta automatyzacji hello.|
resultType | Stan Hello hello zadanie elementu runbook.  Możliwe wartości:<br>— Uruchomione<br>— Zatrzymane<br>— Wstrzymane<br>— Nie powiodło się<br>— Powiodło się|
resultDescription | Opisuje stan wyniku zadania elementu runbook hello.  Możliwe wartości:<br>— Zadanie jest uruchomione<br>— Zadanie nie powiodło się<br>— Zadanie zostało ukończone|
RunbookName | Określa nazwę hello hello elementu runbook.|
SourceSystem | Określa hello system źródła danych hello przesłane.  Do automatyzacji, zostanie użyta wartość hello: OpsManager|
StreamType | Określa typ hello zdarzenia. Możliwe wartości:<br>— Pełne<br>— Dane wyjściowe<br>— Błąd<br>— Ostrzeżenie|
SubscriptionId | Określa identyfikator subskrypcji hello hello zadania.
Time | Data i godzina, kiedy wykonać zadanie elementu runbook hello.|


### <a name="job-streams"></a>Strumienie zadania

Właściwość | Opis|
----------|----------|
Obiekt wywołujący |  Kto zainicjował operację hello.  Możliwe wartości to adres e-mail lub system w przypadku zaplanowanych zadań.|
Kategoria | Klasyfikacja hello typu danych.  Do automatyzacji wartość hello jest JobStreams.|
JobId | Identyfikator GUID jest hello identyfikator hello zadania elementu runbook.|
operationName | Określa typ hello operacje wykonywane na platformie Azure.  Do automatyzacji hello wartość będzie zadania.|
ResourceGroup | Określa nazwę grupy zasobów hello hello zadanie elementu runbook.|
resourceId | Określa identyfikator zasobu hello na platformie Azure.  Do automatyzacji wartość hello jest skojarzony z elementem runbook hello konta automatyzacji hello.|
ResourceProvider | Określa hello Azure usługa, która dostarcza hello zasobów można wdrażać i zarządzać nimi.  Do automatyzacji wartość hello jest automatyzacji Azure.|
ResourceType | Określa typ zasobu hello na platformie Azure.  Do automatyzacji wartość hello jest skojarzony z elementem runbook hello konta automatyzacji hello.|
resultType | wynik Hello hello zadanie elementu runbook w zdarzeniu hello czasu hello został wygenerowany.  Możliwe wartości:<br>— W toku|
resultDescription | Obejmuje strumienia wyjściowego hello z hello elementu runbook.|
RunbookName | Nazwa Hello hello elementu runbook.|
SourceSystem | Określa hello system źródła danych hello przesłane.  Do automatyzacji hello zostanie użyta wartość OpsManager|
StreamType | Typ Hello strumienia zadania. Możliwe wartości:<br>— Postęp<br>— Dane wyjściowe<br>— Ostrzeżenie<br>— Błąd<br>— Debugowanie<br>— Pełne|
Time | Data i godzina, kiedy wykonać zadanie elementu runbook hello.|

Po wykonaniu wyszukiwania dziennika zwraca rekordów kategorii **JobLogs** lub **JobStreams**, możesz wybrać hello **JobLogs** lub **JobStreams** widoku, który zawiera zestaw kafelków podsumowania aktualizacji hello zwrócona przez wyszukiwanie hello.

## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników

Witaj poniższej tabeli przedstawiono przykładowy dziennik wyszukuje rekordów zadań zebrane przez to rozwiązanie. 

Zapytanie | Opis|
----------|----------|
Znajdź zadania dla elementu Runbook StartVM, które zostały zakończone powodzeniem | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Znajdź zadania dla elementu Runbook StopVM, które zostały zakończone powodzeniem | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Pokaż stan zadania w czasie dla elementów Runbook StartVM i StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Usuwanie hello rozwiązania

Jeśli zdecydujesz, że nie są już potrzebne rozwiązania hello toouse żadnych dalszych, należy ją usunąć z hello konta automatyzacji.  Trwa usuwanie rozwiązania hello powoduje tylko usunięcie elementów runbook hello, nie spowoduje usunięcia harmonogramy hello lub zmienne, które zostały utworzone podczas dodawania hello rozwiązania.  Te zasoby należy toodelete ręcznie, jeśli nie używasz je z innymi elementami runbook.  

toodelete hello rozwiązanie, wykonaj następujące kroki hello:

1.  Twoje konto usługi Automatyzacja, zaznacz hello **rozwiązań** kafelka.  
2.  Na powitania **rozwiązań** bloku, wybierz hello rozwiązania **Start-Stop-VM [obszaru roboczego]**.  Na powitania **VMManagementSolution [obszaru roboczego]** bloku, kliknij przycisk menu hello **usunąć**.<br><br> ![Usuwanie maszyny Wirtualnej Mgmt rozwiązania](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  W hello **Usuń rozwiązanie** okna, potwierdzenie toodelete hello rozwiązania.
4.  Informacje hello jest weryfikowany i usunięciu hello rozwiązania, można śledzić postęp w obszarze **powiadomienia** hello menu.  Zostanie zwrócony toohello **VMManagementSolution [obszaru roboczego]** bloku, po uruchomieniu hello procesu tooremove rozwiązania.  

Konto automatyzacji Hello i obszarem roboczym pakietu OMS nie są usuwane w ramach tego procesu.  Jeśli nie chcesz, aby obszar roboczy OMS hello tooretain, konieczne będzie toomanually go usunąć.  Można to zrobić również z hello portalu Azure.   Z hello głównej ekranu w hello portalu Azure, wybierz **analizy dzienników** , a następnie na powitania **analizy dzienników** bloku, wybierz hello obszaru roboczego i kliknij przycisk **usunąć** z menu hello na Witaj blok ustawień obszaru roboczego.  
      
## <a name="next-steps"></a>Następne kroki

- Zobacz toolearn więcej informacji na temat sposobu tooconstruct różne zapytania i przejrzyj hello automatyzacji zadania dzienniki z analizy dzienników [Zaloguj wyszukiwania analizy dzienników](../log-analytics/log-analytics-log-searches.md)
- więcej informacji o wykonanie elementu runbook, w jaki sposób toomonitor zadań i inne szczegółowe informacje techniczne, zobacz toolearn [śledzić zadania elementu runbook](automation-runbook-execution.md)
- toolearn więcej informacji na temat analizy dzienników OMS i źródeł zbierania danych, zobacz [Azure zbierania danych magazynu w omówieniu analizy dzienników](../log-analytics/log-analytics-azure-storage.md)






   

