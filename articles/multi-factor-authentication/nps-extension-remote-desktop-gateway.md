---
title: "aaaRemote bramy usług pulpitu Integracja z usługą Azure MFA NPS rozszerzenia | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono integrowanie infrastruktury bramy usług pulpitu zdalnego z usługą Azure MFA przy użyciu rozszerzenia serwera zasad sieciowych (NPS) hello platformy Microsoft Azure."
services: active-directory
keywords: "Usługa Azure MFA, integracja bramy usług pulpitu zdalnego, Azure Active Directory, serwer zasad sieciowych rozszerzenia"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Integrowanie infrastruktury bramy usług pulpitu zdalnego za pomocą hello rozszerzenia serwera zasad sieciowych (NPS) i Azure AD

Ten artykuł zawiera szczegółowe informacje dla integrowanie infrastruktury bramy usług pulpitu zdalnego z usługi Azure Multi-Factor Authentication (MFA) przy użyciu rozszerzenia serwera zasad sieciowych (NPS) hello platformy Microsoft Azure. 

Umożliwia Hello rozszerzenia usługi zasad sieciowych (NPS) na platformie Azure przez klientów toosafeguard serwera usługi użytkowników zdalnego uwierzytelniania (RADIUS) uwierzytelniania klienta za pomocą usługi Azure opartej na chmurze [Multi-Factor Authentication (MFA)](multi-factor-authentication.md). To rozwiązanie zapewnia weryfikację dwuetapową dodawania drugą warstwę logowania toouser zabezpieczeń i transakcji.

Ten artykuł zawiera instrukcje krok po kroku do integracji z usługą Azure MFA hello infrastruktury serwera NPS przy użyciu rozszerzenia zasad Sieciowych hello na platformie Azure. Dzięki temu weryfikacji dla użytkowników próbujących toolog na tooa bramy usług pulpitu zdalnego. 

Hello zasad sieciowych i dostępu do usługi (NPS) umożliwia organizacjom hello możliwości toodo hello poniżej:
* Definiowanie centralnej lokalizacji hello zarządzania i kontroli żądania sieci, określając, kto może się połączyć, jakich porach dnia mogą przyjmować połączenia hello czas trwania połączenia i hello poziom zabezpieczeń, czy klienci muszą używać tooconnect i tak dalej. Zamiast określenia tych zasad na każdym serwerze sieci VPN lub bramy usług pulpitu zdalnego (RD), te zasady można określić jeden raz w centralnej lokalizacji. Witaj protokołu RADIUS zapewnia hello scentralizowane uwierzytelnianie, autoryzację i Ewidencjonowanie. 
* Ustanów i wymuszania zasad dotyczących kondycji klienta ochrony dostępu do sieci (NAP), które określają, czy urządzenia uzyskują dostęp do nieograniczonego lub ograniczonego toonetwork zasobów.
* Podaj oznacza tooenforce uwierzytelniania i autoryzacji dla punktów dostępu bezprzewodowego z obsługą too802.1x dostępu i przełączników Ethernet.    

Zazwyczaj organizacji używać toosimplify serwera zasad Sieciowych (RADIUS) i scentralizowane zarządzanie hello VPN zasady. Jednak w wielu organizacjach również użyć toosimplify serwera zasad Sieciowych i scentralizowane zarządzanie hello zasady autoryzacji połączeń usług pulpitu usług pulpitu zdalnego (RD CAP). 

Organizacje mogą również integracji z usługą Azure MFA tooenhance zabezpieczeń serwera NPS i zapewniają wysoki poziom zgodności. Pomaga to zapewnić, że użytkownicy ustanowić toolog weryfikacji dwuetapowej na toohello bramy usług pulpitu zdalnego. Dla użytkowników toobe prawa dostępu użytkownik musi podać ich kombinacja nazwy użytkownika i hasła, informacje, które hello użytkownika ma ich formantu. Te informacje musi być zaufany i nie jest łatwo zduplikowany, takie jak numer telefonu komórkowego, numer telefonu stacjonarnego aplikacji na urządzeniu przenośnym i tak dalej.

Dostępność wcześniejsze toohello hello rozszerzenia serwera zasad Sieciowych na platformie Azure, klientów, którzy zamierza tooimplement weryfikacji dwuetapowej dla zintegrowany serwera zasad Sieciowych i środowisk usługi Azure MFA ma tooconfigure i obsługa osobny serwer usługi MFA w środowisku lokalne powitania jako w [bramy usług pulpitu zdalnego i Azure przy użyciu usługi RADIUS serwera Multi-Factor Authentication](multi-factor-authentication-get-started-server-rdg.md).

