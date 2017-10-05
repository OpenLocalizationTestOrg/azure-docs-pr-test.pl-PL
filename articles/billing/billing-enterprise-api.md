---
title: "Azure rozliczeń interfejsów API Enterprise | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="9dc5b-103">Omówienie API raportowania dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="9dc5b-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="9dc5b-104">Interfejsy API raportowania umożliwiają klientom Enterprise Azure programowo ściągania danych rozliczeń i zużycia do narzędzia do analizy danych preferowany.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="9dc5b-105">Włączanie dostępu do interfejsu API danych</span><span class="sxs-lookup"><span data-stu-id="9dc5b-105">Enabling data access to the API</span></span>
* <span data-ttu-id="9dc5b-106">**Generowanie lub pobrać klucz interfejsu API** — logowanie w witrynie Enterprise portal i wykonaj samouczek w pomocy - API raportowania.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="9dc5b-107">Pierwsza sekcja, w tym artykule pomocy wyjaśniono, jak Generowanie lub pobrać klucz interfejsu API dla określonej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="9dc5b-108">**Przekazywanie kluczy w interfejsie API** — klucz interfejsu API musi zostać przekazany dla każdego wywołania do uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="9dc5b-109">Następująca właściwość musi być z nagłówkami HTTP</span><span class="sxs-lookup"><span data-stu-id="9dc5b-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="9dc5b-110">Klucz nagłówka żądania</span><span class="sxs-lookup"><span data-stu-id="9dc5b-110">Request Header Key</span></span> | <span data-ttu-id="9dc5b-111">Wartość</span><span class="sxs-lookup"><span data-stu-id="9dc5b-111">Value</span></span>|
|-|-|
|<span data-ttu-id="9dc5b-112">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="9dc5b-112">Authorization</span></span>| <span data-ttu-id="9dc5b-113">Określ wartość w następującym formacie: **elementu nośnego {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="9dc5b-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="9dc5b-114">Przykład: eyr elementu nośnego... 09</span><span class="sxs-lookup"><span data-stu-id="9dc5b-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="9dc5b-115">Interfejsy API zużycie</span><span class="sxs-lookup"><span data-stu-id="9dc5b-115">Consumption APIs</span></span>
<span data-ttu-id="9dc5b-116">Punktu końcowego struktury Swagger jest dostępna [tutaj](https://consumption.azure.com/swagger/ui/index) dla interfejsów API opisanego poniżej którego powinien umożliwiają łatwe introspection interfejsu API oraz do generowania zestawy SDK klientów przy użyciu [AutoRest](https://github.com/Azure/AutoRest) lub [programu Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="9dc5b-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="9dc5b-117">Począwszy od 1 maja 2014 danych jest dostępna za pośrednictwem tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="9dc5b-118">**Saldo i Podsumowanie** - [saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md) oferuje miesięczne podsumowanie informacji na temat salda, nowych zakupów, opłaty za usługę Azure Marketplace, zmiany i nadwyżkowe opłat.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="9dc5b-119">**Szczegóły użycia** - [API szczegółów użycia](billing-enterprise-api-usage-detail.md) oferuje zestawienie ilości wykorzystanego i opłat szacowany przy rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="9dc5b-120">Wynik zawiera również informacje dotyczące wystąpień, mierniki i działów.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="9dc5b-121">Interfejs API mogą być przeszukiwane przez okres rozliczeń lub określonej daty rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="9dc5b-122">**Opłata magazynu Marketplace** — [Marketplace magazynu opłat API](billing-enterprise-api-marketplace-storecharge.md) zwraca opartej na użyciu marketplace podział opłaty wg dnia w określonym przedziale czasu rozliczeń lub daty rozpoczęcia i zakończenia (jeden raz opłaty nie są uwzględniane).</span><span class="sxs-lookup"><span data-stu-id="9dc5b-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="9dc5b-123">**Arkusz cen** - [API arkusza cen](billing-enterprise-api-pricesheet.md) udostępnia stawkę dla każdego licznika dla danego rejestracji i okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="9dc5b-124">Interfejsy API pomocy</span><span class="sxs-lookup"><span data-stu-id="9dc5b-124">Helper APIs</span></span>
 <span data-ttu-id="9dc5b-125">**Lista rozliczeń okresów** — [rozliczeń API okresów](billing-enterprise-api-billing-periods.md) zwraca listę rozliczeń okresów, które mają dane dotyczące zużycia dla określonej rejestracji w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="9dc5b-126">Każdego okresu zawiera właściwość wskazujący trasę interfejsu API dla cztery zestawy danych - BalanceSummary, UsageDetails opłat w witrynie Marketplace i arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="9dc5b-127">Kody odpowiedzi interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9dc5b-127">API Response Codes</span></span>  
|<span data-ttu-id="9dc5b-128">Kod stanu odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9dc5b-128">Response Status Code</span></span>|<span data-ttu-id="9dc5b-129">Komunikat</span><span class="sxs-lookup"><span data-stu-id="9dc5b-129">Message</span></span>|<span data-ttu-id="9dc5b-130">Opis</span><span class="sxs-lookup"><span data-stu-id="9dc5b-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="9dc5b-131">200</span><span class="sxs-lookup"><span data-stu-id="9dc5b-131">200</span></span>| <span data-ttu-id="9dc5b-132">OK</span><span class="sxs-lookup"><span data-stu-id="9dc5b-132">OK</span></span>|<span data-ttu-id="9dc5b-133">Błąd braku</span><span class="sxs-lookup"><span data-stu-id="9dc5b-133">No error</span></span>|
|<span data-ttu-id="9dc5b-134">401</span><span class="sxs-lookup"><span data-stu-id="9dc5b-134">401</span></span>| <span data-ttu-id="9dc5b-135">Brak autoryzacji</span><span class="sxs-lookup"><span data-stu-id="9dc5b-135">Unauthorized</span></span>| <span data-ttu-id="9dc5b-136">Klucz interfejsu API nie został znaleziony, nieprawidłowy, ważność itp.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="9dc5b-137">404</span><span class="sxs-lookup"><span data-stu-id="9dc5b-137">404</span></span>| <span data-ttu-id="9dc5b-138">Niedostępne</span><span class="sxs-lookup"><span data-stu-id="9dc5b-138">Unavailable</span></span>| <span data-ttu-id="9dc5b-139">Nie znaleziono punktu końcowego raportu</span><span class="sxs-lookup"><span data-stu-id="9dc5b-139">Report endpoint not found</span></span>|
|<span data-ttu-id="9dc5b-140">400</span><span class="sxs-lookup"><span data-stu-id="9dc5b-140">400</span></span>| <span data-ttu-id="9dc5b-141">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9dc5b-141">Bad Request</span></span>| <span data-ttu-id="9dc5b-142">Nieprawidłowe parametry — zakresy dat, liczb EA itp.</span><span class="sxs-lookup"><span data-stu-id="9dc5b-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="9dc5b-143">500</span><span class="sxs-lookup"><span data-stu-id="9dc5b-143">500</span></span>| <span data-ttu-id="9dc5b-144">Błąd serwera</span><span class="sxs-lookup"><span data-stu-id="9dc5b-144">Server Error</span></span>| <span data-ttu-id="9dc5b-145">Unexoected błąd podczas przetwarzania żądania</span><span class="sxs-lookup"><span data-stu-id="9dc5b-145">Unexoected error processing request</span></span>| 









