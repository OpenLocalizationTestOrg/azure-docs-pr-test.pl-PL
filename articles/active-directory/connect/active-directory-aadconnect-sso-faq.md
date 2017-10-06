---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Toofrequently odpowiedzi zadawane pytania dotyczące Azure Active Directory bezproblemowe rejestracji jednokrotnej."
services: active-directory
keywords: "Co to jest usługa Azure AD Connect, zainstaluj usługę Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory bezproblemowe logowanie jednokrotne: często zadawane pytania

W tym artykule można rozwiązać często zadawane pytania o Azure Active Directory bezproblemowe rejestracji jednokrotnej (SSO bezproblemowe). Sprawdzanie wstecz dla nowej zawartości.

>[!IMPORTANT]
>funkcja logowania jednokrotnego bezproblemowe Hello jest obecnie w przeglądzie.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Jakie metody logowania SSO bezproblemowe działają z?

Bezproblemowe logowanie Jednokrotne można łączyć z obu hello [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) lub [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) metody logowania. Jednak ta funkcja nie można używać z Active Directory Federation Services (ADFS).

## <a name="is-seamless-sso-a-free-feature"></a>Jest funkcją wolnego bezproblemowe logowanie Jednokrotne?

Bezproblemowe rejestracji Jednokrotnej jest funkcją wolnego i nie wymagają żadnych płatnej wersji usługi Azure AD toouse go. Nadal pozostaje wolny, gdy funkcja hello osiągnie ogólnej dostępności.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Jakie aplikacje korzystać z `domain_hint` lub `login_hint` parametru możliwości łatwego logowania jednokrotnego?

Jesteśmy w procesie hello kompilowanie hello listę aplikacji, które wysyłają te parametry i hello te, które nie. Jeśli masz aplikacje, które są zainteresowani, Daj nam znać hello sekcji komentarzy.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Obsługuje rejestracji Jednokrotnej bezproblemowe `Alternate ID` jako hello nazwy użytkownika, a nie `userPrincipalName`?

Tak. Bezproblemowe logowanie Jednokrotne obsługuje `Alternate ID` jako hello nazwy użytkownika, gdy skonfigurowane w programie Azure AD Connect, jak pokazano [tutaj](active-directory-aadconnect-get-started-custom.md). Nie wszystkie aplikacje usługi Office 365 obsługują `Alternate ID`. Zapoznaj się z dokumentacją toohello określonej aplikacji hello obsługi instrukcji.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Chcę tooregister urządzeń z systemem innym niż Windows 10 z usługą Azure AD, bez korzystania z usług AD FS. Można używać logowania jednokrotnego bezproblemowe zamiast niego?

