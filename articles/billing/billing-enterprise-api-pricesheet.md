---
title: "aaaAzure rozliczeń Enterprise interfejsów API - arkusza cen | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello interfejsów API raportowania programowo włączyć dane dotyczące zużycia toopull klientów Enterprise Azure."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>Raportowanie interfejsów API dla klientów korporacyjnych — arkusz cen

Hello API arkusza cen zapewnia hello stawkę dla każdego licznika dla hello rejestracji i okresu rozliczeniowego.

##<a name="request"></a>Żądanie
Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany.

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / arkusza cen|
|POBIERZ|/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / arkusza cen|

> [!Note]
> Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.
>

## <a name="response"></a>Odpowiedź

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Jeśli używasz hello interfejsu API w wersji zapoznawczej meterId pole nie jest dostępne.
>

**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|id| Ciąg| Witaj Unikatowy identyfikator, który reprezentuje konkretnego elementu arkusza cen (licznik przez okres rozliczeń)|
|billingPeriodId| Ciąg| Witaj Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń|
|meterId| Ciąg| Identyfikator Hello hello miernika. Może to być mapowane toohello meterId użycia.|
|meterName| Ciąg| Nazwa licznika Hello|
|unitOfMeasure| Ciąg| Witaj jednostka miary dla pomiaru hello usługi|
|includedQuantity| Decimal| Ilość dostępnej |
|numer części| Ciąg| numer części Hello skojarzone z hello licznika|
|unitPrice| Decimal| Witaj cenie jednostkowej dla licznika hello|
|currencyCode| Ciąg| Kod waluty Hello hello unitPrice|
<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Szczegóły użycia interfejsu API](billing-enterprise-api-usage-detail.md)

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md)
