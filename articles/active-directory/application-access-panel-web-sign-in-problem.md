---
title: "aaaProblem podpisywania w witrynie internetowej panelu dostępu toohello | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące tootroubleshoot problemy, które można napotkać podczas próby toosign w toouse hello panelu dostępu"
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="1ec90-103">Problem z logowaniem toohello dostępu panelu witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="1ec90-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="1ec90-104">Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="1ec90-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1ec90-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="1ec90-106">Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec90-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="1ec90-107">Użytkownicy może się zalogować w toohello panelu dostępu, jeśli ma konto służbowe w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ec90-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="1ec90-108">Użytkownicy mogą być uwierzytelniane przez usługę Azure AD bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1ec90-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="1ec90-109">Użytkownicy mogą uwierzytelniać za pomocą usługi Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="1ec90-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="1ec90-110">Użytkownicy mogą być uwierzytelniane przez usługę Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1ec90-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="1ec90-111">Jeśli użytkownik ma subskrypcję platformy Azure lub usługi Office 365 i używa hello portalu Azure lub aplikacji pakietu Office 365, aby były toouse można bezproblemowo hello Panel dostępu, bez konieczności toosign w ponownie.</span><span class="sxs-lookup"><span data-stu-id="1ec90-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="1ec90-112">Użytkownicy, którzy nie zostali uwierzytelnieni się zostanie wyświetlony monit o toosign w za pomocą hello nazwę użytkownika i hasło dla swojego konta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ec90-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="1ec90-113">Jeśli hello organizacji skonfigurował federacyjnych, wpisując hello username jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="1ec90-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="1ec90-114">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="1ec90-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="1ec90-115">Upewnij się, że hello użytkownik loguje się toohello **Popraw adres URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="1ec90-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="1ec90-116">Upewnij się, że przeglądarka hello użytkownika został dodany hello tooits adres URL **Zaufane witryny**</span><span class="sxs-lookup"><span data-stu-id="1ec90-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="1ec90-117">Upewnij się, że konto użytkownika hello jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="1ec90-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="1ec90-118">Upewnij się, że konto użytkownika hello jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="1ec90-119">Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="1ec90-120">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ec90-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="1ec90-121">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ec90-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="1ec90-122">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.</span><span class="sxs-lookup"><span data-stu-id="1ec90-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="1ec90-123">Upewnij się, że tooalso spróbuj wyczyszczenie plików cookie w przeglądarce i podjęcie ponownej próby toosign w.</span><span class="sxs-lookup"><span data-stu-id="1ec90-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="1ec90-124">Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="1ec90-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="1ec90-125">Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="1ec90-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="1ec90-126">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="1ec90-127">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1ec90-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="1ec90-128">Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="1ec90-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="1ec90-129">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1ec90-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="1ec90-130">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1ec90-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="1ec90-131">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="1ec90-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="1ec90-132">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1ec90-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="1ec90-133">Problemy z kontem użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="1ec90-133">Problems with hello user’s account</span></span>

<span data-ttu-id="1ec90-134">Powodu tooa problem z kontem użytkownika hello mogą zostać zablokowane toohello dostęp do panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="1ec90-135">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:</span><span class="sxs-lookup"><span data-stu-id="1ec90-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="1ec90-136">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ec90-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="1ec90-137">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="1ec90-138">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="1ec90-139">Włącz samoobsługowe resetowanie haseł</span><span class="sxs-lookup"><span data-stu-id="1ec90-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="1ec90-140">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="1ec90-141">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="1ec90-142">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="1ec90-143">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="1ec90-144">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="1ec90-145">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ec90-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="1ec90-146">toocheck, jeśli konto użytkownika jest obecny, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-147">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-148">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-149">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-150">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-151">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-151">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-152">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-153">Sprawdź właściwości hello hello użytkownika obiektu toobe się upewnić, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1ec90-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="1ec90-154">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-154">Check a user’s account status</span></span>

<span data-ttu-id="1ec90-155">toocheck użytkownika konta stanu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-156">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-157">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-158">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-159">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-160">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-160">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-161">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-162">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-162">click **Profile**.</span></span>

8.  <span data-ttu-id="1ec90-163">W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono zbyt**nr**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="1ec90-164">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-164">Reset a user’s password</span></span>

<span data-ttu-id="1ec90-165">tooreset hasło użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-166">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-167">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-168">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-169">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-170">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-170">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-171">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-172">Kliknij przycisk hello **resetowania hasła** przycisk u góry bloku użytkownika hello hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="1ec90-173">Kliknij przycisk hello **resetowania hasła** przycisk na powitania **resetowania hasła** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="1ec90-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="1ec90-174">Kopiuj hello **hasło tymczasowe** lub **wprowadź nowe hasło** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ec90-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="1ec90-175">Komunikować się z nowym użytkowniku toohello hasła, one toochange wymagane hasło podczas następnego Zaloguj tooAzure usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ec90-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="1ec90-176">Włącz samoobsługowe Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="1ec90-176">Enable self-service password reset</span></span>

