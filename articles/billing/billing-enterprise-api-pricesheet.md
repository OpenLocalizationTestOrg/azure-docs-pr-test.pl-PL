---
title: "Azure rozliczeń interfejsów API Enterprise - arkusza cen | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat raportowania interfejsów API, które umożliwiają klientom Enterprise Azure programowo pobierać dane dotyczące zużycia."
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>Raportowanie interfejsów API dla klientów korporacyjnych — arkusz cen

API arkusza cen udostępnia stawkę dla każdego licznika dla danego rejestracji i okresu rozliczeniowego.

##<a name="request"></a>Żądanie
Wspólne właściwości nagłówka, które mają zostać dodane zostały określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, zwracany jest danych dla bieżącego okresu rozliczeniowego.

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / arkusza cen|
|POBIERZ|/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / arkusza cen|

> [!Note]
> Aby użyć wersji zapoznawczej interfejsu API, Zastąp v2 v1 w powyższy adres URL.
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
>Jeśli korzystasz z interfejsu API w wersji zapoznawczej, meterId pole nie jest dostępne.
>

**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|id| Ciąg| Unikatowy identyfikator, który reprezentuje konkretnego elementu arkusza cen (licznik przez okres rozliczeń)|
|billingPeriodId| Ciąg| Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń|
|meterId| Ciąg| Identyfikator licznika. Może on być zamapowany na meterId użycia.|
|meterName| Ciąg| Nazwa licznika|
|unitOfMeasure| Ciąg| Jednostka miary dla pomiaru usługi|
|includedQuantity| Decimal| Ilość dostępnej |
|numer części| Ciąg| Numer części skojarzone z licznika|
|unitPrice| Decimal| Cenie jednostkowej dla licznika|
|currencyCode| Ciąg| Kod waluty unitPrice|
<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Szczegóły użycia interfejsu API](billing-enterprise-api-usage-detail.md)

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md)
