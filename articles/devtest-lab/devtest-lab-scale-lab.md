---
title: "Skalowanie przydziały i limity w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować laboratorium w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Skalowanie przydziały i limity w usłudze DevTest Labs
Podczas pracy w usłudze DevTest Labs, można zauważyć, że istnieją pewne domyślne limity do niektórych zasobów platformy Azure, co może wpłynąć na usługę DevTest Labs. Ograniczenia te są określane jako **przydziały**.

> [!NOTE]
> Usługa DevTest Labs nie nakładają żadnych przydziałów. Wszelkie przydziałów, które mogą wystąpić są domyślne ograniczenia ogólne Azure subskrypcji.

Można użyć każdego zasobów platformy Azure, aż dojdziesz limit przydziału. Każda subskrypcja ma oddzielne przydziały i użycia są śledzone na subskrypcję.

Na przykład każda subskrypcja ma domyślnego przydziału rdzeni 20. Dlatego w przypadku tworzenia maszyn wirtualnych w laboratorium z czterech rdzeni, następnie można tworzyć tylko pięć maszyn wirtualnych. 

[Azure subskrypcji i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits) przedstawiono niektóre z najczęściej przydziały dla zasobów platformy Azure. Zasoby najczęściej używane w laboratorium, a dla mogą wystąpić przydziały, zawierają rdzeni maszyny Wirtualnej, publiczne adresy IP interfejsu sieciowego, dysków zarządzanych, przypisanie roli RBAC i obwody usługi ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Wyświetlanie Twoich użycia i przydziały
Te kroki pokazują, jak wyświetlić bieżący przydziały w subskrypcji dla określonych zasobów platformy Azure i zobacz, jaki procent każdego przydziału zostały użyte.

1. Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **rozliczeń** z listy.
1. W bloku rozliczenia Wybierz subskrypcję.
4. Wybierz **użycia + przydziały**.

   ![Przycisk użycia i przydziały](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Użycie + przydziały zostanie wyświetlony blok, listę różnych dostępnych zasobów w subskrypcji i procent przydziału, który jest używany dla zasobów.

   ![Przydziały i użycia](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Żąda więcej zasobów w Twojej subskrypcji
Przekroczenie limitu przydziału domyślny limit zasobów w subskrypcji można zwiększyć maksymalnego limitu, zgodnie z opisem w [subskrypcji platformy Azure i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Tych krokach przedstawiono sposób zażądać zwiększenia limitu przydziału przez [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, wybierz pozycję **rozliczeń**, a następnie wybierz **użycia + przydziały**.
1. Użycie + przydziały bloku, wybierz opcję **żądanie zwiększenia** przycisku.

   ![Przycisk Zwiększ żądania](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. Aby zakończyć i przesłać żądanie, wypełnij wymagane informacje na wszystkich trzech kartach **nowy obsługuje żądania** formularza.

   ![Zwiększ formularz żądania](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Opis ograniczeń Azure i zwiększa](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) zawiera więcej informacji o skontaktowaniu się z pomocą techniczną platformy Azure, aby zażądać zwiększenia limitu przydziału.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Następne kroki
* Eksploruj [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
