---
title: "Problemy przy logowaniu do aplikacji w panelu dostępu | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać problemy podczas uzyskiwania dostępu do aplikacji, z panelu dostępu do programu Microsoft Azure AD w myapps.microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="92d14-103">Problemy przy logowaniu do aplikacji w panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="92d14-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="92d14-104">Panel dostępu jest oparte na sieci web portalu, która pozwala użytkownikom przy użyciu konta służbowego w usłudze Azure Active Directory (Azure AD) do wyświetlania i uruchamiania aplikacji opartej na chmurze, czy administrator usługi Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="92d14-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="92d14-105">Te aplikacje są skonfigurowane w imieniu użytkownika w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92d14-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="92d14-106">Aplikacja musi prawidłowo skonfigurowane i przypisane do użytkownika lub grupy, których użytkownik jest członkiem, aby zobaczyć aplikację w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92d14-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="92d14-107">Typ aplikacji, które użytkownik może być widoczny można podzielić na następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="92d14-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="92d14-108">Aplikacje pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="92d14-108">Office 365 Applications</span></span>

-   <span data-ttu-id="92d14-109">Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="92d14-110">Aplikacje oparte na hasłach logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="92d14-111">Aplikacje z istniejącymi rozwiązaniami do logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="92d14-112">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="92d14-112">General issues to check first</span></span>

