---
title: "Azure rozliczeń interfejsów API Enterprise — szczegóły użycia | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat użycia rozliczeń Azure i RateCard interfejsów API, które są używane do wgląd w użycie zasobów platformy Azure i trendów."
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
ms.openlocfilehash: 5b49220e6eb27544dba54255ee88c56ad79c3141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>Raportowanie interfejsów API dla klientów korporacyjnych — szczegóły użycia

Interfejs API szczegółów użycia oferuje zestawienie ilości wykorzystanego i opłat szacowany przy rejestracji. Wynik zawiera również informacje dotyczące wystąpień, mierniki i działów. Interfejs API mogą być przeszukiwane przez okres rozliczeń lub określonej daty rozpoczęcia i zakończenia. 
## <a name="consumption-apis"></a>Interfejsy API zużycie


##<a name="request"></a>Żądanie 
Wspólne właściwości nagłówka, które mają zostać dodane zostały określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, zwracany jest danych dla bieżącego okresu rozliczeniowego. Przedziałów czasu niestandardowych można określić z początkiem i kończyć się parametrami datę w formacie RRRR MM-dd. Zakres maksymalny czas obsługiwanych jest 36 miesięcy.  

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetails 
|POBIERZ|/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / usagedetails|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetailsbycustomdate? startTime = 2017-01-01 & endTime = 2017-01-10|

> [!Note]
> Aby użyć wersji zapoznawczej interfejsu API, Zastąp v2 v1 w powyższy adres URL.
>

## <a name="response"></a>Odpowiedź

> Z powodu potencjalnie dużej ilości danych wynik stronicowanej jest zestaw. Właściwość nextLink, jeśli jest obecny, określa łącze do następnej strony danych. Jeśli link jest pusta, oznacza to, że jest to ostatnia strona. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Definicje właściwości odpowiedzi**

|Nazwa właściwości| Typ| Opis
|-|-|-|
|id| Ciąg| Unikatowy identyfikator dla wywołania interfejsu API. |
|Dane| Tablica JSON| Tablica dzienne Szczegóły obciążenia dla każdej instance\meter.|
|nextLink| Ciąg| Jeśli istnieją więcej stron danych nextLink wskazuje adres URL zwracany następnej strony danych. |
|accountId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|Identyfikator produktu| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|resourceLocationId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|consumedServiceID| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|departmentId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|accountOwnerEmail| Ciąg| Konto e-mail właściciela konta. |
|Nazwa konta| Ciąg| Odbiorcy wprowadzona nazwa konta. |
|serviceAdministratorId| Ciąg| Adres e-mail dla administratora usługi. |
|subscriptionId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|subscriptionGuid| Ciąg| Globalny identyfikator subskrypcji. |
|Nazwa subskrypcji| Ciąg| Nazwa subskrypcji. |
|Data| Ciąg| Data, w którym wystąpiło zużycia. |
|Produktu| Ciąg| Więcej informacji na temat licznika. Przykład: A1 systemu Windows (VM) - wschodni Region Azji i Pacyfiku|
|meterId| Ciąg| Identyfikator miernika, do którego emitowane użycia. |
|meterCategory| Ciąg| Usługa platformy Azure, która została użyta. |
|meterSubCategory| Ciąg| Definiuje typ usługi Azure, które mogą wpływać na szybkość. Przykład: A1 (z systemem innym niż Windows maszyny Wirtualnej|
|meterRegion| Ciąg| Określa lokalizację centrum danych pewnych usług, które są wyceniane na podstawie lokalizacji centrum danych. |
|meterName| Ciąg| Nazwa licznika. |
|consumedQuantity| O podwójnej precyzji| Wartość licznika, który został zużyty. |
|resourceRate| O podwójnej precyzji| Stawkę na jednostkę rozliczeniowy. |
|Koszt| O podwójnej precyzji| Opłata, które zostały poniesione dla licznika. |
|resourceLocation| Ciąg| Określa centrum danych, w którym jest uruchomiona licznika. |
|consumedService| Ciąg| Usługa platformy Azure, która została użyta. |
|Identyfikator wystąpienia| Ciąg| Ten identyfikator jest nazwa zasobu lub pełny identyfikator zasobu. Aby uzyskać więcej informacji, zobacz [interfejsu API usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| Ciąg| Metadane wewnętrzny usługi Azure. |
|serviceInfo2| Ciąg| Na przykład typ obrazu maszyny wirtualnej i nazwę usługodawcy internetowego usługi ExpressRoute. |
|części informacje dodatkowe Aby| Ciąg| Metadane specyficzne dla usługi. Na przykład typ obrazu dla maszyny wirtualnej. |
|tags| Ciąg| Odbiorcy dodać tagi. Aby uzyskać więcej informacji, zobacz [organizowania zasobów na platformie Azure przy użyciu tagów](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| Ciąg| Tej kolumny nie jest używany. Brak zgodności z poprzednimi wersjami. |
|DepartmentName| Ciąg| Nazwa działu. |
|CostCenter| Ciąg| Centrum kosztów skojarzonego z użycia. |
|unitOfMeasure| Ciąg| Określa jednostkę, dla której usługa jest rozliczana w. Przykład: GB, godziny, 10 000 s. |
|Grupa zasobów| Ciąg| Grupy zasobów, w którym działa mierniku wdrożonej w. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md) 

* [Interfejs API arkusza cen](billing-enterprise-api-pricesheet.md)
