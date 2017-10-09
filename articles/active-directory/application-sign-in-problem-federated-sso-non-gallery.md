---
title: "podpisywania aplikacji z systemem innym niż galerii tooa skonfigurowane dla federacyjnych aaaProblems logowanie jednokrotne | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące hello określonych problemów, które mogą się spodziewać przy logowaniu się w aplikacji tooan skonfigurowane na podstawie SAML federacyjne logowanie jednokrotne z usługą Azure AD"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a>Problemy z zarejestrowaniem w aplikacji innej niż galerii tooa skonfigurowany dla federacyjnego logowania jednokrotnego

tootroubleshoot problemu, wymagana konfiguracja aplikacji hello tooverify w usłudze Azure AD następująco:

-   Zostały wykonane wszystkie kroki konfiguracji hello hello aplikacji galerii Azure AD.

-   Witaj identyfikator i adres URL odpowiedzi, skonfigurowane w usłudze AAD zgodne one oczekiwanych wartości w aplikacji hello

-   Użytkownicy przypisano toohello aplikacji

## <a name="application-not-found-in-directory"></a>Nie można odnaleźć w katalogu aplikacji

*Błąd AADSTS70001: Nie znaleziono aplikacji o identyfikatorze "https://contoso.com" w katalogu hello*.

**Możliwa przyczyna**

Witaj wystawca atrybutu wysyła z tooAzure aplikacji hello AD w żądaniu SAML hello jest niezgodny hello identyfikator wartości ustawionej w aplikacji hello Azure AD.

**Rozdzielczość**

Upewnij się, ten atrybut wystawcy hello w hello SAML żądanie jest zgodne hello wartość identyfikatora skonfigurowane w usłudze Azure AD:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  <span id="_Hlk477190042" class="anchor"></span>Przejdź za**domeny i adres URL** sekcji. Sprawdź, czy hello w hello identyfikator hello wartość hello identyfikator wyświetlany omyłkowo hello jest zgodne z pola tekstowego.

Po wartości identyfikatora hello zostały zaktualizowane w usłudze Azure AD i jej pasującego hello wartości wysyła aplikacja hello w żądaniu SAML hello, powinno być możliwe toosign w toohello aplikacji.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>adres zwrotny Hello jest niezgodna z adresów odpowiedzi hello skonfigurowanych dla aplikacji hello. 

*Błąd AADSTS50011: hello odpowiedzi adres "https://contoso.com" jest niezgodny adresy odpowiedzi hello skonfigurowane dla aplikacji hello* 

**Możliwa przyczyna** 

wartość adresu URL odpowiedzi hello lub wzorca skonfigurowane w usłudze Azure AD Hello AssertionConsumerServiceURL wartość w żądaniu SAML hello nie jest zgodny. Witaj AssertionConsumerServiceURL wartość w żądaniu SAML hello jest hello adresu URL, zobacz błąd hello. 

**Rozdzielczość** 

Upewnij się, ta wartość AssertionConsumerServiceURL hello w żądaniu SAML hello jego pasującego hello wartość adresu URL odpowiedzi skonfigurowane w usłudze Azure AD. 
 
1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.** 

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello. 

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu. 

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory. 

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji. 

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**
  
6.  Wybierz hello aplikację tooconfigure rejestracji jednokrotnej

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Przejdź za**domeny i adres URL** sekcji. Sprawdź lub zaktualizować wartości hello hello adres URL odpowiedzi pole tekstowe toomatch hello AssertionConsumerServiceURL wartość w żądaniu SAML hello.

  * Jeśli nie widzisz pole tekstowe adresu URL odpowiedzi hello wybierz hello **Pokaż zaawansowane ustawienia adresu URL** wyboru. 

Po zaktualizowaniu wartość adresu URL odpowiedzi hello w usłudze Azure AD i ma dopasowania wartości hello wysyła aplikacja hello w hello żądanie SAML, powinno być możliwe toosign w toohello aplikacji.

