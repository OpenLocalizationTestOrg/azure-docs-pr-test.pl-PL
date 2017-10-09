---
title: "Azure AD Connect: uaktualnianie z narzędzia DirSync | Microsoft Docs"
description: "Dowiedz się, jak tooupgrade z narzędzia DirSync tooAzure AD Connect. W tym artykule opisano kroki hello uaktualniania z narzędzia DirSync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: uaktualnianie z narzędzia DirSync
Azure AD Connect jest hello tooDirSync następnika. Możesz znaleźć hello sposoby, które można uaktualnić narzędzia DirSync w tym temacie. Czynności te nie zadziałają w przypadku aktualizowania z innej wersji programu Azure AD Connect lub z narzędzia Azure AD Sync.

Przed rozpoczęciem instalowania Azure AD Connect, upewnij się, zbyt[Pobierz Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) i pełne hello wstępnymi opisane w temacie [Azure AD Connect: sprzęt i wymagania wstępne](active-directory-aadconnect-prerequisites.md). W szczególności mają tooread o następujących powitania od tych obszarów różnią się od DirSync:

* Witaj wymagana wersja programu .net i programu PowerShell. Toobe wymagane na serwerze hello niż DirSync potrzebne są nowsze wersje.
* Witaj konfiguracji serwera proxy. Jeśli używasz tooreach serwera proxy hello internet, przed uaktualnieniem należy skonfigurować to ustawienie. Narzędzie DirSync zawsze używane hello skonfigurowany serwer proxy dla użytkownika hello instalacji, ale ustawienia komputera używa usługi Azure AD Connect zamiast tego.
* Otwórz toobe wymagane Hello adresy URL w powitania serwera proxy. Podstawowe scenariusze, te scenariusze również obsługiwane przez narzędzia DirSync, hello wymagania są takie same hello. Jeśli chcesz toouse jedną z nowych funkcji hello z programem Azure AD Connect, należy otworzyć niektóre nowe adresy URL.

> [!NOTE]
> Po włączeniu Twoje nowe Azure AD Connect serwera toostart synchronizowanie zmian tooAzure AD musi nie wycofasz toousing narzędzia DirSync i Azure AD Sync. Obniżenie wersji Azure AD Connect toolegacy klientów, włącznie z narzędzia DirSync i Azure AD Sync nie jest obsługiwana i może prowadzić tooissues, takich jak utraty danych w usłudze Azure AD.

