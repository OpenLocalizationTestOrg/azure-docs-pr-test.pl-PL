---
title: "Wybieranie typu aplikacji używanego podczas dodawania aplikacji | Dokumentacja firmy Microsoft"
description: "Zrozumienie obsługiwanych typów aplikacji, można zintegrować z usługą Azure AD i ich powiązane opcje konfiguracji"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a>Wybieranie typu aplikacji używanego podczas dodawania aplikacji

Ten artykuł ułatwia zrozumienie cztery typy aplikacji, którą można zintegrować z usługą Azure AD:

* Co to jest obsługiwany przez każdy z nich
* Dlaczego może wybrać aplikację
* Jak skonfigurować właściwości core tych aplikacji, takich jak użytkowników **elastycznie**, lub co **logowanie jednokrotne** technologii.

## <a name="supported-application-types-in-azure-ad"></a>Typy aplikacji obsługiwanych w usłudze Azure AD

Usługi Azure AD obsługuje cztery typy aplikacji głównej, które można dodać przy użyciu **Dodaj** funkcji można znaleźć w **aplikacje dla przedsiębiorstw**. Należą do nich:

-   **Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.

-   **Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, który chcesz zapewnić bezpieczne jednokrotnego do zewnętrznie.

-   **Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce tworzenie aplikacji na platformie rozwoju aplikacji Azure AD, ale który nie istnieje jeszcze.

-   **Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji! Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który chcesz zintegrować dla rejestracji jednokrotnej z usługą Azure AD.

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a>Funkcje i możliwości obsługiwane przez wszystkie powyższe typy aplikacji

Następujące funkcje są obsługiwane przez żaden z powyższych typów 4 aplikacji w usłudze Azure AD:

