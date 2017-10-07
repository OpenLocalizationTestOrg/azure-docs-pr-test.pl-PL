---
title: "aaaVPN integracji z usługą Azure MFA przy użyciu rozszerzenia zasad Sieciowych | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono integrowanie infrastruktury sieci VPN z usługą Azure MFA przy użyciu rozszerzenia serwera zasad sieciowych (NPS) hello platformy Microsoft Azure."
services: active-directory
keywords: "Usługa Azure MFA, integracja sieci VPN, Azure Active Directory, serwer zasad sieciowych rozszerzenia"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Integrowanie infrastruktury sieci VPN z usługi Azure Multi-Factor Authentication (MFA) na platformie Azure przy użyciu hello rozszerzenia serwera zasad sieciowych (NPS)

## <a name="overview"></a>Omówienie

Hello rozszerzenia usługi zasad sieciowych (NPS) na platformie Azure umożliwia organizacjom toosafeguard uwierzytelniania klienta dla serwera usługi użytkowników zdalnego uwierzytelniania (RADIUS) za pomocą opartej na chmurze [Azure Multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), zapewniające weryfikacji dwuetapowej.

Ten artykuł zawiera instrukcje dotyczące integracji z usługą Azure MFA hello infrastruktury serwera NPS przy użyciu rozszerzenia zasad Sieciowych hello na potrzeby weryfikacji dwuetapowej bezpiecznego Azure tooenable dla użytkowników próbujących tooconnect tooyour sieci przy użyciu sieci VPN. 

Witaj zasad sieciowych i dostępu do usługi (NPS) umożliwia organizacjom Witaj następujące możliwości:

* Określ lokalizację centralnego zarządzania hello i kontroli toospecify żądania sieci, którzy mogą łączyć, jakich porach dnia mogą przyjmować połączenia czas trwania hello połączeń i hello poziom zabezpieczeń, czy klienci muszą używać tooconnect i tak dalej. Zamiast określać te zasady na każdym serwerze sieci VPN lub bramy usług pulpitu zdalnego (RD), te zasady można określić jeden raz w centralnej lokalizacji. Służy Hello protokołu RADIUS tooprovide hello scentralizowane uwierzytelnianie, autoryzację i Ewidencjonowanie. 
* Ustanów i wymuszania zasad dotyczących kondycji klienta ochrony dostępu do sieci (NAP), które określają, czy urządzenia uzyskują dostęp do nieograniczonego lub ograniczonego toonetwork zasobów.
* Podaj oznacza tooenforce uwierzytelniania i autoryzacji dla punktów dostępu bezprzewodowego z obsługą too802.1x dostępu i przełączników Ethernet.    

