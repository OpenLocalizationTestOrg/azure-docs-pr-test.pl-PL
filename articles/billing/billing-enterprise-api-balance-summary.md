---
title: "aaaAzure rozliczeń Enterprise interfejsów API - saldo i podsumowanie | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat użycia rozliczenia Azure i RateCard interfejsów API, które są używane tooprovide wgląd w informacje zużycia zasobów platformy Azure i trendów."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>Raportowanie interfejsów API dla klientów korporacyjnych - saldo i podsumowanie

Hello saldo oraz podsumowanie interfejsu API oferuje miesięczne podsumowanie informacji na temat salda, nowych zakupów, opłaty za usługę Azure Marketplace, zmiany i nadwyżkowe opłat.


##<a name="request"></a>Żądanie 
Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany.

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary|
|POBIERZ| /billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / balancesummary|

> [!Note]
> Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.
>

## <a name="response"></a>Odpowiedź

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|id|Ciąg|Witaj Unikatowy identyfikator określonego okresu rozliczeniowego do rejestracji|
|billingPeriodId|Ciąg |Witaj identyfikator okresu rozliczeniowego|
|currencyCode|Ciąg |Kod waluty Hello|
|beginningBalance|Decimal| Saldo początkowe Hello hello okresie rozliczeniowym|
|endingBalance|Decimal| Witaj saldo końcowe hello okresie rozliczeniowym (w przypadku otwartych okresów, które to będą aktualizowane codziennie na)|
|newPurchases|Decimal| Nowe suma zakupu|
|dostosowania|Decimal| Łączna kwota korekty|
|użyte|Decimal| Całkowite użycie zobowiązań|
|serviceOverage|Decimal| Nadwyżkowe elementy w warstwie usług platformy Azure|
|chargesBilledSeparately|Decimal| Opłaty za rachunki|
|totalOverage|Decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|Decimal| Usługa Azure zobowiązań + łączna nadwyżka|
|azureMarketplaceServiceCharges|Decimal| Całkowita liczba opłat za portalu Azure Marketplace|
|newPurchasesDetails|Tablicy JSON ciąg par nazwa-wartość|Lista nowych zakupów|
|adjustmentDetails|Tablicy JSON ciąg par nazwa-wartość|Listy korekt (środki podwyższenie poziomu, SIE, faktury itd.) |


<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Szczegóły użycia interfejsu API](billing-enterprise-api-usage-detail.md) 

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md) 

* [Interfejs API arkusza cen](billing-enterprise-api-pricesheet.md)