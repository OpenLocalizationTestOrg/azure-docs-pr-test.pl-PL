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
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="5ba4c-103">Wybieranie typu aplikacji używanego podczas dodawania aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="5ba4c-104">Ten artykuł ułatwia zrozumienie cztery typy aplikacji, którą można zintegrować z usługą Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="5ba4c-105">Co to jest obsługiwany przez każdy z nich</span><span class="sxs-lookup"><span data-stu-id="5ba4c-105">What is supported by each of them</span></span>
* <span data-ttu-id="5ba4c-106">Dlaczego może wybrać aplikację</span><span class="sxs-lookup"><span data-stu-id="5ba4c-106">Why you might choose which application</span></span>
* <span data-ttu-id="5ba4c-107">Jak skonfigurować właściwości core tych aplikacji, takich jak użytkowników **elastycznie**, lub co **logowanie jednokrotne** technologii.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="5ba4c-108">Typy aplikacji obsługiwanych w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba4c-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="5ba4c-109">Usługi Azure AD obsługuje cztery typy aplikacji głównej, które można dodać przy użyciu **Dodaj** funkcji można znaleźć w **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="5ba4c-110">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-110">These include:</span></span>

-   <span data-ttu-id="5ba4c-111">**Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="5ba4c-112">**Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, który chcesz zapewnić bezpieczne jednokrotnego do zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="5ba4c-113">**Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce tworzenie aplikacji na platformie rozwoju aplikacji Azure AD, ale który nie istnieje jeszcze.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="5ba4c-114">**Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5ba4c-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="5ba4c-115">Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który chcesz zintegrować dla rejestracji jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="5ba4c-116">Funkcje i możliwości obsługiwane przez wszystkie powyższe typy aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="5ba4c-117">Następujące funkcje są obsługiwane przez żaden z powyższych typów 4 aplikacji w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="5ba4c-118">**Szybki start** — rozpocząć korzystanie z aplikacji, szybko wykonując [kroki wdrażania prostego](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="5ba4c-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="5ba4c-119">**Ogólne właściwości zarządzania** — Pobierz [głębokiego łącza bezpośrednie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) do aplikacji, [Dostosuj znakowanie](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) aplikacji lub [wyłączenie aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="5ba4c-120">**Zarządzanie użytkownikami i grupami** — [przypisać](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) lub [Usuń](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) użytkowników i grup do aplikacji i opcjonalnie przypisać role określonej aplikacji Użytkownicy i grupy mają dostęp do</span><span class="sxs-lookup"><span data-stu-id="5ba4c-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="5ba4c-121">**Dostęp do aplikacji Sklep internetowy** — pozwalają użytkownikom na żądanie [dostęp do aplikacji Sklep internetowy](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) do aplikacji z ich paneli dostępu do aplikacji, albo poprzez dodanie aplikacji bezpośrednio lub [ Dołączanie do grupy włączone samoobsługi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), opcjonalnie wymaganie zatwierdzenia biznesowych na bieżąco</span><span class="sxs-lookup"><span data-stu-id="5ba4c-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="5ba4c-122">**Zaloguj się w dziennikach** — zobacz [wszystkie sesje logowania do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), lub wszystkich aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="5ba4c-123">**Dzienniki inspekcji** — zobacz [szczegółowe dzienniki inspekcji o modyfikacje aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), lub do wszystkich aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="5ba4c-124">**Dostęp warunkowy i ryzyka** — Ustaw zaawansowane [zasady dostępu na podstawie warunku](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) który są wymuszane, gdy użytkownicy próbują zalogować się do określonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="5ba4c-125">**Wyświetl uprawnienia** — przeglądać [uprawnienia OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) aplikacji ma dostęp do katalogu z jednej umieść</span><span class="sxs-lookup"><span data-stu-id="5ba4c-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="5ba4c-126">Logowanie jednokrotne i Inicjowanie obsługi trybów obsługiwanych przez typy określonych aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="5ba4c-127">W poniższej tabeli opisano różne rejestracji jednokrotnej i inicjowania obsługi administracyjnej trybów obsługiwanych przez każdą z powyższych typów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="5ba4c-128">Aby ułatwić zrozumienie aplikacji, które należy dodać do obsługi określonego celu, można użyć tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Tabela typów aplikacji](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="5ba4c-130">Jak wybrać tryb pojedynczy logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="5ba4c-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="5ba4c-131">Obsługiwane **logowanie jednokrotne** tryby aplikacji usługi Azure AD są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="5ba4c-132">**Azure AD rejestracji jednokrotnej wyłączone** — Wybieranie usługi Azure AD rejestracji jednokrotnej wyłączone **tryb rejestracji jednokrotnej** Jeśli nie jest jeszcze gotowa do integracji aplikacji z rejestracji jednokrotnej z usługą Azure AD, lub po prostu testowania go</span><span class="sxs-lookup"><span data-stu-id="5ba4c-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="5ba4c-133">**Połączone logowania jednokrotnego** — wybierz [połączonej logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli masz aplikację, która jest już połączona z istniejącym pojedynczego logowania jednokrotnego rozwiązaniem lub jeśli chcesz, aby Publikowanie proste łącze dla użytkowników w ich [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lub [uruchamiający aplikację usługi Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="5ba4c-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="5ba4c-134">**Na podstawie hasła logowania jednokrotnego** — wybierz [opartego na hasłach logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tryb rejestracji jednokrotnej** Jeśli aplikacja renderuje nazwy użytkownika i hasła pola HTML i chcesz przechowywać tej nazwy użytkownika i hasło, aby bezpiecznie odtworzone później w aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="5ba4c-135">**Na podstawie SAML logowania jednokrotnego** — wybierz [na języku SAML logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) jednokrotnego tryb, jeśli aplikacja obsługuje protokoły SAML lub OpenID Connect lub chcesz mieć możliwość mapowanie użytkowników do ról aplikacji określonym na podstawie reguł Definiowanie w Twojej oświadczeń SAML *</span><span class="sxs-lookup"><span data-stu-id="5ba4c-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="5ba4c-136">Ta opcja nie jest dostępna, gdy serwer proxy aplikacji jest skonfigurowana dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="5ba4c-137">**Na podstawie nagłówka logowania jednokrotnego** — wybierz tę opcję, [na podstawie nagłówka logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) logowania jednokrotnego w tryb jednego Jeśli masz aplikację przy użyciu PingAccess, która obsługuje nagłówka HTTP na podstawie uwierzytelniania, który chcesz wykonać jednokrotnego do</span><span class="sxs-lookup"><span data-stu-id="5ba4c-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5ba4c-138">Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji i PingAccess jest skonfigurowana dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="5ba4c-139">**Zintegrowane uwierzytelnianie systemu Windows** — wybierz [zintegrowane uwierzytelnianie systemu Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) jednokrotnego tryb podczas udostępnianie chcesz wykonać jednokrotnego do aplikacji WIA lokalnej</span><span class="sxs-lookup"><span data-stu-id="5ba4c-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5ba4c-140">Ta opcja jest dostępna tylko w przypadku, gdy serwer proxy aplikacji jest skonfigurowana dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="5ba4c-141">Tryby pojedynczego logowania jednokrotnego dla aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="5ba4c-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="5ba4c-142">Aplikacje mają niestandardowe opracowane przez [opracowany niestandardowych aplikacji](#_Custom-Developed_Applications) środowisko obsługuje również dodatkowe pojedynczego logowania jednokrotnego tryby nie są wymienione powyżej.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="5ba4c-143">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-143">These include:</span></span>

-   <span data-ttu-id="5ba4c-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) logowania na podstawie</span><span class="sxs-lookup"><span data-stu-id="5ba4c-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="5ba4c-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) logowania na podstawie</span><span class="sxs-lookup"><span data-stu-id="5ba4c-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="5ba4c-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) logowania na podstawie</span><span class="sxs-lookup"><span data-stu-id="5ba4c-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="5ba4c-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) logowania na podstawie</span><span class="sxs-lookup"><span data-stu-id="5ba4c-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="5ba4c-148">Odczyt [przewodnik dewelopera usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) Aby dowiedzieć się więcej o sposobie tworzenia aplikacji utworzonych niestandardowych, obsługujący pojedynczego logowania jednokrotnego trybów.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="5ba4c-149">Jak ustawić aplikacji logowania jednokrotnego w tryb jednego</span><span class="sxs-lookup"><span data-stu-id="5ba4c-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="5ba4c-150">Aby ustawić aplikacji **logowanie jednokrotne** tryb, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="5ba4c-151">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="5ba4c-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5ba4c-152">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ba4c-153">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ba4c-154">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ba4c-155">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5ba4c-156">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="5ba4c-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5ba4c-157">Wybierz aplikację, dla której chcesz skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5ba4c-158">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="5ba4c-159">Jak wybrać tryb obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="5ba4c-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="5ba4c-160">**Ręcznego inicjowania obsługi administracyjnej** — wybierz [ręcznego](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) tryb obsługi administracyjnej, jeśli masz istniejące konta lub chcesz zarządzać kontami dla tej aplikacji poza usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="5ba4c-161">**Automatycznego inicjowania obsługi administracyjnej** — wybierz [automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **tryb obsługi administracyjnej** Jeśli chcesz włączyć automatyczne udostępnianie oparty na interfejsach API i/lub anulowanie obsługi kont użytkowników do tego aplikacji</span><span class="sxs-lookup"><span data-stu-id="5ba4c-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5ba4c-162">Ta opcja jest dostępna tylko dla aplikacji w obrębie **umieszczony** kategorii [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="5ba4c-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="5ba4c-163">**Na podstawie SCIM automatyczne udostępnianie** — użyj [SCIM alokacją opartą na automatyczne](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) Jeśli aplikacja obsługuje protokół SCIM wykrywania zmian dla użytkowników i grup, które są automatycznie emitowane zmiany dowolnej aplikacji, zintegrowany z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba4c-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5ba4c-164">Ta opcja nie jest wymieniony jako określony tryb inicjowania obsługi administracyjnej, ale jest domyślnie włączona dla wszystkich aplikacji, które są zintegrowane z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="5ba4c-165">Jak ustawić aplikacji do trybu obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="5ba4c-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="5ba4c-166">Aby ustawić aplikacji **inicjowania obsługi administracyjnej** tryb, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="5ba4c-167">Aby ustawić aplikacji **logowanie jednokrotne** tryb, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="5ba4c-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="5ba4c-168">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="5ba4c-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5ba4c-169">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ba4c-170">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ba4c-171">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ba4c-172">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5ba4c-173">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="5ba4c-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5ba4c-174">Wybierz aplikację, dla której chcesz skonfigurować, inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="5ba4c-175">Po załadowaniu aplikacji, kliknij przycisk **inicjowania obsługi administracyjnej** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba4c-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ba4c-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ba4c-176">Next steps</span></span>
[<span data-ttu-id="5ba4c-177">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ba4c-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
