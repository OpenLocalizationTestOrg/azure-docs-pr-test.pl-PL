---
title: "Dodawanie nowych użytkowników do usługi Azure Active Directory | Microsoft Docs"
description: "Wyjaśnia, jak dodać nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
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
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="33921-103">Dodawanie nowych użytkowników do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33921-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33921-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33921-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="33921-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33921-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="33921-106">W tym artykule opisano sposób dodawania nowych użytkowników w organizacji w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33921-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="33921-107">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="33921-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="33921-108">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="33921-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie użytkowników i grup](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="33921-110">Na **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="33921-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Dodaj polecenie](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="33921-112">Wprowadź szczegóły użytkownika, takich jak **nazwa** i **nazwy użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="33921-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="33921-113">Część nazwy domeny nazwa użytkownika musi być domyślna początkowej nazwy domeny "foo.onmicrosoft.com" nazwa domeny lub nazwę domeny zweryfikowane, niefederacyjnych, takie jak "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="33921-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="33921-114">Skopiuj lub w przeciwnym razie należy pamiętać wygenerowane hasło, dzięki czemu można udostępnić go użytkownikowi po zakończeniu tego procesu.</span><span class="sxs-lookup"><span data-stu-id="33921-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="33921-115">Opcjonalnie można otwierać i Wypełnij informacje w **profilu** bloku **grup** bloku lub **roli katalogu** bloku dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33921-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="33921-116">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="33921-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="33921-117">Na **użytkownika** bloku, wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="33921-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="33921-118">Bezpiecznie dystrybucji wygenerowane hasło dla nowego użytkownika, dzięki czemu użytkownicy mogą się logować.</span><span class="sxs-lookup"><span data-stu-id="33921-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="33921-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33921-119">Next steps</span></span>
* [<span data-ttu-id="33921-120">Dodaj użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="33921-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="33921-121">Resetuj hasło użytkownika w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="33921-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="33921-122">Zmień informacje dotyczące pracy użytkownika</span><span class="sxs-lookup"><span data-stu-id="33921-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="33921-123">Zarządzanie profilami użytkowników</span><span class="sxs-lookup"><span data-stu-id="33921-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="33921-124">Usunięcie użytkownika w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="33921-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="33921-125">Przypisanie użytkownika do roli w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="33921-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
