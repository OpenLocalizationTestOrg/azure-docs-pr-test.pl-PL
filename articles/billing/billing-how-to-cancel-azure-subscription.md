---
title: aaaCancel subskrypcji platformy Azure | Dokumentacja firmy Microsoft
description: "Opisuje sposób toocancel Twojej subskrypcji platformy Azure, takich jak hello bezpłatnej wersji próbnej subskrypcji"
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
ms.openlocfilehash: 198d6ab3de143c071a572db899037f8de85a8cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cancel-your-subscription-for-azure"></a>Anulowanie subskrypcji platformy Azure

Możesz anulować subskrypcję platformy Azure jako hello [administratora konta](billing-subscription-transfer.md#whoisaa). Po anulowaniu subskrypcji hello kończy dostępu tooAzure usług i zasobów.

Zanim anulujesz subskrypcję:

* Utwórz kopię zapasową danych. Na przykład jeśli dane są przechowywane w magazynu Azure i SQL, Pobierz kopię. Jeśli maszynę wirtualną, Zapisz obraz ją lokalnie.
* Zamknij usługi. Przejdź toohello [zasobów strony w portalu zarządzania hello](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), i **zatrzymać** wszelkie uruchomione maszyny wirtualne, aplikacji lub innych usług.
* Należy rozważyć przeprowadzenie migracji danych. Zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).

Jeśli anulujesz płatna [plan pomocy technicznej platformy Azure](https://azure.microsoft.com/support/plans/), możesz nadal są naliczane co miesiąc hello pozostałej części hello termin 6 miesięcy.

## <a name="cancel-subscription-using-hello-azure-portal"></a>Anulowanie subskrypcji przy użyciu hello portalu Azure

1. Wybierz subskrypcję z hello [subskrypcji](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

1. Wybierz subskrypcję hello mają toocancel, a następnie kliknij przycisk **anulować subskrypcję**.

    ![Zrzut ekranu pokazujący przycisk Anuluj hello](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. Postępuj zgodnie z monitami i zakończenia anulowania.

## <a name="cancel-subscription-using-hello-azure-account-center"></a>Anulowanie subskrypcji przy użyciu Centrum konta platformy Azure hello

1. Zaloguj się toohello [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) jako hello administratora konta.

1. W obszarze **tooview subskrypcji kliknij szczegóły i użycie**, wybierz subskrypcję hello, które mają toocancel.

    ![Zrzut ekranu pokazujący wybranej subskrypcji przykład](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. Na powitania po prawej stronie powitania strony, wybierz **Anuluj subskrypcję**.

    ![Zrzut ekranu pokazujący przycisk subskrypcji Anuluj hello](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. Wybierz **tak, anulowanie subskrypcji**.

    ![Zrzut ekranu pokazujący hello Anuluj w oknie dialogowym](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. Kliknij pozycję ![Zaznacz przycisk symbolu](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) tooclose hello okna dialogowego okna i przywracać tooyour stronę subskrypcji.

## <a name="what-happens-after-i-cancel-my-subscription"></a>Co się stanie po I anulowanie subskrypcji?

Anulowanie, zatrzymaniu natychmiast rozliczeń. Jednak może potrwać Pokaż anulowania hello w portalu hello too10 minut.

Po wykonaniu tej usługi są wyłączone. Oznacza to, maszynach wirtualnych są alokację tymczasowe adresy IP są zwalniane i magazynu jest tylko do odczytu.

Chyba że w ramach bezpłatnej wersji próbnej lub masz punkty są rozliczane koszt opłat naliczanych oczekujących użycia wygenerowane między ostatniego cyklu rozliczeniowego i datę anulowania hello. Możesz uzyskać rachunku ostatniego na końcu hello hello cyklu rozliczeniowym.

Po anulowaniu subskrypcji oczekiwania 90 dni przed trwałemu usunięciu danych, w razie potrzeby tooaccess lub użytkownik zmieni zdanie. Nie możemy pobierać przechowywania danych hello. toolearn więcej, zobacz [Microsoft Center Trust — jak możemy zarządzać danymi](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).

## <a name="reactivate-subscription"></a>Ponowne uaktywnianie subskrypcji

Jeśli anulujesz subskrypcję z przypadkowo, możesz [uaktywnić go ponownie w Centrum konta hello](billing-subscription-become-disable.md).

Jeśli Twoja subskrypcja nie jest płatność za rzeczywiste użycie, skontaktuj się z obsługą w ciągu 90 dni tooreactivate anulowania subskrypcji.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli nadal masz pytania, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
