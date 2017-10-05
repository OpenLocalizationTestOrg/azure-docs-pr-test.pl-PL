---
title: "Zarządzanie grupami w usłudze Azure Active Directory należy grupy | Dokumentacja firmy Microsoft"
description: "Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak zarządzać tymi członkostwa."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="454a3-104">Zarządzania do grupy, które grupy należy w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="454a3-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="454a3-105">Grupy mogą zawierać inne grupy w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="454a3-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="454a3-106">Oto jak zarządzać tymi członkostwa.</span><span class="sxs-lookup"><span data-stu-id="454a3-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="454a3-107">Jak znaleźć Moja grupa jest członkiem grupy?</span><span class="sxs-lookup"><span data-stu-id="454a3-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="454a3-108">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="454a3-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="454a3-109">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="454a3-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="454a3-111">Na **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="454a3-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie bloku grupy](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="454a3-113">Na **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="454a3-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="454a3-114">Na **grupy - *groupname***  bloku, wybierz opcję **członkostw**.</span><span class="sxs-lookup"><span data-stu-id="454a3-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Otwieranie bloku członkostwa grupy](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="454a3-116">Aby dodać grupy jako członka innej grupy, na **Group - członkostw** bloku, wybierz opcję **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="454a3-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="454a3-117">Wybierz grupę z **Wybieranie grupy** bloku, a następnie wybierz **wybierz** przycisk w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="454a3-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="454a3-118">Grupy można dodać tylko do jednej grupy naraz.</span><span class="sxs-lookup"><span data-stu-id="454a3-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="454a3-119">**Użytkownika** okno filtry wyświetlania na podstawie zgodności wpis do dowolnej części nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="454a3-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="454a3-120">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="454a3-120">No wildcard characters are accepted in that box.</span></span>

   ![Dodaj członkostwa w grupie](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="454a3-122">Aby usunąć grupy jako członka innej grupy, na **Group - członkostw** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="454a3-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="454a3-123">Na ***groupname*** bloku, wybierz opcję **Usuń** polecenie i Potwierdź wybór w wierszu.</span><span class="sxs-lookup"><span data-stu-id="454a3-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Usuń polecenie członkostwa](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="454a3-125">Po zakończeniu zmiany członkostwa w grupach dla Twojej grupy zaznacz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="454a3-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="454a3-126">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="454a3-126">Additional information</span></span>
<span data-ttu-id="454a3-127">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="454a3-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="454a3-128">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="454a3-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="454a3-129">Utwórz nową grupę i dodawanie członków</span><span class="sxs-lookup"><span data-stu-id="454a3-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="454a3-130">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="454a3-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="454a3-131">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="454a3-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="454a3-132">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="454a3-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
