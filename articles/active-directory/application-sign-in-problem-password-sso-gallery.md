---
title: Problemy przy logowaniu do aplikacji Azure AD galerii skonfigurowane dla federacyjnych logowanie jednokrotne | Dokumentacja firmy Microsoft
description: "Jak rozwiązywać problemy z aplikacją Azure AD galerii skonfigurowane dla hasła logowania jednokrotnego"
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
ms.openlocfilehash: f8521d1386bba8004e84fe8862a5f59a65ea19ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>Problemy przy logowaniu do aplikacji Azure AD galerii skonfigurowane dla federacyjnego logowania jednokrotnego

Panel dostępu jest widok, a następnie uruchom chmurowych aplikacji, które administrator usługi Azure AD udzielił im dostępu do portalu sieci web, dzięki czemu użytkownik, który ma konto służbowe w usłudze Azure Active Directory (Azure AD). Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu. Panel dostępu jest oddzielony od portalu Azure i nie wymaga użytkownikom posiadania subskrypcji platformy Azure.

Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

## <a name="meeting-browser-requirements-for-the-access-panel"></a>Spełniające wymagania przeglądarki do panelu dostępu

Panel dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

Logowanie Jednokrotne opartego na hasłach można przeglądarki przez użytkownika końcowego:

-   Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy

-   Chrome — w systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych

-   Firefox 26.0 lub później — w systemie Windows XP SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy

>[!NOTE]
>Rozszerzenie logowania jednokrotnego opartego na hasłach stają się dostępne Edge w systemie Windows 10, gdy staną się również obsługiwany rozszerzenia przeglądarki Edge.
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a>Jak zainstalować rozszerzenie przeglądarki panelu dostępu

Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:

1.  Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.

3.  W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce być kierowane do łącza pobierania. **Dodaj** rozszerzenia do przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać rozszerzenia dla programu Chrome, a program Firefox z bezpośrednich łączy poniżej:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Konfigurowanie zasad grupy dla programu Internet Explorer

Możesz skonfigurować zasady grupy, które umożliwiają zdalnie zainstalować rozszerzenie Panel dostępu dla programu Internet Explorer na komputerach użytkowników.

Wymagania wstępne należą:

-   Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i dołączeniu komputerów użytkowników do domeny.

-   Musi mieć uprawnienie "Edytuj ustawienia" do edycji obiektu zasad grupy (GPO). Domyślnie to uprawnienie mają członków z następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy. [Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Czynności opisane w samouczku [wdrażanie rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) instrukcje krok po kroku dotyczące sposobu konfigurowania zasad grupy oraz wdrażanie dla użytkowników.

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a>Rozwiązywanie problemów z panelu dostępu w programie Internet Explorer

Postępuj zgodnie z [Rozwiązywanie problemów z rozszerzeniem Panel dostępu dla programu Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania rozszerzenia dla programu Internet Explorer.

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak skonfigurować hasło rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD

Aby skonfigurować aplikację z galerii Azure AD, która ma być:

-   [Dodawanie aplikacji w galerii Azure AD](#_Add_an_application)

-   [Skonfiguruj aplikację dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

-   [Przypisywanie użytkowników do aplikacji](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a>Dodawanie aplikacji w galerii Azure AD

Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:

1.  Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

2.  Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.

6.  W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.

7.  Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.

8.  Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.

9.  Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.

### <a name="configure-the-application-for-password-single-sign-on"></a>Skonfiguruj aplikację dla hasła logowania jednokrotnego

Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:

1.  Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**

6.  Wybierz aplikację, aby skonfigurować logowanie jednokrotne

7.  Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.

8.  Wybierz tryb **opartego na hasłach logowania jednokrotnego.**

9.  [Przypisywanie użytkowników do aplikacji](#_How_to_assign).

10. Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników. W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.

### <a name="assign-users-to-the-application"></a>Przypisywanie użytkowników do aplikacji

Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:

1.  Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**

6.  Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.

7.  Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.

8.  Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.

9.  Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.

10. Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**. Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.

12. **Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.

13. Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.

14. **Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.

15. Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.

Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.

## <a name="if-these-troubleshoot-steps-dont-resolve-the-issue"></a>Jeśli te Rozwiązywanie problemów z kroki nie rozwiążą problem 
Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
