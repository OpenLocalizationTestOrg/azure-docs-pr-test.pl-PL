---
title: "Portal Azure — zasady zasobów | Dokumentacja firmy Microsoft"
description: "Opisuje sposób portalu Azure umożliwia tworzenie i zarządzanie zasadami Menedżera zasobów. Zasady można stosować na grupy zasobów lub subskrypcji."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="67073-104">Przypisz i zarządzanie zasadami zasobów za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="67073-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="67073-105">Azure portal umożliwia przypisanie zasad zasobów do grupy zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="67073-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="67073-106">Interfejs użytkownika ułatwia wybierz zasady, które chcesz przypisać i podaj wartości parametrów dla tej zasady dostosować ustawienia zasad.</span><span class="sxs-lookup"><span data-stu-id="67073-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="67073-107">Aby przypisać zasad za pośrednictwem portalu, definicji zasad musi już istnieć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="67073-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="67073-108">Subskrypcja obejmuje kilka definicje wbudowanych zasad, które są gotowe do przypisania do grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="67073-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="67073-109">Widzisz tych zasad wbudowanych i niestandardowych zasad, zdefiniowanych w przypadku użycia portalu do przypisywania zasad.</span><span class="sxs-lookup"><span data-stu-id="67073-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="67073-110">Aby obejrzeć wprowadzenie do zasad i sposób definiowania zasad niestandardowych, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="67073-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="67073-111">Zasady są dziedziczone przez wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="67073-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="67073-112">Tak Jeśli zasady są stosowane do grupy zasobów, ma zastosowanie do wszystkich zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="67073-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="67073-113">W tym artykule określenie **zakres** odwołuje się do grupy zasobów lub subskrypcji, która jest przypisana zasad.</span><span class="sxs-lookup"><span data-stu-id="67073-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="67073-114">Zasady są oceniane podczas tworzenia i aktualizowania zasobów (PUT i poprawka operacji).</span><span class="sxs-lookup"><span data-stu-id="67073-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="67073-115">Przypisać zasady</span><span class="sxs-lookup"><span data-stu-id="67073-115">Assign a policy</span></span>

1. <span data-ttu-id="67073-116">Aby przypisać zasady do grupy zasobów lub subskrypcji, wybierz tej grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="67073-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="67073-117">W ustawieniach, wybierz **zasad**.</span><span class="sxs-lookup"><span data-stu-id="67073-117">In the settings, select **Policies**.</span></span>

   ![Wybieranie zasad](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="67073-119">Aby utworzyć przypisanie zasad dla tego zakresu, wybierz **Dodaj przypisanie**.</span><span class="sxs-lookup"><span data-stu-id="67073-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![Dodaj przypisania](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="67073-121">Wybierz zasady, którą chcesz przypisać.</span><span class="sxs-lookup"><span data-stu-id="67073-121">Select the policy you want to assign.</span></span> <span data-ttu-id="67073-122">Nawet jeśli nie dodano żadnych definicji zasad do subskrypcji, zobaczysz wbudowanych zasad, które są dostępne do przypisania.</span><span class="sxs-lookup"><span data-stu-id="67073-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="67073-123">Zasady te wbudowane obejmują wiele typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="67073-123">These built-in policies cover many common scenarios.</span></span>

   ![Wybierz definicję](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="67073-125">Po wybraniu zasad, zobacz temat Opis zasad i wszelkie parametry dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="67073-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="67073-126">Na przykład poniższy obraz przedstawia **dozwolone lokalizacje** parametr, który jest wymagany dla zasad, która ogranicza dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="67073-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![Pokaż parametry](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="67073-128">Za pomocą interfejsu użytkownika wybierz wartości w celu określenia parametrów zasad (np. lokalizacje, które można użyć do wdrożenia).</span><span class="sxs-lookup"><span data-stu-id="67073-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![Wybierz wartości parametrów](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="67073-130">Należy podać wartości innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="67073-130">Provide values for the other parameters.</span></span> <span data-ttu-id="67073-131">Zakres jest automatycznie przypisywany oparte na wybranej podczas uruchamiania przypisania zasad bloku.</span><span class="sxs-lookup"><span data-stu-id="67073-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="67073-132">Po zakończeniu wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="67073-132">Select **OK** when done.</span></span>

   ![Zdefiniuj parametry](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="67073-134">Zasady zostały przypisane do określonego zakresu.</span><span class="sxs-lookup"><span data-stu-id="67073-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="67073-135">Wyświetl przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="67073-135">View policy assignments</span></span>

<span data-ttu-id="67073-136">Po przypisaniu zasad, zobacz na liście zasad dla tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="67073-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="67073-137">**Szczegóły** karta zawiera podsumowanie przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="67073-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![Pokaż szczegóły](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="67073-139">**Zasada przypisania** karcie są wyświetlane JSON dla definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="67073-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![Pokaż reguły przypisania](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="67073-141">Zmień istniejące przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="67073-141">Change an existing policy assignment</span></span>

<span data-ttu-id="67073-142">Aby zmienić zasady, wybierz **edytować przypisanie** lub **usunąć**</span><span class="sxs-lookup"><span data-stu-id="67073-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![edytowanie lub usuwanie przypisania](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="67073-144">Przypisanie zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="67073-144">Assign custom policies</span></span>

<span data-ttu-id="67073-145">Jeśli zasady niestandardowe zdefiniowane w ramach subskrypcji, te zasady są dostępne do przypisania za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="67073-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="67073-146">Te zasady są poprzedzone znakiem **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="67073-146">Those policies are prefaced with **[Custom]**</span></span>

![zasady niestandardowe](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="67073-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67073-148">Next steps</span></span>
* <span data-ttu-id="67073-149">Informacje na temat składni JSON do definiowania zasad, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="67073-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="67073-150">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="67073-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="67073-151">Schemat zasad jest opublikowana w [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="67073-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

