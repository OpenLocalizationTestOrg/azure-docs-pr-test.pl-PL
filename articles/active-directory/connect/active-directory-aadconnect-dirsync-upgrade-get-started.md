---
title: "Azure AD Connect: uaktualnianie z narzędzia DirSync | Microsoft Docs"
description: "Dowiedz się, jak uaktualnić narzędzie DirSync do programu Azure AD Connect. W tym artykule opisano czynności związane z uaktualnianiem narzędzia DirSync do programu Azure AD Connect."
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
ms.openlocfilehash: 7049af4567947d3d799a38c5a3940ba25a2c0f18
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: uaktualnianie z narzędzia DirSync
Program Azure AD Connect zastępuje narzędzie DirSync. W tym temacie opisano sposoby uaktualniania z narzędzia DirSync. Czynności te nie zadziałają w przypadku aktualizowania z innej wersji programu Azure AD Connect lub z narzędzia Azure AD Sync.

Przed rozpoczęciem instalacji należy [pobrać program Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) i wykonać czynności związane z wymaganiami wstępnymi opisane w temacie [Azure AD Connect: sprzęt i wymagania wstępne](active-directory-aadconnect-prerequisites.md). W szczególności należy zapoznać się z informacjami o następujących obszarach, ponieważ różnią się one od narzędzia DirSync:

* Wymagana wersja platformy .NET i programu PowerShell. Na serwerze są wymagane nowsze wersje niż w przypadku narzędzia DirSync.
* Konfiguracja serwera proxy. Jeśli używasz serwera proxy w celu uzyskiwania dostępu do Internetu, to ustawienie musi zostać skonfigurowane przed uaktualnieniem. Narzędzie DirSync zawsze używało serwera proxy skonfigurowanego dla użytkownika, który je zainstalował, ale program Azure AD Connect używa ustawień maszyny.
* Adresy URL, które muszą być otwarte na serwerze proxy. W przypadku podstawowych scenariuszy (także tych obsługiwanych przez narzędzie DirSync) wymagania są takie same. Aby używać jednej z nowych funkcji dostępnych w programie Azure AD Connect, należy otworzyć dodatkowe adresy URL.

> [!NOTE]
> Aby po włączeniu serwera programu Azure AD Connect rozpocząć synchronizowanie zmian z usługą Azure AD, nie można powrócić do używania narzędzia DirSync lub Azure AD Sync. Obniżenie wersji programu z Azure AD Connect do starszych klientów, w tym DirSync i Azure AD Sync, nie jest obsługiwane i może prowadzić do problemów takich jak utrata danych w usłudze Azure AD.