Aby uzyskać więcej informacji, zobacz [serwera zasad sieciowych (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

tooenhance zabezpieczeń i zapewnia wysoki poziom zgodności, organizacje mogą stosować serwera NPS za pomocą usługi Azure MFA tooensure, czy użytkownicy przy użyciu weryfikacji dwuetapowej toobe mogli połączyć toohello portu wirtualnego na powitania serwera sieci VPN. Dla użytkowników toobe prawa dostępu użytkownik musi podać ich kombinacja nazwy użytkownika i hasła, informacje, które hello użytkownika ma ich formantu. Te informacje musi być zaufany i nie jest łatwo zduplikowany, takie jak numer telefonu komórkowego, numer telefonu stacjonarnego aplikacji na urządzeniu przenośnym i tak dalej.

Dostępność wcześniejsze toohello hello rozszerzenia serwera zasad Sieciowych na platformie Azure, klientów, którzy zamierza tooimplement weryfikacji dwuetapowej dla zintegrowany serwera zasad Sieciowych i środowisk usługi Azure MFA ma tooconfigure i obsługa osobny serwer usługi MFA w środowisku lokalne powitania jako opisano w bramy usług pulpitu zdalnego i Azure przy użyciu usługi RADIUS serwera Multi-Factor Authentication.

dostępność Hello hello rozszerzenia serwera zasad Sieciowych na platformie Azure daje obecnie toodeploy wybór hello organizacje lokalne rozwiązanie MFA lub oparte na chmurze usługi MFA rozwiązania toosecure RADIUS uwierzytelniania klienta.
 
## <a name="authentication-flow"></a>Przepływ uwierzytelniania
Gdy użytkownik łączy tooa portu wirtualnego na serwerze sieci VPN, muszą najpierw zostać uwierzytelnione przy użyciu różnych protokołów, które umożliwiają użycie hello kombinacji nazwy użytkownika i hasła i metody uwierzytelniania opartego na certyfikatach. 

W tooauthenticating dodawania i weryfikowania tożsamości użytkownicy muszą mieć hello odpowiednie uprawnienia. W przypadku prostych implementacji te uprawnienia umożliwiające dostęp są ustawiane bezpośrednio na obiekty użytkownika usługi Active Directory hello. 

 ![Właściwości użytkownika](./media/nps-extension-vpn/image1.png)

W przypadku prostych implementacji każdy serwer sieci VPN lub go przydziela nie zezwala na dostęp na podstawie zasad zdefiniowanych każdego lokalnego serwera sieci VPN.

W implementacji większych i bardziej skalowalne hello zasady tego Udziel lub Odmów dostępu do sieci VPN są scentralizowane na serwerach usługi RADIUS. W takim przypadku serwer sieci VPN hello działa jako serwer dostępu (klienta RADIUS), który przesyła dalej żądań połączenia i serwera RADIUS tooa wiadomości konta. tooconnect toohello wirtualnego portu na powitania serwera sieci VPN, użytkownicy muszą zostać uwierzytelnione i spełniać warunki hello definiowane centralnie na serwerach usługi RADIUS. 

Gdy hello rozszerzenia serwera zasad Sieciowych na platformie Azure jest zintegrowany z powitania serwera NPS, hello pomyślne uwierzytelnienie przebieg jest następujący:

1. serwer sieci VPN Hello otrzymuje żądanie uwierzytelnienia od użytkownik sieci VPN, który zawiera hello nazwy użytkownika i hasła tooconnect tooa zasobu, takiego jak sesji pulpitu zdalnego. 
2. Działając jako klient usługi RADIUS, serwer sieci VPN konwertuje komunikat żądania dostępu RADIUS tooa żądania hello i wiadomość hello wysyła (hasło jest szyfrowane) serwera RADIUS (NPS) toohello zainstalowanym hello rozszerzenia serwera NPS. 
3. Witaj nazwy użytkownika i sprawdzeniu kombinacja hasła w usłudze Active Directory. Jeśli hello nazwy użytkownika / hasło jest nieprawidłowe, powitania serwera RADIUS wysyła komunikat odmowy dostępu. 
4. Jeśli wszystkie warunki jako określone w hello żądanie połączenia serwera zasad Sieciowych i zasady sieciowe są spełnione (na przykład pory dnia lub grupy ograniczeniami członkostwa), żądania uwierzytelniania dodatkowego z usługą Azure MFA wyzwala hello rozszerzenia serwera NPS. 
5. Usługa Azure MFA komunikuje się z usługą Azure Active Directory, pobiera szczegóły hello użytkownika, a następnie wykonuje hello dodatkowego uwierzytelniania przy użyciu metody hello skonfigurowany przez użytkownika hello (wiadomości tekstowej, aplikacji mobilnych itd.). 
6. Na powodzenie hello żądanie uwierzytelniania MFA usługi Azure MFA komunikuje się hello wynik toohello NPS rozszerzenia.
7. Po próba połączenia hello zarówno uwierzytelnieniu i autoryzacji, którym zainstalowano rozszerzenia powitania serwera NPS hello wysyła akceptacji dostępu RADIUS komunikat toohello serwer sieci VPN (klienta RADIUS).
8. Hello użytkownik uzyskuje dostęp do wirtualnego portu toohello na serwer sieci VPN i ustanawia szyfrowane tunel VPN.

## <a name="prerequisites"></a>Wymagania wstępne
Ta sekcja zawiera szczegóły dotyczące wymagania wstępne hello konieczne przed Integrowanie usługi Azure MFA z hello bramy usług pulpitu zdalnego. Przed rozpoczęciem, musi mieć hello następujące wymagania wstępne w miejscu.

* Infrastrukturę sieci VPN.
* Rola zasad sieciowych i dostępu do usługi (NPS)
* Licencja usługi Azure MFA
* Oprogramowanie Windows Server
* Biblioteki
* Zsynchronizowane usługi Azure AD z lokalnej usługi AD 
* Identyfikator GUID usługi Azure Active Directory

### <a name="vpn-infrastructure"></a>Infrastrukturę sieci VPN.
W tym artykule założono, że pracy infrastruktury sieci VPN przy użyciu systemu Microsoft Windows Server 2016 w miejscu i tego serwera sieci VPN hello jest obecnie serwer RADIUS tooa żądań połączenia tooforward skonfigurowany. Skonfiguruj toouse infrastruktury sieci VPN hello centralnego serwera RADIUS w tym przewodniku.

Jeśli nie masz infrastruktury pracę w miejscu, tej infrastruktury może szybko utworzyć według poniższych wskazówek hello w wielu samouczków ustawienia sieci VPN, z którymi można znaleźć na powitania firmy Microsoft i innych witryn. 

### <a name="network-policy-and-access-services-nps-role"></a>Rola zasad sieciowych i dostępu do usługi (NPS)

Witaj usługi roli serwera NPS zawiera powitania serwera usługi RADIUS i funkcji klienta. W tym artykule przyjęto założenie, że zainstalowano rolę serwera zasad Sieciowych hello na serwer członkowski lub kontroler domeny w danym środowisku. Konfiguracji usługi RADIUS dla konfiguracji sieci VPN, w tym przewodniku. Zainstaluj rolę serwera zasad Sieciowych hello na serwerze _innych_ niż serwer sieci VPN.

Informacje na temat instalowania roli serwera NPS hello usługi systemu Windows Server 2012 lub nowszym, zobacz [zainstalować serwer zasad dotyczących kondycji ochrony dostępu do sieci](https://technet.microsoft.com/library/dd296890.aspx). Zasady dostępu do sieci (NAP) jest przestarzała w systemie Windows Server 2016. Opis najlepszych rozwiązań dla serwera zasad Sieciowych, takie jak hello zalecenie tooinstall serwera NPS na kontrolerze domeny, zobacz [najlepsze rozwiązania dotyczące serwera NPS](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licencje

Wymagana jest licencja dla usługi Azure MFA, który jest dostępny za pośrednictwem usługi Azure AD Premium, Enterprise Mobility plus Security (EMS) lub subskrypcji usługi MFA. Aby uzyskać więcej informacji, zobacz [jak tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md). Do celów testowych, możesz użyć subskrypcji wersji próbnej.

### <a name="software"></a>Oprogramowanie

Witaj rozszerzenia serwera NPS wymaga systemu Windows Server 2008 R2 z dodatkiem SP1 lub nowszy z zainstalowaną usługą roli serwera NPS hello. Wszystkie kroki hello w tym przewodniku były wykonywane przy użyciu systemu Windows Server 2016.

### <a name="libraries"></a>Biblioteki

wymagane są następujące dwie biblioteki Hello:

* [Pakiety redystrybucyjne języka Visual C++ dla programu Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Microsoft Azure Active Directory modułu dla Windows PowerShell w wersji 1.1.166.0_ lub nowszej. Witaj najnowszej wersji i instrukcje dotyczące instalacji, zobacz [Microsoft Azure Active Directory środowiska PowerShell modułu wersji Historia wersji](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Te biblioteki nie są dostarczane z powitania serwera NPS rozszerzenia plików Instalatora (wersja 0.9.1.2), pomimo istniejąca dokumentacja stwierdzający, w przeciwnym razie wartość. Co najmniej należy zainstalować hello pakiety Visual C++ Redistributable dla Visual Studio 2013. zainstalowano Hello Microsoft Azure Active Directory modułu dla środowiska Windows PowerShell, jeśli nie jest już obecny za pomocą skryptu konfiguracji uruchomienia w ramach procesu instalacji hello. Brak tooinstall nie konieczności ten moduł wcześniej, jeśli nie jest już zainstalowany.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Usługa Azure Active Directory zsynchronizowane z lokalną usługą Active Directory 

toouse hello rozszerzenia serwera NPS lokalnych użytkowników musi być zsynchronizowane z usługą Azure Active Directory i włączone uwierzytelnianie wieloskładnikowe. W tym przewodniku założono, że użytkowników lokalnych są zsynchronizowane z usługą Azure Active Directory za pomocą AD Connect. Instrukcje dotyczące włączania uwierzytelniania Wieloskładnikowego użytkownicy znajdują się poniżej.
Aby uzyskać informacje dotyczące usługi Azure AD connect, zobacz [integrację katalogów lokalnych z usługą Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Identyfikator GUID usługi Azure Active Directory 
tooinstall hello serwera NPS należy tooknow hello GUID hello Azure Active Directory. Instrukcje dotyczące znajdowania hello GUID hello Azure Active Directory znajdują się w następnej sekcji hello.

## <a name="configure-radius-for-vpn-connections"></a>Konfigurowanie serwera RADIUS dla połączeń sieci VPN

Po zainstalowaniu roli serwera NPS hello na serwerze członkowskim, należy tooconfigure tooauthenticate i autoryzować klienta sieci VPN, które żądania połączenia sieci VPN. 

W tej sekcji założono instalacji roli serwera zasad sieciowych hello, ale nie skonfigurowano go do użytku w infrastrukturze.

>[!NOTE]
>Jeśli masz już działający serwer sieci VPN do uwierzytelniania używa centralny serwer usługi RADIUS, możesz pominąć tę sekcję.
>

### <a name="register-server-in-active-directory"></a>Zarejestruj serwer w usłudze Active Directory
toofunction prawidłowo w tym scenariuszu, serwer zasad Sieciowych hello musi toobe zarejestrowane w usłudze Active Directory.

1. Otwórz Menedżera serwera.
2. W Menedżerze serwera kliknij **narzędzia**, a następnie kliknij przycisk **serwera zasad sieciowych**. 
3. W konsoli serwera zasad sieciowych hello, kliknij prawym przyciskiem myszy **serwer NPS (lokalny)**, a następnie kliknij przycisk **Zarejestruj serwer w usłudze Active Directory**. Kliknij przycisk **OK** dwa razy.

 ![Serwer zasad sieciowych](./media/nps-extension-vpn/image2.png)

4. Pozostaw otwarte do następnej procedury hello hello konsoli.

### <a name="use-wizard-tooconfigure-radius-server"></a>Użyj Kreatora tooconfigure RADIUS serwera
Można użyć standardowego (opartej na kreatorze) lub serwera RADIUS hello tooconfigure opcji konfiguracji zaawansowanej. W tej sekcji założono użycie hello hello opartej na Kreatorze konfiguracji standardowej opcji.

1. W konsoli serwera zasad sieciowych powitania kliknij **serwer NPS (lokalny)**.
2. W obszarze konfiguracji standardowej, wybierz **serwera RADIUS w celu telefonicznych i połączeń sieci VPN**, a następnie kliknij przycisk **Konfigurowanie sieci VPN lub Dial-Up**.

 ![Konfigurowanie sieci VPN](./media/nps-extension-vpn/image3.png)

3. Na powitania wybierz telefonicznych lub typu połączenia sieci prywatnej wirtualnego stronie zaznacz **połączenia wirtualnej sieci prywatnej**i kliknij przycisk **dalej**.

 ![Wirtualna sieć prywatna](./media/nps-extension-vpn/image4.png)

4. Na stronie Określ Dial-Up lub serwer VPN powitania kliknij **Dodaj**.
5. W hello **klienta RADIUS nowe** okno dialogowe, Podaj przyjazną nazwę, wprowadź hello rozpoznawalną nazwę lub adres IP serwera VPN hello i wprowadź tajny wspólne hasło. Należy to wspólne hasło tajny długich i złożonych. Zapisz to hasło, odpowiednio do potrzeb w następnej sekcji hello krokach.

 ![Nowy klient RADIUS](./media/nps-extension-vpn/image5.png)

6. Kliknij przycisk **OK**, a następnie **dalej**.
7. Na powitania **Konfigurowanie metod uwierzytelniania** Zaakceptuj wybór domyślny hello (uwierzytelnianie szyfrowane firmy Microsoft w wersji 2 (MS-CHAPv2) lub wybierz inną opcję i kliknij przycisk **dalej**.

  >[!NOTE]
  >Jeśli konfigurujesz protokołu uwierzytelniania rozszerzonego (EAP), należy używać MS-CHAPv2 lub PEAP. Nie protokołu EAP jest obsługiwana.
 
8. Na stronie Określ grupy użytkowników powitania kliknij **Dodaj** i wybierz odpowiednią grupę, jeśli taka istnieje. W przeciwnym razie pozostaw zaznaczenie hello puste toogrant tooall użytkowników.

 ![Określ grupy użytkowników](./media/nps-extension-vpn/image7.png)

9. Kliknij przycisk **Dalej**.
10. Na stronie określ filtry IP powitania kliknij **dalej**.
11. Na stronie Określ ustawienia szyfrowania hello zaakceptować ustawienia domyślne hello, a następnie kliknij przycisk **dalej**.

 ![Określ szyfrowania](./media/nps-extension-vpn/image8.png)

12. Na powitania Określ nazwę obszaru puste nazwy hello, zaakceptuj ustawienia domyślne hello, a następnie kliknij przycisk **dalej**.

 ![Określ nazwę obszaru](./media/nps-extension-vpn/image9.png)

13. Kliknij hello Kończenie nowego telefoniczne lub połączenia wirtualnej sieci prywatnej i RADIUS strony klienci **Zakończ**.

 ![Zakończenie połączenia](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Sprawdź konfigurację usługi RADIUS
Ta sekcja zawiera szczegóły dotyczące konfiguracji hello zostały utworzone za pomocą Kreatora hello.

1. Na serwerze NPS hello, w konsoli serwera NPS (lokalny) hello, rozwiń klientów usługi RADIUS, a następnie wybierz **klientów RADIUS**.
2. W okienku szczegółów hello, kliknij prawym przyciskiem myszy powitania klienta RADIUS zostały utworzone za pomocą kreatora, a następnie kliknij przycisk **właściwości**. właściwości powitania klienta RADIUS (powitania serwera sieci VPN) powinny być podobne toothose pokazano poniżej.

 ![Właściwości sieci VPN](./media/nps-extension-vpn/image11.png)

3. Kliknij przycisk **anulować**.
4. Na serwerze NPS hello, w konsoli serwera NPS (lokalny) hello, rozwiń węzeł **zasady**i wybierz **zasady żądań połączeń**. Powinny pojawić się hello zasad połączeń sieci VPN, podobny hello obraz poniżej.

 ![Żądania połączeń](./media/nps-extension-vpn/image12.png)

5. W obszarze zasady, wybierz **zasady sieciowe**. Należy przypominający poniższy obraz powitania zasady połączenia wirtualnej sieci prywatnej (VPN).

 ![Właściwości sieci](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>Skonfiguruj uwierzytelnianie usługi RADIUS toouse serwer sieci VPN
W tej sekcji możesz skonfigurować uwierzytelnianie usługi RADIUS toouse serwera sieci VPN hello. W tej sekcji założono mają działającej konfiguracji serwera sieci VPN, ale nie skonfigurowano uwierzytelnianie usługi RADIUS toouse serwera sieci VPN hello. Po skonfigurowaniu serwera sieci VPN hello, potwierdź, że konfigurację działa zgodnie z oczekiwaniami.

>[!NOTE]
>Jeśli masz już działającej konfiguracji serwera sieci VPN korzysta z uwierzytelniania usługi RADIUS, możesz pominąć tę sekcję.
>

### <a name="configure-authentication-provider"></a>Konfigurowanie dostawcy uwierzytelniania
1. Na powitania serwera sieci VPN Otwórz Menedżera serwera.
2. W Menedżerze serwera kliknij **narzędzia**, a następnie **Routing i dostęp zdalny**.
3. W konsoli Routing i dostęp zdalny hello, kliknij prawym przyciskiem myszy  **\[nazwy serwera\] (local)**, a następnie kliknij przycisk **właściwości**.

 ![Routing i dostęp zdalny](./media/nps-extension-vpn/image14.png)
 
4. W hello **[właściwości Name Server} (lokalne)** okna dialogowego kliknij hello **zabezpieczeń** kartę. 
5. Na powitania **zabezpieczeń** kliknij kartę, w obszarze dostawcy uwierzytelniania **uwierzytelnianie usługi RADIUS**, a następnie **Konfiguruj**.

 ![Uwierzytelnianie usługi RADIUS](./media/nps-extension-vpn/image15.png)
 
6. W powitalne okno dialogowe uwierzytelnianie usługi RADIUS, kliknij przycisk **Dodaj**.
7. W hello Dodaj serwer usługi RADIUS, w polu Nazwa serwera, Dodaj hello nazwa lub hello adres IP serwera RADIUS hello skonfigurowanych w poprzedniej sekcji hello.
8. W wspólny klucz tajny kliknij **zmiany** i Dodaj hello udostępnionych poufne hasło utworzone i zarejestrowane wcześniej.
9. W limitu czasu (w sekundach), zmień wartość tooa wartość hello między **30** i **60**. Jest to niezbędne tooallow wystarczająco dużo czasu toocomplete hello drugi składnik uwierzytelniania.
 
 ![Dodawanie serwera RADIUS](./media/nps-extension-vpn/image16.png)
 
10. Kliknij przycisk **OK** dopiero po wykonaniu zamknięcie wszystkich okien dialogowych.

### <a name="test-vpn-connectivity"></a>Przetestowanie łączności z siecią VPN
W tej sekcji Potwierdź uwierzytelnieniu i autoryzacji przez serwer RADIUS hello, podczas próby portu wirtualnego tooVPN tooconnect powitania klienta sieci VPN. W tej sekcji założono, że używasz systemu Windows 10 jako klient sieci VPN. 

>[!NOTE]
>Jeśli już skonfigurowany serwer sieci VPN toohello tooconnect klienta sieci VPN i zapisaniu hello ustawienia, można pominąć tooconfiguring powiązanych kroków hello i zapisywanie obiektu połączenia sieci VPN.
>

1. Na komputerze klienckim sieci VPN kliknij **Start**, a następnie **ustawienia** (koło zębate ikonę).
2. W oknie Ustawienia, kliknij przycisk **sieć i Internet**.
3. Kliknij przycisk **VPN**.
4. Kliknij przycisk **dodać połączenie VPN**.
5. W dodać połączenia VPN, określ systemu Windows (wbudowane) jako hello dostawcy sieci VPN, a następnie pełną hello pozostałych pól, zgodnie z potrzebami i kliknij **zapisać**. 

 ![Dodaj połączenie VPN](./media/nps-extension-vpn/image17.png)
 
6. Otwórz hello **Centrum sieci i udostępniania** w Panelu sterowania.
7. Kliknij przycisk **Zmień ustawienia karty**.

 ![Zmień ustawienia karty sieciowej](./media/nps-extension-vpn/image18.png)

8. Kliknij prawym przyciskiem myszy połączenie sieci VPN hello, a następnie kliknij przycisk Właściwości. 

 ![Właściwości sieci VPN](./media/nps-extension-vpn/image19.png)

9. W powitalne okno dialogowe właściwości sieci VPN, kliknij przycisk hello **zabezpieczeń** kartę. 
10. Na karcie Zabezpieczenia hello, upewnij się, że tylko **Microsoft CHAP Version 2 (MS-CHAP v2)** jest zaznaczone, a następnie kliknij przycisk OK.

 ![Zezwolić protokołów](./media/nps-extension-vpn/image20.png)

11. Kliknij prawym przyciskiem myszy połączenie sieci VPN hello, a następnie kliknij przycisk **Connect**.
12. Na stronie Ustawienia powitania kliknij **Connect**.

Udane połączenie zostanie wyświetlony w dzienniku zabezpieczeń hello na powitania serwera RADIUS jako 6272 identyfikator zdarzenia, jak pokazano poniżej.

 ![Właściwości zdarzenia](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Rozwiązywanie problemów z przewodnika
Załóżmy, że przed skonfigurowaniem toouse serwera sieci VPN hello scentralizowanego serwera RADIUS w celu uwierzytelniania i autoryzacji pracy konfigurację sieci VPN. W takim przypadku istnieje prawdopodobieństwo, że hello problem może być spowodowany konfiguracji powitania serwera RADIUS lub hello użycia nieprawidłowej nazwy użytkownika lub hasła. Na przykład, jeśli używasz hello alternatywny sufiks nazwy UPN użytkownika hello hello próba logowania może zakończyć się niepowodzeniem (należy używać tej samej nazwy konta dla uzyskania najlepszych wyników hello). 

te problemy, toostart doskonale nadaje się jest dziennikami zdarzeń zabezpieczeń hello tooexamine na tootroubleshoot hello serwera RADIUS. toosave czas wyszukiwania dla zdarzeń, można użyć hello opartej na rolach zasad sieciowych i dostępu do serwera niestandardowego widoku w Podglądzie zdarzeń, jako wyświetlane poniżej. Identyfikator zdarzenia 6273 wskazuje, gdzie hello serwera zasad sieciowych odmowa dostępu użytkownika tooa zdarzenia. 

 ![Podgląd zdarzeń](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Skonfiguruj usługę Multi-Factor Authentication
Ta sekcja zawiera instrukcje dotyczące włączania użytkowników dla usługi MFA i konfigurowanie kont na potrzeby weryfikacji dwuetapowej. 

### <a name="enable-multi-factor-authentication"></a>Włączanie uwierzytelniania wieloskładnikowego
W tej sekcji można włączyć konta usługi Azure AD MFA. Użyj hello **klasyczny portal** tooenable użytkowników dla usługi MFA. 

1. Otwórz przeglądarkę i przejdź zbyt[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Zaloguj się jako hello administrator.
3. W portalu hello, w lewym panelu nawigacyjnym powitania kliknij **usługi ACTIVE DIRECTORY**.

 ![Domyślny katalog](./media/nps-extension-vpn/image23.png)

4. Witaj nazwa kolumny, kliknij przycisk **katalog domyślny** (lub innego katalogu, w razie potrzeby).
5. Na stronie Szybki Start powitania kliknij **Konfiguruj**.

 ![Konfigurowanie domyślnych](./media/nps-extension-vpn/image24.png)

6. Na stronie Konfiguruj hello, przewiń w dół i, w sekcji uwierzytelnianie wieloskładnikowe powitania kliknij **Zarządzaj ustawieniami usługi**.

 ![Zarządzaj ustawieniami usługi MFA](./media/nps-extension-vpn/image25.png)
 
7. Na stronie uwierzytelnianie wieloskładnikowe hello, przejrzyj hello domyślnych ustawień usługi, a następnie kliknij **użytkowników**. 

 ![Użytkownicy usługi MFA](./media/nps-extension-vpn/image26.png)
 
8. Na stronie powitania użytkowników wybierz hello użytkownicy mają tooenable dla usługi MFA, a następnie kliknij przycisk **włączyć**.

 ![Właściwości](./media/nps-extension-vpn/image27.png)
 
9. Po wyświetleniu monitu kliknij przycisk **Włącz uwierzytelnianie wieloskładnikowe**.

 ![Włączenie uwierzytelniania MFA](./media/nps-extension-vpn/image28.png)
 
10. Kliknij przycisk **Zamknij**. 
11. Odśwież stronę hello. Witaj stan uwierzytelniania Wieloskładnikowego jest tooEnabled zmienione.

Aby uzyskać informacje dotyczące użytkowników tooenable uwierzytelnianie wieloskładnikowe, zobacz [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Konfigurowanie konta na potrzeby weryfikacji dwuetapowej
Po włączeniu konta dla usługi MFA, użytkownicy nie są możliwe toosign w tooresources objętej zasad MFA hello aż pomyślnie skonfigurowano toouse zaufanego urządzenia, dla hello drugi składnik uwierzytelniania o używane weryfikacji dwuetapowej.

W tej sekcji skonfigurujesz zaufanego urządzenia do użycia w trakcie weryfikacji dwuetapowej. Dostępnych jest kilka opcji dostępnych dla tooconfigure można je w tym następujących hello:

* **Aplikacja mobilna**. Należy zainstalować aplikację Microsoft Authenticator hello na urządzeniu Windows Phone, Android lub iOS. W zależności od zasad organizacji są wymagane toouse aplikacji hello w jednym z dwóch trybów: otrzymywać powiadomienia na potrzeby weryfikacji (powiadomienie jest wypychane urządzenia tooyour) lub użyj kodu weryfikacyjnego (wymagane są kod tooenter weryfikacji Aktualizuje co 30 sekund). 
* **Telefonu komórkowego połączenia lub wiadomości SMS**. Można albo otrzymywać automatyczne połączenia telefonicznego lub wiadomości SMS. Z opcją połączenia telefonicznego hello odpowiedzi na wywołanie hello i naciśnij klawisz tooauthenticate znak # hello. Z opcją tekst hello możesz Odpowiedz na wiadomość SMS toohello lub wprowadź kod weryfikacyjny hello na powitania w interfejsie logowania.
* **Z telefonem biurowym**. Ten proces jest hello taki sam jak opisana na automatyczne połączenia telefoniczne powyżej.

Wykonaj te instrukcje dotyczące konfigurowania urządzenia toouse hello aplikacji mobilnej tooreceive powiadomienie wypychane do weryfikacji.

1. Zaloguj się za[https://aka.ms/mfasetup](https://aka.ms/mfasetup) lub dowolnej lokacji, takich jak [https://portal.azure.com](https://portal.azure.com), gdzie wymagane tooauthenticate przy użyciu poświadczeń konta z obsługą uwierzytelniania Wieloskładnikowego. 
2. Po zarejestrowaniu się przy użyciu nazwy użytkownika i hasła, są prezentowane ekran z monitem o tooset konto hello dodatkowej weryfikacji zabezpieczeń.

 ![Dodatkowe zabezpieczenia](./media/nps-extension-vpn/image29.png)

3. Kliknij przycisk **teraz skonfigurować**.
4. Na stronie weryfikacji dodatkowe zabezpieczenia hello wybierz typ kontaktu (numer telefonu uwierzytelniania, telefon biurowy lub aplikacja mobilna). Następnie wybierz kraj lub region, a następnie wybierz metodę. Metoda Hello jest zależna od wybranego typu skontaktuj się z pomocą. Na przykład jeśli aplikacja mobilna, można wybrać czy tooreceive powiadomień o weryfikacji lub toouse kod weryfikacyjny. Witaj czynności, które wykonują założono, możesz wybrać **aplikacji mobilnej** hello typ kontaktu.

 ![Telefonu uwierzytelniania](./media/nps-extension-vpn/image30.png)

5. Wybierz aplikację mobilną, kliknij przycisk **otrzymywać powiadomienia na potrzeby weryfikacji**, a następnie **Konfigurowanie**. 

 ![Weryfikacja aplikacji mobilnej](./media/nps-extension-vpn/image31.png)
 
6. Jeśli jeszcze tego nie zrobiono tego wcześniej, należy zainstalować aplikację mobilną Witaj wystawca uwierzytelnienia na urządzeniu. 
7. Wykonaj te instrukcje hello hello tooscan aplikacji mobilnej hello przedstawiony kod kreskowy lub ręcznie wprowadzić informacje o hello, a następnie kliknij **gotowe**.

 ![Konfigurowanie aplikacji mobilnej](./media/nps-extension-vpn/image32.png)

8. Na stronie weryfikacji dodatkowe zabezpieczenia powitania kliknij **kontaktu mnie** i urządzenia tooyour toonotification wysyłane odpowiedzi.
9. Na stronie weryfikacji dodatkowe zabezpieczenia hello, wprowadź numer kontaktowy na wypadek utraty aplikacji mobilnej toohello dostęp i kliknij przycisk **dalej**.

 ![Numer telefonu komórkowego](./media/nps-extension-vpn/image33.png)
 
10. Na powitania dodatkowej weryfikacji zabezpieczeń, kliknij przycisk **gotowe**.

urządzenie Hello jest teraz skonfigurowany tooprovide drugi metody weryfikacji. Aby uzyskać informacje na temat konfigurowania konta na potrzeby weryfikacji dwuetapowej, zobacz [Skonfiguruj moje konto na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Instalowanie i Konfigurowanie rozszerzeń serwera NPS

Ta sekcja zawiera instrukcje dotyczące konfigurowania sieci VPN toouse usługi Azure MFA do uwierzytelniania klientów z powitania serwera sieci VPN.

Po zainstalowaniu i skonfigurowaniu rozszerzenia serwera NPS hello, wszystkie uwierzytelnianie klienta usługi RADIUS, który jest przetwarzany przez ten serwer jest wymagane toouse usługi Azure MFA. Jeśli nie wszystkich użytkowników sieci VPN są zarejestrowane w usłudze Azure MFA, możesz skonfigurować innego serwera RADIUS serwera tooauthenticate użytkowników, którzy nie są skonfigurowane toouse MFA. Lub utworzyć wpis rejestru, który umożliwia tooprovide kwestionowane użytkowników drugi składnik uwierzytelniania tylko wtedy, gdy są one rejestrowane w MFA. 

Utwórz nową wartość ciągu o nazwie _REQUIRE_USER_MATCH w HKLM\SOFTWARE\Microsoft\AzureMfa_i ustaw tooTRUE wartość hello, lub FAŁSZ. 

 ![Wymagaj dopasowania użytkownika](./media/nps-extension-vpn/image34.png)
 
Jeśli wartość hello jest tooTRUE zestawu lub nie jest ustawiona, wszystkie żądania uwierzytelniania są żądanie uwierzytelniania MFA tooan podmiotu. Jeśli hello jest wartość tooFALSE, wyzwania MFA są wystawiane tylko toousers, które są rejestrowane w MFA. Należy używać tylko hello ustawienie FALSE podczas testowania lub w środowiskach produkcyjnych w okresie dołączania.

### <a name="acquire-azure-active-directory-guid-id"></a>Uzyskać identyfikator GUID usługi Azure Active Directory

W ramach konfiguracji hello hello rozszerzenia serwera zasad Sieciowych należy toosupply poświadczenia administratora i hello identyfikator usługi Azure Active Directory dla dzierżawy usługi Azure AD. w poniższych krokach Hello przedstawiono, jak identyfikator tooget hello dzierżawy.

1. Zaloguj się toohello portalu Azure w [https://portal.azure.com](https://portal.azure.com) jako administrator globalny hello hello Azure dzierżawy.
2. W hello lewy pasek nawigacyjny, kliknij przycisk hello **usługi Azure Active Directory** ikony.
3. Kliknij pozycję **Właściwości**.
4. toocopy Twojego Schowka toohello identyfikator katalogu, wybierz hello **kopiowania** ikony.
 
 ![Identyfikator katalogu](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Zainstaluj rozszerzenie serwera NPS hello
Witaj rozszerzenia serwera zasad Sieciowych musi toobe zainstalowane na serwerze, który ma hello zasad sieciowych i zainstalowaną rolą usług dostępu (NPS) i tej funkcji jako serwer RADIUS hello w projekcie. Nie należy instalować hello rozszerzenia serwera NPS na serwerze usług pulpitu zdalnego.

1. Pobierz rozszerzenie serwera NPS hello z [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Skopiuj serwera NPS toohello hello instalacji pliku wykonywalnego (NpsExtnForAzureMfaInstaller.exe).
3. Na powitania serwera NPS, kliknij dwukrotnie **NpsExtnForAzureMfaInstaller.exe**. Jeśli zostanie wyświetlony monit, kliknij przycisk **Uruchom**.
4. W hello NPS rozszerzenia dla usługi Azure MFA — okno dialogowe, przejrzyj hello postanowienia licencyjne dotyczące oprogramowania, sprawdź **akceptuję postanowienia licencyjne toohello**i kliknij przycisk **zainstalować**.

 ![Rozszerzenia serwera NPS](./media/nps-extension-vpn/image36.png)
 
5. Na powitania serwera NPS rozszerzenia dla usługi Azure MFA — okno dialogowe, kliknij **Zamknij**.  

 ![Instalator pomyślnie](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Konfigurowanie certyfikatów do użytku z rozszerzeniem NPS hello za pomocą skryptu programu PowerShell
tooensure bezpieczną komunikację i zapewnienia należy tooconfigure certyfikatów do użytku przez rozszerzenie serwera NPS hello. składniki serwera NPS Hello obejmują skrypt programu Windows PowerShell, który konfiguruje certyfikatu z podpisem własnym do użytku z serwera NPS. 

skrypt Hello wykonuje hello następujące akcje:

* Tworzy certyfikat z podpisem własnym
* Kojarzy klucz publiczny certyfikatu tooservice podmiotu zabezpieczeń w usłudze Azure AD
* Magazyny hello certyfikatu w magazynie komputera lokalnego hello
* Przyznaje dostęp do certyfikatu toohello toohello klucza prywatnego użytkownika sieci
* Uruchamia ponownie usługę Serwer zasad sieciowych

Jeśli chcesz toouse własne certyfikaty wymagają publicznego hello tooassociate zasady usługi toohello Twojego certyfikatu w usłudze Azure AD i tak dalej.
skrypt hello toouse, podaj hello rozszerzenia przy użyciu poświadczeń administracyjnych usługi Azure Active Directory i hello wcześniej zostały skopiowane Identyfikatora dzierżawy usługi Azure Active Directory. Uruchom skrypt hello na każdym serwerze NPS, w którym zainstalowano rozszerzenia serwera NPS hello.

1. Otwórz administracyjny wiersz środowiska Windows PowerShell.
2. W wierszu polecenia programu PowerShell hello, wpisz _cd "c:\Program Files\Microsoft\AzureMfa\Config"_i naciśnij klawisz **ENTER**.
3. Typ _.\AzureMfsNpsExtnConfigSetup.ps1_i naciśnij klawisz **ENTER**. 
 * skrypt Hello sprawdza toosee po zainstalowaniu hello modułu programu PowerShell usługi Azure Active Directory. Jeśli nie jest zainstalowany, skrypt hello zainstaluje hello modułu.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Po hello skrypt sprawdza hello instalacji modułu PowerShell hello, wyświetla okno dialogowe hello modułu programu PowerShell usługi Azure Active Directory. Okno dialogowe hello, wprowadź poświadczenia administratora usługi Azure AD i hasło, a następnie kliknij przycisk **Zaloguj**. 
 
 ![Logowanie do programu PowerShell](./media/nps-extension-vpn/image39.png)
 
5. Po wyświetleniu monitu Wklej identyfikator dzierżawcy hello wcześniej zostały skopiowane toohello Schowka i naciśnij klawisz **ENTER**. 

 ![Identyfikator dzierżawy](./media/nps-extension-vpn/image40.png)

6. Witaj skrypt tworzy certyfikat z podpisem własnym i wykonuje inne zmiany w konfiguracji. dane wyjściowe Hello przypomina obraz powitania pokazano poniżej.

 ![Certyfikatu z podpisem własnym](./media/nps-extension-vpn/image41.png)

7. Uruchom ponownie serwer hello.
 
### <a name="verify-configuration"></a>Weryfikowanie konfiguracji
tooverify hello konfiguracji, należy tooestablish nowego połączenia sieci VPN z serwerem sieci VPN. Po pomyślnym wprowadzania poświadczeń dla uwierzytelniania podstawowego, hello połączenia sieci VPN przed oczekuje na powitania toosucceed dodatkowego uwierzytelniania hello połączenie zostanie nawiązane, jak pokazano poniżej. 

 ![Weryfikowanie konfiguracji](./media/nps-extension-vpn/image42.png)

Jeśli zostanie pomyślnie uwierzytelniony przy użyciu metody dodatkowej weryfikacji hello, wcześniej skonfigurowane w usłudze Azure MFA, to toohello połączonych zasobów. Jednak jeśli hello dodatkowego uwierzytelniania zakończy się niepowodzeniem, nie będzie mógł tooresource dostępu. 

W przykładzie hello poniżej Witaj wystawca uwierzytelnienia aplikacji w systemie Windows phone jest używane tooprovide hello dodatkowego uwierzytelniania.

 ![Sprawdź konto](./media/nps-extension-vpn/image43.png)

Po zostały pomyślnie uwierzytelniony przy użyciu metody pomocnicze hello, są przyznawane toohello dostęp do wirtualnego portu na powitania serwera sieci VPN. Jednak ponieważ były wymagane toouse dodatkowej metody uwierzytelniania przy użyciu aplikacji mobilnej na zaufanym urządzeniu dziennika hello w procesie jest bardziej bezpieczne, nie może być używa tylko nazwy użytkownika / kombinacja hasła.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Sprawdź dzienniki Podglądu zdarzeń dla zdarzeń pomyślnego logowania
tooview hello zdarzeń pomyślnego logowania w dziennikach podglądu zdarzeń systemu Windows hello, można wystawiać powitania po dziennika tooquery polecenia programu Windows PowerShell zabezpieczenia systemu Windows hello na powitania serwera NPS.

tooquery zdarzeń pomyślnego logowania w dziennikach podglądu zdarzeń zabezpieczeń hello, użyj hello następujące polecenie,
* _Get-WinEvent - Nazwa_dziennika zabezpieczeń_ | gdzie {$_.ID - eq "6272"} | FL 

 ![Podgląd zdarzeń zabezpieczeń](./media/nps-extension-vpn/image44.png)
 
Możesz również wyświetlić dziennika zabezpieczeń hello lub hello usług zasad sieciowych i dostępu widok niestandardowy, jak pokazano poniżej:

 ![Dostęp do zasad sieci](./media/nps-extension-vpn/image45.png)

Na powitania serwera, w którym zainstalowano rozszerzenia serwera NPS powitania dla usługi Azure MFA, można znaleźć dzienniki Podglądu zdarzeń aplikacji toohello określonego rozszerzenia w **aplikacji i usług Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent - Nazwa_dziennika zabezpieczeń_ | gdzie {$_.ID - eq "6272"} | FL

 ![Liczba zdarzeń (event)](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Rozwiązywanie problemów z przewodnika
Jeśli konfiguracja hello nie działa zgodnie z oczekiwaniami, tootroubleshoot toostart dobrym miejscem jest tooverify, który hello użytkownika jest skonfigurowane toouse usługi Azure MFA. Użytkownik hello połączyć za[https://portal.azure.com](https://portal.azure.com). Jeśli monit o podanie dodatkowego uwierzytelniania i można pomyślnie uwierzytelnić, można wyeliminować niepoprawnej konfiguracji usługi Azure MFA.

Jeśli usługi Azure MFA działa dla użytkowników hello, należy przejrzeć dzienniki zdarzeń z odpowiednich hello. Obejmują one dzienników zdarzeń zabezpieczeń, brama operacyjne i usługi Azure MFA hello omówione w poprzedniej sekcji hello. 

Poniżej przedstawiono przykładowe dane wyjściowe dziennika zabezpieczeń przedstawiający zdarzenia logowania nie powiodło się (6273 identyfikator zdarzenia):

 ![Dziennik zabezpieczeń](./media/nps-extension-vpn/image47.png)

Poniżej znajdują się zdarzenia związane z dzienników AzureMFA hello:

 ![Dzienniki usługi Azure MFA](./media/nps-extension-vpn/image48.png)

tooperform Zaawansowane rozwiązywanie problemów z opcjami, należy zapoznać się z hello NPS format plików dziennika bazy danych zainstalowanym hello usługi zasad Sieciowych. Te pliki dziennika są tworzone w _%SystemRoot%\System32\Logs_ folderu plików tekstowych rozdzielanych przecinkami. Aby uzyskać opis tych plików dziennika, zobacz [zinterpretować pliki dziennika Format bazy danych serwera NPS](https://technet.microsoft.com/library/cc771748.aspx). 

wpisy Hello w tych plikach dziennika są trudne toointerpret bez importowania ich do arkusza kalkulacyjnego lub bazy danych. Można odnaleźć numeru z usługi IAS analizatory składni online tooassist przy interpretowaniu hello plików dziennika. Poniżej przedstawiono dane wyjściowe hello jednego takiego do pobrania [aplikacji "shareware"](http://www.deepsoftware.com/iasviewer): 

 ![Aplikacja "shareware"](./media/nps-extension-vpn/image49.png)

Na koniec, aby uzyskać dodatkowe Rozwiązywanie problemów z opcjami, możesz użyć analizatora protokołów, takich jak Wireshark lub [programu Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). Hello poniższy obraz z programu Wireshark przedstawia wiadomości powitania RADIUS między serwerem sieci VPN hello i powitania serwera NPS.

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

Aby uzyskać więcej informacji, zobacz [integracji istniejącej infrastrukturze serwera NPS z usługi Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Następne kroki
[Jak tooget uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)

[Brama usług pulpitu zdalnego i serwer Azure Multi-Factor Authentication korzystające z usługi RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrowanie katalogów lokalnych z usługą Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

