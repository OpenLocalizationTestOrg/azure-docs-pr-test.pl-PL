---
title: "Azure AD Connect: Rozwiązywanie problemów z łącznością | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak łączność tootroubleshoot problemów z programem Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Rozwiązywanie problemów z łącznością z programem Azure AD Connect
W tym artykule opisano, jak działa połączenie między Azure AD Connect i Azure AD i jak problemy z łącznością tootroubleshoot. Te problemy są najprawdopodobniej toobe w środowisku z serwerem proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Rozwiązywanie problemów z łącznością w Kreatorze instalacji hello
Azure AD Connect jest korzystających z nowoczesnego uwierzytelniania (przy użyciu biblioteki ADAL hello), do uwierzytelniania. Kreator instalacji Hello i hello aparatu synchronizacji odpowiednich wymagają toobe machine.config skonfigurowany prawidłowo, ponieważ te dwa aplikacji .NET.

W tym artykule zostanie przedstawiony sposób Fabrikam łączy tooAzure AD przy użyciu jego serwera proxy. Serwer proxy Hello nosi nazwę fabrikamproxy i używa portu 8080.

Najpierw musimy toomake czy [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) został poprawnie skonfigurowany.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> W niektórych blogi innych niż Microsoft jest udokumentowany czy należy dokonać zmian toomiiserver.exe.config zamiast tego. Jednak ten plik jest zastępowany na każdym uaktualnieniu, nawet jeśli działa podczas początkowej instalacji, hello system przestanie działać na pierwszym uaktualnienia. Z tego powodu hello zaleca tooupdate machine.config zamiast tego.
>
>