## <a name="user-not-assigned-a-role"></a>Nie przypisaną rolę użytkownika

*Błąd AADSTS50105: hello zalogowany użytkownik "brian@contoso.com" nie jest przypisana rola tooa dla aplikacji hello*

**Możliwa przyczyna**

Hello użytkownikowi nie udzielono dostępu toohello aplikacji w usłudze Azure AD.

**Rozdzielczość**

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

Po krótkim czasie użytkownicy hello, wybranych będą mogli toolaunch te aplikacje przy użyciu hello metod opisanych w sekcji Opis rozwiązania hello.

## <a name="not-a-valid-saml-request"></a>Nie prawidłowy SAML żądanie

*Błąd AADSTS75005: hello żądanie nie jest prawidłowy komunikat protokołu Saml2.*

**Możliwa przyczyna**

Usługi Azure AD nie obsługuje hello SAML żądania wysyłane przez aplikację powitania dla logowania jednokrotnego. Dostępne są następujące typowe problemy:

-   Brak wymaganego pola w żądaniu SAML hello

-   Metoda żądania zakodowane SAML

**Rozdzielczość**

1.  Przechwycenie żądania SAML. Postępuj zgodnie z samouczkiem hello [jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn jak toocapture hello SAML żądania.

2.  Skontaktuj się z dostawcą aplikacji hello i udziału:

    -   Żądanie SAML

    -   [Wymagania dotyczące protokołu usługi AD pojedynczego logowania jednokrotnego SAML Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Należy sprawdzić poprawność obsługują hello Azure AD SAML implementacji dla logowania jednokrotnego.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Żaden z zasobów na liście requiredResourceAccess

*Błąd AADSTS65005: aplikacja kliencka hello zażądał tooresource dostępu "00000002-0000-0000-c000-000000000000'. To żądanie nie powiodło się, ponieważ powitania klienta nie określono tego zasobu na swojej liście requiredResourceAccess*.

**Możliwa przyczyna**

obiekt aplikacji Hello jest uszkodzony.

**Rozdzielczość**

toosolve hello problem, Usuń hello aplikacji z katalogu hello. Następnie należy dodać i skonfigurować aplikacji hello, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Kliknij przycisk **usunąć** w lewym górnym hello aplikacji hello **omówienie** bloku.

8.  Odśwież usługi Azure AD i dodawanie aplikacji hello z galerii Azure AD hello. Skonfiguruj ponownie aplikacji hello.

Po ponownej konfiguracji aplikacji hello, powinno być możliwe toosign w toohello aplikacji.

## <a name="certificate-or-key-not-configured"></a>Certyfikat lub klucz nie jest skonfigurowany

Błąd AADSTS50003: Nie klucza podpisywania skonfigurowane.

**Możliwa przyczyna**

obiekt aplikacji Hello jest uszkodzony i usługi Azure AD nie rozpoznaje certyfikatu hello skonfigurowanego dla aplikacji hello.

**Rozdzielczość**

toodelete i utworzyć nowy certyfikat, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk **Utwórz nowy certyfikat** w obszarze hello **SAML certyfikatu podpisywania** sekcji.

9.  Wybierz datę wygaśnięcia. Następnie kliknij przycisk **zapisać.**

10. Sprawdź **uaktywnić nowego świadectwa** toooverride hello active certyfikatu. Następnie kliknij przycisk **zapisać** u góry bloku hello hello i zaakceptować certyfikat przerzucania hello tooactivate.

11. W obszarze hello **certyfikat podpisywania SAML** , kliknij przycisk **Usuń** tooremove hello **nieużywane** certyfikatu.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problem w przypadku dostosowywania hello SAML oświadczenia wysyłane tooan aplikacji

toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
[Wymagania dotyczące protokołu usługi AD pojedynczego logowania jednokrotnego SAML Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
