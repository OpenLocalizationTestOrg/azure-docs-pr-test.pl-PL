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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="b878d-103">Raportowanie interfejsów API dla klientów korporacyjnych — opłata magazynu Marketplace</span><span class="sxs-lookup"><span data-stu-id="b878d-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="b878d-104">Witaj Marketplace magazynu opłat API zwraca hello opartej na użyciu marketplace opłat podział według dnia hello określonego okresu rozliczeniowego lub daty rozpoczęcia i zakończenia (jeden raz opłaty nie są uwzględniane).</span><span class="sxs-lookup"><span data-stu-id="b878d-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="b878d-105">Żądanie</span><span class="sxs-lookup"><span data-stu-id="b878d-105">Request</span></span> 
<span data-ttu-id="b878d-106">Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b878d-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b878d-107">Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="b878d-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="b878d-108">Przedziałów czasu niestandardowych można określić z rozpoczęciem powitalne i kończyć się parametrami Data podczas hello formacie RRRR MM-dd hello maksymalny obsługiwany zakres to 36 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="b878d-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="b878d-109">Metoda</span><span class="sxs-lookup"><span data-stu-id="b878d-109">Method</span></span> | <span data-ttu-id="b878d-110">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b878d-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b878d-111">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="b878d-111">GET</span></span>|<span data-ttu-id="b878d-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b878d-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="b878d-113">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="b878d-113">GET</span></span>|<span data-ttu-id="b878d-114">/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b878d-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="b878d-115">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="b878d-115">GET</span></span>|<span data-ttu-id="b878d-116">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 2017-01-01 & endTime = 2017-01-10</span><span class="sxs-lookup"><span data-stu-id="b878d-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="b878d-117">Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b878d-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b878d-118">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b878d-118">Response</span></span>
 
    
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
    

<span data-ttu-id="b878d-119">**Definicje właściwości odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="b878d-119">**Response property definitions**</span></span>

