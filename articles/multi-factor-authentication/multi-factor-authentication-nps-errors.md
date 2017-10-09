---
title: "kody błędów aaaTroubleshoot hello rozszerzenia usługi Azure MFA NPS | Dokumentacja firmy Microsoft"
description: "Uzyskaj pomoc dotyczącą rozwiązywania problemów związanych z hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure z określonego rozwiązania dla typowe komunikaty o błędach"
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
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Komunikatami o błędach z hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure

Jeśli wystąpią błędy hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure, użyj tego artykułu tooreach rozwiązanie szybciej. 

## <a name="troubleshooting-steps-for-common-errors"></a>Kroki rozwiązywania problemów dotyczących typowych błędów

| Kod błędu: | Kroki rozwiązywania problemów |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Skontaktuj się z pomocą techniczną](#contact-microsoft-support)i opisz hello lista czynności do zbierania dzienników. Podaj te informacje, które można o co się stało przed błąd hello, w tym identyfikator dzierżawcy i główna nazwa użytkownika (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Może to być problem z jak hello certyfikat klienta został zainstalowany lub skojarzony z dzierżawą. Postępuj zgodnie z instrukcjami hello [Rozwiązywanie problemów hello rozszerzenia serwera NPS MFA](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate problemy z certyfikatów klientów. |
| **ESTS_TOKEN_ERROR** | Postępuj zgodnie z instrukcjami hello [Rozwiązywanie problemów hello rozszerzenia serwera NPS MFA](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate certyfikatu klienta i ADAL token problemów. |
| **HTTPS_COMMUNICATION_ERROR** | serwer NPS Hello jest tooreceive odpowiedzi z usługi Azure MFA. Sprawdź, czy zapory są otwarte dwukierunkowo dla ruchu tooand z https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | Sprawdź, czy można osiągnąć https://adnotifications.windowsazure.com i https://login.microsoftonline.com/ na serwerze hello uruchomioną hello rozszerzenia serwera NPS. Jeśli te lokacje nie są ładowane, rozwiązywania problemów z łącznością na tym serwerze. |
| **REGISTRY_CONFIG_ERROR** | Brak klucza w rejestrze hello aplikacji hello, które mogą być, ponieważ hello [skrypt programu PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) nie został wykonany po instalacji. komunikat o błędzie Hello powinna zawierać hello Brak klucza. Upewnij się, że masz klucz hello w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa. |
| **REQUEST_FORMAT_ERROR** <br> Brak obowiązkowego atrybutu userName\Identifier promień żądania RADIUS. Sprawdź, czy serwer NPS jest odbierania żądań RADIUS | Ten błąd zazwyczaj odzwierciedla problemu. Witaj rozszerzenia serwera zasad Sieciowych muszą być zainstalowane w serwerach NPS, które mogą odbierać żądań RADIUS. Serwery NPS, które są zainstalowane jako zależności dla usług takich jak brama usług pulpitu zdalnego i usługa RRAS nie odbierania żądań radius. Rozszerzenia serwera NPS nie działa, gdy zainstalowany na takie instalacje i błędy out, ponieważ nie można odczytać szczegółów hello z żądania uwierzytelniania hello. |
| **REQUEST_MISSING_CODE** | Upewnij się, że hello hasło szyfrowania protokołu między powitania serwera zasad Sieciowych i serwerów NAS obsługuje hello dodatkowej metody uwierzytelniania używany. **PAP** obsługuje wszystkie hello metody uwierzytelniania usługi Azure MFA w chmurze hello: połączenie telefoniczne, wiadomość tekstowa jednokierunkowe powiadomienie aplikacji mobilnej i kod weryfikacyjny z aplikacji mobilnej. **CHAPV2** i **EAP** obsługi połączeń telefonicznych i powiadomienia aplikacji mobilnej. |
| **USERNAME_CANONICALIZATION_ERROR** | Sprawdź, czy hello użytkownik musi być obecny w lokalnym wystąpieniu usługi Active Directory i że hello usługi zasad Sieciowych ma uprawnienia tooaccess hello katalog. Jeśli używane są relacje zaufania między lasami, [się z pomocą techniczną](#contact-microsoft-support) Aby uzyskać dalszą pomoc. |


   

### <a name="alternate-login-id-errors"></a>Alternatywnego Identyfikatora błędów

| Kod błędu: | Komunikat o błędzie | Kroki rozwiązywania problemów |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Błąd: userObjectSid wyszukiwania nie powiodło się | Sprawdź, czy ten użytkownik hello istnieje w lokalnym wystąpieniu usługi Active Directory. Jeśli używane są relacje zaufania między lasami, [się z pomocą techniczną](#contact-microsoft-support) Aby uzyskać dalszą pomoc. |
| **ALTERNATE_LOGIN_ID_ERROR** | Błąd: Wyszukiwanie alternatywny LoginId nie powiodło się. | Sprawdź, czy LDAP_ALTERNATE_LOGINID_ATTRIBUTE jest ustawiony tooa [atrybut prawidłowe usługi active directory](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> LDAP_FORCE_GLOBAL_CATALOG ustawiono tooTrue lub LDAP_LOOKUP_FORESTS jest skonfigurowany z niepustą wartość, sprawdź, czy skonfigurowano wykazu globalnego, i atrybutu AlternateLoginId hello jest dodawany tooit. <br><br> LDAP_LOOKUP_FORESTS jest skonfigurowany z niepustą wartość, sprawdź, czy wartość hello jest poprawna. Jeśli istnieje więcej niż jedną nazwę lasu, hello nazwy muszą być oddzielone średnikami, nie spacji. <br><br> Jeśli te czynności nie rozwiąże problemu hello [się z pomocą techniczną](#contact-microsoft-support) Aby uzyskać dalszą pomoc. |
| **ALTERNATE_LOGIN_ID_ERROR** | Błąd: Alternatywne LoginId wartość jest pusta | Sprawdź, czy ten atrybut AlternateLoginId hello jest skonfigurowane dla użytkownika hello. |


## <a name="errors-your-users-may-encounter"></a>Mogą wystąpić błędy użytkowników

| Kod błędu: | Komunikat o błędzie | Kroki rozwiązywania problemów |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Dzierżawy obiekt wywołujący nie ma uwierzytelnianie toodo uprawnienia dostępu dla użytkownika hello | Sprawdź, czy hello dzierżawy domeny i domeny hello hello nazwy głównej użytkownika (UPN) są hello takie same. Na przykład, upewnij się, że user@contoso.com próbuje dzierżawie Contoso toohello tooauthenticate. Hello UPN reprezentuje prawidłowego użytkownika dzierżawcy hello na platformie Azure. |
| **AuthenticationMethodNotConfigured** | Metoda uwierzytelniania nie zostało skonfigurowane dla użytkownika hello określono Hello | Użytkownik hello dodania lub sprawdzenia ich metod weryfikacji, zgodnie z instrukcjami toohello [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Podanej metody uwierzytelniania nie jest obsługiwana. | Zbieraj wszystkie dzienniki zawierające ten błąd i [się z pomocą techniczną](#contact-microsoft-support). Kontakt z pomocą techniczną, podaj hello nazwy użytkownika i hello dodatkowej weryfikacji metody, która wyzwoliła błąd hello. |
| **BecAccessDenied** | Wywołanie MSODS Bec zwróciło odmowa dostępu, prawdopodobnie hello username nie został zdefiniowany w dzierżawie powitalnych | Użytkownik Hello znajduje się w lokalnym usługi Active Directory, ale nie jest synchronizowany do usługi Azure AD przez AD Connect. Lub hello użytkownika brakuje hello dzierżawcy. Dodaj hello tooAzure użytkownika AD, a następnie je dodać ich metod weryfikacji, zgodnie z instrukcjami toohello [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** lub **StrongAuthenticationServiceInvalidParameter** | numer telefonu Hello ma nierozpoznawalny format | Być użytkownik hello Popraw swoje numery telefonów weryfikacji. |
| **InvalidSession** | Witaj określona sesja jest nieprawidłowa lub mogło wygasnąć | Sesja Hello miało więcej niż trzy minuty toocomplete. Sprawdź, ten użytkownik hello jest wprowadzić kod weryfikacyjny hello lub odpowiada toohello powiadomienie aplikacji, w ciągu trzech minut inicjowania hello żądanie uwierzytelnienia. Jeśli to nie rozwiąże problemu hello, sprawdź, czy nie występują żadne opóźnień sieci między klienta, serwer NAS, serwer zasad Sieciowych i punktu końcowego usługi Azure MFA hello.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Dla użytkownika hello nie skonfigurowano żadnych domyślną metodą uwierzytelniania | Użytkownik hello dodania lub sprawdzenia ich metod weryfikacji, zgodnie z instrukcjami toohello [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md). Sprawdź użytkownika hello została wybrana opcja domyślną metodą uwierzytelniania i skonfigurowanej tej metody dla swojego konta. |
| **OathCodePinIncorrect** | Nieprawidłowy kod i wprowadzony numer pin. | Ten błąd nie jest oczekiwany w hello rozszerzenia serwera NPS. Jeśli użytkownikowi napotkał, [się z pomocą techniczną](#contact-microsoft-support) dla pomocy w rozwiązywaniu problemów. |
| **ProofDataNotFound** | Dowód danych nie została skonfigurowana dla hello określona metoda uwierzytelniania. | Użytkownik hello Spróbuj innej metody weryfikacji, lub Dodaj nowych metod weryfikacji, zgodnie z instrukcjami toohello [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md). Jeśli użytkownik hello kontynuuje toosee ten błąd po potwierdza, że ich metodę weryfikacji jest prawidłowo skonfigurowany, [się z pomocą techniczną](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Nieprawidłowy kod i wprowadzony numer pin. (OneWaySMS) | Ten błąd nie jest oczekiwany w hello rozszerzenia serwera NPS. Jeśli użytkownikowi napotkał, [się z pomocą techniczną](#contact-microsoft-support) dla pomocy w rozwiązywaniu problemów. |
| **TenantIsBlocked** | Dzierżawy jest zablokowany. | [Skontaktuj się z pomocą techniczną](#contact-microsoft-support) o identyfikatorze katalogu ze strony właściwości hello Azure AD w hello portalu Azure. |
| **UserNotFound** | Nie można odnaleźć określonego użytkownika Hello | Witaj dzierżawy nie jest już widoczna jako aktywny w usłudze Azure AD. Sprawdź, czy Twoja subskrypcja jest aktywna i masz hello wymagane pierwszej strony aplikacji. Upewnij się również hello dzierżawcy w podmiocie certyfikatu hello jest zgodne z oczekiwaniami i hello certyfikat jest nadal ważne i zarejestrowanych w obszarze hello nazwy głównej usługi. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Komunikaty dotyczące użytkowników mogą wystąpić, które nie są błędy

Czasami użytkownicy mogą pobrać wiadomości z usługi Multi-Factor Authentication, ponieważ żądanie ich uwierzytelnianie nie powiodło się. Te nie są błędy w produkcie hello konfiguracji, ale są zamierzone ostrzeżenia wyjaśniający, dlaczego żądanie uwierzytelniania zostało odrzucone.

| Kod błędu: | Komunikat o błędzie | Zalecane czynności | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Nieprawidłowy kod entered\OATH niepoprawny kod | To nie jest błąd, użytkownik wprowadził nieprawidłowy kod. | Witaj użytkownik wprowadził nieprawidłowy kod hello. Niech ponów żądanie o nowy kod lub zaloguj się ponownie. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Osiągnięto ponawiania maksymalny dozwolony kodu | Hello użytkownika nie powiodło się żądanie weryfikacji hello zbyt wiele razy. W zależności od ustawień potrzebnych toobe teraz odblokowany przez administratora.  |
| **SMSAuthFailedWrongCodeEntered** | Problem kodu wprowadzona/tekstu nieprawidłową OTP wiadomości | Witaj użytkownik wprowadził nieprawidłowy kod hello. Niech ponów żądanie o nowy kod lub zaloguj się ponownie. |

## <a name="errors-that-require-support"></a>Błędy, które wymagają obsługi

Jeśli wystąpią jeden z tych błędów, zaleca się możesz [się z pomocą techniczną](#contact-microsoft-support) diagnostycznego pomocy. Brak nie standardowy zestaw czynności rozwiązujących te błędy. Skontaktuj się z pomocą techniczną, być tooinclude się, jak dużo dowiedzieć się, jak to możliwe hello kroki, które spowodowały błąd tooan i informacje o Twojej dzierżawy.

| Kod błędu: | Komunikat o błędzie |
| ---------- | ------------- |
| **InvalidParameter** | Żądanie nie może mieć wartości null |
| **InvalidParameter** | Identyfikator obiektu nie może być zerowe ani puste dla ReplicationScope: {0} |
| **InvalidParameter** | Witaj długość NazwaFirmy \{0} \ jest dłuższa niż hello maksymalną dopuszczalną długość {1} |
| **InvalidParameter** | UserPrincipalName nie może być zerowy lub pusty |
| **InvalidParameter** | Witaj, pod warunkiem, że dla identyfikatora dzierżawcy nie znajduje się w poprawnym formacie |
| **InvalidParameter** | Identyfikator sesji nie może być zerowy lub pusty |
| **InvalidParameter** | Nie można rozpoznać żadnych ProofData z żądania lub Msods. Witaj ProofData jest nieznany |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Następne kroki

### <a name="troubleshoot-user-accounts"></a>Rozwiązywanie problemów z kontami użytkownika

Jeśli użytkownicy są [wystąpił problem w trakcie weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-troubleshoot.md), pomóc w ich własnym diagnozowanie problemów. 

### <a name="contact-microsoft-support"></a>Skontaktuj się z pomocą techniczną firmy Microsoft

Jeśli potrzebujesz dodatkowej pomocy, skontaktuj się z pracownikiem pomocy technicznej za pośrednictwem [obsługi serwera usługi Azure Multi-Factor Authentication](https://support.microsoft.com/oas/default.aspx?prid=14947). Podczas kontaktowania się z nami, jest przydatne, jeśli te informacje mogą obejmować o problem jak to możliwe. Zawiera informacje, które można podać hello strony, gdy był wyświetlany błąd hello, hello błędu kodu, identyfikator określonej sesji hello, hello identyfikator użytkownika hello, który był wyświetlany błąd hello, dzienników i debugowania.

dzienniki debugowania toocollect diagnostyki pomocy technicznej, użyj hello następujące kroki: 

1. Otwórz wiersz polecenia administratora i uruchom następujące polecenia:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Odtwórz problem hello

3. Zatrzymaj śledzenie hello przy użyciu następujących poleceń:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. ZIP hello zawartość folderu C:\NPS hello i Dołącz do sprawę pomocy technicznej toohello pliku zip hello.


