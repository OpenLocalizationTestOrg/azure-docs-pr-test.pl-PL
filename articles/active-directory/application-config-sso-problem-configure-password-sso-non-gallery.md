---
title: "Konfigurowanie hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello typowych problemów osób krój, podczas konfigurowania haseł logowanie jednokrotne dla aplikacji z systemem innym niż galerii niestandardowych, które nie są wymienione w hello galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii

W tym artykule pomóc toounderstand hello typowych problemów osób krój podczas konfigurowania **hasło logowania jednokrotnego** z aplikacji innych niż galerii.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Sposób logowania toocapture pól dla aplikacji

Przechwytywanie pola logowania jest obsługiwana tylko dla komputerów z obsługą HTML strony logowania i jest **nie jest obsługiwane dla niestandardowych stron logowania**, takich jak implementacje używające Flash i inne technologie włączone HTML.

Istnieją dwa sposoby, można przechwytywać logowania pól niestandardowych aplikacji:

-   Automatyczne logowanie pola przechwytywania

-   Ręczne znaku w polu przechwytywania

**Automatyczne logowanie pola przechwytywania** działa prawidłowo w przypadku większości włączone HTML strony logowania, jeśli używają one **dobrze znane identyfikatory DIV hello nazwy użytkownika i hasła, wprowadź** pola. działa to sposób Hello jest za pomocą oskrobaniu hello HTML na powitania strony toofind identyfikatorów DIV, spełniających określone kryteria i następnie zapisywania tych metadanych dla tej aplikacji, można później odtwarzana tooit hasła.

**Przechwytywanie ręczne znaku w polu** mogą być używane w przypadku hello aplikacji hello **dostawcy nie etykietę** hello wejściowy pola używane w celu logowania się. Ręczne znaku w polu przechwytywania można również w przypadku hello podczas hello **dostawcy renderuje wielu pól** co nie może być wykrywane automatycznie. Usługi Azure AD można przechowywać dane jako wiele pól znajdują się na powitania Zaloguj się na stronie tak długo, jak możesz Napisz, których te pola są na stronie powitania.

Ogólnie rzecz biorąc **Jeśli pole automatycznego logowania przechwytywania nie działa, zawsze zalecamy w trakcie hello opcja ręcznego.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Jak tooautomatically przechwytywania pola logowania dla aplikacji

tooconfigure **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania automatycznego logowania pola**, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  Wprowadź hello **adres URL logowania**. Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu. **Upewnij się, hello logowania pola są widoczne pod adresem URL hello, musisz podać**.

10. Kliknij przycisk hello **zapisać** przycisku.

11. Po można to zrobić, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasła pole wprowadzania i umożliwić toosecurely usługi Azure AD toouse przekazuje hasła toothat aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu hello.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Jak toomanually przechwytywania pola logowania dla aplikacji

