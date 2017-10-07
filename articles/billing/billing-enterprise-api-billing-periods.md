---
title: "aaaAzure rozliczeń API Enterprise - rozliczeń okresów | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>Raportowanie interfejsów API dla klientów korporacyjnych - okresów rozliczeń

Hello rozliczeń API okresów zwraca listę rozliczeń okresów, które mają dane dotyczące zużycia dla hello określić rejestracji w odwrotnej kolejności. Każdego okresu zawiera właściwość wskazujący trasę interfejsu API toohello dla hello cztery zestawy danych - BalanceSummary, UsageDetails Marktplace opłat i arkusza cen. Jeśli okres hello nie ma danych, hello odpowiednia właściwość ma wartość null. 


##<a name="request"></a>Żądanie 
Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md). 

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods|

> [!Note]
> Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.
>

## <a name="response"></a>Odpowiedź
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|billingPeriodId| Ciąg| Witaj Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń|
|billingStart| Data i godzina| Data rozpoczęcia okresu hello reprezentującym ISO 8601|
|billingEnd| Data i godzina| Data zakończenia okresu hello reprezentującym ISO 8601|
|balanceSummary| Ciąg| Hello ścieżki adresu URL, który przekierowuje toohello saldo podsumowanie danych dla tego okresu.|
|usageDetails| Ciąg| Hello ścieżki adresu URL, który przekierowuje toohello szczegóły użycia danych dla tego okresu.|
|marketplaceCharges| Ciąg| Hello ścieżki adresu URL, który przekierowuje toohello opłat w witrynie Marketplace danych dla tego okresu.|
|Arkusz cen| Ciąg| Hello ścieżki adresu URL, który przekierowuje toohello danych arkusza cen dla tego okresu.|

<br/>
## <a name="see-also"></a>Zobacz też

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Szczegóły użycia interfejsu API](billing-enterprise-api-usage-detail.md) 

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md) 

* [Interfejs API arkusza cen](billing-enterprise-api-pricesheet.md)