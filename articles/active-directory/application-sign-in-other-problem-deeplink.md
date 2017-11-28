---
title: "Logowanie przy użyciu głębokiego łącza aplikacji tooan aaaProblems | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy dotyczące uzyskiwania dostępu do aplikacji z adres URL głębokiego łącza za pomocą usługi Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="1700d-103">Problemy przy logowaniu tooan aplikacji przy użyciu głębokiego łącza</span><span class="sxs-lookup"><span data-stu-id="1700d-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="1700d-104">Hello Panel dostępu jest oparte na sieci web portalu, który umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory (Azure AD) tooview i rozpocząć aplikacje oparte na chmurze tego hello administratora usługi Azure AD ma udzielić dostępu do.</span><span class="sxs-lookup"><span data-stu-id="1700d-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="1700d-105">Te aplikacje są skonfigurowane w imieniu użytkownika hello w portalu usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="1700d-106">Aplikacja Hello musi być prawidłowo skonfigurowane i przypisane toohello użytkownika lub grupy hello użytkownika jest członkiem grupy aplikacji hello toosee w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1700d-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="1700d-107">Linków bezpośrednich lub dostęp użytkownika adresy URL są łącza, które użytkownicy mogą korzystać tooaccess ich rejestracji Jednokrotnej hasła aplikacji bezpośrednio ze swojego adresu URL przeglądarek pasków.</span><span class="sxs-lookup"><span data-stu-id="1700d-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="1700d-108">Przechodząc toothis łącza, użytkownicy będą automatycznie zalogowaniem się do aplikacji hello bez toohello toogo panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1700d-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="1700d-109">Jest to hello tego samego łącza, czy użytkownicy przy użyciu tooaccess tych aplikacji z uruchamianie aplikacji hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="1700d-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="1700d-110">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="1700d-110">General issues toocheck first</span></span>

-   <span data-ttu-id="1700d-111">Upewnij się, Twoje przy użyciu **przeglądarki** który spełnia wymagania minimalne hello hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1700d-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="1700d-112">Upewnij się, że przeglądarka hello użytkownika został dodany adres URL hello tooits aplikacji hello **Zaufane witryny**.</span><span class="sxs-lookup"><span data-stu-id="1700d-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="1700d-113">Upewnij się, że aplikacja hello toocheck **skonfigurowane** poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1700d-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="1700d-114">Upewnij się, że konto użytkownika hello jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="1700d-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="1700d-115">Upewnij się, że konto użytkownika hello jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="1700d-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="1700d-116">Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="1700d-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="1700d-117">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1700d-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="1700d-118">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1700d-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="1700d-119">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.</span><span class="sxs-lookup"><span data-stu-id="1700d-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="1700d-120">Upewnij się, że tooalso spróbuj wyczyszczenie plików cookie w przeglądarce i podjęcie ponownej próby toosign w.</span><span class="sxs-lookup"><span data-stu-id="1700d-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="1700d-121">Sprawdzanie, czy hello głębokiego łącza.</span><span class="sxs-lookup"><span data-stu-id="1700d-121">Checking hello deeplink</span></span>

<span data-ttu-id="1700d-122">toocheck, jeśli masz poprawne głębokiego łącza hello, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-123">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1700d-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1700d-124">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-125">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-126">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-127">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1700d-128">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1700d-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1700d-129">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1700d-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="1700d-130">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="1700d-131">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="1700d-132">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="1700d-133">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1700d-134">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1700d-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="1700d-135">Wybierz hello aplikacji hello głębokiego łącza hello wyboru dla.</span><span class="sxs-lookup"><span data-stu-id="1700d-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="1700d-136">Znajdź etykietę hello **adres URL dostępu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1700d-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="1700d-137">Ten adres URL głębokiego łącza można powinna być zgodna.</span><span class="sxs-lookup"><span data-stu-id="1700d-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="1700d-138">Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="1700d-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="1700d-139">hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-140">Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1700d-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="1700d-141">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1700d-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="1700d-142">Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="1700d-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="1700d-143">Oparte na przeglądarce można ukierunkowanej toohello łącze.</span><span class="sxs-lookup"><span data-stu-id="1700d-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="1700d-144">**Dodaj** hello rozszerzenia tooyour przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1700d-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="1700d-145">Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1700d-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="1700d-146">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1700d-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="1700d-147">Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="1700d-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="1700d-148">Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="1700d-149">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="1700d-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="1700d-150">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="1700d-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1700d-151">Jak hasło tooconfigure logowanie jednokrotne dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1700d-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1700d-152">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="1700d-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1700d-153">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="1700d-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="1700d-154">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1700d-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="1700d-155">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="1700d-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="1700d-156">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-157">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="1700d-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="1700d-158">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-159">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-160">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-161">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="1700d-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1700d-162">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** , nazwa typu hello aplikacji hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="1700d-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="1700d-163">Wybierz aplikację hello ma tooconfigure dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1700d-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="1700d-164">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1700d-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="1700d-165">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="1700d-166">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="1700d-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="1700d-167">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1700d-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="1700d-168">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-169">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1700d-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1700d-170">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-171">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-172">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-173">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1700d-174">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1700d-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1700d-175">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1700d-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1700d-176">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1700d-177">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="1700d-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1700d-178">[Przypisywanie użytkowników aplikacji toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="1700d-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="1700d-179">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="1700d-180">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="1700d-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1700d-181">Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="1700d-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1700d-182">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="1700d-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1700d-183">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="1700d-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="1700d-184">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1700d-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="1700d-185">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="1700d-185">Add a non-gallery application</span></span>

<span data-ttu-id="1700d-186">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-187">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="1700d-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="1700d-188">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-189">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-190">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-191">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="1700d-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1700d-192">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="1700d-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="1700d-193">Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1700d-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="1700d-194">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="1700d-194">Select **Add.**</span></span>

<span data-ttu-id="1700d-195">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="1700d-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="1700d-196">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1700d-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="1700d-197">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-198">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1700d-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1700d-199">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-200">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-201">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-202">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="1700d-203">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1700d-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1700d-204">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1700d-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1700d-205">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1700d-206">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="1700d-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1700d-207">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="1700d-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="1700d-208">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="1700d-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="1700d-209">Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1700d-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="1700d-210">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="1700d-211">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="1700d-212">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="1700d-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="1700d-213">Jak tooassign bezpośrednio aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="1700d-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="1700d-214">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1700d-215">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1700d-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1700d-216">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1700d-217">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1700d-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1700d-218">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1700d-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1700d-219">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1700d-220">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1700d-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1700d-221">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1700d-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1700d-222">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1700d-223">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="1700d-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1700d-224">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="1700d-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1700d-225">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1700d-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1700d-226">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="1700d-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1700d-227">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="1700d-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1700d-228">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="1700d-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="1700d-229">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1700d-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1700d-230">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="1700d-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="1700d-231">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1700d-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="1700d-232">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1700d-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="1700d-233">Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="1700d-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="1700d-234">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="1700d-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="1700d-235">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="1700d-235">Correlation error ID</span></span>

-   <span data-ttu-id="1700d-236">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="1700d-236">UPN (user email address)</span></span>

-   <span data-ttu-id="1700d-237">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="1700d-237">TenantID</span></span>

-   <span data-ttu-id="1700d-238">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="1700d-238">Browser type</span></span>

-   <span data-ttu-id="1700d-239">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="1700d-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1700d-240">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="1700d-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1700d-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1700d-241">Next steps</span></span>
[<span data-ttu-id="1700d-242">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1700d-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
