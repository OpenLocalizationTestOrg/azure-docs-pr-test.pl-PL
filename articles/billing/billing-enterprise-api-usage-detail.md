---
title: "aaaAzure rozliczeń Enterprise interfejsów API — szczegóły użycia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>Raportowanie interfejsów API dla klientów korporacyjnych — szczegóły użycia

Hello użycia szczegółów API oferuje zestawienie ilości wykorzystanego i opłat szacowany przy rejestracji. wynik Hello zawiera również informacje dotyczące wystąpień, mierniki i działów. Witaj interfejsu API mogą być przeszukiwane przez okres rozliczeń lub określona data rozpoczęcia i zakończenia. 
## <a name="consumption-apis"></a>Interfejsy API zużycie


##<a name="request"></a>Żądanie 
Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md). Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany. Przedziałów czasu niestandardowych można określić z rozpoczęciem powitalne i kończyć się parametrami datę w formacie hello RRRR MM-dd. Hello maksymalny czas obsługiwany zakres to 36 miesięcy.  

|Metoda | Identyfikator URI żądania|
|-|-|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetails 
|POBIERZ|/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / usagedetails|
|POBIERZ|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetailsbycustomdate? startTime = 2017-01-01 & endTime = 2017-01-10|

> [!Note]
> Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.
>

## <a name="response"></a>Odpowiedź

> Powodu potencjalnie dużej liczby wyników hello danych toohello stronicowanej jest zestaw. Właściwość nextLink Hello, jeśli jest obecny, określa hello łącze do następnej strony hello danych. Jeśli hello link jest pusta, wskazuje to, że to hello ostatniej strony. 
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
|id| Ciąg| Witaj Unikatowy identyfikator dla wywołania hello interfejsu API. |
|Dane| Tablica JSON| Witaj tablicy dzienne Szczegóły obciążenia dla każdej instance\meter.|
|nextLink| Ciąg| Jeśli istnieją więcej stron danych hello nextLink punktów toohello adres URL tooreturn hello następnej strony danych. |
|accountId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|Identyfikator produktu| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|resourceLocationId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|consumedServiceID| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|departmentId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|accountOwnerEmail| Ciąg| Konto e-mail właściciela konta hello. |
|Nazwa konta| Ciąg| Odbiorcy wprowadzona nazwa konta hello. |
|serviceAdministratorId| Ciąg| Adres e-mail dla administratora usługi. |
|subscriptionId| int| Pole przestarzałe. Brak zgodności z poprzednimi wersjami. |
|subscriptionGuid| Ciąg| Globalne Unikatowy identyfikator dla hello subskrypcji. |
|Nazwa subskrypcji| Ciąg| Nazwa subskrypcji hello. |
|Data| Ciąg| Data Hello, w którym wystąpiło zużycia. |
|Produktu| Ciąg| Więcej informacji na temat hello miernika. Przykład: A1 systemu Windows (VM) - wschodni Region Azji i Pacyfiku|
|meterId| Ciąg| Identyfikator Hello hello miernika, którego emitowane użycia. |
|meterCategory| Ciąg| Witaj usługi platformy Azure, która została użyta. |
|meterSubCategory| Ciąg| Definiuje typ usługi Azure hello, które mogą wpływać na szybkość hello. Przykład: A1 (z systemem innym niż Windows maszyny Wirtualnej|
|meterRegion| Ciąg| Określa lokalizację hello datacenter hello niektórych usług, które kosztują na podstawie lokalizacji centrum danych. |
|meterName| Ciąg| Nazwa licznika hello. |
|consumedQuantity| O podwójnej precyzji| Kwota Hello hello licznika, który został zużyty. |
|resourceRate| O podwójnej precyzji| szybkość Hello stosowane na jednostkę rozliczeniowy. |
|Koszt| O podwójnej precyzji| Opłata Hello, które zostały poniesione dla licznika hello. |
|resourceLocation| Ciąg| Identyfikuje hello centrum danych, gdzie działa hello miernika. |
|consumedService| Ciąg| Witaj usługi platformy Azure, która została użyta. |
|Identyfikator wystąpienia| Ciąg| Ten identyfikator jest hello Nazwa zasobu hello lub hello w pełni kwalifikowany identyfikator zasobu. Aby uzyskać więcej informacji, zobacz [interfejsu API usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| Ciąg| Metadane wewnętrzny usługi Azure. |
|serviceInfo2| Ciąg| Na przykład typ obrazu maszyny wirtualnej i nazwę usługodawcy internetowego usługi ExpressRoute. |
|części informacje dodatkowe Aby| Ciąg| Metadane specyficzne dla usługi. Na przykład typ obrazu dla maszyny wirtualnej. |
|tags| Ciąg| Odbiorcy dodać tagi. Aby uzyskać więcej informacji, zobacz [organizowania zasobów na platformie Azure przy użyciu tagów](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| Ciąg| Tej kolumny nie jest używany. Brak zgodności z poprzednimi wersjami. |
|DepartmentName| Ciąg| Nazwa hello działu. |
|CostCenter| Ciąg| Centrum kosztów Hello użycia hello jest skojarzony. |
|unitOfMeasure| Ciąg| Identyfikuje hello jednostki, która usługa hello jest rozliczana w. Przykład: GB, godziny, 10 000 s. |
|Grupa zasobów| Ciąg| w których hello wdrożonej miernika jest uruchomiony w grupie zasobów Hello. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Zobacz też

* [Okresy rozliczeń interfejsu API](billing-enterprise-api-billing-periods.md)

* [Saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md)

* [Opłata magazynu Marketplace interfejsu API](billing-enterprise-api-marketplace-storecharge.md) 

* [Interfejs API arkusza cen](billing-enterprise-api-pricesheet.md)