Jeśli nie przeprowadzasz uaktualnienia z narzędzia DirSync, zobacz [dokumentację pokrewną](#related-documentation), aby zapoznać się z innymi scenariuszami.

## <a name="upgrade-from-dirsync"></a>Uaktualnianie przy użyciu narzędzia DirSync
Istnieją różne opcje uaktualniania, w zależności od istniejącego wdrożenia narzędzia DirSync. Jeśli szacowany czas uaktualniania wynosi mniej niż trzy godziny, zalecane jest przeprowadzenie uaktualnienia w miejscu. Jeśli szacowany czas uaktualniania wynosi ponad trzy godziny, zalecane jest przeprowadzenie wdrożenia równoległego na innym serwerze. Szacuje się, że uaktualnienie trwa więcej niż trzy godziny, jeśli masz ponad 50 000 obiektów.

| Scenariusz |
| --- | --- |
| [Uaktualnienie w miejscu](#in-place-upgrade) |
| [Wdrożenie równoległe](#parallel-deployment) |

> [!NOTE]
> Jeśli planujesz uaktualnienie narzędzia DirSync do programu Azure AD Connect, nie odinstalowuj narzędzia DirSync samodzielnie przed przeprowadzeniem uaktualnienia. Program Azure AD Connect odczyta konfigurację narzędzia DirSync i przeprowadzi jej migrację, a następnie odinstaluje to narzędzie po sprawdzeniu serwera.

**Uaktualnienie w miejscu**  
Oczekiwany czas trwania uaktualnienia jest wyświetlany w kreatorze. Jest on szacowany na podstawie założenia, że uaktualnienie bazy danych zawierającej 50 000 obiektów (użytkowników, kontaktów i grup) zajmuje trzy godziny. Program Azure AD Connect sugeruje uaktualnienie w miejscu, jeśli baza danych zawiera mniej niż 50 000 obiektów. Jeśli zdecydujesz się kontynuować, podczas uaktualniania zostaną automatycznie zastosowane bieżące ustawienia, a na serwerze zostanie automatycznie przywrócona aktywna synchronizacja.

Jeśli chcesz przeprowadzić migrację konfiguracji i wdrożenie równoległe, możesz pominąć zalecenie uaktualnienia w miejscu. Możesz na przykład skorzystać z tej okazji, aby odświeżyć sprzęt i system operacyjny. Aby uzyskać więcej informacji, zobacz sekcję [Wdrożenie równoległe](#parallel-deployment).

**Wdrożenie równoległe**  
Jeśli masz więcej niż 50 000 obiektów, zalecane jest wdrożenie równoległe. Dzięki przeprowadzeniu tego wdrożenia użytkownicy nie odczują opóźnień w działaniu. W procesie instalacji programu Azure AD Connect czas przestoju wymagany do uaktualnienia jest szacowany, ale jeśli już wcześniej przeprowadzano uaktualnienie narzędzia DirSync, najlepiej posłużyć się własnym doświadczeniem.

### <a name="supported-dirsync-configurations-to-be-upgraded"></a>Obsługiwane konfiguracje narzędzia DirSync przy uaktualnianiu
Następujące zmiany konfiguracji są obsługiwane w przypadku uaktualnionego narzędzia DirSync:

* Filtrowanie domen i jednostek organizacyjnych
* Identyfikator alternatywny (UPN)
* Ustawienia synchronizacji haseł i wdrożenia hybrydowego programu Exchange
* Ustawienia lasu/domeny i usługi Azure AD
* Filtrowanie na podstawie atrybutów użytkownika

Następującej zmiany nie można uwzględnić w uaktualnieniu. Jeśli jest używana poniższa konfiguracja, uaktualnienie zostanie zablokowane:

* Nieobsługiwane zmiany w narzędziu DirSync, na przykład usunięte atrybuty lub użycie niestandardowej biblioteki DLL rozszerzenia

![Uaktualnienie zablokowane](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

W takim przypadku zalecane jest zainstalowanie nowego serwera z programem Azure AD Connect w [trybie przejściowym](active-directory-aadconnectsync-operations.md#staging-mode) i zweryfikowanie starej konfiguracji narzędzia DirSync oraz nowej konfiguracji programu Azure AD Connect. Ponownie zastosuj zmiany, korzystając z konfiguracji niestandardowej, zgodnie z opisem w temacie [Synchronizacja programu Azure AD Connect: konfiguracja niestandardowa](active-directory-aadconnectsync-whatis.md).

Hasła używane przez narzędzie DirSync do kont usług nie mogą zostać pobrane i nie są migrowane. Te hasła są resetowane podczas uaktualnienia.

### <a name="high-level-steps-for-upgrading-from-dirsync-to-azure-ad-connect"></a>Ogólne kroki uaktualniania narzędzia DirSync do programu Azure AD Connect
1. Wprowadzenie do programu Azure AD Connect
2. Analiza bieżącej konfiguracji narzędzia DirSync
3. Uzyskanie hasła administratora globalnego usługi Azure AD
4. Uzyskanie poświadczeń konta administratora przedsiębiorstwa (używanych tylko podczas instalacji programu Azure AD Connect)
5. Instalacja programu Azure AD Connect
   * Odinstalowanie (lub tymczasowe wyłączenie) narzędzia DirSync
   * Instalowanie programu Azure AD Connect
   * Opcjonalne rozpoczęcie synchronizacji

Dodatkowe kroki są wymagane, jeśli:

* Aktualnie używasz pełnej wersji programu SQL Server — lokalnie lub zdalnie
* Synchronizacja ma obejmować więcej niż 50 000 obiektów

## <a name="in-place-upgrade"></a>Uaktualnienie w miejscu
1. Uruchom instalator (MSI) programu Azure AD Connect.
2. Przeczytaj i zaakceptuj postanowienia licencyjne i zasady zachowania poufności informacji.  
   ![Wprowadzenie do usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Kliknij przycisk Dalej, aby rozpocząć analizę istniejącej instalacji narzędzia DirSync.  
   ![Analizowanie istniejącej instalacji narzędzia Directory Sync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Po zakończeniu analizy zostanie wyświetlone zalecenie dotyczące dalszego postępowania.  
   * Jeśli używasz programu SQL Server Express i masz mniej niż 50 000 obiektów, jest wyświetlany następujący ekran:  
     ![Analiza zakończona, wszystko gotowe do uaktualnienia narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Jeśli na potrzeby narzędzia DirSync używasz pełnego programu SQL Server, zamiast tego ekranu zostanie wyświetlona następująca strona:  
     ![Analiza zakończona, wszystko gotowe do uaktualnienia narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     Zostaną wyświetlone informacje dotyczące istniejącego serwera bazy danych SQL Server używanego przez narzędzie DirSync. W razie potrzeby wprowadź odpowiednie zmiany. Kliknij przycisk **Dalej**, aby kontynuować instalację.
   * Jeśli masz więcej niż 50 000 obiektów, zostanie wyświetlony następujący ekran:  
     ![Analiza zakończona, wszystko gotowe do uaktualnienia narzędzia DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     Aby przejść do uaktualnienia w miejscu, kliknij pole wyboru obok komunikatu: **Kontynuuj uaktualnianie narzędzia DirSync na tym komputerze.**
     Aby zamiast tego przeprowadzić [wdrożenie równoległe](#parallel-deployment), należy wyeksportować ustawienia konfiguracji narzędzia DirSync i przenieść konfigurację na nowy serwer.
5. Wprowadź hasło do konta aktualnie używanego do łączenia się z usługą Azure AD. Musi to być konto używane aktualnie przez narzędzie DirSync.  
   ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Jeśli wystąpi błąd lub problemy z łącznością, zobacz [Rozwiązywanie problemów z łącznością](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Podaj konto administratora przedsiębiorstwa dla usługi Active Directory.  
   ![Wprowadzanie poświadczeń usług AD DS](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Wszystko jest teraz gotowe do konfiguracji. Po kliknięciu polecenia **Uaktualnij** narzędzie DirSync zostanie odinstalowane, a program Azure AD Connect zostanie skonfigurowany i rozpocznie synchronizację.  
   ![Wszystko gotowe do skonfigurowania](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Po zakończeniu instalacji wyloguj się, a następnie zaloguj się ponownie w systemie Windows przed użyciem narzędzia Synchronization Service Manager lub Synchronization Rule Editor albo wprowadzeniem jakichkolwiek innych zmian konfiguracji.

## <a name="parallel-deployment"></a>Wdrożenie równoległe
### <a name="export-the-dirsync-configuration"></a>Eksportowanie konfiguracji narzędzia DirSync
**Wdrożenie równoległe, gdy liczba obiektów jest większa niż 50 000**

Jeśli masz więcej niż 50 000 obiektów, podczas instalacji programu Azure AD Connect będzie zalecane wdrożenie równoległe.

Zostanie wyświetlony ekran podobny do poniższego:  
![Analiza zakończona](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Jeśli chcesz przeprowadzić wdrożenie równoległe, wykonaj następujące kroki:

* Kliknij przycisk **Eksportuj ustawienia**. Po zainstalowaniu programu Azure AD Connect na osobnym serwerze te ustawienia są migrowane z bieżącego narzędzia DirSync do nowej instalacji programu Azure AD Connect.

Po pomyślnym wyeksportowaniu ustawień możesz zakończyć działanie kreatora instalacji programu Azure AD Connect na serwerze narzędzia DirSync. Przejdź do następnego kroku, aby [zainstalować program Azure AD Connect na osobnym serwerze](#installation-of-azure-ad-connect-on-separate-server)

**Wdrożenie równoległe, gdy liczba obiektów jest mniejsza niż 50 000**

Jeśli masz mniej niż 50 000 obiektów, ale mimo to chcesz przeprowadzić wdrożenie równoległe, wykonaj następujące czynności:

1. Uruchom instalator (MSI) programu Azure AD Connect.
2. Po wyświetleniu ekranu **Azure AD Connect — zapraszamy!** zakończ działanie kreatora instalacji, klikając znak „X” w prawym górnym rogu okna.
3. Otwórz wiersz polecenia.
4. Z poziomu lokalizacji instalacji programu Azure AD Connect (domyślnie: C:\Program Files\Microsoft Azure Active Directory Connect) uruchom następujące polecenie: `AzureADConnect.exe /ForceExport`.
5. Kliknij przycisk **Eksportuj ustawienia**. Po zainstalowaniu programu Azure AD Connect na osobnym serwerze te ustawienia są migrowane z bieżącego narzędzia DirSync do nowej instalacji programu Azure AD Connect.

![Analiza zakończona](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Po pomyślnym wyeksportowaniu ustawień możesz zakończyć działanie kreatora instalacji programu Azure AD Connect na serwerze narzędzia DirSync. Przejdź do następnego kroku, aby [zainstalować program Azure AD Connect na osobnym serwerze](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Instalowanie programu Azure AD Connect na osobnym serwerze
W przypadku instalowania programu Azure AD Connect na nowym serwerze domyślnym wariantem jest czysta instalacja programu Azure AD Connect. Ponieważ jednak planujesz użyć konfiguracji narzędzia DirSync, należy wykonać kilka dodatkowych kroków:

1. Uruchom instalator (MSI) programu Azure AD Connect.
2. Po wyświetleniu ekranu **Azure AD Connect — zapraszamy!** zakończ działanie kreatora instalacji, klikając znak „X” w prawym górnym rogu okna.
3. Otwórz wiersz polecenia.
4. Z poziomu lokalizacji instalacji programu Azure AD Connect (domyślnie: C:\Program Files\Microsoft Azure Active Directory Connect) uruchom następujące polecenie: `AzureADConnect.exe /migrate`.
   Zostanie uruchomiony kreator instalacji programu Azure AD Connect z wyświetlonym następującym ekranem:  
   ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Wybierz plik ustawień wyeksportowany z narzędzia DirSync.
6. Skonfiguruj opcje zaawansowane, takie jak:
   * Niestandardowa lokalizacja instalacji programu Azure AD Connect.
   * Istniejące wystąpienie programu SQL Server (domyślnie program Azure AD Connect instaluje program SQL Server 2012 Express). Nie używaj tego samego wystąpienia bazy danych, którego używa serwer narzędzia DirSync.
   * Konto usługi używane do połączenia z serwerem SQL (jeśli korzystasz ze zdalnej bazy danych programu SQL Server, musi to być konto usługi domeny).
     Na tym ekranie są dostępne następujące opcje:  
     ![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Kliknij przycisk **Dalej**.
8. Na stronie **Wszystko gotowe do skonfigurowania** pozostaw zaznaczone pole wyboru **Uruchom proces synchronizacji, gdy tylko konfiguracja zostanie ukończona**. Serwer jest teraz w [trybie przejściowym](active-directory-aadconnectsync-operations.md#staging-mode), więc zmiany nie są eksportowane do usługi Azure AD.
9. Kliknij pozycję **Zainstaluj**.
10. Po zakończeniu instalacji wyloguj się, a następnie zaloguj się ponownie w systemie Windows przed użyciem narzędzia Synchronization Service Manager lub Synchronization Rule Editor albo wprowadzeniem jakichkolwiek innych zmian konfiguracji.

> [!NOTE]
> Rozpocznie się synchronizacja między usługą Active Directory systemu Windows Server a usługą Azure Active Directory, ale żadne zmiany nie zostaną wyeksportowane do usługi Azure AD. Jednocześnie tylko jedno narzędzie do synchronizacji może aktywnie eksportować zmiany. Ten stan jest nazywany [trybem przejściowym](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-to-begin-synchronization"></a>Sprawdzanie, czy program Azure AD Connect jest gotowy do rozpoczęcia synchronizacji
Aby sprawdzić, czy program Azure AD Connect jest gotowy do zastąpienia narzędzia DirSync, należy otworzyć aplikację **Synchronization Service Manager** znajdującą się w grupie **Azure AD Connect** w menu Start.

W aplikacji przejdź na kartę **Operacje**. Na tej karcie potwierdź, że zakończono następujące operacje:

* Importowanie w łączniku usługi AD
* Importowanie w programie Azure AD Connector
* Pełna synchronizacja w łączniku usługi AD
* Pełna synchronizacja w programie Azure AD Connector

![Zakończenie importowania i synchronizacji](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Przejrzyj wyniki tych operacji, aby upewnić się, że nie wystąpiły żadne błędy.

Jeśli chcesz wyświetlić i sprawdzić zmiany, które mają zostać wyeksportowane do usługi Azure AD, zapoznaj się z instrukcjami weryfikacji konfiguracji w sekcji [tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode). Wprowadzaj wymagane zmiany konfiguracji do momentu, w którym nie znajdziesz już niczego nieoczekiwanego.

Po ukończeniu tych kroków i uzyskania zadowalających wyników wszystko jest gotowe, aby przełączyć się z narzędzia DirSync na usługę Azure AD.

### <a name="uninstall-dirsync-old-server"></a>Odinstalowywanie narzędzia DirSync (stary serwer)
* W obszarze **Programy i funkcje** znajdź pozycję **Narzędzie do synchronizacji z usługą Microsoft Azure Active Directory**
* Odinstaluj **Narzędzie do synchronizacji z usługą Windows Azure Active Directory**
* Odinstalowywanie może potrwać do 15 minut.

Jeśli wolisz odinstalować narzędzie DirSync później, możesz również tymczasowo zamknąć serwer lub wyłączyć usługę. Jeśli coś się nie powiedzie, ta metoda umożliwia jego ponowne włączenie. Jednak niepowodzenie następnego kroku nie jest oczekiwane, więc nie powinno to być potrzebne.

Po odinstalowaniu lub wyłączeniu narzędzia DirSync na żadnym serwerze nie będzie aktywne eksportowanie do usługi Azure AD. Aby jakiekolwiek zmiany w lokalnej usłudze Active Directory były znów synchronizowane z usługą Azure AD, należy wykonać następny krok polegający na włączeniu programu Azure AD Connect.

### <a name="enable-azure-ad-connect-new-server"></a>Włączanie programu Azure AD Connect (nowy serwer)
Po zainstalowaniu i ponownym uruchomieniu programu Azure AD Connect będzie możliwe wprowadzenie dodatkowych zmian w konfiguracji. Uruchom program **Azure AD Connect**, korzystając z menu Start lub ze skrótu na pulpicie. Pamiętaj, aby nie próbować uruchomić ponownie instalatora MSI.

Powinien zostać wyświetlony następujący ekran:  
![Dodatkowe zadania](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Wybierz pozycję **Konfigurowanie trybu przejściowego**.
* Wyłącz tryb przejściowy, usuwając zaznaczenie pola wyboru **Włącz tryb przejściowy**.

![Wprowadzanie poświadczeń usługi Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Kliknij przycisk **Dalej**
* Na stronie potwierdzenia kliknij przycisk **Zainstaluj**.

Serwer programu Azure AD Connect jest teraz aktywnym serwerem i nie możesz przełączyć się z powrotem do istniejącego serwera narzędzia DirSync.

## <a name="next-steps"></a>Następne kroki
Po zainstalowaniu programu Azure AD Connect możesz [zweryfikować instalację i przypisać licencje](active-directory-aadconnect-whats-next.md).

Dowiedz się więcej na temat nowych funkcji włączonych w ramach instalacji: [Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md), [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) oraz [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Dowiedz się więcej na te popularne tematy: [harmonogram i sposób włączania synchronizacji](active-directory-aadconnectsync-feature-scheduler.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
