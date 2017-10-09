---
title: "tooAzure dostępu aaaManage rozliczeń, za pomocą ról | Dokumentacja firmy Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Zarządzanie informacjami o toobilling dostępu na platformie Azure przy użyciu kontroli dostępu opartej na rolach

Przypisując jedną powitania po subskrypcji tooyour ról użytkowników można przyznać dostęp dla platformy Azure rozliczeń toomembers informacji zespołu: konto administratora, administratora usługi, administratora współpracującego, właściciela, współautora, czytnika i rozliczeń czytnika. Mają oni dostęp do informacji toobilling w hello [portalu Azure](https://portal.azure.com/), oraz mogą używać hello [rozliczeń interfejsów API](billing-usage-rate-card-overview.md) tooprogrammatically uzyskać faktury (raz nie zgłoszono — ruch przychodzący) i szczegóły użycia. Aby uzyskać więcej informacji o który Przyznaj ról, a role można zrobić, zobacz [role w programie Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Stosowanie dodatkowych użytkowników tooaccess faktury

Witaj konto administratora musi włączyć przy użyciu hello [portalu Azure](https://portal.azure.com/) Zezwalaj tooinvoices dostęp inni użytkownicy i za pomocą interfejsu API.

1. Witaj administratora konta, wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.

1. Wybierz **faktury** , a następnie **dostępu tooinvoices**.

    ![Zrzut ekranu pokazuje, jak toodelegate dostępu tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Włącz **na** dostępu hello następuje zapisywania zmian hello, użytkownicy tooallow fakturze toodownload zakresie ról subskrypcji.

    ![Zrzut ekranu przedstawia tooinvoice dostępu toodelegate — wyłączone](./media/billing-manage-access/AA-optinAllow.png)

Zgodzie na rozwiązanie umożliwia administratora usługi, administratora współpracującego właściciela, współautora, czytnika i rozliczeń czytnika na powitania subskrypcji toodownload PDF faktury w hello portalu Azure. Faktury starsze niż grudnia 2016 są jednak dostępne toohello tylko Administrator konta teraz.

Witaj administratora konta można również skonfigurować faktury toohave wysyłane za pośrednictwem poczty e-mail. toolearn więcej, zobacz [uzyskać potwierdzenia w wiadomości e-mail](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Dodawanie użytkowników toohello rozliczeń czytnika roli

Hello rozliczeń czytnika rola ma dostęp tylko do odczytu toosubscription informacji dotyczących rozliczeń w portalu Azure, a nie tooservices dostępu, takich jak konta magazynu i maszyn wirtualnych. Przypisz hello rozliczeń czytnika roli toosomeone musi uzyskać dostępu do informacji dotyczących rozliczeń toohello subskrypcji, ale nie hello toomanage możliwości usługi Azure usługi. Ta rola jest odpowiednia dla użytkowników w organizacji, którzy finansowych i kosztów zarządzania należy wykonać tylko dla subskrypcji platformy Azure.

1. Wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.

1. Wybierz **(IAM) kontroli dostępu** , a następnie kliknij przycisk **Dodaj**.

    ![Zrzut ekranu przedstawia IAM w bloku subskrypcji hello](./media/billing-manage-access/select-iam.PNG)

1. Wybierz **rozliczeń czytnika** w hello **wybierz rolę** strony.

    ![Zrzut ekranu przedstawia rozliczeń czytnika w widoku podręcznego hello](./media/billing-manage-access/select-roles.PNG)

1. Wpisz hello e-mail dla użytkownika hello tooinvite, a następnie kliknij przycisk **OK** toosend hello zaproszenia.

    ![Zrzut ekranu pokazujący tooenter tooinvite poczty e-mail, ktoś](./media/billing-manage-access/add-user.PNG)

1. Wykonaj instrukcje hello zaproszenia e-mail toolog w jako czytnik rozliczeń.

    ![Zrzut ekranu pokazujący, co hello czytnika rozliczeń można zobaczyć w portalu Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> funkcja rozliczeń czytnika Hello jest w wersji zapoznawczej i jeszcze nie obsługuje subskrypcji enterprise (EA) lub nieglobalna chmury.

## <a name="adding-users-tooother-roles"></a>Dodawanie ról tooother użytkowników

Dostęp użytkownicy w innych ról, takich jak właścicielem lub współautorem, nie tylko rozliczeniowymi, ale również usług platformy Azure. Zobacz te role toomanage [Dodawanie lub zmienianie role administratora platformy Azure, zarządzających hello subskrypcji lub usługi](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Kto ma dostęp do hello [Centrum konta](https://account.windowsazure.com)?

Hello tylko Administrator konta może rejestrować się w Centrum konta toohello. Hello konto administratora jest hello prawnym właścicielem hello subskrypcji. Domyślnie osoba hello utworzył konto na lub zakupiono hello subskrypcji platformy Azure jest hello administratora konta, chyba że hello [przeniesienia własności subskrypcji](billing-subscription-transfer.md) toosomebody else. Hello administratora konta można tworzyć subskrypcje, anulowanie subskrypcji, zmienić hello adres rozliczeń dla subskrypcji i zarządzanie zasadami dostępu dla subskrypcji hello.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli masz więcej pytań, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
