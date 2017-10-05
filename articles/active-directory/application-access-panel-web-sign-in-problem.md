---
title: "Problem z logowaniem do panelu dostępu do witryny sieci Web | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące rozwiązywania problemów, które można napotkać podczas próby rejestrowania się do panelu dostępu"
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
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="93630-103">Problem z logowaniem do panelu dostępu do witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="93630-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="93630-104">Panel dostępu jest widok, a następnie uruchom chmurowych aplikacji, które administrator usługi Azure AD udzielił im dostępu do portalu sieci web, dzięki czemu użytkownik, który ma konto służbowe w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93630-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="93630-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="93630-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="93630-106">Panel dostępu jest oddzielony od portalu Azure i nie wymaga użytkownikom posiadania subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93630-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="93630-107">Użytkownicy mogą Zaloguj się do panelu dostępu jeśli ma konto służbowe w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93630-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="93630-108">Użytkownicy mogą być uwierzytelniane przez usługę Azure AD bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="93630-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="93630-109">Użytkownicy mogą uwierzytelniać za pomocą usługi Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="93630-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="93630-110">Użytkownicy mogą być uwierzytelniane przez usługę Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="93630-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="93630-111">Jeśli użytkownik ma subskrypcję platformy Azure lub usługi Office 365 i korzysta z portalu Azure lub aplikacji usługi Office 365, będzie mógł używać panelu dostępu bezproblemowo bez konieczności ponownego logowania się.</span><span class="sxs-lookup"><span data-stu-id="93630-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="93630-112">Użytkownicy, którzy nie zostali uwierzytelnieni monit logowania przy użyciu nazwy użytkownika i hasło dla swojego konta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93630-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="93630-113">Jeśli organizacja ma skonfigurowany federacyjnego, wpisując nazwę użytkownika jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="93630-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="93630-114">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="93630-114">General issues to check first</span></span> 

-   <span data-ttu-id="93630-115">Upewnij się, że użytkownik loguje się do **Popraw adres URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="93630-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="93630-116">Upewnij się, że przeglądarka użytkownika został dodany adres URL do jego **Zaufane witryny**</span><span class="sxs-lookup"><span data-stu-id="93630-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="93630-117">Upewnij się, że konto użytkownika jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="93630-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="93630-118">Upewnij się, że konto użytkownika jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="93630-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="93630-119">Upewnij się, że użytkownika **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="93630-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="93630-120">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="93630-121">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="93630-122">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** jest aktualny, aby umożliwić uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasad, które mają być egzekwowane.</span><span class="sxs-lookup"><span data-stu-id="93630-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="93630-123">Upewnij się, że również spróbuj wyczyszczenie plików cookie w przeglądarce, a następnie spróbuj się ponownie zalogować.</span><span class="sxs-lookup"><span data-stu-id="93630-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="93630-124">Spełniające wymagania przeglądarki do panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="93630-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="93630-125">Panel dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="93630-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="93630-126">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="93630-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="93630-127">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="93630-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="93630-128">Logowanie Jednokrotne opartego na hasłach można przeglądarki przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="93630-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="93630-129">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="93630-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="93630-130">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="93630-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="93630-131">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="93630-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="93630-132">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="93630-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="93630-133">Problemy z kontem użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-133">Problems with the user’s account</span></span>

<span data-ttu-id="93630-134">Dostęp do panelu dostępu mogą zostać zablokowane z powodu problemu z kontem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="93630-135">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:</span><span class="sxs-lookup"><span data-stu-id="93630-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="93630-136">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93630-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="93630-137">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="93630-138">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="93630-139">Włącz samoobsługowe resetowanie haseł</span><span class="sxs-lookup"><span data-stu-id="93630-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="93630-140">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="93630-141">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="93630-142">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="93630-143">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="93630-144">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="93630-145">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93630-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="93630-146">Aby sprawdzić, czy konto użytkownika jest obecne, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-147">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-148">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-149">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-150">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-151">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-151">click **All users**.</span></span>

6.  <span data-ttu-id="93630-152">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-153">Sprawdź właściwości obiektu użytkownika, należy upewnić się, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="93630-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="93630-154">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-154">Check a user’s account status</span></span>

<span data-ttu-id="93630-155">Aby sprawdzić stan konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-156">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-157">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-158">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-159">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-160">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-160">click **All users**.</span></span>

6.  <span data-ttu-id="93630-161">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-162">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="93630-162">click **Profile**.</span></span>

8.  <span data-ttu-id="93630-163">W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono **nr**.</span><span class="sxs-lookup"><span data-stu-id="93630-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="93630-164">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-164">Reset a user’s password</span></span>

<span data-ttu-id="93630-165">Aby zresetować hasło użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-166">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-167">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-168">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-169">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-170">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-170">click **All users**.</span></span>

