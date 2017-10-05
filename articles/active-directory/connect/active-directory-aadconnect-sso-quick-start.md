---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — Szybki Start | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak rozpocząć pracę z usługi Azure Active Directory bezproblemowe logowanie jednokrotne."
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory bezproblemowe logowanie jednokrotne: Szybki start

## <a name="how-to-deploy-seamless-sso"></a>Jak wdrożyć bezproblemowe logowanie Jednokrotne

Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne) automatycznie podpisuje użytkowników, gdy są na komputerach stacjonarnych firmowej podłączone do sieci firmowej. Umożliwia użytkownikom łatwy dostęp do aplikacji opartej na chmurze bez konieczności żadnych składników dodatkowych lokalnych.

>[!IMPORTANT]
>Funkcja logowania jednokrotnego bezproblemowe jest obecnie w przeglądzie.

Aby wdrożyć bezproblemowe logowania jednokrotnego, musisz wykonaj następujące kroki:

## <a name="step-1-check-prerequisites"></a>Krok 1: Sprawdź wymagania wstępne

Upewnij się, że zostały spełnione następujące wymagania wstępne:

1. Konfigurowanie serwera usługi Azure AD Connect: Jeśli używasz [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) jako metody logowania, są wymagane żadne dalsze akcje. Jeśli używasz [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) jako metody logowania, a w przypadku zapory między Azure AD Connect i Azure AD, upewnij się, że:
- W przypadku korzystania z wersji 1.1.484.0 lub nowszej programu Azure AD Connect.
- Azure AD Connect może komunikować się z `*.msappproxy.net` adresy URL i przez port 443. To wymaganie wstępne dotyczy tylko po włączeniu funkcji, nie do rzeczywistego użytkownika logowania.
- Azure AD Connect można nawiązywać połączenia IP bezpośrednio z [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653). Ponownie te wymagania wstępne ma zastosowanie tylko wtedy, gdy zostanie włączona funkcja.
2. Dla każdego lasu usługi AD, synchronizacji z usługą Azure AD (za pomocą usługi Azure AD Connect) i dla użytkowników, których chcesz włączyć bezproblemowe logowanie Jednokrotne potrzebne są poświadczenia administratora domeny.

## <a name="step-2-enable-the-feature"></a>Krok 2: Włączanie funkcji

Bezproblemowe logowanie Jednokrotne można włączyć za pomocą [Azure AD Connect](active-directory-aadconnect.md).

Jeśli przeprowadzasz nową instalację programu Azure AD Connect, wybierz [niestandardową ścieżkę](active-directory-aadconnect-get-started-custom.md). Na stronie "Logowanie użytkowników" zaznacz opcję "Włącz pojedynczy znak".

![Azure AD Connect - logowanie użytkowników](./media/active-directory-aadconnect-sso/sso8.png)

Jeśli masz już zainstalowany program Azure AD Connect, wybierz polecenie "Zmień użytkownika strony logowania" w Azure AD Connect, a następnie kliknij przycisk "Dalej". Następnie zaznacz opcję "Włącz pojedynczy znak".

