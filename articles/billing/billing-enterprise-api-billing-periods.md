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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="4e58a-103">Raportowanie interfejsów API dla klientów korporacyjnych - okresów rozliczeń</span><span class="sxs-lookup"><span data-stu-id="4e58a-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="4e58a-104">Hello rozliczeń API okresów zwraca listę rozliczeń okresów, które mają dane dotyczące zużycia dla hello określić rejestracji w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4e58a-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="4e58a-105">Każdego okresu zawiera właściwość wskazujący trasę interfejsu API toohello dla hello cztery zestawy danych - BalanceSummary, UsageDetails Marktplace opłat i arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="4e58a-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="4e58a-106">Jeśli okres hello nie ma danych, hello odpowiednia właściwość ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="4e58a-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="4e58a-107">Żądanie</span><span class="sxs-lookup"><span data-stu-id="4e58a-107">Request</span></span> 
<span data-ttu-id="4e58a-108">Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="4e58a-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="4e58a-109">Metoda</span><span class="sxs-lookup"><span data-stu-id="4e58a-109">Method</span></span> | <span data-ttu-id="4e58a-110">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4e58a-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="4e58a-111">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="4e58a-111">GET</span></span>| <span data-ttu-id="4e58a-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods</span><span class="sxs-lookup"><span data-stu-id="4e58a-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="4e58a-113">Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4e58a-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="4e58a-114">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4e58a-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="4e58a-115">**Definicje właściwości odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="4e58a-115">**Response property definitions**</span></span>

|<span data-ttu-id="4e58a-116">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="4e58a-116">Property Name</span></span>| <span data-ttu-id="4e58a-117">Typ</span><span class="sxs-lookup"><span data-stu-id="4e58a-117">Type</span></span>| <span data-ttu-id="4e58a-118">Opis</span><span class="sxs-lookup"><span data-stu-id="4e58a-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="4e58a-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="4e58a-119">billingPeriodId</span></span>| <span data-ttu-id="4e58a-120">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e58a-120">string</span></span>| <span data-ttu-id="4e58a-121">Witaj Unikatowy identyfikator, który reprezentuje określonym okresie rozliczeń</span><span class="sxs-lookup"><span data-stu-id="4e58a-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="4e58a-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="4e58a-122">billingStart</span></span>| <span data-ttu-id="4e58a-123">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="4e58a-123">datetime</span></span>| <span data-ttu-id="4e58a-124">Data rozpoczęcia okresu hello reprezentującym ISO 8601</span><span class="sxs-lookup"><span data-stu-id="4e58a-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="4e58a-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="4e58a-125">billingEnd</span></span>| <span data-ttu-id="4e58a-126">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="4e58a-126">datetime</span></span>| <span data-ttu-id="4e58a-127">Data zakończenia okresu hello reprezentującym ISO 8601</span><span class="sxs-lookup"><span data-stu-id="4e58a-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="4e58a-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="4e58a-128">balanceSummary</span></span>| <span data-ttu-id="4e58a-129">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e58a-129">string</span></span>| <span data-ttu-id="4e58a-130">Hello ścieżki adresu URL, który przekierowuje toohello saldo podsumowanie danych dla tego okresu.</span><span class="sxs-lookup"><span data-stu-id="4e58a-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="4e58a-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="4e58a-131">usageDetails</span></span>| <span data-ttu-id="4e58a-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e58a-132">string</span></span>| <span data-ttu-id="4e58a-133">Hello ścieżki adresu URL, który przekierowuje toohello szczegóły użycia danych dla tego okresu.</span><span class="sxs-lookup"><span data-stu-id="4e58a-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="4e58a-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="4e58a-134">marketplaceCharges</span></span>| <span data-ttu-id="4e58a-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e58a-135">string</span></span>| <span data-ttu-id="4e58a-136">Hello ścieżki adresu URL, który przekierowuje toohello opłat w witrynie Marketplace danych dla tego okresu.</span><span class="sxs-lookup"><span data-stu-id="4e58a-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="4e58a-137">Arkusz cen</span><span class="sxs-lookup"><span data-stu-id="4e58a-137">priceSheet</span></span>| <span data-ttu-id="4e58a-138">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e58a-138">string</span></span>| <span data-ttu-id="4e58a-139">Hello ścieżki adresu URL, który przekierowuje toohello danych arkusza cen dla tego okresu.</span><span class="sxs-lookup"><span data-stu-id="4e58a-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="4e58a-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4e58a-140">See also</span></span>

* [<span data-ttu-id="4e58a-141">Saldo oraz podsumowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4e58a-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="4e58a-142">Szczegóły użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4e58a-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="4e58a-143">Opłata magazynu Marketplace interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4e58a-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="4e58a-144">Interfejs API arkusza cen</span><span class="sxs-lookup"><span data-stu-id="4e58a-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)