dostępność Hello hello rozszerzenia serwera zasad Sieciowych na platformie Azure daje obecnie toodeploy wybór hello organizacje lokalne rozwiązanie MFA lub oparte na chmurze usługi MFA rozwiązania toosecure RADIUS uwierzytelniania klienta.

## <a name="authentication-flow"></a>Przepływ uwierzytelniania

Dla użytkowników toobe przyznano dostęp do zasobów toonetwork za pośrednictwem bramy usług pulpitu zdalnego, muszą spełniać warunki hello określone w jednej usług pulpitu zdalnego zasady autoryzacji połączeń (RD CAP) i jeden usług pulpitu zdalnego zasady autoryzacji zasobów (RD RAP). Zasady RD CAP Określ, kto jest autoryzowany tooconnect tooRD bram. Zasady RD RAP Określ hello zasobów sieciowych, takich jak usługa Pulpit zdalny lub aplikacji zdalnych, ten użytkownik hello jest dozwolone tooconnect toothrough hello bramy usług pulpitu zdalnego. 

Brama usług pulpitu zdalnego może być skonfigurowany toouse sklepu centralne zasady dla RD CAP. Zasady RD RAP nie można użyć centralnych zasad, jak są przetwarzane na powitania bramy usług pulpitu zdalnego. Przykładem toouse bramy usług pulpitu zdalnego skonfigurowane sklepu centralne zasady dla RD CAP jest serwera NPS tooanother klienta RADIUS, który służy jako hello centralne zasady magazynu.

Gdy hello rozszerzenia serwera zasad Sieciowych na platformie Azure są zintegrowane z powitania serwera zasad Sieciowych i bramy usług pulpitu zdalnego, hello pomyślne uwierzytelnienie przebieg jest następujący:

1. serwer bramy usług pulpitu zdalnego Hello odbiera żądanie uwierzytelnienia z zasobu tooa tooconnect użytkownika pulpitu zdalnego, takich jak sesji pulpitu zdalnego. Działając jako klient usługi RADIUS, serwera bramy usług pulpitu zdalnego hello konwertuje komunikat żądania dostępu RADIUS tooa żądania hello i wysyła serwera RADIUS (NPS) toohello wiadomość hello zainstalowanym hello rozszerzenia serwera NPS. 
2. Witaj nazwy użytkownika i kombinacja hasła jest zweryfikowana w usłudze Active Directory i hello użytkownik jest uwierzytelniony.
3. Jeśli hello wszystkie warunki określone w hello żądanie połączenia serwera zasad Sieciowych i zasad sieci hello są spełnione (na przykład pory dnia lub grupy ograniczeniami członkostwa), żądania uwierzytelniania dodatkowego z usługą Azure MFA wyzwala hello rozszerzenia serwera NPS. 
4. Usługa Azure MFA komunikuje się z usługą Azure AD, pobiera szczegóły hello użytkownika, a następnie wykonuje hello dodatkowego uwierzytelniania przy użyciu metody hello skonfigurowany przez użytkownika hello (wiadomości tekstowej, aplikacji mobilnych itd.). 
5. Na powodzenie hello żądanie uwierzytelniania MFA usługi Azure MFA komunikuje się hello wynik toohello NPS rozszerzenia.
6. serwer NPS Hello zainstalowanym rozszerzenia hello wysyła komunikat akceptacji dostępu usługi RADIUS dla serwera bramy usług pulpitu zdalnego toohello zasad dotyczących hello RD CAP.
7. Witaj, użytkownik otrzymuje dostęp toohello żądanego zasobu sieciowego za pomocą hello bramy usług pulpitu zdalnego.

## <a name="prerequisites"></a>Wymagania wstępne
Ta sekcja zawiera szczegóły dotyczące wymagania wstępne hello konieczne przed Integrowanie usługi Azure MFA z hello bramy usług pulpitu zdalnego. Przed rozpoczęciem, musi mieć hello następujące wymagania wstępne w miejscu.  

