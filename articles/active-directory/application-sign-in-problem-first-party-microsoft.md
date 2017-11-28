---
title: aaaProblems logowanie tooa aplikacji firmy Microsoft | Dokumentacja firmy Microsoft
description: "Rozwiązywanie typowych problemów, które muszą ponieść przy logowaniu się w toofirst firmy Microsoft Applications przy użyciu usługi Azure AD (takich jak usługi Office 365)"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="59506-103">Problemy przy logowaniu tooa aplikacji firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="59506-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="59506-104">Microsoft Applications (takich jak Office 365 Exchange, SharePoint, Yammer itp.) są przypisane i zarządzane nieco inaczej niż 3 aplikacji SaaS innych producentów i inne aplikacje, które integracji z usługą Azure AD na logowanie jednokrotne w.</span><span class="sxs-lookup"><span data-stu-id="59506-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="59506-105">Istnieją trzy sposoby, które użytkownik może uzyskać dostęp tooa firma Microsoft opublikowała aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="59506-106">W przypadku aplikacji hello usługi Office 365 lub innych mechanizmów płatną użytkownicy uzyskują dostęp za pośrednictwem **przypisania licencji** albo bezpośrednio tootheir konta użytkownika, a lub za pośrednictwem grupy za pomocą naszych możliwość przypisania na podstawie grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="59506-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="59506-107">W przypadku aplikacji czy firmy Microsoft lub stron trzecich publikuje za darmo dla każdego toouse użytkownicy mogą otrzymać dostęp za pośrednictwem **zgody użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="59506-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="59506-108">This0 oznacza Zaloguj toohello aplikacji przy użyciu swojego konta usługi Azure AD pracy lub nauki i umożliwić jego toohave dostępu toosome ograniczony zestaw danych na koncie.</span><span class="sxs-lookup"><span data-stu-id="59506-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="59506-109">W przypadku aplikacji czy firmy Microsoft lub 3rd Strona publikuje za darmo dla każdego toouse użytkownicy mogą również uzyskać dostęp za pośrednictwem **zgody administratora**.</span><span class="sxs-lookup"><span data-stu-id="59506-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="59506-110">Oznacza to, że administrator wykrył, że aplikacja hello mogą być używane przez wszyscy użytkownicy w organizacji hello, zaloguj się w aplikacji toohello przy użyciu konta administratora globalnego i przyznać dostęp tooeveryone w organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="59506-111">tootroubleshoot problemu, rozpoczyna się od hello [ogólne obszarów problemów z tooconsider dostęp do aplikacji](#general-problem-areas-with-application-access-to-consider) , a następnie odczytywane hello [wskazówki: tootroubleshoot kroki Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget hello uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="59506-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="59506-112">Ogólne obszarów problemów z tooconsider dostęp do aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="59506-113">Poniżej znajduje się lista hello obszarów problemów ogólne, które można wejść do, jeśli masz informacje o tym, gdzie toostart, ale firma Microsoft zaleca się przeczytanie tooget wskazówki hello szybkie przechodzenie: [wskazówki: tootroubleshoot kroki Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="59506-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="59506-114">Problemy z kontem użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="59506-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="59506-115">Problemy z grupy</span><span class="sxs-lookup"><span data-stu-id="59506-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="59506-116">Problemy z zasadami dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="59506-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="59506-117">Problemy z zgody aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="59506-118">Kroki tootroubleshoot Microsoft Application dostępu</span><span class="sxs-lookup"><span data-stu-id="59506-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="59506-119">Poniżej są niektóre typowe problemy pracowników wystąpiły podczas ich nie logowania tooa aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="59506-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="59506-120">Ogólne problemy toocheck najpierw</span><span class="sxs-lookup"><span data-stu-id="59506-120">General issues toocheck first</span></span>

  * <span data-ttu-id="59506-121">Upewnij się, że hello użytkownik loguje się toohello **Popraw adres URL** , a nie adres URL lokalnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="59506-122">Upewnij się, że konto użytkownika hello jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="59506-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="59506-123">Upewnij się, że hello **konto użytkownika istnieje** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59506-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="59506-124">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59506-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="59506-125">Upewnij się, że konto użytkownika hello jest **włączone** dla logowania. [Sprawdź stan konta użytkownika](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="59506-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="59506-126">Upewnij się, że użytkownik hello **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="59506-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="59506-127">[Resetuj hasło użytkownika](#reset-a-users-password) lub [włączyć samoobsługowe Resetowanie hasła](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="59506-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="59506-128">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59506-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="59506-129">[Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="59506-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="59506-130">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59506-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="59506-131">[Sprawdź zasady dostępu warunkowego określonych](#problems-with-conditional-access-policies) lub [Sprawdź zasady dostępu warunkowego określonej aplikacji](#check-a-specific-applications-conditional-access-policy) lub [zasad dostępu warunkowego określonych wyłączone](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="59506-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="59506-132">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** działa toodate tooallow uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasady toobe wymuszane.</span><span class="sxs-lookup"><span data-stu-id="59506-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="59506-133">[Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="59506-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="59506-134">Aby uzyskać **Microsoft** **aplikacje, które wymagają licencji** (takich jak usługi Office 365), poniżej przedstawiono niektóre toocheck określonych problemów po zostały wykluczone powyższe problemy ogólne hello:</span><span class="sxs-lookup"><span data-stu-id="59506-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="59506-135">Upewnij się, hello użytkownika lub ma **przypisanej licencji.**</span><span class="sxs-lookup"><span data-stu-id="59506-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="59506-136">[Sprawdź przypisane licencje użytkownika](#check-a-users-assigned-licenses) lub [Sprawdź grupy przypisane licencje.](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="59506-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="59506-137">Jeśli jest licencja hello **przypisane tooa** **Grupa statyczna**, upewnij się, że hello **użytkownik jest członkiem** tej grupy.</span><span class="sxs-lookup"><span data-stu-id="59506-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="59506-138">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="59506-139">W przypadku licencji hello **przypisane tooa** **Dynamiczna grupa**, upewnij się, że hello **grupa dynamiczna reguła została poprawnie ustawiona**.</span><span class="sxs-lookup"><span data-stu-id="59506-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="59506-140">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="59506-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="59506-141">Jeśli licencja hello jest **przypisane tooa** **Dynamiczna grupa**, upewnij się, że hello grupa dynamiczna ma **zakończyło się przetwarzanie** członkostwa i że hello **jest użytkownik element członkowski** (może to zająć pewien czas).</span><span class="sxs-lookup"><span data-stu-id="59506-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="59506-142">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="59506-143">Po wprowadzeniu się licencji hello jest przypisany, upewnij się, że licencja hello jest **niewygasły**.</span><span class="sxs-lookup"><span data-stu-id="59506-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="59506-144">Upewnij się, że licencja hello jest **dla aplikacji hello** uzyskują oni dostęp.</span><span class="sxs-lookup"><span data-stu-id="59506-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="59506-145">Dla **Microsoft** **aplikacje, które nie wymagają licencji**, w tym miejscu są inne toocheck rzeczy:</span><span class="sxs-lookup"><span data-stu-id="59506-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="59506-146">Jeśli aplikacja hello żąda **uprawnienia na poziomie użytkownika** (na przykład "dostęp do skrzynek pocztowych użytkowników"), upewnij się, że ten użytkownik hello zalogował się toohello aplikacji i wykonał **operacji zgody na poziomie użytkownika**  aplikacja hello toolet dostęp do swoich danych.</span><span class="sxs-lookup"><span data-stu-id="59506-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="59506-147">Jeśli aplikacja hello żąda **uprawnień na poziomie administratora** (na przykład "dostęp do skrzynek pocztowych wszystkich użytkowników"), upewnij się, że przeprowadził administratora globalnego **operacja zgody na poziomie administratora imieniu wszyscy użytkownicy** hello organizacji.</span><span class="sxs-lookup"><span data-stu-id="59506-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="59506-148">Problemy z kontem użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="59506-148">Problems with hello user’s account</span></span>

<span data-ttu-id="59506-149">Dostęp do aplikacji mogą zostać zablokowane powodu tooa problem z użytkownika, który jest przypisany toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="59506-150">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:</span><span class="sxs-lookup"><span data-stu-id="59506-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="59506-151">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59506-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="59506-152">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="59506-153">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="59506-154">Włącz samoobsługowe resetowanie haseł</span><span class="sxs-lookup"><span data-stu-id="59506-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="59506-155">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="59506-156">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="59506-157">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="59506-158">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="59506-159">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="59506-160">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59506-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="59506-161">toocheck, jeśli konto użytkownika jest obecny, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-162">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-163">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-164">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-165">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-166">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-166">click **All users**.</span></span>

6.  <span data-ttu-id="59506-167">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-168">Sprawdź właściwości hello hello użytkownika obiektu toobe się upewnić, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="59506-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="59506-169">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-169">Check a user’s account status</span></span>

<span data-ttu-id="59506-170">toocheck użytkownika konta stanu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-171">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-172">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-173">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-174">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-175">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-175">click **All users**.</span></span>

6.  <span data-ttu-id="59506-176">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-177">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="59506-177">click **Profile**.</span></span>

8.  <span data-ttu-id="59506-178">W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono zbyt**nr**.</span><span class="sxs-lookup"><span data-stu-id="59506-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="59506-179">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-179">Reset a user’s password</span></span>

<span data-ttu-id="59506-180">tooreset hasło użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-181">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-182">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-183">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-184">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-185">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-185">click **All users**.</span></span>

6.  <span data-ttu-id="59506-186">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-187">Kliknij przycisk hello **resetowania hasła** przycisk u góry bloku użytkownika hello hello.</span><span class="sxs-lookup"><span data-stu-id="59506-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="59506-188">Kliknij przycisk hello **resetowania hasła** przycisk na powitania **resetowania hasła** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="59506-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="59506-189">Kopiuj hello **hasło tymczasowe** lub **wprowadź nowe hasło** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59506-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="59506-190">Komunikować się z nowym użytkowniku toohello hasła, one toochange wymagane hasło podczas następnego Zaloguj tooAzure usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59506-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="59506-191">Włącz samoobsługowe Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="59506-191">Enable self-service password reset</span></span>

<span data-ttu-id="59506-192">hasło samoobsługi tooenable resetowania, wykonaj poniższe kroki wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="59506-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="59506-193">Włącz użytkowników tooreset swoich haseł w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59506-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="59506-194">Włącz tooreset użytkowników lub zmieniać swoje hasła lokalnej usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="59506-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="59506-195">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="59506-196">toocheck użytkownika do usługi Multi-Factor stanu uwierzytelniania, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-197">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-198">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-199">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-200">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-201">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-201">click **All users**.</span></span>

6.  <span data-ttu-id="59506-202">Kliknij przycisk hello **uwierzytelnianie wieloskładnikowe** u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="59506-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="59506-203">Raz hello **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, znajdują się na powitania **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="59506-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="59506-204">Znajdź użytkownika hello hello listy użytkowników przez wyszukiwanie, filtrowanie i sortowanie.</span><span class="sxs-lookup"><span data-stu-id="59506-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="59506-205">Wybierz hello użytkownika z listy hello użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="59506-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="59506-206">**Uwaga**: Jeśli użytkownik znajduje się w **wymuszone** stanu może ustawić je także**wyłączone** tymczasowo toolet je z powrotem do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="59506-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="59506-207">Gdy są one ponownie, można zmienić stanu za**włączone** ponownie toorequire je zarejestrować toore, zaloguj się do niego swoje informacje kontaktowe podczas następnego.</span><span class="sxs-lookup"><span data-stu-id="59506-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="59506-208">Alternatywnie można wykonać kroki hello w hello [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) tooverify lub ustaw dla nich dane.</span><span class="sxs-lookup"><span data-stu-id="59506-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="59506-209">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="59506-210">toocheck uwierzytelniania użytkownika informacje używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania haseł, skontaktuj się z pomocą wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-211">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-212">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-213">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-214">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-215">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-215">click **All users**.</span></span>

6.  <span data-ttu-id="59506-216">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-217">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="59506-217">click **Profile**.</span></span>

8.  <span data-ttu-id="59506-218">Przewiń w dół za**informacje kontaktowe uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="59506-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="59506-219">**Przegląd** hello danych zarejestrowane dla użytkownika hello i aktualizacji, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="59506-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="59506-220">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-220">Check a user’s group memberships</span></span>

<span data-ttu-id="59506-221">toocheck użytkownika członkostw, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-222">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-223">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-224">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-225">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-226">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-226">click **All users**.</span></span>

6.  <span data-ttu-id="59506-227">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-228">Kliknij przycisk **grup** toosee, który grupuje hello użytkownika jest członkiem.</span><span class="sxs-lookup"><span data-stu-id="59506-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="59506-229">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="59506-230">toocheck użytkownika przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-231">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-232">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-233">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-234">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-235">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-235">click **All users**.</span></span>

6.  <span data-ttu-id="59506-236">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-237">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="59506-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="59506-238">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-238">Assign a user a license</span></span> 

<span data-ttu-id="59506-239">tooassign tooa licencji użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-240">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-241">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-242">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-243">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-244">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59506-244">click **All users**.</span></span>

6.  <span data-ttu-id="59506-245">**Wyszukiwanie** dla użytkownika hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-246">Kliknij przycisk **licencji** toosee, w którym użytkownik hello licencji obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="59506-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="59506-247">Kliknij przycisk hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59506-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="59506-248">Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="59506-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="59506-249">**Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów.</span><span class="sxs-lookup"><span data-stu-id="59506-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="59506-250">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="59506-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="59506-251">Kliknij przycisk hello **przypisać** przycisk tooassign użytkownika toothis tych licencji.</span><span class="sxs-lookup"><span data-stu-id="59506-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="59506-252">Problemy z grupy</span><span class="sxs-lookup"><span data-stu-id="59506-252">Problems with groups</span></span>

<span data-ttu-id="59506-253">Dostęp do aplikacji mogą zostać zablokowane powodu tooa problem z grupy, która jest przypisany toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="59506-254">Poniżej przedstawiono kilka sposobów, można rozwiązać i rozwiązać problemy z grupy i członkostwa w grupach:</span><span class="sxs-lookup"><span data-stu-id="59506-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="59506-255">Sprawdź członkostwo w grupie</span><span class="sxs-lookup"><span data-stu-id="59506-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="59506-256">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="59506-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="59506-257">Sprawdź grupy przypisane licencje.</span><span class="sxs-lookup"><span data-stu-id="59506-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="59506-258">Ponownie przetworzyć grupy licencji</span><span class="sxs-lookup"><span data-stu-id="59506-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="59506-259">Przypisz grupę licencji</span><span class="sxs-lookup"><span data-stu-id="59506-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="59506-260">Sprawdź członkostwo w grupie</span><span class="sxs-lookup"><span data-stu-id="59506-260">Check a group’s membership</span></span>

<span data-ttu-id="59506-261">toocheck członkostwa w grupie, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-262">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-263">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-264">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-265">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-266">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="59506-266">click **All groups**.</span></span>

6.  <span data-ttu-id="59506-267">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-268">Kliknij przycisk **członków** tooreview hello listę użytkowników przypisane toothis grupy.</span><span class="sxs-lookup"><span data-stu-id="59506-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="59506-269">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="59506-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="59506-270">toocheck kryteria członkostwa grupy dynamicznej, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-271">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-272">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-273">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-274">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-275">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="59506-275">click **All groups**.</span></span>

6.  <span data-ttu-id="59506-276">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-277">Kliknij przycisk **członkostwo dynamiczne reguły.**</span><span class="sxs-lookup"><span data-stu-id="59506-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="59506-278">Przejrzyj hello **proste** lub **zaawansowane** reguły zdefiniowane dla tej grupy i upewnij się, hello ma toobe członkiem tej grupy użytkownika spełnia te kryteria.</span><span class="sxs-lookup"><span data-stu-id="59506-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="59506-279">Sprawdź grupy przypisane licencje.</span><span class="sxs-lookup"><span data-stu-id="59506-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="59506-280">toocheck grupy przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-281">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-282">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-283">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-284">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-285">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="59506-285">click **All groups**.</span></span>

6.  <span data-ttu-id="59506-286">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-287">Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="59506-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="59506-288">Ponownie przetworzyć grupy licencji</span><span class="sxs-lookup"><span data-stu-id="59506-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="59506-289">tooreprocess grupy przypisane licencje, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-290">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-291">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-292">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-293">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-294">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="59506-294">click **All groups**.</span></span>

6.  <span data-ttu-id="59506-295">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-296">Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="59506-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="59506-297">Kliknij przycisk hello **ponownie przetworzyć** tooensure przycisku, który hello członków grupy licencji przypisanych toothis są aktualne.</span><span class="sxs-lookup"><span data-stu-id="59506-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="59506-298">Może to zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy.</span><span class="sxs-lookup"><span data-stu-id="59506-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="59506-299">toodo to szybsze, należy wziąć pod uwagę tymczasowo przypisywanie licencji użytkownika toohello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="59506-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="59506-300">[Przypisywanie licencji użytkownika](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="59506-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="59506-301">Przypisz grupę licencji</span><span class="sxs-lookup"><span data-stu-id="59506-301">Assign a group a license</span></span>

<span data-ttu-id="59506-302">tooassign tooa grupę licencji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59506-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="59506-303">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-304">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-305">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-306">Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-307">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="59506-307">click **All groups**.</span></span>

6.  <span data-ttu-id="59506-308">**Wyszukiwanie** grupy hello planuje się i **kliknij wiersz hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="59506-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="59506-309">Kliknij przycisk **licencji** toosee grupy hello licencji, do której obecnie przypisana.</span><span class="sxs-lookup"><span data-stu-id="59506-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="59506-310">Kliknij przycisk hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59506-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="59506-311">Wybierz **jeden lub więcej produktów** z hello listę dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="59506-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="59506-312">**Opcjonalne** kliknij hello **opcje przydziału** toogranularly elementu przypisać produktów.</span><span class="sxs-lookup"><span data-stu-id="59506-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="59506-313">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="59506-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="59506-314">Kliknij przycisk hello **przypisać** przycisk tooassign grupy toothis tych licencji.</span><span class="sxs-lookup"><span data-stu-id="59506-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="59506-315">Może to zająć dużo czasu, w zależności od rozmiaru hello i złożoność hello grupy.</span><span class="sxs-lookup"><span data-stu-id="59506-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="59506-316">toodo to szybsze, należy wziąć pod uwagę tymczasowo przypisywanie licencji użytkownika toohello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="59506-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="59506-317">[Przypisywanie licencji użytkownika](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="59506-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="59506-318">Problemy z zasadami dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="59506-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="59506-319">Sprawdzanie zasad określonych dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="59506-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="59506-320">toocheck albo do sprawdzania zasad pojedynczego dostępu warunkowego:</span><span class="sxs-lookup"><span data-stu-id="59506-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="59506-321">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-322">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-323">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-324">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-325">Kliknij przycisk hello **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="59506-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="59506-326">Kliknij zasady hello myślisz sprawdzania.</span><span class="sxs-lookup"><span data-stu-id="59506-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="59506-327">Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59506-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="59506-328">Możesz wyłączyć tootemporarily to tooensure zasad go nie wpływają na znak ubezp toodo hello tego zestawu **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku .</span><span class="sxs-lookup"><span data-stu-id="59506-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="59506-329">Sprawdź zasady dostępu warunkowego określonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="59506-330">toocheck albo do sprawdzania zasad aktualnie skonfigurowany dostęp warunkowy pojedynczej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="59506-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="59506-331">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-332">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-333">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-334">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-335">Kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59506-335">click **All applications**.</span></span>

6.  <span data-ttu-id="59506-336">Wyszukiwanie aplikacji hello interesuje lub hello użytkownik próbuje toosign w aplikacji tooby wyświetlanie identyfikatora aplikacji lub nazwa.</span><span class="sxs-lookup"><span data-stu-id="59506-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="59506-337">Jeśli nie widzisz aplikacji hello, którego szukasz, kliknij przycisk hello **filtru** przycisk i zwiększa zakresu hello listy hello zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59506-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="59506-338">Toosee więcej kolumn, kliknij przycisk hello **kolumn** przycisk tooadd dodatkowe szczegóły dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="59506-339">Kliknij przycisk hello **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="59506-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="59506-340">Kliknij zasady hello myślisz sprawdzania.</span><span class="sxs-lookup"><span data-stu-id="59506-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="59506-341">Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59506-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="59506-342">Możesz wyłączyć tootemporarily to tooensure zasad go nie wpływają na znak ubezp toodo hello tego zestawu **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku .</span><span class="sxs-lookup"><span data-stu-id="59506-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="59506-343">Wyłącz zasady dostępu warunkowego określonych</span><span class="sxs-lookup"><span data-stu-id="59506-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="59506-344">toocheck albo do sprawdzania zasad pojedynczego dostępu warunkowego:</span><span class="sxs-lookup"><span data-stu-id="59506-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="59506-345">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="59506-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="59506-346">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="59506-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="59506-347">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="59506-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="59506-348">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="59506-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="59506-349">Kliknij przycisk hello **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="59506-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="59506-350">Kliknij zasady hello myślisz sprawdzania.</span><span class="sxs-lookup"><span data-stu-id="59506-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="59506-351">Wyłącz zasady hello przez ustawienie hello **Włącz zasady** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisk.</span><span class="sxs-lookup"><span data-stu-id="59506-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="59506-352">Problemy z zgody aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-352">Problems with application consent</span></span>

<span data-ttu-id="59506-353">Dostęp do aplikacji mogą zostać zablokowane, ponieważ nie przeprowadzono hello odpowiednich uprawnień zgodą operacji.</span><span class="sxs-lookup"><span data-stu-id="59506-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="59506-354">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywaniu problemów zgody aplikacji:</span><span class="sxs-lookup"><span data-stu-id="59506-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="59506-355">Wykonanie operacji zgody na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="59506-356">Operacja zgody na poziomie administratora dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="59506-357">Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="59506-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="59506-358">Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="59506-359">Wykonanie operacji zgody na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="59506-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="59506-360">Dla dowolnego Open ID Connect aplikacja obsługująca żąda uprawnień nawigowanie po znaku toohello aplikacji na ekranie wykonuje aplikacji toohello poziomu zgody użytkownika hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59506-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="59506-361">Jeśli chcesz toodo to programowo, zobacz [żąda zgody użytkownika](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="59506-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="59506-362">Operacja zgody na poziomie administratora dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="59506-363">Dla **tylko aplikacje opracowane za pomocą modelu aplikacji hello V1**, możesz wymusić ten toooccur poziomu zgody administratora, dodając "**? prompt = admin\_zgody**" toohello koniec Zaloguj się adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59506-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="59506-364">Dla **dowolnej aplikacji utworzony przy użyciu modelu aplikacji hello V2**, wykonując instrukcje hello w obszarze hello można wymusić ten toooccur zgody na poziomie administratora **zażądać uprawnień hello z katalogu Administrator** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="59506-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="59506-365">Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="59506-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="59506-366">Dla **aplikacji pojedynczej dzierżawy** który zażądać uprawnień (np. te opracowujesz lub własny w organizacji), można wykonać **zgody na poziomie administracyjnym** operacji imieniu wszystkie Użytkownicy zalogować się jako Administrator globalny i klikając hello **udzielić uprawnień** u góry hello hello **rejestru aplikacji -&gt; wszystkie aplikacje —&gt; wybierz aplikację - &gt; Wymagane uprawnienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="59506-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="59506-367">Dla **dowolnej aplikacji utworzony przy użyciu hello V1 lub V2 modelu aplikacji**, wykonując instrukcje hello w obszarze hello można wymusić ten toooccur zgody na poziomie administratora **zażądać uprawnień hello z Administrator katalogu** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="59506-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="59506-368">Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji</span><span class="sxs-lookup"><span data-stu-id="59506-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="59506-369">Dla **aplikacje wielodostępne** tego zażądać uprawnień (np. aplikacji innej firmy lub firmy Microsoft, które zostały zaakceptowane), można wykonać **zgody na poziomie administracyjnym** operacji.</span><span class="sxs-lookup"><span data-stu-id="59506-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="59506-370">Zaloguj się jako Administrator globalny i klikając hello **udzielić uprawnień** przycisku w obszarze hello **aplikacje przedsiębiorstwa -&gt; wszystkie aplikacje —&gt; wybierz aplikację -&gt; Uprawnienia** bloku (dostępne wkrótce).</span><span class="sxs-lookup"><span data-stu-id="59506-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="59506-371">Może również wymuszać toooccur tej zgody na poziomie administratora, wykonując instrukcje hello w obszarze hello **poprosić hello uprawnienia administratora katalogu** sekcji [przy użyciu punktu końcowego zgody administratora hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="59506-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59506-372">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59506-372">Next steps</span></span>
[<span data-ttu-id="59506-373">Przy użyciu punktu końcowego zgody administratora hello</span><span class="sxs-lookup"><span data-stu-id="59506-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

