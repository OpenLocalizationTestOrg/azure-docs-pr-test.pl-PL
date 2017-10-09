---
title: aaaHow tooconfigure federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft
description: "Jak tooconfigure federacyjne logowanie jednokrotne dla istniejących galerii Azure AD aplikacji i używania samouczki tooget szybkie przechodzenie"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD

Wszystkie aplikacje w galerii hello Azure AD włączone możliwości przedsiębiorstwa pojedynczego logowania ma dostępne samouczek krok po kroku. Dostęp można uzyskać hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.

## <a name="overview-of-steps-required"></a>Omówienie kroków wymaganych
tooconfigure aplikację z galerii Azure AD hello należy:

-   [Dodawanie aplikacji hello galerii Azure AD](#add-an-application-from-the-azure-ad-gallery)

-   [Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Pobieranie metadanych usługi Azure AD i certyfikatów](#download-the-azure-ad-metadata-or-certificate)

-   [Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Przypisywanie użytkowników toohello aplikacji](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Dodawanie aplikacji hello galerii Azure AD

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

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Konfigurowanie rejestracji jednokrotnej dla aplikacji hello galerii Azure AD

tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **współadministrator**.

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

   1. Kliknij przycisk **zapisać.** Zostanie wyświetlony nowy atrybut hello hello tabeli.

13. Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello. Ponadto ma hello metadane z adresów URL i certyfikatu wymaganego toosetup rejestracji Jednokrotnej z aplikacji hello.

14. Kliknij przycisk **zapisać** toosave hello konfiguracji.

15. Przypisywanie użytkowników toohello aplikacji.

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika

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

   2. Kliknij pozycję **Zapisz**. Zostanie wyświetlony nowy atrybut hello hello tabeli.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Pobieranie metadanych usługi Azure AD hello lub certyfikat

metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  *  Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje**.

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie. W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.

Usługi Azure AD nie udostępnia metadane hello tooget adresu URL. można pobrać metadanych Hello jako plik XML.

## <a name="assign-users-toohello-application"></a>Przypisywanie użytkowników toohello aplikacji

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

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Dostosowywanie oświadczeń SAML hello wysyłane tooan aplikacji

toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)



