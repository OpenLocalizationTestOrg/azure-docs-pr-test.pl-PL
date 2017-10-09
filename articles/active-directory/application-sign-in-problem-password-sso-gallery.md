---
title: aaaProblems logowanie tooan aplikacji Azure AD galerii skonfigurowane dla federacyjnych logowanie jednokrotne | Dokumentacja firmy Microsoft
description: "Jak tootroubleshoot problemy związane z galerii Azure AD aplikacji skonfigurowana dla hasła logowania jednokrotnego"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>Problemy przy logowaniu tooan galerii Azure AD aplikacji skonfigurowana dla federacyjnego logowania jednokrotnego

Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do. Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu. Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.

toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu

Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:

-   Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy

-   Chrome — w systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych

-   Firefox 26.0 lub później — w systemie Windows XP SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy

>[!NOTE]
>Witaj opartego na hasłach logowania jednokrotnego rozszerzenie udostępnienie Edge w systemie Windows 10, gdy staną się również obsługiwany rozszerzenia przeglądarki Edge.
>
>

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

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Konfigurowanie zasad grupy dla programu Internet Explorer

Możesz skonfigurować zasady grupy, które pozwalają tooremotely instalacji hello panelu dostępu rozszerzenie programu Internet Explorer na komputerach użytkowników.

wymagania wstępne Hello obejmują:

-   Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.

-   Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO). Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy. [Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Czynności opisane w samouczku hello [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) instrukcje krok po kroku dotyczące sposobu tooconfigure hello zasad grupy i wdróż je toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Rozwiązywanie problemów z hello panelu dostępu w programie Internet Explorer

Wykonaj hello [rozwiązywanie hello rozszerzenia Panel dostępu dla programu Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania hello rozszerzenia dla programu Internet Explorer.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji hello galerii Azure AD](#_Add_an_application)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

-   [Przypisywanie użytkowników toohello aplikacji](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Dodawanie aplikacji hello galerii Azure AD

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

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

6.  Wybierz hello aplikację tooconfigure rejestracji jednokrotnej

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  [Przypisywanie użytkowników aplikacji toohello](#_How_to_assign).

10. Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello. W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.

### <a name="assign-users-toohello-application"></a>Przypisywanie użytkowników toohello aplikacji

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

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a>Jeśli te Rozwiązywanie problemów z czynności nie rozwiązuje problemu hello 
Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
