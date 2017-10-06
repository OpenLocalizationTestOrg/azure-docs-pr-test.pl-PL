---
title: 'Synchronizacja programu Azure AD Connect: Konfigurowanie filtrowania | Dokumentacja firmy Microsoft'
description: "Wyjaśniono, jak tooconfigure filtrowanie synchronizacji Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Synchronizacja programu Azure AD Connect: konfigurowanie filtrowania
Za pomocą filtrowania, można kontrolować obiekty, które są wyświetlane w usłudze Azure Active Directory (Azure AD) z katalogu lokalnego. Konfiguracja domyślna Hello przyjmuje wszystkie obiekty we wszystkich domenach w lasach hello skonfigurowane. Ogólnie rzecz biorąc jest to zalecana konfiguracja hello. Użytkowników przy użyciu usługi Office 365 obciążeń, takich jak Exchange Online i Skype dla firm, korzystać z pełną globalnej listy adresowej, wysyłać wiadomości e-mail i wywołać Wszyscy. W konfiguracji domyślnej hello zostałyby hello, które same występować, że mają oni z implementacją lokalnego programu Exchange lub Lync.

W niektórych przypadkach, jest wymagana konfiguracja domyślna toohello niektóre zmiany. Oto kilka przykładów:

* Planowanie toouse hello [wielu Azure AD directory topologii](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). Następnie należy tooapply toocontrol filtru, obiekty, które są synchronizowane tooa określonej usługi Azure AD directory.
* Uruchom projekt pilotażowy dla platformy Azure lub usługi Office 365 i mają tylko dla podzbioru użytkowników w usłudze Azure AD. W małych pilotażu hello nie jest ważna toohave pełną funkcjonalność hello toodemonstrate globalnej liście adresowej.
* Masz wiele kont usług i innych gromadzone kont, które nie mają w usłudze Azure AD.
* Ze względu na zgodność nie usuwaj żadnych użytkownika konta lokalnego. Możesz tylko je wyłączyć. Jednak w usłudze Azure AD mają tylko aktywne konta toobe obecny.

W tym artykule opisano, jak tooconfigure hello różnych metod filtrowania.

> [!IMPORTANT]
> Microsoft nie obsługuje modyfikowania lub działania synchronizacji Azure AD Connect poza hello akcje, które są udokumentowane formalnie. Te czynności może spowodować niespójne lub nieobsługiwany stan synchronizacji Azure AD Connect. W związku z tym Microsoft nie świadczy pomocy technicznej dla tych wdrożeń.

## <a name="basics-and-important-notes"></a>Podstawy i ważne uwagi
Synchronizacja programu Azure AD Connect można włączyć, filtrowanie, w dowolnym momencie. Jeśli rozpoczynać się od domyślnej konfiguracji synchronizacji katalogów, a następnie skonfigurować filtrowanie, hello obiektów, które są odfiltrowywane nie są zsynchronizowane tooAzure AD. Z powodu tej zmiany wszystkie obiekty w usłudze Azure AD, które wcześniej zostały zsynchronizowane, ale następnie zostały przefiltrowane są usuwane z usługi Azure AD.

