---
title: "Problemy przy logowaniu do aplikacji przy użyciu głębokiego łącza | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać problemy dotyczące uzyskiwania dostępu do aplikacji z adres URL głębokiego łącza za pomocą usługi Azure AD"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="9c869-103">Problemy przy logowaniu do aplikacji przy użyciu głębokiego łącza</span><span class="sxs-lookup"><span data-stu-id="9c869-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="9c869-104">Panel dostępu jest oparte na sieci web portalu, która pozwala użytkownikom przy użyciu konta służbowego w usłudze Azure Active Directory (Azure AD) do wyświetlania i uruchamiania aplikacji opartej na chmurze, czy administrator usługi Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="9c869-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="9c869-105">Te aplikacje są skonfigurowane w imieniu użytkownika w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c869-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="9c869-106">Aplikacja musi prawidłowo skonfigurowane i przypisane do użytkownika lub grupy, których użytkownik jest członkiem, aby zobaczyć aplikację w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c869-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="9c869-107">Linków bezpośrednich lub dostęp użytkownika adresy URL są łączy, których użytkownicy mogą uzyskać dostęp do ich rejestracji Jednokrotnej hasła aplikacji bezpośrednio z ich paski adres URL przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9c869-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="9c869-108">Przechodząc do tego łącza, użytkownicy będą automatycznie zalogowaniem się do aplikacji bez konieczności najpierw przejdź do panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c869-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="9c869-109">Jest to tego samego łącza, umożliwiająca użytkownikom dostęp do tych aplikacji z uruchamiający aplikację usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="9c869-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="9c869-110">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="9c869-110">General issues to check first</span></span>

-   <span data-ttu-id="9c869-111">Upewnij się, Twoje przy użyciu **przeglądarki** spełniające minimalne wymagania dotyczące panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c869-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="9c869-112">Upewnij się, że przeglądarka użytkownika został dodany adres URL aplikacji do jego **Zaufane witryny**.</span><span class="sxs-lookup"><span data-stu-id="9c869-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="9c869-113">Upewnij się sprawdzić, aplikacja jest **skonfigurowane** poprawnie.</span><span class="sxs-lookup"><span data-stu-id="9c869-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="9c869-114">Upewnij się, że konto użytkownika jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="9c869-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="9c869-115">Upewnij się, że konto użytkownika jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="9c869-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="9c869-116">Upewnij się, że użytkownika **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="9c869-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="9c869-117">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c869-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="9c869-118">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c869-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="9c869-119">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** jest aktualny, aby umożliwić uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasad, które mają być egzekwowane.</span><span class="sxs-lookup"><span data-stu-id="9c869-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="9c869-120">Upewnij się, że również spróbuj wyczyszczenie plików cookie w przeglądarce, a następnie spróbuj się ponownie zalogować.</span><span class="sxs-lookup"><span data-stu-id="9c869-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="9c869-121">Sprawdzanie głębokiego łącza</span><span class="sxs-lookup"><span data-stu-id="9c869-121">Checking the deeplink</span></span>

