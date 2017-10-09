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
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="70c24-103">Raportowanie interfejsów API dla klientów korporacyjnych — arkusz cen</span><span class="sxs-lookup"><span data-stu-id="70c24-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="70c24-104">Hello API arkusza cen zapewnia hello stawkę dla każdego licznika dla hello rejestracji i okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="70c24-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="70c24-105">Żądanie</span><span class="sxs-lookup"><span data-stu-id="70c24-105">Request</span></span>
<span data-ttu-id="70c24-106">Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="70c24-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="70c24-107">Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="70c24-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="70c24-108">Metoda</span><span class="sxs-lookup"><span data-stu-id="70c24-108">Method</span></span> | <span data-ttu-id="70c24-109">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="70c24-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="70c24-110">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="70c24-110">GET</span></span>|<span data-ttu-id="70c24-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / arkusza cen</span><span class="sxs-lookup"><span data-stu-id="70c24-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="70c24-112">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="70c24-112">GET</span></span>|<span data-ttu-id="70c24-113">/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / arkusza cen</span><span class="sxs-lookup"><span data-stu-id="70c24-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="70c24-114">Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.</span><span class="sxs-lookup"><span data-stu-id="70c24-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="70c24-115">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="70c24-115">Response</span></span>

    
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
><span data-ttu-id="70c24-116">Jeśli używasz hello interfejsu API w wersji zapoznawczej meterId pole nie jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="70c24-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="70c24-117">**Definicje właściwości odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="70c24-117">**Response property definitions**</span></span>

|<span data-ttu-id="70c24-118">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="70c24-118">Property Name</span></span>| <span data-ttu-id="70c24-119">Typ</span><span class="sxs-lookup"><span data-stu-id="70c24-119">Type</span></span>| <span data-ttu-id="70c24-120">Opis</span><span class="sxs-lookup"><span data-stu-id="70c24-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="70c24-121">id</span><span class="sxs-lookup"><span data-stu-id="70c24-121">id</span></span>| <span data-ttu-id="70c24-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-122">string</span></span>| <span data-ttu-id="70c24-123">Witaj Unikatowy identyfikator, który reprezentuje konkretnego elementu arkusza cen (licznik przez okres rozliczeń)</span><span class="sxs-lookup"><span data-stu-id="70c24-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="70c24-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="70c24-124">billingPeriodId</span></span>| <span data-ttu-id="70c24-125">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-125">string</span></span>| <span data-ttu-id="70c24-126">Witaj Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń</span><span class="sxs-lookup"><span data-stu-id="70c24-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="70c24-127">meterId</span><span class="sxs-lookup"><span data-stu-id="70c24-127">meterId</span></span>| <span data-ttu-id="70c24-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-128">string</span></span>| <span data-ttu-id="70c24-129">Identyfikator Hello hello miernika.</span><span class="sxs-lookup"><span data-stu-id="70c24-129">hello identifier for hello meter.</span></span> <span data-ttu-id="70c24-130">Może to być mapowane toohello meterId użycia.</span><span class="sxs-lookup"><span data-stu-id="70c24-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="70c24-131">meterName</span><span class="sxs-lookup"><span data-stu-id="70c24-131">meterName</span></span>| <span data-ttu-id="70c24-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-132">string</span></span>| <span data-ttu-id="70c24-133">Nazwa licznika Hello</span><span class="sxs-lookup"><span data-stu-id="70c24-133">hello meter name</span></span>|
|<span data-ttu-id="70c24-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="70c24-134">unitOfMeasure</span></span>| <span data-ttu-id="70c24-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-135">string</span></span>| <span data-ttu-id="70c24-136">Witaj jednostka miary dla pomiaru hello usługi</span><span class="sxs-lookup"><span data-stu-id="70c24-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="70c24-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="70c24-137">includedQuantity</span></span>| <span data-ttu-id="70c24-138">Decimal</span><span class="sxs-lookup"><span data-stu-id="70c24-138">decimal</span></span>| <span data-ttu-id="70c24-139">Ilość dostępnej</span><span class="sxs-lookup"><span data-stu-id="70c24-139">Quantity that is included</span></span> |
|<span data-ttu-id="70c24-140">numer części</span><span class="sxs-lookup"><span data-stu-id="70c24-140">partNumber</span></span>| <span data-ttu-id="70c24-141">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-141">string</span></span>| <span data-ttu-id="70c24-142">numer części Hello skojarzone z hello licznika</span><span class="sxs-lookup"><span data-stu-id="70c24-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="70c24-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="70c24-143">unitPrice</span></span>| <span data-ttu-id="70c24-144">Decimal</span><span class="sxs-lookup"><span data-stu-id="70c24-144">decimal</span></span>| <span data-ttu-id="70c24-145">Witaj cenie jednostkowej dla licznika hello</span><span class="sxs-lookup"><span data-stu-id="70c24-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="70c24-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="70c24-146">currencyCode</span></span>| <span data-ttu-id="70c24-147">Ciąg</span><span class="sxs-lookup"><span data-stu-id="70c24-147">string</span></span>| <span data-ttu-id="70c24-148">Kod waluty Hello hello unitPrice</span><span class="sxs-lookup"><span data-stu-id="70c24-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="70c24-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="70c24-149">See also</span></span>

* [<span data-ttu-id="70c24-150">Okresy rozliczeń interfejsu API</span><span class="sxs-lookup"><span data-stu-id="70c24-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="70c24-151">Szczegóły użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="70c24-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="70c24-152">Saldo oraz podsumowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="70c24-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="70c24-153">Opłata magazynu Marketplace interfejsu API</span><span class="sxs-lookup"><span data-stu-id="70c24-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
