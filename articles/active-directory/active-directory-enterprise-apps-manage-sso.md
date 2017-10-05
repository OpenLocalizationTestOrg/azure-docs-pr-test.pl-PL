---
title: "Pojedynczy zarządzania logowania jednokrotnego dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać jednokrotnego na aplikacje przedsiębiorstwa za pomocą usługi Azure Active Directory"
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
ms.openlocfilehash: c975428550690254ba989935fe5110c5903e7102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klasyczna witryna Azure Portal](active-directory-sso-integrate-saas-apps.md)
> 

W tym artykule opisano sposób użycia [portalu Azure](https://portal.azure.com) do zarządzania ustawieniami pojedynczego logowania jednokrotnego dla aplikacji przedsiębiorstwa. Enterprise aplikacje to aplikacje, które są wdrożone i używane w organizacji. Ten artykuł dotyczy szczególnie aplikacje, które zostały dodane z [galerii aplikacji usługi Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-the-portal"></a>Znajdowanie aplikacji w portalu
Wszystkie aplikacje firmowe, które są skonfigurowane dla logowania jednokrotnego, można wyświetlać i zarządzać w portalu Azure. Aplikacje można znaleźć w **więcej usług** &gt; **aplikacje dla przedsiębiorstw** części portalu. 

![Blok aplikacje dla przedsiębiorstw][1]

Wybierz **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji, które zostały skonfigurowane. Wybieranie aplikacji ładuje bloku zasobów dla danej aplikacji, w którym raporty można wyświetlać dla danej aplikacji i różne ustawienia mogą być zarządzane.

Aby zarządzać ustawienia rejestracji jednokrotnej, wybierz **logowanie jednokrotne**.

![Bloku zasobów aplikacji][2]

## <a name="single-sign-on-modes"></a>Tryby rejestracji jednokrotnej
**Logowanie jednokrotne** bloku rozpoczyna się od **tryb** menu, dzięki czemu jeden tryb logowania jednokrotnego do skonfigurowania. Dostępne opcje to:

* **Na podstawie SAML logowania** — ta opcja jest dostępna, jeśli aplikacja obsługuje pełne federacyjnego logowania jednokrotnego w usłudze Azure Active Directory przy użyciu protokołu SAML 2.0.
* **Na podstawie hasła logowania** — ta opcja jest dostępna, jeśli usługi Azure AD obsługuje formularz hasła wypełnianie dla tej aplikacji.
* **Połączony na znak** — wcześniej znana jako "Istniejące rejestracji jednokrotnej", ta opcja umożliwia administratorom umieść link do tej aplikacji w ich użytkownik uruchamiający aplikację Panel dostępu usługi Azure AD lub usługi Office 365.

Aby uzyskać więcej informacji na temat trybów, zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Na podstawie SAML logowania jednokrotnego
**Na języku SAML logowania** opcja powoduje wyświetlenie bloku, który jest podzielony na cztery sekcje:

### <a name="domains-and-urls"></a>Domenach i adresach URL
Jest to, gdzie wszystkie szczegółowe informacje o domenie i adresy URL aplikacji są dodawane do katalogu usługi Azure AD. Są wyświetlane wszystkie dane wejściowe wymagane do przygotowania aplikacji do pracy rejestracji jednokrotnej bezpośrednio na ekranie, dlatego wszystkie dane wejściowe Opcjonalnie można wyświetlić, wybierając **Pokaż zaawansowane ustawienia adresu URL** wyboru. Zawiera pełną listę obsługiwanych dane wejściowe:

* **Zaloguj się na adres URL** — gdy użytkownik przechodzi do logowania się w tej aplikacji. Jeśli aplikacja jest skonfigurowana do wykonania na, a następnie, gdy użytkownik przechodzi do tego adresu URL usługi zainicjował dostawcy funkcji logowania jednokrotnego, dostawca usług nie niezbędne przekierowanie do usługi Azure AD do uwierzytelniania i zalogować użytkownika. Jeśli to pole zostanie wypełnione, usługi Azure AD będzie używać tego adresu URL do uruchamiania aplikacji z usługi Office 365 i panelu dostępu usługi Azure AD. Jeśli to pole zostanie pominięte, a następnie usługi Azure AD wykonuje zamiast tego dostawcy tożsamości-inicjowane logowania po uruchomieniu aplikacji z usługi Office 365, Panel dostępu usługi Azure AD lub Azure AD pojedynczy adres URL logowania.
* **Identyfikator** — ten identyfikator URI musi jednoznacznie wskazywać aplikacji, dla których jednym logowania jest skonfigurowane. Jest to wartość, która wysyła usługi Azure AD z powrotem do aplikacji jako parametr odbiorców tokenu SAML i aplikacji powinien go zweryfikować. Ta wartość jest także wyświetlany jako identyfikator obiektu w dowolnym metadanych SAML udostępniany przez aplikację.
* **Adres URL odpowiedzi** — adres URL odpowiedzi jest, gdy aplikacja oczekuje odebrać tokenu SAML. Jest to także określane jako adres URL usługi konsumenta potwierdzenia (ACS). Po te zostały wprowadzone, kliknij przycisk Dalej, aby przejść do następnego ekranu. Ten ekran informuje o co musi zostać skonfigurowane na stronie aplikacji do akceptowania tokenu SAML z usługi Azure AD.
* **Stan przekazywania** — stan przekazywania jest opcjonalnym parametrem, który może pomóc informujące aplikacji, gdzie przekieruje użytkownika, po zakończeniu uwierzytelniania. Zwykle jest to wartość prawidłowy adres URL w aplikacji, jednak niektóre aplikacje używają tego pola inaczej (zobacz aplikacji rejestracji jednokrotnej w dokumentacji, aby uzyskać szczegółowe informacje). Aby ustawić stan przekazywania jest nowa funkcja, która jest unikatowa dla nowego portalu Azure.

### <a name="user-attributes"></a>Atrybuty użytkownika
Jest to, gdzie Administratorzy można wyświetlać i edytować atrybuty, które zostały wysłane w tokenie SAML, który usługi Azure AD wystawia aplikacji każdego logowania użytkownika.

Atrybut tylko edytowalny, obsługiwane jest **identyfikator użytkownika** atrybutu. Wartość tego atrybutu jest polem w usłudze Azure AD, który unikatowo identyfikuje każdego użytkownika w aplikacji. Na przykład jeśli aplikacja została wdrożona przy użyciu "Adres E-mail" jako nazwy użytkownika i unikatowym identyfikatorem, następnie będzie można ustawić wartości do pola "user.mail" w usłudze Azure AD.

### <a name="saml-signing-certificate"></a>Certyfikat podpisywania SAML
W tej sekcji przedstawiono szczegóły certyfikatu, który używa usługi Azure AD do podpisywania tokeny SAML, które są wysyłane do aplikacji, w każdym razem, użytkownik jest uwierzytelniany. Umożliwia on właściwości bieżącego certyfikatu, aby sprawdził, łącznie z datą wygaśnięcia.

### <a name="application-configuration"></a>Konfiguracja aplikacji
Ostatnia zawiera dokumentacja i/lub kontrolki, należy skonfigurować aplikację do użycia usługi Azure Active Directory jako dostawcy tożsamości.

**Konfiguruj aplikację** menu wysuwanego udostępnia nowe zwięzła, osadzone instrukcje dotyczące konfigurowania aplikacji. Jest to kolejną nową funkcją unikatowe dla nowego portalu Azure.

> [!NOTE]
> Pełny przykład osadzonych dokumentacji Zobacz aplikacji witryny Salesforce.com. Dodatkowe aplikacje w dokumentacji jest stale dodawane.
> 
> 

![Osadzony dokumentów][3]

## <a name="password-based-sign-on"></a>Na podstawie hasła logowania
Jeśli jest obsługiwany dla aplikacji, wybierając tryb logowania jednokrotnego opartego na hasłach i wybierając **zapisać** natychmiast konfiguruje wykonania opartego na hasłach logowania jednokrotnego. Aby uzyskać więcej informacji na temat wdrażania opartego na hasłach logowania jednokrotnego, zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Na podstawie hasła logowania][4]

## <a name="linked-sign-on"></a>Połączonego logowania
Jeśli obsługiwane w przypadku aplikacji, wybierając tryb połączonego logowania jednokrotnego pozwala na wprowadź adres URL, który ma być Panel dostępu usługi Azure AD lub usługi Office 365 przekierowania po kliknięciu tej aplikacji. Aby uzyskać więcej informacji na temat połączonego logowania jednokrotnego (wcześniej znane jako "istniejące SSO"), zobacz [jak logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Połączonego logowania jednokrotnego][5]

##<a name="feedback"></a>Opinia

Mamy nadzieję przy użyciu udoskonalone środowisko usługi Azure AD. Pamiętaj o opinie przesyłanych! Opinie i pomysły dotyczące poprawy **portalu administracyjnego** sekcji naszych [forum opinii](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Firma Microsoft jest podekscytowani, informacje o kompilowaniu chłodnych nowości codziennie i użyj wskazówek z kształtem i zdefiniować, co mamy utworzyć w następnej kolejności.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
