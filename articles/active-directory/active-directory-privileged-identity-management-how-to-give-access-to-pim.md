---
title: "Jak zapewnić dostęp do Privileged Identity Management - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać role użytkowników na podstawie rozszerzenia usługi Azure Active Directory Privileged Identity Management, którymi zarządzają usługi PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="e19e0-103">Przyznawanie dostępu do zarządzania usługi Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e19e0-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e19e0-104">Administrator globalny, który umożliwia usłudze Azure AD Privileged Identity Management (PIM) dla organizacji, automatycznie pobrać przypisania ról i dostępu do usługi PIM.</span><span class="sxs-lookup"><span data-stu-id="e19e0-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="e19e0-105">Nikt pobiera zapisu domyślnie, łącznie z innych administratorów globalnych.</span><span class="sxs-lookup"><span data-stu-id="e19e0-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="e19e0-106">Inne globalne Administratorzy, administratorów zabezpieczeń i czytników zabezpieczeń mają dostęp tylko do odczytu do usługi Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="e19e0-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="e19e0-107">Aby udzielić dostępu do usługi PIM, pierwszego użytkownika można przypisać użytkownikom **administrator ról uprzywilejowanych** roli.</span><span class="sxs-lookup"><span data-stu-id="e19e0-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="e19e0-108">Ten przydział musi być wykonywane za pomocą programu PIM się i nie można zmienić za pomocą programu PowerShell lub innych portalach.</span><span class="sxs-lookup"><span data-stu-id="e19e0-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="e19e0-109">Zarządzanie programem Azure AD PIM wymaga usługi Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="e19e0-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="e19e0-110">Ponieważ konta Microsoft nie można zarejestrować dla usługi Azure MFA, użytkownik, który zaloguje się za pomocą konta Microsoft nie może uzyskać dostępu usługi Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="e19e0-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="e19e0-111">Upewnij się, zawsze istnieją co najmniej dwóch użytkowników należących do roli administrator ról uprzywilejowanych w przypadku, gdy jeden użytkownik jest zablokowany lub ich konto zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="e19e0-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="e19e0-112">Udostępnij innym użytkownika do zarządzania PIM</span><span class="sxs-lookup"><span data-stu-id="e19e0-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="e19e0-113">Zaloguj się do [portalu Azure](https://portal.azure.com/) i wybierz **Azure AD Privileged Identity Management** aplikacji na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e19e0-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="e19e0-114">Wybierz **Zarządzanie ról uprzywilejowanych** > **administrator ról uprzywilejowanych** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e19e0-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Dodawanie ról uprzywilejowanych administratorów — zrzut ekranu][1]
3. <span data-ttu-id="e19e0-116">W bloku użytkowników zarządzanych Dodaj krok 1 została już ukończona.</span><span class="sxs-lookup"><span data-stu-id="e19e0-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="e19e0-117">Zaznacz krok 2, **Wybierz użytkowników** i Wyszukaj użytkownika, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="e19e0-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Wybierz użytkowników — zrzut ekranu][2]
4. <span data-ttu-id="e19e0-119">Wybierz użytkownika z wyników wyszukiwania, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e19e0-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="e19e0-120">Kliknij przycisk **OK** Aby zapisać wybrane opcje.</span><span class="sxs-lookup"><span data-stu-id="e19e0-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="e19e0-121">Użytkownik, który wybrano będą wyświetlane na liście ról uprzywilejowanych administratorów.</span><span class="sxs-lookup"><span data-stu-id="e19e0-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="e19e0-122">Zawsze, gdy przypisaniu roli dla kogoś, kto ich są automatycznie konfigurowane jako kwalifikujących się do aktywowania roli.</span><span class="sxs-lookup"><span data-stu-id="e19e0-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="e19e0-123">Jeśli chcesz uczynić je stałym w tej roli, kliknij użytkownika na liście.</span><span class="sxs-lookup"><span data-stu-id="e19e0-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="e19e0-124">Wybierz **upewnij uprawnienie** w menu informacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e19e0-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="e19e0-125">Wyślij łącze do użytkownika [wprowadzenie do korzystania z usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e19e0-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="e19e0-126">Usuwanie praw dostępu przez innego użytkownika do zarządzania usługi PIM</span><span class="sxs-lookup"><span data-stu-id="e19e0-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="e19e0-127">Zawsze przed usunięciem ktoś z roli administrator ról uprzywilejowanych, upewnij się, nadal będą dwóch użytkowników przypisanych do niej.</span><span class="sxs-lookup"><span data-stu-id="e19e0-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="e19e0-128">Na pulpicie nawigacyjnym usługi PIM kliknij rolę **administrator ról uprzywilejowanych**.</span><span class="sxs-lookup"><span data-stu-id="e19e0-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="e19e0-129">Zostanie wyświetlona lista użytkowników obecnie w tej roli.</span><span class="sxs-lookup"><span data-stu-id="e19e0-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="e19e0-130">Kliknij na użytkownika na liście użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e19e0-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="e19e0-131">Polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="e19e0-131">Click on **Remove**.</span></span>  <span data-ttu-id="e19e0-132">Otrzymasz komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="e19e0-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="e19e0-133">Kliknij przycisk **tak** Aby usunąć użytkownika z roli.</span><span class="sxs-lookup"><span data-stu-id="e19e0-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="e19e0-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e19e0-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
