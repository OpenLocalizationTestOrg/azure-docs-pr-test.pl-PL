---
title: "aaaError na stronie aplikacji po zalogowaniu się | Dokumentacja firmy Microsoft"
description: "Jak tooresolve problemy z usługą Azure AD Zaloguj się, gdy sama aplikacja hello emituje błąd"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Błąd na stronie aplikacji po zalogowaniu

W tym scenariuszu usługi Azure AD podpisała hello użytkownika w, ale aplikacja hello jest wyświetlany błąd nie zezwala hello toosuccessfully Zakończ hello podczas rejestracji w przepływie. W tym scenariuszu aplikacja hello nie akceptuje hello problem odpowiedzi przez usługę Azure AD.

Istnieje kilka możliwych przyczyn Dlaczego aplikacji hello zaakceptował hello odpowiedzi z usługi Azure AD. Jeśli błąd hello w aplikacji hello nie jest wystarczająco wyczyść tooknow co Brak odpowiedzi hello następnie:

-   Jeśli aplikacja hello jest galerii hello Azure AD, sprawdź zostały wykonane wszystkie kroki hello w artykule hello [jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Użyj narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) toocapture SAML żądania, odpowiedzi SAML i tokenu SAML.

-   Udostępnij odpowiedzi SAML hello tooknow dostawcy aplikacji hello brakujących.

## <a name="missing-attributes-in-hello-saml-response"></a>Brak atrybutów w hello odpowiedzi SAML

tooadd atrybutu w toobe konfiguracji usługi Azure AD hello wysyłany w odpowiedzi hello Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk **wyświetlanie i edytowanie użytkownika wszystkie inne atrybuty w obszarze** hello **atrybuty użytkownika** hello tooedit sekcji atrybutów aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.

   tooadd atrybutu:

   * Kliknij przycisk **Dodaj atrybut**. Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.

   * Kliknij przycisk **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

9.  Zapisz konfigurację hello.

Następnym zalogowaniu użytkownika hello toohello aplikacji, usługi Azure AD Wyślij nowy atrybut hello w hello odpowiedzi SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>Aplikacja Hello oczekuje na format lub inną wartość identyfikatora użytkownika

Witaj toohello logowania aplikacji kończy się niepowodzeniem ponieważ hello odpowiedzi SAML nie ma atrybutów, takich jak role lub aplikacji hello oczekuje inny format hello EntityID atrybutu.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Dodaj atrybut w konfiguracji aplikacji hello Azure AD:

hello toochange wartość identyfikatora użytkownika, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  W obszarze hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.

## <a name="change-entityid-user-identifier-format"></a>Zmiana formatu EntityID (identyfikator użytkownika)

Jeśli aplikacja hello oczekuje innego formatu hello EntityID atrybutu. Następnie będzie format EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.

Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format. Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>Aplikacja Hello oczekuje inny podpis metody hello odpowiedzi SAML

toochange, które części tokenu SAML hello są podpisane cyfrowo przez usługę Azure Active Directory. Wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze hello **certyfikat podpisywania SAML** sekcji.

9.  Wybierz odpowiednie hello **opcja podpisywania** oczekiwany przez aplikacji hello:

  * Odpowiedzi SAML logowania

  * Podpisywanie odpowiedzi SAML i potwierdzenia

  * Potwierdzenia języka SAML logowania

Następnym zalogowaniu użytkownika hello toohello aplikacji, rejestrowania usługi Azure AD hello część odpowiedzi SAML hello wybrane.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>Aplikacja Hello oczekuje hello podpisywania toobe algorytmu SHA-1

Domyślnie program Azure AD podpisuje token SAML hello przy użyciu hello większości algorytmu zabezpieczeń. Zmiana algorytmu znak hello tooSHA-1 nie jest zalecane, chyba że wymagane przez aplikację hello.

toochange hello algorytm podpisywania, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze hello **certyfikat podpisywania SAML** sekcji.

9.  Wybierz algorytm SHA-1, hello **algorytm podpisywania**.

Loguje użytkownika toohello aplikacji hello następnym, rejestrowania usługi Azure AD hello tokenu SAML przy użyciu algorytmu SHA-1.

## <a name="next-steps"></a>Następne kroki
[Jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