-   **Szybki start** — rozpocząć korzystanie z aplikacji, szybko wykonując [kroki wdrażania prostego](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Ogólne właściwości zarządzania** — Pobierz [głębokiego łącza bezpośrednie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) do aplikacji, [Dostosuj znakowanie](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) aplikacji lub [wyłączenie aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)dla wszystkich użytkowników.

-   **Zarządzanie użytkownikami i grupami** — [przypisać](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) lub [Usuń](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) użytkowników i grup do aplikacji i opcjonalnie przypisać role określonej aplikacji Użytkownicy i grupy mają dostęp do

-   **Dostęp do aplikacji Sklep internetowy** — pozwalają użytkownikom na żądanie [dostęp do aplikacji Sklep internetowy](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) do aplikacji z ich paneli dostępu do aplikacji, albo poprzez dodanie aplikacji bezpośrednio lub [ Dołączanie do grupy włączone samoobsługi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), opcjonalnie wymaganie zatwierdzenia biznesowych na bieżąco

-   **Zaloguj się w dziennikach** — zobacz [wszystkie sesje logowania do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), lub wszystkich aplikacji

-   **Dzienniki inspekcji** — zobacz [szczegółowe dzienniki inspekcji o modyfikacje aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), lub do wszystkich aplikacji

-   **Dostęp warunkowy i ryzyka** — Ustaw zaawansowane [zasady dostępu na podstawie warunku](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) który są wymuszane, gdy użytkownicy próbują zalogować się do określonej aplikacji

-   **Wyświetl uprawnienia** — przeglądać [uprawnienia OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) aplikacji ma dostęp do katalogu z jednej umieść

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Logowanie jednokrotne i Inicjowanie obsługi trybów obsługiwanych przez typy określonych aplikacji

W poniższej tabeli opisano różne rejestracji jednokrotnej i inicjowania obsługi administracyjnej trybów obsługiwanych przez każdą z powyższych typów aplikacji. Aby ułatwić zrozumienie aplikacji, które należy dodać do obsługi określonego celu, można użyć tej tabeli.

  ![Tabela typów aplikacji](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a>Jak wybrać tryb pojedynczy logowania jednokrotnego

Obsługiwane **logowanie jednokrotne** tryby aplikacji usługi Azure AD są wymienione poniżej.

-   **Azure AD rejestracji jednokrotnej wyłączone** — Wybieranie usługi Azure AD rejestracji jednokrotnej wyłączone **tryb rejestracji jednokrotnej** Jeśli nie jest jeszcze gotowa do integracji aplikacji z rejestracji jednokrotnej z usługą Azure AD, lub po prostu testowania go

-   **Połączone logowania jednokrotnego** — wybierz [połączonej logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli masz aplikację, która jest już połączona z istniejącym pojedynczego logowania jednokrotnego rozwiązaniem lub jeśli chcesz, aby Publikowanie proste łącze dla użytkowników w ich [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lub [uruchamiający aplikację usługi Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Na podstawie hasła logowania jednokrotnego** — wybierz [opartego na hasłach logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli aplikacja renderuje nazwy użytkownika i hasła pola HTML i chcesz przechowywać tej nazwy użytkownika i hasło, aby bezpiecznie odtworzone później w aplikacji

-   **Na podstawie SAML logowania jednokrotnego** — wybierz [na języku SAML logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) jednokrotnego tryb, jeśli aplikacja obsługuje protokoły SAML lub OpenID Connect lub chcesz mieć możliwość mapowanie użytkowników do ról aplikacji określonym na podstawie reguł Definiowanie w Twojej oświadczeń SAML *

   >[!NOTE]
   >Ta opcja nie jest dostępna, gdy serwer proxy aplikacji jest skonfigurowana dla aplikacji.
   >
   >

-   **Na podstawie nagłówka logowania jednokrotnego** — wybierz tę opcję, [na podstawie nagłówka logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) logowania jednokrotnego w tryb jednego Jeśli masz aplikację przy użyciu PingAccess, która obsługuje nagłówka HTTP na podstawie uwierzytelniania, który chcesz wykonać jednokrotnego do 

   >[!NOTE]
   >Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji i PingAccess jest skonfigurowana dla aplikacji.
   >
   >

-   **Zintegrowane uwierzytelnianie systemu Windows** — wybierz [zintegrowane uwierzytelnianie systemu Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) jednokrotnego tryb podczas udostępnianie chcesz wykonać jednokrotnego do aplikacji WIA lokalnej 

   >[!NOTE]
   >Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji jest skonfigurowana dla aplikacji.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Tryby pojedynczego logowania jednokrotnego dla aplikacji utworzonych niestandardowych

Aplikacje mają niestandardowe opracowane przez [opracowany niestandardowych aplikacji](#_Custom-Developed_Applications) środowisko obsługuje również dodatkowe pojedynczego logowania jednokrotnego tryby nie są wymienione powyżej. Należą do nich:

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) logowania na podstawie

-   [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) logowania na podstawie

-   [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) logowania na podstawie

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) logowania na podstawie

Odczyt [przewodnik dewelopera usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) Aby dowiedzieć się więcej o sposobie tworzenia aplikacji utworzonych niestandardowych, obsługujący pojedynczego logowania jednokrotnego trybów.

## <a name="how-to-set-an-applications-single-sign-on-mode"></a>Jak ustawić aplikacji logowania jednokrotnego w tryb jednego

Aby ustawić aplikacji **logowanie jednokrotne** tryb, postępuj zgodnie z instrukcjami poniżej:

1.  Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**

6.  Wybierz aplikację, dla której chcesz skonfigurować logowanie jednokrotne.

7.  Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.

## <a name="how-to-choose-a-provisioning-mode"></a>Jak wybrać tryb obsługi administracyjnej

-   **Ręcznego inicjowania obsługi administracyjnej** — wybierz [ręcznego](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) tryb obsługi administracyjnej, jeśli masz istniejące konta lub chcesz zarządzać kontami dla tej aplikacji poza usługą Azure AD.

-   **Automatycznego inicjowania obsługi administracyjnej** — wybierz [automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **tryb obsługi administracyjnej** Jeśli chcesz włączyć automatyczne udostępnianie oparty na interfejsach API i/lub anulowanie obsługi kont użytkowników do tego aplikacji 

   >[!NOTE]
   >Ta opcja jest dostępna tylko dla aplikacji w obrębie **umieszczony** kategorii [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Na podstawie SCIM automatyczne udostępnianie** — użyj [SCIM alokacją opartą na automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) Jeśli aplikacja obsługuje protokół SCIM wykrywania zmian dla użytkowników i grup, które są automatycznie emitowane zmiany dowolnej aplikacji, zintegrowany z usługą Azure AD 

   >[!NOTE]
   >Ta opcja nie jest wymieniony jako określony tryb inicjowania obsługi administracyjnej, ale jest domyślnie włączona dla wszystkich aplikacji, które są zintegrowane z usługą Azure AD.
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a>Jak ustawić aplikacji do trybu obsługi administracyjnej

Aby ustawić aplikacji **inicjowania obsługi administracyjnej** tryb, postępuj zgodnie z instrukcjami poniżej:

Aby ustawić aplikacji **logowanie jednokrotne** tryb, postępuj zgodnie z instrukcjami poniżej:

1.  Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**

6.  Wybierz aplikację, dla której chcesz skonfigurować, inicjowania obsługi administracyjnej.

7.  Po załadowaniu aplikacji, kliknij przycisk **inicjowania obsługi administracyjnej** z menu nawigacji po lewej stronie aplikacji.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