toomanually przechwytywania logowania pól, trzeba rozszerzenia przeglądarki panelu dostępu hello zainstalowany i **nie jest uruchomiona w trybie inPrivate, incognito lub prywatnej.** Rozszerzenie przeglądarki hello tooinstall, wykonaj kroki hello hello [jak tooinstall hello rozszerzenia przeglądarki panelu dostępu](#i-cannot-manually-detect-sign-in-fields-for-my-application) sekcji.

tooconfigure **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania ręczne znaku w polu**, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**

9.  Wprowadź hello **adres URL logowania**. Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu. **Upewnij się, hello logowania pola są widoczne pod adresem URL hello, musisz podać**.

10. Kliknij przycisk hello **zapisać** przycisku.

11. Po można to zrobić, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasła pole wprowadzania i umożliwić toosecurely usługi Azure AD toouse przekazuje hasła toothat aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu hello. W przypadku hello, że to się nie powiedzie, może **zmienić hello logowania w trybie toouse ręczne znaku w polu przechwytywania** kontynuując toostep 12.

12. Kliknij przycisk **Konfiguruj &lt;appname&gt; ustawienia jednego hasła logowania jednokrotnego**.

13. Wybierz hello **ręcznie wykryć pola logowania** opcji konfiguracji.

14. Kliknij przycisk **OK**.

15. Kliknij pozycję **Zapisz**.

16. Wykonaj hello na ekranie instrukcjami toouse hello panelu dostępu.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Wyświetlany jest komunikat Błąd "Nie można odnaleźć żadnych pól logowania pod tym adresem URL"

Zostanie wyświetlony ten błąd, gdy automatyczne wykrywanie pól logowanie nie powiodło się. Ten problem, spróbuj ręcznie znaku w polu wykrywania przez następujące hello etapami hello tooresolve [jak toomanually przechwytywania pola logowania dla aplikacji](#how-to-manually-capture-sign-in-fields-for-an-application) sekcji.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Komunikat "toosave rejestracji jednokrotnej konfiguracji"

W niektórych rzadkich przypadkach aktualizacja hello pojedynczego logowania jednokrotnego konfiguracji może zakończyć się niepowodzeniem. tooresolve to spróbuj zapisać hello pojedynczego logowania jednokrotnego ponownie konfigurację.

Jeśli ten proces jest kontynuowany toofail spójnie, otwieranie sprawy pomocy technicznej i podaj hello informacje zebrane w hello [jak toosee szczegóły hello powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak tooget pomóc, wysyłając powiadomienia szczegóły tooa inżynier pomocy technicznej](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>I nie można ręcznie wykrywania logowania w polach Moja aplikacja

Witaj zachowania, które można napotkać podczas ręcznego wykrywania nie działa, należą:

-   Proces przechwytywania ręczne Hello pojawił się toowork, ale pola hello przechwytywane nie była prawidłowa

-   Witaj prawej strony pola nie pobrać wyróżniony podczas wykonywania procesu przechwytywania hello

-   Proces przechwytywania Hello przejście strony logowania toohello aplikacji zgodnie z oczekiwaniami, ale nic się nie dzieje

-   Ręczne przechwytywania jest wyświetlany toowork, ale nie jest realizowane logowania jednokrotnego gdy Moi użytkownicy przejdą toohello aplikacji hello panelu dostępu.

Jeśli którekolwiek z tych problemów, sprawdź następujące hello:

-   Upewnij się, że masz najnowszej wersji rozszerzenia przeglądarki panelu dostępu hello hello **zainstalowane** i **włączone** wykonując kroki hello w hello [jak tooinstall hello przeglądarki panelu dostępu rozszerzenie](#how-to-install-the-access-panel-browser-extension) sekcji.

-   Upewnij się, że nie próbujesz proces przechwytywania hello podczas do przeglądarki, **incognito, przeglądanie inPrivate lub prywatnej tryb**. rozszerzenie panelu dostępu Hello nie jest obsługiwana w tych trybach.

-   Upewnij się, że użytkownicy nie próbujesz toosign w toohello aplikacji hello panelu dostępu podczas w **incognito, przeglądanie inPrivate lub prywatnej tryb**. rozszerzenie panelu dostępu Hello nie jest obsługiwana w tych trybach.

-   Spróbuj ponownie proces przechwytywania ręczne hello, zapewnienie znaczników hello red za pośrednictwem hello odpowiednich pól.

-   Jeśli proces przechwytywania ręczne hello prawdopodobnie toohang lub strona logowania hello nie niczego (przypadku 3 powyżej), spróbuj proces przechwytywania ręczne hello ponownie. Jednak to czas, po zakończeniu procesu hello, naciśnij klawisz hello **F12** przycisk tooopen konsoli dla deweloperów w przeglądarce. Raz, otwórz hello **konsoli** i typ **window.location= "&lt;wprowadź hello znaku w adresie url zostało określone podczas konfigurowania aplikacji hello&gt;"** , a następnie naciśnij klawisz  **Wprowadź**. Siła ta strona przekierowywania co zakończyć proces przechwytywania hello i przechowywać hello pola, które została przechwycona.

Jeśli z tych metod nie działają dla Ciebie, możemy pomóc. Otwieranie sprawy pomocy technicznej z hello szczegółowe informacje, które miały, a także hello informacje zebrane w hello [jak toosee szczegóły hello powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak tooget pomóc, wysyłając powiadomienia szczegóły tooa pomocy technicznej inżynier](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje (jeśli dotyczy).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu

hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:

1.  Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.

2.  Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.

3.  Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.

4.  Oparte na przeglądarce można ukierunkowanej toohello łącze. **Dodaj** hello rozszerzenia tooyour przeglądarki.

5.  Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.

6.  Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.

7.  Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji.

Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:

-   [Rozszerzenie panelu dostępu Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Rozszerzenie panelu dostępu Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Jak toosee szczegóły hello powiadomieniu portalu

Szczegóły hello powiadomienia portalu można wyświetlić, wykonując poniższe kroki hello:

1.  Kliknij przycisk hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu portalu Azure hello hello

2.  Wybierz wszystkich powiadomień w **błąd** stanu (te z toothem dalej czerwony (!)).

  >! Należy zwrócić uwagę] możesz nie kliknij powiadomienia w **Powodzenie** lub **w toku** stanu.
  >
  >

3.  Ta Otwórz hello **szczegóły powiadomienia** bloku.

4.  Dzięki tym informacjom samodzielnie toounderstand więcej szczegółowych informacji o hello problem.

5.  Jeśli nadal potrzebujesz pomocy, można również udostępniać te informacje pomocy technicznej odtwarzania lub hello grupy tooget Pomoc produktu o problemie.

6.  Kliknij hello **kopiowania** **ikona** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o z pracownikiem pomocy technicznej lub produkt grupy.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Jak tooget pomóc, wysyłając powiadomienia szczegóły tooa specjaliście pomocy technicznej

Jest bardzo ważne, aby udostępniać **hello wszystkie dane przedstawione poniżej** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie. Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku hello **ikony błędu kopiowania**, znaleziono prawej toohello hello **błąd kopiowania** pola tekstowego.

## <a name="notification-details-explained"></a>Szczegóły powiadomienia wyjaśniono

Hello poniżej opisano bardziej jakie poszczególnych elementów powiadomień hello oznacza oraz przykłady zapewnia każdego z nich.

### <a name="essential-notification-items"></a>Elementy podstawowych powiadomień

-   **Tytuł** — Witaj opisowy tytuł hello powiadomień

    -   Przykład — **ustawienia serwera proxy aplikacji**

-   **Opis elementu** — Witaj opis co nastąpiło w wyniku operacji hello

    -   Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**

-   **Identyfikator powiadomień** — Unikatowy identyfikator hello hello powiadomienia

    -   Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Identyfikator żądania klienta** — identyfikator określonego żądania hello wprowadzone przez przeglądarkę

    -   Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Czas UTC sygnatury** — Witaj znaczników czasu, w którym wystąpił hello powiadomień, w formacie UTC

    -   Przykład — **2017-03-23T19:50:43.7583681Z**

-   **Wewnętrzny identyfikator transakcji** — Witaj wewnętrzny identyfikator możemy użyć błąd hello toolook w naszych systemów

    -   Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **Nazwa UPN** — Witaj użytkownika, który wykonał operację hello

    -   Przykład —**tperkins@f128.info**

-   **Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy hello, która hello użytkownika wykonującego operację hello hello był członkiem

    -   Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Identyfikator obiektu użytkownika** — Witaj Unikatowy identyfikator hello użytkownika, który wykonał operację hello

    -   Przykład — **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementy szczegółowe powiadomienia

-   **Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy błąd hello

    -   Przykład * — **ustawienia serwera proxy aplikacji**

-   **Stan** — Witaj określonego stanu hello powiadomień

    -   Przykład * — **nie powiodło się**

-   **Obiekt o identyfikatorze** — **(może być pusta)** hello Identyfikatora obiektu, względem których hello wykonano operację

    -   Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Szczegóły** — Witaj szczegółowy opis co nastąpiło w wyniku operacji hello

    -   Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**

-   **Błąd kopiowania** — kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o inżyniera grupa pomocy technicznej lub produktu

    -   Przykład —```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)

