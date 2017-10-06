---
title: "aaaProblem podpisywania w witrynie internetowej panelu dostępu toohello | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące tootroubleshoot problemy, które można napotkać podczas próby toosign w toouse hello panelu dostępu"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Problem z logowaniem toohello dostępu panelu witryny sieci Web

Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do. Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu. Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.

Użytkownicy może się zalogować w toohello panelu dostępu, jeśli ma konto służbowe w usłudze Azure AD.

-   Użytkownicy mogą być uwierzytelniane przez usługę Azure AD bezpośrednio.

-   Użytkownicy mogą uwierzytelniać za pomocą usługi Active Directory Federation Services (AD FS).

-   Użytkownicy mogą być uwierzytelniane przez usługę Active Directory systemu Windows Server.

Jeśli użytkownik ma subskrypcję platformy Azure lub usługi Office 365 i używa hello portalu Azure lub aplikacji pakietu Office 365, aby były toouse można bezproblemowo hello Panel dostępu, bez konieczności toosign w ponownie. Użytkownicy, którzy nie zostali uwierzytelnieni się zostanie wyświetlony monit o toosign w za pomocą hello nazwę użytkownika i hasło dla swojego konta w usłudze Azure AD. Jeśli hello organizacji skonfigurował federacyjnych, wpisując hello username jest wystarczająca.

## <a name="general-issues-toocheck-first"></a>Ogólne problemy toocheck najpierw 

-   Upewnij się, że hello użytkownik loguje się toohello **Popraw adres URL**: <https://myapps.microsoft.com>

-   Upewnij się, że przeglądarka hello użytkownika został dodany hello tooits adres URL **Zaufane witryny**

-   Upewnij się, że konto użytkownika hello jest **włączone** dla logowania.

-   Upewnij się, że konto użytkownika hello jest **bez blokady.**

-   Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**

-   Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.

-   Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.

-   Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.

-   Upewnij się, że tooalso spróbuj wyczyszczenie plików cookie w przeglądarce i podjęcie ponownej próby toosign w.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu

Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:

-   Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy

-   Krawędź w systemie Windows 10 Anniversary Edition lub nowszy 

-   Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych

-   Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy


## <a name="problems-with-hello-users-account"></a>Problemy z kontem użytkownika hello

Powodu tooa problem z kontem użytkownika hello mogą zostać zablokowane toohello dostęp do panelu dostępu. Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:

-   [Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Sprawdź stan konta użytkownika](#check-a-users-account-status)

-   [Resetowanie hasła użytkownika](#reset-a-users-password)

-   [Włącz samoobsługowe resetowanie haseł](#enable-self-service-password-reset)

-   [Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status)

-   [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)

-   [Sprawdzanie członkostwa w grupach użytkownika](#check-a-users-group-memberships)

-   [Sprawdź przypisane licencje użytkownika](#check-a-users-assigned-licenses)

-   [Przypisywanie licencji użytkownika](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory

toocheck, jeśli konto użytkownika jest obecny, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Sprawdź właściwości hello hello użytkownika obiektu toobe się upewnić, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.

### <a name="check-a-users-account-status"></a>Sprawdź stan konta użytkownika

toocheck użytkownika konta stanu, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **profilu**.

8.  W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono zbyt**nr**.

### <a name="reset-a-users-password"></a>Resetowanie hasła użytkownika

tooreset hasło użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk hello **resetowania hasła** przycisk u góry bloku użytkownika hello hello.

8.  Kliknij przycisk hello **resetowania hasła** przycisk na powitania **resetowania hasła** wyświetlonym bloku.

9.  Kopiuj hello **hasło tymczasowe** lub **wprowadź nowe hasło** hello użytkownika.

10. Komunikować się z nowym użytkowniku toohello hasła, one toochange wymagane hasło podczas następnego Zaloguj tooAzure usługi Active Directory.

### <a name="enable-self-service-password-reset"></a>Włącz samoobsługowe Resetowanie hasła

hasło samoobsługi tooenable resetowania, wykonaj poniższe kroki wdrażania hello:

-   [Włącz użytkowników tooreset swoich haseł w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Włącz tooreset użytkowników lub zmieniać swoje hasła lokalnej usługi Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Sprawdź stan usługi Multi-Factor authentication użytkownika

toocheck użytkownika do usługi Multi-Factor stanu uwierzytelniania, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  Kliknij przycisk hello **uwierzytelnianie wieloskładnikowe** u góry hello hello bloku.

7.  Raz hello **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, znajdują się na powitania **użytkowników** kartę.

8.  Znajdź użytkownika hello hello listy użytkowników przez wyszukiwanie, filtrowanie i sortowanie.

9.  Wybierz hello użytkownika z listy hello użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.

   >[!NOTE]
   >Jeśli użytkownik znajduje się w **wymuszone** stanu może ustawić je także**wyłączone** tymczasowo toolet je z powrotem do swojego konta. Gdy są one ponownie, można zmienić stanu za**włączone** ponownie toorequire je zarejestrować toore, zaloguj się do niego swoje informacje kontaktowe podczas następnego. Alternatywnie można wykonać kroki hello w hello [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) tooverify lub ustaw dla nich dane.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Sprawdź informacje kontaktowe uwierzytelniania użytkownika

toocheck uwierzytelniania użytkownika informacje używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania haseł, skontaktuj się z pomocą wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **profilu**.

8.  Przewiń w dół za**informacje kontaktowe uwierzytelniania**.

9.  **Przegląd** hello danych zarejestrowane dla użytkownika hello i aktualizacji, zgodnie z potrzebami.

### <a name="check-a-users-group-memberships"></a>Sprawdzanie członkostwa w grupach użytkownika

toocheck użytkownika członkostw, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **grup** toosee, który grupuje hello użytkownika jest członkiem.

### <a name="check-a-users-assigned-licenses"></a>Sprawdź przypisane licencje użytkownika

toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.

### <a name="assign-a-user-a-license"></a>Przypisywanie licencji użytkownika 

tooassign tooa licencji użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **wszyscy użytkownicy**.

6.  **Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.

7.  Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.

8.  Kliknij przycisk hello **przypisać** przycisku.

9.  Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.

10. **Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów. Kliknij przycisk **Ok** po zakończeniu.

11. Kliknij przycisk hello **przypisać** przycisk tooassign użytkownika toothis tych licencji.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Identyfikator dzierżawy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
