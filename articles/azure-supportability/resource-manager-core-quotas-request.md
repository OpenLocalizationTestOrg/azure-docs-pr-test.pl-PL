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
# <a name="resource-manager-core-quota-increase-requests"></a>Żądania Zwiększ limit przydziału rdzeni Menedżera zasobów

Limity przydziału Menedżera zasobów core są wymuszane na poziomie regionu i poziomu rodziny SKU.
Więcej informacji na temat sposobu przydziały są wymuszane na [subskrypcji platformy Azure i ograniczenia usługi](http://aka.ms/quotalimits) strony.
Aby dowiedzieć się więcej na temat rodziny SKU, może porównania kosztów i wydajności na [cennik maszyn wirtualnych](http://aka.ms/pricingcompute) strony.

Aby zażądać zwiększenia, należy utworzyć przydział sprawy pomocy technicznej dla rdzeni w portalu Azure [https://portal.azure.com](https://portal.azure.com).

> [!NOTE]
> Dowiedz się, jak [Utwórz żądanie obsługi](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) w portalu Azure

1. Na stronie nowe żądanie pomocy technicznej wybierz typ problemu jako "Przydziału" i typ przydziału jako "Rdzeni".

    ![Blok podstawowych ustawień limitu przydziału](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. Wybierz model wdrożenia jako "Resource Manager" i wybierz lokalizację.

    ![Przydział Problem bloku](./media/resource-manager-core-quotas-request/Problem-step.png)

3. Wybierz rodziny SKU, która wymaga zwiększenia.

    ![Wybrane serii jednostki SKU](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. Wprowadź nowe limity, którą chcesz dla tej subskrypcji.

    ![Nowe żądanie przydział jednostki SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- Aby usunąć wiersza, usuń zaznaczenie pola wyboru z listy rozwijanej rodziny SKU jednostka SKU, lub kliknij ikonę odrzucenia "x".
Po wprowadzeniu żądany limit przydziału dla każdej rodziny SKU, kliknij przycisk Dalej, na stronie krok Problem, aby kontynuować tworzenia żądania obsługi.