6.  <span data-ttu-id="93630-171">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-172">Kliknij przycisk **resetowania hasła** na górze bloku użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="93630-173">Kliknij przycisk **resetowania hasła** znajdującego się na **resetowania hasła** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="93630-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="93630-174">Kopiuj **hasło tymczasowe** lub **wprowadź nowe hasło** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="93630-175">Komunikować się z tego nowego hasła dla użytkownika, konieczności zmianę hasła podczas kolejnego logowania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="93630-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="93630-176">Włącz samoobsługowe Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="93630-176">Enable self-service password reset</span></span>

<span data-ttu-id="93630-177">Aby włączyć samoobsługowe Resetowanie hasła, wykonaj poniższe kroki wdrażania:</span><span class="sxs-lookup"><span data-stu-id="93630-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="93630-178">Umożliwianie użytkownikom resetowania swoich haseł w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93630-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="93630-179">Umożliwianie użytkownikom resetowania lub zmieniania swoich haseł lokalnej usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="93630-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="93630-180">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="93630-181">Aby sprawdzić stan usługi Multi-Factor authentication użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-182">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-183">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-184">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-185">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-186">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-186">click **All users**.</span></span>

6.  <span data-ttu-id="93630-187">Kliknij przycisk **uwierzytelnianie wieloskładnikowe** u góry bloku.</span><span class="sxs-lookup"><span data-stu-id="93630-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="93630-188">Raz **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, czy na **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="93630-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="93630-189">Znajdź użytkownika, na liście użytkowników przez wyszukiwanie, filtrowanie i sortowanie.</span><span class="sxs-lookup"><span data-stu-id="93630-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="93630-190">Wybierz użytkownika z listy użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="93630-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="93630-191">Jeśli użytkownik znajduje się w **wymuszone** stanu, użytkownik może ustawić ich **wyłączone** tymczasowo w celu umożliwienia im wrócić do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="93630-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="93630-192">Gdy są one ponownie, można zmienić ich stan, aby **włączone** ponownie, aby wymagały ponownie zarejestrować swoje informacje kontaktowe podczas ich następnego logowania.</span><span class="sxs-lookup"><span data-stu-id="93630-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="93630-193">Alternatywnie możesz wykonać kroki opisane w [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) Sprawdź lub ustaw dla nich dane.</span><span class="sxs-lookup"><span data-stu-id="93630-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="93630-194">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="93630-195">Aby sprawdzić informacje kontaktowe uwierzytelniania użytkownika używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania hasła, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-196">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-197">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-198">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-199">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-200">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-200">click **All users**.</span></span>

6.  <span data-ttu-id="93630-201">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-202">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="93630-202">click **Profile**.</span></span>

8.  <span data-ttu-id="93630-203">Przewiń w dół do **informacje kontaktowe uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="93630-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="93630-204">**Przegląd** danych zarejestrowanych dla użytkowników i aktualizacji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="93630-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="93630-205">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-205">Check a user’s group memberships</span></span>

<span data-ttu-id="93630-206">Aby sprawdzić członkostwa w grupach użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-207">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-208">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-209">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-210">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-211">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-211">click **All users**.</span></span>

6.  <span data-ttu-id="93630-212">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-213">Kliknij przycisk **grup** Aby wyświetlić grupy, które użytkownik jest członkiem.</span><span class="sxs-lookup"><span data-stu-id="93630-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="93630-214">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="93630-215">Aby sprawdzić przypisane licencje użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-216">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-217">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-218">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-219">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-220">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-220">click **All users**.</span></span>

6.  <span data-ttu-id="93630-221">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-222">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="93630-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="93630-223">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="93630-223">Assign a user a license</span></span> 

<span data-ttu-id="93630-224">Aby przypisać licencję do użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93630-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="93630-225">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="93630-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93630-226">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93630-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93630-227">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="93630-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93630-228">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="93630-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93630-229">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="93630-229">click **All users**.</span></span>

6.  <span data-ttu-id="93630-230">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="93630-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93630-231">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="93630-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="93630-232">Kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="93630-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="93630-233">Wybierz **jeden lub więcej produktów** z listy dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="93630-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="93630-234">**Opcjonalne** kliknij **opcje przydziału** element, aby przypisać częściami produktów.</span><span class="sxs-lookup"><span data-stu-id="93630-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="93630-235">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="93630-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="93630-236">Kliknij przycisk **przypisać** przycisk, aby przypisać licencje do tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93630-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="93630-237">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu</span><span class="sxs-lookup"><span data-stu-id="93630-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="93630-238">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="93630-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="93630-239">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="93630-239">Correlation error ID</span></span>

-   <span data-ttu-id="93630-240">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="93630-240">UPN (user email address)</span></span>

-   <span data-ttu-id="93630-241">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="93630-241">Tenant ID</span></span>

-   <span data-ttu-id="93630-242">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="93630-242">Browser type</span></span>

-   <span data-ttu-id="93630-243">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="93630-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="93630-244">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="93630-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="93630-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93630-245">Next steps</span></span>
[<span data-ttu-id="93630-246">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="93630-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
