---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="74343-103">Dodawanie nowych użytkowników lub użytkownicy z Microsoft tooAzure kont usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="74343-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="74343-104">Dodaj użytkowników toopopulate katalogu.</span><span class="sxs-lookup"><span data-stu-id="74343-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="74343-105">W tym artykule opisano sposób tooadd nowych użytkowników w organizacji, jak i tooadd użytkowników, którzy mają konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74343-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="74343-106">Aby uzyskać więcej informacji na temat dodawania użytkowników z innych katalogów w usłudze Azure Active Directory lub dodawania użytkowników z firm partnerskich, zobacz [Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="74343-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="74343-107">Dodano użytkownicy nie mają uprawnień administratora domyślnie, ale można przypisać toothem role w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="74343-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74343-108">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="74343-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="74343-109">Dla tooadd użytkownika w Centrum administracyjnym hello Azure AD, zobacz temat [Dodaj nowe tooAzure użytkowników usługi Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74343-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="74343-110">Dodawanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="74343-110">Add a user</span></span>
1. <span data-ttu-id="74343-111">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="74343-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="74343-112">Wybierz **usługi Active Directory**, a następnie wybierz nazwę hello katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="74343-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="74343-113">Wybierz hello **użytkowników** , a następnie na pasku poleceń hello, wybierz **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="74343-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="74343-114">Na powitania **Poinformuj nas o tym użytkowniku** w obszarze **typ użytkownika**, wybierz opcję:</span><span class="sxs-lookup"><span data-stu-id="74343-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="74343-115">**Nowy użytkownik w organizacji** — dodaje nowe konto użytkownika w katalogu.</span><span class="sxs-lookup"><span data-stu-id="74343-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="74343-116">**Użytkownik z istniejącym kontem Microsoft** — dodaje istniejące Microsoft konsumenta konta tooyour katalog (na przykład konto programu Outlook)</span><span class="sxs-lookup"><span data-stu-id="74343-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="74343-117">W zależności od **typu użytkownika** wprowadź nazwę użytkownika (dla nowego użytkownika) lub adres e-mail (dla użytkownika z kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="74343-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="74343-118">Na użytkownika hello **profilu** Podaj imię i nazwisko, nazwę przyjazną użytkownikowi i rolę użytkownika z hello **ról** listy.</span><span class="sxs-lookup"><span data-stu-id="74343-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="74343-119">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="74343-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="74343-120">Określ, czy za**Włączanie uwierzytelniania wieloskładnikowego** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="74343-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="74343-121">Na powitania **Uzyskaj hasło tymczasowe** wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="74343-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74343-122">Jeśli Twoja organizacja korzysta z więcej niż jedną domenę, musisz wiedzieć o hello następujące problemy podczas dodawania konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="74343-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="74343-123">tooadd kont użytkowników z hello tego samego główna nazwa użytkownika (UPN) między domenami, **pierwszy** dodać, na przykład geoffgrisso@contoso.onmicrosoft.com, **następuje** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="74343-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="74343-124">**Nie** dodawaj adresu geoffgrisso@contoso.com przed dodaniem adresu geoffgrisso@contoso.onmicrosoft.com. To zamówienie jest ważne i może być skomplikowane tooundo.</span><span class="sxs-lookup"><span data-stu-id="74343-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="74343-125">Zmiana informacji o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="74343-125">Change user information</span></span>
<span data-ttu-id="74343-126">Możesz zmienić dowolny atrybut użytkownika, z wyjątkiem identyfikatora obiektu hello.</span><span class="sxs-lookup"><span data-stu-id="74343-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="74343-127">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="74343-127">Open your directory.</span></span>
2. <span data-ttu-id="74343-128">Wybierz hello **użytkowników** kartę i hello następnie wybierz nazwę wyświetlaną użytkownika ma toochange hello.</span><span class="sxs-lookup"><span data-stu-id="74343-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="74343-129">Wprowadź zmiany, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="74343-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="74343-130">Jeśli użytkownik hello, który chcesz zmienić jest synchronizowane z lokalnej usługi Active Directory, nie można zmienić informacje o użytkowniku hello za pomocą tej procedury.</span><span class="sxs-lookup"><span data-stu-id="74343-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="74343-131">toochange hello użytkownika, użyj narzędzi zarządzania lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="74343-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="74343-132">Zarządzanie użytkownikami typu Gość i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="74343-132">Guest user management and limitations</span></span>
<span data-ttu-id="74343-133">Konta gościa korzystają użytkownicy z innych katalogów, którzy byli dokumentów programu SharePoint tooaccess katalogu zaproszonych tooyour, aplikacji lub innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74343-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="74343-134">Konto gościa w katalogu ma jego podstawowy atrybut UserType ustawiona zbyt "Gość."</span><span class="sxs-lookup"><span data-stu-id="74343-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="74343-135">Normalnych użytkowników (w szczególności członków katalogu) ma atrybut UserType hello "Członek".</span><span class="sxs-lookup"><span data-stu-id="74343-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="74343-136">Goście mają ograniczony zestaw praw w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="74343-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="74343-137">Te prawa ograniczają możliwość hello gości toodiscover informacji o innych użytkowników w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="74343-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="74343-138">Jednak gościa nadal interakcji użytkowników z hello użytkownikami i grupami skojarzonymi z zasobami hello, nad którymi pracuje.</span><span class="sxs-lookup"><span data-stu-id="74343-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="74343-139">Goście mogą:</span><span class="sxs-lookup"><span data-stu-id="74343-139">Guest users can:</span></span>

* <span data-ttu-id="74343-140">Wyświetlać innych użytkowników i grup skojarzonych z toowhich subskrypcji platformy Azure, w których są przydzielone</span><span class="sxs-lookup"><span data-stu-id="74343-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="74343-141">Zobacz hello członkami toowhich grup, do których należą</span><span class="sxs-lookup"><span data-stu-id="74343-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="74343-142">Wyszukiwać innych użytkowników w katalogu hello, jeśli znają hello pełny adres e-mail użytkownika, powitalne</span><span class="sxs-lookup"><span data-stu-id="74343-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="74343-143">Zobaczyć tylko ograniczony zestaw atrybutów użytkowników hello, ich wyszukiwanie — ograniczone toodisplay nazwa, adres e-mail, główna nazwa użytkownika (UPN) i miniatury zdjęcia</span><span class="sxs-lookup"><span data-stu-id="74343-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="74343-144">Pobierz listę zweryfikowanych domen w katalogu hello</span><span class="sxs-lookup"><span data-stu-id="74343-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="74343-145">Tooapplications zgody, przyznania im hello takie same prawa dostępu, jakie mają członkowie w katalogu</span><span class="sxs-lookup"><span data-stu-id="74343-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="74343-146">Ustawianie zasad dostępu dla gościa</span><span class="sxs-lookup"><span data-stu-id="74343-146">Set guest user access policies</span></span>
<span data-ttu-id="74343-147">Witaj **Konfiguruj** karta katalogu zawiera opcje toocontrol dostępu dla gości.</span><span class="sxs-lookup"><span data-stu-id="74343-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="74343-148">Te opcje mogą zostać zmienione wyłącznie za pośrednictwem klasycznego portalu Azure przez globalnego administratora katalogu.</span><span class="sxs-lookup"><span data-stu-id="74343-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="74343-149">Obecnie nie ma metody robienia tego przez interfejs API lub program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74343-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="74343-150">tooopen hello **Konfiguruj** karcie hello Azure klasycznym portalu, wybierz **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="74343-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Karta Konfigurowanie w usłudze Azure Active Directory][1]

<span data-ttu-id="74343-152">Następnie można edytować hello opcje toocontrol dostępu dla gości.</span><span class="sxs-lookup"><span data-stu-id="74343-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![Opcje kontroli dostępu dla gości][2]

## <a name="whats-next"></a><span data-ttu-id="74343-154">Co dalej</span><span class="sxs-lookup"><span data-stu-id="74343-154">What's next</span></span>
* [<span data-ttu-id="74343-155">Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74343-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="74343-156">Administrowanie usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="74343-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="74343-157">Zarządzanie hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="74343-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="74343-158">Zarządzanie grupami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="74343-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
