---
title: 'Synchronizacja programu Azure AD Connect: Konfiguracja synchronizacji Azure AD Connect | Dokumentacja firmy Microsoft'
description: "Przedstawiono sposób toomake Konfiguracja toohello zmiany w programie Azure AD Connect synchronizacji."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Synchronizacja programu Azure AD Connect: jak toomake toohello zmiany domyślną konfigurację
Celem tego tematu Hello jest toowalk przez jak toomake zmienia toohello domyślnej konfiguracji synchronizacji Azure AD Connect. Ona instrukcje dla niektórych typowych scenariuszy. Z wiedzy powinno być możliwe toomake tooyour niektórych prostych zmian własnej konfiguracji na podstawie własnych reguł biznesowych.

## <a name="synchronization-rules-editor"></a>Edytor reguł synchronizacji
Edytor reguł synchronizacji Hello jest używany toosee i zmień hello domyślna konfiguracja. Można go znaleźć w hello Start Menu w obszarze hello **Azure AD Connect** grupy.  
![Edytor reguł synchronizacji z Menu Start](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Po otwarciu, zostanie wyświetlony hello domyślnych out-of-box reguł.

![Edytor reguł synchronizacji](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Nawigacja w edytorze hello
Hello listy rozwijane u góry hello edytora hello pozwalają tooquickly znaleźć określonej reguły. Na przykład jeśli chcesz toosee hello reguły, których proxyAddresses atrybutu hello jest dołączony zmienić hello listach rozwijanych toohello następujące:  
![Filtrowanie SRE](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
Filtrowanie tooreset i obciążenia nową konfigurację, naciśnij klawisz **F5** hello klawiatury.

toohello w prawym górnym narożniku, znajduje się przycisk **Dodaj nową regułę**. Ten przycisk jest używane toocreate reguły niestandardowe.

U dołu hello masz przycisków dla działania w regule wybranego synchronizacji. **Edytuj** i **usunąć** oczekiwaniami ich. **Eksportuj** tworzy skrypt programu PowerShell do odtworzenia hello reguły synchronizacji. Ta procedura umożliwia toomove reguły synchronizacji z jednego serwera tooanother.

## <a name="create-your-first-custom-rule"></a>Tworzenie pierwszej reguły niestandardowe
Zmiana najczęściej Hello jest przepływów atrybutów toohello zmiany. Hello danych w katalogu źródłowym nie może być tak jak Azure AD. Przykład Witaj w tej sekcji, ma toomake się hello podanej nazwy użytkownika jest zawsze w **przypadku prawidłowego**.

### <a name="disable-hello-scheduler"></a>Wyłączanie harmonogramu hello
Witaj [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md) domyślnie uruchamiane co 30 minut. Ma toomake się, że nie jest uruchomiona podczas wprowadzania zmian i rozwiązywanie problemów z nowych zasad. Wyłączanie harmonogramu hello tootemporarily, uruchom program PowerShell i uruchom`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Wyłączanie harmonogramu hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Tworzenie reguły hello
1. Kliknij przycisk **Dodaj nową regułę**.
2. Na powitania **opis** strony wprowadź następujące hello:  
   ![Liczba przychodzących reguł filtrowania](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Name: Udostępnij reguły hello opisową nazwę.
   * Opis: Niektóre wyjaśnienie, ktoś inny może zrozumieć, jakie reguły hello jest.
   * Połączony system: hello systemu hello obiektu można znaleźć w. W takim przypadku wybierz hello łącznika usługi Active Directory.
   * Typ obiektu połączony System/Metaverse: Wybierz **użytkownika** i **osoby** odpowiednio.
   * Typ łącza: Zmień tę wartość za**Join**.
   * Pierwszeństwo: Podaj wartość, która jest unikatowa w systemie hello. Niższa wartość liczbowa oznacza wyższy priorytet.
   * Tag: Może pozostać puste. Tylko reguły out-of-box firmy Microsoft powinna mieć to pole wypełniane przy użyciu wartości.
3. Na powitania **filtru Scoping** wprowadź **givenName ISNOTNULL**.  
   ![Reguła filtr zakresów ruchu przychodzącego](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Ta sekcja jest używane toodefine reguły hello obiektów, które dotyczą. Jeśli pole pozostanie puste, hello reguły będą miały zastosowania tooall obiekty użytkownika. Ale obejmowałoby sal konferencyjnych, kont usług i innych obiektów użytkownika z systemem innym niż osób.
4. Na powitania **dołączyć reguły**, pozostaw puste.
5. Na powitania **przekształcenia** zbyt Zmień powitania dla przepływu**wyrażenia**. Wybierz hello atrybut Target **givenName**, a w źródle wprowadź `PCase([givenName])`.
   ![Reguła ruchu przychodzącego przekształcenia](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   Aparat synchronizacji Hello jest rozróżniana wielkość liter, zarówno na powitania funkcja nazwy i nazwy hello hello atrybutu. Jeśli wpiszesz problem, zobacz ostrzeżenie podczas dodawania hello reguły. Edytor Hello pozwala toosave i kontynuować, dlatego trzeba tooreopen hello regułę i poprawne hello regułę.
6. Kliknij przycisk **Dodaj** toosave hello reguły.

Nowe reguły niestandardowe powinny być widoczne z hello innych synchronizacji w systemie hello reguły.

### <a name="verify-hello-change"></a>Sprawdź zmiany hello
Dzięki tej zmianie nowego ma toomake się, że działa zgodnie z oczekiwaniami i nie jest zgłaszanie błędów. W zależności od hello liczbę obiektów, do których masz istnieją dwa różne sposoby toodo ten krok.

1. Uruchom pełną synchronizację wszystkich obiektów
2. Uruchom Podgląd i pełną synchronizację dla pojedynczego obiektu

Uruchom **usługi synchronizacji** z hello start menu. kroki Hello w tej sekcji są w tego narzędzia.

1. **Pełna synchronizacja wszystkich obiektów**  
   Wybierz **łączniki** u góry hello. Zidentyfikuj hello łącznika wprowadzone zmiany tooin hello poprzedniej sekcji, w tym przypadku hello usług domenowych w usłudze Active Directory i zaznacz go. Wybierz **Uruchom** z działań i wybierz **pełną synchronizację** i **OK**.
   ![Pełna synchronizacja](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   obiekty Hello teraz są aktualizowane w magazynie metaverse hello. Teraz należy toolook obiektu hello w magazynie metaverse hello.
2. **Podgląd i pełną synchronizację dla pojedynczego obiektu**  
   Wybierz **łączniki** u góry hello. Zidentyfikuj hello łącznika wprowadzone zmiany tooin hello poprzedniej sekcji, w tym przypadku hello usług domenowych w usłudze Active Directory i zaznacz go. Wybierz **wyszukiwania przestrzeni łącznika**. Użyj toofind zakres obiektu mają toouse tootest hello zmiany. Wybierz obiekt hello, a następnie kliknij przycisk **Podgląd**. W nowym ekranie powitania wybierz **zatwierdzić Podgląd**.  
   ![Zatwierdź podglądu](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   Zmiana Hello jest teraz metaverse toohello zatwierdzone.

**Przyjrzyj się hello obiektu hello metaverse**  
Teraz należy toopick kilka przykładowych obiektów toomake czy hello Oczekiwano wartości i reguły hello zastosowane. Wybierz **wyszukiwanie Metaverse** od góry hello. Dodaj dowolny filtr, który należy toofind hello odpowiednich obiektów. W wyniku wyszukiwania hello Otwórz obiektu. Spójrz na powitania wartości atrybutów i również sprawdzić w hello **reguły synchronizacji** kolumny, która hello reguły stosowane zgodnie z oczekiwaniami.  
![Wyszukiwanie magazynu metaverse](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Włącz hello harmonogramu
Jeśli wszystko, co jest zgodne z oczekiwaniami, możesz włączyć ponownie hello harmonogramu. Z programu PowerShell, uruchom `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Inne typowe zmiany przepływu atrybutów
Hello poprzedniej sekcji opisano, jak toomake zmienia tooan przepływ atrybutów. W tej sekcji znajdują się dodatkowe przykłady. kroki Hello jak reguły synchronizacji hello toocreate jest skrócona, ale można znaleźć kroki pełne hello w poprzedniej sekcji hello.

### <a name="use-another-attribute-than-hello-default"></a>Użyj atrybutu innego niż domyślny hello
W firmie Fabrikam Brak lasu, gdy jest używany alfabetu lokalne powitania imię, nazwisko i nazwę wyświetlaną. Witaj zestaw znaków łacińskich reprezentację te atrybuty znajdują się w hello atrybuty rozszerzenia. Podczas kompilowania hello globalnej listy adresowej w usłudze Azure AD i Office 365, hello organizacja chce toobe tych atrybutów, zamiast tego użyć.

Z konfiguracji domyślnej obiekt z lasu lokalne powitania wygląda następująco:  
![Przepływ atrybutów 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

toocreate reguły z innych przepływów atrybutów hello następujące:

* Uruchom **Synchronization Rule Editor** z hello start menu.
* Z **przychodzący** toohello nadal wybrany w lewo, kliknij przycisk hello **Dodaj nową regułę**.
* Reguła hello należy podać nazwę i opis. Wybierz hello lokalnej usługi Active Directory i hello odpowiednich typów obiektów. W **typu łącza**, wybierz pozycję **Join**. Pierwszeństwa wybierz numer, który nie jest używany przez inną regułę. reguły out-of-box Hello rozpoczyna się od 100, dlatego wartość hello 50 może być używana w tym przykładzie.
  ![Przepływ atrybutu 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Pozostaw puste zakresu (to znaczy stosuje tooall obiektów użytkownika w lesie hello).
* Pozostaw puste zasady sprzężenia, (umożliwiających hello dojścia reguły out-of-box wszelkie sprzężenia).
* W przekształcenia Utwórz powitania po przepływów:  
  ![Przepływ atrybutu 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Kliknij przycisk **Dodaj** toosave hello reguły.
* Przejdź za**Menedżera usługi synchronizacji**. Na **łączniki**, wybierz hello łącznika, gdzie dodaliśmy hello reguły. Wybierz **Uruchom**, i **pełnej synchronizacji**. Pełna synchronizacja ponownie oblicza wszystkie obiekty przy użyciu hello bieżące reguły.

Jest to wynik hello hello sam obiekt z tej zasady niestandardowej:  
![Przepływ atrybutu 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Długość atrybutów
Atrybuty ciągu są przez domyślny zestaw toobe można indeksować i hello maksymalna długość to 448 znaków. Podczas pracy z atrybutami ciągów, które mogą zawierać więcej, upewnij się, że tooinclude hello następujące przepływu atrybutu hello:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Zmiana hello userPrincipalSuffix
Atrybut userPrincipalName Hello w usłudze Active Directory nie jest zawsze znane hello użytkowników i mogą nie być odpowiednie, jak hello identyfikator logowania. Hello Azure AD Connect, Kreator instalacji usługi synchronizacji umożliwia pobranie inny atrybut, na przykład poczty. Jednak w niektórych przypadkach hello atrybutu muszą zostać obliczone. Na przykład hello firmy Contoso ma dwa katalogi usługi Azure AD, co w środowisku produkcyjnym i jeden do testowania. Chcę hello użytkowników w ich test dzierżawy toouse innego sufiksu hello identyfikator logowania.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

W tym wyrażeniu wykonaj wszystkie elementy w lewo z hello najpierw @-sign (Word) i ZŁĄCZ.teksty z ciągiem stałym.

### <a name="convert-a-multi-value-tooa-single-value"></a>Konwertuj tooa wielowartościowych pojedynczą wartość
Niektóre atrybuty w usłudze Active Directory są wielowartościowe w schemacie hello, mimo że wyglądają jednej wartości w użytkownicy usługi Active Directory i komputery. Przykładem jest hello opis atrybutu.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

W tym wyrażenia w przypadku, gdy atrybut hello ma wartość, wykonać hello pierwszego elementu (element) w atrybucie hello usunięcia spacji wiodących i końcowych spacji (Trim), a następnie zachować hello najpierw 448 znaków (po lewej) ciąg hello.

### <a name="do-not-flow-an-attribute"></a>Nie przepływu atrybutu
W tle na powitania scenariusz dla tej sekcji, zobacz [kontrolować proces przepływu atrybutu hello](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Istnieją dwa sposoby toonot przepływu atrybutu. najpierw Hello jest dostępna w Kreatorze instalacji hello i pozwala zbyt[Usuń wybranych atrybutów](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Ta opcja działa, jeśli atrybut hello przed nigdy nie zostały zsynchronizowane. Jednak jeśli rozpoczęto toosynchronize ten atrybut i później usunąć go z tą funkcją, następnie aparatu synchronizacji hello zatrzymuje zarządzanie hello atrybutu i istniejące wartości hello pozostaną w usłudze Azure AD.

Jeśli tooremove hello wartość atrybutu i upewnij się, że nie wpływają hello w przyszłości, należy zamiast tego Utwórz regułę niestandardową.

W firmie Fabrikam mieć uświadomiliśmy sobie, że niektóre atrybuty możemy zsynchronizować toohello chmury powitalne nie będą już istnieje. Chcemy toomake się, że te atrybuty są usuwane z usługi Azure AD.  
![Złe rozszerzenie atrybutów](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Utwórz nową regułę synchronizacji ruchu przychodzącego i wypełnić opis hello ![opisów](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Tworzenie przepływów atrybutów typu **wyrażenie** i ze źródłem hello **AuthoritativeNull**. Witaj literału **AuthoritativeNull** wskazuje, że wartość hello powinna być pusta w hello MV, nawet jeśli niższy priorytet reguły synchronizacji próbuje toopopulate hello wartość.
  ![Przekształcania atrybuty rozszerzenia](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Zapisz hello reguły synchronizacji. Uruchom **usługi synchronizacji**, Znajdź hello łącznik, wybierz **Uruchom**, i **pełnej synchronizacji**. Ten krok ponownie oblicza wszystkie przepływy atrybutów.
* Sprawdź, czy tego hello przeznaczone są zmiany dotyczące toobe wyeksportowane przez wyszukiwanie hello przestrzeni łącznika.
  ![Usuń przemieszczanego](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Tworzenie reguł przy użyciu programu PowerShell
Za pomocą edytora reguły synchronizacji hello działa prawidłowo, jeśli masz tylko kilka toomake zmiany. Jeśli potrzebujesz toomake dużej liczby zmian, programu PowerShell może być lepszym rozwiązaniem. Niektóre zaawansowane funkcje są dostępne tylko przy użyciu programu PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Pobierz skrypt programu PowerShell hello reguły out-of-box
toosee hello skrypt programu PowerShell, utworzony out-of-box regułę, wybierz hello reguły synchronizacji hello zasady edytora i kliknij przycisk **wyeksportować**. Dzięki temu akcji hello PowerShell skryptu hello utworzonej reguły.

### <a name="advanced-precedence"></a>Pierwszeństwo zaawansowane
reguły synchronizacji out-of-box Hello rozpoczynać się od wartości pierwszeństwo 100. Jeśli masz wiele lasów należy toomake wiele niestandardowych zmiany, a następnie reguły synchronizacji 99 może nie być wystarczającej ilości.

Możesz wydać hello aparatu synchronizacji, która ma dodatkowe zasady wstawiony przed regułami out-of-box hello. tooget to zachowanie, wykonaj następujące kroki:

1. Oznacz hello pierwszej reguły synchronizacji out-of-box (ta reguła jest hello **w od użytkownika AD Join**) Edytor reguł synchronizacji hello i wybierz **wyeksportować**. Skopiuj wartość identyfikatora SR hello.  
![PowerShell przed zmianą](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Utwórz nową regułę synchronizacji hello. Można użyć toocreate Edytor reguł synchronizacji hello go. Wyeksportować skrypt programu PowerShell tooa reguły hello.
3. We właściwości hello **PrecedenceBefore**, Wstaw wartość identyfikatora hello z hello out-of-box reguły. Zestaw hello **pierwszeństwo** za**0**. Upewnij się, hello identyfikator atrybutu jest unikatowy i identyfikator GUID z inną regułą nie ponownego użycia. Upewnij się również, że hello **ImmutableTag** nie ustawiono właściwości; tej właściwości można ustawić tylko dla reguły out-of-box. Zapisz skrypt programu PowerShell hello i uruchom go. wynik Hello jest niestandardowe reguły jest przypisywana wartość priorytetu hello 100, a wszystkie inne zasady out-of-box jest zwiększany.  
![PowerShell po zmianie](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

Może mieć wiele reguł synchronizacji niestandardowych za pomocą hello sam **PrecedenceBefore** wartości w razie potrzeby.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Włącz synchronizację PreferredDataLocation
Azure AD Connect obsługuje synchronizacji hello **PreferredDataLocation** atrybutu dla **użytkownika** obiektów w wersji 1.1.524.0 i po. W szczególności wprowadzono następujące zmiany:

* Schemat Hello typu obiektu hello **użytkownika** w hello łącznika usługi Azure AD jest rozszerzony tooinclude PreferredDataLocation atrybut, który jest typu string i jest pojedynczej wartości.

* Schemat Hello typu obiektu hello **osoby** w hello Metaverse jest rozszerzony tooinclude PreferredDataLocation atrybut, który jest typu string i jest pojedynczej wartości.

Domyślnie atrybut PreferredDataLocation hello nie włączono synchronizacji ponieważ nie ma odpowiedniego atrybutu PreferredDataLocation w lokalnej usłudze Active Directory. Musisz ręcznie włączyć synchronizację.

> [!IMPORTANT]
> Obecnie usługi Azure AD umożliwia atrybutu PreferredDataLocation hello zarówno synchronizowanych obiektów użytkowników i w chmurze toobe obiekty użytkownika bezpośrednio skonfigurowany przy użyciu programu Azure AD PowerShell. Po włączeniu synchronizacji atrybutów PreferredDataLocation hello, musisz zatrzymać przy użyciu programu Azure AD PowerShell tooconfigure hello atrybutu na **synchronizowane obiekty użytkownika** jako Azure AD Connect zostaną one zastąpione na podstawie wartości atrybutów źródła Hello w lokalnej usłudze Active Directory.

> [!IMPORTANT]
> Na 1 września 2017 r, Azure AD będzie już miało możliwości atrybutu PreferredDataLocation hello na **synchronizowane obiekty użytkownika** toobe bezpośrednio skonfigurowany przy użyciu programu Azure AD PowerShell. Atrybut PreferredLocation tooconfigure synchronizowane obiekty użytkownika, należy użyć Azure tylko AD Connect.

Przed włączeniem synchronizacji atrybutu PreferredDataLocation hello, musisz:

 * Najpierw zdecyduj, które toobe lokalnej usługi Active Directory atrybutu używany jako atrybut źródłowy hello. Powinien być typu **ciąg** i **jednowartościowych**.

 * Atrybut PreferredDataLocation hello zostały wcześniej skonfigurowane na istniejące synchronizowane obiekty użytkownika w usłudze Azure AD przy użyciu programu PowerShell usługi Azure AD, należy **Poprawka usterki systemu** atrybutu hello wartości toohello odpowiednie obiekty użytkownika w usłudze Active Directory lokalnymi.
 
    > [!IMPORTANT]
    > Jeśli to zrobisz, nie Poprawka usterki systemu hello atrybut wartości toohello odpowiednie obiekty użytkownika w lokalnej usłudze Active Directory, Azure AD Connect spowoduje usunięcie istniejącej wartości atrybutów hello w usłudze Azure AD po synchronizacji dla atrybutu PreferredDataLocation hello włączone.

 * Zaleca się konfigurowanie atrybut źródłowy hello na co najmniej kilka lokalnych użytkowników usługi AD obiekty, które mogą służyć do weryfikacji później.
 
Hello kroki tooenable synchronizacji atrybutu PreferredDataLocation hello można podsumować jako:

1. Wyłączanie harmonogramu synchronizacji i sprawdź, że nie ma synchronizacji w toku

2. Dodaj toohello atrybut źródła hello AD łącznika lokalnego schematu

3. Dodaj PreferredDataLocation toohello łącznika usługi Azure AD schematu

4. Utwórz wartość atrybutu hello tooflow reguła synchronizacji ruchu przychodzącego z lokalnej usługi Active Directory

5. Utwórz synchronizacji ruchu wychodzącego reguły tooflow hello atrybutu wartość tooAzure AD

6. Uruchom pełną synchronizację cyklu

7. Włącz harmonogram synchronizacji

> [!NOTE]
> Hello pozostałej części tej sekcji omówiono następujące kroki w szczegółach. Zostały one opisane w kontekście hello wdrożenia usługi Azure AD z topologii z jednym lasem i bez reguły synchronizacji niestandardowych. Jeśli topologią wielu lasów, reguły synchronizacji niestandardowych skonfigurowane lub tymczasowej serwer, należy odpowiednio tooadjust hello kroki.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Krok 1: Wyłącz harmonogramu synchronizacji i sprawdź, że nie ma synchronizacji w toku
Upewnij się, synchronizacja nie ma miejsce podczas pracy w środku hello aktualizowanie synchronizacji tooavoid reguły niezamierzone zmiany jest eksportowane tooAzure AD. Harmonogram synchronizacji wbudowanych hello toodisable:

 1. Uruchom sesję programu PowerShell na powitania serwera Azure AD Connect.

 2. Wyłącz zaplanowanej synchronizacji, uruchamiając polecenie cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Uruchom hello **Menedżera usługi synchronizacji** przez przejście → tooSTART usługi synchronizacji.
 
 4. Przejdź toohello **operacji** karcie i upewnij się, Brak operacji ze stanem *"w"toku.*

![Menedżera usługi synchronizacji — Sprawdź żadnych operacji w toku](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Krok 2: Dodawanie toohello atrybut źródła hello AD łącznika lokalnego schematu
Nie wszystkie atrybuty AD są importowane do hello lokalnej przestrzeni łącznika usługi AD. tooadd hello źródła toohello listy atrybutów hello zaimportowane atrybuty:

 1. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.
 
 2. Kliknij prawym przyciskiem myszy na powitania **lokalnego łącznika AD** i wybierz **właściwości**.
 
 3. W wyskakującym oknie dialogowym hello Przejdź toohello **wybierz atrybuty** kartę.
 
 4. Upewnij się, że atrybut źródłowy hello jest zaznaczona na liście atrybutów hello.
 
 5. Kliknij przycisk **OK** toosave.

![Dodaj lokalne tooon atrybut źródła schematu w łączniku AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Krok 3: Dodawanie PreferredDataLocation toohello łącznika usługi Azure AD schematu
Domyślnie program hello PreferredDataLocation atrybut nie jest importowany do hello Azure AD Connect miejsca. tooadd hello PreferredDataLocation atrybutu toohello listę importowanych atrybutów:

 1. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.

 2. Kliknij prawym przyciskiem myszy na powitania **łącznika usługi Azure AD** i wybierz **właściwości**.

 3. W wyskakującym oknie dialogowym hello Przejdź toohello **wybierz atrybuty** kartę.

 4. Upewnij się, że atrybut PreferredDataLocation hello jest zaznaczona na liście atrybutów hello.

 5. Kliknij przycisk **OK** toosave.

![Dodawanie źródła tooAzure atrybut schematu łącznika AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Krok 4: Tworzenie wartości atrybutu hello tooflow reguła synchronizacji ruchu przychodzącego z lokalnej usługi Active Directory
Reguła synchronizacji ruchu przychodzącego Hello umożliwia tooflow wartość atrybutu hello z atrybutem źródłowym hello z lokalnej usługi Active Directory toohello Metaverse:

1. Uruchom hello **Edytor reguł synchronizacji** przez przejście → tooSTART synchronizacji zasady edytora.

2. Filtr wyszukiwania zestawu hello **kierunek** toobe **przychodzący**.

3. Kliknij przycisk **Dodaj nową regułę** toocreate przycisk nowej reguły przychodzącej.

4. W obszarze hello **opis** karcie, podaj hello następującej konfiguracji:
 
    | Atrybut | Wartość | Szczegóły |
    | --- | --- | --- |
    | Nazwa | *Podaj nazwę* | Na przykład *"w z usługi Active Directory — PreferredDataLocation użytkownika"* |
    | Opis | *Podaj opis* |  |
    | System połączony | *Wybierz lokalne powitania łączniku AD* |  |
    | Połączony System typu obiektu | **Użytkownika** |  |
    | Typ obiektu Metaverse | **Osoby** |  |
    | Typ łącza | **Dołącz** |  |
    | Priorytet | *Wybierz liczbę z zakresu od 1 – 99* | 1 – 99 jest zarezerwowana dla reguły synchronizacji niestandardowych. Odbiera wartość, która jest używana przez inną regułę synchronizacji. |

5. Przejdź toohello **filtru Scoping** karta i Dodaj **pojedynczego grupę ustalania zakresu filtru z powitania po klauzuli**:
 
    | Atrybut | Operator | Wartość |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Użytkownika\_ | 
 
    Filtr zakresu określa, które lokalna Usługa AD obiekty ta reguła synchronizacji ruchu przychodzącego. W tym przykładzie używamy hello użyć tego samego zakresu filtru jako *"w z usługi Active Directory — typowe użytkownika"* OOB reguły synchronizacji, która uniemożliwia reguły synchronizacji hello stosowane tooUser obiektów utworzonych za pomocą zapisu zwrotnego użytkowników usługi AD platformy Azure Funkcja. Może być konieczne tootweak hello zakresu filtru zgodnie z tooyour wdrożenia usługi Azure AD Connect.

6. Przejdź toohello **tab przekształcenia** i wdrożenie hello następujące reguły przekształcania:
 
    | Typ przepływu | Atrybut TARGET | Element źródłowy | Zastosuj raz | Scal typu |
    | --- | --- | --- | --- | --- |
    | Bezpośrednie | PreferredDataLocation | Wybierz atrybut źródłowy hello | Unchecked | Aktualizacja |

7. Kliknij przycisk **Dodaj** toocreate hello regułę dla ruchu przychodzącego.

![Utwórz regułę synchronizacji ruchu przychodzącego](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Krok 5: Tworzenie synchronizacji ruchu wychodzącego reguły tooflow hello atrybutu wartość tooAzure AD
Reguła synchronizacji ruchu wychodzącego Hello umożliwia tooflow wartość atrybutu hello z hello Metaverse toohello PreferredDataLocation atrybutu w usłudze Azure AD:

1. Przejdź toohello **reguły synchronizacji** edytora.

2. Filtr wyszukiwania zestawu hello **kierunek** toobe **wychodzące**.

3. Kliknij przycisk **Dodaj nową regułę** przycisku.

4. W obszarze hello **opis** karcie, podaj hello następującej konfiguracji:

    | Atrybut | Wartość | Szczegóły |
    | --- | --- | --- |
    | Nazwa | *Podaj nazwę* | Na przykład "limit tooAAD — PreferredDataLocation użytkownika" |
    | Opis | *Podaj opis* |
    | System połączony | *Wybierz łącznik AAD hello* |
    | Połączony System typu obiektu | Użytkownik ||
    | Typ obiektu Metaverse | **Osoby** ||
    | Typ łącza | **Dołącz** ||
    | Priorytet | *Wybierz liczbę z zakresu od 1 – 99* | 1 – 99 jest zarezerwowana dla reguły synchronizacji niestandardowych. YDo odbiera wartość, która jest używana przez inną regułę synchronizacji. |

5. Przejdź toohello **filtru Scoping** karta i Dodaj **pojedynczego grupę ustalania zakresu filtru z klauzulami dwóch**:
 
    | Atrybut | Operator | Wartość |
    | --- | --- | --- |
    | sourceObjectType | RÓWNOŚCI | Użytkownik |
    | cloudMastered | NOTEQUAL | True |

    Filtr zakresu określa obiekty usługi Azure AD, że ta reguła synchronizacji ruchu wychodzącego. W tym przykładzie używamy hello tego samego zakresu filtru "Out tooAD — tożsamości użytkownika" OOB reguły synchronizacji. Go zapobiega reguły synchronizacji hello tooUser zastosowanych obiektów, które nie są synchronizowane z lokalnej usługi Active Directory. Może być konieczne tootweak hello zakresu filtru zgodnie z tooyour wdrożenia usługi Azure AD Connect.
    
6. Przejdź toohello **przekształcania** karcie i wdrożenie hello następujące reguły przekształcania:

    | Typ przepływu | Atrybut TARGET | Element źródłowy | Zastosuj raz | Scal typu |
    | --- | --- | --- | --- | --- |
    | Bezpośrednie | PreferredDataLocation | PreferredDataLocation | Unchecked | Aktualizacja |

7. Zamknij **Dodaj** toocreate hello wychodzącą regułę.

![Utwórz regułę synchronizacji ruchu wychodzącego](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Krok 6: Uruchom pełną synchronizację cyklu
Ogólnie rzecz biorąc cyklu Pełna synchronizacja jest wymagane, ponieważ firma Microsoft ma dodaje nowe atrybuty hello tooboth AD i schematu łącznika usługi Azure AD i wprowadzono reguły synchronizacji niestandardowych. Zalecane jest, sprawdź hello zmiany przed wykonaniem operacji eksportowania ich tooAzure AD. Możesz użyć hello następujące kroki tooverify hello zmiany podczas uruchamiania ręcznie hello kroki, które tworzą cyklu pełną synchronizację. 

1. Uruchom **pełny import** krok na powitania **lokalnego łącznika AD**:

   1. Przejdź toohello **operacji** kartę w hello Synchronization Service Manager.

   2. Kliknij prawym przyciskiem myszy na powitania **lokalnego łącznika AD** i wybierz **Uruchom...**

   3. W wyskakującym oknie dialogowym hello, wybierz **pełny Import** i kliknij przycisk **OK**.
    
   4. Poczekaj, aż toocomplete operacji.

    > [!NOTE]
    > Pełny Import można pominąć na powitania AD łącznika lokalnego, jeśli atrybut źródłowy hello jest już uwzględniony w hello lista importowanych atrybutów. Innymi słowy, nie masz toomake zmiany podczas [krok 2: Dodaj toohello atrybut źródła hello AD łącznika lokalnego schematu](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Uruchom **pełny import** krok na powitania **łącznika usługi Azure AD**:

   1. Kliknij prawym przyciskiem myszy na powitania **łącznika usługi Azure AD** i wybierz **Uruchom...**

   2. W wyskakującym oknie dialogowym hello, wybierz **pełny Import** i kliknij przycisk **OK**.
   
   3. Poczekaj, aż toocomplete operacji.

3. Sprawdź zmian reguły synchronizacji hello na istniejący obiekt użytkownika:

atrybut źródłowy Hello z lokalnej usługi Active Directory i PreferredDataLocation z usługi Azure AD zostały zaimportowane do hello odpowiednich miejsca łącznik. Przed wykonaniem kroku Pełna synchronizacja, zaleca się wykonanie **Podgląd** istniejącego użytkownika obiektu w hello na lokalnej przestrzeni łącznika usługi AD. Obiekt Hello, przez Ciebie powinien mieć atrybut źródłowy hello wypełnione. Pomyślnie **Podgląd** z hello PreferredDataLocation wypełnione hello Metaverse jest poprawnie skonfigurowane reguły synchronizacji hello dobry wskaźnik. Aby uzyskać informacje dotyczące toodo **Podgląd**, można znaleźć toosection [Sprawdź zmiany hello](#verify-the-change).

4. Uruchom **pełną synchronizację** krok na powitania **lokalnego łącznika AD**:

   1. Kliknij prawym przyciskiem myszy na powitania **lokalnego łącznika AD** i wybierz **Uruchom...**
  
   2. W wyskakującym oknie dialogowym hello, wybierz **pełną synchronizację** i kliknij przycisk **OK**.
   
   3. Poczekaj, aż toocomplete operacji.

5. Sprawdź **oczekujące operacje eksportowania** tooAzure AD:

   1. Kliknij prawym przyciskiem myszy na powitania **łącznika usługi Azure AD** i wybierz **przestrzeni łącznika wyszukiwania**.

   2. W hello przestrzeni łącznika wyszukiwania wyskakujące okno dialogowe:

      1. Ustaw **zakres** za**wyeksportować oczekujące**.
      
      2. Sprawdź wszystkie trzy pola wyboru, w tym **dodawania, modyfikowania i usuwania**.
      
      3. Kliknij przycisk hello **wyszukiwania** przycisk tooget hello listę obiektów z toobe zmiany wyeksportowane. zmiany hello tooexamine dla danego obiektu, kliknij dwukrotnie hello obiektu.
      
      4. Sprawdź, czy zmiany hello są oczekiwane.

6. Uruchom **wyeksportować** krok na powitania **łącznika usługi Azure AD**
      
   1. Kliknij prawym przyciskiem myszy hello **łącznika usługi Azure AD** i wybierz **Uruchom...**
   
   2. W hello uruchomić łącznik wyskakującym oknie dialogowym wybierz **wyeksportować** i kliknij przycisk **OK**.
   
   3. Poczekaj, aż toocomplete tooAzure AD eksportu.

> [!NOTE]
> Można zauważyć, że kroki hello nie zawierają hello krok pełnej synchronizacji i eksportowanie na powitania łącznika usługi Azure AD. ponieważ hello wartości atrybutów są wynikających z lokalnymi tooAzure usługi Active Directory AD tylko Hello kroki nie są wymagane.

### <a name="step-7-re-enable-sync-scheduler"></a>Krok 7: Ponownie włączyć harmonogram synchronizacji
Ponowne włączenie harmonogramu synchronizacji wbudowanych hello:

1. Uruchom sesję programu PowerShell.

2. Ponownie włączyć zaplanowanej synchronizacji, uruchamiając polecenie cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o model konfiguracji hello w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Dowiedz się więcej o hello język wyrażeń w [opis deklaratywne inicjowania obsługi administracyjnej wyrażenia](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