Tak, ten scenariusz wymaga wersji 2.1 lub nowszej hello [Dołącz do miejsca pracy klienta](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Jak można I Przerzuć klucz odszyfrowywania Kerberos hello hello `AZUREADSSOACCT` konto komputera?

Koniecznie toofrequently Przerzuć klucz odszyfrowywania Kerberos hello hello `AZUREADSSOACCT` konta komputera, (co reprezentuje usługi Azure AD) utworzone w lokalnym lesie usługi Active Directory.

>[!IMPORTANT]
>Zdecydowanie zaleca się wdrażanie za pośrednictwem klucz odszyfrowujący Kerberos hello co najmniej 30 dni.

Wykonaj następujące kroki na powitania serwera lokalnego, na którym uruchomiony jest program Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Krok 1. Pobierz listę lasów usługi AD, w którym włączono bezproblemowe logowanie Jednokrotne

1. Najpierw należy pobrać i zainstalować hello [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Następnie Pobierz i zainstaluj hello [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Przejdź toohello `%programfiles%\Microsoft Azure Active Directory Connect` folderu.
4. Moduł bezproblemowe PowerShell logowania jednokrotnego hello importu za pomocą tego polecenia: `Import-Module .\AzureADSSO.psd1`.
5. Uruchom program PowerShell jako Administrator. W programie PowerShell, wywołaj `New-AzureADSSOAuthenticationContext`. To polecenie powinien zapewnić tooenter podręcznego poświadczenia administratora globalnego Twojej dzierżawy.
6. Wywołanie `Get-AzureADSSOStatus`. Tego polecenia zapewnia hello listy lasów usługi AD (zobacz listę domen"hello"), na którym ta funkcja została włączona.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Krok 2. Zaktualizuj klucz odszyfrowujący Kerberos hello w każdym lesie usługi AD, skonfigurowanego go go na

1. Wywołanie `$creds = Get-Credential`. Po wyświetleniu monitu wprowadź poświadczenia administratora domeny hello na powitania przeznaczone lesie usługi Active Directory.
2. Wywołanie `Update-AzureADSSOForest -OnPremCredentials $creds`. To polecenie aktualizacji hello klucz odszyfrowujący protokołu Kerberos dla hello `AZUREADSSOACCT` konto komputera, w tym określonym lesie usługi AD i aktualizuje go w usłudze Azure AD.
3. Powtórz hello w poprzednich krokach dla każdego lasu usługi AD, która po skonfigurowaniu funkcji hello na.

>[!IMPORTANT]
>Upewnij się, że _nie_ Uruchom hello `Update-AzureADSSOForest` polecenia więcej niż raz. W przeciwnym razie funkcja hello przestanie działać do czasu hello biletów Kerberos użytkowników wygaśnie i są ponownie w lokalnej usługi Active Directory.

## <a name="how-can-i-disable-seamless-sso"></a>Jak wyłączyć bezproblemowe logowanie Jednokrotne

Bezproblemowe logowania jednokrotnego, można wyłączyć za pomocą usługi Azure AD Connect.

Uruchom usługi Azure AD Connect, wybierz polecenie "Zmień użytkownika strony logowania" i kliknij przycisk "Dalej". Następnie usuń zaznaczenie opcji "Włącz logowanie jednokrotne" hello. Kontynuuj pracę kreatora hello. Po zakończeniu Kreatora hello bezproblemowe rejestracji Jednokrotnej jest wyłączona na dzierżawy.

Jednakże zostanie wyświetlony komunikat na ekranie odczytujący w następujący sposób:

"Rejestracji jednokrotnej jest obecnie wyłączony, ale brak tooperform ręczne wykonanie dodatkowych czynności w kolejności toocomplete czyszczenia. Dowiedz się więcej"

toocomplete hello procesu, wykonaj czynności ręcznych hello na lokalny serwer, na którym uruchomiony jest program Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Krok 1. Pobierz listę lasów usługi AD, w którym włączono bezproblemowe logowanie Jednokrotne

1. Najpierw należy pobrać i zainstalować hello [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Następnie Pobierz i zainstaluj hello [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Przejdź toohello `%programfiles%\Microsoft Azure Active Directory Connect` folderu.
4. Moduł bezproblemowe PowerShell logowania jednokrotnego hello importu za pomocą tego polecenia: `Import-Module .\AzureADSSO.psd1`.
5. Uruchom program PowerShell jako Administrator. W programie PowerShell, wywołaj `New-AzureADSSOAuthenticationContext`. To polecenie powinien zapewnić tooenter podręcznego poświadczenia administratora globalnego Twojej dzierżawy.
6. Wywołanie `Get-AzureADSSOStatus`. Tego polecenia zapewnia hello listy lasów usługi AD (zobacz listę domen"hello"), na którym ta funkcja została włączona.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Krok 2. Ręcznie usuń hello `AZUREADSSOACCT` konta komputera w każdym lesie usługi AD, który zostanie wyświetlony na liście.

## <a name="next-steps"></a>Następne kroki

- [**Szybki Start** ](active-directory-aadconnect-sso-quick-start.md) — Uzyskaj i systemem Azure AD bezproblemowe Usługa rejestracji Jednokrotnej.
- [**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