Jeśli nie przeprowadzasz uaktualnienia z narzędzia DirSync, zobacz [dokumentację pokrewną](#related-documentation), aby zapoznać się z innymi scenariuszami.

## <a name="upgrade-from-dirsync"></a>Uaktualnianie przy użyciu narzędzia DirSync
W zależności od istniejącego wdrożenia narzędzia DirSync istnieją różne opcje uaktualniania hello. Jeśli hello szacowany czas uaktualniania wynosi mniej niż 3 godziny, zalecenie hello jest toodo uaktualnienie w miejscu. Jeśli hello szacowany czas uaktualniania wynosi ponad 3 godziny, zalecenie hello jest toodo wdrożenia równoległego na innym serwerze. Szacuje się, że jeśli masz więcej niż 50 000 obiektów ma więcej niż trzy godziny toodo hello uaktualnienia.

| Scenariusz |
| --- | --- |
| [Uaktualnienie w miejscu](#in-place-upgrade) |
| [Wdrożenie równoległe](#parallel-deployment) |

> [!NOTE]
> Podczas planowania tooupgrade z narzędzia DirSync tooAzure AD Connect, nie odinstalowuj narzędzia DirSync samodzielnie przed uaktualnieniem hello. Azure AD Connect będzie odczytu i migracji hello konfiguracji narzędzia DirSync i Odinstaluj po sprawdzeniu powitania serwera.

**Uaktualnienie w miejscu**  
Hello oczekuje się, że czas toocomplete hello uaktualniania jest wyświetlane przez kreatora hello. Ta szacowana jest oparta na powitania założenie, że ma trzy godziny toocomplete uaktualnienia bazy danych zawierającej 50 000 obiektów (użytkowników, kontaktów i grup). Jeśli hello liczbę obiektów w bazie danych jest mniejsza niż 50 000, Azure AD Connect zaleca uaktualnienie w miejscu. Jeśli zdecydujesz toocontinue bieżące ustawienia są automatycznie stosowane podczas uaktualniania, a serwer zostanie automatycznie wznowione synchronizacji z usługą active.

Jeśli chcesz toodo migracji konfiguracji i przeprowadzić wdrożenie równoległe, można zastąpić zalecenie uaktualnienia w miejscu hello. Możesz na przykład skorzystać z hello możliwości toorefresh hello sprzętu i systemu operacyjnego. Aby uzyskać więcej informacji, zobacz hello [wdrożenie równoległe](#parallel-deployment) sekcji.

**Wdrożenie równoległe**  
Jeśli masz więcej niż 50 000 obiektów, zalecane jest wdrożenie równoległe. Dzięki przeprowadzeniu tego wdrożenia użytkownicy nie odczują opóźnień w działaniu. Hello instalacji Azure AD Connect podejmuje przestoju hello tooestimate hello uaktualnienia, ale jeśli w przeszłości hello przeprowadzano uaktualnienie narzędzia DirSync, własne środowisko jest prawdopodobnie toobe hello najlepsze przewodnik.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Obsługiwane toobe konfiguracji narzędzia DirSync uaktualnienia
następujące zmiany w konfiguracji Hello są obsługiwane przez uaktualnionego DirSync:

* Filtrowanie domen i jednostek organizacyjnych
* Identyfikator alternatywny (UPN)
* Ustawienia synchronizacji haseł i wdrożenia hybrydowego programu Exchange
* Ustawienia lasu/domeny i usługi Azure AD
* Filtrowanie na podstawie atrybutów użytkownika

Nie można uaktualnić Hello zmiany. Jeśli masz tej konfiguracji hello uaktualnienie zostanie zablokowane:

* Nieobsługiwane zmiany w narzędziu DirSync, na przykład usunięte atrybuty lub użycie niestandardowej biblioteki DLL rozszerzenia

![Uaktualnienie zablokowane](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

W takich przypadkach hello zaleca tooinstall nowy serwer Azure AD Connect w [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode) i sprawdź hello starej konfiguracji narzędzia DirSync oraz nowej konfiguracji usługi Azure AD Connect. Ponownie zastosuj zmiany, korzystając z konfiguracji niestandardowej, zgodnie z opisem w temacie [Synchronizacja programu Azure AD Connect: konfiguracja niestandardowa](active-directory-aadconnectsync-whatis.md).

Witaj hasła używane przez narzędzie DirSync do kont usług hello nie można pobrać i nie są migrowane. Te hasła są resetowane podczas uaktualniania hello.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Ogólne kroki uaktualniania z narzędzia DirSync tooAzure AD Connect
1. Witamy tooAzure AD Connect
2. Analiza bieżącej konfiguracji narzędzia DirSync
3. Uzyskanie hasła administratora globalnego usługi Azure AD
4. Zbieranie poświadczeń dla konta administratora przedsiębiorstwa (używane tylko podczas instalacji hello programu Azure AD Connect)
5. Instalacja programu Azure AD Connect
   * Odinstalowanie (lub tymczasowe wyłączenie) narzędzia DirSync
   * Instalowanie programu Azure AD Connect
   * Opcjonalne rozpoczęcie synchronizacji

Dodatkowe kroki są wymagane, jeśli:

* Aktualnie używasz pełnej wersji programu SQL Server — lokalnie lub zdalnie
* Synchronizacja ma obejmować więcej niż 50 000 obiektów

## <a name="in-place-upgrade"></a>Uaktualnienie w miejscu
1. Uruchom program hello Azure AD Connect Instalator (MSI).
2. Należy przeczytać i zaakceptować warunki toolicense i poufności informacji.  
   ![Zapraszamy tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Kliknij przycisk Dalej toobegin analizę istniejącej instalacji narzędzia DirSync.  
   ![Analizowanie istniejącej instalacji narzędzia Directory Sync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Po zakończeniu analizy hello Zobacz hello zalecenia dotyczące tooproceed.  
   * Jeśli korzystasz z programu SQL Server Express i masz mniej niż 50 000 obiektów, jest wyświetlany po ekranie powitania:  
     ![Analiza zakończona, gotowe tooupgrade z narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Jeśli na potrzeby narzędzia DirSync używasz pełnego programu SQL Server, zamiast tego ekranu zostanie wyświetlona następująca strona:  
     ![Analiza zakończona, gotowe tooupgrade z narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     zostaną wyświetlone informacje Hello dotyczące hello istniejącej bazy danych SQL server używanego przez narzędzie DirSync. W razie potrzeby wprowadź odpowiednie zmiany. Kliknij przycisk **dalej** toocontinue hello instalacji.
   * Jeśli masz więcej niż 50 000 obiektów, zostanie wyświetlony następujący ekran:  
     ![Analiza zakończona, gotowe tooupgrade z narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed o uaktualnienie w miejscu, kliknij przycisk Następny komunikat toothis hello wyboru: **Kontynuuj uaktualnianie narzędzia DirSync na tym komputerze.**
     toodo [wdrożenie równoległe](#parallel-deployment) zamiast tego należy wyeksportować ustawienia konfiguracji narzędzia DirSync hello i Przenieś hello konfiguracji toohello nowego serwera.
5. Podaj hello hasło dla konta hello się, że obecnie używasz tooconnect tooAzure AD. Musi to być konto hello aktualnie używane przez narzędzie DirSync.  
   ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Jeśli wystąpi błąd lub problemy z łącznością, zobacz [Rozwiązywanie problemów z łącznością](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Podaj konto administratora przedsiębiorstwa dla usługi Active Directory.  
   ![Wprowadzanie poświadczeń usług AD DS](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Możesz teraz gotowy tooconfigure. Po kliknięciu polecenia **Uaktualnij** narzędzie DirSync zostanie odinstalowane, a program Azure AD Connect zostanie skonfigurowany i rozpocznie synchronizację.  
   ![Gotowe tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Po ukończeniu instalacji hello, wyloguj się i zaloguj ponownie tooWindows przed użyciem Menedżera usługi synchronizacji, Synchronization Rule Editor lub spróbuj toomake inne zmiany w konfiguracji.

## <a name="parallel-deployment"></a>Wdrożenie równoległe
### <a name="export-hello-dirsync-configuration"></a>Eksportowanie konfiguracji narzędzia DirSync hello
**Wdrożenie równoległe, gdy liczba obiektów jest większa niż 50 000**

Jeśli masz więcej niż 50 000 obiektów, a następnie hello instalacji Azure AD Connect będzie zalecane wdrożenie równoległe.

Zostanie wyświetlony ekran podobny następujące toohello:  
![Analiza zakończona](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Jeśli chcesz tooproceed do wdrożenia równoległego, należy hello tooperform następujące kroki:

* Kliknij przycisk hello **wyeksportować ustawienia** przycisku. Po zainstalowaniu usługi Azure AD Connect na osobnym serwerze te ustawienia są migrowane z bieżącej instalacji nowego Azure AD Connect tooyour narzędzia DirSync.

Po pomyślnym wyeksportowaniu ustawień możesz zakończyć działanie hello Kreator Azure AD Connect na powitania serwera narzędzia DirSync. Przejdź do kroku dalej hello zbyt[zainstalować program Azure AD Connect na osobnym serwerze](#installation-of-azure-ad-connect-on-separate-server)

**Wdrożenie równoległe, gdy liczba obiektów jest mniejsza niż 50 000**

Jeśli masz mniej niż 50 000 obiektów, ale nadal chcesz toodo wdrożenie równoległe, następnie hello następujące:

1. Uruchom hello Azure AD Connect Instalator (MSI).
2. Po wyświetleniu hello **tooAzure powitalnej AD Connect** ekranu, Kreator instalacji hello zakończenia klikając hello prawym górnym rogu okna hello hello "X".
3. Otwórz wiersz polecenia.
4. Z hello zainstalować lokalizacji programu Azure AD Connect (domyślne: C:\Program Files\Microsoft Azure Active Directory Connect) wykonaj następujące polecenie hello: `AzureADConnect.exe /ForceExport`.
5. Kliknij przycisk hello **wyeksportować ustawienia** przycisku. Po zainstalowaniu usługi Azure AD Connect na osobnym serwerze te ustawienia są migrowane z bieżącej instalacji nowego Azure AD Connect tooyour narzędzia DirSync.

![Analiza zakończona](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Po pomyślnym wyeksportowaniu ustawień możesz zakończyć działanie hello Kreator Azure AD Connect na powitania serwera narzędzia DirSync. Przejdź do kroku dalej hello zbyt[zainstalować program Azure AD Connect na osobnym serwerze](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Instalowanie programu Azure AD Connect na osobnym serwerze
Po zainstalowaniu usługi Azure AD Connect na nowym serwerze założeń hello jest, które mają tooperform czystej instalacji programu Azure AD Connect. Ponieważ mają konfiguracji narzędzia DirSync hello toouse istnieją tootake pewnych dodatkowych czynności:

1. Uruchom hello Azure AD Connect Instalator (MSI).
2. Po wyświetleniu hello **tooAzure powitalnej AD Connect** ekranu, Kreator instalacji hello zakończenia klikając hello prawym górnym rogu okna hello hello "X".
3. Otwórz wiersz polecenia.
4. Z hello zainstalować lokalizacji programu Azure AD Connect (domyślne: C:\Program Files\Microsoft Azure Active Directory Connect) wykonaj następujące polecenie hello: `AzureADConnect.exe /migrate`.
   Kreator instalacji Hello Azure AD Connect uruchamia i stanowi po ekranie powitania:  
   ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Wybierz plik ustawień hello wyeksportowany z narzędzia Dirsync.
6. Skonfiguruj opcje zaawansowane, takie jak:
   * Niestandardowa lokalizacja instalacji programu Azure AD Connect.
   * Istniejące wystąpienie programu SQL Server (domyślnie program Azure AD Connect instaluje program SQL Server 2012 Express). Nie używaj hello tego samego wystąpienia bazy danych używa serwer narzędzia DirSync.
   * Konto usługi używane tooSQL tooconnect serwera (jeśli bazy danych programu SQL Server jest zdalny, a następnie to konto musi być kontem domeny usługi).
     Na tym ekranie są dostępne następujące opcje:  
     ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Kliknij przycisk **Dalej**.
8. Na powitania **gotowe tooconfigure** zostaw hello **Uruchom proces synchronizacji hello zaraz po zakończeniu konfiguracji hello** zaznaczone. Serwer Hello jest teraz w [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode) dlatego zmiany nie są wyeksportowanego tooAzure AD.
9. Kliknij pozycję **Zainstaluj**.
10. Po ukończeniu instalacji hello, wyloguj się i zaloguj ponownie tooWindows przed użyciem Menedżera usługi synchronizacji, Synchronization Rule Editor lub spróbuj toomake inne zmiany w konfiguracji.

> [!NOTE]
> Rozpoczyna się synchronizacja usługi Active Directory systemu Windows Server i usługi Azure Active Directory, ale zmiany nie są wyeksportowanego tooAzure AD. Jednocześnie tylko jedno narzędzie do synchronizacji może aktywnie eksportować zmiany. Ten stan jest nazywany [trybem przejściowym](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Sprawdź, czy usługa Azure AD Connect jest gotowy toobegin synchronizacji
tooverify, który Azure AD Connect jest gotowy tootake za pośrednictwem narzędzia DirSync, należy tooopen **Menedżera usługi synchronizacji** w grupie hello **Azure AD Connect** z hello start menu.

W aplikacji hello Przejdź toohello **operacji** kartę. Na tej karcie upewnij się, że hello następujące operacje zostały ukończone:

* Zaimportuj na powitania łączniku AD
* Zaimportuj na powitania łącznika usługi Azure AD
* Pełna synchronizacja w hello łączniku AD
* Pełna synchronizacja w hello łącznika usługi Azure AD

![Zakończenie importowania i synchronizacji](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Przejrzyj wyniki tych operacji hello i upewnij się, że nie ma żadnych błędów.

Toosee i sprawdzić zmiany hello, które są o tooAzure toobe wyeksportowane AD, Odczytaj, jak tooverify hello Konfiguracja [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode). Wprowadzaj wymagane zmiany konfiguracji do momentu, w którym nie znajdziesz już niczego nieoczekiwanego.

Wszystko jest gotowe tooswitch z narzędzia DirSync tooAzure AD podczas zostały wykonane następujące kroki i są zadowoleni z wyniku hello.

### <a name="uninstall-dirsync-old-server"></a>Odinstalowywanie narzędzia DirSync (stary serwer)
* W obszarze **Programy i funkcje** znajdź pozycję **Narzędzie do synchronizacji z usługą Microsoft Azure Active Directory**
* Odinstaluj **Narzędzie do synchronizacji z usługą Windows Azure Active Directory**
* Dezinstalacja Hello może potrwać too15 toocomplete minut.

Jeśli wolisz toouninstall DirSync później, możesz również tymczasowo zamknąć serwer hello lub wyłączyć usługę hello. Jeśli jakaś nieprawidłowość, ta metoda pozwala toore enable go. Jednak nie przewiduje się tym następnego kroku hello zakończą się niepowodzeniem, to nie powinna być potrzebne.

Z narzędziem DirSync zostanie odinstalowana lub wyłączona serwer nie jest aktywne eksportowanie tooAzure AD. Witaj następny krok tooenable Azure AD Connect należy wykonać przed wszelkie zmiany w lokalnej usługi Active Directory będą nadal synchronizowane toobe tooAzure AD.

### <a name="enable-azure-ad-connect-new-server"></a>Włączanie programu Azure AD Connect (nowy serwer)
Po zakończeniu instalacji, otworzyć usługi Azure AD connect będzie pozwalają toomake dodatkowych zmian konfiguracyjnych. Uruchom **Azure AD Connect** z hello start menu lub hello skrót na pulpicie hello. Upewnij się, że nie należy toorun hello ponownie Instalatora MSI.

Powinny pojawić się następujące hello:  
![Dodatkowe zadania](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Wybierz pozycję **Konfigurowanie trybu przejściowego**.
* Wyłącz tryb przejściowy przez zaznaczenie pola hello **Włącz tryb przejściowy** wyboru.

![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Kliknij przycisk hello **dalej** przycisku
* Na stronie potwierdzenia powitania kliknij hello **zainstalować** przycisku.

Azure AD Connect jest teraz serwerem aktywnym i musisz nie przełączyć wstecz toousing istniejącego serwera narzędzia DirSync.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz Azure AD Connect można [zweryfikować hello instalację i przypisywanie licencji](active-directory-aadconnect-whats-next.md).

Dowiedz się więcej na temat nowych funkcji włączonych instalacji hello: [automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md), [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), i [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Dowiedz się więcej na te popularne tematy: [harmonogram i sposób synchronizacji tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
