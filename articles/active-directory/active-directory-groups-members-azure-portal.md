---
title: "Zarządzanie członkami grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dodawanie i usuwanie użytkowników i urządzeń z grupy w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="bb2af-103">Zarządzanie członkostwami grup użytkowników w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb2af-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="bb2af-104">W tym artykule wyjaśniono, jak można zarządzać członkami grupy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb2af-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="bb2af-105">Jak znaleźć członków i zarządzać nimi?</span><span class="sxs-lookup"><span data-stu-id="bb2af-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="bb2af-106">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="bb2af-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="bb2af-107">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bb2af-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="bb2af-109">Na **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="bb2af-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie bloku grupy](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="bb2af-111">Na **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="bb2af-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="bb2af-112">Na **grupy - *groupname***  bloku, wybierz opcję **członków**.</span><span class="sxs-lookup"><span data-stu-id="bb2af-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Otwieranie bloku elementy członkowskie](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="bb2af-114">Aby dodać członków do grupy, na **grupy - członków** bloku, wybierz opcję **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="bb2af-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Dodaj polecenie elementy członkowskie](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="bb2af-116">Na **członków** bloku, wybierz jeden lub więcej użytkowników lub urządzeń do dodania do grupy, a następnie wybierz **wybierz** przycisk w dolnej części bloku, aby dodać je do grupy.</span><span class="sxs-lookup"><span data-stu-id="bb2af-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="bb2af-117">**Użytkownika** okno filtry wyświetlania na podstawie zgodności wpis do dowolnej części nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bb2af-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="bb2af-118">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="bb2af-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="bb2af-119">Aby usunąć członków z grupy, na **grupy - członków** bloku, wybierz element członkowski.</span><span class="sxs-lookup"><span data-stu-id="bb2af-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="bb2af-120">Na ***membername*** bloku, wybierz opcję **Usuń** polecenie i Potwierdź wybór w wierszu.</span><span class="sxs-lookup"><span data-stu-id="bb2af-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Usuń elementy członkowskie, polecenie](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="bb2af-122">Po zakończeniu zmiana członków grupy, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="bb2af-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="bb2af-123">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="bb2af-123">Additional information</span></span>
<span data-ttu-id="bb2af-124">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bb2af-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bb2af-125">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="bb2af-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="bb2af-126">Utwórz nową grupę i dodawanie członków</span><span class="sxs-lookup"><span data-stu-id="bb2af-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="bb2af-127">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="bb2af-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="bb2af-128">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="bb2af-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="bb2af-129">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="bb2af-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
