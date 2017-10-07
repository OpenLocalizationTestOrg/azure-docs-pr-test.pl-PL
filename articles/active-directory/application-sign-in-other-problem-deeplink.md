---
title: "Logowanie przy użyciu głębokiego łącza aplikacji tooan aaaProblems | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy dotyczące uzyskiwania dostępu do aplikacji z adres URL głębokiego łącza za pomocą usługi Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a>Problemy przy logowaniu tooan aplikacji przy użyciu głębokiego łącza

Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do. 

Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello. Aplikacja Hello musi być prawidłowo skonfigurowane i przypisane toohello użytkownika lub grupy hello użytkownika jest członkiem grupy aplikacji hello toosee w hello panelu dostępu.

Linków bezpośrednich lub dostęp użytkownika adresy URL są łącza, które użytkownicy mogą korzystać tooaccess ich rejestracji Jednokrotnej hasła aplikacji bezpośrednio ze swojego adresu URL przeglądarek pasków. Przechodząc toothis łącza, użytkownicy będą automatycznie zalogowaniem się do aplikacji hello bez toohello toogo panelu dostępu. Jest to hello tego samego łącza, czy użytkownicy przy użyciu tooaccess tych aplikacji z uruchamianie aplikacji hello usługi Office 365.

## <a name="general-issues-toocheck-first"></a>Ogólne problemy toocheck najpierw

-   Upewnij się, Twoje przy użyciu **przeglądarki** który spełnia wymagania minimalne hello hello panelu dostępu.

-   Upewnij się, że przeglądarka hello użytkownika został dodany adres URL hello tooits aplikacji hello **Zaufane witryny**.

-   Upewnij się, że aplikacja hello toocheck **skonfigurowane** poprawnie.

-   Upewnij się, że konto użytkownika hello jest **włączone** dla logowania.

-   Upewnij się, że konto użytkownika hello jest **bez blokady.**

-   Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**

-   Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.

-   Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.

-   Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.

-   Upewnij się, że tooalso spróbuj wyczyszczenie plików cookie w przeglądarce i podjęcie ponownej próby toosign w.

## <a name="checking-hello-deeplink"></a>Sprawdzanie, czy hello głębokiego łącza.

toocheck, jeśli masz poprawne głębokiego łącza hello, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

7.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

8.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

9.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

10. Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

11. Wybierz hello aplikacji hello głębokiego łącza hello wyboru dla.

12. Znajdź etykietę hello **adres URL dostępu użytkownika**. Ten adres URL głębokiego łącza można powinna być zgodna.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu

hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:

1.  Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.

3.  Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce można ukierunkowanej toohello łącze. **Dodaj** hello rozszerzenia tooyour przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji hello galerii Azure AD](#add-an-application-from-the-Azure-AD-gallery)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Dodawanie aplikacji hello galerii Azure AD

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.

6.  W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.

7.  Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.

8.  Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.

9.  Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego

tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  [Przypisywanie użytkowników aplikacji toohello](#how-to-assign-a-user-to-an-application-directly).

10. Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello. W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji z systemem innym niż galerii](#add-a-non-gallery-application)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Dodawanie aplikacji z systemem innym niż galerii

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.

6.  Kliknij przycisk **Non galerii aplikacji.**

7.  Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego. Wybierz **dodać.**

Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego

tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

    1.  Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  Wprowadź hello **adres URL logowania**. Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu. Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.

10. Przypisywanie użytkowników toohello aplikacji.

11. Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello. W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Jak tooassign bezpośrednio aplikację tooan użytkownika

tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.

9.  Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.

10. Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**. Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.

12. **Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.

13. Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.

14. **Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.

15. Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.

Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello. 

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