<span data-ttu-id="1ec90-177">hasło samoobsługi tooenable resetowania, wykonaj poniższe kroki wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="1ec90-178">Włącz użytkowników tooreset swoich haseł w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ec90-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="1ec90-179">Włącz tooreset użytkowników lub zmieniać swoje hasła lokalnej usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ec90-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="1ec90-180">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="1ec90-181">toocheck użytkownika do usługi Multi-Factor stanu uwierzytelniania, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-182">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-183">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-184">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-185">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-186">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-186">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-187">Kliknij przycisk hello **uwierzytelnianie wieloskładnikowe** u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="1ec90-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="1ec90-188">Raz hello **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, znajdują się na powitania **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="1ec90-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="1ec90-189">Znajdź użytkownika hello hello listy użytkowników przez wyszukiwanie, filtrowanie i sortowanie.</span><span class="sxs-lookup"><span data-stu-id="1ec90-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="1ec90-190">Wybierz hello użytkownika z listy hello użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1ec90-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1ec90-191">Jeśli użytkownik znajduje się w **wymuszone** stanu może ustawić je także**wyłączone** tymczasowo toolet je z powrotem do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="1ec90-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="1ec90-192">Gdy są one ponownie, można zmienić stanu za**włączone** ponownie toorequire je zarejestrować toore, zaloguj się do niego swoje informacje kontaktowe podczas następnego.</span><span class="sxs-lookup"><span data-stu-id="1ec90-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="1ec90-193">Alternatywnie można wykonać kroki hello w hello [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) tooverify lub ustaw dla nich dane.</span><span class="sxs-lookup"><span data-stu-id="1ec90-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="1ec90-194">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="1ec90-195">toocheck uwierzytelniania użytkownika informacje używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania haseł, skontaktuj się z pomocą wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-196">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-197">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-198">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-199">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-200">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-200">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-201">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-202">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-202">click **Profile**.</span></span>

8.  <span data-ttu-id="1ec90-203">Przewiń w dół za**informacje kontaktowe uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="1ec90-204">**Przegląd** hello danych zarejestrowane dla użytkownika hello i aktualizacji, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1ec90-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="1ec90-205">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-205">Check a user’s group memberships</span></span>

<span data-ttu-id="1ec90-206">toocheck użytkownika członkostw, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-207">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-208">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-209">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-210">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-211">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-211">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-212">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-213">Kliknij przycisk **grup** toosee, który grupuje hello użytkownika jest członkiem.</span><span class="sxs-lookup"><span data-stu-id="1ec90-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="1ec90-214">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="1ec90-215">toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-216">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-217">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-218">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-219">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-220">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-220">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-221">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-222">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="1ec90-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="1ec90-223">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="1ec90-223">Assign a user a license</span></span> 

<span data-ttu-id="1ec90-224">tooassign tooa licencji użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ec90-225">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1ec90-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1ec90-226">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ec90-227">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ec90-228">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="1ec90-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1ec90-229">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ec90-229">click **All users**.</span></span>

6.  <span data-ttu-id="1ec90-230">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1ec90-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1ec90-231">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="1ec90-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="1ec90-232">Kliknij przycisk hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ec90-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="1ec90-233">Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="1ec90-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="1ec90-234">**Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów.</span><span class="sxs-lookup"><span data-stu-id="1ec90-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="1ec90-235">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="1ec90-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1ec90-236">Kliknij przycisk hello **przypisać** przycisk tooassign użytkownika toothis tych licencji.</span><span class="sxs-lookup"><span data-stu-id="1ec90-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="1ec90-237">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello</span><span class="sxs-lookup"><span data-stu-id="1ec90-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="1ec90-238">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="1ec90-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="1ec90-239">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="1ec90-239">Correlation error ID</span></span>

-   <span data-ttu-id="1ec90-240">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="1ec90-240">UPN (user email address)</span></span>

-   <span data-ttu-id="1ec90-241">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="1ec90-241">Tenant ID</span></span>

-   <span data-ttu-id="1ec90-242">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="1ec90-242">Browser type</span></span>

-   <span data-ttu-id="1ec90-243">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="1ec90-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1ec90-244">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="1ec90-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ec90-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ec90-245">Next steps</span></span>
[<span data-ttu-id="1ec90-246">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1ec90-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
