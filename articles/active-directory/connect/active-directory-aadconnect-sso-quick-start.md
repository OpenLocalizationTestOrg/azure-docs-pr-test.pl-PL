---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — Szybki Start | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób uruchamiania tooget z usługi Azure Active Directory bezproblemowe logowanie jednokrotne."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory bezproblemowe logowanie jednokrotne: Szybki start

## <a name="how-toodeploy-seamless-sso"></a>Jak toodeploy bezproblemowe logowanie Jednokrotne

Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne) automatycznie podpisuje użytkowników, gdy są w sieci firmowej tooyour połączonych komputerów firmowych. Umożliwia użytkownikom łatwe tooyour aplikacji działających w chmurze bez konieczności żadnych składników dodatkowych lokalnych.

>[!IMPORTANT]
>funkcja logowania jednokrotnego bezproblemowe Hello jest obecnie w przeglądzie.

toodeploy bezproblemowe logowanie Jednokrotne, należy toofollow następujące kroki:

## <a name="step-1-check-prerequisites"></a>Krok 1: Sprawdź wymagania wstępne

Upewnij się, że hello następujące wymagania wstępne zostały spełnione:

1. Konfigurowanie serwera usługi Azure AD Connect: Jeśli używasz [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) jako metody logowania, są wymagane żadne dalsze akcje. Jeśli używasz [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) jako metody logowania, a w przypadku zapory między Azure AD Connect i Azure AD, upewnij się, że:
- W przypadku korzystania z wersji 1.1.484.0 lub nowszej programu Azure AD Connect.
- Azure AD Connect może komunikować się z `*.msappproxy.net` adresy URL i przez port 443. To wymaganie wstępne dotyczy tylko po włączeniu funkcji hello nie do rzeczywistego użytkownika logowania.
- Azure AD Connect można wprowadzać bezpośredniego toohello połączeń IP [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653). Ponownie te wymagania wstępne ma zastosowanie tylko wtedy, gdy zostanie włączona funkcja hello.
2. Potrzebne są poświadczenia administratora domeny dla każdego lasu usługi AD, aby synchronizować tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają tooenable bezproblemowe logowania jednokrotnego.

## <a name="step-2-enable-hello-feature"></a>Krok 2: Włączanie funkcji hello

Bezproblemowe logowanie Jednokrotne można włączyć za pomocą [Azure AD Connect](active-directory-aadconnect.md).

Jeśli przeprowadzasz nową instalację programu Azure AD Connect, wybierz hello [niestandardową ścieżkę](active-directory-aadconnect-get-started-custom.md). Na powitania "użytkownika" strony logowania zaznacz opcję "Włącz logowanie jednokrotne" hello.

![Azure AD Connect - logowanie użytkowników](./media/active-directory-aadconnect-sso/sso8.png)

Jeśli masz już zainstalowany program Azure AD Connect, wybierz polecenie "Zmień użytkownika strony logowania" w Azure AD Connect, a następnie kliknij przycisk "Dalej". Następnie zaznacz opcję "Włącz logowanie jednokrotne" hello.

![Azure AD Connect - zmiany logowania użytkownika](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Kontynuacja za pomocą Kreatora hello pobrać toohello "Włącz logowanie jednokrotne" strony. Podaj poświadczenia administratora domeny dla każdego lasu usługi AD, aby synchronizować tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają tooenable bezproblemowe logowania jednokrotnego. 

Po zakończeniu Kreatora hello bezproblemowe rejestracji Jednokrotnej jest włączona na dzierżawy.

>[!NOTE]
> poświadczenia administratora domeny Hello nie są przechowywane w programie Azure AD Connect lub w usłudze Azure AD, ale są tylko używane tooenable hello funkcji.

Wykonaj te tooverify instrukcje prawidłowo włączona bezproblemowe rejestracji Jednokrotnej:

1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) z hello poświadczenia administratora globalnego dla dzierżawy.
2. Wybierz **usługi Azure Active Directory** na powitania nawigacji po lewej stronie.
3. Wybierz **programu Azure AD Connect**.
4. Sprawdź, że hello **bezproblemowe logowanie jednokrotne** funkcji jest pokazywana jako **włączone**.