<span data-ttu-id="9c869-122">Aby sprawdzić, czy masz poprawne głębokiego łącza, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-123">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9c869-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c869-124">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-125">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-126">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-127">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c869-128">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c869-129">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9c869-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="9c869-130">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c869-131">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="9c869-132">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="9c869-133">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9c869-134">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="9c869-135">Wybierz aplikację, która ma głębokiego łącza do sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="9c869-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="9c869-136">Znajdź etykiety **adres URL dostępu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="9c869-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="9c869-137">Ten adres URL głębokiego łącza można powinna być zgodna.</span><span class="sxs-lookup"><span data-stu-id="9c869-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="9c869-138">Jak zainstalować rozszerzenie przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="9c869-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="9c869-139">Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-140">Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c869-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="9c869-141">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c869-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="9c869-142">W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="9c869-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="9c869-143">Oparte na przeglądarce być kierowane do łącza pobierania.</span><span class="sxs-lookup"><span data-stu-id="9c869-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="9c869-144">**Dodaj** rozszerzenia do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9c869-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="9c869-145">Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="9c869-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="9c869-146">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9c869-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="9c869-147">Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c869-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="9c869-148">Może również pobrać rozszerzenia dla programu Chrome, a program Firefox z bezpośrednich łączy poniżej:</span><span class="sxs-lookup"><span data-stu-id="9c869-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="9c869-149">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="9c869-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="9c869-150">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="9c869-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9c869-151">Jak skonfigurować hasło rejestracji jednokrotnej dla galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c869-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9c869-152">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="9c869-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c869-153">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c869-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="9c869-154">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9c869-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9c869-155">Dodawanie aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c869-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="9c869-156">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-157">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="9c869-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="9c869-158">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-159">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-160">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-161">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c869-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c869-162">W **wprowadź nazwę** pole tekstowe z **Dodaj z galerii** wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="9c869-163">Wybierz aplikację, którą chcesz skonfigurować pod kątem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9c869-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="9c869-164">Przed dodaniem aplikacji, można zmienić jego nazwę z **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9c869-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="9c869-165">Kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9c869-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="9c869-166">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9c869-167">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9c869-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9c869-168">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-169">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9c869-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c869-170">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-171">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-172">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-173">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c869-174">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c869-175">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9c869-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c869-176">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c869-177">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="9c869-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9c869-178">[Przypisywanie użytkowników do aplikacji](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="9c869-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="9c869-179">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9c869-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9c869-180">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="9c869-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9c869-181">Jak skonfigurować hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9c869-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9c869-182">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="9c869-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c869-183">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9c869-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="9c869-184">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9c869-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="9c869-185">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="9c869-185">Add a non-gallery application</span></span>

<span data-ttu-id="9c869-186">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-187">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministrator**.</span><span class="sxs-lookup"><span data-stu-id="9c869-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="9c869-188">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-189">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-190">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-191">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c869-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c869-192">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="9c869-193">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9c869-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="9c869-194">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="9c869-194">Select **Add.**</span></span>

<span data-ttu-id="9c869-195">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9c869-196">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9c869-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9c869-197">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-198">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="9c869-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c869-199">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-200">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-201">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-202">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="9c869-203">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c869-204">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9c869-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c869-205">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c869-206">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="9c869-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9c869-207">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="9c869-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="9c869-208">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="9c869-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="9c869-209">Upewnij się, że logowanie pola są widoczne pod adresem URL.</span><span class="sxs-lookup"><span data-stu-id="9c869-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="9c869-210">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-210">Assign users to the application.</span></span>

11. <span data-ttu-id="9c869-211">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9c869-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9c869-212">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="9c869-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="9c869-213">Jak przypisać użytkownika bezpośrednio do aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c869-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="9c869-214">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c869-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9c869-215">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="9c869-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c869-216">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9c869-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c869-217">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9c869-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c869-218">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c869-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c869-219">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c869-220">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9c869-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c869-221">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="9c869-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9c869-222">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c869-223">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c869-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9c869-224">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9c869-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9c869-225">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9c869-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9c869-226">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="9c869-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9c869-227">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9c869-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9c869-228">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9c869-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9c869-229">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c869-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9c869-230">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="9c869-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9c869-231">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9c869-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9c869-232">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c869-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="9c869-233">Jeśli te kroki rozwiązywania problemów nie nie Rozwiąż problem.</span><span class="sxs-lookup"><span data-stu-id="9c869-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="9c869-234">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="9c869-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="9c869-235">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="9c869-235">Correlation error ID</span></span>

-   <span data-ttu-id="9c869-236">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="9c869-236">UPN (user email address)</span></span>

-   <span data-ttu-id="9c869-237">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="9c869-237">TenantID</span></span>

-   <span data-ttu-id="9c869-238">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="9c869-238">Browser type</span></span>

-   <span data-ttu-id="9c869-239">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="9c869-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="9c869-240">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="9c869-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c869-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c869-241">Next steps</span></span>
[<span data-ttu-id="9c869-242">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c869-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
