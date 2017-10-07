---
title: "aaaDownload rozliczeń faktury i dziennego użycia danych Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toodownload lub widoku Azure rozliczeniowego faktury i dziennego użycia danych."
keywords: "faktury rozliczeń, pobierania faktury, faktury azure, azure użycie"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Pobierz lub wyświetlanie Twoich Azure rozliczeń faktury i dziennego użycia danych
Twoja faktura można pobrać z hello [portalu Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) lub została ona wysłana w wiadomości e-mail. toodownload Twojego dzienne dane dotyczące użycia, przejdź toohello [Centrum konta platformy Azure](https://account.windowsazure.com). Tylko w przypadku niektórych ról ma uprawnienie tooget rozliczeń faktury i użycie informacji, takich jak hello administratora konta. toolearn więcej informacji na temat uzyskiwania dostępu do informacji toobilling, zobacz [tooAzure dostępu Zarządzanie rozliczeniami za pomocą ról](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Pobierz faktury w wiadomości e-mail (PDF)
Można włączyć i skonfigurować tooreceive dodatkowych adresatów, faktury platformy Azure w wiadomości e-mail. Ta funkcja nie mogą być dostępne dla niektórych subskrypcji, takie jak ofert obsługi, umowy Enterprise Agreement lub Azure otwartym.

1. Wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Zgody na każdej subskrypcji użytkownika. Kliknij przycisk **faktury** następnie **E-mail fakturą**. 

    ![Zrzut ekranu pokazujący hello opcjonalnych przepływu](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Kliknij przycisk **uczestnictwa w** i zaakceptuj postanowienia hello.

    ![Zrzut ekranu pokazujący hello opcjonalnych przepływu](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Po zaakceptowane hello umowy, można skonfigurować dodatkowych adresatów.

    ![Zrzut ekranu pokazujący hello opcjonalnych przepływu](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Jeśli nie otrzymasz wiadomość e-mail po wykonaniu kroków hello, upewnij się, Twój adres e-mail jest poprawny w hello [preferencjach komunikacji w profilu](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Pobierać faktury z portalu Azure (PDF)

1. Wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure jako [użytkownikowi dostępu tooinvoices](billing-manage-access.md).

2. Wybierz **faktury**. 

    ![Zrzut ekranu pokazujący hello dotyczącymi rozliczeń i użycie opcji](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Kliknij przycisk **Pobierz faktury** tooview kopię faktury PDF. Informacja **nie jest dostępny**, zobacz [Dlaczego nie widzę faktury hello ostatnim okresie rozliczeniowym?](#noinvoice)

    ![Zrzut ekranu pokazujący rozliczeń okresów, opcja pobierania hello i sumy opłat dla każdego okresu rozliczeniowego](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. Dzienne użycie można także wyświetlić, klikając hello okresie rozliczeniowym. 

Aby uzyskać więcej informacji na temat faktury, zobacz [zrozumieć rachunku platformy Microsoft Azure](billing-understand-your-bill.md). Aby uzyskać pomoc, zarządzanie kosztami, [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Pobierz użycie z hello Centrum konta (.csv)

1. Zaloguj się na powitania [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) jako hello administratora konta.

2. Wybierz subskrypcję hello, dla której ma zostać hello faktury i użycie informacji.

3. Wybierz **HISTORII rozliczeń**. 

    ![Zrzut ekranu pokazujący opcji historii rozliczeń](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Twoje instrukcje dla hello ostatni sześć okresów rozliczeniowych i hello bieżącego okresu unbilled jest widoczny. 

    ![Zrzut ekranu pokazujący okresów rozliczeniowych, opcje toodownload faktury i dziennego użycia i sumy opłat dla każdego okresu rozliczeniowego](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Wybierz **widoku bieżącej instrukcji** toosee szacunkową informacji o opłatach na powitania czasu hello szacowania został wygenerowany. Te informacje jest aktualizowana tylko raz dziennie i może nie zawierać wszystkich użycie. Faktura miesięczne mogą się różnić od tego szacowania.

    ![Zrzut ekranu pokazujący hello opcji instrukcji bieżącego widoku](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Zrzut ekranu pokazujący hello oszacowanie bieżących opłat](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Wybierz **Pobierz dane użycia** toodownload hello dzienne dane użycia do pliku CSV. Jeśli zobaczysz dostępne dwie wersje, Pobierz w wersji 2.

    ![Zrzut ekranu pokazujący hello opcji Pobierz dane użycia](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Witaj konto administratora mogą uzyskiwać dostęp do Centrum konta platformy Azure hello. Innych administratorów rozliczeń, takich jak właściciela, można uzyskać informacji o użyciu przy użyciu hello [rozliczeń interfejsów API](billing-usage-rate-card-overview.md).

Aby uzyskać więcej informacji na temat dzienne użycie zobacz [zrozumieć rachunku platformy Microsoft Azure](billing-understand-your-bill.md). Aby uzyskać pomoc, zarządzanie kosztami, [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](billing-getting-started.md).

## <a name="noinvoice"></a>Dlaczego nie widzę faktury hello ostatnim okresie rozliczeniowym

Może istnieć kilka przyczyn widzisz faktury:

- Ma wartość miesięczne środki w ramach subskrypcji, która nie przekracza lub masz bezpłatnej wersji próbnej. Faktury generowany jest tylko wtedy, gdy zobowiązań pieniędzy.

- Jest to mniej niż 30 dni od dnia hello subskrybowane tooAzure.

- Witaj faktury nie jest jeszcze wygenerowane. Poczekaj na koniec hello hello okresie rozliczeniowym.

- Jeśli nie masz hello administratora konta, starsze faktury nie może być avaialbe tooyou.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli masz więcej pytań, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.

