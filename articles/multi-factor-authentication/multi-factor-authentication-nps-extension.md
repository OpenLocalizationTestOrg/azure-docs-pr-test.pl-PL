---
title: "aaaUse istniejącego serwera NPS serwerów tooprovide możliwości usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "powitania serwera zasad sieciowych rozszerzenie dla usługi Azure Multi-Factor Authentication jest prostym rozwiązaniem tooadd oparte na chmurze dwuetapowej vericiation możliwości tooyour istniejącej infrastruktury uwierzytelniania."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Integracja istniejącej infrastrukturze serwera NPS z usługi Azure Multi-Factor Authentication

rozszerzenia serwera zasad sieciowych (NPS) dla usługi Azure MFA Hello dodaje MFA możliwości tooyour uwierzytelniania infrastruktury chmurowej przy użyciu istniejących serwerów. Z hello rozszerzenia serwera zasad Sieciowych można dodać połączenie telefoniczne, wiadomość tekstowa lub telefonu aplikacji weryfikacji tooyour istniejących przepływ uwierzytelniania bez konieczności tooinstall, konfigurowania i konserwacji nowych serwerów. 

To rozszerzenie został utworzony dla organizacji, które mają tooprotect połączeń sieci VPN bez wdrażania powitania serwera usługi Azure MFA. Hello rozszerzenia serwera NPS działa jako karta między usługi RADIUS i oparte na chmurze usługi Azure MFA tooprovide drugiego etapu uwierzytelniania dla użytkowników federacyjnych lub zsynchronizowane.

W przypadku używania powitania serwera NPS rozszerzenia dla usługi Azure MFA, przepływ uwierzytelniania hello obejmuje hello następujące składniki: 

1. **Serwer NAS lub sieć VPN** odbiera żądania od klientów sieci VPN i konwertuje je na serwerach tooNPS żądań RADIUS. 
2. **Serwer NPS** łączy tooActive katalogu tooperform hello podstawowego uwierzytelniania dla aplikacji hello RADIUS żądań i na sukces, przekazuje hello żądania tooany zainstalowanych rozszerzeń.  
3. **Rozszerzenia serwera NPS** wyzwala tooAzure żądania usługi MFA dla hello dodatkowego uwierzytelniania. Po rozszerzenia hello odbiera odpowiedź hello i hello żądanie uwierzytelniania MFA zakończy się powodzeniem, kończy żądanie uwierzytelnienia hello podając tokeny zabezpieczające, które obejmują MFA oświadczenia wydane przez usługę STS Azure powitania serwera NPS.  
4. **Usługa Azure MFA** komunikuje się z usługi Azure Active Directory tooretrieve hello szczegóły użytkownika i wykonuje hello dodatkowego uwierzytelniania przy użyciu użytkownika toohello metodę skonfigurowaną weryfikację.

powitania po diagram ilustruje ten przepływ żądania uwierzytelniania wysokiego poziomu: 

