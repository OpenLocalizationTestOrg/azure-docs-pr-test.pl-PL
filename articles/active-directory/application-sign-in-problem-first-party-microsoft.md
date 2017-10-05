---
title: Problemy przy logowaniu do aplikacji firmy Microsoft | Dokumentacja firmy Microsoft
description: "Rozwiązywanie typowych problemów, które muszą ponieść po zalogowaniu się do firmy Microsoft Applications przy użyciu usługi Azure AD (takich jak usługi Office 365)"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="fe974-103">Problemy przy logowaniu do aplikacji firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe974-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="fe974-104">Microsoft Applications (takich jak Office 365 Exchange, SharePoint, Yammer itp.) są przypisane i zarządzane nieco inaczej niż 3 aplikacji SaaS innych producentów i inne aplikacje, które integracji z usługą Azure AD na logowanie jednokrotne w.</span><span class="sxs-lookup"><span data-stu-id="fe974-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="fe974-105">Istnieją trzy sposoby, czy użytkownik może uzyskać dostęp do aplikacji publikowanych przez firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fe974-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="fe974-106">W przypadku aplikacji w usłudze Office 365 lub innych mechanizmów płatną użytkownicy uzyskują dostęp za pośrednictwem **przypisania licencji** albo bezpośrednio do swojego konta użytkownika, albo przez grupę przy użyciu naszego możliwość przypisania na podstawie grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="fe974-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="fe974-107">Dla aplikacji, które firmy Microsoft lub stron trzecich publikuje za darmo dla każdego z nich do używania, użytkownicy mogą otrzymać dostęp za pośrednictwem **zgody użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="fe974-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="fe974-108">This0 oznacza, że Zaloguj się do aplikacji z ich Azure AD konta służbowego i zezwolenie na dostęp do niektórych ograniczony zestaw danych na koncie.</span><span class="sxs-lookup"><span data-stu-id="fe974-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="fe974-109">Dla aplikacji, które firmy Microsoft lub 3rd Strona publikuje za darmo dla każdego z nich do używania, użytkownicy mogą również uzyskać dostęp za pośrednictwem **zgody administratora**.</span><span class="sxs-lookup"><span data-stu-id="fe974-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="fe974-110">Oznacza to, że administrator wykrył, że aplikacja może być używany przez wszyscy użytkownicy w organizacji, aby zalogować się do aplikacji przy użyciu konta administratora globalnego i przyznać dostęp wszystkim użytkownikom w organizacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="fe974-111">Aby rozwiązać problem, uruchom przy użyciu [ogólne obszarów problemów z dostępem do aplikacji wziąć pod uwagę](#general-problem-areas-with-application-access-to-consider) , a następnie odczytywane [wskazówki: kroki rozwiązywania problemów z Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access) uzyskanie do szczegółów.</span><span class="sxs-lookup"><span data-stu-id="fe974-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="fe974-112">Ogólne obszarów problemów z dostępem aplikacji do uwzględnienia</span><span class="sxs-lookup"><span data-stu-id="fe974-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="fe974-113">Poniżej przedstawiono listę obszarów problemów ogólne, które można przejść do szczegółów Jeśli wiadomo, gdzie można uruchomić, ale zaleca się przeczytanie wskazówki, aby zacząć szybko: [wskazówki: kroki rozwiązywania problemów z Microsoft Application dostępu](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="fe974-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="fe974-114">Problemy z kontem użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="fe974-115">Problemy z grupy</span><span class="sxs-lookup"><span data-stu-id="fe974-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="fe974-116">Problemy z zasadami dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="fe974-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="fe974-117">Problemy z zgody aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="fe974-118">Kroki rozwiązywania problemów z Microsoft Application dostępu</span><span class="sxs-lookup"><span data-stu-id="fe974-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="fe974-119">Poniżej są niektóre typowe problemy pracowników wystąpiły podczas ich użytkownik nie zaloguje się do aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fe974-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="fe974-120">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="fe974-120">General issues to check first</span></span>

  * <span data-ttu-id="fe974-121">Upewnij się, że użytkownik loguje się do **Popraw adres URL** , a nie adres URL lokalnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="fe974-122">Upewnij się, że konto użytkownika jest **bez blokady.**</span><span class="sxs-lookup"><span data-stu-id="fe974-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="fe974-123">Upewnij się, że **konto użytkownika istnieje** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe974-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="fe974-124">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe974-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="fe974-125">Upewnij się, że konto użytkownika jest **włączone** dla logowania.</span><span class="sxs-lookup"><span data-stu-id="fe974-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="fe974-126">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="fe974-127">Upewnij się, że użytkownika **nie wygasł lub zapomnienia hasła.**</span><span class="sxs-lookup"><span data-stu-id="fe974-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="fe974-128">[Resetuj hasło użytkownika](#reset-a-users-password) lub [włączyć samoobsługowe Resetowanie hasła](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="fe974-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="fe974-129">Upewnij się, że **uwierzytelnianie wieloskładnikowe** nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="fe974-130">[Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="fe974-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="fe974-131">Upewnij się, że **zasady dostępu warunkowego** lub **Identity Protection** zasad nie blokuje dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="fe974-132">[Sprawdź zasady dostępu warunkowego określonych](#problems-with-conditional-access-policies) lub [Sprawdź zasady dostępu warunkowego określonej aplikacji](#check-a-specific-applications-conditional-access-policy) lub [zasad dostępu warunkowego określonych wyłączone](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="fe974-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="fe974-133">Upewnij się, że użytkownik **informacje kontaktowe uwierzytelniania** jest aktualny, aby umożliwić uwierzytelnianie wieloskładnikowe lub dostępu warunkowego zasad, które mają być egzekwowane.</span><span class="sxs-lookup"><span data-stu-id="fe974-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="fe974-134">[Sprawdź stan usługi Multi-Factor authentication użytkownika](#check-a-users-multi-factor-authentication-status) lub [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="fe974-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="fe974-135">Aby uzyskać **Microsoft** **aplikacje, które wymagają licencji** (takich jak usługi Office 365), poniżej przedstawiono niektóre określonych problemów, aby sprawdzić po zostały wykluczone powyższe problemy ogólne:</span><span class="sxs-lookup"><span data-stu-id="fe974-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="fe974-136">Upewnij się, użytkownika lub ma **przypisanej licencji.**</span><span class="sxs-lookup"><span data-stu-id="fe974-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="fe974-137">[Sprawdź przypisane licencje użytkownika](#check-a-users-assigned-licenses) lub [Sprawdź grupy przypisane licencje.](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="fe974-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="fe974-138">W przypadku licencji **przypisane do** **Grupa statyczna**, upewnij się, że **użytkownik jest członkiem** tej grupy.</span><span class="sxs-lookup"><span data-stu-id="fe974-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="fe974-139">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="fe974-140">W przypadku licencji **przypisane do** **Dynamiczna grupa**, upewnij się, że **grupa dynamiczna reguła została poprawnie ustawiona**.</span><span class="sxs-lookup"><span data-stu-id="fe974-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="fe974-141">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="fe974-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="fe974-142">W przypadku licencji **przypisane do** **Dynamiczna grupa**, upewnij się, że grupa dynamiczna ma **zakończyło się przetwarzanie** członkostwa oraz że **użytkownik jest członkiem** (może to zająć pewien czas).</span><span class="sxs-lookup"><span data-stu-id="fe974-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="fe974-143">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="fe974-144">Po należy upewnić się, licencja jest przypisany, upewnij się, że licencja jest **niewygasły**.</span><span class="sxs-lookup"><span data-stu-id="fe974-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="fe974-145">Upewnij się, że licencja jest **dla aplikacji** uzyskują oni dostęp.</span><span class="sxs-lookup"><span data-stu-id="fe974-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="fe974-146">Dla **Microsoft** **aplikacje, które nie wymagają licencji**, poniżej przedstawiono niektóre inne czynności do wykonania:</span><span class="sxs-lookup"><span data-stu-id="fe974-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="fe974-147">Jeśli aplikacja żąda **uprawnienia na poziomie użytkownika** (na przykład "dostęp do skrzynek pocztowych użytkowników"), upewnij się, że użytkownik zalogował się do aplikacji i wykonał **operacji zgody użytkownika na poziomie** aby umożliwić aplikacji dostęp do swoich danych.</span><span class="sxs-lookup"><span data-stu-id="fe974-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="fe974-148">Jeśli aplikacja żąda **uprawnień na poziomie administratora** (na przykład "dostęp do skrzynek pocztowych wszystkich użytkowników"), upewnij się, że przeprowadził administratora globalnego **operacji zgody na poziomie administratora w imieniu wszystkich użytkowników** w organizacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="fe974-149">Problemy z kontem użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-149">Problems with the user’s account</span></span>

<span data-ttu-id="fe974-150">Dostęp do aplikacji mogą zostać zablokowane z powodu problemu z użytkownikiem, który jest przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="fe974-151">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywania problemów z użytkownikami i ich ustawienia konta:</span><span class="sxs-lookup"><span data-stu-id="fe974-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="fe974-152">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe974-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="fe974-153">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="fe974-154">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="fe974-155">Włącz samoobsługowe resetowanie haseł</span><span class="sxs-lookup"><span data-stu-id="fe974-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="fe974-156">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="fe974-157">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="fe974-158">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="fe974-159">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="fe974-160">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="fe974-161">Sprawdź, czy konto użytkownika istnieje w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe974-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="fe974-162">Aby sprawdzić, czy konto użytkownika jest obecne, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-163">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-164">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-165">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-166">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-167">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-167">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-168">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-169">Sprawdź właściwości obiektu użytkownika, należy upewnić się, że wyglądają zgodnie z oczekiwaniami i żadne dane nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="fe974-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="fe974-170">Sprawdź stan konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-170">Check a user’s account status</span></span>

<span data-ttu-id="fe974-171">Aby sprawdzić stan konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-172">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-173">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-174">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-175">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-176">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-176">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-177">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-178">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="fe974-178">click **Profile**.</span></span>

8.  <span data-ttu-id="fe974-179">W obszarze **ustawienia** upewnij się, że **Zaloguj bloku** ustawiono **nr**.</span><span class="sxs-lookup"><span data-stu-id="fe974-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="fe974-180">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-180">Reset a user’s password</span></span>

<span data-ttu-id="fe974-181">Aby zresetować hasło użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-182">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-183">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-184">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-185">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-186">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-186">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-187">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-188">Kliknij przycisk **resetowania hasła** na górze bloku użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="fe974-189">Kliknij przycisk **resetowania hasła** znajdującego się na **resetowania hasła** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="fe974-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="fe974-190">Kopiuj **hasło tymczasowe** lub **wprowadź nowe hasło** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="fe974-191">Komunikować się z tego nowego hasła dla użytkownika, konieczności zmianę hasła podczas kolejnego logowania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe974-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="fe974-192">Włącz samoobsługowe Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="fe974-192">Enable self-service password reset</span></span>

<span data-ttu-id="fe974-193">Aby włączyć samoobsługowe Resetowanie hasła, wykonaj poniższe kroki wdrażania:</span><span class="sxs-lookup"><span data-stu-id="fe974-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="fe974-194">Umożliwianie użytkownikom resetowania swoich haseł w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe974-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="fe974-195">Umożliwianie użytkownikom resetowania lub zmieniania swoich haseł lokalnej usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe974-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="fe974-196">Sprawdź stan usługi Multi-Factor authentication użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="fe974-197">Aby sprawdzić stan usługi Multi-Factor authentication użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-198">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-199">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-200">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-201">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-202">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-202">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-203">Kliknij przycisk **uwierzytelnianie wieloskładnikowe** u góry bloku.</span><span class="sxs-lookup"><span data-stu-id="fe974-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="fe974-204">Raz **portalu administracyjnego usługi Multi-Factor Authentication** obciążeń, upewnij się, czy na **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="fe974-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="fe974-205">Znajdź użytkownika, na liście użytkowników przez wyszukiwanie, filtrowanie i sortowanie.</span><span class="sxs-lookup"><span data-stu-id="fe974-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="fe974-206">Wybierz użytkownika z listy użytkowników i **włączyć**, **wyłączyć**, lub **Wymuś** usługi Multi-Factor authentication zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="fe974-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="fe974-207">**Uwaga**: Jeśli użytkownik znajduje się w **wymuszone** stanu, użytkownik może ustawić ich **wyłączone** tymczasowo w celu umożliwienia im wrócić do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="fe974-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="fe974-208">Gdy są one ponownie, można zmienić ich stan, aby **włączone** ponownie, aby wymagały ponownie zarejestrować swoje informacje kontaktowe podczas ich następnego logowania.</span><span class="sxs-lookup"><span data-stu-id="fe974-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="fe974-209">Alternatywnie możesz wykonać kroki opisane w [Sprawdź informacje kontaktowe uwierzytelniania użytkownika](#check-a-users-authentication-contact-info) Sprawdź lub ustaw dla nich dane.</span><span class="sxs-lookup"><span data-stu-id="fe974-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="fe974-210">Sprawdź informacje kontaktowe uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="fe974-211">Aby sprawdzić informacje kontaktowe uwierzytelniania użytkownika używane do uwierzytelniania wieloskładnikowego, dostępu warunkowego, ochrony tożsamości i resetowania hasła, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-212">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-213">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-214">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-215">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-216">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-216">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-217">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-218">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="fe974-218">click **Profile**.</span></span>

8.  <span data-ttu-id="fe974-219">Przewiń w dół do **informacje kontaktowe uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="fe974-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="fe974-220">**Przegląd** danych zarejestrowanych dla użytkowników i aktualizacji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="fe974-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="fe974-221">Sprawdzanie członkostwa w grupach użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-221">Check a user’s group memberships</span></span>

<span data-ttu-id="fe974-222">Aby sprawdzić członkostwa w grupach użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-223">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-224">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-225">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-226">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-227">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-227">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-228">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-229">Kliknij przycisk **grup** Aby wyświetlić grupy, które użytkownik jest członkiem.</span><span class="sxs-lookup"><span data-stu-id="fe974-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="fe974-230">Sprawdź przypisane licencje użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="fe974-231">Aby sprawdzić przypisane licencje użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-232">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-233">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-234">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-235">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-236">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-236">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-237">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-238">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="fe974-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="fe974-239">Przypisywanie licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-239">Assign a user a license</span></span> 

<span data-ttu-id="fe974-240">Aby przypisać licencję do użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-241">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-242">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-243">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-244">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-245">Kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe974-245">click **All users**.</span></span>

6.  <span data-ttu-id="fe974-246">**Wyszukiwanie** dla użytkownika planuje się i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-247">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje użytkownika został przypisany.</span><span class="sxs-lookup"><span data-stu-id="fe974-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="fe974-248">Kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe974-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="fe974-249">Wybierz **jeden lub więcej produktów** z listy dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="fe974-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="fe974-250">**Opcjonalne** kliknij **opcje przydziału** element, aby przypisać częściami produktów.</span><span class="sxs-lookup"><span data-stu-id="fe974-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="fe974-251">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="fe974-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="fe974-252">Kliknij przycisk **przypisać** przycisk, aby przypisać licencje do tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="fe974-253">Problemy z grupy</span><span class="sxs-lookup"><span data-stu-id="fe974-253">Problems with groups</span></span>

<span data-ttu-id="fe974-254">Dostęp do aplikacji mogą zostać zablokowane z powodu problemu z grupy, który jest przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="fe974-255">Poniżej przedstawiono kilka sposobów, można rozwiązać i rozwiązać problemy z grupy i członkostwa w grupach:</span><span class="sxs-lookup"><span data-stu-id="fe974-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="fe974-256">Sprawdź członkostwo w grupie</span><span class="sxs-lookup"><span data-stu-id="fe974-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="fe974-257">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="fe974-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="fe974-258">Sprawdź grupy przypisane licencje.</span><span class="sxs-lookup"><span data-stu-id="fe974-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="fe974-259">Ponownie przetworzyć grupy licencji</span><span class="sxs-lookup"><span data-stu-id="fe974-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="fe974-260">Przypisz grupę licencji</span><span class="sxs-lookup"><span data-stu-id="fe974-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="fe974-261">Sprawdź członkostwo w grupie</span><span class="sxs-lookup"><span data-stu-id="fe974-261">Check a group’s membership</span></span>

<span data-ttu-id="fe974-262">Aby sprawdzić członkostwa w grupie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-263">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-264">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-265">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-266">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-267">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fe974-267">click **All groups**.</span></span>

6.  <span data-ttu-id="fe974-268">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-269">Kliknij przycisk **członków** Aby przejrzeć listę użytkowników przypisanych do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="fe974-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="fe974-270">Sprawdź kryteria członkostwa grupy dynamicznej</span><span class="sxs-lookup"><span data-stu-id="fe974-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="fe974-271">Aby sprawdzić kryteria członkostwa grupy dynamicznej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-272">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-273">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-274">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-275">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-276">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fe974-276">click **All groups**.</span></span>

6.  <span data-ttu-id="fe974-277">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-278">Kliknij przycisk **członkostwo dynamiczne reguły.**</span><span class="sxs-lookup"><span data-stu-id="fe974-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="fe974-279">Przegląd **proste** lub **zaawansowane** reguły zdefiniowane dla tej grupy i upewnij się, że mają być członkami tej grupy użytkownika spełnia te kryteria.</span><span class="sxs-lookup"><span data-stu-id="fe974-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="fe974-280">Sprawdź grupy przypisane licencje.</span><span class="sxs-lookup"><span data-stu-id="fe974-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="fe974-281">Aby sprawdzić grupy przypisane licencje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-282">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-283">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-284">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-285">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-286">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fe974-286">click **All groups**.</span></span>

6.  <span data-ttu-id="fe974-287">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-288">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje grupy został przypisany.</span><span class="sxs-lookup"><span data-stu-id="fe974-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="fe974-289">Ponownie przetworzyć grupy licencji</span><span class="sxs-lookup"><span data-stu-id="fe974-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="fe974-290">Aby ponownie przetworzyć grupy przypisane licencje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-291">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-292">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-293">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-294">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-295">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fe974-295">click **All groups**.</span></span>

6.  <span data-ttu-id="fe974-296">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-297">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje grupy został przypisany.</span><span class="sxs-lookup"><span data-stu-id="fe974-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="fe974-298">Kliknij przycisk **ponownie przetworzyć** przycisk, aby upewnić się, że licencji przypisanych do członków tej grupy są aktualne.</span><span class="sxs-lookup"><span data-stu-id="fe974-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="fe974-299">Może to zająć dużo czasu, w zależności od rozmiaru i złożoności grupy.</span><span class="sxs-lookup"><span data-stu-id="fe974-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fe974-300">Aby szybciej to zrobić, należy wziąć pod uwagę tymczasowo bezpośrednio przypisywania licencji do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="fe974-301">[Przypisywanie licencji użytkownika](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="fe974-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="fe974-302">Przypisz grupę licencji</span><span class="sxs-lookup"><span data-stu-id="fe974-302">Assign a group a license</span></span>

<span data-ttu-id="fe974-303">Aby przypisać licencję do grupy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe974-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="fe974-304">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-305">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-306">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-307">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-308">Kliknij przycisk **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fe974-308">click **All groups**.</span></span>

6.  <span data-ttu-id="fe974-309">**Wyszukiwanie** dla grupy Użytkownicy zainteresowani i **kliknij wiersz** do wybrania.</span><span class="sxs-lookup"><span data-stu-id="fe974-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fe974-310">Kliknij przycisk **licencji** aby zobaczyć, które obecnie licencje grupy został przypisany.</span><span class="sxs-lookup"><span data-stu-id="fe974-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="fe974-311">Kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe974-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="fe974-312">Wybierz **jeden lub więcej produktów** z listy dostępnych produktów.</span><span class="sxs-lookup"><span data-stu-id="fe974-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="fe974-313">**Opcjonalne** kliknij **opcje przydziału** element, aby przypisać częściami produktów.</span><span class="sxs-lookup"><span data-stu-id="fe974-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="fe974-314">Kliknij przycisk **Ok** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="fe974-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="fe974-315">Kliknij przycisk **przypisać** przycisk, aby przypisać licencje do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="fe974-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="fe974-316">Może to zająć dużo czasu, w zależności od rozmiaru i złożoności grupy.</span><span class="sxs-lookup"><span data-stu-id="fe974-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fe974-317">Aby szybciej to zrobić, należy wziąć pod uwagę tymczasowo bezpośrednio przypisywania licencji do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="fe974-318">[Przypisywanie licencji użytkownika](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="fe974-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="fe974-319">Problemy z zasadami dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="fe974-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="fe974-320">Sprawdzanie zasad określonych dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="fe974-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="fe974-321">Aby sprawdzić lub zweryfikować zasady dostępu warunkowego pojedynczego:</span><span class="sxs-lookup"><span data-stu-id="fe974-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="fe974-322">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-323">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-324">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-325">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-326">Kliknij przycisk **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="fe974-327">Kliknij zasady, o których planuje się zapoznanie się.</span><span class="sxs-lookup"><span data-stu-id="fe974-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="fe974-328">Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fe974-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fe974-329">Możesz też chcieć tymczasowo wyłączyć tę zasadę, aby upewnić się, nie wpływa logowania.</span><span class="sxs-lookup"><span data-stu-id="fe974-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="fe974-330">Aby to zrobić, ustaw **Włącz zasady** Przełącz, aby **nr** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe974-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="fe974-331">Sprawdź zasady dostępu warunkowego określonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="fe974-332">Sprawdź lub sprawdzić poprawności pojedynczej aplikacji aktualnie skonfigurowane zasady dostępu warunkowego:</span><span class="sxs-lookup"><span data-stu-id="fe974-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="fe974-333">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-334">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-335">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-336">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-337">Kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fe974-337">click **All applications**.</span></span>

6.  <span data-ttu-id="fe974-338">Wyszukaj aplikację, która planuje się lub użytkownik próbuje zalogować się do nazwy wyświetlanej aplikacji lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="fe974-339">Jeśli nie widzisz aplikacji, którego szukasz, kliknij przycisk **filtru** przycisk i zakres na liście, aby rozwinąć **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fe974-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="fe974-340">Jeśli chcesz zobaczyć więcej kolumn, kliknij przycisk **kolumn** przycisk, aby dodać dodatkowe szczegóły dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="fe974-341">Kliknij przycisk **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="fe974-342">Kliknij zasady, o których planuje się zapoznanie się.</span><span class="sxs-lookup"><span data-stu-id="fe974-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="fe974-343">Sprawdź, czy ma żadnych określonych warunków, przydziałów lub innych ustawień, które mogą być blokowane dostępu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fe974-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="fe974-344">Możesz też chcieć tymczasowo wyłączyć tę zasadę, aby upewnić się, nie wpływa logowania.</span><span class="sxs-lookup"><span data-stu-id="fe974-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="fe974-345">Aby to zrobić, ustaw **Włącz zasady** Przełącz, aby **nr** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe974-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="fe974-346">Wyłącz zasady dostępu warunkowego określonych</span><span class="sxs-lookup"><span data-stu-id="fe974-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="fe974-347">Aby sprawdzić lub zweryfikować zasady dostępu warunkowego pojedynczego:</span><span class="sxs-lookup"><span data-stu-id="fe974-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="fe974-348">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="fe974-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fe974-349">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe974-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fe974-350">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe974-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fe974-351">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fe974-352">Kliknij przycisk **dostępu warunkowego** element nawigacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="fe974-353">Kliknij zasady, o których planuje się zapoznanie się.</span><span class="sxs-lookup"><span data-stu-id="fe974-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="fe974-354">Wyłącz zasady przez ustawienie **Włącz zasady** Przełącz, aby **nr** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe974-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="fe974-355">Problemy z zgody aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-355">Problems with application consent</span></span>

<span data-ttu-id="fe974-356">Dostęp do aplikacji mogą zostać zablokowane, ponieważ nie przeprowadzono operacji zgody odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="fe974-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="fe974-357">Poniżej przedstawiono kilka sposobów umożliwiają rozwiązywanie problemów oraz rozwiązywaniu problemów zgody aplikacji:</span><span class="sxs-lookup"><span data-stu-id="fe974-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="fe974-358">Wykonanie operacji zgody na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="fe974-359">Operacja zgody na poziomie administratora dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="fe974-360">Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="fe974-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="fe974-361">Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="fe974-362">Wykonanie operacji zgody na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe974-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="fe974-363">Dla dowolnego Open ID Connect aplikacja obsługująca żąda uprawnień przechodząc do rejestrowania aplikacji na ekranie wykonuje poziomu zgody użytkownika do aplikacji dla zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe974-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="fe974-364">Jeśli chcesz to zrobić programowo, zobacz [żąda zgody użytkownika](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="fe974-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="fe974-365">Operacja zgody na poziomie administratora dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="fe974-366">Dla **tylko aplikacje opracowane za pomocą modelu aplikacji V1**, możesz wymusić występuje przez dodanie poziomu zgody użytkownika tego administratora "**? prompt = administratora\_zgody**" na końcu aplikacji znaku w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="fe974-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="fe974-367">Dla **wszelkie aplikacje opracowane za pomocą modelu aplikacji V2**, można wymusić tej zgody poziomie administratora nastąpić, postępując zgodnie z instrukcjami dotyczącymi **poprosić uprawnienia administratora katalogu** sekcji [przy użyciu punktu końcowego zgody administratora](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fe974-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="fe974-368">Wykonaj zgody na poziomie administratora dla aplikacji pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="fe974-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="fe974-369">Dla **pojedynczej dzierżawy aplikacji** który zażądać uprawnień (np. te opracowujesz lub własny w organizacji), można wykonać **zgody na poziomie administratora** operacji w imieniu wszystkich użytkowników zalogować się jako Administrator globalny i klikając **udzielić uprawnień** przycisk w górnej części **rejestru aplikacji -&gt; wszystkie aplikacje —&gt; wybierz aplikację -&gt; wymagane uprawnienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="fe974-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="fe974-370">Dla **wszelkie aplikacje opracowane za pomocą modelu aplikacji V1 lub V2**, można wymusić tej zgody poziomie administratora nastąpić, postępując zgodnie z instrukcjami dotyczącymi **poprosić uprawnienia administratora katalogu** sekcji [przy użyciu punktu końcowego zgody administratora](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fe974-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="fe974-371">Wykonaj zgody na poziomie administratora dla wielodostępnych aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe974-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="fe974-372">Dla **aplikacje wielodostępne** tego zażądać uprawnień (np. aplikacji innej firmy lub firmy Microsoft, które zostały zaakceptowane), można wykonać **zgody na poziomie administracyjnym** operacji.</span><span class="sxs-lookup"><span data-stu-id="fe974-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="fe974-373">Zaloguj się jako Administrator globalny i klikając **udzielić uprawnień** przycisku w obszarze **aplikacje przedsiębiorstwa -&gt; wszystkie aplikacje —&gt; wybierz aplikację -&gt; uprawnienia** bloku (dostępne wkrótce).</span><span class="sxs-lookup"><span data-stu-id="fe974-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="fe974-374">Można również wymusić tej zgody poziomie administratora nastąpić, postępując zgodnie z instrukcjami dotyczącymi **poprosić uprawnienia administratora katalogu** sekcji [przy użyciu punktu końcowego zgody administratora](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fe974-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe974-375">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe974-375">Next steps</span></span>
[<span data-ttu-id="fe974-376">Przy użyciu punktu końcowego zgody administratora</span><span class="sxs-lookup"><span data-stu-id="fe974-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

