---
title: "grupy hello aaaManage grupy należy tooin usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak toomanage tych członkostwa."
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
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="fa91d-104">Zarządzanie grupami toowhich, do której należy grupa w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa91d-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="fa91d-105">Grupy mogą zawierać inne grupy w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa91d-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="fa91d-106">Oto jak toomanage tych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="fa91d-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="fa91d-107">Jak znaleźć Moja grupa jest członkiem grupy hello?</span><span class="sxs-lookup"><span data-stu-id="fa91d-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="fa91d-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="fa91d-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="fa91d-109">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa91d-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="fa91d-111">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="fa91d-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie hello grup bloku](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="fa91d-113">Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="fa91d-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="fa91d-114">Na powitania **grupy - *groupname***  bloku, wybierz opcję **członkostw**.</span><span class="sxs-lookup"><span data-stu-id="fa91d-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Otwieranie hello grupy członkostwa w bloku](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="fa91d-116">tooadd grupy jako członka innej grupy, na powitania **Group - członkostw** bloku, wybierz hello **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa91d-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="fa91d-117">Wybierz grupę z hello **Wybieranie grupy** bloku, a następnie wybierz opcję hello **wybierz** przycisk u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="fa91d-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="fa91d-118">Można dodać grupy tooonly jednej grupy naraz.</span><span class="sxs-lookup"><span data-stu-id="fa91d-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="fa91d-119">Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fa91d-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="fa91d-120">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="fa91d-120">No wildcard characters are accepted in that box.</span></span>

   ![Dodaj członkostwa w grupie](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="fa91d-122">tooremove grupy jako członka innej grupy, na powitania **Group - członkostw** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="fa91d-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="fa91d-123">Na powitania ***groupname*** bloku, wybierz hello **Usuń** polecenie i Potwierdź wybór hello w wierszu.</span><span class="sxs-lookup"><span data-stu-id="fa91d-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Usuń polecenie członkostwa](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="fa91d-125">Po zakończeniu zmiany członkostwa w grupach dla Twojej grupy zaznacz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fa91d-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="fa91d-126">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="fa91d-126">Additional information</span></span>
<span data-ttu-id="fa91d-127">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa91d-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="fa91d-128">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="fa91d-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="fa91d-129">Utwórz nową grupę i dodawanie członków</span><span class="sxs-lookup"><span data-stu-id="fa91d-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="fa91d-130">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="fa91d-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="fa91d-131">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="fa91d-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="fa91d-132">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="fa91d-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
