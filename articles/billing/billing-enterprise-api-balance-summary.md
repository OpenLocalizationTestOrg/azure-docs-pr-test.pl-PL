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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="216b4-103">Raportowanie interfejsów API dla klientów korporacyjnych - saldo i podsumowanie</span><span class="sxs-lookup"><span data-stu-id="216b4-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="216b4-104">Hello saldo oraz podsumowanie interfejsu API oferuje miesięczne podsumowanie informacji na temat salda, nowych zakupów, opłaty za usługę Azure Marketplace, zmiany i nadwyżkowe opłat.</span><span class="sxs-lookup"><span data-stu-id="216b4-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="216b4-105">Żądanie</span><span class="sxs-lookup"><span data-stu-id="216b4-105">Request</span></span> 
<span data-ttu-id="216b4-106">Wspólne właściwości nagłówka wymagające toobe dodawane są określone [tutaj](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="216b4-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="216b4-107">Jeśli nie określono okresie rozliczeniowym, dane dotyczące rozliczeń bieżącego hello okresu jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="216b4-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="216b4-108">Metoda</span><span class="sxs-lookup"><span data-stu-id="216b4-108">Method</span></span> | <span data-ttu-id="216b4-109">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="216b4-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="216b4-110">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="216b4-110">GET</span></span>| <span data-ttu-id="216b4-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="216b4-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="216b4-112">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="216b4-112">GET</span></span>| <span data-ttu-id="216b4-113">/billingPeriods/ https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} {billingPeriod} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="216b4-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="216b4-114">Wersja zapoznawcza hello toouse interfejsu API, Zamień v2 v1 w hello powyżej adresu URL.</span><span class="sxs-lookup"><span data-stu-id="216b4-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="216b4-115">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="216b4-115">Response</span></span>

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


<span data-ttu-id="216b4-116">**Definicje właściwości odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="216b4-116">**Response property definitions**</span></span>

|<span data-ttu-id="216b4-117">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="216b4-117">Property Name</span></span>| <span data-ttu-id="216b4-118">Typ</span><span class="sxs-lookup"><span data-stu-id="216b4-118">Type</span></span>| <span data-ttu-id="216b4-119">Opis</span><span class="sxs-lookup"><span data-stu-id="216b4-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="216b4-120">id</span><span class="sxs-lookup"><span data-stu-id="216b4-120">id</span></span>|<span data-ttu-id="216b4-121">Ciąg</span><span class="sxs-lookup"><span data-stu-id="216b4-121">string</span></span>|<span data-ttu-id="216b4-122">Witaj Unikatowy identyfikator określonego okresu rozliczeniowego do rejestracji</span><span class="sxs-lookup"><span data-stu-id="216b4-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="216b4-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="216b4-123">billingPeriodId</span></span>|<span data-ttu-id="216b4-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="216b4-124">string</span></span> |<span data-ttu-id="216b4-125">Witaj identyfikator okresu rozliczeniowego</span><span class="sxs-lookup"><span data-stu-id="216b4-125">hello billing period Id</span></span>|
|<span data-ttu-id="216b4-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="216b4-126">currencyCode</span></span>|<span data-ttu-id="216b4-127">Ciąg</span><span class="sxs-lookup"><span data-stu-id="216b4-127">string</span></span> |<span data-ttu-id="216b4-128">Kod waluty Hello</span><span class="sxs-lookup"><span data-stu-id="216b4-128">hello currency code</span></span>|
|<span data-ttu-id="216b4-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="216b4-129">beginningBalance</span></span>|<span data-ttu-id="216b4-130">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-130">decimal</span></span>| <span data-ttu-id="216b4-131">Saldo początkowe Hello hello okresie rozliczeniowym</span><span class="sxs-lookup"><span data-stu-id="216b4-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="216b4-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="216b4-132">endingBalance</span></span>|<span data-ttu-id="216b4-133">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-133">decimal</span></span>| <span data-ttu-id="216b4-134">Witaj saldo końcowe hello okresie rozliczeniowym (w przypadku otwartych okresów, które to będą aktualizowane codziennie na)</span><span class="sxs-lookup"><span data-stu-id="216b4-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="216b4-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="216b4-135">newPurchases</span></span>|<span data-ttu-id="216b4-136">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-136">decimal</span></span>| <span data-ttu-id="216b4-137">Nowe suma zakupu</span><span class="sxs-lookup"><span data-stu-id="216b4-137">Total new purchase amount</span></span>|
|<span data-ttu-id="216b4-138">dostosowania</span><span class="sxs-lookup"><span data-stu-id="216b4-138">adjustments</span></span>|<span data-ttu-id="216b4-139">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-139">decimal</span></span>| <span data-ttu-id="216b4-140">Łączna kwota korekty</span><span class="sxs-lookup"><span data-stu-id="216b4-140">Total adjustment amount</span></span>|
|<span data-ttu-id="216b4-141">użyte</span><span class="sxs-lookup"><span data-stu-id="216b4-141">utilized</span></span>|<span data-ttu-id="216b4-142">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-142">decimal</span></span>| <span data-ttu-id="216b4-143">Całkowite użycie zobowiązań</span><span class="sxs-lookup"><span data-stu-id="216b4-143">Total Commitment usage</span></span>|
|<span data-ttu-id="216b4-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="216b4-144">serviceOverage</span></span>|<span data-ttu-id="216b4-145">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-145">decimal</span></span>| <span data-ttu-id="216b4-146">Nadwyżkowe elementy w warstwie usług platformy Azure</span><span class="sxs-lookup"><span data-stu-id="216b4-146">Overage for Azure services</span></span>|
|<span data-ttu-id="216b4-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="216b4-147">chargesBilledSeparately</span></span>|<span data-ttu-id="216b4-148">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-148">decimal</span></span>| <span data-ttu-id="216b4-149">Opłaty za rachunki</span><span class="sxs-lookup"><span data-stu-id="216b4-149">Charges Billed separately</span></span>|
|<span data-ttu-id="216b4-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="216b4-150">totalOverage</span></span>|<span data-ttu-id="216b4-151">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-151">decimal</span></span>| <span data-ttu-id="216b4-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="216b4-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="216b4-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="216b4-153">totalUsage</span></span>|<span data-ttu-id="216b4-154">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-154">decimal</span></span>| <span data-ttu-id="216b4-155">Usługa Azure zobowiązań + łączna nadwyżka</span><span class="sxs-lookup"><span data-stu-id="216b4-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="216b4-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="216b4-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="216b4-157">Decimal</span><span class="sxs-lookup"><span data-stu-id="216b4-157">decimal</span></span>| <span data-ttu-id="216b4-158">Całkowita liczba opłat za portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="216b4-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="216b4-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="216b4-159">newPurchasesDetails</span></span>|<span data-ttu-id="216b4-160">Tablicy JSON ciąg par nazwa-wartość</span><span class="sxs-lookup"><span data-stu-id="216b4-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="216b4-161">Lista nowych zakupów</span><span class="sxs-lookup"><span data-stu-id="216b4-161">List of new purchases</span></span>|
|<span data-ttu-id="216b4-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="216b4-162">adjustmentDetails</span></span>|<span data-ttu-id="216b4-163">Tablicy JSON ciąg par nazwa-wartość</span><span class="sxs-lookup"><span data-stu-id="216b4-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="216b4-164">Listy korekt (środki podwyższenie poziomu, SIE, faktury itd.)</span><span class="sxs-lookup"><span data-stu-id="216b4-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="216b4-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="216b4-165">See also</span></span>

* [<span data-ttu-id="216b4-166">Okresy rozliczeń interfejsu API</span><span class="sxs-lookup"><span data-stu-id="216b4-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="216b4-167">Szczegóły użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="216b4-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="216b4-168">Opłata magazynu Marketplace interfejsu API</span><span class="sxs-lookup"><span data-stu-id="216b4-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="216b4-169">Interfejs API arkusza cen</span><span class="sxs-lookup"><span data-stu-id="216b4-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)