![Portal Azure — blok Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Krok 3: Wdrażanie funkcji hello

tooroll hello funkcji tooyour użytkowników, należy tooadd dwie usługi Azure AD adresów URL (https://autologon.microsoftazuread-sso.com i https://aadg.windows.net.nsatc.net) toousers ustawienia strefy Intranet przy użyciu zasad grupy w usłudze Active Directory.

>[!NOTE]
> Witaj następujące instrukcje działa tylko dla programu Internet Explorer i Google Chrome w systemie Windows (Jeśli zestaw adresów URL zaufanych witryn współużytkuje z programu Internet Explorer). Przeczytaj hello następnej sekcji tooset instrukcje Mozilla Firefox i Google Chrome na komputerach Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Dlaczego należy ustawienia strefy Intranet toomodify użytkowników?

Domyślnie przeglądarki hello automatycznie oblicza hello prawo strefy (w Internecie lub intranecie) z adresu URL. Na przykład http://contoso/ jest mapowanych toohello strefy intranetowej, http://intranet.contoso.com/ jest mapowanych toohello strefy Internet (ponieważ hello adres URL zawiera kropkę). Przeglądarki wysyłaj punktu końcowego chmury tooa biletów Kerberos — jak hello dwa Azure AD adresy URL - chyba, że adres URL jest dodanych w sposób jawny strefy Intranet toohello przeglądarki.

### <a name="detailed-steps"></a>Szczegółowe procedury

1. Narzędzia do zarządzania zasadami grupy Otwórz hello.
2. Edytuj hello zasady grupy zastosowane toosome lub wszystkich użytkowników. W tym przykładzie używamy hello **domyślne zasady domeny**.
3. Przejdź za**strony Panel\Security formantu użytkownika Konfiguracja komputera\Szablony administracyjne\Składniki systemu Windows\Internet Explorer\Internetowy** i wybierz **tooZone Lista przypisywanie lokacji**.
![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso6.png)  
4. Włącz hello zasady, a następnie wprowadź hello następującej wartości (Azure adresy URL usługi AD w którym bilety Kerberos są przekazywane) i danych (*1* wskazuje strefy Intranet) w oknie dialogowym hello.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Toodisallow niektórych użytkowników przy użyciu logowania jednokrotnego bezproblemowe — na przykład, jeśli ci użytkownicy są logują się na udostępnionym kioski - ustawić hello poprzedzających wartości zbyt*4*. Ta akcja dodaje hello Azure AD adresy URL toohello strefy witryny z ograniczeniami, a nie bezproblemowe logowanie Jednokrotne cały czas hello.

5. Kliknij przycisk **OK** i **OK** ponownie.

![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Zagadnienia dotyczące przeglądarki

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox nie automatycznie wykonuje uwierzytelnianie Kerberos. Każdy użytkownik ma toomanually Dodaj adresy URL hello Azure AD tootheir Firefox ustawienia za pomocą hello następujące kroki:
1. Uruchom program Firefox, a następnie wprowadź `about:config` na pasku adresu hello. Odrzucić żadnych powiadomień, które są wyświetlane.
2. Wyszukaj hello **network.negotiate-auth.trusted URI** preferencji. Ta opcja wyświetla listę zaufanych witryn w programie Firefox uwierzytelniania Kerberos.
3. Kliknij prawym przyciskiem myszy i wybierz polecenie "Modyfikuj".
4. Wprowadź "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" hello pola.
5. Kliknij przycisk "OK" i ponownie otwórz hello przeglądarki.

#### <a name="safari-on-mac-os"></a>Przeglądarka Safari w systemie Mac OS

Upewnij się, czy maszyna hello z systemem Mac OS jest tooAD połączone. Zobacz instrukcje na temat toodo który [tutaj](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome w systemie Mac OS

Google Chrome na innych platform z systemem innym niż Windows i Mac OS, można znaleźć zbyt[w tym artykule](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) Aby uzyskać informacje dotyczące sposobu toowhitelist hello adresy URL usługi Azure AD dla zintegrowanego uwierzytelniania.

Przy użyciu innych zasad grupy usługi Active Directory tooroll rozszerzenia hello Azure AD adresy URL tooFirefox i Google Chrome na użytkowników komputerów Mac, wykracza poza zakres tego artykułu.

#### <a name="known-limitations"></a>Znane ograniczenia

Bezproblemowe logowanie Jednokrotne nie działa w trybie prywatnym przeglądania na przeglądarki Firefox i krawędzi. Również nie działa w programie Internet Explorer Jeśli przeglądarka hello jest uruchomiony w trybie ochrona rozszerzona.

>[!IMPORTANT]
>Firma Microsoft niedawno wycofane obsługę tooinvestigate krawędzi problemy zgłoszone przez klienta.

## <a name="step-4-test-hello-feature"></a>Krok 4: Testowanie hello funkcji

Funkcja hello tootest dla określonego użytkownika, upewnij się, że _wszystkie_ hello następujące warunki zostały spełnione:
  - Hello użytkownik loguje się na urządzeniach firmowych.
  - Witaj urządzenie zostało tooyour wcześniej przyłączone do domeny usługi Active Directory (AD).
  - urządzenie Hello ma bezpośredniego połączenia tooyour domenowych Kontrolerze, hello sieci przewodowej lub bezprzewodowej w sieci firmowej lub za pośrednictwem połączenia dostępu zdalnego, takich jak połączenia sieci VPN.
  - Masz [wprowadzanie funkcji hello](##step-3-roll-out-the-feature) toothis użytkownika przy użyciu zasad grupy.

Scenariusz hello tootest gdzie hello użytkownik wprowadza tylko hello nazwy użytkownika, ale nie hasło hello:
- Zaloguj się do *https://myapps.microsoft.com/* w nowej sesji przeglądarki prywatnych.

Scenariusz hello tootest gdzie hello użytkownika nie ma hasła nazwa użytkownika lub hello hello tooenter: 
- Zaloguj się do *https://myapps.microsoft.com/contoso.onmicrosoft.com* w nowej sesji przeglądarki prywatnych. Zastąp "*contoso*" nazwą swojej dzierżawy.
- Lub zaloguj się do *https://myapps.microsoft.com/contoso.com* w nowej sesji przeglądarki prywatnych. Zastąp "*contoso.com*" z zweryfikowanej domeny (nie domeny federacyjnej) w dzierżawie.

## <a name="step-5-roll-over-keys"></a>Krok 5: Przerzucane kluczy

W kroku 2 Azure AD Connect tworzy kont komputerów (reprezentujący usługi Azure AD) w wszystkich lasach hello AD, na których włączono bezproblemowe logowania jednokrotnego. Dowiedz się więcej szczegółów w [tutaj](active-directory-aadconnect-sso-how-it-works.md). Ze względów bezpieczeństwa zaleca się, że można często są przerzucane hello Kerberos odszyfrowywania klucze te konta komputera.

>[!IMPORTANT]
>Nie trzeba toodo ten krok _natychmiast_ po włączeniu funkcji hello. Przerzuć kluczy odszyfrowujących Kerberos hello co najmniej 30 dni.

## <a name="next-steps"></a>Następne kroki

- [**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
