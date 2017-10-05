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
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="47a88-103">Raportowanie interfejsów API dla klientów korporacyjnych — arkusz cen</span><span class="sxs-lookup"><span data-stu-id="47a88-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="47a88-104">API arkusza cen udostępnia stawkę dla każdego licznika dla danego rejestracji i okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="47a88-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="47a88-105">Żądanie</span><span class="sxs-lookup"><span data-stu-id="47a88-105">Request</span></span>
<span data-ttu-id="47a88-106">Wspólne właściwości nagłówka, które mają zostać dodane zostały określone [tutaj](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="47a88-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="47a88-107">Jeśli nie określono okresie rozliczeniowym, zwracany jest danych dla bieżącego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="47a88-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="47a88-108">Metoda</span><span class="sxs-lookup"><span data-stu-id="47a88-108">Method</span></span> | <span data-ttu-id="47a88-109">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="47a88-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="47a88-110">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="47a88-110">GET</span></span>|<span data-ttu-id="47a88-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / arkusza cen</span><span class="sxs-lookup"><span data-stu-id="47a88-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="47a88-112">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="47a88-112">GET</span></span>|<span data-ttu-id="47a88-113">/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / arkusza cen</span><span class="sxs-lookup"><span data-stu-id="47a88-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="47a88-114">Aby użyć wersji zapoznawczej interfejsu API, Zastąp v2 v1 w powyższy adres URL.</span><span class="sxs-lookup"><span data-stu-id="47a88-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="47a88-115">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="47a88-115">Response</span></span>

    
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
><span data-ttu-id="47a88-116">Jeśli korzystasz z interfejsu API w wersji zapoznawczej, meterId pole nie jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="47a88-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="47a88-117">**Definicje właściwości odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="47a88-117">**Response property definitions**</span></span>

|<span data-ttu-id="47a88-118">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="47a88-118">Property Name</span></span>| <span data-ttu-id="47a88-119">Typ</span><span class="sxs-lookup"><span data-stu-id="47a88-119">Type</span></span>| <span data-ttu-id="47a88-120">Opis</span><span class="sxs-lookup"><span data-stu-id="47a88-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="47a88-121">id</span><span class="sxs-lookup"><span data-stu-id="47a88-121">id</span></span>| <span data-ttu-id="47a88-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-122">string</span></span>| <span data-ttu-id="47a88-123">Unikatowy identyfikator, który reprezentuje konkretnego elementu arkusza cen (licznik przez okres rozliczeń)</span><span class="sxs-lookup"><span data-stu-id="47a88-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="47a88-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="47a88-124">billingPeriodId</span></span>| <span data-ttu-id="47a88-125">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-125">string</span></span>| <span data-ttu-id="47a88-126">Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń</span><span class="sxs-lookup"><span data-stu-id="47a88-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="47a88-127">meterId</span><span class="sxs-lookup"><span data-stu-id="47a88-127">meterId</span></span>| <span data-ttu-id="47a88-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-128">string</span></span>| <span data-ttu-id="47a88-129">Identyfikator licznika.</span><span class="sxs-lookup"><span data-stu-id="47a88-129">The identifier for the meter.</span></span> <span data-ttu-id="47a88-130">Może on być zamapowany na meterId użycia.</span><span class="sxs-lookup"><span data-stu-id="47a88-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="47a88-131">meterName</span><span class="sxs-lookup"><span data-stu-id="47a88-131">meterName</span></span>| <span data-ttu-id="47a88-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-132">string</span></span>| <span data-ttu-id="47a88-133">Nazwa licznika</span><span class="sxs-lookup"><span data-stu-id="47a88-133">The meter name</span></span>|
|<span data-ttu-id="47a88-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="47a88-134">unitOfMeasure</span></span>| <span data-ttu-id="47a88-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-135">string</span></span>| <span data-ttu-id="47a88-136">Jednostka miary dla pomiaru usługi</span><span class="sxs-lookup"><span data-stu-id="47a88-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="47a88-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="47a88-137">includedQuantity</span></span>| <span data-ttu-id="47a88-138">Decimal</span><span class="sxs-lookup"><span data-stu-id="47a88-138">decimal</span></span>| <span data-ttu-id="47a88-139">Ilość dostępnej</span><span class="sxs-lookup"><span data-stu-id="47a88-139">Quantity that is included</span></span> |
|<span data-ttu-id="47a88-140">numer części</span><span class="sxs-lookup"><span data-stu-id="47a88-140">partNumber</span></span>| <span data-ttu-id="47a88-141">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-141">string</span></span>| <span data-ttu-id="47a88-142">Numer części skojarzone z licznika</span><span class="sxs-lookup"><span data-stu-id="47a88-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="47a88-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="47a88-143">unitPrice</span></span>| <span data-ttu-id="47a88-144">Decimal</span><span class="sxs-lookup"><span data-stu-id="47a88-144">decimal</span></span>| <span data-ttu-id="47a88-145">Cenie jednostkowej dla licznika</span><span class="sxs-lookup"><span data-stu-id="47a88-145">The unit price for the meter</span></span>|
|<span data-ttu-id="47a88-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="47a88-146">currencyCode</span></span>| <span data-ttu-id="47a88-147">Ciąg</span><span class="sxs-lookup"><span data-stu-id="47a88-147">string</span></span>| <span data-ttu-id="47a88-148">Kod waluty unitPrice</span><span class="sxs-lookup"><span data-stu-id="47a88-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="47a88-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="47a88-149">See also</span></span>

* [<span data-ttu-id="47a88-150">Okresy rozliczeń interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47a88-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="47a88-151">Szczegóły użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47a88-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="47a88-152">Saldo oraz podsumowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47a88-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="47a88-153">Opłata magazynu Marketplace interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47a88-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
