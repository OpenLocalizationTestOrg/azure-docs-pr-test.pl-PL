---
title: "portal aaaAzure zasady zasobów | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse toocreate portalu Azure Resource Manager zasad i zarządzania nimi. Zasady można stosować na powitania grupy zasobów lub subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="973cc-104">Użyj tooassign portalu Azure i zarządzanie zasadami zasobów</span><span class="sxs-lookup"><span data-stu-id="973cc-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="973cc-105">Witaj portalu Azure umożliwia możesz tooassign zasady tooresource grup zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="973cc-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="973cc-106">Interfejs użytkownika Hello umożliwia łatwe tooselect hello zasad mają tooassign i podaj wartości parametrów dla tej zasady toocustomize hello ustawienia zasad.</span><span class="sxs-lookup"><span data-stu-id="973cc-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="973cc-107">tooassign zasad za pośrednictwem portalu hello definicji zasad hello musi już istnieć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="973cc-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="973cc-108">Subskrypcja obejmuje kilka definicje wbudowanych zasad, które są gotowe do momentu tooassign tooresource grupy lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="973cc-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="973cc-109">Widzisz tych zasad wbudowanych i niestandardowych zasad, które zdefiniowano przy użyciu zasad portalu tooassign hello.</span><span class="sxs-lookup"><span data-stu-id="973cc-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="973cc-110">Wprowadzenie toopolicies i jak toodefine dostosowane zasady, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="973cc-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="973cc-111">Zasady są dziedziczone przez wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="973cc-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="973cc-112">Jeśli zasady są stosowane tooa grupy zasobów, jest odpowiednie tooall hello zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="973cc-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="973cc-113">W tym artykule określenie hello **zakres** odwołuje się toohello grupy zasobów lub subskrypcji, która jest przypisana hello zasad.</span><span class="sxs-lookup"><span data-stu-id="973cc-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="973cc-114">Zasady są oceniane podczas tworzenia i aktualizowania zasobów (PUT i poprawka operacji).</span><span class="sxs-lookup"><span data-stu-id="973cc-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="973cc-115">Przypisać zasady</span><span class="sxs-lookup"><span data-stu-id="973cc-115">Assign a policy</span></span>

1. <span data-ttu-id="973cc-116">tooassign tooeither zasad grupy zasobów lub subskrypcji, należy wybrać odpowiednie grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="973cc-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="973cc-117">W ustawieniach hello wybierz **zasad**.</span><span class="sxs-lookup"><span data-stu-id="973cc-117">In hello settings, select **Policies**.</span></span>

   ![Wybieranie zasad](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="973cc-119">Wybierz przypisanie zasad dla tego zakresu toocreate **Dodaj przypisanie**.</span><span class="sxs-lookup"><span data-stu-id="973cc-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![Dodaj przypisania](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="973cc-121">Wybierz zasady hello ma tooassign.</span><span class="sxs-lookup"><span data-stu-id="973cc-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="973cc-122">Nawet jeśli nie dodano żadnych subskrypcji tooyour definicje zasad, zobacz się hello wbudowanych zasad, które są dostępne do przypisania.</span><span class="sxs-lookup"><span data-stu-id="973cc-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="973cc-123">Zasady te wbudowane obejmują wiele typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="973cc-123">These built-in policies cover many common scenarios.</span></span>

   ![Wybierz definicję](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="973cc-125">Po wybraniu zasad, zobacz opis zasad hello i wszelkie parametry dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="973cc-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="973cc-126">Na przykład hello poniższy obraz przedstawia hello **dozwolone lokalizacje** parametr, który jest wymagany dla hello zasadę, która ogranicza hello dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="973cc-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![Pokaż parametry](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="973cc-128">Za pomocą interfejsu użytkownika hello wybierz hello toospecify wartości dla parametrów zasad hello (na przykład hello lokalizacje, które mogą być używane do wdrożenia).</span><span class="sxs-lookup"><span data-stu-id="973cc-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![Wybierz wartości parametrów](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="973cc-130">Podaj wartości hello innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="973cc-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="973cc-131">zakres Hello zostanie automatycznie przypisany oparte na powitania bloku, wybranych podczas uruchamiania hello przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="973cc-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="973cc-132">Po zakończeniu wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="973cc-132">Select **OK** when done.</span></span>

   ![Zdefiniuj parametry](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="973cc-134">Przypisaniu zasad hello toohello określony zakres.</span><span class="sxs-lookup"><span data-stu-id="973cc-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="973cc-135">Wyświetl przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="973cc-135">View policy assignments</span></span>

<span data-ttu-id="973cc-136">Po przypisaniu zasad, zobacz liście hello zasad dla tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="973cc-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="973cc-137">Witaj **szczegóły** karta zawiera podsumowanie hello przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="973cc-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![Pokaż szczegóły](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="973cc-139">Witaj **zasada przypisania** karcie są wyświetlane hello JSON dla definicji zasad hello.</span><span class="sxs-lookup"><span data-stu-id="973cc-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![Pokaż reguły przypisania](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="973cc-141">Zmień istniejące przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="973cc-141">Change an existing policy assignment</span></span>

<span data-ttu-id="973cc-142">toochange zasady, wybierz **edytować przypisanie** lub **usunąć**</span><span class="sxs-lookup"><span data-stu-id="973cc-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![edytowanie lub usuwanie przypisania](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="973cc-144">Przypisanie zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="973cc-144">Assign custom policies</span></span>

<span data-ttu-id="973cc-145">Jeśli zasady niestandardowe zdefiniowane w ramach subskrypcji, te zasady są dostępne do przypisania w ramach hello portalu.</span><span class="sxs-lookup"><span data-stu-id="973cc-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="973cc-146">Te zasady są poprzedzone znakiem **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="973cc-146">Those policies are prefaced with **[Custom]**</span></span>

![zasady niestandardowe](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="973cc-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="973cc-148">Next steps</span></span>
* <span data-ttu-id="973cc-149">toolearn o składni JSON hello do definiowania zasad, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="973cc-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="973cc-150">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="973cc-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="973cc-151">Schemat zasad Hello jest opublikowana w [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="973cc-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

