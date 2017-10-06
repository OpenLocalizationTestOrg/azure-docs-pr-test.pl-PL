---
title: aaaHow toodetermine jakie jednokrotnego toouse metody | Dokumentacja firmy Microsoft
description: "Zrozumienie hello pojedynczego logowania jednokrotnego trybów obsługiwanych przez usługę Azure AD i jak toopick aplikacji hello które jeden toochoose dla osób zainteresowanych."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Jak toodetermine jakie jednokrotnego toouse — metoda

W tym artykule pomocy toounderstand hello pojedynczego logowania jednokrotnego trybów obsługiwanych przez usługę Azure AD i jak toopick aplikacji hello które jeden toochoose dla osób zainteresowanych.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Logowanie jednokrotne i Inicjowanie obsługi trybów obsługiwanych przez typy określonych aplikacji

w poniższej tabeli Hello opisano hello różnych rejestracji jednokrotnej i Inicjowanie obsługi trybów obsługiwanych przez każdą hello powyżej typów aplikacji. Korzystając z tej tabeli toohelp toounderstand aplikacji, które należy toosupport tooadd określonego celu.

  ![Tabela typów region](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Jak toochoose tryb pojedynczy logowania jednokrotnego

Witaj obsługiwane **logowanie jednokrotne** tryby aplikacji usługi Azure AD są wymienione poniżej.

-   **Azure AD rejestracji jednokrotnej wyłączone** — Wybieranie usługi Azure AD rejestracji jednokrotnej wyłączone **tryb rejestracji jednokrotnej** Jeśli nie jest jeszcze gotowy toointegrate tę aplikację przy rejestracji jednokrotnej z usługą Azure AD, lub po prostu testowania go

-   **Połączone logowania jednokrotnego** — wybierz hello [połączonej logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli masz aplikację, która jest już połączona z istniejącym pojedynczego logowania jednokrotnego rozwiązaniem lub jeśli chcesz toopublish prosty łączy dla użytkowników w ich [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lub [uruchamiający aplikację usługi Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Na podstawie hasła logowania jednokrotnego** — wybierz hello [opartego na hasłach logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli aplikacja renderuje nazwy użytkownika i hasła pola HTML i ma toostore który Nazwa użytkownika i hasło bezpiecznie toobe odtwarzany toohello aplikację później

-   **Na podstawie SAML logowania jednokrotnego** — wybierz hello [na języku SAML logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) na podstawie ról aplikacji toospecific jednokrotnego tryb, jeśli aplikacja obsługuje protokoły SAML lub OpenID Connect hello lub użytkownicy mogli toomap toobe reguły zdefiniowane w Twojej SAML oświadczeń *(**Uwaga:** ta opcja nie jest dostępne, gdy serwer proxy aplikacji hello jest skonfigurowany dla aplikacji) *

-   **Na podstawie nagłówka logowania jednokrotnego** — wybierz tę opcję, [na podstawie nagłówka logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) logowania jednokrotnego w tryb jednego Jeśli masz aplikację przy użyciu PingAccess, która obsługuje nagłówka HTTP na podstawie uwierzytelniania, która ma jednokrotnego tooperform na zbyt *(**Uwaga:** ta opcja jest dostępna tylko, gdy serwer proxy aplikacji hello i PingAccess jest skonfigurowana dla aplikacji) *

-   **Zintegrowane uwierzytelnianie systemu Windows** — wybierz hello [zintegrowane uwierzytelnianie systemu Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) jednokrotnego tryb podczas udostępnianie aplikacji WIA lokalnej, która ma jednokrotnego tooperform na zbyt*()*  *Uwaga:** ta opcja jest dostępna tylko wtedy, gdy serwer proxy aplikacji hello jest skonfigurowany dla aplikacji) *

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Tryby pojedynczego logowania jednokrotnego dla aplikacji utworzonych niestandardowych

Aplikacje mają niestandardowe opracowane przez hello [opracowany niestandardowych aplikacji](#_Custom-Developed_Applications) środowisko obsługuje również dodatkowe pojedynczego logowania jednokrotnego tryby nie są wymienione powyżej. Należą do nich:

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) logowania na podstawie

-   [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) logowania na podstawie

-   [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) logowania na podstawie

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) logowania na podstawie

Witaj odczytu [przewodnik dewelopera usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn więcej informacji na temat jak toocreate opracowany niestandardowych aplikacji, która obsługuje te pojedynczy tryby logowania jednokrotnego.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Jak tooset aplikacji na jednym trybie logowania jednokrotnego

tooset aplikacji **logowanie jednokrotne** tryb, wykonaj poniższe instrukcje hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz hello aplikację tooconfigure rejestracji jednokrotnej

7.  Po załadowaniu aplikacji hello, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)