![Azure AD Connect - zmiany logowania użytkownika](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Kontynuuj pracę z kreatorem, aż do strony "Włącz pojedynczy znak". Podaj poświadczenia administratora domeny dla każdego lasu usługi AD, synchronizacji z usługą Azure AD (za pomocą usługi Azure AD Connect) i dla użytkowników, których chcesz włączyć bezproblemowe logowania jednokrotnego. 

Po zakończeniu działania kreatora bezproblemowe rejestracji Jednokrotnej jest włączona na dzierżawy.

>[!NOTE]
> Poświadczenia administratora domeny nie są przechowywane w programie Azure AD Connect lub w usłudze Azure AD, ale tylko służą do włączenia tej funkcji.

Wykonaj te instrukcje, aby sprawdzić prawidłowo włączone bezproblemowe rejestracji Jednokrotnej:

1. Zaloguj się do [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.
2. Wybierz **usługi Azure Active Directory** w nawigacji po lewej stronie.
3. Wybierz **programu Azure AD Connect**.
4. Sprawdź, czy **bezproblemowe logowanie jednokrotne** funkcji jest pokazywana jako **włączone**.

![Portal Azure — blok Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a>Krok 3: Wdrażanie funkcji

Aby wdrożyć funkcję dla użytkowników, należy dodać adresów URL usługi Azure AD (https://autologon.microsoftazuread-sso.com i https://aadg.windows.net.nsatc.net) do ustawień intranetowej strefy użytkowników przy użyciu zasad grupy w usłudze Active Directory.

>[!NOTE]
> Poniższe instrukcje prawidłowe tylko dla programu Internet Explorer i Google Chrome w systemie Windows (Jeśli zestaw adresów URL zaufanych witryn współużytkuje z programu Internet Explorer). Przeczytaj następnej sekcji, aby uzyskać instrukcje dotyczące konfigurowania Mozilla Firefox i Google Chrome na komputerach Mac.

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a>Dlaczego należy zmodyfikować ustawienia strefy Intranet użytkowników?

Domyślnie przeglądarka automatycznie oblicza prawo strefy (w Internecie lub intranecie) z adresu URL. Na przykład http://contoso/ jest mapowany do strefy Intranet, podczas gdy http://intranet.contoso.com/ jest mapowany na strefie Internet (ponieważ adres URL zawiera kropkę). Przeglądarki nie wysyłaj biletów Kerberos do punktu końcowego w chmurze — takich jak Azure adresów URL AD - chyba, że adres URL jest w sposób jawny dodane do strefy Intranet w przeglądarce.

### <a name="detailed-steps"></a>Szczegółowe procedury

1. Otwórz narzędzie Zarządzanie zasadami grupy.
2. Edytowanie zasad grupy, która jest stosowana do niektórych lub wszystkich użytkowników. W tym przykładzie używamy **domyślne zasady domeny**.
3. Przejdź do **strony Panel\Security formantu użytkownika Konfiguracja komputera\Szablony administracyjne\Składniki systemu Windows\Internet Explorer\Internetowy** i wybierz **witrynę do strefy przypisania listy**.
![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso6.png)  
4. Włącz zasady, a następnie wprowadź następujące wartości (gdzie bilety Kerberos są przekazywane URL usługi Azure AD) i danych (*1* wskazuje strefy Intranet) w oknie dialogowym.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Jeśli chcesz uniemożliwić użytkownikom niektóre przy użyciu logowania jednokrotnego bezproblemowe — na przykład, jeśli ci użytkownicy są logują się na udostępnionym kioski — ustawioną poprzednimi wartościami *4*. Ta akcja dodaje adresy URL usługi Azure AD do strefy witryny z ograniczeniami, a nie powiedzie się bezproblemowe logowanie Jednokrotne cały czas.

5. Kliknij przycisk **OK** i **OK** ponownie.

![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Zagadnienia dotyczące przeglądarki

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox nie automatycznie wykonuje uwierzytelnianie Kerberos. Każdy użytkownik będzie musiał ręcznie dodać adresy URL usługi Azure AD do ich ustawień przeglądarki Firefox, wykonując następujące kroki:
1. Uruchom program Firefox, a następnie wprowadź `about:config` na pasku adresu. Odrzucić żadnych powiadomień, które są wyświetlane.
2. Wyszukaj **network.negotiate-auth.trusted URI** preferencji. Ta opcja wyświetla listę zaufanych witryn w programie Firefox uwierzytelniania Kerberos.
3. Kliknij prawym przyciskiem myszy i wybierz polecenie "Modyfikuj".
4. Wprowadź "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" w tym polu.
5. Kliknij przycisk "OK" i ponownie otwórz przeglądarkę.

#### <a name="safari-on-mac-os"></a>Przeglądarka Safari w systemie Mac OS

Upewnij się, że maszynę z systemem Mac OS jest przyłączony do usługi AD. Zobacz instrukcje na temat w tym [tutaj](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome w systemie Mac OS

Google Chrome na innych platform z systemem innym niż Windows i Mac OS, można znaleźć w temacie [w tym artykule](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) informacji na temat dozwolonych programu Azure AD adresy URL zintegrowane uwierzytelnianie.

Wdrażanie usługi Azure AD adresy URL Firefox i Google Chrome na użytkowników komputerów Mac za pomocą rozszerzenia innych firm zasad grupy usługi Active Directory jest poza zakres tego artykułu.

#### <a name="known-limitations"></a>Znane ograniczenia

Bezproblemowe logowanie Jednokrotne nie działa w trybie prywatnym przeglądania na przeglądarki Firefox i krawędzi. Również nie działa w programie Internet Explorer Jeśli przeglądarka jest uruchomiony w trybie ochrona rozszerzona.

>[!IMPORTANT]
>Firma Microsoft niedawno wycofane obsługę krawędzi do badania problemów zgłoszonych przez klientów.

## <a name="step-4-test-the-feature"></a>Krok 4: Testowanie funkcji

Aby przetestować tę funkcję dla określonego użytkownika, upewnij się, że _wszystkie_ są spełnione następujące warunki:
  - Użytkownik loguje się na urządzeniach firmowych.
  - Urządzenia został wcześniej przyłączony do domeny usługi Active Directory (AD).
  - Urządzenie korzysta z bezpośredniego połączenia do Twojej domeny kontrolera (DC), w firmowej sieci przewodowej lub bezprzewodowej lub za pośrednictwem połączenia dostępu zdalnego, takich jak połączenia sieci VPN.
  - Masz [wprowadzanie funkcję](##step-3-roll-out-the-feature) do tego użytkownika za pomocą zasad grupy.

Do przetestowania tego scenariusza, w którym użytkownik musi wprowadzić tylko nazwę użytkownika, ale nie hasło:
- Zaloguj się do *https://myapps.microsoft.com/* w nowej sesji przeglądarki prywatnych.

Do przetestowania tego scenariusza, w którym użytkownik nie musi wprowadzić nazwę użytkownika lub hasło: 
- Zaloguj się do *https://myapps.microsoft.com/contoso.onmicrosoft.com* w nowej sesji przeglądarki prywatnych. Zastąp "*contoso*" nazwą swojej dzierżawy.
- Lub zaloguj się do *https://myapps.microsoft.com/contoso.com* w nowej sesji przeglądarki prywatnych. Zastąp "*contoso.com*" z zweryfikowanej domeny (nie domeny federacyjnej) w dzierżawie.

## <a name="step-5-roll-over-keys"></a>Krok 5: Przerzucane kluczy

W kroku 2 Azure AD Connect tworzy konta komputerów (reprezentujący usługi Azure AD) we wszystkich lasach AD, na których włączono bezproblemowe logowania jednokrotnego. Dowiedz się więcej szczegółów w [tutaj](active-directory-aadconnect-sso-how-it-works.md). Ze względów bezpieczeństwa zaleca się, że często wdrożysz za pośrednictwem protokołu Kerberos kluczy odszyfrowywania tych kont komputerów.

>[!IMPORTANT]
>Nie trzeba wykonać ten krok _natychmiast_ po włączeniu funkcji. Przerzuć klucze Kerberos odszyfrowywania co najmniej 30 dni.

## <a name="next-steps"></a>Następne kroki

- [**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) — odpowiedzi na często zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak rozwiązać typowe problemy z funkcją.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
