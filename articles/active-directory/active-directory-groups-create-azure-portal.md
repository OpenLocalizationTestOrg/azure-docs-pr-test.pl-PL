---
title: "aaaCreate grupę dla użytkowników w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toocreate grupy w usłudze Azure Active Directory i dodawanie członków grupy toohello"
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="0e454-103">Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e454-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e454-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0e454-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="0e454-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0e454-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="0e454-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e454-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="0e454-107">W tym artykule opisano sposób toocreate i wypełnić nową grupę w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e454-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="0e454-108">Użyj zadań zarządzania tooperform grupy, takich jak przypisywanie licencji lub uprawnienia tooa liczby użytkowników lub urządzeń naraz.</span><span class="sxs-lookup"><span data-stu-id="0e454-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="0e454-109">Jak utworzyć grupę?</span><span class="sxs-lookup"><span data-stu-id="0e454-109">How do I create a group?</span></span>
1. <span data-ttu-id="0e454-110">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="0e454-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="0e454-111">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0e454-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="0e454-113">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="0e454-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie hello grup bloku](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="0e454-115">Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz hello **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e454-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Polecenie Dodaj hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="0e454-117">Na powitania **grupy** bloku, Dodaj nazwę i opis grupy hello.</span><span class="sxs-lookup"><span data-stu-id="0e454-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="0e454-118">tooselect członków tooadd toohello grupy wybierz **przypisane** w hello **Typ członkostwa** , a następnie wybierz **członków**.</span><span class="sxs-lookup"><span data-stu-id="0e454-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="0e454-119">Aby uzyskać więcej informacji o sposobie toomanage hello członkostwa w grupie dynamicznie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady członkostwa w grupie](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0e454-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Wybieranie elementów członkowskich tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="0e454-121">Na powitania **członków** bloku, wybierz jedną lub więcej użytkowników lub urządzeń grupy toohello tooadd i wybierz hello **wybierz** przycisk u dołu hello hello bloku tooadd ich toohello grupy.</span><span class="sxs-lookup"><span data-stu-id="0e454-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="0e454-122">Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0e454-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="0e454-123">Nie symbole wieloznaczne są akceptowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="0e454-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="0e454-124">Po zakończeniu dodawania elementów członkowskich toohello grupy, wybierz **Utwórz** na powitania **grupy** bloku.</span><span class="sxs-lookup"><span data-stu-id="0e454-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Tworzenie grupy potwierdzenia](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="0e454-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e454-126">Next steps</span></span>
<span data-ttu-id="0e454-127">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e454-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0e454-128">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="0e454-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0e454-129">Zarządzanie ustawieniami grupy</span><span class="sxs-lookup"><span data-stu-id="0e454-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="0e454-130">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="0e454-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="0e454-131">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="0e454-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="0e454-132">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="0e454-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