* Infrastruktura usług pulpitu zdalnego
* Licencja usługi Azure MFA
* Oprogramowanie Windows Server
* Rola zasad sieciowych i dostępu do usługi (NPS)
* Zsynchronizowane usługi Azure AD z lokalnej usługi AD 
* Identyfikator GUID usługi Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infrastruktura usług pulpitu zdalnego
W miejscu musi mieć działający infrastruktury usług pulpitu zdalnego (RDS). Jeśli nie, a następnie tej infrastruktury może szybko utworzyć na platformie Azure przy użyciu następujących hello szybki start szablonu: [wdrażania Utwórz kolekcję sesji pulpitu zdalnego](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

W razie potrzeby toomanually utworzyć RDS infrastruktury lokalnej szybko podczas testowania, wykonaj hello kroki toodeploy jeden. 
**Dowiedz się więcej**: [wdrożenia usług pulpitu zdalnego z szybki start Azure](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) i [RDS podstawowe wdrożenie infrastruktury](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Licencje
Wymagana jest licencja dla usługi Azure MFA, który jest dostępny za pośrednictwem usługi Azure AD Premium, Enterprise Mobility plus Security (EMS) lub subskrypcji usługi MFA. Aby uzyskać więcej informacji, zobacz [jak tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md). Do celów testowych, możesz użyć subskrypcji wersji próbnej.

### <a name="software"></a>Oprogramowanie
Witaj rozszerzenia serwera NPS wymaga systemu Windows Server 2008 R2 z dodatkiem SP1 lub nowszy z zainstalowaną usługą roli serwera NPS hello. Wszystkie kroki hello w tej sekcji zostały wykonywane przy użyciu systemu Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>Rola zasad sieciowych i dostępu do usługi (NPS)
Hello usługi roli serwera NPS zawiera powitania serwera usługi RADIUS i klienta, funkcje, a także zasady dostępu do sieci usługi kondycji. Musi być zainstalowana rola to na co najmniej dwa komputery w infrastrukturze: hello bramy usług pulpitu zdalnego i drugi serwer członkowski lub kontroler domeny. Domyślnie roli hello jest już obecny na powitania komputer skonfigurowany jako hello bramy usług pulpitu zdalnego.  Również zainstalowanie roli serwera NPS hello na co najmniej na innym komputerze, takich jak kontroler domeny lub serwer członkowski.

Aby uzyskać informacje na temat instalowania roli serwera NPS hello usługi systemu Windows Server 2012 lub starszy, zobacz [zainstalować serwer zasad dotyczących kondycji ochrony dostępu do sieci](https://technet.microsoft.com/library/dd296890.aspx). Opis najlepszych rozwiązań dla serwera zasad Sieciowych, takie jak hello zalecenie tooinstall serwera NPS na kontrolerze domeny, zobacz [najlepsze rozwiązania dotyczące serwera NPS](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Usługa Azure Active Directory zsynchronizowane z lokalną usługą Active Directory 
toouse hello rozszerzenia serwera NPS lokalnych użytkowników muszą być zsynchronizowane z usługą Azure AD i włączyć usługę MFA. W tej sekcji założono, że użytkowników lokalnych są zsynchronizowane z usługą Azure AD za pomocą AD Connect. Aby uzyskać informacje dotyczące usługi Azure AD connect, zobacz [integrację katalogów lokalnych z usługą Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Identyfikator GUID usługi Azure Active Directory
tooinstall serwera NPS należy tooknow hello GUID hello Azure AD. Instrukcje dotyczące znajdowania hello GUID hello Azure AD znajdują się poniżej.

## <a name="configure-multi-factor-authentication"></a>Skonfiguruj usługę Multi-Factor Authentication 
Ta sekcja zawiera instrukcje dotyczące integrowania usługi Azure MFA z hello bramy usług pulpitu zdalnego. Jako administrator należy skonfigurować usługę Azure MFA hello zanim użytkownicy będą mogli samodzielnie zarejestrować ich wieloskładnikowego urządzenia lub aplikacji.

Wykonaj kroki hello w [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](multi-factor-authentication-get-started-cloud.md) tooenable uwierzytelnianie wieloskładnikowe dla użytkowników usługi Azure AD. 

### <a name="configure-accounts-for-two-step-verification"></a>Konfigurowanie konta na potrzeby weryfikacji dwuetapowej
Gdy konta została włączona dla usługi MFA, nie możesz zarejestrować się tooresources podlega postanowieniom hello zasad MFA aż pomyślnie zostały skonfigurowane toouse zaufanego urządzenia dla hello drugi składnik uwierzytelniania został uwierzytelniony przy użyciu weryfikacji dwuetapowej.

Wykonaj kroki hello w [co oznacza Azure Multi-Factor Authentication dla mnie?](./end-user/multi-factor-authentication-end-user.md) toounderstand i poprawnie skonfigurować urządzenia dla usługi MFA z kontem użytkownika.

## <a name="install-and-configure-nps-extension"></a>Instalowanie i Konfigurowanie rozszerzeń serwera NPS
Ta sekcja zawiera instrukcje dotyczące konfigurowania usługi pulpitu zdalnego toouse infrastruktury usługi Azure MFA do uwierzytelniania klientów z hello bramy usług pulpitu zdalnego.

### <a name="acquire-azure-active-directory-guid-id"></a>Uzyskać identyfikator GUID usługi Azure Active Directory

W ramach konfiguracji hello hello rozszerzenia serwera zasad Sieciowych należy toosupply poświadczenia administratora i hello identyfikator usługi Azure AD dla dzierżawy usługi Azure AD. Hello następujące kroki pokazują, jak identyfikator tooget hello dzierżawy.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator globalny hello hello Azure dzierżawy.
2. Lewy pasek nawigacyjny hello, wybierz hello **usługi Azure Active Directory** ikony.
3. Wybierz **właściwości**.
4. W bloku właściwości hello obok hello identyfikator katalogu, kliknij przycisk hello **kopiowania** ikony, jak pokazano poniżej toocopy hello identyfikator tooclipboard.

 ![Właściwości](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Zainstaluj rozszerzenie serwera NPS hello
Zainstaluj rozszerzenie serwera NPS hello na serwerze, który ma hello zasad sieciowych i zainstalowaną rolą usług dostępu (NPS). Ta działa jako serwer RADIUS hello projekt. 

>[!Important]
> Upewnij się, że rozszerzenie serwera NPS hello nie należy instalować na serwerze bramy usług pulpitu zdalnego.
> 

1. Pobierz hello [rozszerzenia serwera NPS](https://aka.ms/npsmfa). 
2. Skopiuj serwera NPS toohello hello instalacji pliku wykonywalnego (NpsExtnForAzureMfaInstaller.exe).
3. Na powitania serwera NPS, kliknij dwukrotnie **NpsExtnForAzureMfaInstaller.exe**. Jeśli zostanie wyświetlony monit, kliknij przycisk **Uruchom**.
4. W hello NPS rozszerzenia dla usługi Azure MFA — okno dialogowe, przejrzyj hello postanowienia licencyjne dotyczące oprogramowania, sprawdź **akceptuję postanowienia licencyjne toohello**i kliknij przycisk **zainstalować**.
 
  ![Instalator usługi Azure MFA](./media/nps-extension-remote-desktop-gateway/image2.png)

5. W hello NPS rozszerzenia dla usługi Azure MFA — okno dialogowe kliknij przycisk Zamknij. 

  ![Rozszerzenia serwera zasad Sieciowych na potrzeby usługi Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Konfigurowanie certyfikatów do użytku z rozszerzeniem NPS hello za pomocą skryptu programu PowerShell
Następnie należy tooconfigure certyfikaty dla powitania serwera NPS rozszerzenia tooensure bezpieczną komunikację i gwarancji. składniki serwera NPS Hello obejmują skrypt programu Windows PowerShell, który konfiguruje certyfikatu z podpisem własnym do użytku z serwera NPS. 

skrypt Hello wykonuje hello następujące akcje:

* Tworzy certyfikat z podpisem własnym
* Kojarzy klucz publiczny certyfikatu tooservice podmiotu zabezpieczeń w usłudze Azure AD
* Magazyny hello certyfikatu w magazynie komputera lokalnego hello
* Przyznaje dostęp użytkownika sieci toohello klucza prywatnego certyfikatu toohello
* Uruchamia ponownie usługę Serwer zasad sieciowych

Jeśli chcesz toouse własne certyfikaty wymagają publicznego hello tooassociate zasady usługi toohello Twojego certyfikatu w usłudze Azure AD i tak dalej.

skrypt hello toouse, podaj hello rozszerzenia przy użyciu poświadczeń usługi Azure AD administratora i hello Identyfikatora dzierżawy usługi Azure AD, które wcześniej zostały skopiowane. Uruchom skrypt hello na każdym serwerze NPS, w którym zainstalowano rozszerzenia serwera NPS hello. Następnie hello następujące:

1. Otwórz administracyjny wiersz środowiska Windows PowerShell.
2. W wierszu polecenia programu PowerShell hello, wpisz **cd "c:\Program Files\Microsoft\AzureMfa\Config"**i naciśnij klawisz **ENTER**.
3. Typ _.\AzureMfsNpsExtnConfigSetup.ps1_i naciśnij klawisz **ENTER**. skrypt Hello sprawdza toosee po zainstalowaniu hello modułu programu PowerShell usługi Azure Active Directory. Jeśli nie jest zainstalowany, skrypt hello zainstaluje hello modułu.

  ![Program Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Po hello skrypt sprawdza hello instalacji modułu PowerShell hello, wyświetla okno dialogowe hello modułu programu PowerShell usługi Azure Active Directory. Okno dialogowe hello, wprowadź poświadczenia administratora usługi Azure AD i hasło, a następnie kliknij przycisk **logowania**.

  ![Konta programu Powershell](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Po wyświetleniu monitu Wklej identyfikator dzierżawcy hello wcześniej zostały skopiowane toohello Schowka i naciśnij klawisz **ENTER**.

  ![Wprowadź identyfikator dzierżawy](./media/nps-extension-remote-desktop-gateway/image6.png)

6. Witaj skrypt tworzy certyfikat z podpisem własnym i wykonuje inne zmiany w konfiguracji. dane wyjściowe Hello powinna być takich jak obraz powitania pokazano poniżej.

  ![Certyfikatu z podpisem własnym](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Konfigurowanie składników serwera NPS na bramy usług pulpitu zdalnego
W tej sekcji skonfigurujesz zasady autoryzacji połączeń bramy usług pulpitu zdalnego hello i inne ustawienia usługi RADIUS.

Przepływ uwierzytelniania Hello wymaga, aby komunikaty RADIUS być wymieniane między hello bramy usług pulpitu zdalnego i powitania serwera NPS zainstalowanym powitania serwera NPS. Oznacza to, że należy skonfigurować ustawienia klientów usługi RADIUS na serwerze NPS bramy usług pulpitu zdalnego i hello, zainstalowanym hello rozszerzenia serwera NPS. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Konfigurowanie bramy usług pulpitu zdalnego połączenia autoryzacji zasady toouse centralnego magazynu
Zasady autoryzacji połączeń usług pulpitu zdalnego (RD CAP) określ hello wymagania dotyczące łączenia tooa bramy usług pulpitu zdalnego serwera. Zasady RD CAP mogą być przechowywane lokalnie (ustawienie domyślne) lub mogą być przechowywane w centralnym magazynie RD CAP, który jest uruchomiony serwer zasad Sieciowych. tooconfigure integracji usługi Azure MFA z usług pulpitu zdalnego, należy toospecify hello Użyj centralnego magazynu.

1. Na serwerze bramy usług pulpitu zdalnego hello Otwórz **Menedżera serwera**. 
2. Menu hello, kliknij przycisk **narzędzia**, punktu zbyt**usług pulpitu zdalnego**, a następnie kliknij przycisk **Menedżera bramy usług pulpitu zdalnego**.

  ![Usługi pulpitu zdalnego](./media/nps-extension-remote-desktop-gateway/image8.png)

3. W hello Menedżer bramy usług pulpitu zdalnego, kliknij prawym przyciskiem myszy  **\[nazwy serwera\] (Local)**i kliknij przycisk **właściwości**.

  ![Nazwa serwera](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Okno dialogowe właściwości hello, wybierz hello **RD CAP** kartę magazynu.
5. Na karcie magazynu zasad RD CAP hello wybierz **centralnym serwerze NPS**. 
6. W hello **powitania serwera NPS wprowadź nazwę lub adres IP** pole, typ hello adresu IP lub serwera nazwy serwera hello, w którym zainstalowano rozszerzenia serwera NPS hello.

  ![Wprowadź nazwę lub adres IP](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Kliknij pozycję **Dodaj**.
8. W hello **wspólny klucz tajny** okno dialogowe, wpisz wspólny klucz tajny, a następnie kliknij przycisk **OK**. Upewnij się, Zapisz ten wspólny klucz tajny i bezpieczne przechowywanie hello rekordu.

 >[!NOTE]
 >Wspólny klucz tajny jest używany tooestablish zaufania między serwerami usługi RADIUS hello i klientami. Utwórz hasło długich i złożonych.
 >

 ![Wspólny klucz tajny](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Kliknij przycisk **OK** hello tooclose — okno dialogowe.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Skonfiguruj wartość limitu czasu usługi RADIUS na zdalnego pulpitu bramy serwera zasad Sieciowych
tooensure jest czas poświadczeń użytkowników toovalidate, przeprowadzenia weryfikacji dwuetapowej, odbierania odpowiedzi i odpowiadać tooRADIUS wiadomości, jest konieczne tooadjust hello RADIUS limit czasu.

1. Na powitania serwera bramy usług pulpitu zdalnego, w Menedżerze serwera kliknij **narzędzia**, a następnie kliknij przycisk **serwera zasad sieciowych**. 
2. W hello **serwer NPS (lokalny)** rozwiń **klientów usługi RADIUS i serwerach**i wybierz **serwera RADIUS**.

 ![Serwer zdalny RADIUS](./media/nps-extension-remote-desktop-gateway/image12.png)

3. W okienku szczegółów hello, kliknij dwukrotnie **grupy serwerów bramy usług terminalowych**.

 >[!NOTE]
 >Tej grupy serwerów usługi RADIUS został utworzony podczas konfigurowania serwera centralnego hello w celu zasady serwera NPS. Witaj bramy usług pulpitu zdalnego przekazuje serwera toothis wiadomości usługi RADIUS lub grupy serwerów, w przypadku więcej niż jednej grupy hello.
 >

4. W hello **właściwości grupy serwerów bramy usług terminalowych** okno dialogowe, wybierz hello adres IP lub nazwę hello serwer zasad Sieciowych skonfigurowany toostore RD CAP, a następnie kliknij przycisk **Edytuj**. 

 ![Grupy serwerów bramy usług terminalowych](./media/nps-extension-remote-desktop-gateway/image13.png)

5. W hello **edytowanie serwera RADIUS** okno dialogowe, wybierz opcję hello **równoważenia obciążenia** kartę.
6. W hello **równoważenia obciążenia** na karcie hello **liczba sekund bez odpowiedzi, zanim żądanie zostanie uznane za** pola, zmień wartość domyślną hello z 3 tooa wartość z zakresu od 30 do 60 sekund.
7. W hello **liczba sekund między żądaniami, gdy serwer jest identyfikowany jako niedostępny** pola, zmień wartość domyślną wartość tooa 30 sekund, która jest większa niż wartość hello określona w poprzednim kroku hello równy tooor hello.

 ![Edytowanie serwera Radius](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Kliknij przycisk OK, dwa razy tooclose hello okien dialogowych.

### <a name="verify-connection-request-policies"></a>Sprawdź zasady żądań połączeń 
Domyślnie podczas konfigurowania hello bramy usług pulpitu zdalnego toouse sklepu centralne zasady dla zasady autoryzacji połączeń, hello bramy usług pulpitu zdalnego jest serwer NPS toohello tooforward skonfigurowanych zakończenia żądania. powitania serwera NPS z rozszerzeniem usługi Azure MFA hello zainstalowane, żądanie dostępu RADIUS hello procesów. Hello następujące kroki pokazują, jak tooverify hello domyślne połączenie żądania zasad. 

1. Na powitania bramy usług pulpitu zdalnego, w konsoli serwera NPS (lokalny) hello, rozwiń **zasady**i wybierz **zasady żądań połączeń**.
2. Kliknij prawym przyciskiem myszy **Połącz zasady żądań**, a następnie kliknij dwukrotnie **zasady autoryzacji bramy serwera terminali**.
3. W hello **właściwości zasad autoryzacji bramy serwera terminali** okna dialogowego kliknij hello **ustawienia** kartę.
4. Na **ustawienia** kliknij kartę, w obszarze przesyłanie dalej żądania połączenia **uwierzytelniania**. Klienta RADIUS jest skonfigurowany tooforward żądania uwierzytelniania.

 ![Ustawienia uwierzytelniania](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Kliknij przycisk **anulować**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Konfigurowanie serwera NPS na serwerze hello zainstalowanym hello rozszerzenia serwera NPS
serwer NPS Hello hello rozszerzenia serwera NPS w przypadku potrzeby zainstalowanych toobe stanie tooexchange RADIUS wiadomości z powitania serwera NPS na powitania bramy usług pulpitu zdalnego. tooenable ten komunikat programu exchange, należy tooconfigure hello NPS składników na serwerze hello zainstalowanym hello usługi rozszerzenia serwera NPS. 

### <a name="register-server-in-active-directory"></a>Zarejestruj serwer w usłudze Active Directory
toofunction prawidłowo w tym scenariuszu, serwer zasad Sieciowych hello musi toobe zarejestrowane w usłudze Active Directory.

1. Otwórz **Menedżera serwera**.
2. W Menedżerze serwera kliknij **narzędzia**, a następnie kliknij przycisk **serwera zasad sieciowych**. 
3. W konsoli serwera zasad sieciowych hello, kliknij prawym przyciskiem myszy **serwer NPS (lokalny)**, a następnie kliknij przycisk **Zarejestruj serwer w usłudze Active Directory**. 
4. Kliknij przycisk **OK** dwa razy.

 ![Zarejestruj serwer w usłudze AD](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Pozostaw otwarte do następnej procedury hello hello konsoli.

### <a name="create-and-configure-radius-client"></a>Tworzenie i konfigurowanie klienta RADIUS 
Witaj bramy usług pulpitu zdalnego wymaga toobe skonfigurowany jako serwer NPS toohello klienta RADIUS. 

1. Na serwerze NPS hello, którym jest zainstalowany hello rozszerzenia serwera NPS, w hello **serwer NPS (lokalny)** konsoli, kliknij prawym przyciskiem myszy **klientów RADIUS** i kliknij przycisk **nowy**.

 ![Nowi klienci usługi RADIUS](./media/nps-extension-remote-desktop-gateway/image17.png)

2. W hello **klienta RADIUS nowe** okna dialogowego wprowadź przyjazną nazwę, taką jak _bramy_, i hello adres IP lub nazwa DNS serwera bramy usług pulpitu zdalnego hello. 
3. W hello **wspólne hasło** i hello **Potwierdź wspólny klucz tajny** wprowadź hello tego samego hasła używanego wcześniej.

 ![Nazwy i adresu](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Kliknij przycisk **OK** okno dialogowe tooclose hello RADIUS nowego klienta.

### <a name="configure-network-policy"></a>Konfigurowanie zasad sieciowych
Serwer NPS hello odwołania z hello rozszerzenia usługi Azure MFA jest hello magazynu wyznaczonego centralne zasady dla hello zasady autoryzacji połączeń (CAP). W związku z tym należy tooimplement ograniczenie w odpowiedzi na powitania serwera NPS serwera tooauthorize prawidłowych połączeń żądania.  

1. W konsoli serwera NPS (lokalny) hello rozwiń **zasady**i kliknij przycisk **zasady sieciowe**.
2. Kliknij prawym przyciskiem myszy **serwerów dostępu tooother połączeń**i kliknij przycisk **zduplikowane zasad**. 

 ![Zduplikowana zasad](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Kliknij prawym przyciskiem myszy **serwerów dostępu kopiowania połączeń tooother**i kliknij przycisk **właściwości**.

 ![Właściwości sieci](./media/nps-extension-remote-desktop-gateway/image20.png)

4. W hello **serwerów dostępu kopiowania połączeń tooother** okno dialogowe, w polu Nazwa zasady wprowadź odpowiednią nazwę, taką jak **RDG_CAP**. Sprawdź **zasady włączone**i wybierz **udzielić dostępu**. Opcjonalnie w polu Typ dostępu do sieci, wybierz **bramy usług pulpitu zdalnego**, można także pozostawić go jako **nieokreślony**.

 ![Kopiowanie połączeń](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Kliknij przycisk hello **ograniczenia** i sprawdź **Zezwalaj klientom tooconnect bez negocjowania metodę uwierzytelniania**.

 ![Zezwalaj klientom tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Opcjonalnie kliknij hello **warunki** karta i Dodaj warunki, które muszą zostać spełnione w przypadku toobe połączenia hello autoryzacji, na przykład członkostwa w określonej grupie systemu Windows.

 ![Warunki](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Kliknij przycisk **OK**. Gdy zostanie wyświetlony monit o tooview hello odpowiedni temat pomocy, kliknij przycisk **nr**.
8. Upewnij się, że nowych zasad jest u góry hello listy hello, że hello jest włączona, i że przyznaje ona dostęp.

 ![Zasady sieciowe](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Weryfikowanie konfiguracji
tooverify hello konfiguracji, należy toolog na powitania bramy usług pulpitu zdalnego za pomocą odpowiedniego klienta RDP. Można toouse się, że konto, które jest dozwolona przez użytkownika zasady autoryzacji połączeń i jest włączone dla usługi Azure MFA. 

Pokaż w hello obraz poniżej, można użyć hello **Remote Web Access pulpitu** strony.

![Dostęp w sieci Web do usług pulpitu zdalnego](./media/nps-extension-remote-desktop-gateway/image25.png)

Po pomyślnym wprowadzania poświadczeń dla uwierzytelniania podstawowego, stan inicjowania połączenia zdalnego wyświetlane okno dialogowe połączenie pulpitu zdalnego hello, jak pokazano poniżej. 

Jeśli zostanie pomyślnie uwierzytelniony z hello dodatkowej metody uwierzytelniania wcześniej skonfigurowane w usłudze Azure MFA, to toohello połączonych zasobów. Jednak jeśli hello dodatkowego uwierzytelniania zakończy się niepowodzeniem, nie będzie mógł tooresource dostępu. 

![Inicjowanie połączenia zdalnego](./media/nps-extension-remote-desktop-gateway/image26.png)

W przykładzie hello poniżej Witaj wystawca uwierzytelnienia aplikacji w systemie Windows phone jest używane tooprovide hello dodatkowego uwierzytelniania.

![Konta](./media/nps-extension-remote-desktop-gateway/image27.png)

Po zostały pomyślnie uwierzytelniony przy użyciu hello dodatkowej metody uwierzytelniania, którego jest się zalogowanym hello bramy usług pulpitu zdalnego, jak zwykle. Jednak ponieważ są wymagane toouse dodatkowej metody uwierzytelniania przy użyciu aplikacji mobilnej na zaufanym urządzeniu, procesu logowania hello jest bezpieczniejsza niż jest to.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Sprawdź dzienniki Podglądu zdarzeń dla zdarzeń pomyślnego logowania
tooview hello pomyślnego logowania zdarzeń w dziennikach podglądu zdarzeń systemu Windows hello, można wystawiać hello następującego polecenia programu Windows PowerShell, tooquery hello usług terminalowych systemu Windows i dzienniki zabezpieczeń systemu Windows.

tooquery pomyślnego logowania zdarzenia operacyjne dzienniki bramy hello _(Viewer\Applications zdarzeń i usług Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, użyj następującego polecenia hello:

* _Get-WinEvent - Nazwa_dziennika Microsoft-Windows-TerminalServices — bramy/operacyjnej_ | gdzie {$_.ID - eq "300"} | FL 
* To polecenie wyświetla zdarzeń systemu Windows, przedstawiających hello użytkownika zostały spełnione wymagania dotyczące zasad autoryzacji zasobów (RD RAP) i przyznano dostęp.

![Wyświetl podgląd zdarzeń](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent - Nazwa_dziennika Microsoft-Windows-TerminalServices — bramy/operacyjnej_ | gdzie {$_.ID - eq "200"} | FL
* To polecenie wyświetla zdarzenia hello, których wyświetlane, gdy użytkownik spełnione wymagania zasad autoryzacji połączeń.

![Autoryzacja połączeń](./media/nps-extension-remote-desktop-gateway/image29.png)

Można również wyświetlić ten dziennik i filtr na identyfikatorów, 300 i 200 zdarzeń. tooquery zdarzeń pomyślnego logowania w dziennikach podglądu zdarzeń zabezpieczeń hello, użyj hello następujące polecenie:

* _Get-WinEvent - Nazwa_dziennika zabezpieczeń_ | gdzie {$_.ID - eq "6272"} | FL 
* To polecenie można uruchomić na jednym hello centralnej serwera NPS lub hello serwera bramy usług pulpitu zdalnego. 

![Zdarzeń pomyślnego logowania](./media/nps-extension-remote-desktop-gateway/image30.png)

Możesz również wyświetlić dziennika zabezpieczeń hello lub hello usług zasad sieciowych i dostępu widok niestandardowy, jak pokazano poniżej:

![Usługi zasad sieciowych i dostępu](./media/nps-extension-remote-desktop-gateway/image31.png)

Na powitania serwera, w którym zainstalowano rozszerzenia serwera NPS powitania dla usługi Azure MFA, można znaleźć dzienniki Podglądu zdarzeń aplikacji toohello określonego rozszerzenia w _aplikacji i usług Logs\Microsoft\AzureMfa_. 

![Dzienniki aplikacji Podgląd zdarzeń](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Rozwiązywanie problemów z przewodnika

Jeśli konfiguracja hello nie działa zgodnie z oczekiwaniami, hello pierwszym miejscu toostart tootroubleshoot jest tooverify, który hello użytkownika jest skonfigurowane toouse usługi Azure MFA. Użytkownik hello połączyć toohello [portalu Azure](https://portal.azure.com). Jeśli użytkownicy są monitowani o podanie dodatkowej weryfikacji i można pomyślnie uwierzytelnić, można wyeliminować niepoprawnej konfiguracji usługi Azure MFA.

Jeśli usługi Azure MFA działa dla użytkowników hello, należy przejrzeć dzienniki zdarzeń z odpowiednich hello. Obejmują one dzienników zdarzeń zabezpieczeń, brama operacyjne i usługi Azure MFA hello omówione w poprzedniej sekcji hello. 

Poniżej przedstawiono przykładowe dane wyjściowe dziennika zabezpieczeń przedstawiający zdarzenia logowania nie powiodło się (6273 identyfikator zdarzenia).

![Zdarzenia logowania nie powiodło się](./media/nps-extension-remote-desktop-gateway/image33.png)

Poniżej znajdują się zdarzenia związane z dzienników AzureMFA hello:

![Dzienników usługi Azure MFA](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform Zaawansowane rozwiązywanie problemów z opcjami, należy zapoznać się z hello NPS format plików dziennika bazy danych zainstalowanym hello usługi zasad Sieciowych. Te pliki dziennika są tworzone w _%SystemRoot%\System32\Logs_ folderu plików tekstowych rozdzielanych przecinkami. 

Aby uzyskać opis tych plików dziennika, zobacz [zinterpretować pliki dziennika Format bazy danych serwera NPS](https://technet.microsoft.com/library/cc771748.aspx). wpisy Hello w tych plikach dziennika może być trudne toointerpret bez importowania ich do arkusza kalkulacyjnego lub bazy danych. Można znaleźć kilka IAS analizatory składni online tooassist przy interpretowaniu hello plików dziennika. 

Witaj obraz poniżej przedstawia hello dane wyjściowe jednego takiego do pobrania [aplikacji "shareware"](http://www.deepsoftware.com/iasviewer). 

![Aplikacja "shareware"](./media/nps-extension-remote-desktop-gateway/image35.png)

Na koniec, aby uzyskać dodatkowe Rozwiązywanie problemów z opcjami, możesz użyć analizatora protokołów, takich [programu Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). 

Witaj obraz poniżej z programu Microsoft Message Analyzer przedstawia ruch sieciowy filtrowane wg protokołu RADIUS, zawierający nazwę użytkownika hello **Contoso\AliceC**.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Następne kroki
[Jak tooget uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)

[Brama usług pulpitu zdalnego i serwer Azure Multi-Factor Authentication korzystające z usługi RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrowanie katalogów lokalnych z usługą Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
