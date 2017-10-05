---
title: Anulowanie subskrypcji platformy Azure | Dokumentacja firmy Microsoft
description: "Opis sposobu anulowania subskrypcji platformy Azure, takich jak subskrypcji bezpłatnej wersji próbnej"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a>Anulowanie subskrypcji platformy Azure

Możesz anulować subskrypcję platformy Azure jako [administratora konta](billing-subscription-transfer.md#whoisaa). Po anulowaniu subskrypcji kończy się dostępu do usług platformy Azure i zasobów.

Zanim anulujesz subskrypcję:

* Utwórz kopię zapasową danych. Na przykład jeśli dane są przechowywane w magazynu Azure i SQL, Pobierz kopię. Jeśli maszynę wirtualną, Zapisz obraz ją lokalnie.
* Zamknij usługi. Przejdź do [zasobów strony w portalu zarządzania](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), i **zatrzymać** wszelkie uruchomione maszyny wirtualne, aplikacji lub innych usług.
* Należy rozważyć przeprowadzenie migracji danych. Zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).

Jeśli anulujesz płatna [plan pomocy technicznej platformy Azure](https://azure.microsoft.com/support/plans/), możesz nadal są naliczane co miesiąc w pozostałej części termin 6 miesięcy.

## <a name="cancel-subscription-using-the-azure-portal"></a>Anulowanie subskrypcji przy użyciu portalu Azure

1. Wybierz subskrypcję z [subskrypcji](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

1. Wybierz subskrypcję, którą chcesz anulować i kliknij przycisk **anulować subskrypcję**.

    ![Zrzut ekranu pokazujący przycisk Anuluj](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. Postępuj zgodnie z monitami i zakończenia anulowania.

## <a name="cancel-subscription-using-the-azure-account-center"></a>Anulowanie subskrypcji przy użyciu Centrum konta platformy Azure

1. Zaloguj się do [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) jako administratora konta.

1. W obszarze **kliknij subskrypcję, aby wyświetlić szczegóły i użycie**, zaznacz subskrypcję, którą chcesz anulować.

    ![Zrzut ekranu pokazujący wybranej subskrypcji przykład](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. W prawej części strony, wybierz **Anuluj subskrypcję**.

    ![Zrzut ekranu pokazujący przycisk Anuluj subskrypcję](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. Wybierz **tak, anulowanie subskrypcji**.

    ![Zrzut ekranu pokazujący okno dialogowe Anuluj](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. Kliknij pozycję ![Zaznacz przycisk symbolu](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) Aby zamknąć okno dialogowe i wrócić do strony swojego subskrypcji.

## <a name="what-happens-after-i-cancel-my-subscription"></a>Co się stanie po I anulowanie subskrypcji?

Anulowanie, zatrzymaniu natychmiast rozliczeń. Jednak może potrwać do 10 minut pokazu anulowania w portalu.

Po wykonaniu tej usługi są wyłączone. Oznacza to, maszynach wirtualnych są alokację tymczasowe adresy IP są zwalniane i magazynu jest tylko do odczytu.

Chyba że w ramach bezpłatnej wersji próbnej lub masz punkty są rozliczane koszt opłat naliczanych oczekujących użycia wygenerowane między z ostatniego cyklu rozliczeniowego i datę anulowania. Otrzymasz rachunku ostatniego końca cyklu rozliczeniowego.

Po anulowaniu subskrypcji oczekiwania 90 dni przed trwałe usunięcie danych w przypadku, gdy trzeba do niego dostęp, czy zmienisz zdanie. Nie możemy pobierać przechowywania danych. Aby dowiedzieć się więcej, zobacz [Microsoft Center Trust — jak możemy zarządzać danymi](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).

## <a name="reactivate-subscription"></a>Ponowne uaktywnianie subskrypcji

Jeśli anulujesz subskrypcję z przypadkowo, możesz [uaktywnić go ponownie w Centrum konta](billing-subscription-become-disable.md).

Jeśli Twoja subskrypcja nie jest płatność za rzeczywiste użycie, się z pomocą techniczną w ciągu 90 dni od anulowania, aby ponownie aktywować subskrypcję.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli nadal masz pytania, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.
