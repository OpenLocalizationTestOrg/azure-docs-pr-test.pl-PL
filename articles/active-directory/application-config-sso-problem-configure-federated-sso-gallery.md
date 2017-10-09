---
title: aaaProblem Konfigurowanie federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft
description: "Niektóre hello typowe problemy mogą wystąpić podczas konfigurowania federacyjnych pojedynczy adres logowania jednokrotnego dla aplikacji, które są wymienione w hello galerii aplikacji usługi Azure AD za pomocą protokołu SAML"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD

Jeśli napotkasz problem podczas konfigurowania aplikacji. Sprawdź, czy zostały wykonane wszystkie kroki hello w samouczku hello aplikacji hello. W konfiguracji aplikacji hello masz dokumentacji wbudowany w sposób tooconfigure hello aplikacji. Ponadto można uzyskać dostęp hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.

## <a name="cant-add-another-instance-of-hello-application"></a>Nie można dodać inne wystąpienie aplikacji hello

tooadd drugiego wystąpienia aplikacji, należy toobe stanie:

-   Skonfiguruj Unikatowy identyfikator hello drugie wystąpienie. Nie można tego samego identyfikatora używane dla pierwszego wystąpienia hello powitalne tooconfigure stanie.

-   Skonfiguruj inny certyfikat niż hello używane jako hello pierwszego wystąpienia.

Jeśli hello aplikacji nie obsługuje żadnego z hello powyżej. Następnie nie będzie możliwe tooconfigure drugiego wystąpienia.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Nie można dodać hello identyfikator lub hello adres URL odpowiedzi

Jeśli nie jest możliwe tooconfigure hello identyfikator lub hello adres URL odpowiedzi, potwierdź hello identyfikator i wartości adresu URL odpowiedzi są takie same wzorce hello wstępnie skonfigurowane dla aplikacji hello.

wzorce hello tooknow wstępnie skonfigurowane dla aplikacji hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.** Przejdź toostep 7. Jeśli jesteś już w bloku konfiguracji aplikacji hello w usłudze Azure AD.

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Wybierz **na języku SAML logowania jednokrotnego** z hello **tryb** listy rozwijanej.

9.  Przejdź toohello **identyfikator** lub **adres URL odpowiedzi** pole tekstowe, w obszarze hello **sekcji domeny i adres URL.**

10. Istnieją trzy sposoby tooknow hello obsługiwane wzorce dla aplikacji hello:

   * W polu tekstowym hello, zobacz wzorcem hello obsługiwane jako symbol zastępczy *przykład:* <https://contoso.com>.

   * Jeśli wzorzec hello nie jest obsługiwana, podczas próby tooenter hello wartość w polu tekstowym hello zostanie wyświetlony czerwony wykrzyknik. Umieść kursor nad hello czerwony wykrzyknik, zobaczysz hello obsługiwane wzorce.

   * W samouczku hello aplikacji hello można także uzyskać informacje o wzorce hello obsługiwane. W obszarze hello **Konfigurowanie usługi Azure AD rejestracji jednokrotnej** sekcji. Przejdź toohello krok w przypadku wartości skonfigurowanych hello hello **domeny i adres URL** sekcji.

Jeśli hello wartości nie są zgodne z wzorców hello wstępnie skonfigurowane w usłudze Azure AD. Możesz:

-   Praca z hello aplikacji dostawcy tooget wartości, które jest zgodny z wzorcem hello wstępnie skonfigurowane w usłudze Azure AD

-   Można skontaktować się zespół usługi Azure AD < aadapprequest@microsoft.com > lub zostaw komentarz w aktualizacji hello samouczek toorequest hello hello obsługiwane wzorce dla aplikacji hello

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Gdzie ustawić hello format EntityID (identyfikator użytkownika)

Możesz nie być w formacie EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.

Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format. Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sekcji hello NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Nie można znaleźć konfiguracji metadanych usługi Azure AD hello hello toocomplete z aplikacji hello

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

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Nie wiadomo, jak toocustomize SAML oświadczenia wysyłane tooan aplikacji

toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
