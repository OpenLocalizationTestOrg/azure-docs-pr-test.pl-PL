---
title: "Żądania Zwiększ limit przydziału rdzeni Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Żądania Zwiększ limit przydziału rdzeni Azure Resource Manager"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="74cdd-103">Żądania Zwiększ limit przydziału rdzeni Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="74cdd-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="74cdd-104">Limity przydziału Menedżera zasobów core są wymuszane na poziomie regionu i poziomu rodziny SKU.</span><span class="sxs-lookup"><span data-stu-id="74cdd-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="74cdd-105">Więcej informacji na temat sposobu przydziały są wymuszane na [subskrypcji platformy Azure i ograniczenia usługi](http://aka.ms/quotalimits) strony.</span><span class="sxs-lookup"><span data-stu-id="74cdd-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="74cdd-106">Aby dowiedzieć się więcej na temat rodziny SKU, może porównania kosztów i wydajności na [cennik maszyn wirtualnych](http://aka.ms/pricingcompute) strony.</span><span class="sxs-lookup"><span data-stu-id="74cdd-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="74cdd-107">Aby zażądać zwiększenia, należy utworzyć przydział sprawy pomocy technicznej dla rdzeni w portalu Azure [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74cdd-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="74cdd-108">Dowiedz się, jak [Utwórz żądanie obsługi](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="74cdd-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="74cdd-109">Na stronie nowe żądanie pomocy technicznej wybierz typ problemu jako "Przydziału" i typ przydziału jako "Rdzeni".</span><span class="sxs-lookup"><span data-stu-id="74cdd-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Blok podstawowych ustawień limitu przydziału](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="74cdd-111">Wybierz model wdrożenia jako "Resource Manager" i wybierz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="74cdd-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Przydział Problem bloku](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="74cdd-113">Wybierz rodziny SKU, która wymaga zwiększenia.</span><span class="sxs-lookup"><span data-stu-id="74cdd-113">Select the SKU Families that require an increase.</span></span>

    ![Wybrane serii jednostki SKU](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="74cdd-115">Wprowadź nowe limity, którą chcesz dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="74cdd-115">Enter the new limits you would like on the subscription.</span></span>

    ![Nowe żądanie przydział jednostki SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="74cdd-117">Aby usunąć wiersza, usuń zaznaczenie pola wyboru z listy rozwijanej rodziny SKU jednostka SKU, lub kliknij ikonę odrzucenia "x".</span><span class="sxs-lookup"><span data-stu-id="74cdd-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="74cdd-118">Po wprowadzeniu żądany limit przydziału dla każdej rodziny SKU, kliknij przycisk Dalej, na stronie krok Problem, aby kontynuować tworzenia żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="74cdd-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
