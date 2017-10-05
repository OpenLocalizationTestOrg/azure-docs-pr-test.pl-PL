---
title: "Zarządzanie właściwościami grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak edytować właściwości i inne ustawienia konfiguracji dla grupy w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2f058f9a-5a8f-4b4b-b3b7-885ff10cb1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: b4baccafc0a9178223dbf64c664fc34ab9f7f916
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-the-settings-for-a-group-in-azure-active-directory"></a><span data-ttu-id="4a44e-103">Zarządzanie ustawieniami grupy w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a44e-103">Manage the settings for a group in Azure Active Directory</span></span>
<span data-ttu-id="4a44e-104">W tym artykule wyjaśniono, jak zmienić ustawienia grupy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a44e-104">This article explains how to change the settings for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-and-change-the-settings"></a><span data-ttu-id="4a44e-105">Jak znaleźć i zmienić ustawienia?</span><span class="sxs-lookup"><span data-stu-id="4a44e-105">How do I find and change the settings?</span></span>
1. <span data-ttu-id="4a44e-106">Zaloguj się w [centrum administracyjnym usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="4a44e-106">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4a44e-107">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4a44e-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Otwieranie użytkowników i grup bloku](./media/active-directory-groups-settings-azure-portal/search-user-management.png)
3. <span data-ttu-id="4a44e-109">Na **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="4a44e-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Otwieranie wszystkich bloku grupy](./media/active-directory-groups-settings-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="4a44e-111">Na **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="4a44e-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="4a44e-112">Na **grupy - *groupname***  bloku, wybierz opcję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="4a44e-112">On the **Group - *groupname*** blade, select **Properties**.</span></span>

   ![Otwieranie bloku właściwości](./media/active-directory-groups-settings-azure-portal/select-group-properties.png)
6. <span data-ttu-id="4a44e-114">Gdy skończysz, zmiana właściwości grupy, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4a44e-114">When you finish changing properties for the group, select **Save**.</span></span>    

   ![Trwa zapisywanie zmian właściwości](./media/active-directory-groups-settings-azure-portal/save-group-properties.png)

## <a name="next-steps"></a><span data-ttu-id="4a44e-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a44e-116">Next steps</span></span>
<span data-ttu-id="4a44e-117">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a44e-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4a44e-118">Zobacz istniejących grup</span><span class="sxs-lookup"><span data-stu-id="4a44e-118">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4a44e-119">Utwórz nową grupę i dodawanie członków</span><span class="sxs-lookup"><span data-stu-id="4a44e-119">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="4a44e-120">Elementy członkowskie grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="4a44e-120">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="4a44e-121">Zarządzanie członkostwami grup</span><span class="sxs-lookup"><span data-stu-id="4a44e-121">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="4a44e-122">Dynamiczne reguły dla użytkowników w grupie zarządzania</span><span class="sxs-lookup"><span data-stu-id="4a44e-122">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
