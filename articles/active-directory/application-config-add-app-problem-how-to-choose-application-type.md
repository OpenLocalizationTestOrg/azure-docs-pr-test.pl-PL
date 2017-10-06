---
title: "która aplikacja wpisz toouse podczas dodawania aplikacji toochoose aaaHow | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello obsługiwane typy aplikacji można zintegrować z usługą Azure AD i ich powiązane opcje konfiguracji"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Jak toochoose, która aplikacja wpisz toouse podczas dodawania aplikacji

W tym artykule pomocy toounderstand hello cztery typy aplikacji, którą można zintegrować z usługą Azure AD:

* Co to jest obsługiwany przez każdy z nich
* Dlaczego może wybrać aplikację
* Jak tooconfigure właściwości core tych aplikacji, jak użytkowników **elastycznie**, lub co **logowanie jednokrotne** toouse technologii.

## <a name="supported-application-types-in-azure-ad"></a>Typy aplikacji obsługiwanych w usłudze Azure AD

Azure AD obsługuje czterech głównych typów aplikacji, które można dodać przy użyciu hello **Dodaj** funkcji można znaleźć w **aplikacje dla przedsiębiorstw**. Należą do nich:

-   **Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.

-   **Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, które mają tooprovide bezpiecznego jednokrotnego tooexternally.

-   **Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce toodevelop na hello platformę tworzenia aplikacji w usłudze Azure AD, ale który nie istnieje jeszcze.

-   **Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji! Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który ma toointegrate dla rejestracji jednokrotnej z usługą Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Funkcje i możliwości obsługiwane przez wszystkie hello powyżej typy aplikacji

Witaj następujące funkcje są obsługiwane przez żadną hello powyżej 4 typy aplikacji w usłudze Azure AD:

