---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a><span data-ttu-id="6315c-103">Dodaj nowy tooAzure użytkowników usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="6315c-103">Add new users tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6315c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6315c-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="6315c-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6315c-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="6315c-106">W tym artykule opisano, jak tooadd nowych użytkowników w organizacji w hello Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6315c-106">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="6315c-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="6315c-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="6315c-108">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6315c-108">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie użytkowników i grup](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="6315c-110">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6315c-110">On hello **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Polecenie Dodaj hello](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="6315c-112">Wprowadź szczegóły użytkownika hello, takich jak **nazwa** i **nazwy użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6315c-112">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="6315c-113">części nazwy domeny Hello hello nazwa użytkownika musi być nazwa domeny "foo.onmicrosoft.com" nazwy domeny początkowej domyślne hello lub nazwę domeny zweryfikowane, niefederacyjnych, takie jak "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="6315c-113">hello domain name portion of hello user name must either be hello initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="6315c-114">Kopiowania lub w inny sposób hello Uwaga wygenerowane hasło użytkownika, dzięki czemu możesz podać go toohello użytkownika po zakończeniu tego procesu.</span><span class="sxs-lookup"><span data-stu-id="6315c-114">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="6315c-115">Opcjonalnie można otwierać i podanie informacji hello w hello **profilu** bloku, hello **grup** bloku lub hello **roli katalogu** bloku hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6315c-115">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="6315c-116">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6315c-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="6315c-117">Na powitania **użytkownika** bloku, wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6315c-117">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="6315c-118">Bezpiecznie należy rozpowszechnić hello wygenerowane hasło toohello nowego użytkownika, tak aby hello użytkownicy mogą się logować.</span><span class="sxs-lookup"><span data-stu-id="6315c-118">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="6315c-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6315c-119">Next steps</span></span>
* [<span data-ttu-id="6315c-120">Dodaj użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="6315c-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="6315c-121">Resetuj hasło użytkownika w hello nowego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6315c-121">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="6315c-122">Zmień informacje dotyczące pracy użytkownika</span><span class="sxs-lookup"><span data-stu-id="6315c-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="6315c-123">Zarządzanie profilami użytkowników</span><span class="sxs-lookup"><span data-stu-id="6315c-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="6315c-124">Usunięcie użytkownika w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6315c-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="6315c-125">Przypisz rolę użytkownika tooa w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6315c-125">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
