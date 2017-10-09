---
title: "na podstawie aaaRole kontroli dostępu w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Rozpocznij zarządzanie dostępem z opartej na rolach kontrola dostępu w portalu Azure hello. Użyj roli przypisania tooassign uprawnienia tooyour zasobów."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="7a118-104">Korzystanie z kontroli dostępu opartej na rolach toomanage dostępu tooyour subskrypcji platformy Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="7a118-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a118-105">Zarządzanie dostępem użytkowników lub grup</span><span class="sxs-lookup"><span data-stu-id="7a118-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="7a118-106">Zarządzanie dostępem do zasobów</span><span class="sxs-lookup"><span data-stu-id="7a118-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="7a118-107">Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7a118-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="7a118-108">Przy użyciu funkcji RBAC, można udzielić tylko hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="7a118-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="7a118-109">W tym artykule opisano, jak rozpocząć pracę z RBAC w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7a118-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="7a118-110">Jeśli chcesz uzyskać więcej szczegółowych informacji na temat sposobu, w jaki RBAC ułatwia zarządzanie dostępem, zobacz [Co to jest kontrola dostępu oparta na rolach](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="7a118-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="7a118-111">W ramach każdej subskrypcji można przyznać się too2000 przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="7a118-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="7a118-112">Wyświetlanie dostępu</span><span class="sxs-lookup"><span data-stu-id="7a118-112">View access</span></span>
<span data-ttu-id="7a118-113">Można zobaczyć, kto ma dostęp do zasobów tooa, grupy zasobów lub subskrypcji z głównego bloku hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a118-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7a118-114">Na przykład chcemy toosee, kto ma dostęp tooone naszych grup zasobów:</span><span class="sxs-lookup"><span data-stu-id="7a118-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="7a118-115">Wybierz **grup zasobów** hello pasku nawigacyjnym po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="7a118-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="7a118-116">![Grupy zasobów — ikona](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="7a118-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="7a118-117">Witaj wybierz nazwę grupy zasobów hello z hello **grup zasobów** bloku.</span><span class="sxs-lookup"><span data-stu-id="7a118-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="7a118-118">Wybierz **(IAM) kontroli dostępu** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="7a118-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="7a118-119">blok kontroli dostępu Hello zawiera listę wszystkich użytkowników, grup i aplikacji, które zostały przyznane grupy zasobów toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="7a118-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Blok użytkowników — dostęp dziedziczony a przypisany (zrzut ekranu)](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="7a118-121">Zwróć uwagę, zbyt ograniczone niektóre role**tego zasobu** a inne **dziedziczonych** go z innym zakresem.</span><span class="sxs-lookup"><span data-stu-id="7a118-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="7a118-122">Dostępu jest przypisane w szczególności toohello grupy zasobów albo dziedziczony z subskrypcji nadrzędnej toohello przypisania.</span><span class="sxs-lookup"><span data-stu-id="7a118-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7a118-123">Klasyczni Administratorzy i współadministratorzy są traktowani jako właściciele subskrypcji hello w nowym modelu RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="7a118-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="7a118-124">Dodawanie dostępu</span><span class="sxs-lookup"><span data-stu-id="7a118-124">Add Access</span></span>
<span data-ttu-id="7a118-125">Można przyznać dostęp z wewnątrz hello zasobu, grupy zasobów lub subskrypcji, która jest zakresem hello hello przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="7a118-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="7a118-126">Wybierz **Dodaj** w bloku kontroli dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="7a118-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="7a118-127">Czy chcesz tooassign z hello roli wybierz hello **wybierz rolę** bloku.</span><span class="sxs-lookup"><span data-stu-id="7a118-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="7a118-128">Wybierz użytkownika hello, grupę lub aplikację w katalogu, który ma dostęp toogrant do.</span><span class="sxs-lookup"><span data-stu-id="7a118-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="7a118-129">Można przeszukiwać katalog hello o nazw wyświetlanych, adresów e-mail i identyfikatorów obiektów.</span><span class="sxs-lookup"><span data-stu-id="7a118-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Blok dodawania użytkowników — zrzut ekranu wyszukiwania](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="7a118-131">Wybierz **OK** toocreate hello przypisania.</span><span class="sxs-lookup"><span data-stu-id="7a118-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="7a118-132">Witaj **Dodawanie użytkownika** podręcznego śledzi postęp hello.</span><span class="sxs-lookup"><span data-stu-id="7a118-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="7a118-133">![Pasek postępu dodawania użytkownika — zrzut ekranu](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="7a118-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="7a118-134">Po pomyślnym dodaniu przypisania roli, pojawi się na powitania **użytkowników** bloku.</span><span class="sxs-lookup"><span data-stu-id="7a118-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="7a118-135">Usuwanie dostępu</span><span class="sxs-lookup"><span data-stu-id="7a118-135">Remove Access</span></span>
1. <span data-ttu-id="7a118-136">Wskaźnik nad hello nazwy przypisania hello, które mają tooremove.</span><span class="sxs-lookup"><span data-stu-id="7a118-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="7a118-137">Pole wyboru zostanie wyświetlona nazwa toohello dalej.</span><span class="sxs-lookup"><span data-stu-id="7a118-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="7a118-138">Użyj hello tooselect pola wyboru jednego lub więcej przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="7a118-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="7a118-139">Wybierz pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="7a118-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="7a118-140">Wybierz **tak** tooconfirm hello usuwania.</span><span class="sxs-lookup"><span data-stu-id="7a118-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="7a118-141">Przypisań dziedziczonych nie można usunąć.</span><span class="sxs-lookup"><span data-stu-id="7a118-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="7a118-142">Tooremove dziedziczone przypisania, należy należy toodo go na powitania zakresu, której utworzono hello przypisania roli.</span><span class="sxs-lookup"><span data-stu-id="7a118-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="7a118-143">W hello **zakres** kolumny, obok zbyt**dziedziczonych** jest łącze, które umożliwia przejście zasobów toohello gdy ta rola została przypisana.</span><span class="sxs-lookup"><span data-stu-id="7a118-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="7a118-144">Przejście zasobu toohello podane przypisania roli hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="7a118-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Blok Użytkownicy — dostęp dziedziczony wyłącza przycisk usuwania (zrzut ekranu)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="7a118-146">Inne narzędzia toomanage dostępu</span><span class="sxs-lookup"><span data-stu-id="7a118-146">Other tools toomanage access</span></span>
<span data-ttu-id="7a118-147">Można przypisywać role i Zarządzaj dostępem za pomocą poleceń Azure RBAC w narzędziach innych niż hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7a118-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="7a118-148">Wykonaj toolearn łącza hello więcej o warunkach wstępnych hello i wprowadzenie do poleceń Azure RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="7a118-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="7a118-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a118-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="7a118-150">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7a118-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="7a118-151">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7a118-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="7a118-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a118-152">Next Steps</span></span>
* [<span data-ttu-id="7a118-153">Tworzenie raportu historii zmian dostępu</span><span class="sxs-lookup"><span data-stu-id="7a118-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="7a118-154">Zobacz hello [wbudowane role RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="7a118-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="7a118-155">Definiowanie własnych [niestandardowych ról dla kontroli dostępu opartej na rolach na platformie Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="7a118-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

