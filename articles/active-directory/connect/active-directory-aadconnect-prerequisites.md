---
title: "Azure AD Connect: Wymagania wstępne i sprzętu | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano wymagania wstępne hello i wymagania sprzętowe hello Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Wymagania wstępne dotyczące usługi Azure AD Connect
W tym temacie opisano wymagania wstępne hello i wymagania sprzętowe hello Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Przed zainstalowaniem usługi Azure AD Connect
Przed zainstalowaniem usługi Azure AD Connect, istnieje kilka rzeczy, które są potrzebne.

### <a name="azure-ad"></a>Azure AD
* Subskrypcja platformy Azure lub [subskrypcji wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/). Ta subskrypcja jest tylko wymagane do uzyskiwania dostępu do hello portalu Azure, a nie za pomocą usługi Azure AD Connect. Jeśli używasz programu PowerShell lub usługi Office 365, nie należy toouse subskrypcji platformy Azure, Azure AD Connect. Jeśli użytkownik ma licencję usługi Office 365, można także użyć portalu hello usługi Office 365. Z płatnej licencji usługi Office 365 można także uzyskać na powitania portalu Azure w portalu usługi Office 365 hello.
  * Można również użyć hello [portalu Azure](https://portal.azure.com). Ten portal nie wymaga licencji usługi Azure AD.
* [Dodać i zweryfikować domeny hello](../active-directory-domains-add-azure-portal.md) planowanie toouse w usłudze Azure AD. Na przykład jeśli plan toouse contoso.com dla użytkowników, upewnij się, że ta domena została zweryfikowana i nie używasz tylko hello contoso.onmicrosoft.com domyślnej domeny.
* Dzierżawa usługi Azure AD umożliwia przez obiekty domyślne 50k. Podczas weryfikowania domeny hello limit jest zwiększone too300k obiektów. Jeśli potrzebujesz więcej obiektów w usłudze Azure AD, należy tooopen limit hello toohave sprawy pomocy technicznej jeszcze bardziej zwiększyć. Jeśli potrzebujesz więcej niż 500 obiektów k potrzebna licencja, takich jak usługi Office 365, Azure AD podstawowa usługi Azure AD Premium lub pakietu Enterprise Mobility i zabezpieczeń.

### <a name="prepare-your-on-premises-data"></a>Przygotowywanie danych lokalnych
* Użyj [narzędzia IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify błędami takimi jak duplikaty i problemów z formatowaniem w katalogu przed synchronizacją tooAzure AD i Office 365.
* Przegląd [funkcje opcjonalne synchronizacji, można włączyć w usłudze Azure AD](active-directory-aadconnectsyncservice-features.md) i ocenić, które funkcje należy włączyć.

### <a name="on-premises-active-directory"></a>Lokalna usługa Active Directory
* Witaj AD schematu wersji i lasu poziom funkcjonalności musi być systemu Windows Server 2003 lub nowszym. kontrolery domeny Hello można dowolną wersją tak długo, jak hello schematu i lasu poziomu wymagania.
* Jeśli planujesz funkcji hello toouse **funkcji zapisywania zwrotnego haseł**, kontrolery domeny hello musi być w systemie Windows Server 2008 (z najnowszą SP) lub nowszym. Jeśli Twoje kontrolery domeny są 2008 (pre-R2), a następnie również należy zastosować [poprawkę KB2386717](http://support.microsoft.com/kb/2386717).
* musi być zapisywalny kontroler domeny Hello jest używany przez usługę Azure AD. Jest **nieobsługiwane** toouse kontrolera RODC (kontroler domeny tylko do odczytu) i Azure AD Connect nie jest zgodna z żadnym zapisu przekierowania.
* Jest **nieobsługiwane** toouse przy użyciu drugiego poziomu (jednej etykiety domen) lasami/domenami lokalnymi.
* Jest **nieobsługiwane** toouse lokalnej lasami/domenami przy użyciu "kropkami" (nazwa zawiera znak kropki ".") Nazwy NetBios.
* Zalecane jest zbyt[włączyć Kosz usługi Active Directory hello](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Serwer systemu Azure AD Connect
* Nie można zainstalować usługi Azure AD Connect na Small Business Server lub Windows Server Essentials. Serwer Hello muszą używać systemu Windows Server standard lub większą.
* Hello Azure AD Connect serwer musi mieć pełnym interfejsem GUI zainstalowane. Jest **nieobsługiwane** tooinstall w instalacji server core.
* Azure AD Connect musi być zainstalowany w systemie Windows Server 2008 lub nowszym. Ten serwer może być kontrolerem domeny lub serwer członkowski po przy użyciu ustawień ekspresowych. Jeśli używasz ustawienia niestandardowe, powitania serwera może być autonomiczne i nie ma toobe tooa przyłączone do domeny.
* Po zainstalowaniu usługi Azure AD Connect w systemie Windows Server 2008 lub Windows Server 2008 R2, upewnij się, że tooapply hello najnowszych poprawek z witryny Windows Update. Instalacja Hello nie jest możliwe toostart z serwerem bez poprawki.
* Jeśli planujesz funkcji hello toouse **synchronizacji haseł**, hello Azure AD Connect serwera musi być w systemie Windows Server 2008 R2 z dodatkiem SP1 lub nowszym.
* Jeśli planujesz toouse **konto usługi zarządzane przez grupę**, hello Azure AD Connect serwera musi być w systemie Windows Server 2012 lub nowszym.
* Hello Azure AD Connect serwer musi mieć [.NET Framework 4.5.1](#component-prerequisites) lub nowszym i [Microsoft PowerShell 3.0](#component-prerequisites) lub nowszy.
* powitania serwera Azure AD Connect nie może mieć włączonymi zasadami grupy przekształcania programu PowerShell.
* Jeśli wdrażana usług federacyjnych Active Directory, serwerów hello, w którym są zainstalowane usługi AD FS lub serwer Proxy aplikacji sieci Web musi być Windows Server 2012 R2 lub nowszym. [Zdalne zarządzanie systemem Windows](#windows-remote-management) na te serwery do zdalnej instalacji musi być włączona.
* Jeśli wdrażana usług federacyjnych Active Directory, należy [certyfikaty SSL](#ssl-certificate-requirements).
* Jeśli usług federacyjnych Active Directory został wdrożony, a następnie należy tooconfigure [rozpoznawanie nazw](#name-resolution-for-federation-servers).
* Jeśli Twoje Administratorzy globalni mają włączone uwierzytelnianie MFA, hello adresu URL **https://secure.aadcdn.microsoftonline-p.com** musi znajdować się na liście zaufanych witryn hello. Jesteś zostanie wyświetlony monit o tooadd, ta lokacja toohello listy zaufanych witryn po wyświetleniu monitu dla żądania usługi MFA i nie został dodany przed. Można użyć programu Internet Explorer tooadd on tooyour Zaufane witryny.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server używane przez program Azure AD Connect
* Azure AD Connect wymaga danych tożsamości toostore bazy danych programu SQL Server. Domyślnie jest instalowany program SQL Server 2012 Express LocalDB (światła wersja programu SQL Server Express). SQL Server Express ma limit rozmiaru 10GB, umożliwiający toomanage około 100 000 obiektów. Jeśli potrzebujesz toomanage wyższej liczby obiektów katalogu należy toopoint hello instalacji Kreator tooa inną instalację programu SQL Server.
* Jeśli używasz oddzielny serwer SQL, mają zastosowanie te wymagania:
  * Azure AD Connect obsługuje wszystkie odmian programu Microsoft SQL Server z programu SQL Server 2008 (za pomocą najnowszego dodatku Service Pack) tooSQL Server 2016 z dodatkiem SP1. Baza danych SQL Azure firmy Microsoft jest **nieobsługiwane** jako bazy danych.
  * Należy użyć bez uwzględniania wielkości liter sortowania bazy danych SQL. Te sortowania są oznaczone symbolem \_CI_ w ich imieniu. Jest **nieobsługiwane** toouse sortowania z uwzględnieniem wielkości liter, identyfikowane przez \_cs_ — w ich imieniu.
  * Może mieć tylko jeden aparat synchronizacji pojedyncze wystąpienie serwera SQL. Jest **nieobsługiwane** tooshare SQL wystąpienia z synchronizacji programu FIM/MIM narzędzia DirSync i Azure AD Sync.

### <a name="accounts"></a>Konta
* Konto administratora globalnego usługi Azure AD dla dzierżawy usługi Azure AD hello mają toointegrate z. To konto musi być **konto służbowe lub organizacji** i nie może być **konta Microsoft**.
* Użyj ustawień ekspresowych lub uaktualnienie z narzędzia DirSync, musi mieć konto administratora przedsiębiorstwa dla lokalnej usługi Active Directory.
* [Konta w usłudze Active Directory](active-directory-aadconnect-accounts-permissions.md) użycie ścieżki instalacji hello ustawienia niestandardowe.

### <a name="connectivity"></a>Łączność
* Hello Azure AD Connect serwera wymaga rozpoznawania nazw DNS dla intranetowych i internetowych. Witaj serwer DNS musi być w stanie tooresolve nazwy obu tooyour lokalnej usługi Active Directory i hello punktów końcowych usługi Azure AD.
* Jeżeli masz zapory w sieci Intranet i trzeba porty tooopen między hello Azure AD Connect serwerów i kontrolerach domeny, zobacz [Azure AD Connect porty](active-directory-aadconnect-ports.md) Aby uzyskać więcej informacji.
* Jeśli Twój limit serwera proxy lub zapory, który można uzyskać dostępu do adresów URL, następnie hello adresy URL w [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) musi być otwarty.
  * Jeśli używasz hello Microsoft Cloud w Niemczech lub hello chmury Microsoft Azure dla instytucji rządowych, a następnie zobacz [zagadnienia dotyczące wystąpienia usługi synchronizacji programu Azure AD Connect](active-directory-aadconnect-instances.md) dla adresu URL.
* Azure AD Connect jest domyślnie przy użyciu protokołu TLS 1.0 toocommunicate z usługą Azure AD. To tooTLS, 1.2 można zmienić, wykonując kroki hello w [włączenia protokołu TLS 1.2, programu Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Jeśli używasz serwera proxy ruchu wychodzącego do łączenia toohello Internet, hello następujące ustawienie w hello **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** konieczne jest dodanie pliku hello Kreatora instalacji i Azure AD Connect synchronizacji toobe stanie tooconnect toohello Internet i Azure AD. Należy podać ten tekst u dołu hello hello pliku. W tym kodzie &lt;PROXYADRESS&gt; reprezentuje hello rzeczywiste proxy IP adres lub nazwę hosta.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Jeśli serwer proxy wymaga uwierzytelniania, a następnie hello [konto usługi](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) musi znajdować się w hello domeny, w przypadku należy użyć hello dostosowane ustawienia instalacji ścieżka toospecify [konto niestandardowe usługi](active-directory-aadconnect-get-started-custom.md#install-required-components). Należy również toomachine.config różnych zmian. Z tą zmianą w pliku machine.config aparatu kreatora i synchronizacji instalacji hello odpowiada na żądania tooauthentication z powitania serwera proxy. Na wszystkich stronach kreatora instalacji, z wyłączeniem hello **Konfiguruj** strony hello zalogowany użytkownika używane są poświadczenia. Na powitania **Konfiguruj** strony na końcu hello hello Kreatora instalacji, kontekst hello jest wyłączone toohello [konto usługi](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) utworzone przez użytkownika. sekcja machine.config Hello powinna wyglądać następująco.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Azure AD Connect wysyła tooAzure żądania sieci web usługi AD w ramach synchronizacji katalogów, usługi Azure AD może potrwać too5 toorespond minut. Bardzo często konfiguracji limit czasu bezczynności połączenia toohave serwerów proxy. Upewnij się, że konfiguracja hello ustawiono tooat co najmniej 6 minut lub więcej.

Aby uzyskać więcej informacji, zobacz MSDN temat hello [domyślny serwer proxy elementu](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Aby uzyskać więcej informacji, jeśli masz problemy z łącznością, zobacz [Rozwiązywanie problemów z łącznością](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Inne
* Opcjonalnie: Test użytkownika konta tooverify synchronizacji.

## <a name="component-prerequisites"></a>Wymagania wstępne dotyczące składnika
### <a name="powershell-and-net-framework"></a>Środowiska PowerShell i .net Framework
Azure AD Connect jest zależny od firmy Microsoft PowerShell i .NET Framework 4.5.1. Potrzebujesz tej wersji lub nowszy zainstalowany na serwerze. W zależności od wersji systemu Windows Server hello następujące:

* Windows Server 2012 R2
  * Microsoft PowerShell jest instalowany domyślnie. Nie jest wymagana żadna akcja.
  * .NET framework 4.5.1 i jego nowszych wersjach są dostępne za pośrednictwem usługi Windows Update. Upewnij się, że zainstalowano hello najnowsze aktualizacje tooWindows serwera w hello Panelu sterowania.
* Windows Server 2008R2 i Windows Server 2012
  * Hello najnowszej wersji programu PowerShell firmy Microsoft jest dostępna w **Windows Management Framework 4.0**, dostępnych na [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 i jego nowszych wersjach są dostępne na [Microsoft Download Center](http://www.microsoft.com/downloads).
* Windows Server 2008
  * Witaj najnowsza wersja obsługiwana wersja programu PowerShell jest dostępny w **Windows Management Framework 3.0**, dostępnych na [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 i jego nowszych wersjach są dostępne na [Microsoft Download Center](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Włącz protokół TLS 1.2 dla programu Azure AD Connect
Azure AD Connect używa protokołu TLS 1.0 domyślnie do szyfrowania hello komunikacji między serwerem aparatu synchronizacji hello i Azure AD. Można to zmienić, konfigurując toouse aplikacji .net protokołu TLS 1.2, domyślnie na powitania serwera. Więcej informacji na temat protokołu TLS 1.2 znajduje się w [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358).

1. Nie można włączyć protokołu TLS 1.2 w systemie Windows Server 2008. Należy systemu Windows Server 2008 R2 lub nowszym. Upewnij się, że ma hello .net 4.5.1 poprawek zainstalowanych w systemie operacyjnym, zobacz [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358). Konieczne może być ta poprawka lub jego nowsza wersja już zainstalowana na serwerze.
2. Jeśli używasz systemu Windows Server 2008 R2, upewnij się, że jest włączony protokół TLS 1.2. Na serwerze Windows Server 2012 i nowszych wersjach już powinien być włączony protokół TLS 1.2.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. We wszystkich systemach operacyjnych ustawić ten klucz rejestru, a następnie ponownie uruchomić powitania serwera.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Jeśli chcesz tooenable protokołu TLS 1.2 między serwerem aparatu synchronizacji hello i zdalnym serwerze SQL, a następnie upewnij się, że masz zainstalowanych dla wersji hello wymagane [obsługę protokołu TLS 1.2 dla programu Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Wymagania wstępne dotyczące federacyjnego instalacji i konfiguracji
### <a name="windows-remote-management"></a>Zdalne zarządzanie systemem Windows
Korzystając z usługi Azure AD Connect toodeploy usług federacyjnych Active Directory lub powitania serwera Proxy aplikacji sieci Web, sprawdź następujące wymagania:

* Jeśli serwer docelowy hello jest przyłączony do domeny, następnie upewnij się, że zdalnego zarządzania systemu Windows jest włączona.
  * W oknie polecenia z podwyższonym poziomem uprawnień Psh — polecenie`Enable-PSRemoting –force`
* Jeśli serwer docelowy hello jest poza domeną przyłączone WAP maszyny, a następnie istnieje kilka dodatkowych wymagań
  * Na powitania docelowym komputerze (WAP):
    * Upewnij się, hello winrm (zdalne zarządzanie systemem Windows / usługi WS-Management) jest uruchomiona za pomocą przystawki usługi hello
    * W oknie polecenia z podwyższonym poziomem uprawnień Psh — polecenie`Enable-PSRemoting –force`
  * Na komputerze hello, na które hello Kreator jest uruchomiony (Jeśli maszyna docelowa hello jest domeny z systemem innym niż sprzężone lub niezaufanej domeny):
    * W oknie polecenia z podwyższonym poziomem uprawnień PSH polecenie hello`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * W Menedżerze serwera:
      * Dodaj pulę toomachine hosta DMZ WAP (Menedżer serwera -> Zarządzaj -> Dodaj serwery... karta DNS)
      * Karta serwery wszystkie Menedżera serwera: kliknij prawym przyciskiem myszy serwer proxy i wybierz polecenie Zarządzaj jako..., wprowadź poświadczenia lokalnego (nie domeny) hello WAP maszyny
      * toovalidate PSH połączenia zdalnego, w hello karcie w Menedżerze serwera wszystkie serwery: kliknij prawym przyciskiem myszy serwer proxy i wybierz polecenie programu Windows PowerShell. Należy otworzyć sesję zdalną PSH można ustalić tooensure zdalnej sesji programu PowerShell.

### <a name="ssl-certificate-requirements"></a>Wymagania dotyczące certyfikatów SSL
* Zdecydowanie zaleca się toouse hello tego samego certyfikatu SSL na wszystkich węzłach farmę usług AD FS i wszystkich serwerów proxy aplikacji sieci Web.
* Witaj, certyfikat musi być X509 certyfikatu.
* Certyfikatu z podpisem własnym można używać na serwerach federacyjnych w środowisku laboratorium testowego. W środowisku produkcyjnym zalecamy uzyskać hello certyfikatów z publicznego urzędu certyfikacji.
  * Jeśli używa certyfikatu, który nie jest zaufany publicznie, upewnij się, hello certyfikat zainstalowany na każdym serwerze Proxy aplikacji sieci Web jest zaufany na serwerze lokalnym zarówno hello i na wszystkich serwerach federacyjnych
* tożsamości Hello hello certyfikatu musi odpowiadać nazwie usługi federacyjnej hello (np. sts.contoso.com).
  * tożsamość Hello jest albo podmiotu alternatywnej nazwy (SAN) rozszerzenie typu dNSName lub, jeśli nie ma żadnych wpisów sieci SAN, nazwa podmiotu hello określona jako nazwę pospolitą.  
  * Wiele wpisów sieci SAN mogą być obecne w hello certyfikatu, pod warunkiem jeden z nich jest zgodna nazwa usługi federacyjnej hello.
  * Jeśli planujesz toouse dołączanie do miejsca pracy, dodatkowe sieci SAN jest wymagany w przypadku wartości hello **enterpriseregistration.** następuje hello sufiks główną nazwę użytkownika (UPN) Twojej organizacji, na przykład **enterpriseregistration.contoso.com**.
* Certyfikaty na podstawie CryptoAPI next generation (CNG) kluczy i dostawcy magazynu kluczy nie są obsługiwane. Oznacza to, że muszą używać certyfikatu na podstawie CSP (dostawca usług kryptograficznych) i nie dostawcy magazynu KLUCZY (Dostawca magazynu kluczy).
* Certyfikaty — symbol wieloznaczny są obsługiwane.

### <a name="name-resolution-for-federation-servers"></a>Rozpoznawanie nazw dla serwerów federacyjnych
* Skonfigurować rekordy DNS dla hello nazwa usługi federacyjnej usług AD FS (np. sts.contoso.com) dla intranetowych hello (wewnętrznego serwera DNS) i hello ekstranetu (publicznym systemie DNS za pomocą rejestratora domen). Aż rekord usługi DNS hello w intranecie, upewnij się, że używasz A rekordów i nie rekordy CNAME. Jest to wymagane dla toowork uwierzytelniania systemu windows poprawnie z komputera dołączonego do domeny.
* Jeśli wdrażasz więcej niż jednego serwera usług AD FS lub serwer Proxy aplikacji sieci Web, upewnij się, że zostały skonfigurowane przez moduł równoważenia obciążenia i hello rekordy DNS dla hello AD FS federation service nazwa (np. sts.contoso.com) punktu toohello modułu równoważenia obciążenia.
* Dla toowork zintegrowanego uwierzytelniania systemu windows dla aplikacji przeglądarki, za pomocą programu Internet Explorer w sieci intranet upewnij się, że hello nazwa usługi federacyjnej usług AD FS (np. sts.contoso.com) jest dodawany toohello strefy intranet w programie Internet Explorer. Może to być kontrolowane za pomocą zasad grupy i tooall wdrożone komputery przyłączone domenę.

## <a name="azure-ad-connect-supporting-components"></a>Obsługa składników usługi Azure AD Connect
Witaj poniżej znajduje się lista składników, które Azure AD Connect instaluje na serwerze hello zainstalowanym Azure AD Connect. Ta lista jest podstawowe instalacji ekspresowej. Jeśli wybierzesz toouse innego serwera SQL na powitania Zainstaluj stronę usługi synchronizacji i następnie SQL Express LocalDB nie ma zainstalowanego lokalnie.

* Azure AD Connect Health
* Microsoft Online Services Asystenta logowania dla specjalistów IT (zainstalowany ale nie zależność)
* Microsoft SQL Server 2012 Command Line Utilities
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Microsoft Visual C++ 2013 redystrybucji pakietu

## <a name="hardware-requirements-for-azure-ad-connect"></a>Wymagania sprzętowe programu Azure AD Connect
Witaj w poniższej tabeli przedstawiono hello minimalne wymagania dotyczące komputera do synchronizacji Azure AD Connect hello.

| Liczba obiektów w usłudze Active Directory | Procesor CPU | Memory (Pamięć) | Rozmiar dysku twardego |
| --- | --- | --- | --- |
| Mniej niż 10 000 |1,6 GHz |4 GB |70 GB |
| 10,000–50,000 |1,6 GHz |4 GB |70 GB |
| 50,000–100,000 |1,6 GHz |16 GB |100 GB |
| Dla 100 000 lub więcej obiektów jest wymagana hello pełna wersja programu SQL Server | | | |
| 100,000–300,000 |1,6 GHz |32 GB |300 GB |
| 300,000–600,000 |1,6 GHz |32 GB |450 GB |
| Ponad 600 000. |1,6 GHz |32 GB |500 GB |

Witaj minimalne wymagania dotyczące komputerów z uruchomionymi usługami AD FS lub serwerów aplikacji sieci Web jest hello następujące czynności:

* Procesora CPU: Dwóch podstawowych 1,6 GHz lub nowszej
* PAMIĘCI: 2 GB lub nowszej
* Maszyna wirtualna platformy Azure: A2 konfiguracji lub nowszej

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
