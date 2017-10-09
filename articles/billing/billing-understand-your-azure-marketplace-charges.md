---
title: "aaaUnderstand Twojego Azure koszty usługi zewnętrzne | Dokumentacja firmy Microsoft"
description: "Informacje o rozliczeniach usług zewnętrznych, wcześniej znana jako Marketplace, opłaty na platformie Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>Zrozumienie dla zewnętrznych opłaty za usługę Azure rozliczeniowego
Usługi zewnętrzne używane toobe o nazwie portalu Azure Marketplace. Ogólnie rzecz biorąc są w przypadku usług opublikowanych przez strony trzecie dostępne dla platformy Azure, ale są zintegrowane całkowicie w obrębie platformy Azure. Na przykład ClearDB i SendGrid są usług zewnętrznych, które można kupić na platformie Azure, ale nie są publikowane przez firmę Microsoft.

Podczas obsługi administracyjnej nowych zewnętrznej usługi lub zasobu, wyświetlane jest ostrzeżenie:

![Ostrzeżenie zakupu Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> Zewnętrznych usług są publikowane przez firmy, które nie są firmy Microsoft, ale czasami produktów firmy Microsoft są również podzielone na usług zewnętrznych.
> 
> 

## <a name="how-external-services-are-billed"></a>W jaki sposób są rozliczane usług zewnętrznych
- Zewnętrznych usług są rozliczane oddzielnie. Są one traktowane jako pojedyncze zamówienia w ramach Twojej subskrypcji platformy Azure. Hello okresie rozliczeniowym dla każdej usługi jest ustawiana po zakupie usługi hello. Nie toobe mylić z hello okresie rozliczeniowym subskrypcji hello, w ramach którego go zakupiono. Otrzymasz również oddzielne rachunków i karty kredytowej jest naliczane osobno.
- Każda usługa zewnętrzny ma inny model rozliczeń. Niektóre usługi są rozliczane w sposób płatności obejmujące, podczas gdy inne miesięczne płatności na podstawie modelu. Karty kredytowej jest wymagane dla zewnętrznych usług Azure, nie można kupić usług zewnętrznych o płatności faktury.
- Nie można użyć miesięczne bezpłatnych środków dla usług zewnętrznych. Jeśli używasz subskrypcji platformy Azure, która obejmuje [wolne środków](https://azure.microsoft.com/pricing/spending-limits/), nie mogą one być zastosowane tooexternal rachunków usługi. Za pomocą usług zewnętrznych toopurchase karty kredytowej.


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>Widok zewnętrznej usługi wydatków i historię w hello portalu Azure
Można wyświetlić listę usług zewnętrznych hello znajdujących się na każdej subskrypcji w ramach hello [portalu Azure](https://portal.azure.com/): 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) hello konta administratora.
2. W menu centralnym hello wybierz **subskrypcje**.
   
    ![Wybierz subskrypcje w menu centralnym hello](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. W hello **subskrypcje** bloku, wybierz hello subskrypcji mają tooview, a następnie wybierz **usług zewnętrznych**.
   
    ![Wybierz subskrypcję w bloku rozliczeń hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. Każdy zamówień zewnętrznej usługi, nazwę wydawcy hello, warstwy usług, których używasz, nazwa nadana hello zasobów i bieżący stan kolejności hello powinna zostać wyświetlona. toosee poza rachunków, wybierz zewnętrznej usługi.
   
    ![Wybierz zewnętrznej usługi](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. W tym miejscu można wyświetlić poza kwoty rachunku tym hello podatku podział.
   
    ![Widok usług zewnętrznych historię rozliczeń](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>Zewnętrzna usługa widoku wydatków dla klientów Enterprise Agreement (EA)
Zobacz wydatków zewnętrznej usługi klientom EA i pobierania raportów w portalu EA hello. Zobacz [Azure Marketplace w celu EA klienci](https://ea.azure.com/helpdocs/azureMarketplace) tooget uruchomiona.

## <a name="manage-payment-methods-for-external-service-orders"></a>Zarządzanie formy płatności dla zewnętrznych zleceniami
Aktualizowanie metody płatności zamówień zewnętrznej usługi z hello [Centrum konta](https://account.windowsazure.com/).

> [!NOTE]
> Jeśli zakupiono subskrypcję za pomocą konta służbowego [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake zmienia tooyour formy płatności.
> 
> 

1. Zaloguj się toohello [Centrum konta](https://account.windowsazure.com/) i [Przejdź toohello **marketplace** kartę](https://account.windowsazure.com/Store)
   
    ![Wybierz pozycję marketplace w Centrum konta hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. Wybierz hello ma toomanage zewnętrznej usługi.
   
    ![Wybierz hello ma toomanage zewnętrznej usługi.](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. Kliknij przycisk **Zmień formę płatności** po prawej stronie powitania hello strony. To łącze powoduje możesz tooa innego portalu toomanage formy płatności.
   
    ![Podsumowanie zlecenia](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. Kliknij przycisk **Edytuj informacje o** i postępuj zgodnie z instrukcjami tooupdate dane o płatności.
   
    ![Wybierz pozycję Edytuj informacje](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>Anulowanie zamówienia zewnętrznej usługi
Toocancel zamówienia zewnętrznej usługi, usunąć zasób hello w hello [portalu Azure](https://portal.azure.com).

![Usuwanie zasobu](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal masz pytania, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.

