---
title: "podpisywania aplikacji tooan z panelu dostępu hello aaaProblems | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy dotyczące uzyskiwania dostępu do aplikacji z hello panelu dostępu do programu Microsoft Azure AD w myapps.microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Problemy przy logowaniu tooan aplikacji hello panelu dostępu

Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do. 

Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello. Aplikacja Hello musi być prawidłowo skonfigurowane i przypisane toohello użytkownika lub grupy hello użytkownika jest członkiem grupy aplikacji hello toosee w hello panelu dostępu.

Typ Hello aplikacje, które użytkownik może być widoczny spadek hello następujące kategorie:

-   Aplikacje pakietu Office 365

-   Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego

-   Aplikacje oparte na hasłach logowania jednokrotnego

-   Aplikacje z istniejącymi rozwiązaniami do logowania jednokrotnego

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

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu

Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS. toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello. To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.

Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:

-   Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy

-   Krawędź w systemie Windows 10 Anniversary Edition lub nowszy

-   Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych

-   Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu

hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:

1.  Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.

3.  Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce można ukierunkowanej toohello łącze. **Dodaj** hello rozszerzenia tooyour przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji

Może również pobrać hello rozszerzenia dla programu Chrome i krawędzi, z poniższe linki bezpośrednie hello:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu krawędzi](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak tooconfigure federacyjne logowanie jednokrotne dla galerii aplikacji usługi Azure AD

Wszystkie aplikacji w galerii Azure AD hello włączone możliwości przedsiębiorstwa rejestracji jednokrotnej ma dostępne samouczek krok po kroku. Dostęp można uzyskać hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji hello galerii Azure AD](#add-an-application)

-   [Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Pobieranie metadanych usługi Azure AD i certyfikatów](#download-the-azure-ad-metadata-or-certificate)

-   [Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Przypisywanie użytkowników toohello aplikacji](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Dodawanie aplikacji hello galerii Azure AD

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku

6.  W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.

7.  Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.

8.  Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.

9.  Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Konfigurowanie rejestracji jednokrotnej dla aplikacji hello galerii Azure AD

tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Wybierz **na języku SAML logowania jednokrotnego** z hello **tryb** listy rozwijanej.

9.  Wprowadź wartości hello wymagane w **domeny i adres URL.** Te wartości należy uzyskać od dostawcy aplikacji hello.

   1. Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello logowania na adres URL jest wymagana wartość. Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.

   2. Aplikacja hello tooconfigure jako zainicjował IdP SSO hello adres URL odpowiedzi jest wymagana wartość. Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.

10. **Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz toosee hello — wymagane wartości.

11. W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.

12. **Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.

   tooadd atrybutu:

   1. Kliknij przycisk **Dodaj atrybut**. Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.

   2. Kliknij przycisk **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

13. Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello. Ponadto ma hello metadane z adresów URL i certyfikatu wymaganego toosetup rejestracji Jednokrotnej z aplikacji hello.

14. Kliknij przycisk **zapisać** toosave hello konfiguracji.

15. Przypisywanie użytkowników toohello aplikacji.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika

tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello ma tooshow tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej. Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.

    >[!NOTE]
    >Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format. Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.
    >
    >

9.  atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.

   tooadd atrybutu:

   1. Kliknij przycisk **Dodaj atrybut**. Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.

   2. Kliknij przycisk **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Pobieranie metadanych usługi Azure AD hello lub certyfikat

metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie. W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.

    Usługi Azure AD nie udostępnia metadane hello tooget adresu URL. można pobrać metadanych Hello jako plik XML.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii

tooconfigure aplikacji z systemem innym niż galerii, potrzebujesz toohave usługi Azure AD premium oraz aplikacja hello obsługuje SAML 2.0. Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)](#configuring-single-sign-on)

-   [Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Pobieranie metadanych usługi Azure AD i certyfikatów](#download-the-azure-ad-metadata-or-certificate)

-   [Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)

tooconfigure logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD hello, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku

6.  Kliknij przycisk **Non galerii aplikacji** w hello **dodać własną aplikację** sekcji

7.  Wprowadź nazwę aplikacji hello hello w hello **nazwa** pola tekstowego.

8.  Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

9.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

10. Wybierz **na języku SAML logowania jednokrotnego** w hello **tryb** listy rozwijanej

11. Wprowadź wartości hello wymagane w **domeny i adres URL.** Te wartości należy uzyskać od dostawcy aplikacji hello.

  1. Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane przez dostawców tożsamości, wprowadź hello adres URL odpowiedzi i hello identyfikator.

  2. **Opcjonalnie:** aplikacji hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello znaku w adresie URL jest wymagana wartość.

12. W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.

13. **Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.

   tooadd atrybutu:

   1. Kliknij przycisk **Dodaj atrybut**. Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.

   2. Kliknij przycisk **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

14. Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello. Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji hello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika

tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej. Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.

   >[!NOTE]
   >Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format. Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.
   >
   >

9.  atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.

   tooadd atrybutu:

   1. Kliknij przycisk **Dodaj atrybut**. Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.

   2 kliknij **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Pobieranie metadanych usługi Azure AD hello lub certyfikat

metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie. W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.

    Usługi Azure AD nie udostępnia metadane hello tooget adresu URL. można pobrać metadanych Hello jako plik XML.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji hello galerii Azure AD](#add-an-application)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Dodawanie aplikacji hello galerii Azure AD

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku

6.  W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** sekcji, nazwa typu hello aplikacji hello

7.  Wybierz hello aplikację tooconfigure dla rejestracji jednokrotnej

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

9.  Przypisywanie użytkowników toohello aplikacji.

10. Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello. W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii

tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji z systemem innym niż galerii](#add-a-non-gallery-application)

-   [Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Dodawanie aplikacji z systemem innym niż galerii

tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku

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

 * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

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

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)

