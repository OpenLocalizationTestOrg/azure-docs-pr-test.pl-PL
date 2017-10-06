---
title: "podpisywania aplikacji tooan z panelu dostępu hello aaaProblems | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy dotyczące uzyskiwania dostępu do aplikacji z hello panelu dostępu do programu Microsoft Azure AD w myapps.microsoft.com"
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
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="9ddfc-103">Problemy przy logowaniu tooan aplikacji hello panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="9ddfc-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="9ddfc-104">Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="9ddfc-105">Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="9ddfc-106">Aplikacja Hello musi być prawidłowo skonfigurowane i przypisane toohello użytkownika lub grupy hello użytkownika jest członkiem grupy aplikacji hello toosee w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="9ddfc-107">Typ Hello aplikacje, które użytkownik może być widoczny spadek hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="9ddfc-108">Aplikacje pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="9ddfc-108">Office 365 Applications</span></span>

-   <span data-ttu-id="9ddfc-109">Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="9ddfc-110">Aplikacje oparte na hasłach logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="9ddfc-111">Aplikacje z istniejącymi rozwiązaniami do logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="9ddfc-112">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="9ddfc-112">General issues toocheck first</span></span>

-   <span data-ttu-id="9ddfc-113">Upewnij się, Twoje przy użyciu **przeglądarki** który spełnia wymagania minimalne hello hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="9ddfc-114">Upewnij się, że przeglądarka hello użytkownika został dodany adres URL hello tooits aplikacji hello **Zaufane witryny**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="9ddfc-115">Upewnij się, że aplikacja hello toocheck **skonfigurowane** poprawnie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="9ddfc-116">Upewnij się, że konto użytkownika hello jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="9ddfc-117">Upewnij się, że konto użytkownika hello jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="9ddfc-118">Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="9ddfc-119">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="9ddfc-120">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="9ddfc-121">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="9ddfc-122">Upewnij się, że tooalso spróbuj wyczyszczenie plików cookie w przeglądarce i podjęcie ponownej próby toosign w.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="9ddfc-123">Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="9ddfc-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="9ddfc-124">Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="9ddfc-125">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="9ddfc-126">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="9ddfc-127">Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="9ddfc-128">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="9ddfc-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="9ddfc-129">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="9ddfc-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="9ddfc-130">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="9ddfc-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="9ddfc-131">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="9ddfc-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="9ddfc-132">Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="9ddfc-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="9ddfc-133">hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-134">Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="9ddfc-135">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="9ddfc-136">Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="9ddfc-137">Oparte na przeglądarce można ukierunkowanej toohello łącze.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="9ddfc-138">**Dodaj** hello rozszerzenia tooyour przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="9ddfc-139">Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="9ddfc-140">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="9ddfc-141">Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ddfc-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="9ddfc-142">Może również pobrać hello rozszerzenia dla programu Chrome i krawędzi, z poniższe linki bezpośrednie hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="9ddfc-143">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="9ddfc-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="9ddfc-144">Rozszerzenie panelu dostępu krawędzi</span><span class="sxs-lookup"><span data-stu-id="9ddfc-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9ddfc-145">Jak tooconfigure federacyjne logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9ddfc-146">Wszystkie aplikacji w galerii Azure AD hello włączone możliwości przedsiębiorstwa rejestracji jednokrotnej ma dostępne samouczek krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="9ddfc-147">Dostęp można uzyskać hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="9ddfc-148">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ddfc-149">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="9ddfc-150">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9ddfc-151">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ddfc-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9ddfc-152">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="9ddfc-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9ddfc-153">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9ddfc-154">Przypisywanie użytkowników toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ddfc-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="9ddfc-155">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="9ddfc-156">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-157">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ddfc-158">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-159">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-160">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-161">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="9ddfc-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="9ddfc-162">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="9ddfc-163">Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="9ddfc-164">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="9ddfc-165">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="9ddfc-166">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="9ddfc-167">Konfigurowanie rejestracji jednokrotnej dla aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="9ddfc-168">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-170">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-171">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-172">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-173">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ddfc-174">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-175">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-176">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-177">Wybierz **na języku SAML logowania jednokrotnego** z hello **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="9ddfc-178">Wprowadź wartości hello wymagane w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="9ddfc-179">Te wartości należy uzyskać od dostawcy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="9ddfc-180">Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello logowania na adres URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="9ddfc-181">Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="9ddfc-182">Aplikacja hello tooconfigure jako zainicjował IdP SSO hello adres URL odpowiedzi jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="9ddfc-183">Dla pewnych aplikacji hello identyfikator jest również wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="9ddfc-184">**Opcjonalnie:** kliknij **Pokaż zaawansowane ustawienia adresu URL** Jeśli chcesz toosee hello — wymagane wartości.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="9ddfc-185">W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="9ddfc-186">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="9ddfc-187">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="9ddfc-188">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-188">click **Add attribute**.</span></span> <span data-ttu-id="9ddfc-189">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="9ddfc-190">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-190">Click **Save.**</span></span> <span data-ttu-id="9ddfc-191">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="9ddfc-192">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="9ddfc-193">Ponadto ma hello metadane z adresów URL i certyfikatu wymaganego toosetup rejestracji Jednokrotnej z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="9ddfc-194">Kliknij przycisk **zapisać** toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="9ddfc-195">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="9ddfc-196">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ddfc-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="9ddfc-197">tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-198">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-199">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-200">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-201">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-202">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ddfc-203">Jeśli nie ma aplikacji hello ma tooshow tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-204">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-205">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-206">W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="9ddfc-207">Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ddfc-208">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="9ddfc-209">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="9ddfc-210">atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="9ddfc-211">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="9ddfc-212">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-212">click **Add attribute**.</span></span> <span data-ttu-id="9ddfc-213">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="9ddfc-214">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-214">Click **Save.**</span></span> <span data-ttu-id="9ddfc-215">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9ddfc-216">Pobieranie metadanych usługi Azure AD hello lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="9ddfc-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="9ddfc-217">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-218">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-219">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-220">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-221">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-222">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ddfc-223">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-224">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-225">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-226">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9ddfc-227">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="9ddfc-228">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="9ddfc-229">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9ddfc-230">Jak tooconfigure federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9ddfc-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9ddfc-231">tooconfigure aplikacji z systemem innym niż galerii, potrzebujesz toohave usługi Azure AD premium oraz aplikacja hello obsługuje SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="9ddfc-232">Aby uzyskać więcej informacji o wersji usługi Azure AD, odwiedź stronę [cennik usługi Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9ddfc-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="9ddfc-233">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="9ddfc-234">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ddfc-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9ddfc-235">Pobieranie metadanych usługi Azure AD i certyfikatów</span><span class="sxs-lookup"><span data-stu-id="9ddfc-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9ddfc-236">Skonfiguruj wartości metadanych usługi Azure AD w aplikacji hello (znak na adres URL, wystawcy, adres URL wylogowania i certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="9ddfc-237">Konfigurowanie aplikacji hello wartości metadanych w usłudze Azure AD (znak na adres URL odpowiedzi adres URL, identyfikator)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="9ddfc-238">tooconfigure logowanie jednokrotne dla aplikacji, która nie znajduje się w galerii Azure AD hello, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-239">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-240">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-241">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-242">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-243">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="9ddfc-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="9ddfc-244">Kliknij przycisk **Non galerii aplikacji** w hello **dodać własną aplikację** sekcji</span><span class="sxs-lookup"><span data-stu-id="9ddfc-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="9ddfc-245">Wprowadź nazwę aplikacji hello hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="9ddfc-246">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="9ddfc-247">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="9ddfc-248">Wybierz **na języku SAML logowania jednokrotnego** w hello **tryb** listy rozwijanej</span><span class="sxs-lookup"><span data-stu-id="9ddfc-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="9ddfc-249">Wprowadź wartości hello wymagane w **domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="9ddfc-250">Te wartości należy uzyskać od dostawcy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="9ddfc-251">Aplikacja hello tooconfigure jako logowanie Jednokrotne zainicjowane przez dostawców tożsamości, wprowadź hello adres URL odpowiedzi i hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="9ddfc-252">**Opcjonalnie:** aplikacji hello tooconfigure jako logowanie Jednokrotne zainicjowane SP, hello znaku w adresie URL jest wymagana wartość.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="9ddfc-253">W hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="9ddfc-254">**Opcjonalnie:** kliknij **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="9ddfc-255">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="9ddfc-256">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-256">click **Add attribute**.</span></span> <span data-ttu-id="9ddfc-257">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="9ddfc-258">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-258">Click **Save.**</span></span> <span data-ttu-id="9ddfc-259">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="9ddfc-260">Kliknij przycisk **Konfiguruj &lt;Nazwa aplikacji&gt;**  tooaccess dokumentacji na temat tooconfigure rejestracji jednokrotnej w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="9ddfc-261">Ponadto ma Azure AD adresy URL i certyfikatu wymaganego dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="9ddfc-262">Wybierz identyfikator użytkownika i dodaj aplikację toohello toobe wysyłane atrybutów użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ddfc-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="9ddfc-263">tooselect hello identyfikator użytkownika lub Dodaj atrybuty użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-264">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-265">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-266">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-267">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-268">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ddfc-269">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-270">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-271">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-272">W obszarze hello **atrybuty użytkownika** zaznacz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="9ddfc-273">Hello zaznaczoną opcję musi mieć wartość oczekiwana hello toomatch użytkownika hello tooauthenticate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="9ddfc-274">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="9ddfc-275">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="9ddfc-276">atrybuty użytkownika tooadd, kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** tooedit hello atrybuty aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="9ddfc-277">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-277">tooadd an attribute:</span></span>

   <span data-ttu-id="9ddfc-278">1. Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-278">1.click **Add attribute**.</span></span> <span data-ttu-id="9ddfc-279">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="9ddfc-280">2 kliknij **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-280">2 Click **Save.**</span></span> <span data-ttu-id="9ddfc-281">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9ddfc-282">Pobieranie metadanych usługi Azure AD hello lub certyfikat</span><span class="sxs-lookup"><span data-stu-id="9ddfc-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="9ddfc-283">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-284">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-285">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-286">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-287">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-288">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="9ddfc-289">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-290">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-291">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-292">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9ddfc-293">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="9ddfc-294">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="9ddfc-295">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9ddfc-296">Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9ddfc-297">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ddfc-298">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="9ddfc-299">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="9ddfc-300">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ddfc-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="9ddfc-301">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-302">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ddfc-303">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-304">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-305">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-306">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="9ddfc-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="9ddfc-307">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** sekcji, nazwa typu hello aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9ddfc-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="9ddfc-308">Wybierz hello aplikację tooconfigure dla rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9ddfc-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="9ddfc-309">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="9ddfc-310">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="9ddfc-311">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="9ddfc-312">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="9ddfc-313">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-314">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-315">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-316">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-317">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-318">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="9ddfc-319">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-320">Wybierz hello aplikację tooconfigure rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9ddfc-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="9ddfc-321">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-322">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9ddfc-323">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="9ddfc-324">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="9ddfc-325">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9ddfc-326">Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9ddfc-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9ddfc-327">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ddfc-328">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9ddfc-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="9ddfc-329">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="9ddfc-330">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9ddfc-330">Add a non-gallery application</span></span>

<span data-ttu-id="9ddfc-331">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-332">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ddfc-333">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-334">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-335">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-336">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="9ddfc-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="9ddfc-337">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="9ddfc-338">Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="9ddfc-339">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-339">Select **Add.**</span></span>

<span data-ttu-id="9ddfc-340">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="9ddfc-341">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9ddfc-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="9ddfc-342">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-343">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ddfc-344">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-345">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-346">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-347">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="9ddfc-348">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-349">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="9ddfc-350">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-351">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9ddfc-352">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="9ddfc-353">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="9ddfc-354">Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="9ddfc-355">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="9ddfc-356">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="9ddfc-357">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="9ddfc-358">Jak tooassign bezpośrednio aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ddfc-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="9ddfc-359">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="9ddfc-360">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9ddfc-361">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9ddfc-362">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ddfc-363">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9ddfc-364">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9ddfc-365">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="9ddfc-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9ddfc-366">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="9ddfc-367">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9ddfc-368">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9ddfc-369">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9ddfc-370">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9ddfc-371">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="9ddfc-372">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="9ddfc-373">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="9ddfc-374">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="9ddfc-375">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="9ddfc-376">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="9ddfc-377">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ddfc-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="9ddfc-378">Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello</span><span class="sxs-lookup"><span data-stu-id="9ddfc-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="9ddfc-379">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="9ddfc-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="9ddfc-380">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="9ddfc-380">Correlation error ID</span></span>

-   <span data-ttu-id="9ddfc-381">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="9ddfc-381">UPN (user email address)</span></span>

-   <span data-ttu-id="9ddfc-382">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="9ddfc-382">TenantID</span></span>

-   <span data-ttu-id="9ddfc-383">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="9ddfc-383">Browser type</span></span>

-   <span data-ttu-id="9ddfc-384">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="9ddfc-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="9ddfc-385">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="9ddfc-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ddfc-386">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ddfc-386">Next steps</span></span>
[<span data-ttu-id="9ddfc-387">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ddfc-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

