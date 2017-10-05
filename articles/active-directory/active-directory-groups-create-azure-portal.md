---
title: "Utwórz grupę dla użytkowników w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak utworzyć grupę w usłudze Azure Active Directory i dodawanie członków do grupy"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="bd022-103">Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd022-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd022-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd022-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="bd022-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd022-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="bd022-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd022-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="bd022-107">W tym artykule opisano sposób tworzenia i wypełniania nową grupę w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd022-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="bd022-108">Grupa służy do wykonywania zadań zarządzania, takich jak przypisywanie licencji lub uprawnień do liczby użytkowników lub urządzeń naraz.</span><span class="sxs-lookup"><span data-stu-id="bd022-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="bd022-109">Jak utworzyć grupę?</span><span class="sxs-lookup"><span data-stu-id="bd022-109">How do I create a group?</span></span>
1. <span data-ttu-id="bd022-110">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd022-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="bd022-111">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bd022-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="bd022-113">Na **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="bd022-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie bloku grupy](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="bd022-115">Na **użytkowników i grup — wszystkie grupy** bloku, wybierz opcję **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="bd022-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Dodaj polecenie](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="bd022-117">Na **grupy** bloku, Dodaj nazwę i opis grupy.</span><span class="sxs-lookup"><span data-stu-id="bd022-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="bd022-118">Aby wybrać elementy członkowskie, aby dodać do grupy, wybierz **przypisane** w **Typ członkostwa** , a następnie wybierz **członków**.</span><span class="sxs-lookup"><span data-stu-id="bd022-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="bd022-119">Aby uzyskać więcej informacji o sposobie zarządzania członkostwa w grupie dynamicznie, zobacz [tworzenie zaawansowanych reguł członkostwa w grupie za pomocą atrybutów](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd022-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Wybieranie członków do dodania](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="bd022-121">Na **członków** bloku, wybierz jeden lub więcej użytkowników lub urządzeń do dodania do grupy, a następnie wybierz **wybierz** przycisk w dolnej części bloku, aby dodać je do grupy.</span><span class="sxs-lookup"><span data-stu-id="bd022-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="bd022-122">**Użytkownika** okno filtry wyświetlania na podstawie zgodności wpis do dowolnej części nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bd022-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="bd022-123">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="bd022-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="bd022-124">Po zakończeniu dodawania członków do grupy, wybierz **Utwórz** na **grupy** bloku.</span><span class="sxs-lookup"><span data-stu-id="bd022-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Tworzenie grupy potwierdzenia](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="bd022-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd022-126">Next steps</span></span>
<span data-ttu-id="bd022-127">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd022-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bd022-128">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="bd022-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="bd022-129">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="bd022-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="bd022-130">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="bd022-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="bd022-131">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="bd022-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="bd022-132">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="bd022-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
