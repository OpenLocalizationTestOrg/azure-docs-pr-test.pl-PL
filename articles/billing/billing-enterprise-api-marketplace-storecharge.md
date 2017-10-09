---
title: "aaaAzure rozliczeń Enterprise interfejsów API - opłat w witrynie Marketplace | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>Raportowanie interfejsów API dla klientów korporacyjnych — opłata magazynu Marketplace

Witaj Marketplace magazynu opłat API zwraca hello opartej na użyciu marketplace opłat podział według dnia hello określonego okresu rozliczeniowego lub daty rozpoczęcia i zakończenia (jeden raz opłaty nie są uwzględniane).

##<a name="request"></a>Żądanie 
Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany. Przedziałów czasu niestandardowych można określić z rozpoczęciem powitalne i kończyć się parametrami Data podczas hello formacie RRRR MM-dd hello maksymalny obsługiwany zakres to 36 miesięcy.  

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges|
|POBIERZ|/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / marketplacecharges|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 2017-01-01 & endTime = 2017-01-10|

> [!Note]
> Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.
>

## <a name="response"></a>Odpowiedź
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|id|Ciąg|Unikatowy identyfikator elementu opłat hello marketplace|
|subscriptionGuid|Identyfikator GUID|Witaj Guid subskrypcji|
|Nazwa subskrypcji|Ciąg|Witaj Nazwa subskrypcji|
|meterId|Ciąg|Identyfikator hello wysyłanego licznika|
|usageStartDate|Data i godzina|Czas rozpoczęcia hello użycie rekordu|
|usageEndDate|Data i godzina|Godzina zakończenia hello użycie rekordu|
|offerName|Ciąg|Nazwa oferty Hello|
|Grupa zasobów|Ciąg|Witaj zasobów grupy|
|Identyfikator wystąpienia|Ciąg|Identyfikator wystąpienia|
|części informacje dodatkowe Aby|Ciąg|Dodatkowe informacje o ciągu JSON|
|tags|Ciąg|Tag ciągu JSON|
|orderNumber|Ciąg|numer zamówienia Hello|
|unitOfMeasure|Ciąg|Jednostka miary dla pomiaru hello|
|CostCenter|Ciąg|Centrum kosztów Hello|
|accountId|int|Konto Hello identyfikator|
|Nazwa konta|Ciąg |Witaj nazwa konta|
|accountOwnerId|Ciąg|Witaj, identyfikator właściciela konta|
|departmentId|int|Dział Hello identyfikator|
|DepartmentName|Ciąg|Nazwa działu Hello|
|publisherName|Ciąg|Nazwa wydawcy Hello|
|planName|Ciąg|Nazwa planu Hello|
|consumedQuantity|Decimal|Ilość wykorzystanego w tym okresie czasu|
|resourceRate|Decimal|Jednostka ceny hello licznika|
|extendedCost|Decimal|Szacowany na podstawie ilości zużytego i rozszerzone koszt opłat|
<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Szczegóły użycia interfejsu API](billing-enterprise-api-usage-detail.md) 

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Interfejs API arkusza cen](billing-enterprise-api-pricesheet.md)