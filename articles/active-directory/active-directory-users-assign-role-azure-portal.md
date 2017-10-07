---
title: "aaaAssign użytkownika tooadministrator ról w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak toochange administracyjne informacje o użytkowniku w usłudze Azure Active Directory"
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
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="271f6-103">Przypisywanie ról tooadministrator w usłudze Azure Active Directory użytkownika</span><span class="sxs-lookup"><span data-stu-id="271f6-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="271f6-104">W tym artykule opisano sposób tooassign użytkownika tooa roli administracyjnej w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="271f6-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="271f6-105">Aby uzyskać informacje dotyczące dodawania nowych użytkowników w organizacji, zobacz [Dodaj nowe tooAzure użytkowników usługi Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="271f6-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="271f6-106">Dodano użytkownicy nie mają uprawnień administratora domyślnie, ale można przypisać toothem role w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="271f6-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="271f6-107">Przypisywanie roli użytkownika tooa</span><span class="sxs-lookup"><span data-stu-id="271f6-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="271f6-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="271f6-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="271f6-109">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="271f6-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="271f6-111">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="271f6-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![Otwieranie hello blok wszystkich użytkowników](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="271f6-113">Na powitania **użytkowników i grup — wszyscy użytkownicy** bloku, wybierz użytkownika z listy hello.</span><span class="sxs-lookup"><span data-stu-id="271f6-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="271f6-114">W bloku hello hello wybranego użytkownika, wybierz **roli katalogu**, a następnie przypisz rolę tooa użytkownika hello z hello **roli katalogu** listy.</span><span class="sxs-lookup"><span data-stu-id="271f6-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="271f6-115">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="271f6-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Przypisywanie roli tooa użytkownika](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="271f6-117">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="271f6-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="271f6-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="271f6-118">Next steps</span></span>
* [<span data-ttu-id="271f6-119">Dodaj użytkownika</span><span class="sxs-lookup"><span data-stu-id="271f6-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="271f6-120">Resetuj hasło użytkownika w hello nowego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="271f6-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="271f6-121">Zmień informacje dotyczące pracy użytkownika</span><span class="sxs-lookup"><span data-stu-id="271f6-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="271f6-122">Zarządzanie profilami użytkowników</span><span class="sxs-lookup"><span data-stu-id="271f6-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="271f6-123">Usunięcie użytkownika w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="271f6-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