-   <span data-ttu-id="92d14-113">Upewnij się, Twoje przy użyciu **przeglądarki** spełniające minimalne wymagania dotyczące panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92d14-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="92d14-114">Upewnij się, że przeglądarka użytkownika został dodany adres URL aplikacji do jego **Zaufane witryny**.</span><span class="sxs-lookup"><span data-stu-id="92d14-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="92d14-115">Upewnij się sprawdzić, aplikacja jest **skonfigurowane** poprawnie.</span><span class="sxs-lookup"><span data-stu-id="92d14-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="92d14-116">Upewnij się, że konto użytkownika jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="92d14-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="92d14-117">Upewnij się, że konto użytkownika jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="92d14-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="92d14-118">Upewnij się, że użytkownika **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="92d14-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="92d14-119">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="92d14-120">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="92d14-121">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** jest aktualny, aby umożliwić uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasad, które mają być egzekwowane.</span><span class="sxs-lookup"><span data-stu-id="92d14-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="92d14-122">Upewnij się, że również spróbuj wyczyszczenie plików cookie w przeglądarce, a następnie spróbuj się ponownie zalogować.</span><span class="sxs-lookup"><span data-stu-id="92d14-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="92d14-123">Spełniające wymagania przeglądarki do panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="92d14-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="92d14-124">Panel dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="92d14-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="92d14-125">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="92d14-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="92d14-126">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="92d14-127">Logowanie Jednokrotne opartego na hasłach można przeglądarki przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="92d14-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="92d14-128">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="92d14-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="92d14-129">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="92d14-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="92d14-130">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="92d14-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="92d14-131">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="92d14-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="92d14-132">Jak zainstalować rozszerzenie przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="92d14-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="92d14-133">Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-134">Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92d14-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="92d14-135">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92d14-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="92d14-136">W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="92d14-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="92d14-137">Oparte na przeglądarce być kierowane do łącza pobierania.</span><span class="sxs-lookup"><span data-stu-id="92d14-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="92d14-138">**Dodaj** rozszerzenia do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="92d14-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="92d14-139">Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="92d14-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="92d14-140">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="92d14-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="92d14-141">Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="92d14-142">Może również pobrać rozszerzenia dla programu Chrome i krawędzi z bezpośrednich łączy poniżej:</span><span class="sxs-lookup"><span data-stu-id="92d14-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="92d14-143">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="92d14-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="92d14-144">Rozszerzenie panelu dostępu krawędzi</span><span class="sxs-lookup"><span data-stu-id="92d14-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="92d14-145">Konfigurowanie federacyjnych rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="92d14-146">Wszystkie aplikacji w galerii Azure AD włączone możliwości przedsiębiorstwa rejestracji jednokrotnej ma dostępne samouczek krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="92d14-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="92d14-147">Dostęp można uzyskać [lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="92d14-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="92d14-148">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="92d14-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="92d14-149">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="92d14-150">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="92d14-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="92d14-151">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="92d14-152">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="92d14-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="92d14-153">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="92d14-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="92d14-154">Przypisywanie użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="92d14-155">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="92d14-156">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-157">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="92d14-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="92d14-158">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-159">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-160">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-161">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="92d14-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="92d14-162">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="92d14-163">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="92d14-164">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="92d14-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="92d14-165">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92d14-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="92d14-166">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="92d14-167">Konfigurowanie rejestracji jednokrotnej dla aplikacji z galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="92d14-168">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-170">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-171">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-172">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-173">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="92d14-174">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-175">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="92d14-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="92d14-176">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-177">Wybierz **na języku SAML logowania jednokrotnego** z **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="92d14-178">Wprowadź wymagane wartości w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="92d14-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="92d14-179">Te wartości należy uzyskać od dostawcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="92d14-180">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane SP, zaloguj się na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="92d14-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="92d14-181">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="92d14-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="92d14-182">Aby skonfigurować aplikację jako logowanie Jednokrotne zainicjowane IdP, adres URL odpowiedzi jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="92d14-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="92d14-183">Dla pewnych aplikacji identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="92d14-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="92d14-184">**Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz zobaczyć wartości innych niż wymagana.</span><span class="sxs-lookup"><span data-stu-id="92d14-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="92d14-185">W **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="92d14-186">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="92d14-187">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="92d14-187">To add an attribute:</span></span>

   1. <span data-ttu-id="92d14-188">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="92d14-188">click **Add attribute**.</span></span> <span data-ttu-id="92d14-189">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="92d14-190">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="92d14-190">Click **Save.**</span></span> <span data-ttu-id="92d14-191">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92d14-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="92d14-192">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  dokumentacji dostępu na temat konfigurowania rejestracji jednokrotnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="92d14-193">Ponadto ma metadanych adresy URL i certyfikatu wymagane do konfiguracji logowania jednokrotnego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="92d14-194">Kliknij przycisk **zapisać** Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="92d14-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="92d14-195">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="92d14-196">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="92d14-197">Aby wybrać identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-198">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-199">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-200">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-201">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-202">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="92d14-203">Jeśli nie widzisz aplikacji ma być wyświetlane w tym miejscu, należy użyć **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-204">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="92d14-205">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-206">W obszarze **atrybuty użytkownika** wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="92d14-207">Wybrana opcja musi być zgodna z oczekiwaną wartością w aplikacji w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="92d14-208">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="92d14-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="92d14-209">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="92d14-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="92d14-210">Aby dodać atrybuty użytkownika, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="92d14-211">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="92d14-211">To add an attribute:</span></span>

   1. <span data-ttu-id="92d14-212">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="92d14-212">click **Add attribute**.</span></span> <span data-ttu-id="92d14-213">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="92d14-214">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="92d14-214">Click **Save.**</span></span> <span data-ttu-id="92d14-215">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92d14-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="92d14-216">Pobieranie metadanych usługi Azure AD lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="92d14-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="92d14-217">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-218">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-219">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-220">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-221">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-222">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="92d14-223">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-224">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="92d14-225">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-226">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="92d14-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="92d14-227">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="92d14-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="92d14-228">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="92d14-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="92d14-229">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="92d14-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="92d14-230">Jak skonfigurować federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="92d14-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="92d14-231">Aby skonfigurować aplikację z systemem innym niż galerii, musisz mieć usługi Azure AD premium, a aplikacja obsługuje SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="92d14-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="92d14-232">Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="92d14-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="92d14-233">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="92d14-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="92d14-234">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="92d14-235">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="92d14-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="92d14-236">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="92d14-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="92d14-237">Skonfiguruj wartości metadanych aplikacji w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="92d14-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="92d14-238">Aby skonfigurować logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-239">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-240">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-241">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-242">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-243">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="92d14-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="92d14-244">Kliknij przycisk **Non galerii aplikacji** w **dodać własną aplikację** sekcji</span><span class="sxs-lookup"><span data-stu-id="92d14-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="92d14-245">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="92d14-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="92d14-246">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92d14-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="92d14-247">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="92d14-248">Wybierz **na języku SAML logowania jednokrotnego** w **tryb** listy rozwijanej</span><span class="sxs-lookup"><span data-stu-id="92d14-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="92d14-249">Wprowadź wymagane wartości w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="92d14-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="92d14-250">Te wartości należy uzyskać od dostawcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="92d14-251">Aby skonfigurować aplikację jako SSO inicjowanych przez dostawców tożsamości, wprowadź adres URL odpowiedzi i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="92d14-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="92d14-252">**Opcjonalnie:** Konfigurowanie aplikacji jako logowanie Jednokrotne zainicjowane SP, zaloguj się na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="92d14-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="92d14-253">W **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="92d14-254">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="92d14-255">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="92d14-255">To add an attribute:</span></span>

   1. <span data-ttu-id="92d14-256">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="92d14-256">click **Add attribute**.</span></span> <span data-ttu-id="92d14-257">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="92d14-258">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="92d14-258">Click **Save.**</span></span> <span data-ttu-id="92d14-259">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92d14-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="92d14-260">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  dokumentacji dostępu na temat konfigurowania rejestracji jednokrotnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="92d14-261">Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="92d14-262">Wybierz identyfikator użytkownika i dodać atrybuty użytkownika mają być wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="92d14-263">Aby wybrać identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-264">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-265">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-266">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-267">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-268">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="92d14-269">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-270">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="92d14-271">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-272">W obszarze **atrybuty użytkownika** wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="92d14-273">Wybrana opcja musi być zgodna z oczekiwaną wartością w aplikacji w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="92d14-274">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="92d14-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="92d14-275">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="92d14-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="92d14-276">Aby dodać atrybuty użytkownika, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92d14-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="92d14-277">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="92d14-277">To add an attribute:</span></span>

   <span data-ttu-id="92d14-278">1. Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="92d14-278">1.click **Add attribute**.</span></span> <span data-ttu-id="92d14-279">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="92d14-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="92d14-280">2 kliknij **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="92d14-280">2 Click **Save.**</span></span> <span data-ttu-id="92d14-281">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92d14-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="92d14-282">Pobieranie metadanych usługi Azure AD lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="92d14-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="92d14-283">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-284">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-285">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-286">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-287">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-288">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="92d14-289">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-290">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92d14-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="92d14-291">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-292">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="92d14-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="92d14-293">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="92d14-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="92d14-294">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="92d14-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="92d14-295">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="92d14-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="92d14-296">Jak skonfigurować hasło rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="92d14-297">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="92d14-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="92d14-298">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="92d14-299">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="92d14-300">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d14-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="92d14-301">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-302">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="92d14-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="92d14-303">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-304">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-305">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-306">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="92d14-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="92d14-307">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="92d14-308">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="92d14-309">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="92d14-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="92d14-310">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92d14-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="92d14-311">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="92d14-312">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="92d14-313">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-314">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-315">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-316">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-317">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-318">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="92d14-319">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-320">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92d14-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="92d14-321">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-322">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="92d14-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="92d14-323">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-323">Assign users to the application.</span></span>

10. <span data-ttu-id="92d14-324">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92d14-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="92d14-325">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="92d14-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="92d14-326">Jak skonfigurować hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="92d14-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="92d14-327">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="92d14-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="92d14-328">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="92d14-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="92d14-329">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="92d14-330">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="92d14-330">Add a non-gallery application</span></span>

<span data-ttu-id="92d14-331">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-332">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="92d14-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="92d14-333">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-334">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-335">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-336">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="92d14-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="92d14-337">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="92d14-338">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="92d14-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="92d14-339">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="92d14-339">Select **Add.**</span></span>

<span data-ttu-id="92d14-340">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="92d14-341">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="92d14-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="92d14-342">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-343">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="92d14-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92d14-344">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-345">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-346">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-347">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="92d14-348">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-349">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="92d14-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="92d14-350">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-351">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="92d14-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="92d14-352">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="92d14-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="92d14-353">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="92d14-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="92d14-354">Upewnij się, że logowanie pola są widoczne pod adresem URL.</span><span class="sxs-lookup"><span data-stu-id="92d14-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="92d14-355">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-355">Assign users to the application.</span></span>

11. <span data-ttu-id="92d14-356">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92d14-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="92d14-357">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="92d14-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="92d14-358">Jak przypisać użytkownika bezpośrednio do aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="92d14-359">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92d14-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="92d14-360">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="92d14-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92d14-361">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="92d14-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92d14-362">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="92d14-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92d14-363">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92d14-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92d14-364">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="92d14-365">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="92d14-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="92d14-366">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="92d14-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="92d14-367">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="92d14-368">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="92d14-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="92d14-369">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="92d14-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="92d14-370">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="92d14-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="92d14-371">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="92d14-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="92d14-372">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="92d14-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="92d14-373">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="92d14-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="92d14-374">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92d14-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="92d14-375">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="92d14-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="92d14-376">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92d14-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="92d14-377">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92d14-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="92d14-378">Jeśli te kroki rozwiązywania problemów nie Rozwiąż problem</span><span class="sxs-lookup"><span data-stu-id="92d14-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="92d14-379">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="92d14-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="92d14-380">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="92d14-380">Correlation error ID</span></span>

-   <span data-ttu-id="92d14-381">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="92d14-381">UPN (user email address)</span></span>

-   <span data-ttu-id="92d14-382">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="92d14-382">TenantID</span></span>

-   <span data-ttu-id="92d14-383">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="92d14-383">Browser type</span></span>

-   <span data-ttu-id="92d14-384">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="92d14-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="92d14-385">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="92d14-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="92d14-386">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92d14-386">Next steps</span></span>
[<span data-ttu-id="92d14-387">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="92d14-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