-   **Szybki start** — rozpocząć korzystanie z aplikacji, szybko wykonując [kroki wdrażania prostego](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Ogólne właściwości zarządzania** — Pobierz [głębokiego łącza bezpośrednie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) aplikacji tooan [Dostosowywanie znakowania hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) aplikacji lub [wyłączenie aplikacji hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) dla wszystkich użytkowników.

-   **Zarządzanie użytkownikami i grupami** — [przypisać](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) lub [Usuń](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) aplikacji tooan użytkowników i grup oraz opcjonalnie ról określonych aplikacji hello Przypisz użytkowników i grupy mają dostęp do

-   **Dostęp do aplikacji Sklep internetowy** — Włączanie toorequest Twojego użytkowników [dostęp do aplikacji Sklep internetowy](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan aplikacji z ich dostęp do aplikacji płyty przez dodanie aplikacji bezpośrednio lub [ Dołączanie do grupy włączone samoobsługi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), opcjonalnie wymaganie zatwierdzenia firm wzdłuż hello sposób

-   **Zaloguj się w dziennikach** — zobacz [hello wszystkich aplikacji tooan logowania](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), lub wszystkich aplikacji

-   **Dzienniki inspekcji** — zobacz [szczegółowe dzienniki inspekcji o zmianach aplikacji tooan](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), lub tooall aplikacji

-   **Dostęp warunkowy i ryzyka** — Ustaw zaawansowane [zasady dostępu na podstawie warunku](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) który są wymuszane, gdy użytkownicy próbują toosign w określonej aplikacji tooa

-   **Wyświetl uprawnienia** — przeglądać hello [uprawnienia OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) aplikacja ma tooin dostępu do katalogu z jednego miejsca

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Logowanie jednokrotne i Inicjowanie obsługi trybów obsługiwanych przez typy określonych aplikacji

w poniższej tabeli Hello opisano hello różnych rejestracji jednokrotnej i Inicjowanie obsługi trybów obsługiwanych przez każdą hello powyżej typów aplikacji. Korzystając z tej tabeli toohelp toounderstand aplikacji, które należy toosupport tooadd określonego celu.

  ![Tabela typów aplikacji](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Jak toochoose tryb pojedynczy logowania jednokrotnego

Witaj obsługiwane **logowanie jednokrotne** tryby aplikacji usługi Azure AD są wymienione poniżej.

-   **Azure AD rejestracji jednokrotnej wyłączone** — Wybieranie usługi Azure AD rejestracji jednokrotnej wyłączone **tryb rejestracji jednokrotnej** Jeśli nie jest jeszcze gotowy toointegrate tę aplikację przy rejestracji jednokrotnej z usługą Azure AD, lub po prostu testowania go

-   **Połączone logowania jednokrotnego** — wybierz hello [połączonej logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli masz aplikację, która jest już połączona z istniejącym pojedynczego logowania jednokrotnego rozwiązaniem lub jeśli chcesz toopublish prosty łączy dla użytkowników w ich [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lub [uruchamiający aplikację usługi Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Na podstawie hasła logowania jednokrotnego** — wybierz hello [opartego na hasłach logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli aplikacja renderuje nazwy użytkownika i hasła pola HTML i ma toostore który Nazwa użytkownika i hasło bezpiecznie toobe odtwarzany toohello aplikację później

-   **Na podstawie SAML logowania jednokrotnego** — wybierz hello [na języku SAML logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) na podstawie ról aplikacji toospecific jednokrotnego tryb, jeśli aplikacja obsługuje protokoły SAML lub OpenID Connect hello lub użytkownicy mogli toomap toobe reguły zdefiniowane w Twojej SAML oświadczeń *

   >[!NOTE]
   >Ta opcja nie jest dostępna, gdy serwer proxy aplikacji hello jest skonfigurowany dla aplikacji.
   >
   >

-   **Na podstawie nagłówka logowania jednokrotnego** — wybierz tę opcję, [na podstawie nagłówka logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) logowania jednokrotnego w tryb jednego Jeśli masz aplikację przy użyciu PingAccess, która obsługuje nagłówka HTTP na podstawie uwierzytelniania, która ma jednokrotnego tooperform na zbyt

   >[!NOTE]
   >Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji hello i PingAccess jest skonfigurowana dla aplikacji.
   >
   >

-   **Zintegrowane uwierzytelnianie systemu Windows** — wybierz hello [zintegrowane uwierzytelnianie systemu Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) jednokrotnego tryb podczas udostępnianie aplikacji WIA lokalnej, która ma jednokrotnego tooperform na zbyt

   >[!NOTE]
   >Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji hello jest skonfigurowany dla aplikacji.
   >
   >

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

6.  Wybierz aplikację hello, dla której ma zostać tooconfigure rejestracji jednokrotnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

## <a name="how-toochoose-a-provisioning-mode"></a>Jak toochoose tryb obsługi administracyjnej

-   **Ręcznego inicjowania obsługi administracyjnej** — wybierz hello [ręcznego](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) tryb obsługi administracyjnej, jeśli masz istniejące konta lub chcesz toomanage kont dla tej aplikacji poza usługą Azure AD.

-   **Automatycznego inicjowania obsługi administracyjnej** — wybierz hello [automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **tryb obsługi administracyjnej** Jeśli tooenable automatyczne oparty na interfejsach API udostępnianie i/lub usuwania inicjowania obsługi administracyjnej toothis kont użytkowników aplikacji 

   >[!NOTE]
   >Ta opcja jest dostępna tylko dla aplikacji w obrębie hello **umieszczony** kategorii hello [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Na podstawie SCIM automatyczne udostępnianie** — użyj [SCIM alokacją opartą na automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) Jeśli aplikacja obsługuje protokół SCIM hello wykrywania toousers zmian i grup, które są automatycznie emitowane zmian Aplikacja tooany zintegrowane z usługą Azure AD 

   >[!NOTE]
   >Ta opcja nie jest wymieniony jako określony tryb inicjowania obsługi administracyjnej, ale jest domyślnie włączona dla wszystkich aplikacji, które są zintegrowane z usługą Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Jak tooset aplikacji do trybu obsługi administracyjnej

tooset aplikacji **inicjowania obsługi administracyjnej** tryb, wykonaj poniższe instrukcje hello:

tooset aplikacji **logowanie jednokrotne** tryb, wykonaj poniższe instrukcje hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello, dla której ma zostać tooconfigure inicjowania obsługi administracyjnej.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **inicjowania obsługi administracyjnej** z menu nawigacji po lewej stronie powitania aplikacji.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
