---
title: "aaaAzure rozliczeń interfejsów API Enterprise | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="ddb6d-103">Omówienie API raportowania dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="ddb6d-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="ddb6d-104">Witaj raportowania interfejsy API umożliwia Enterprise Azure klienci tooprogrammatically ściągania konsumenckich i danych dotyczących rozliczeń do narzędzia do analizy danych preferowany.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="ddb6d-105">Włączanie interfejsu API toohello dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="ddb6d-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="ddb6d-106">**Generowanie lub pobrać klucza interfejsu API hello** — dziennik toohello Enterprise portal i wykonaj hello samouczka w pomocy - API raportowania.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="ddb6d-107">Hello w pierwszej sekcji tego artykułu Pomocy opisano, jak toogenerate lub pobrać klucz hello interfejsu API dla hello określony rejestracji.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="ddb6d-108">**Przekazując klucze interfejsu API hello** — klucz interfejsu API hello musi toobe przekazany dla każdego wywołania do uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="ddb6d-109">Witaj następującej właściwości musi nagłówki toohello HTTP toobe</span><span class="sxs-lookup"><span data-stu-id="ddb6d-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="ddb6d-110">Klucz nagłówka żądania</span><span class="sxs-lookup"><span data-stu-id="ddb6d-110">Request Header Key</span></span> | <span data-ttu-id="ddb6d-111">Wartość</span><span class="sxs-lookup"><span data-stu-id="ddb6d-111">Value</span></span>|
|-|-|
|<span data-ttu-id="ddb6d-112">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="ddb6d-112">Authorization</span></span>| <span data-ttu-id="ddb6d-113">Określ wartość hello w następującym formacie: **elementu nośnego {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="ddb6d-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="ddb6d-114">Przykład: eyr elementu nośnego... 09</span><span class="sxs-lookup"><span data-stu-id="ddb6d-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="ddb6d-115">Interfejsy API zużycie</span><span class="sxs-lookup"><span data-stu-id="ddb6d-115">Consumption APIs</span></span>
<span data-ttu-id="ddb6d-116">Punktu końcowego struktury Swagger jest dostępna [tutaj](https://consumption.azure.com/swagger/ui/index) dla hello interfejsów API opisane poniżej którego powinien Włącz introspection łatwe hello interfejsu API i zestawów SDK klienta toogenerate możliwości hello [AutoRest](https://github.com/Azure/AutoRest) lub [ Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="ddb6d-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="ddb6d-117">Począwszy od 1 maja 2014 danych jest dostępna za pośrednictwem tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="ddb6d-118">**Saldo i Podsumowanie** — Witaj [saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md) oferuje miesięczne podsumowanie informacji na temat salda, nowych zakupów, opłaty za usługę Azure Marketplace, zmiany i nadwyżkowe opłat.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="ddb6d-119">**Szczegóły użycia** — Witaj [API szczegółów użycia](billing-enterprise-api-usage-detail.md) oferuje zestawienie ilości wykorzystanego i opłat szacowany przy rejestracji.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="ddb6d-120">wynik Hello zawiera również informacje dotyczące wystąpień, mierniki i działów.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="ddb6d-121">Witaj interfejsu API mogą być przeszukiwane przez okres rozliczeń lub określona data rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="ddb6d-122">**Opłata magazynu Marketplace** — Witaj [Marketplace magazynu opłat API](billing-enterprise-api-marketplace-storecharge.md) zwraca hello opartej na użyciu marketplace opłat podział według dnia dla hello określonego okresu rozliczeniowego lub daty rozpoczęcia i zakończenia (jeden raz opłaty nie są uwzględniane) .</span><span class="sxs-lookup"><span data-stu-id="ddb6d-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="ddb6d-123">**Arkusz cen** — Witaj [API arkusza cen](billing-enterprise-api-pricesheet.md) udostępnia hello stawkę dla każdego licznika dla hello rejestracji i okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="ddb6d-124">Interfejsy API pomocy</span><span class="sxs-lookup"><span data-stu-id="ddb6d-124">Helper APIs</span></span>
 <span data-ttu-id="ddb6d-125">**Lista rozliczeń okresów** — Witaj [rozliczeń API okresów](billing-enterprise-api-billing-periods.md) zwraca listę rozliczeń okresów, które mają dane dotyczące zużycia dla hello określonych rejestracji w odwrotnej kolejności chronologicznej.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="ddb6d-126">Każdego okresu zawiera właściwość wskazujący trasę interfejsu API toohello dla hello cztery zestawy danych - BalanceSummary, UsageDetails opłat w witrynie Marketplace i arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="ddb6d-127">Kody odpowiedzi interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ddb6d-127">API Response Codes</span></span>  
|<span data-ttu-id="ddb6d-128">Kod stanu odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ddb6d-128">Response Status Code</span></span>|<span data-ttu-id="ddb6d-129">Komunikat</span><span class="sxs-lookup"><span data-stu-id="ddb6d-129">Message</span></span>|<span data-ttu-id="ddb6d-130">Opis</span><span class="sxs-lookup"><span data-stu-id="ddb6d-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="ddb6d-131">200</span><span class="sxs-lookup"><span data-stu-id="ddb6d-131">200</span></span>| <span data-ttu-id="ddb6d-132">OK</span><span class="sxs-lookup"><span data-stu-id="ddb6d-132">OK</span></span>|<span data-ttu-id="ddb6d-133">Błąd braku</span><span class="sxs-lookup"><span data-stu-id="ddb6d-133">No error</span></span>|
|<span data-ttu-id="ddb6d-134">401</span><span class="sxs-lookup"><span data-stu-id="ddb6d-134">401</span></span>| <span data-ttu-id="ddb6d-135">Brak autoryzacji</span><span class="sxs-lookup"><span data-stu-id="ddb6d-135">Unauthorized</span></span>| <span data-ttu-id="ddb6d-136">Klucz interfejsu API nie został znaleziony, nieprawidłowy, ważność itp.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="ddb6d-137">404</span><span class="sxs-lookup"><span data-stu-id="ddb6d-137">404</span></span>| <span data-ttu-id="ddb6d-138">Niedostępne</span><span class="sxs-lookup"><span data-stu-id="ddb6d-138">Unavailable</span></span>| <span data-ttu-id="ddb6d-139">Nie znaleziono punktu końcowego raportu</span><span class="sxs-lookup"><span data-stu-id="ddb6d-139">Report endpoint not found</span></span>|
|<span data-ttu-id="ddb6d-140">400</span><span class="sxs-lookup"><span data-stu-id="ddb6d-140">400</span></span>| <span data-ttu-id="ddb6d-141">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="ddb6d-141">Bad Request</span></span>| <span data-ttu-id="ddb6d-142">Nieprawidłowe parametry — zakresy dat, liczb EA itp.</span><span class="sxs-lookup"><span data-stu-id="ddb6d-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="ddb6d-143">500</span><span class="sxs-lookup"><span data-stu-id="ddb6d-143">500</span></span>| <span data-ttu-id="ddb6d-144">Błąd serwera</span><span class="sxs-lookup"><span data-stu-id="ddb6d-144">Server Error</span></span>| <span data-ttu-id="ddb6d-145">Unexoected błąd podczas przetwarzania żądania</span><span class="sxs-lookup"><span data-stu-id="ddb6d-145">Unexoected error processing request</span></span>| 









