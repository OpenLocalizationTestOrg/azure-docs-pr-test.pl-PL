---
title: "Przypisz użytkownika do ról administratora w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak zmienić administratora informacje o użytkowniku w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="52fcb-103">Przypisz użytkownika do ról administratora w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52fcb-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="52fcb-104">W tym artykule opisano sposób przypisywania roli administracyjnej dla użytkownika w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52fcb-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="52fcb-105">Aby uzyskać informacje dotyczące dodawania nowych użytkowników w organizacji, zobacz [Dodawanie nowych użytkowników do usługi Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="52fcb-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="52fcb-106">Dodani użytkownicy domyślnie nie mają uprawnień administratora, ale możesz przypisać im role w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="52fcb-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="52fcb-107">Przypisywanie użytkownikowi roli</span><span class="sxs-lookup"><span data-stu-id="52fcb-107">Assign a role to a user</span></span>
1. <span data-ttu-id="52fcb-108">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="52fcb-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="52fcb-109">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="52fcb-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="52fcb-111">Na **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="52fcb-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Otwieranie bloku wszystkich użytkowników](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="52fcb-113">Na **użytkowników i grup — wszyscy użytkownicy** bloku, wybierz użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="52fcb-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="52fcb-114">W bloku dla wybranego użytkownika, wybierz **roli katalogu**, a następnie przypisz użytkownika do roli **roli katalogu** listy.</span><span class="sxs-lookup"><span data-stu-id="52fcb-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="52fcb-115">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="52fcb-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Przypisanie użytkownika do roli](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="52fcb-117">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="52fcb-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52fcb-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52fcb-118">Next steps</span></span>
* [<span data-ttu-id="52fcb-119">Dodaj użytkownika</span><span class="sxs-lookup"><span data-stu-id="52fcb-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="52fcb-120">Resetuj hasło użytkownika w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52fcb-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="52fcb-121">Zmień informacje dotyczące pracy użytkownika</span><span class="sxs-lookup"><span data-stu-id="52fcb-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="52fcb-122">Zarządzanie profilami użytkowników</span><span class="sxs-lookup"><span data-stu-id="52fcb-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="52fcb-123">Usunięcie użytkownika w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52fcb-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
