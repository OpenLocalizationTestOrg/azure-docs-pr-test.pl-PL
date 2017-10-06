---
title: aaaUnderstand rachunku dla platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooread i zrozumieć ich użycia, a kwota rachunku dla subskrypcji platformy Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Opis zawartości rachunku za korzystanie z platformy Microsoft Azure
naliczać opłaty toounderstand platformy Azure, faktury hello szczegółowe codziennego użycia pliku i kosztów zarządzania raportów w portalu Azure hello hello porównania.

tooobtain PDF faktury i kopię szczegółowe codziennego użycia pliku CSV pobieranie, zobacz [uzyskać Azure rozliczeń faktury i dziennego użycia danych](billing-download-azure-invoice-daily-usage-date.md). 

Szczegółowe warunki i opisy faktury i szczegółowe pliku codziennego użycia, zobacz [zrozumieć warunki na fakturę Microsoft Azure](billing-understand-your-invoice.md) i [użycia szczegółowe omówienie warunki na platformy Microsoft Azure](billing-understand-your-usage.md). 

Aby uzyskać szczegółowe informacje na powitania koszt raporty zarządzania, zobacz [portalu Azure koszt zarządzania](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Jak utworzyć się, że opłaty hello w fakturą są poprawne?
Jeśli Twoja faktura, który ma więcej szczegółów na jest opłat, istnieje kilka opcji.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Opcja 1: Przejrzyj faktury i porównania hello użycia i kosztów z hello szczegółowe użycia pliku CSV

Hello szczegółowe dane użycia pliku CSV zawiera Twoje opłat okresie rozliczeniowym i dziennego użycia. tooget Twojego szczegółowe dane użycia pliku CSV, zobacz [uzyskać Azure rozliczeń faktury i dziennego użycia danych](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Twoje opłaty za użycie są wyświetlane na poziomie miernika hello. Witaj następujące pojęcia oznaczają hello czynność na obu faktury hello i hello szczegółowe dane użycia pliku. Na przykład hello rozliczeń cyklu na fakturze hello jest równoważne toohello okresie rozliczeniowym pokazano hello szczegółowe dane użycia pliku.

 | Faktura (PDF) | Szczegółowe dane użycia (CSV)|
 | --- | --- |
|Cykl rozliczeń | Okres rozliczeniowy |
 |Nazwa |Kategoria miernika |
 |Typ |Licznik podkategorii |
 |Zasób |Nazwa miernika |
 |Region |Region miernika |
 |Zużyte |Zużyta ilość |
 |Dołączono |Uwzględniona ilość |
 |Płatne |Ilość nadwyżkowego użycia |

Witaj **opłaty za użycie** części faktury ma hello całkowitej wartości dla każdego licznika, który został wykorzystany okresie rozliczeniowym. Na przykład hello Poniższy zrzut ekranu przedstawia opłat użycia dla hello usługi Harmonogram systemu Azure.

![Opłaty za użycie faktury](./media/billing-understand-your-bill/1.png)

Witaj **instrukcji** sekcji szczegółowe dotyczące użycia CSV pokazuje hello tego samego opłat. Zarówno hello *zużyto* kwota i *wartość* faktury hello dopasowania.

![Opłaty za użycie CSV](./media/billing-understand-your-bill/2.png)

toosee podział dodatkowego codziennie, przejdź toohello **dzienne dane dotyczące użycia** sekcji hello CSV. Filtruj "Harmonogramu" w obszarze *kategorii licznika* , aby zobaczyć, które dni hello został wykorzystany i ile został wykorzystany. Witaj *zasobów* i *grupy zasobów* informacji znajduje się także do porównania. Witaj *zużyto* wartości powinny sumują toowhat firmy wyświetlane na fakturze hello.

![Dzienne użycie części hello CSV](./media/billing-understand-your-bill/3.png)

Koszt hello tooget na dzień, należy pomnożyć hello *zużyto* kwoty z hello *szybkość* wartość z zakresu od hello **instrukcji** sekcji.

Zobacz toolearn więcej informacji na temat faktury hello [zrozumieć faktura Azure](billing-understand-your-invoice.md).

toolearn o poszczególnych kolumn hello hello CSV, zobacz [określić sposób użycia szczegółowe Azure](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Opcja 2: Przejrzyj faktury i porównania z użycia hello i kosztów w hello portalu Azure

Hello portalu Azure ułatwia również zweryfikować Twojego opłat. Hello portalu Azure zapewnia szybki przegląd z użycia i hello obciążeń faktura kosztów zarządzania wykresy.

toocontinue z przykład Witaj z powyższych, odwiedź stronę hello [subskrypcji](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), wybierz subskrypcję, a następnie wybierz pozycję **analizy kosztów**. Z tego miejsca można określić przedział czasu hello i widoczne dla usługi Azure harmonogram hello użycia.

![Widok analizy kosztów w portalu Azure](./media/billing-understand-your-bill/4.png)

toosee hello codzienne podziału kosztów w **historii kosztów**, kliknij wiersz hello.

![Wyświetl historię kosztów w portalu Azure](./media/billing-understand-your-bill/5.png)

toolearn więcej, zobacz [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](billing-getting-started.md#costs).

## <a name="external"></a>Informacje o zewnętrznych opłaty za usługę?
Usług zewnętrznych (znanej także jako portalu Azure Marketplace zamówienia) są dostarczane przez dostawców usługi niezależne i są rozliczane oddzielnie. Witaj opłaty nie wyświetlone na faktura platformy Azure. toolearn więcej, zobacz [zrozumieć sieci Azure koszty usługi zewnętrzne](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Jak dokonać płatności?

Jeśli konfigurujesz kartą kredytową lub debetową jako metody płatności, płatności hello jest pobierana automatycznie w ciągu 10 dni, po zakończeniu okresu rozliczeniowego hello. W instrukcji karty kredytowej czy powiedzieć hello pozycji **MSFT Azure**.

Jeśli użytkownik [płać za fakturowania](billing-how-to-pay-by-invoice.md), Wyślij Twojej lokalizacji toohello płatności wymienione na powitania dolnej części faktury. Aby uzyskać Pomoc [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Jak sprawdzić stan hello płatności kartą kredytową?

[Tworzenie biletu pomocy technicznej](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask stanu hello płatności. 

## <a name="tips-for-cost-management"></a>Wskazówki dotyczące zarządzania koszt
- Szacowanie kosztów za pomocą hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/) i [całkowity koszt posiadania kalkulatora](https://aka.ms/azure-tco-calculator)i uzyskać hello [szczegółowych informacji o cenach dla każdej usługi](https://azure.microsoft.com/en-us/pricing/).
- [Konfigurowanie alertów rozliczeń](billing-set-up-alerts.md).
- [Przejrzyj użycia i kosztów regularnie w portalu Azure hello](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
