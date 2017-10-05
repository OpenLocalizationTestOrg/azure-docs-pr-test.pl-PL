---
title: "Dodawanie nowych użytkowników do usługi Azure Active Directory | Microsoft Docs"
description: "Wyjaśnia, jak dodać nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
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
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="7829f-103">Dodawanie nowych użytkowników lub użytkownicy z kontami Microsoft do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7829f-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="7829f-104">Dodaj użytkowników, aby wypełnić katalog.</span><span class="sxs-lookup"><span data-stu-id="7829f-104">Add users to populate your directory.</span></span> <span data-ttu-id="7829f-105">W tym artykule opisano sposób dodawania nowych użytkowników do organizacji oraz sposób dodawania użytkowników, którzy mają konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7829f-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="7829f-106">Aby uzyskać więcej informacji na temat dodawania użytkowników z innych katalogów w usłudze Azure Active Directory lub dodawania użytkowników z firm partnerskich, zobacz [Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="7829f-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="7829f-107">Dodani użytkownicy domyślnie nie mają uprawnień administratora, ale możesz przypisać im role w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="7829f-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7829f-108">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="7829f-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="7829f-109">Jak dodać użytkownika w Centrum administracyjnym usługi Azure AD, zobacz [Dodawanie nowych użytkowników do usługi Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7829f-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="7829f-110">Dodawanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="7829f-110">Add a user</span></span>
1. <span data-ttu-id="7829f-111">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7829f-112">Wybierz usługę **Active Directory**, a następnie wybierz nazwę katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="7829f-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="7829f-113">Wybierz kartę **Użytkownicy**, a następnie na pasku poleceń wybierz polecenie **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7829f-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="7829f-114">Na stronie **Poinformuj nas o tym użytkowniku** w obszarze **Typ użytkownika** wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="7829f-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="7829f-115">**Nowy użytkownik w organizacji** — dodaje nowe konto użytkownika w katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="7829f-116">**Użytkownik z istniejącym kontem Microsoft** — dodaje istniejące konto klienta Microsoft do katalogu (na przykład konto programu Outlook)</span><span class="sxs-lookup"><span data-stu-id="7829f-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="7829f-117">W zależności od **typu użytkownika** wprowadź nazwę użytkownika (dla nowego użytkownika) lub adres e-mail (dla użytkownika z kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="7829f-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="7829f-118">Na stronie **Profil** użytkownika podaj imię i nazwisko, nazwę przyjazną użytkownikowi i rolę użytkownika z listy **Role**.</span><span class="sxs-lookup"><span data-stu-id="7829f-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="7829f-119">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7829f-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="7829f-120">Określ, czy **włączyć usługę Multi-Factor Authentication** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7829f-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="7829f-121">Na stronie **Uzyskaj hasło tymczasowe** wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7829f-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7829f-122">Jeśli Twoja organizacja korzysta z więcej niż jednej domeny, podczas dodawania konta użytkownika musisz wiedzieć o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="7829f-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="7829f-123">Aby dodać konta użytkowników z tą samą główną nazwą użytkownika (UPN) między domenami, **najpierw** dodaj np. adres geoffgrisso@contoso.onmicrosoft.com, **a następnie** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7829f-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="7829f-124">**Nie** dodawaj adresu geoffgrisso@contoso.com przed dodaniem adresu geoffgrisso@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7829f-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="7829f-125">Ta kolejność jest ważna, a jej cofnięcie może być kłopotliwe.</span><span class="sxs-lookup"><span data-stu-id="7829f-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="7829f-126">Zmiana informacji o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="7829f-126">Change user information</span></span>
<span data-ttu-id="7829f-127">Możesz zmienić dowolny atrybut użytkownika z wyjątkiem identyfikatora obiektu.</span><span class="sxs-lookup"><span data-stu-id="7829f-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="7829f-128">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="7829f-128">Open your directory.</span></span>
2. <span data-ttu-id="7829f-129">Wybierz kartę **Użytkownicy**, a następnie wybierz nazwę wyświetlaną użytkownika, którą chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="7829f-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="7829f-130">Wprowadź zmiany, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7829f-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="7829f-131">Nie możesz zmienić informacji o użytkowniku przy użyciu tej procedury, jeśli użytkownik, którego informacje chcesz zmienić, jest zsynchronizowany z lokalną usługą Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7829f-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="7829f-132">Aby zmienić informacje o takim użytkowniku, użyj narzędzi zarządzania lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7829f-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="7829f-133">Zarządzanie użytkownikami typu Gość i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="7829f-133">Guest user management and limitations</span></span>
<span data-ttu-id="7829f-134">Z konta gościa korzystają użytkownicy z innych katalogów, którzy otrzymali zaproszenie do katalogu w celu uzyskania dostępu do dokumentów programu SharePoint, aplikacji lub innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7829f-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="7829f-135">Podstawowy atrybut UserType na koncie gościa w katalogu jest ustawiony na opcję „Gość”.</span><span class="sxs-lookup"><span data-stu-id="7829f-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="7829f-136">Atrybut UserType normalnych użytkowników (w szczególności członków katalogu) jest ustawiony na opcję „Członek”.</span><span class="sxs-lookup"><span data-stu-id="7829f-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="7829f-137">Goście mają ograniczony zestaw praw w katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="7829f-138">Te prawa ograniczają gościom możliwość wyszukiwania informacji o innych użytkownikach w katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="7829f-139">Goście mogą jednak nadal współdziałać z użytkownikami i grupami skojarzonymi z zasobami, nad którymi pracują.</span><span class="sxs-lookup"><span data-stu-id="7829f-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="7829f-140">Goście mogą:</span><span class="sxs-lookup"><span data-stu-id="7829f-140">Guest users can:</span></span>

* <span data-ttu-id="7829f-141">Wyświetlać innych użytkowników i grupy skojarzone z subskrypcją platformy Azure, do której są przypisani</span><span class="sxs-lookup"><span data-stu-id="7829f-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="7829f-142">Wyświetlać członków grup, do których należą</span><span class="sxs-lookup"><span data-stu-id="7829f-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="7829f-143">Wyszukiwać innych użytkowników w katalogu, jeśli znają pełny adres e-mail użytkownika</span><span class="sxs-lookup"><span data-stu-id="7829f-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="7829f-144">Wyświetlać ograniczony zestaw atrybutów wyszukiwanych użytkowników — ograniczony do nazwy wyświetlanej, adresu e-mail, głównej nazwy użytkownika (UPN) i miniatury zdjęcia</span><span class="sxs-lookup"><span data-stu-id="7829f-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="7829f-145">Pobierać listę zweryfikowanych domen w katalogu</span><span class="sxs-lookup"><span data-stu-id="7829f-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="7829f-146">Wyrazić zgodę na aplikacje przydzielające im takie same prawa dostępu w katalogu, jakie mają członkowie</span><span class="sxs-lookup"><span data-stu-id="7829f-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="7829f-147">Ustawianie zasad dostępu dla gościa</span><span class="sxs-lookup"><span data-stu-id="7829f-147">Set guest user access policies</span></span>
<span data-ttu-id="7829f-148">Karta katalogu **Konfiguruj** zawiera opcje kontroli dostępu dla gości.</span><span class="sxs-lookup"><span data-stu-id="7829f-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="7829f-149">Te opcje mogą zostać zmienione wyłącznie za pośrednictwem klasycznego portalu Azure przez globalnego administratora katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="7829f-150">Obecnie nie ma metody robienia tego przez interfejs API lub program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7829f-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="7829f-151">Aby otworzyć kartę **Konfiguruj** w klasycznym portalu Azure, wybierz opcję **usługi Active Directory**, a następnie wybierz nazwę katalogu.</span><span class="sxs-lookup"><span data-stu-id="7829f-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Karta Konfigurowanie w usłudze Azure Active Directory][1]

<span data-ttu-id="7829f-153">Następnie możesz edytować opcje kontroli dostępu dla gości.</span><span class="sxs-lookup"><span data-stu-id="7829f-153">Then you can edit the options to control access for guest users.</span></span>

![Opcje kontroli dostępu dla gości][2]

## <a name="whats-next"></a><span data-ttu-id="7829f-155">Co dalej</span><span class="sxs-lookup"><span data-stu-id="7829f-155">What's next</span></span>
* [<span data-ttu-id="7829f-156">Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7829f-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="7829f-157">Administrowanie usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="7829f-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="7829f-158">Zarządzanie hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="7829f-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="7829f-159">Zarządzanie grupami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="7829f-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