![Diagram przepływu uwierzytelniania](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Planowanie wdrożenia

Witaj rozszerzenia serwera zasad Sieciowych automatycznie obsługuje nadmiarowość, więc nie trzeba specjalnej konfiguracji.

Można utworzyć dowolną liczbę serwerów NPS z włączoną usługą Azure MFA. W przypadku instalowania wielu serwerów, należy użyć certyfikatu klienta różnicy dla każdego z nich. Tworzenie certyfikatu dla każdego serwera oznacza indywidualnie zaktualizować każdego certyfikatu, a nie martw się o przestoju na wszystkich serwerach.

Serwery sieci VPN trasy żądania uwierzytelniania, więc toobe muszą pamiętać o hello nowych serwerów NPS z włączoną usługą Azure MFA.

## <a name="prerequisites"></a>Wymagania wstępne

Witaj rozszerzenia serwera NPS jest przeznaczona toowork z istniejącej infrastruktury. Upewnij się, że masz hello następujące wymagania wstępne, aby rozpocząć.

### <a name="licenses"></a>Licencje

Hello rozszerzenia serwera zasad Sieciowych na potrzeby usługi Azure MFA jest dostępne toocustomers z [licencji dla usługi Azure Multi-Factor Authentication](multi-factor-authentication.md) (dołączony do usługi Azure AD Premium, EMS lub subskrypcji usługi MFA).

### <a name="software"></a>Oprogramowanie

Windows Server 2008 R2 z dodatkiem SP1 lub nowszej.

### <a name="libraries"></a>Biblioteki

Te biblioteki są automatycznie instalowane z rozszerzeniem hello.
-   [Pakiety redystrybucyjne języka Visual C++ dla programu Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Microsoft Azure Active Directory modułu dla Windows PowerShell w wersji 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Usługa Azure Active Directory

Wszyscy przy użyciu rozszerzenia zasad Sieciowych hello muszą być zsynchronizowane tooAzure usługi Active Directory za pomocą usługi Azure AD Connect, a musi być zarejestrowana w usłudze MFA.

Po zainstalowaniu rozszerzenia hello potrzebne hello poświadczenia identyfikator i administratora katalogu dla dzierżawy usługi Azure AD. Identyfikator katalogu można znaleźć w hello [portalu Azure](https://portal.azure.com). Zaloguj się jako administrator, wybierz hello **usługi Azure Active Directory** ikona powitania po lewej stronie, następnie wybierz **właściwości**. Kopiuj hello identyfikatora GUID w hello **identyfikator katalogu** i zapisz go. Używasz tego identyfikatora GUID jako Identyfikatora dzierżawcy hello po zainstalowaniu hello rozszerzenia serwera NPS.

![Znajdź swój identyfikator katalogu we właściwościach usługi Azure Active Directory](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Przygotowywanie środowiska

Przed zainstalowaniem rozszerzenia serwera NPS hello ma tooprepare możesz środowiska toohandle hello uwierzytelniania ruchu.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Włącz hello rola serwera NPS na serwerze przyłączonym do domeny

serwer NPS Hello łączy tooAzure usługi Active Directory i uwierzytelnia hello żądania usługi MFA. Należy wybrać serwer dla tej roli. Firma Microsoft zaleca, wybierając serwer, który nie obsłuży żądania od innych usług, ponieważ hello rozszerzenia serwera NPS zgłasza błędów dla żądań, które nie są usługi RADIUS.

1. Na serwerze otwórz hello **Kreatora dodawania ról i funkcji** z hello menu Menedżera serwera — Szybki Start.
2. Wybierz **Instalacja roli lub funkcji** dla danego typu instalacji.
3. Wybierz hello **usług zasad sieciowych i dostępu** roli serwera. Okno może wyskakujące tooinform o toorun wymagane funkcje tej roli.
4. Aż Kreator hello hello stronę potwierdzenia. Wybierz **zainstalować**.

Teraz, gdy masz serwer wyznaczony serwera NPS należy także skonfigurować ten serwer toohandle przychodzących żądań RADIUS z hello rozwiązanie z siecią VPN.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Skonfiguruj toocommunicate rozwiązanie sieci VPN z serwera NPS hello

W zależności od tego, które rozwiązanie sieci VPN, należy hello tooconfigure kroki, które różnią się z zasadami uwierzytelniania usługi RADIUS. Skonfiguruj ten serwer RADIUS NPS tooyour toopoint zasad.

### <a name="sync-domain-users-toohello-cloud"></a>Chmura toohello użytkownicy domeny synchronizacji

Ten krok może już zostać ukończone na swojej dzierżawy, ale jest dobrym toodouble — Sprawdź, czy Azure AD Connect został zsynchronizowany baz danych.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Wybierz **usługi Azure Active Directory** > **programu Azure AD Connect**
3. Sprawdź, czy stan synchronizacji **włączone** i który ostatniej synchronizacji był mniejszy niż godzinę temu.

Tookick poza nowe round synchronizacji, należy nam hello instrukcjami [synchronizacja programu Azure AD Connect: harmonogram](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Określić, które użytkownicy mogą używać metody uwierzytelniania

Istnieją dwa czynniki wpływające na które metody uwierzytelniania są dostępne z wdrażaniem rozszerzenia serwera NPS:

1. Algorytm szyfrowania hasła Hello używany podczas komunikacji między klientem RADIUS hello (sieci VPN, serwer Netscaler lub innych) i powitania serwera NPS.
   - **PAP** obsługuje wszystkie hello metody uwierzytelniania usługi Azure MFA w chmurze hello: połączenie telefoniczne, wiadomość tekstowa jednokierunkowe powiadomienie aplikacji mobilnej i kod weryfikacyjny z aplikacji mobilnej.
   - **CHAPV2** i **EAP** obsługi połączeń telefonicznych i powiadomienia aplikacji mobilnej.
2. Hello wejściowych metody, które hello aplikacji klienckiej (sieć VPN, serwer Netscaler lub innych) może obsłużyć. Na przykład powitania klienta VPN ma na niektórych oznacza tooallow hello użytkownika tootype w kod weryfikacyjny z aplikacji mobilnej lub tekst?

Podczas wdrażania hello rozszerzenia serwera NPS, użyj tych tooevaluate czynników, które metody są dostępne dla użytkowników. Jeśli klient RADIUS obsługą protokołu PAP, ale powitania klienta UX nie ma pól wejściowych dla kod weryfikacyjny, połączenia telefonicznego i powiadomienia aplikacji mobilnej to Witaj dwie opcje są obsługiwane.

Możesz [wyłączyć metody uwierzytelniania nieobsługiwany](multi-factor-authentication-whats-next.md#selectable-verification-methods) na platformie Azure.

### <a name="enable-users-for-mfa"></a>Włącz użytkowników dla usługi MFA

Przed wdrożeniem hello pełne rozszerzenia serwera NPS należy tooenable MFA dla użytkowników hello, które mają tooperform weryfikacji dwuetapowej. Więcej natychmiast rozszerzenia hello tootest podczas wdrażania, musisz mieć konto co najmniej jeden test, który pełni jest zarejestrowany w usłudze Multi-Factor Authentication.

Użyj tych tooget kroki testowe konto uruchomiona:
1. Zaloguj się za[https://aka.ms/mfasetup](https://aka.ms/mfasetup) przy użyciu konta testowego. 
2. Wykonaj tooset monity hello metodę weryfikacji.
3. Utwórz zasady dostępu warunkowego lub [zmiany stanu użytkownika hello](multi-factor-authentication-get-started-user-states.md) toorequire weryfikację dwuetapową dla konta testowego hello. 

Użytkownicy również potrzebują toofollow tooenroll te kroki przed uwierzytelniają rozszerzeniem powitania serwera NPS.

## <a name="install-hello-nps-extension"></a>Zainstaluj rozszerzenie serwera NPS hello

> [!IMPORTANT]
> Zainstaluj rozszerzenie serwera NPS hello na innym serwerze niż punkt dostępu sieci VPN hello.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Pobierz i zainstaluj powitania serwera NPS rozszerzenia dla usługi Azure MFA

1.  [Pobierz hello rozszerzenia serwera NPS](https://aka.ms/npsmfa) z hello Microsoft Download Center.
2.  Skopiuj hello toohello binarnej ma tooconfigure serwera zasad sieciowych.
3.  Uruchom *setup.exe* i postępuj zgodnie z instrukcjami instalacji hello. Jeśli wystąpią błędy, dokładnie Sprawdź ten powitalne dwie biblioteki z sekcji wymagań wstępnych hello zostały pomyślnie zainstalowane.

### <a name="run-hello-powershell-script"></a>Uruchom skrypt programu PowerShell hello

Witaj Instalator tworzy skrypt programu PowerShell w tej lokalizacji: `C:\Program Files\Microsoft\AzureMfa\Config` (gdzie C:\ to dysk instalacji). Ten skrypt programu PowerShell wykonuje hello następujące akcje:

-   Tworzenie certyfikatu z podpisem własnym.
-   Kojarzenie klucza publicznego hello hello usługi toohello certyfikatu podmiotu zabezpieczeń w usłudze Azure AD.
-   Magazyn hello certyfikatu w magazynie certyfikatów komputera lokalnego hello.
-   Certyfikat Udziel dostępu toohello prywatnego klucza tooNetwork użytkownika.
-   Uruchom ponownie powitania serwera NPS.

Chyba że chcesz toouse własne certyfikaty (zamiast hello certyfikaty z podpisem własnym, które hello generuje skrypt programu PowerShell), uruchom hello skrypt programu PowerShell toocomplete hello instalacji. Po zainstalowaniu rozszerzenia hello na wielu serwerach, każdy z nich ma własny certyfikat.

1. Uruchom program Windows PowerShell jako administrator.
2. Zmień katalog.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Uruchom skrypt programu PowerShell hello utworzonych przez Instalatora hello.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell monit o podanie identyfikatora dzierżawcy Użyj hello katalogu Identyfikatora GUID, który został skopiowany z portalu Azure w sekcji wymagania wstępne hello hello.
5. Zaloguj się jako administrator, tooAzure AD.
6. PowerShell wyświetla komunikat z potwierdzeniem po zakończeniu hello skryptu.  

Powtórz te czynności na wszelkie dodatkowe serwery NPS, które mają tooset dla równoważenia obciążenia.

>[!NOTE]
>Jeśli używasz własne certyfikaty zamiast generowania certyfikatów przy użyciu hello skrypt programu PowerShell, upewnij się, że są wyrównane konwencji nazewnictwa toohello serwera NPS. Hello nazwa podmiotu musi być **CN =\<TenantID\>, OU = Microsoft NPS rozszerzenia**. 

## <a name="configure-your-nps-extension"></a>Skonfiguruj rozszerzenie serwera NPS

Ta sekcja obejmuje zagadnienia dotyczące projektowania oraz sugestie dotyczące pomyślnego wdrożenia rozszerzenia serwera NPS.

### <a name="configuration-limitations"></a>Ograniczenia konfiguracji

- nie ma Hello rozszerzenia serwera zasad Sieciowych na potrzeby usługi Azure MFA, użytkownicy toomigrate narzędzia i ustawienia z serwera usługi MFA toohello chmury. Z tego powodu zalecamy przy użyciu rozszerzenia hello nowych wdrożeń zamiast istniejącego wdrożenia. Jeśli używasz rozszerzenia hello na istniejące wdrożenie, użytkownicy mają tooperform dowód up ponownie toopopulate ich MFA szczegółowych informacji w chmurze hello.  
- Witaj rozszerzenia serwera zasad Sieciowych używa hello UPN z hello lokalnej usługi Active directory tooidentify hello użytkownika na usługę Azure MFA do wykonywania hello dodatkowej uwierzytelniania hello rozszerzenia może być skonfigurowany toouse inny identyfikator takich jak logowanie alternatywny identyfikator lub niestandardowe usługi Active Directory pola innego niż głównej nazwy użytkownika. Zobacz [zaawansowane opcje konfiguracji hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe](multi-factor-authentication-advanced-vpn-configurations.md) Aby uzyskać więcej informacji.
- Nie wszystkie protokoły szyfrowania obsługuje wszystkie metody weryfikacji.
   - **PAP** obsługuje połączenie telefoniczne, wiadomość tekstowa jednokierunkowe powiadomienie aplikacji mobilnej i kod weryfikacyjny z aplikacji mobilnej
   - **CHAPV2** i **EAP** obsługi połączeń telefonicznych i powiadomienia aplikacji mobilnej

### <a name="control-radius-clients-that-require-mfa"></a>Formant klientów usługi RADIUS, które wymagają usługi MFA

Po włączeniu uwierzytelnianie wieloskładnikowe dla klienta RADIUS przy użyciu hello rozszerzenia serwera NPS wszystkie uwierzytelnienia dla tego klienta są wymagane tooperform MFA. Jeśli chcesz tooenable MFA dla niektórych klientów usługi RADIUS, a innych nie można skonfigurować dwa serwery NPS i zainstaluj rozszerzenie hello na tylko jeden z nich. Konfigurowanie klientów usługi RADIUS, które mają toorequire MFA toosend żądań toohello serwera NPS skonfigurowany z rozszerzeniem hello i innych klientów usługi RADIUS toohello serwer NPS nie jest skonfigurowany z rozszerzeniem hello.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Przygotowanie do użytkowników, którzy nie są rejestrowane w usłudze MFA

Jeśli masz użytkowników, którzy nie są rejestrowane w usłudze MFA, można określić, co się dzieje, gdy próbują tooauthenticate. Użyj ustawienia rejestru hello *REQUIRE_USER_MATCH* w ścieżce rejestru hello *HKLM\Software\Microsoft\AzureMFA* toocontrol hello funkcji zachowanie. To ustawienie nie ma opcji konfiguracji pojedynczego:

| Klucz | Wartość | Domyślne |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | PRAWDA/FAŁSZ | Nieustawione (tooTRUE równoważne) |

Witaj celem tego ustawienia jest toodetermine jakie toodo, gdy użytkownik nie jest zarejestrowane w usłudze MFA. Po klucz hello nie istnieje, nie jest ustawiona lub ma wartość tooTRUE, hello użytkownik nie jest zarejestrowany, a następnie hello rozszerzenia nie powiodło się żądanie uwierzytelniania MFA hello. Po klucz hello ustawiono tooFALSE i hello użytkownik nie jest zarejestrowany, uwierzytelnianie będzie kontynuowane bez wykonywania MFA.

Możesz wybrać toocreate ten klucz i ustawić jej tooFALSE podczas dołączania są użytkownicy, i może nie wszystkie zarejestrowane na potrzeby usługi Azure MFA jeszcze. Jednak ponieważ klucz hello ustawienia pozwala na użytkowników, którzy nie są rejestrowane w usłudze MFA toosign w, należy usunąć ten klucz przed przejściem tooproduction.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Jak sprawdzić, czy tego certyfikatu klienta hello jest zainstalowana zgodnie z oczekiwaniami?

Wyszukaj certyfikat z podpisem własnym hello utworzonych przez Instalatora hello w magazynie certyfikatów hello i sprawdź, czy klucz prywatny hello ma uprawnienia przyznane toouser **usługi SIECIOWEJ**. Hello certyfikatu ma nazwę podmiotu **CN \<tenantid\>, OU = Microsoft rozszerzenia serwera NPS**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Jak sprawdzić, czy Moje certyfikat klienta jest skojarzony toomy dzierżawy w usłudze Azure Active Directory?

Otwórz wiersz polecenia programu PowerShell i hello uruchom następujące polecenia:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Te polecenia Drukuj wszystkie certyfikaty hello kojarzenie dzierżawy z wystąpieniem hello rozszerzenia serwera NPS w sesji programu PowerShell. Wyszukaj certyfikat przez wyeksportowanie Twojego certyfikatu klienta w formacie "X.509(.cer) algorytmem Base-64" bez klucza prywatnego hello i porównania go z listy hello z programu PowerShell.

Nieprawidłowa-z i prawidłowe-dopóki sygnatury czasowe, które są w formie czytelny dla człowieka, może być używane toofilter się oczywiste misfits, jeśli polecenie hello zwraca więcej niż jeden certyfikat.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Dlaczego moje żądania kończą się niepowodzeniem z błędem tokenu ADAL?

Ten błąd może być z powodu tooone z kilku powodów. Wykonaj następujące kroki rozwiązywania toohelp:

1. Uruchom ponownie serwer NPS.
2. Sprawdź, czy ten certyfikat klienta jest zainstalowany, zgodnie z oczekiwaniami.
3. Sprawdź, czy certyfikat hello jest skojarzony z dzierżawą w usłudze Azure AD.
4. Sprawdź, czy ten https://login.microsoftonline.com/ jest dostępny z serwera hello systemem hello rozszerzenia.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Dlaczego uwierzytelniania nie ze względu na błąd w dziennikach HTTP informujący, że nie znaleziono użytkownika hello?

Sprawdź, czy działa AD Connect, a użytkownik hello jest obecny w usłudze Active Directory systemu Windows i usługi Azure Active Directory.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>Dlaczego widzę HTTP błędy w dziennikach Uzyskuj dostęp do mojej uwierzytelnienia się niepowodzeniem?

Sprawdź, czy ten https://adnotifications.windowsazure.com jest dostępny z serwera hello hello rozszerzenia serwera NPS.


## <a name="next-steps"></a>Następne kroki

- Konfigurowanie alternatywnych identyfikatorów logowania lub konfigurowania listy wyjątek dla adresów IP, która nie należy przeprowadzać weryfikację dwuetapową w [zaawansowane opcje konfiguracji hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe](nps-extension-advanced-configuration.md)

- [Komunikatami o błędach z hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-nps-errors.md)
