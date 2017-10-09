---
title: "aaaScale przydziały i limity w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale laboratorium w usłudze Azure DevTest Labs"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Skalowanie przydziały i limity w usłudze DevTest Labs
Podczas pracy w usłudze DevTest Labs, można zauważyć, że istnieją pewne domyślne limity toosome zasobów platformy Azure, które mogą mieć wpływ na usługi DevTest Labs hello. Te granice są określonego tooas **przydziały**.

> [!NOTE]
> Witaj usługi DevTest Labs nie nakładają żadnych przydziałów. Wszelkie przydziałów, które mogą wystąpić są domyślne ograniczenia hello subskrypcji ogólna platformy Azure.

Można użyć każdego zasobów platformy Azure, aż dojdziesz limit przydziału. Każda subskrypcja ma oddzielne przydziały i użycia są śledzone na subskrypcję.

Na przykład każda subskrypcja ma domyślnego przydziału rdzeni 20. Dlatego w przypadku tworzenia maszyn wirtualnych w laboratorium z czterech rdzeni, następnie można tworzyć tylko pięć maszyn wirtualnych. 

[Azure subskrypcji i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits) przedstawiono niektóre z najczęściej przydziały hello zasobów platformy Azure. Hello zasoby najczęściej używane w laboratorium, a dla mogą wystąpić przydziałów, zawierają rdzeni maszyny Wirtualnej, publiczne adresy IP interfejsu sieciowego, dysków zarządzanych, przypisanie roli RBAC i obwody usługi ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Wyświetlanie Twoich użycia i przydziały
Te kroki pokazują, jak tooview hello bieżącego przydziały w subskrypcji dla określonych zasobów platformy Azure i toosee, jaki procent każdego przydziału zostały użyte.

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **rozliczeń** z listy hello.
1. W bloku rozliczenia hello Wybierz subskrypcję.
4. Wybierz **użycia + przydziały**.

   ![Przycisk użycia i przydziały](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Witaj użycia + przydziały zostanie wyświetlony blok wyświetlania różne zasoby dostępne w tej subskrypcji oraz hello procent przydziału hello, który jest używany dla zasobów.

   ![Przydziały i użycia](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Żąda więcej zasobów w Twojej subskrypcji
Przekroczenie limitu przydziału hello domyślny limit zasobów w subskrypcji można zwiększyć się tooa maksymalny limit, zgodnie z opisem w [subskrypcji platformy Azure i ograniczenia usługi](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Te kroki pokazują, jak toorequest, zwiększ limit przydziału, za pośrednictwem hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, wybierz pozycję **rozliczeń**, a następnie wybierz **użycia + przydziały**.
1. Witaj użycia + bloku przydziałów, wybierz hello **żądanie zwiększenia** przycisku.

   ![Przycisk Zwiększ żądania](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete i przesłać Żądanie hello, wypełnij hello wymagane informacje na wszystkich kartach trzy hello **nowy obsługuje żądania** formularza.

   ![Zwiększ formularz żądania](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Opis ograniczeń Azure i zwiększa](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) zawiera więcej informacji o skontaktowaniu się z pomocą techniczną platformy Azure toorequest przydział zwiększenia.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Następne kroki
* Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
