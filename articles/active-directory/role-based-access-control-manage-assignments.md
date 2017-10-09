---
title: "przydziały dostępu do zasobów platformy Azure aaaView | Dokumentacja firmy Microsoft"
description: "Wyświetl i zarządzaj nimi wszystkie hello przypisania opartej na rolach kontroli dostępu dla dowolnego użytkownika lub grupę w hello portalu Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="620ac-103">Wyświetl przypisania dostępu dla użytkowników i grup w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="620ac-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="620ac-104">Zarządzanie dostępem użytkowników lub grup</span><span class="sxs-lookup"><span data-stu-id="620ac-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="620ac-105">Zarządzanie dostępem do zasobów</span><span class="sxs-lookup"><span data-stu-id="620ac-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="620ac-106">Kontrola dostępu oparta na rolach (RBAC) w hello Azure Active Directory (Azure AD), można zarządzać access tooyour Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="620ac-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="620ac-107">Dostęp z RBAC przypisaną jest szczegółowych, ponieważ można ograniczyć uprawnienia hello na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="620ac-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="620ac-108">**Zakres:** przypisania roli RBAC są zakresami tooa określonej subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="620ac-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="620ac-109">Podana pojedynczego zasobu tooa dostępu przez użytkownika nie może uzyskać dostępu żadnych innych zasobów w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="620ac-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="620ac-110">**Rola:** zakresu hello przypisania hello jest zawężony dostępu nawet dalsze przez przypisanie roli.</span><span class="sxs-lookup"><span data-stu-id="620ac-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="620ac-111">Role można wysokiego poziomu, takich jak właściciela lub określonych, takich jak czytnik maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="620ac-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="620ac-112">Role można przypisać tylko z wewnątrz hello subskrypcji, grupy zasobów lub zasobu, który jest zakresem hello hello przypisania.</span><span class="sxs-lookup"><span data-stu-id="620ac-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="620ac-113">Jednak można wyświetlić wszystkie przypisania dostępu powitania dla danego użytkownika lub grupy w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="620ac-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="620ac-114">Użytkownik może zawierać maksymalnie too2000 przypisania roli w każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="620ac-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="620ac-115">Uzyskaj więcej informacji o tym, jak za[Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="620ac-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="620ac-116">Wyświetl dostępu przypisania</span><span class="sxs-lookup"><span data-stu-id="620ac-116">View access assignments</span></span>
<span data-ttu-id="620ac-117">toolook się hello przypisań dostępu dla jednego użytkownika lub grupę, uruchom w usłudze Azure Active Directory w hello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="620ac-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="620ac-118">Wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="620ac-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="620ac-119">Jeśli ta opcja nie jest widoczna na liście nawigacji, wybierz **więcej usług** , a następnie przewiń w dół toofind **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="620ac-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="620ac-120">Wybierz **użytkowników i grup**, a następnie albo **wszyscy użytkownicy** lub **wszystkich grup**.</span><span class="sxs-lookup"><span data-stu-id="620ac-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="620ac-121">Na przykład możemy skupić się na poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="620ac-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="620ac-122">![Zarządzaj użytkownikami i grupami w usłudze Azure Active Directory — zrzut ekranu](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="620ac-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="620ac-123">Wyszukiwanie hello użytkownika według nazwy lub nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="620ac-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="620ac-124">Wybierz **zasobów Azure** na powitania użytkownika bloku.</span><span class="sxs-lookup"><span data-stu-id="620ac-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="620ac-125">Są wyświetlane wszystkie hello przypisania dostępu dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="620ac-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="620ac-126">Przydziały tooview uprawnienia do odczytu</span><span class="sxs-lookup"><span data-stu-id="620ac-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="620ac-127">Ta strona zawiera tylko przypisania dostępu hello czy masz uprawnienie tooread.</span><span class="sxs-lookup"><span data-stu-id="620ac-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="620ac-128">Na przykład mieć dostęp do odczytu toosubscription A i przejdź toocheck bloku zasobów Azure toohello przypisania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="620ac-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="620ac-129">Można wyświetlać swoje przydziały dostępu dla subskrypcji A, ale nie widzi ona również ma dostęp do przypisania na subskrypcji B.</span><span class="sxs-lookup"><span data-stu-id="620ac-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="620ac-130">Usuwanie przypisania dostępu</span><span class="sxs-lookup"><span data-stu-id="620ac-130">Delete access assignments</span></span>
<span data-ttu-id="620ac-131">Z tego bloku można usunąć przypisania dostępu, które zostały przypisane bezpośrednio tooa użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="620ac-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="620ac-132">Jeśli przypisanie dostępu hello została odziedziczona z grupy nadrzędnej, wymaga toogo toohello zasobów lub subskrypcji i zarządzanie hello przypisania.</span><span class="sxs-lookup"><span data-stu-id="620ac-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="620ac-133">Z listy hello wszystkie hello przypisania dostępu dla użytkownika lub grupy wybierz hello, co ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="620ac-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="620ac-134">Wybierz **Usuń** , a następnie **tak** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="620ac-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="620ac-135">![Usuń przypisanie dostępu — zrzut ekranu](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="620ac-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="620ac-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="620ac-136">Next steps</span></span>

* <span data-ttu-id="620ac-137">Rozpoczynanie pracy z kontroli dostępu opartej na rolach zbyt[Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="620ac-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="620ac-138">Zobacz hello [wbudowane role RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="620ac-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