|<span data-ttu-id="b878d-120">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b878d-120">Property Name</span></span>| <span data-ttu-id="b878d-121">Typ</span><span class="sxs-lookup"><span data-stu-id="b878d-121">Type</span></span>| <span data-ttu-id="b878d-122">Opis</span><span class="sxs-lookup"><span data-stu-id="b878d-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="b878d-123">id</span><span class="sxs-lookup"><span data-stu-id="b878d-123">id</span></span>|<span data-ttu-id="b878d-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-124">string</span></span>|<span data-ttu-id="b878d-125">Unikatowy identyfikator elementu opłat hello marketplace</span><span class="sxs-lookup"><span data-stu-id="b878d-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="b878d-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="b878d-126">subscriptionGuid</span></span>|<span data-ttu-id="b878d-127">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="b878d-127">Guid</span></span>|<span data-ttu-id="b878d-128">Witaj Guid subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b878d-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="b878d-129">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b878d-129">subscriptionName</span></span>|<span data-ttu-id="b878d-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-130">string</span></span>|<span data-ttu-id="b878d-131">Witaj Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b878d-131">hello Subscription Name</span></span>|
|<span data-ttu-id="b878d-132">meterId</span><span class="sxs-lookup"><span data-stu-id="b878d-132">meterId</span></span>|<span data-ttu-id="b878d-133">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-133">string</span></span>|<span data-ttu-id="b878d-134">Identyfikator hello wysyłanego licznika</span><span class="sxs-lookup"><span data-stu-id="b878d-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="b878d-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="b878d-135">usageStartDate</span></span>|<span data-ttu-id="b878d-136">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b878d-136">DateTime</span></span>|<span data-ttu-id="b878d-137">Czas rozpoczęcia hello użycie rekordu</span><span class="sxs-lookup"><span data-stu-id="b878d-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="b878d-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="b878d-138">usageEndDate</span></span>|<span data-ttu-id="b878d-139">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b878d-139">DateTime</span></span>|<span data-ttu-id="b878d-140">Godzina zakończenia hello użycie rekordu</span><span class="sxs-lookup"><span data-stu-id="b878d-140">End time for hello usage record</span></span>|
|<span data-ttu-id="b878d-141">offerName</span><span class="sxs-lookup"><span data-stu-id="b878d-141">offerName</span></span>|<span data-ttu-id="b878d-142">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-142">string</span></span>|<span data-ttu-id="b878d-143">Nazwa oferty Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-143">hello Offer name</span></span>|
|<span data-ttu-id="b878d-144">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="b878d-144">resourceGroup</span></span>|<span data-ttu-id="b878d-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-145">string</span></span>|<span data-ttu-id="b878d-146">Witaj zasobów grupy</span><span class="sxs-lookup"><span data-stu-id="b878d-146">hello resource Group</span></span>|
|<span data-ttu-id="b878d-147">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="b878d-147">instanceId</span></span>|<span data-ttu-id="b878d-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-148">string</span></span>|<span data-ttu-id="b878d-149">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="b878d-149">Instance Id</span></span>|
|<span data-ttu-id="b878d-150">części informacje dodatkowe Aby</span><span class="sxs-lookup"><span data-stu-id="b878d-150">additionalInfo</span></span>|<span data-ttu-id="b878d-151">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-151">string</span></span>|<span data-ttu-id="b878d-152">Dodatkowe informacje o ciągu JSON</span><span class="sxs-lookup"><span data-stu-id="b878d-152">Additional info JSON string</span></span>|
|<span data-ttu-id="b878d-153">tags</span><span class="sxs-lookup"><span data-stu-id="b878d-153">tags</span></span>|<span data-ttu-id="b878d-154">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-154">string</span></span>|<span data-ttu-id="b878d-155">Tag ciągu JSON</span><span class="sxs-lookup"><span data-stu-id="b878d-155">Tag JSON string</span></span>|
|<span data-ttu-id="b878d-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="b878d-156">orderNumber</span></span>|<span data-ttu-id="b878d-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-157">string</span></span>|<span data-ttu-id="b878d-158">numer zamówienia Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-158">hello order number</span></span>|
|<span data-ttu-id="b878d-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="b878d-159">unitOfMeasure</span></span>|<span data-ttu-id="b878d-160">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-160">string</span></span>|<span data-ttu-id="b878d-161">Jednostka miary dla pomiaru hello</span><span class="sxs-lookup"><span data-stu-id="b878d-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="b878d-162">CostCenter</span><span class="sxs-lookup"><span data-stu-id="b878d-162">costCenter</span></span>|<span data-ttu-id="b878d-163">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-163">string</span></span>|<span data-ttu-id="b878d-164">Centrum kosztów Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-164">hello cost center</span></span>|
|<span data-ttu-id="b878d-165">accountId</span><span class="sxs-lookup"><span data-stu-id="b878d-165">accountId</span></span>|<span data-ttu-id="b878d-166">int</span><span class="sxs-lookup"><span data-stu-id="b878d-166">int</span></span>|<span data-ttu-id="b878d-167">Konto Hello identyfikator</span><span class="sxs-lookup"><span data-stu-id="b878d-167">hello account Id</span></span>|
|<span data-ttu-id="b878d-168">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="b878d-168">accountName</span></span>|<span data-ttu-id="b878d-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-169">string</span></span> |<span data-ttu-id="b878d-170">Witaj nazwa konta</span><span class="sxs-lookup"><span data-stu-id="b878d-170">hello Account Name</span></span>|
|<span data-ttu-id="b878d-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="b878d-171">accountOwnerId</span></span>|<span data-ttu-id="b878d-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-172">string</span></span>|<span data-ttu-id="b878d-173">Witaj, identyfikator właściciela konta</span><span class="sxs-lookup"><span data-stu-id="b878d-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="b878d-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="b878d-174">departmentId</span></span>|<span data-ttu-id="b878d-175">int</span><span class="sxs-lookup"><span data-stu-id="b878d-175">int</span></span>|<span data-ttu-id="b878d-176">Dział Hello identyfikator</span><span class="sxs-lookup"><span data-stu-id="b878d-176">hello department Id</span></span>|
|<span data-ttu-id="b878d-177">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="b878d-177">departmentName</span></span>|<span data-ttu-id="b878d-178">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-178">string</span></span>|<span data-ttu-id="b878d-179">Nazwa działu Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-179">hello department name</span></span>|
|<span data-ttu-id="b878d-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="b878d-180">publisherName</span></span>|<span data-ttu-id="b878d-181">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-181">string</span></span>|<span data-ttu-id="b878d-182">Nazwa wydawcy Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-182">hello publisher name</span></span>|
|<span data-ttu-id="b878d-183">planName</span><span class="sxs-lookup"><span data-stu-id="b878d-183">planName</span></span>|<span data-ttu-id="b878d-184">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b878d-184">string</span></span>|<span data-ttu-id="b878d-185">Nazwa planu Hello</span><span class="sxs-lookup"><span data-stu-id="b878d-185">hello Plan name</span></span>|
|<span data-ttu-id="b878d-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="b878d-186">consumedQuantity</span></span>|<span data-ttu-id="b878d-187">Decimal</span><span class="sxs-lookup"><span data-stu-id="b878d-187">decimal</span></span>|<span data-ttu-id="b878d-188">Ilość wykorzystanego w tym okresie czasu</span><span class="sxs-lookup"><span data-stu-id="b878d-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="b878d-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="b878d-189">resourceRate</span></span>|<span data-ttu-id="b878d-190">Decimal</span><span class="sxs-lookup"><span data-stu-id="b878d-190">decimal</span></span>|<span data-ttu-id="b878d-191">Jednostka ceny hello licznika</span><span class="sxs-lookup"><span data-stu-id="b878d-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="b878d-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="b878d-192">extendedCost</span></span>|<span data-ttu-id="b878d-193">Decimal</span><span class="sxs-lookup"><span data-stu-id="b878d-193">decimal</span></span>|<span data-ttu-id="b878d-194">Szacowany na podstawie ilości zużytego i rozszerzone koszt opłat</span><span class="sxs-lookup"><span data-stu-id="b878d-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="b878d-195">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b878d-195">See also</span></span>

* [<span data-ttu-id="b878d-196">Okresy rozliczeń interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b878d-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b878d-197">Szczegóły użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b878d-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="b878d-198">Saldo oraz podsumowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b878d-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="b878d-199">Interfejs API arkusza cen</span><span class="sxs-lookup"><span data-stu-id="b878d-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)