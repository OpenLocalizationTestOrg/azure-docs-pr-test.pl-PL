---
title: "aaaSingle zarządzania logowania jednokrotnego dla aplikacji przedsiębiorstwa w hello Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage logowania jednokrotnego dla aplikacji przedsiębiorstwa przy użyciu hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klasyczna witryna Azure Portal](active-directory-sso-integrate-saas-apps.md)
> 

W tym artykule opisano sposób toouse hello [portalu Azure](https://portal.azure.com) toomanage jednego ustawienia rejestracji aplikacji dla przedsiębiorstw. Enterprise aplikacje to aplikacje, które są wdrożone i używane w organizacji. Ten artykuł dotyczy szczególnie tooapps dodanych z hello [galerii aplikacji usługi Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Znajdowanie aplikacji w portalu hello
Wszystkie aplikacje firmowe, które są skonfigurowane dla logowania jednokrotnego, można wyświetlać i zarządzane w hello portalu Azure. aplikacji Hello znajdują się w hello **więcej usług** &gt; **aplikacje dla przedsiębiorstw** sekcji hello portalu. 

![Blok aplikacje dla przedsiębiorstw][1]

Wybierz **wszystkie aplikacje** tooview listę wszystkich aplikacji, które zostały skonfigurowane. Wybieranie aplikacji ładuje hello bloku zasobów dla danej aplikacji, w którym raporty można wyświetlać dla danej aplikacji i różne ustawienia mogą być zarządzane.

Wybierz toomanage jednego ustawienia rejestracji, **logowanie jednokrotne**.

![Bloku zasobów aplikacji][2]

## <a name="single-sign-on-modes"></a>Tryby rejestracji jednokrotnej
Witaj **logowanie jednokrotne** bloku rozpoczyna się od **tryb** menu, dzięki czemu toobe tryb rejestracji jednokrotnej hello skonfigurowane. Witaj dostępne opcje to:

* **Na podstawie SAML logowania** — ta opcja jest dostępna, jeśli aplikacja hello obsługuje pełne federacyjne logowanie jednokrotne z usługą Azure Active Directory przy użyciu protokołu SAML 2.0 hello.
* **Na podstawie hasła logowania** — ta opcja jest dostępna, jeśli usługi Azure AD obsługuje formularz hasła wypełnianie dla tej aplikacji.
* **Połączony na znak** — wcześniej znana jako "Istniejące rejestracji jednokrotnej", ta opcja umożliwia administratorom tooplace aplikacją toothis łącze w ich użytkownik uruchamiający aplikację Panel dostępu usługi Azure AD lub usługi Office 365.

Aby uzyskać więcej informacji na temat trybów, zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Na podstawie SAML logowania jednokrotnego
Witaj **na języku SAML logowania** opcja powoduje wyświetlenie bloku, który jest podzielony na cztery sekcje:

### <a name="domains-and-urls"></a>Domenach i adresach URL
Jest to, gdzie wszystkie szczegółowe informacje dotyczące domeny i adresy URL aplikacji hello są dodawane tooyour katalog usługi Azure AD. Wszystkie dane wejściowe wymagane toomake pracy rejestracji jednokrotnej aplikacji są wyświetlane bezpośrednio na ekranie powitania, podczas gdy wszystkie dane wejściowe opcjonalne można wyświetlić, wybierając hello **Pokaż zaawansowane ustawienia adresu URL** wyboru. zawiera pełną listę obsługiwanych wejść Hello:

* **Zaloguj się na adres URL** — w przypadku, gdy użytkownik hello przechodzi toothis toosign w aplikacji. Jeśli aplikacja hello jest logowania jednym inicjowanych przez dostawcę usługi skonfigurowanego tooperform gdy użytkownik nawiguje toothis adres URL, dostawca usług hello hello niezbędne przekierowanie tooAzure AD tooauthenticate i zaloguj hello użytkownika w. Jeśli to pole zostanie wypełnione, usługi Azure AD będą używać tej aplikacji hello toolaunch adres URL z usługi Office 365 i hello Panel dostępu usługi Azure AD. Jeśli to pole zostanie pominięte, a następnie usługi Azure AD wykonuje zamiast tego dostawcy tożsamości-jednokrotnego inicjowane logowania po hello aplikacja jest uruchamiana z usługi Office 365, hello Panel dostępu usługi Azure AD lub hello Azure AD pojedynczego adresu URL.
* **Identyfikator** — ten identyfikator URI musi jednoznacznie wskazywać aplikacji hello, dla których jednym logowania jest skonfigurowane. Jest to wartość hello Azure AD wysyła wstecz tooapplication jako parametr odbiorców tokenu SAML hello Witaj, czy aplikacja hello jest oczekiwany toovalidate go. Ta wartość jest również wyświetlany jako hello identyfikator jednostki w dowolnym metadanych SAML podał aplikacji hello.
* **Adres URL odpowiedzi** — adres URL odpowiedzi hello jest, gdzie aplikacja hello oczekuje tokenu SAML hello tooreceive. Dotyczy to również adres URL usługi konsumenta potwierdzenia (ACS) hello tooas określonego. Po te zostały wprowadzone, kliknij przycisk Dalej tooproceed toohello następnego ekranu. Ten ekran informuje o jakie toobe potrzeb skonfigurowane na powitania aplikacji po stronie tooenable tooaccept tokenu SAML z usługi Azure AD.
* **Stan przekazywania** — stan przekazywania hello jest opcjonalnym parametrem, który może pomóc sprawdzić aplikacji hello, gdzie tooredirect hello użytkownika, po zakończeniu uwierzytelniania. Zwykle wartość hello jest prawidłowy adres URL w aplikacji hello, jednak niektóre aplikacje używają tego pola inaczej (zobacz aplikacji hello rejestracji jednokrotnej w dokumentacji, aby uzyskać szczegółowe informacje). stan przekazywania hello tooset możliwości Hello jest nowa funkcja, która jest unikatowa toohello nowego portalu Azure.

### <a name="user-attributes"></a>Atrybuty użytkownika
Jest to, gdzie administratorzy mogą wyświetlać i edytować hello atrybuty, które są wysyłane w tokenie SAML hello, czy usługa Azure AD wystawia aplikacji toohello poszczególnych użytkowników, zaloguj się na.

Witaj tylko atrybut możliwości edycji obsługiwane jest hello **identyfikator użytkownika** atrybutu. wartość tego atrybutu Hello jest polem hello w usłudze Azure AD, który unikatowo identyfikuje każdego użytkownika w aplikacji hello. Na przykład jeśli aplikacja hello została wdrożona przy użyciu hello "Adres E-mail" jako nazwy użytkownika hello i unikatowym identyfikatorem, następnie hello będzie można ustawić wartości pola "user.mail" toohello w usłudze Azure AD.

### <a name="saml-signing-certificate"></a>Certyfikat podpisywania SAML
W tej sekcji przedstawiono szczegóły hello certyfikatu hello używany tokeny SAML hello toosign wystawiane toohello aplikacji, który uwierzytelnia każdego użytkownika w czasie hello w usłudze Azure AD. Umożliwia on właściwości hello hello bieżącego certyfikatu toobe inspekcji, w tym datę wygaśnięcia hello.

### <a name="application-configuration"></a>Konfiguracja aplikacji
Hello końcowego sekcja zawiera hello dokumentacji i/lub formanty wymagane tooconfigure hello samej aplikacji toouse usługi Azure Active Directory jako dostawcy tożsamości.

Witaj **Konfiguruj aplikację** menu wysuwanego udostępnia nowe zwięzła, osadzone instrukcje dotyczące konfigurowania aplikacji hello. Jest to inny nowych funkcji unikatowy toohello nowego portalu Azure.

> [!NOTE]
> Pełny przykład osadzonych dokumentacji Zobacz hello aplikacji witryny Salesforce.com. Dodatkowe aplikacje w dokumentacji jest stale dodawane.
> 
> 

![Osadzony dokumentów][3]

## <a name="password-based-sign-on"></a>Na podstawie hasła logowania
Jeśli są obsługiwane w przypadku aplikacji hello, wybierając hello opartego na hasłach tryb logowania jednokrotnego i wybierając **zapisać** natychmiast konfiguruje ją toodo opartego na hasłach logowania jednokrotnego. Aby uzyskać więcej informacji na temat wdrażania opartego na hasłach logowania jednokrotnego, zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Na podstawie hasła logowania][4]

## <a name="linked-sign-on"></a>Połączonego logowania
Jeśli obsługiwane w przypadku aplikacji hello, wybranie trybu logowania jednokrotnego hello połączone pozwala tooenter adres URL hello interesujące hello Panel dostępu usługi Azure AD lub usługi Office 365 tooredirect toowhen użytkowników, kliknij w tej aplikacji. Aby uzyskać więcej informacji na temat połączonego logowania jednokrotnego (wcześniej znane jako "istniejące SSO"), zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Połączonego logowania jednokrotnego][5]

##<a name="feedback"></a>Opinia

Mamy nadzieję, przy użyciu hello udoskonalone środowisko usługi Azure AD. Pamiętaj o opinie hello przesyłanych! Opublikuj Twoje opinie i pomysły dotyczące poprawy na powitania **portalu administracyjnego** sekcji naszych [forum opinii](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Firma Microsoft jest podekscytowani, informacje o kompilowaniu chłodnych nowości codziennie i użyj tooshape Twojego wskazówki i zdefiniować, co mamy utworzyć w następnej kolejności.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