Przed wprowadzeniem zmian toofiltering, upewnij się, że możesz [wyłączyć hello zaplanowane zadanie](#disable-scheduled-task) tak przypadkowo nie Eksportuj zmiany, że jeszcze nie zweryfikowano toobe poprawne.

Ponieważ wiele obiektów na powitania filtrowania może usunąć sam czas, ma toomake się nowe filtry są poprawne, przed rozpoczęciem eksportowania wszelkie zmiany tooAzure AD. Po ukończeniu czynności konfiguracyjnych hello, zdecydowanie zaleca się przestrzeganie hello [kroki weryfikacji](#apply-and-verify-changes) przed wyeksportować i wprowadzić zmiany tooAzure AD.

funkcji można usuwać wiele obiektów przypadkowo, hello tooprotect "[Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" jest domyślnie włączone. Jeśli usuniesz wiele obiektów, które powinny przejść toofiltering (domyślnie 500), należy toofollow hello kroków w tym hello tooallow artykułu usuwa toogo za pośrednictwem tooAzure AD.

Jeśli używasz kompilacji zanim listopad 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), Konfiguracja filtru tooa zmiany i korzystać z synchronizacji haseł, wówczas należy tootrigger pełnej synchronizacji haseł wszystkich po zakończeniu konfiguracji hello. Procedura w sposób tootrigger hasła pełnej synchronizacji, w sekcji [wyzwolenia pełnej synchronizacji haseł wszystkich](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Podczas kompilacji 1.0.9125 lub później, następnie hello regular **pełnej synchronizacji** akcji oblicza również, czy hasła powinny być synchronizowane, a jeśli ten dodatkowy krok nie jest już wymagane.

Jeśli **użytkownika** obiekty przypadkowo zostały usunięte w usłudze Azure AD z powodu błędu filtrowania, można ponownie utworzyć hello obiektów użytkowników w usłudze Azure AD przez usunięcie konfiguracji filtrowania. Następnie można ponownie zsynchronizuj swoje katalogi. Ta akcja przywraca hello użytkowników z Kosza hello w usłudze Azure AD. Jednak można cofnąć usunięcia innych obiektów. Na przykład jeśli przypadkowego usunięcia grupy zabezpieczeń i było używane tooACL zasobu, grupy hello i jego listy kontroli dostępu nie można odzyskać.

Azure AD Connect usuwa tylko obiekty, że raz uwzględniono toobe w zakresie. Jeśli te obiekty nie znajdują się w zakresie ma obiektów w usłudze Azure AD, które zostały utworzone przez inny aparat synchronizacji, dodawanie filtrowanie nie powoduje usunięcia ich. Na przykład jeśli rozpoczyna serwera narzędzia DirSync, na którym utworzyć pełną kopię całej katalogu w usłudze Azure AD i zainstalować nowy serwer synchronizacji Azure AD Connect równolegle z włączono od początku hello filtrowanie, Azure AD Connect nie powoduje usunięcia hello dodatkowe obiekty, które zostały utworzone przy użyciu narzędzia DirSync.

Witaj konfiguracji filtrowania jest zachowywana po instalacji lub uaktualnienia tooa nowszej wersji programu Azure AD Connect. To jest zawsze najlepsze praktyki tooverify, który hello konfiguracji nie został przypadkowo zmienić po zakończeniu uaktualnienia tooa nowszej wersji przed uruchomieniem pierwszego cyklu synchronizacji hello.

Jeśli masz więcej niż jednym lesie, a następnie należy zastosować hello filtrowania konfiguracje, które zostały opisane w tym temacie tooevery lesie (przy założeniu, że mają takie same hello konfiguracji dla wszystkich z nich).

### <a name="disable-hello-scheduled-task"></a>Wyłącz hello zaplanowanego zadania
toodisable hello wbudowanych harmonogramu, która wyzwala cykl synchronizacji co 30 minut, wykonaj następujące kroki:

1. Przejdź tooa wierszu polecenia programu PowerShell.
2. Uruchom `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable hello harmonogramu.
3. Zmiany hello opisane w tym artykule.
4. Uruchom `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable hello ponownie harmonogramu.

**Jeśli używasz usługi Azure AD Connect kompilacji przed 1.1.105.0**  
toodisable hello zaplanowane zadanie, które wyzwala cykl synchronizacji co trzy godziny, wykonaj następujące kroki:

1. Uruchom **harmonogram zadań** z hello **Start** menu.
2. Bezpośrednio pod **Biblioteka Harmonogramu zadań**, znajdowanie hello zadania o nazwie **Azure AD Sync Scheduler**, kliknij prawym przyciskiem myszy, a następnie wybierz **wyłączyć**.  
   ![Harmonogram zadań](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. Teraz można wprowadzić zmiany w konfiguracji i ręcznie uruchomić aparatu synchronizacji hello z hello **Menedżera usługi synchronizacji** konsoli.

Po zakończeniu wszystkich zmian filtrowania, nie zapomnij toocome Wstecz i **włączyć** hello zadanie ponownie.

## <a name="filtering-options"></a>Opcje filtrowania
Możesz zastosować powitania po filtrowania narzędzia synchronizacji katalogów toohello konfiguracji typy:

* [**Na podstawie grupy**](#group-based-filtering): filtrowanie oparte na pojedynczej grupy można skonfigurować tylko na początkowej instalacji za pomocą Kreatora instalacji hello.
* [**Oparte na domenie**](#domain-based-filtering): przy użyciu tej opcji, możesz wybrać domen zsynchronizować tooAzure AD. Można również dodawać i usuwać domeny z Konfiguracja aparatu synchronizacji hello, po wprowadzeniu zmian tooyour lokalnej infrastruktury po zainstalowaniu synchronizacja programu Azure AD Connect.
* [**Jednostka organizacyjna (OU) — na podstawie**](#organizational-unitbased-filtering): przy użyciu tej opcji, które jednostek organizacyjnych można wybrać synchronizacji tooAzure AD. Ta opcja jest dla wszystkich typów obiektów w wybranych jednostek organizacyjnych.
* [**Na podstawie atrybutów**](#attribute-based-filtering): przy użyciu tej opcji, możesz filtrować obiektów na podstawie wartości atrybutu hello obiektów. Można również mieć różnych filtrów do różnych typów obiektów.

Można używać wielu opcji filtrowania na powitania tym samym czasie. Na przykład można użyć filtrowanie na podstawie jednostki Organizacyjnej tooonly zawierają obiekty w jednej jednostce Organizacyjnej. At hello sam opartych na atrybutach filtrowania toofilter hello obiekty można użyć więcej czasu. Korzystając z wielu metod filtrowania, filtry hello używają logiczne "i" od hello filtrów.

## <a name="domain-based-filtering"></a>Filtrowanie oparte na domenie
Ta sekcja umożliwia tooconfigure kroki hello filtru domeny. Jeśli dodane lub usunięte domen w lesie, po zainstalowaniu usługi Azure AD Connect, należy również hello tooupdate konfiguracji filtrowania.

Witaj preferowany sposób filtrowanie oparte na domenie toochange jest uruchomiony Kreator instalacji hello i zmieniając [domeny i jednostki Organizacyjnej filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Kreator instalacji Hello automatyzuje wszystkich zadań hello, które są opisane w tym temacie.

Kroki te należy wykonać tylko, jeśli Kreator instalacji toorun hello jakiegoś powodu.

Oparte na domenie filtrowania Konfiguracja obejmuje następujące kroki:

1. [Wybierz domeny hello](#select-domains-to-be-synchronized) , które mają tooinclude hello synchronizacji.
2. Każdy dodawaniem i usuwaniem domeny, Dostosuj hello [profilów uruchamiania](#update-run-profiles).
3. [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>Wybierz hello domen toobe zsynchronizowane
domeny hello tooset filtrów, hello następujące kroki:

1. Zaloguj się toohello serwer z systemem synchronizacja programu Azure AD Connect przy użyciu konta należącego do hello **ADSyncAdmins** grupy zabezpieczeń.
2. Uruchom **usługi synchronizacji** z hello **Start** menu.
3. Wybierz **łączniki**i w hello **łączniki** wybierz hello łącznika z typem hello **usług domenowych w usłudze Active Directory**. W **akcje**, wybierz pozycję **właściwości**.  
   ![Właściwości łącznika](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Kliknij przycisk **Konfigurowanie partycji katalogu**.
5. W hello **Wybieranie partycji katalogu** listy, wybierz i usuń zaznaczenie domeny, zgodnie z potrzebami. Sprawdź, że wybrane są tylko partycje hello, które mają toosynchronize.  
   ![Partycje](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Jeśli została zmieniona infrastruktury lokalnej usługi Active Directory i dodać lub usunąć domen z lasu hello, kliknij przycisk hello **Odśwież** tooget przycisk zaktualizowanej listy. Podczas odświeżania, są wyświetlane pytanie o poświadczenia. Podaj wszystkie poświadczenia z tooWindows dostęp do odczytu serwera usługi Active Directory. Nie ma toobe hello użytkownika, który jest wypełniony hello — okno dialogowe.  
   ![Wymagane odświeżenie](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Gdy wszystko będzie gotowe, zamknij hello **właściwości** okno dialogowe, klikając **OK**. Usunięcie domen z lasu hello wyskakujących komunikat informuje, że domeny został usunięty i że konfiguracji zostaną wyczyszczone.
7. Kontynuować tooadjust hello [profilów uruchamiania](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Zaktualizować profile hello Uruchom
Jeśli użytkownik zaktualizował filtru domeny, należy również tooupdate hello Uruchom profilów.

1. W hello **łączniki** listy, upewnij się, że hello zaznaczono łącznik, który został zmodyfikowany w poprzednim kroku hello. W **akcje**, wybierz pozycję **Konfigurowanie profilów uruchamiania**.  
   ![Łącznik 1 profilów uruchamiania](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Znajdź i zidentyfikuj hello następujące profile:
    * Pełny Import
    * Pełna synchronizacja
    * Import zmian
    * Synchronizacja przyrostowa
    * Eksportowanie
3. Dla każdego profilu dostosować hello **dodane** i **usunięte** domen.
    1. Dla każdego z profilów hello pięciu hello następujące kroki dla każdego **dodane** domeny:
        1. Wybierz profil hello Uruchom, a następnie kliknij przycisk **nowy krok**.
        2. Na powitania **kroku skonfigurować** strony w hello **typu** menu rozwijanego hello wybierz typ kroku z hello sama nazwa jak hello profil, który jest konfigurowanie. Następnie kliknij przycisk **Next** (Dalej).  
        ![Łącznik 2 profilów uruchamiania](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Na powitania **konfiguracji łącznika** strony w hello **partycji** menu rozwijanego, wybierz hello nazwę domeny hello dodano tooyour domeny filtru.  
        ![Łącznik 3 profilów uruchamiania](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. Witaj tooclose **konfigurowania profilu uruchamiania** okna dialogowego, kliknij przycisk **Zakończ**.
    2. Dla każdego z profilów hello pięciu hello następujące kroki dla każdego **usunięte** domeny:
        1. Wybierz profil hello Uruchom.
        2. Jeśli hello **wartość** z hello **partycji** atrybutu jest identyfikatorem GUID, wybierz hello Uruchom krok i kliknij przycisk **usunąć krok**.  
        ![Łącznik 4 profilów uruchamiania](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Sprawdź zmiany. Każda domena, które mają toosynchronize powinien być wyświetlany jako etapem każdego profilu uruchamiania.
4. Witaj tooclose **Konfigurowanie profilów uruchamiania** okna dialogowego, kliknij przycisk **OK**.
5.  toocomplete hello konfiguracji, należy toorun **pełny import** i **synchronizacja różnicowa**. Kontynuuj czytanie sekcji hello [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Filtrowanie na podstawie jednostki organizacyjnej
Witaj preferowany sposób filtrowanie na podstawie jednostki Organizacyjnej toochange, uruchamiając Kreatora instalacji hello i zmieniając [domeny i jednostki Organizacyjnej filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Kreator instalacji Hello automatyzuje wszystkich zadań hello, które są opisane w tym temacie.

Kroki te należy wykonać tylko, jeśli Kreator instalacji toorun hello jakiegoś powodu.

tooconfigure organizacji na podstawie jednostki filtrowania, hello następujące kroki:

1. Zaloguj się toohello serwer z systemem synchronizacja programu Azure AD Connect przy użyciu konta należącego do hello **ADSyncAdmins** grupy zabezpieczeń.
2. Uruchom **usługi synchronizacji** z hello **Start** menu.
3. Wybierz **łączniki**i w hello **łączniki** wybierz hello łącznika z typem hello **usług domenowych w usłudze Active Directory**. W **akcje**, wybierz pozycję **właściwości**.  
   ![Właściwości łącznika](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Kliknij przycisk **Konfigurowanie partycji katalogu**, wybierz pozycję hello domeny mają tooconfigure, a następnie kliknij przycisk **kontenery**.
5. Po wyświetleniu monitu podaj wszystkie poświadczenia z dostępem do odczytu tooyour lokalnej usługi Active Directory. Nie ma toobe hello użytkownika, który jest wypełniony hello — okno dialogowe.
6. W hello **wybierz kontenery** okno dialogowe, wyczyść hello jednostek organizacyjnych, że nie ma toosynchronize z katalogiem w chmurze hello, a następnie kliknij przycisk **OK**.  
   ![Jednostki organizacyjne w hello — okno dialogowe Wybieranie kontenerów](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Witaj **komputery** kontenera należy wybrać dla toobe komputerów z systemem Windows 10 pomyślnie zsynchronizowano tooAzure AD. Jeśli komputery przyłączone do domeny znajdują się w innych jednostek organizacyjnych, upewnij się, że są wybrane.
   * Witaj **ForeignSecurityPrincipals** kontenera należy wybrać, jeśli masz wiele lasów z relacji zaufania. Ten kontener umożliwia toobe członkostwa grupy zabezpieczeń między lasami rozwiązane.
   * Witaj **RegisteredDevices** jednostki Organizacyjnej należy wybrać, jeśli włączono funkcję zapisywania zwrotnego urządzeń hello. Jeśli używasz innej funkcji zapisywania zwrotnego, takie jak zapisywanie zwrotne grup, upewnij się, że wybrane są następujące lokalizacje.
   * Wybierz inne OU, gdzie znajdują się użytkownicy, obiekty InetOrgPerson, grup, kontaktów i komputery. Na rysunku hello tych jednostek organizacyjnych znajdują się w hello ManagedObjects jednostki Organizacyjnej.
   * Jeśli używasz filtrowanie na podstawie grupy, hello jednostki Organizacyjnej, w której znajduje się grupa hello muszą być uwzględnione.
   * Należy pamiętać, że możesz określić, czy nowych jednostek organizacyjnych, które są dodawane po zakończeniu konfiguracji filtrowania hello są zsynchronizowane lub nie jest zsynchronizowany. Zobacz następną sekcję hello, aby uzyskać szczegółowe informacje.
7. Gdy wszystko będzie gotowe, zamknij hello **właściwości** okno dialogowe, klikając **OK**.
8. toocomplete hello konfiguracji, należy toorun **pełny import** i **synchronizacja różnicowa**. Kontynuuj czytanie sekcji hello [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Synchronizuj nowych jednostek organizacyjnych
Domyślnie są synchronizowane nowych jednostek organizacyjnych, które są tworzone po filtrowania został skonfigurowany. Ten stan jest wskazywany przez zaznaczenie pola wyboru. Możesz również usunąć zaznaczenie niektórych podkluczy jednostek organizacyjnych. tooget to zachowanie, kliknij pole hello, aż przyjmie postać białe niebieski znacznika wyboru (stanu domyślnego). Następnie usuń zaznaczenie wszystkich sub-jednostkach organizacyjnych użytkownik chce toosynchronize.

Jeśli wszystkie podrzędne jednostki organizacyjne są zsynchronizowane, pole hello jest białym znacznikiem wyboru niebieski.  
![Jednostki Organizacyjnej z wszystkich zaznaczonych bloków](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Jeśli niektóre podrzędne jednostki organizacyjne zostały usunięte, pole hello jest szary z białym znacznikiem wyboru.  
![Jednostki Organizacyjnej z niektórych sub-jednostek organizacyjnych niezaznaczony](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

W tej konfiguracji nowej jednostki Organizacyjnej, który został utworzony w obszarze ManagedObjects jest zsynchronizowany.

Kreator instalacji Hello Azure AD Connect tworzy zawsze tej konfiguracji.

### <a name="dont-synchronize-new-ous"></a>Nie Synchronizuj nowych jednostek organizacyjnych
Można skonfigurować synchronizacji hello toonot aparatu synchronizacji nowych jednostek organizacyjnych, po zakończeniu hello konfiguracji filtrowania. Ten stan jest wskazywany w hello interfejsu użytkownika przy wyświetlaniu kolor szary z zaznaczone pole hello. tooget to zachowanie, kliknij pole hello, aż przyjmie postać białe bez znacznika wyboru. Następnie wybierz hello sub-jednostek organizacyjnych, które mają toosynchronize.

![Jednostki Organizacyjnej z głównego hello niezaznaczony](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

W tej konfiguracji nowej jednostki Organizacyjnej, który został utworzony w obszarze ManagedObjects nie jest zsynchronizowany.

## <a name="attribute-based-filtering"></a>Filtrowanie na podstawie atrybutu
Upewnij się, że używasz hello listopad 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) lub nowszej kompilacji dla tych kroków toowork.

Filtrowanie na podstawie atrybutu jest hello najbardziej elastycznym toofilter obiektów. Korzystając z możliwości hello [aprowizacją deklaratywną](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol prawie każdego aspektu działania gdy obiekt jest synchronizowane tooAzure AD.

Możesz zastosować [przychodzących](#inbound-filtering) filtrowania z metaverse toohello usługi Active Directory, i [wychodzących](#outbound-filtering) filtrowania z hello metaverse tooAzure AD. Firma Microsoft zaleca stosowanie filtrowanie ruchu przychodzącego, ponieważ jest to najprostszy toomaintain hello. Należy używać tylko filtrowanie ruchu wychodzącego przed hello oceny można przeprowadzać toojoin obiektów z więcej niż jednym lesie są wymagane.

### <a name="inbound-filtering"></a>Liczba przychodzących filtrowania
Filtrowanie ruchu przychodzącego używa konfiguracji domyślnej hello, gdzie obiekty mają tooAzure AD musi mieć cloudFiltered atrybut metaverse hello Nieustawione toobe wartość tooa zsynchronizowane. Jeśli wartość tego atrybutu jest ustawiona zbyt**True**, a następnie hello obiektu nie jest zsynchronizowany. Nie należy ustawiać zbyt**False**, zgodnie z projektem. toomake się innymi regułami hello możliwości toocontribute wartość, ten atrybut jest tylko powinien wartości hello toohave **True** lub **NULL** (Brak).

W filtrowanie ruchu przychodzącego użyjesz możliwości hello **zakres** toodetermine, które obiekty toosynchronize lub Synchronizuj. To gdzie wprowadzeniu toofit dopasowania wymagań swojej organizacji. Moduł zakresu Hello ma **grupy** i **klauzuli** toodetermine, gdy reguła synchronizacji znajduje się w zakresie. Grupa zawiera jeden lub wiele klauzul. Brak logiczne "i" między wiele klauzul i logiczne "lub" między wiele grup.

Daj nam przyjrzeć się przykładem:  
![Zakres](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
To powinno zostać odczytany jako **(działu = IT) lub (działu = sprzedaży i c = US)**.

W hello następujące przykłady i kroki, obiekt użytkownika hello jest używany jako przykład, ale możesz użyć tej funkcji dla wszystkich typów obiektów.

W następujące przykłady hello wartość priorytetu hello rozpoczyna się od 50. Może być dowolna liczba nie jest używany, ale powinna być niższa niż 100.

#### <a name="negative-filtering-do-not-sync-these"></a>Filtrowanie ujemny: "synchronizuje je"
W hello poniższy przykład, można odfiltrować (Synchronizuj) wszystkich użytkowników gdzie **extensionAttribute15** ma wartość hello **NoSync**.

1. Zaloguj się toohello serwer z systemem synchronizacja programu Azure AD Connect przy użyciu konta należącego do hello **ADSyncAdmins** grupy zabezpieczeń.
2. Uruchom **Edytor reguł synchronizacji** z hello **Start** menu.
3. Upewnij się, że **przychodzący** jest zaznaczone, a następnie kliknij przycisk **Dodaj nową regułę**.
4. Nadaj nazwę opisową reguły hello takich jak "*w z usługi Active Directory — DoNotSyncFilter użytkownika*". Wybierz hello las poprawna, wybierz **użytkownika** jako hello **typu obiektu CS**i wybierz **osoby** jako hello **typu obiektu MV**. W **typu łącza**, wybierz pozycję **Join**. W **pierwszeństwo**wpisz wartość, która nie jest obecnie używany przez inną regułę synchronizacji (na przykład 50), a następnie kliknij przycisk **dalej**.  
   ![Opis elementu 1 dla ruchu przychodzącego](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. W **filtru Scoping**, kliknij przycisk **Dodaj grupę**i kliknij przycisk **Dodaj klauzulę**. W **atrybutu**, wybierz pozycję **ExtensionAttribute15**. Upewnij się, że **Operator** ustawiono zbyt**RÓWNY**i wpisz wartość hello **NoSync** w hello **wartość** pole. Kliknij przycisk **Dalej**.  
   ![Liczba przychodzących zakresu 2](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Pozostaw hello **Join** zasady pusty, a następnie kliknij przycisk **dalej**.
7. Kliknij przycisk **dodać przekształcania**, wybierz pozycję hello **dla przepływu** jako **stałej**i wybierz **cloudFiltered** jako hello  **Atrybut TARGET**. W hello **źródła** polu tekstowym **True**. Kliknij przycisk **Dodaj** toosave hello reguły.  
   ![Liczba przychodzących przekształcania 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. toocomplete hello konfiguracji, należy toorun **pełnej synchronizacji**. Kontynuuj czytanie sekcji hello [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filtrowanie dodatnią: "tylko synchronizować te"
Wyrażanie dodatnią filtrowania może być trudniejsze, ponieważ masz tooconsider obiektów, które nie są oczywiste toobe synchronizowane, takich jak sal konferencyjnych. Ma również będzie toooverride hello domyślnego filtru w regule out-of-box hello **w z usługi Active Directory — użytkownik przyłączyć**. Podczas tworzenia niestandardowego filtru, upewnij się, toonot obejmują krytycznego obiekty, obiekty konflikt replikacji specjalne skrzynek pocztowych i hello kont usług Azure AD Connect.

Opcja filtrowania dodatnią Hello wymaga dwie reguły synchronizacji. Należy z hello poprawny zakres obiektów toosynchronize jedną regułę (lub kilka). Należy również drugą regułę synchronizacji wychwytywania, który odfiltrowuje wszystkie obiekty, które nie zostały jeszcze zidentyfikowane jako obiekt, który powinien zostać zsynchronizowany.

W hello poniższy przykład, tylko synchronizować obiekty użytkownika, gdy atrybut działu hello ma wartość hello **sprzedaży**.

1. Zaloguj się toohello serwer z systemem synchronizacja programu Azure AD Connect przy użyciu konta należącego do hello **ADSyncAdmins** grupy zabezpieczeń.
2. Uruchom **Edytor reguł synchronizacji** z hello **Start** menu.
3. Upewnij się, że **przychodzący** jest zaznaczone, a następnie kliknij przycisk **Dodaj nową regułę**.
4. Nadaj nazwę opisową reguły hello takich jak "*w z usługi Active Directory — sprzedaży użytkownika synchronizacji*". Wybierz hello las poprawna, wybierz **użytkownika** jako hello **typu obiektu CS**i wybierz **osoby** jako hello **typu obiektu MV**. W **typu łącza**, wybierz pozycję **Join**. W **pierwszeństwo**wpisz wartość, która nie jest obecnie używany przez inną regułę synchronizacji (na przykład 51), a następnie kliknij przycisk **dalej**.  
   ![Opis elementu 4 przychodzące](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. W **filtru Scoping**, kliknij przycisk **Dodaj grupę**i kliknij przycisk **Dodaj klauzulę**. W **atrybutu**, wybierz pozycję **działu**. Upewnij się, że Operator ustawiono zbyt**RÓWNY**i wpisz wartość hello **sprzedaży** w hello **wartość** pole. Kliknij przycisk **Dalej**.  
   ![Liczba przychodzących zakres 5](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Pozostaw hello **Join** zasady pusty, a następnie kliknij przycisk **dalej**.
7. Kliknij przycisk **dodać przekształcania**, wybierz pozycję **stałej** jako hello **dla przepływu**i wybierz hello **cloudFiltered** jako hello  **Atrybut TARGET**. W hello **źródła** wpisz **False**. Kliknij przycisk **Dodaj** toosave hello reguły.  
   ![Liczba przychodzących przekształcania 6](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Jest to szczególnych przypadkach, w którym jawnie ustawić cloudFiltered zbyt**False**.
8. Reguła synchronizacji wychwytywania hello toocreate mamy teraz. Nadaj nazwę opisową reguły hello takich jak "*w z usługi Active Directory — filtr wychwytywania użytkownika*". Wybierz hello las poprawna, wybierz **użytkownika** jako hello **typu obiektu CS**i wybierz **osoby** jako hello **typu obiektu MV**. W **typu łącza**, wybierz pozycję **Join**. W **pierwszeństwo**, wpisz wartość, która nie jest obecnie używany przez inną regułę synchronizacji (na przykład 99). Wybrana wartość priorytetu (niższe pierwszeństwo) hello poprzednie reguły synchronizacji. Ale również zostały pozostawać niektóre miejsca, aby dodać więcej reguł filtrowania synchronizacji później należy toostart synchronizowanie dodatkowe działów. Kliknij przycisk **Dalej**.  
   ![Opis elementu 7 przychodzące](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Pozostaw **filtru Scoping** pusty, a następnie kliknij przycisk **dalej**. Pusty filtr wskazuje, że reguły hello jest stosowane toobe tooall obiektów.
10. Pozostaw hello **Join** zasady pusty, a następnie kliknij przycisk **dalej**.
11. Kliknij przycisk **dodać przekształcania**, wybierz pozycję **stałej** jako hello **dla przepływu**i wybierz **cloudFiltered** jako hello  **Atrybut TARGET**. W hello **źródła** wpisz **True**. Kliknij przycisk **Dodaj** toosave hello reguły.  
    ![Liczba przychodzących przekształcania 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. toocomplete hello konfiguracji, należy toorun **pełnej synchronizacji**. Kontynuuj czytanie sekcji hello [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

Jeśli zajdzie potrzeba, można utworzyć więcej reguł pierwszego typu hello dodanie więcej obiektów w hello synchronizacji.

### <a name="outbound-filtering"></a>Filtrowanie ruchu wychodzącego
W niektórych przypadkach jest konieczne toodo hello filtrowania dopiero po dołączeniu hello obiektów w magazynie metaverse hello. Na przykład można ją niezbędne toolook hello atrybut poczty z lasu zasobów hello i atrybut userPrincipalName hello z hello konta lasu, toodetermine, jeśli obiekt powinien zostać zsynchronizowany. W takich przypadkach możesz utworzyć hello filtrowanie hello wychodzącą regułę.

W tym przykładzie zmienisz hello filtrowania, tak aby tylko dla użytkowników, które mają zarówno ich poczty i userPrincipalName kończy się rozszerzeniem @contoso.com są synchronizowane:

1. Zaloguj się toohello serwer z systemem synchronizacja programu Azure AD Connect przy użyciu konta należącego do hello **ADSyncAdmins** grupy zabezpieczeń.
2. Uruchom **Edytor reguł synchronizacji** z hello **Start** menu.
3. W obszarze **typu reguły**, kliknij przycisk **wychodzące**.
4. Znajdź hello reguły o nazwie **się tooAAD — użytkownik przyłączyć**i kliknij przycisk **Edytuj**.
5. W oknie podręcznym hello odpowiedzi **tak** toocreate kopię hello reguły.
6. Na powitania **opis** Zmień **pierwszeństwo** tooan nieużywanych wartość, na przykład 50.
7. Kliknij przycisk **filtru Scoping** na hello nawigacji po lewej stronie, a następnie kliknij przycisk **Dodaj klauzulę**. W **atrybutu**, wybierz pozycję **poczty**. W **Operator**, wybierz pozycję **ENDSWITH**. W **wartość**, typ  **@contoso.com** , a następnie kliknij przycisk **Dodaj klauzulę**. W **atrybutu**, wybierz pozycję **userPrincipalName**. W **Operator**, wybierz pozycję **ENDSWITH**. W **wartość**, typ  **@contoso.com** .
8. Kliknij pozycję **Zapisz**.
9. toocomplete hello konfiguracji, należy toorun **pełnej synchronizacji**. Kontynuuj czytanie sekcji hello [Zastosuj i Sprawdź zmiany](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Zastosuj i Sprawdź zmiany
Po wprowadzeniu zmian w konfiguracji, należy najpierw zastosować je toohello obiektów, które już znajdują się w systemie hello. Można ją również hello obiektów, które nie są obecnie w aparacie synchronizacji hello powinna zostać przetworzona (i aparatu synchronizacji hello musi systemu źródłowego hello tooread ponownie tooverify jego zawartość).

Jeśli zmieniono konfigurację hello przy użyciu **domeny** lub **jednostki organizacyjnej** filtrowania, a następnie należy toodo **pełny import**, a następnie **Delta Synchronizacja**.

Jeśli zmieniono konfigurację hello przy użyciu **atrybutu** filtrowania, a następnie należy toodo **pełnej synchronizacji**.

Witaj następujące kroki:

1. Uruchom **usługi synchronizacji** z hello **Start** menu.
2. Wybierz **łączniki**. W hello **łączniki** wybierz hello łącznika, w którym wprowadzono zmiany wcześniejszej konfiguracji. W **akcje**, wybierz pozycję **Uruchom**.  
   ![Uruchom łącznika](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. W **profilów uruchamiania**, wybierz operację hello wspomniano w poprzedniej sekcji hello. Należy toorun dwie akcje wykonywania hello drugi po hello pierwsza z nich zostało zakończone. (hello **stanu** kolumna jest **bezczynny** hello wybrane łącznika.)

Po synchronizacji hello wszystkie zmiany są przemieszczane toobe wyeksportowane. Przed wprowadzeniem zmian hello faktycznie w usłudze Azure AD, ma tooverify, czy te zmiany są poprawne.

1. Uruchom wiersz polecenia i przejdź zbyt`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Uruchom polecenie `csexport "Name of Connector" %temp%\export.xml /f:x`.  
   Nazwa Hello hello łącznika jest usługi synchronizacji. Ma ona nazwę too"contoso.com podobne — AAD" dla usługi Azure AD.
3. Uruchom polecenie `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`.
4. Istnieje już plik o nazwie export.csv, która może być zbadana w programie Microsoft Excel % temp %. Ten plik zawiera wszystkie zmiany hello, które są o toobe wyeksportowane.
5. Wprowadzić konieczne zmiany hello toohello danych lub konfiguracji, a następnie uruchom te kroki ponownie (importowania, synchronizowania i sprawdź, czy) do momentu hello zmiany, które są o toobe eksportowane są oczekiwań.

Po zakończeniu, wyeksportuj hello zmiany tooAzure AD.

1. Wybierz **łączniki**. W hello **łączniki** wybierz hello łącznika usługi Azure AD. W **akcje**, wybierz pozycję **Uruchom**.
2. W **profilów uruchamiania**, wybierz pozycję **wyeksportować**.
3. Jeśli zmiany w konfiguracji usuwają wiele obiektów, następnie zostanie wyświetlony błąd w pliku eksportu hello gdy numer hello jest większy niż próg hello skonfigurowane (domyślnie 500). Jeśli zostanie wyświetlony ten błąd, a następnie należy hello Wyłącz tootemporarily "[Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" funkcji.

Teraz nadszedł czas tooenable hello harmonogramu ponownie.

1. Uruchom **harmonogram zadań** z hello **Start** menu.
2. Bezpośrednio pod **Biblioteka Harmonogramu zadań**, znajdowanie hello zadania o nazwie **Azure AD Sync Scheduler**, kliknij prawym przyciskiem myszy, a następnie wybierz **włączyć**.

## <a name="group-based-filtering"></a>Filtrowanie na podstawie grupy
Można skonfigurować na podstawie grupy filtrowania hello pierwszej instalacji Azure AD Connect przy użyciu [instalacji niestandardowej](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). Jego przeznaczonych do wdrożenia pilotażowego, w którym ma niewielki zestaw obiektów toobe synchronizowane. Po wyłączeniu filtrowanie na podstawie grupy, nie można włączyć ponownie. Ma ona *nieobsługiwane* toouse oparte na grupach filtrowanie w konfiguracji niestandardowej. Go jest obsługiwane tylko tooconfigure tej funkcji za pomocą Kreatora instalacji hello. Po zakończeniu pracy programu pilotażowego, następnie użyj jednej z hello inne opcje filtrowania w tym temacie. Korzystając z filtrowanie oparte na jednostce Organizacyjnej w połączeniu z filtrowanie na podstawie grupy, hello jednostką organizacyjną, w którym znajdują się hello grupy i jej elementów członkowskich należy dołączyć.

Podczas synchronizowania wiele lasów usługi AD, można skonfigurować filtrowanie na podstawie grupy, określając inną grupę przez każdy łącznik AD. Jeśli chcesz toosynchronize użytkownika w jednym lesie usługi AD i hello tego samego użytkownika zawiera co najmniej bardziej odpowiednie FSP (obcego podmiotu zabezpieczeń) obiektów w innych lasach AD, musisz zapewnić hello obiektu użytkownika i wszystkie odpowiednie obiekty FSP należą na podstawie grupy Filtrowanie zakresu. Jeśli co najmniej jeden z obiektów FSP hello są wyłączone przez filtrowanie na podstawie grupy, obiekt użytkownika hello nie będą synchronizowane tooAzure AD.

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.
- Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure AD](active-directory-aadconnect.md).
