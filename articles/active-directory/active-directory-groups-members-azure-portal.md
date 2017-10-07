---
title: "aaaManage hello członków grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooadd lub usuwanie użytkowników i urządzeń z grupy w usłudze Azure Active Directory"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="c45df-103">Zarządzanie członkostwami grup użytkowników w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c45df-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="c45df-104">W tym artykule opisano, jak toomanage hello członków grupy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c45df-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="c45df-105">Jak znaleźć członków hello i zarządzać nimi?</span><span class="sxs-lookup"><span data-stu-id="c45df-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="c45df-106">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="c45df-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c45df-107">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c45df-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="c45df-109">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="c45df-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie hello grup bloku](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="c45df-111">Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="c45df-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="c45df-112">Na powitania **grupy - *groupname***  bloku, wybierz opcję **członków**.</span><span class="sxs-lookup"><span data-stu-id="c45df-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Otwieranie hello członków bloku](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="c45df-114">tooadd grupy toohello elementy członkowskie, na powitania **grupy - członków** bloku, wybierz opcję **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="c45df-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Dodaj polecenie elementy członkowskie](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="c45df-116">Na powitania **członków** bloku, wybierz jedną lub więcej użytkowników lub urządzeń grupy toohello tooadd i wybierz hello **wybierz** przycisk u dołu hello hello bloku tooadd ich toohello grupy.</span><span class="sxs-lookup"><span data-stu-id="c45df-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="c45df-117">Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c45df-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="c45df-118">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="c45df-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="c45df-119">tooremove członków z grupy hello na powitania **grupy - członków** bloku, wybierz element członkowski.</span><span class="sxs-lookup"><span data-stu-id="c45df-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="c45df-120">Na powitania ***membername*** bloku, wybierz hello **Usuń** polecenie i Potwierdź wybór hello w wierszu.</span><span class="sxs-lookup"><span data-stu-id="c45df-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Usuń elementy członkowskie, polecenie](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="c45df-122">Po zakończeniu zmiana członków grupy hello, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c45df-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c45df-123">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="c45df-123">Additional information</span></span>
<span data-ttu-id="c45df-124">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c45df-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c45df-125">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="c45df-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c45df-126">Utwórz nową grupę i dodawanie członków</span><span class="sxs-lookup"><span data-stu-id="c45df-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="c45df-127">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="c45df-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="c45df-128">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="c45df-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="c45df-129">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="c45df-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
