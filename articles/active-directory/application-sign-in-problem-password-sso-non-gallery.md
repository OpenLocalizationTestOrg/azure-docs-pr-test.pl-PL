---
title: "Problemy przy logowaniu do aplikacji Azure AD galerii skonfigurowane hasło logowanie jednokrotne | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono obszarów problemów, które zapewniają wskazówki dotyczące rozwiązywania problemów związanych z rejestrowanie w galerii Azure AD skonfigurowaną pod kątem hasło logowania jednokrotnego"
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="685d7-103">Problemy przy logowaniu do aplikacji Azure AD galerii skonfigurowane dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="685d7-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="685d7-104">Panel dostępu jest widok, a następnie uruchom chmurowych aplikacji, które administrator usługi Azure AD udzielił im dostępu do portalu sieci web, dzięki czemu użytkownik, który ma konto służbowe w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="685d7-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="685d7-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="685d7-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="685d7-106">Panel dostępu jest oddzielony od portalu Azure i nie wymaga użytkownikom posiadania subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="685d7-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="685d7-107">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="685d7-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="685d7-108">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="685d7-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="685d7-109">Spełniające wymagania przeglądarki do panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="685d7-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="685d7-110">Panel dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="685d7-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="685d7-111">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="685d7-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="685d7-112">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="685d7-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="685d7-113">Logowanie Jednokrotne opartego na hasłach można przeglądarki przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="685d7-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="685d7-114">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="685d7-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="685d7-115">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="685d7-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="685d7-116">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="685d7-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="685d7-117">Rozszerzenie logowania jednokrotnego opartego na hasłach stają się dostępne Edge w systemie Windows 10, gdy staną się również obsługiwany rozszerzenia przeglądarki Edge.</span><span class="sxs-lookup"><span data-stu-id="685d7-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="685d7-118">Jak zainstalować rozszerzenie przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="685d7-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="685d7-119">Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="685d7-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="685d7-120">Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="685d7-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="685d7-121">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="685d7-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="685d7-122">W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="685d7-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="685d7-123">Oparte na przeglądarce być kierowane do łącza pobierania.</span><span class="sxs-lookup"><span data-stu-id="685d7-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="685d7-124">**Dodaj** rozszerzenia do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="685d7-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="685d7-125">Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="685d7-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="685d7-126">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="685d7-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="685d7-127">Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="685d7-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="685d7-128">Może również pobrać rozszerzenia dla programu Chrome, a program Firefox z bezpośrednich łączy poniżej:</span><span class="sxs-lookup"><span data-stu-id="685d7-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="685d7-129">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="685d7-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="685d7-130">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="685d7-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="685d7-131">Konfigurowanie zasad grupy dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="685d7-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="685d7-132">Możesz skonfigurować zasady grupy, które umożliwiają zdalnie zainstalować rozszerzenie Panel dostępu dla programu Internet Explorer na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="685d7-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="685d7-133">Wymagania wstępne należą:</span><span class="sxs-lookup"><span data-stu-id="685d7-133">The prerequisites include:</span></span>

-   <span data-ttu-id="685d7-134">Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i dołączeniu komputerów użytkowników do domeny.</span><span class="sxs-lookup"><span data-stu-id="685d7-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="685d7-135">Musi mieć uprawnienie "Edytuj ustawienia" do edycji obiektu zasad grupy (GPO).</span><span class="sxs-lookup"><span data-stu-id="685d7-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="685d7-136">Domyślnie to uprawnienie mają członków z następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="685d7-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="685d7-137">[Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="685d7-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="685d7-138">Czynności opisane w samouczku [wdrażanie rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) instrukcje krok po kroku dotyczące sposobu konfigurowania zasad grupy oraz wdrażanie dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="685d7-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="685d7-139">Rozwiązywanie problemów z panelu dostępu w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="685d7-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="685d7-140">Postępuj zgodnie z [Rozwiązywanie problemów z rozszerzeniem Panel dostępu dla programu Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania rozszerzenia dla programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="685d7-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="685d7-141">Jak skonfigurować hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="685d7-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="685d7-142">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="685d7-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="685d7-143">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="685d7-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="685d7-144">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="685d7-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="685d7-145">Przypisywanie użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="685d7-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="685d7-146">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="685d7-146">Add a non-gallery application</span></span>

<span data-ttu-id="685d7-147">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="685d7-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="685d7-148">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="685d7-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="685d7-149">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="685d7-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="685d7-150">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="685d7-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="685d7-151">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="685d7-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="685d7-152">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="685d7-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="685d7-153">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="685d7-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="685d7-154">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="685d7-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="685d7-155">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="685d7-155">Select **Add.**</span></span>

<span data-ttu-id="685d7-156">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="685d7-157">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="685d7-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="685d7-158">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="685d7-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="685d7-159">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="685d7-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="685d7-160">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="685d7-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="685d7-161">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="685d7-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="685d7-162">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="685d7-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="685d7-163">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="685d7-164">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="685d7-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="685d7-165">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="685d7-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="685d7-166">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="685d7-167">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="685d7-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="685d7-168">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="685d7-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="685d7-169">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="685d7-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="685d7-170">Upewnij się, że logowanie pola są widoczne pod adresem URL.</span><span class="sxs-lookup"><span data-stu-id="685d7-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="685d7-171">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-171">Assign users to the application.</span></span>

11. <span data-ttu-id="685d7-172">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="685d7-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="685d7-173">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="685d7-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="685d7-174">Przypisywanie użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="685d7-174">Assign users to the application</span></span>

<span data-ttu-id="685d7-175">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="685d7-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="685d7-176">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="685d7-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="685d7-177">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="685d7-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="685d7-178">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="685d7-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="685d7-179">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="685d7-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="685d7-180">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="685d7-181">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="685d7-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="685d7-182">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="685d7-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="685d7-183">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="685d7-184">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="685d7-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="685d7-185">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="685d7-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="685d7-186">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="685d7-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="685d7-187">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="685d7-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="685d7-188">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="685d7-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="685d7-189">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="685d7-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="685d7-190">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="685d7-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="685d7-191">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="685d7-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="685d7-192">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="685d7-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="685d7-193">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="685d7-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="685d7-194">Jeśli te kroki rozwiązywania problemów nie Rozwiąż problem</span><span class="sxs-lookup"><span data-stu-id="685d7-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="685d7-195">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="685d7-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="685d7-196">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="685d7-196">Correlation error ID</span></span>

-   <span data-ttu-id="685d7-197">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="685d7-197">UPN (user email address)</span></span>

-   <span data-ttu-id="685d7-198">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="685d7-198">TenantID</span></span>

-   <span data-ttu-id="685d7-199">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="685d7-199">Browser type</span></span>

-   <span data-ttu-id="685d7-200">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="685d7-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="685d7-201">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="685d7-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="685d7-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="685d7-202">Next steps</span></span>
[<span data-ttu-id="685d7-203">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="685d7-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

