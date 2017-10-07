---
title: "Logowanie tooan skonfigurować hasła aplikacji galerii Azure AD aaaProblems logowanie jednokrotne | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono obszarów problemów, które znajdują się wskazówki tootroubleshoot problemów powiązanych toosigning w tooAzure galerii AD skonfigurowaną pod kątem hasło logowania jednokrotnego"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="28990-103">Problemy przy logowaniu tooan galerii Azure AD aplikacji skonfigurowana dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="28990-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="28990-104">Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="28990-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="28990-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="28990-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="28990-106">Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28990-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="28990-107">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="28990-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="28990-108">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="28990-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="28990-109">Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="28990-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="28990-110">Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="28990-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="28990-111">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="28990-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="28990-112">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="28990-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="28990-113">Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="28990-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="28990-114">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="28990-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="28990-115">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="28990-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="28990-116">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="28990-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="28990-117">Witaj opartego na hasłach logowania jednokrotnego rozszerzenie udostępnienie Edge w systemie Windows 10, gdy staną się również obsługiwany rozszerzenia przeglądarki Edge.</span><span class="sxs-lookup"><span data-stu-id="28990-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="28990-118">Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="28990-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="28990-119">hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28990-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="28990-120">Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28990-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="28990-121">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="28990-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="28990-122">Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="28990-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="28990-123">Oparte na przeglądarce można ukierunkowanej toohello łącze.</span><span class="sxs-lookup"><span data-stu-id="28990-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="28990-124">**Dodaj** hello rozszerzenia tooyour przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="28990-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="28990-125">Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="28990-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="28990-126">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="28990-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="28990-127">Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="28990-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="28990-128">Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:</span><span class="sxs-lookup"><span data-stu-id="28990-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="28990-129">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="28990-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="28990-130">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="28990-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="28990-131">Konfigurowanie zasad grupy dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="28990-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="28990-132">Możesz skonfigurować zasady grupy, które pozwalają tooremotely instalacji hello panelu dostępu rozszerzenie programu Internet Explorer na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28990-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="28990-133">wymagania wstępne Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="28990-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="28990-134">Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28990-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="28990-135">Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO).</span><span class="sxs-lookup"><span data-stu-id="28990-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="28990-136">Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="28990-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="28990-137">[Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="28990-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="28990-138">Czynności opisane w samouczku hello [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) instrukcje krok po kroku dotyczące sposobu tooconfigure hello zasad grupy i wdróż je toousers.</span><span class="sxs-lookup"><span data-stu-id="28990-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="28990-139">Rozwiązywanie problemów z hello panelu dostępu w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="28990-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="28990-140">Wykonaj hello [rozwiązywanie hello rozszerzenia Panel dostępu dla programu Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania hello rozszerzenia dla programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="28990-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="28990-141">Jak hasło tooconfigure logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="28990-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="28990-142">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="28990-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="28990-143">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="28990-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="28990-144">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="28990-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="28990-145">Przypisywanie użytkowników toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="28990-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="28990-146">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="28990-146">Add a non-gallery application</span></span>

<span data-ttu-id="28990-147">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28990-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="28990-148">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="28990-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="28990-149">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="28990-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="28990-150">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="28990-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="28990-151">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28990-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="28990-152">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="28990-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="28990-153">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="28990-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="28990-154">Wprowadź nazwę aplikacji hello w hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="28990-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="28990-155">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="28990-155">Select **Add.**</span></span>

<span data-ttu-id="28990-156">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="28990-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="28990-157">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="28990-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="28990-158">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28990-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="28990-159">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="28990-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="28990-160">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="28990-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="28990-161">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="28990-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="28990-162">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28990-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="28990-163">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="28990-164">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="28990-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="28990-165">Wybierz hello aplikację tooconfigure rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="28990-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="28990-166">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="28990-167">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="28990-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="28990-168">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="28990-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="28990-169">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="28990-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="28990-170">Upewnij się, że hello logowania pola są widoczne na powitania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="28990-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="28990-171">Przypisywanie użytkowników toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="28990-172">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="28990-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="28990-173">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="28990-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="28990-174">Przypisywanie użytkowników toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="28990-174">Assign users toohello application</span></span>

<span data-ttu-id="28990-175">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28990-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="28990-176">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="28990-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="28990-177">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="28990-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="28990-178">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="28990-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="28990-179">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28990-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="28990-180">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="28990-181">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="28990-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="28990-182">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28990-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="28990-183">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="28990-184">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="28990-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="28990-185">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="28990-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="28990-186">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="28990-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="28990-187">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="28990-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="28990-188">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="28990-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="28990-189">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="28990-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="28990-190">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28990-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="28990-191">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="28990-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="28990-192">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28990-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="28990-193">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="28990-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="28990-194">Jeśli te kroki rozwiązywania problemów nie hello rozwiązać problem hello</span><span class="sxs-lookup"><span data-stu-id="28990-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="28990-195">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="28990-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="28990-196">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="28990-196">Correlation error ID</span></span>

-   <span data-ttu-id="28990-197">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="28990-197">UPN (user email address)</span></span>

-   <span data-ttu-id="28990-198">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="28990-198">TenantID</span></span>

-   <span data-ttu-id="28990-199">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="28990-199">Browser type</span></span>

-   <span data-ttu-id="28990-200">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="28990-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="28990-201">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="28990-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="28990-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28990-202">Next steps</span></span>
[<span data-ttu-id="28990-203">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="28990-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