Serwer proxy Hello musi mieć również adresy URL hello wymagane otwarty. Lista oficjalnego Hello jest zawarta w [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Tych adresów URL hello w poniższej tabeli jest hello bezwzględną systemu od zera toobe minimalna stanie tooconnect tooAzure AD w ogóle. Ta lista nie zawiera żadnych opcjonalne funkcje, takie jak zapisywanie zwrotne haseł lub Azure AD Connect Health. Jest udokumentowany toohelp tutaj przy rozwiązywaniu hello początkową konfigurację.

| ADRES URL | Port | Opis |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Wyświetla listę używanych toodownload listy CRL. |
| \*. verisign.com |HTTP/80 |Wyświetla listę używanych toodownload listy CRL. |
| \*. entrust.com |HTTP/80 |Wyświetla listę listy CRL toodownload używane dla usługi MFA. |
| \*.windows.net |PROTOKOŁU HTTPS I 443 |Toosign używanych w tooAzure AD. |
| Secure.aadcdn.microsoftonline p.com |PROTOKOŁU HTTPS I 443 |Używany do uwierzytelniania Wieloskładnikowego. |
| \*.microsoftonline.com |PROTOKOŁU HTTPS I 443 |Używane tooconfigure danych usługi Azure AD directory i importowania/eksportowania. |

## <a name="errors-in-hello-wizard"></a>Błędy w Kreatorze hello
Kreator instalacji Hello korzysta z dwóch różnych kontekstach zabezpieczeń. Na stronie powitania **tooAzure AD Connect**, używa hello aktualnie zalogowany użytkownik. Na stronie powitania **Konfiguruj**, jest zmiana toohello [konta usługi hello aparatu synchronizacji hello](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Jeśli wystąpi problem, zostanie wyświetlone prawdopodobnie już na powitania **tooAzure AD Connect** w Kreatorze hello, ponieważ konfiguracja serwera proxy hello jest globalnego.

następujące problemy Hello są hello typowe błędy, które wystąpią w Kreatorze instalacji hello.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Kreator instalacji Hello nie został prawidłowo skonfigurowany
Ten błąd jest wyświetlany, gdy Kreator hello można nawiązać połączenia z powitania serwera proxy.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Jeśli zostanie wyświetlony ten błąd, sprawdź hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) została poprawnie skonfigurowana.
* Jeśli wygląda prawidłowe, wykonaj kroki hello w [weryfikacji łączności serwera proxy](#verify-proxy-connectivity) toosee, jeśli problem hello znajduje się poza również hello kreatora.

### <a name="a-microsoft-account-is-used"></a>Jest używane konto Microsoft
Jeśli używasz **konta Microsoft** zamiast **organizacji lub szkolnymi** konta, zobacz błąd ogólny.  
![Account firmy Microsoft jest używane](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>punkt końcowy usługi MFA Hello jest nieosiągalny
Ten błąd pojawia się, jeśli hello punktu końcowego **https://secure.aadcdn.microsoftonline-p.com** nie można nawiązać połączenia i administratora globalnego jest włączone uwierzytelnianie MFA.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Jeśli zostanie wyświetlony ten błąd, sprawdź tego punktu końcowego hello **secure.aadcdn.microsoftonline p.com** dodano toohello serwera proxy.

### <a name="hello-password-cannot-be-verified"></a>Nie można zweryfikować hasło Hello
Jeśli hello Kreator instalacji zakończy się pomyślnie z połączeniem tooAzure AD, ale nie można zweryfikować hello samego hasła, zobacz ten błąd:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Jest hasłem hello tymczasowego hasła i musi zostać zmienione? To jest rzeczywiście hello prawidłowe hasło? Spróbuj toosign w toohttps://login.microsoftonline.com (na innym komputerze niż serwer Azure AD Connect hello) i sprawdź, czy konto hello jest użyteczne.

### <a name="verify-proxy-connectivity"></a>Sprawdź łączność serwera proxy
tooverify Jeśli hello Azure AD Connect serwer ma rzeczywistego łączności z powitania serwera Proxy i Internet, użyj niektórych toosee PowerShell Jeśli powitania serwera proxy jest stosowanie żądania sieci web, lub nie. W wierszu programu PowerShell, uruchom `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Technicznie hello pierwsze wywołanie jest toohttps://login.microsoftonline.com i ten identyfikator URI działa również, ale hello innych URI toorespond szybsze).

PowerShell korzysta z konfiguracji hello w pliku machine.config toocontact hello proxy. Ustawienia Hello winhttp/Netsh nie powinien mieć wpływ na tych poleceń cmdlet.

Jeśli serwer proxy hello jest skonfigurowany poprawnie, należy pobrać stan oznaczający powodzenie: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Jeśli zostanie wyświetlony **serwera zdalnego tooconnect toohello**, programu PowerShell próbuje toomake bezpośrednie wywołania bez użycia serwera proxy hello lub DNS nie jest poprawnie skonfigurowana. Upewnij się, że hello **machine.config** pliku jest poprawnie skonfigurowana.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Jeśli powitania serwera proxy nie jest skonfigurowane poprawnie, jest wyświetlany komunikat o błędzie: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Błąd | Tekst błędu | Komentarz |
| --- | --- | --- |
| 403 |Dostęp zabroniony |nie został otwarty powitania serwera proxy dla hello żądanego adresu URL. Ponownie hello konfiguracji serwera proxy i upewnij się, że hello [adresy URL](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) został otwarty. |
| 407 |Wymagane jest uwierzytelnianie serwera proxy |wymagany serwer proxy Hello logowania i żaden nie został podany. Jeśli serwer proxy wymaga uwierzytelnienia, upewnij się, że toohave to ustawienie skonfigurowane w pliku machine.config hello. Upewnij się, że korzystasz z konta domeny dla użytkownika hello hello kreatora i hello konta usługi. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>Witaj wzorzec komunikacji między Azure AD Connect i Azure AD
Jeśli zostały wykonane następujące kroki poprzedniego i nadal nie można połączyć, może w tym momencie uruchomić, analizując dzienniki sieci. W tej sekcji jest dokumentowanie wzorca normalnego i pomyślne łączność. Jest również wyświetlanie listy typowych śledzi czerwony, które może być ignorowane podczas czytania hello dzienniki sieci.

* Brak toohttps://dc.services.visualstudio.com wywołania. Nie jest wymagane toohave, który można zignorować ten adres URL, Otwórz na serwerze proxy hello hello toosucceed instalacji i te wywołania.
* Zobacz, zawierający toobe rzeczywiste hostów hello nsatc.net przestrzeni nazw DNS hello i innych przestrzeniach nazw pod microsoftonline.com nie rozpoznawania nazw dns. Jednak nie są wszystkie żądania usługi sieci web na powitania używanego serwera nazw i nie masz tooadd proxy toohello tych adresów URL.
* adminwebservice punkty końcowe Hello provisioningapi odnajdywania punktów końcowych i użyć toofind hello rzeczywisty punkt końcowy toouse. Te punkty końcowe są różne w zależności od regionu.

### <a name="reference-proxy-logs"></a>Odwołanie do dzienników serwera proxy
Poniżej przedstawiono zrzut z rzeczywistego proxy dziennika i hello Kreatora instalacji w przypadku wykonano (toohello zduplikowane wpisy tego samego punktu końcowego zostały usunięte). W tej sekcji może służyć jako odwołanie dla własnego dzienników serwera proxy i sieci. punkty końcowe rzeczywiste hello mogą się różnić w danym środowisku (w szczególności tych adresów URL w *kursywą*).

**Połącz tooAzure AD**

| Time | ADRES URL |
| --- | --- |
| 1/11/2016 8:31 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |Połącz: / /*bba800 zakotwiczenia*. microsoftonline.com:443 |
| 1/11/2016 8:32 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |Połącz: / /*bwsc02 przekazywania*. microsoftonline.com:443 |

**Konfigurowanie**

| Time | ADRES URL |
| --- | --- |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |Połącz: / /*bba800 zakotwiczenia*. microsoftonline.com:443 |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |Połącz: / /*bba900 zakotwiczenia*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |Połącz: / /*bba800 zakotwiczenia*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |Połącz: / /*bwsc02 przekazywania*. microsoftonline.com:443 |

**Początkowej synchronizacji**

| Time | ADRES URL |
| --- | --- |
| 1/11/2016 8:48 |Connect://login.Windows.NET:443 |
| 1/11/2016 8:49 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |Połącz: / /*bba900 zakotwiczenia*. microsoftonline.com:443 |
| 1/11/2016 8:49 |Połącz: / /*bba800 zakotwiczenia*. microsoftonline.com:443 |

## <a name="authentication-errors"></a>Błędy uwierzytelniania
W tej sekcji omówiono błędów, które mogą zostać zwrócone z biblioteki ADAL (Biblioteka uwierzytelniania hello używane przez program Azure AD Connect) i programu PowerShell. Błąd Hello wyjaśniono powinny pomóc w zrozumieć innej.

### <a name="invalid-grant"></a>Nieprawidłowy Grant
Nieprawidłowa nazwa użytkownika lub hasło. Aby uzyskać więcej informacji, zobacz [nie można zweryfikować hasło hello](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Typ nieznanego użytkownika
Katalog usługi Azure AD nie można odnaleźć lub rozwiązany. Może być próby toologin z nazwą użytkownika w niezweryfikowanej domeny?

### <a name="user-realm-discovery-failed"></a>Odnajdowanie obszaru użytkownika nie powiodło się
Problemy z konfiguracją sieci lub serwera proxy. Nie można osiągnąć Hello sieci. Zobacz [Rozwiązywanie problemów z łącznością w Kreatorze instalacji hello](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Hasło użytkownika wygasło
Twoje poświadczenia wygasły. Zmień hasło.

### <a name="authorizationfailure"></a>AuthorizationFailure
Nieznany problem.

### <a name="authentication-cancelled"></a>Uwierzytelnianie anulowane
Żądanie uwierzytelniania wieloskładnikowego (MFA) Hello zostało anulowane.

### <a name="connecttomsonline"></a>ConnectToMSOnline
Uwierzytelnianie zakończyło się pomyślnie, ale programu Azure AD PowerShell ma problem z uwierzytelnianiem.

### <a name="azurerolemissing"></a>AzureRoleMissing
Uwierzytelnianie zakończyło się pomyślnie. Nie jesteś administratorem globalnym.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Uwierzytelnianie zakończyło się pomyślnie. Zarządzanie tożsamościami uprzywilejowanymi został włączony i obecnie nie jesteś administratorem globalnym. Aby uzyskać więcej informacji, zobacz [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Uwierzytelnianie zakończyło się pomyślnie. Nie można pobrać informacji o firmie z usługi Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
Uwierzytelnianie zakończyło się pomyślnie. Nie można pobrać informacji o domenie z usługi Azure AD.

### <a name="unexpected-exception"></a>Nieoczekiwany wyjątek
Wyświetlany jako wystąpił nieoczekiwany błąd w Kreatorze instalacji hello. Może się zdarzyć przy próbie toouse **Account Microsoft** zamiast **konto służbowe lub organizacji**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Kroki rozwiązywania problemów z poprzednimi wersjami.
Z wersjami, począwszy od numeru kompilacji 1.1.105.0 (wydane luty 2016) hello Asystenta logowania w witrynie została wycofana. Ta konfiguracja sekcji i hello nie powinny już być wymagane, ale jest przechowywana jako odwołanie.

Witaj jednokrotnego w toowork Asystenta muszą być skonfigurowane winhttp. Tej konfiguracji można wykonać za pomocą [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Asystent logowania Hello nie został prawidłowo skonfigurowany
Ten błąd jest wyświetlany, gdy hello Asystenta logowania w witrynie nie można osiągnąć powitania serwera proxy lub nie zezwala na powitania serwera proxy hello żądania.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Jeśli zostanie wyświetlony ten błąd, obejrzyj hello konfiguracji serwera proxy w [netsh](active-directory-aadconnect-prerequisites.md#connectivity) i sprawdź poprawność.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Jeśli wygląda prawidłowe, wykonaj kroki hello w [weryfikacji łączności serwera proxy](#verify-proxy-connectivity) toosee, jeśli problem hello znajduje się poza również hello kreatora.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
