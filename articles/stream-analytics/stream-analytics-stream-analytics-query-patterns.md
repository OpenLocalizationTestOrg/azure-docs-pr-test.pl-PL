---
title: "aaaQuery przykłady typowych wzorców użycia w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Typowych wzorców zapytań usługi Azure Stream Analytics"
keywords: "Przykłady zapytań"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="143d9-104">Zapytanie przykłady typowych wzorców użycia usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="143d9-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="143d9-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="143d9-105">Introduction</span></span>
<span data-ttu-id="143d9-106">Zapytania w usłudze Azure Stream Analytics są wyrażone według języka przypominającego SQL zapytań.</span><span class="sxs-lookup"><span data-stu-id="143d9-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="143d9-107">Te zapytania są udokumentowane w hello [materiały referencyjne dotyczące języka zapytań usługi Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="143d9-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="143d9-108">Ten artykuł opisanych rozwiązań tooseveral typowych wzorców zapytań, na podstawie rzeczywistych sytuacji.</span><span class="sxs-lookup"><span data-stu-id="143d9-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="143d9-109">Jest pracy w toku i kontynuuje toobe zaktualizowano o nowe wzorce w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="143d9-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="143d9-110">Przykład zapytania: konwersji typów danych</span><span class="sxs-lookup"><span data-stu-id="143d9-110">Query example: Convert data types</span></span>
<span data-ttu-id="143d9-111">**Opis elementu**: Definiowanie typów hello właściwości na powitania strumienia wejściowego.</span><span class="sxs-lookup"><span data-stu-id="143d9-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="143d9-112">Na przykład wagi samochodu hello pochodzi na powitania strumień wejściowy jako ciągi i musi toobe konwertowane za**INT** tooperform **suma** go.</span><span class="sxs-lookup"><span data-stu-id="143d9-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="143d9-113">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-113">**Input**:</span></span>

| <span data-ttu-id="143d9-114">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-114">Make</span></span> | <span data-ttu-id="143d9-115">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-115">Time</span></span> | <span data-ttu-id="143d9-116">Waga</span><span class="sxs-lookup"><span data-stu-id="143d9-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-117">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-117">Honda</span></span> |<span data-ttu-id="143d9-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="143d9-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="143d9-119">"1000"</span></span> |
| <span data-ttu-id="143d9-120">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-120">Honda</span></span> |<span data-ttu-id="143d9-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="143d9-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="143d9-122">"2000"</span></span> |

<span data-ttu-id="143d9-123">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-123">**Output**:</span></span>

| <span data-ttu-id="143d9-124">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-124">Make</span></span> | <span data-ttu-id="143d9-125">Waga</span><span class="sxs-lookup"><span data-stu-id="143d9-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-126">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-126">Honda</span></span> |<span data-ttu-id="143d9-127">3000</span><span class="sxs-lookup"><span data-stu-id="143d9-127">3000</span></span> |

<span data-ttu-id="143d9-128">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="143d9-129">**Wyjaśnienie**: Użyj **RZUTOWANIA** instrukcji w hello **wagi** pola toospecify jego typu danych.</span><span class="sxs-lookup"><span data-stu-id="143d9-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="143d9-130">Lista hello obsługiwane typy danych w [typy danych (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="143d9-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="143d9-131">Przykład zapytania: nie podobne podobne toodo dopasowanie wzorca</span><span class="sxs-lookup"><span data-stu-id="143d9-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="143d9-132">**Opis elementu**: Sprawdź, czy wartość pola w zdarzeniu hello ze wzorcem niektórych.</span><span class="sxs-lookup"><span data-stu-id="143d9-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="143d9-133">Na przykład sprawdzić, czy wynik hello zwraca płyt licencji, które A zaczynać się i kończyć 9.</span><span class="sxs-lookup"><span data-stu-id="143d9-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="143d9-134">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-134">**Input**:</span></span>

| <span data-ttu-id="143d9-135">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-135">Make</span></span> | <span data-ttu-id="143d9-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-136">LicensePlate</span></span> | <span data-ttu-id="143d9-137">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-138">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-138">Honda</span></span> |<span data-ttu-id="143d9-139">ABC 123</span><span class="sxs-lookup"><span data-stu-id="143d9-139">ABC-123</span></span> |<span data-ttu-id="143d9-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-141">Toyota</span></span> |<span data-ttu-id="143d9-142">AAA 999</span><span class="sxs-lookup"><span data-stu-id="143d9-142">AAA-999</span></span> |<span data-ttu-id="143d9-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="143d9-144">Nissan</span></span> |<span data-ttu-id="143d9-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="143d9-145">ABC-369</span></span> |<span data-ttu-id="143d9-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-147">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-147">**Output**:</span></span>

| <span data-ttu-id="143d9-148">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-148">Make</span></span> | <span data-ttu-id="143d9-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-149">LicensePlate</span></span> | <span data-ttu-id="143d9-150">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-151">Toyota</span></span> |<span data-ttu-id="143d9-152">AAA 999</span><span class="sxs-lookup"><span data-stu-id="143d9-152">AAA-999</span></span> |<span data-ttu-id="143d9-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="143d9-154">Nissan</span></span> |<span data-ttu-id="143d9-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="143d9-155">ABC-369</span></span> |<span data-ttu-id="143d9-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-157">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="143d9-158">**Wyjaśnienie**: Użyj hello **jak** hello toocheck instrukcji **LicensePlate** wartość w polu.</span><span class="sxs-lookup"><span data-stu-id="143d9-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="143d9-159">Powinna zaczynać A, a następnie mieć dowolny ciąg zawierający zero lub więcej znaków i następnie kończyć 9.</span><span class="sxs-lookup"><span data-stu-id="143d9-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="143d9-160">Przykład zapytania: Określ logikę różnych przypadków/wartości (instrukcji CASE)</span><span class="sxs-lookup"><span data-stu-id="143d9-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="143d9-161">**Opis elementu**: Podaj innej obliczania pola, na podstawie określonego kryterium.</span><span class="sxs-lookup"><span data-stu-id="143d9-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="143d9-162">Na przykład można podać opis ciągu ile samochodów dla hello same należy przekazany z szczególnych przypadkach 1.</span><span class="sxs-lookup"><span data-stu-id="143d9-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="143d9-163">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-163">**Input**:</span></span>

| <span data-ttu-id="143d9-164">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-164">Make</span></span> | <span data-ttu-id="143d9-165">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-166">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-166">Honda</span></span> |<span data-ttu-id="143d9-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-168">Toyota</span></span> |<span data-ttu-id="143d9-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-170">Toyota</span></span> |<span data-ttu-id="143d9-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-172">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-172">**Output**:</span></span>

| <span data-ttu-id="143d9-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="143d9-173">CarsPassed</span></span> | <span data-ttu-id="143d9-174">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-175">1 Honda</span></span> |<span data-ttu-id="143d9-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="143d9-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="143d9-177">2 Toyotas</span></span> |<span data-ttu-id="143d9-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="143d9-179">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="143d9-180">**Wyjaśnienie**: hello **przypadku** klauzuli pozwala nam tooprovide różnych obliczeń, na podstawie kryteriów, niektóre (w tym przypadku hello liczba samochodów hello w oknie agregacji hello).</span><span class="sxs-lookup"><span data-stu-id="143d9-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="143d9-181">Przykład zapytania: wysyłanie danych wyjściowych toomultiple danych</span><span class="sxs-lookup"><span data-stu-id="143d9-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="143d9-182">**Opis elementu**: toomultiple danych wysyłania danych wyjściowych obiektów docelowych w jednym zadaniu.</span><span class="sxs-lookup"><span data-stu-id="143d9-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="143d9-183">Na przykład analizować dane oparte na wartościach progowych alertu i wszystkie zdarzenia tooblob magazyn archiwum.</span><span class="sxs-lookup"><span data-stu-id="143d9-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="143d9-184">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-184">**Input**:</span></span>

| <span data-ttu-id="143d9-185">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-185">Make</span></span> | <span data-ttu-id="143d9-186">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-187">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-187">Honda</span></span> |<span data-ttu-id="143d9-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-189">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-189">Honda</span></span> |<span data-ttu-id="143d9-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-191">Toyota</span></span> |<span data-ttu-id="143d9-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-193">Toyota</span></span> |<span data-ttu-id="143d9-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-195">Toyota</span></span> |<span data-ttu-id="143d9-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="143d9-197">**Output1**:</span></span>

| <span data-ttu-id="143d9-198">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-198">Make</span></span> | <span data-ttu-id="143d9-199">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-200">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-200">Honda</span></span> |<span data-ttu-id="143d9-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-202">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-202">Honda</span></span> |<span data-ttu-id="143d9-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-204">Toyota</span></span> |<span data-ttu-id="143d9-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-206">Toyota</span></span> |<span data-ttu-id="143d9-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-208">Toyota</span></span> |<span data-ttu-id="143d9-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="143d9-210">**Output2**:</span></span>

| <span data-ttu-id="143d9-211">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-211">Make</span></span> | <span data-ttu-id="143d9-212">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-212">Time</span></span> | <span data-ttu-id="143d9-213">Licznik</span><span class="sxs-lookup"><span data-stu-id="143d9-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-214">Toyota</span></span> |<span data-ttu-id="143d9-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="143d9-216">3</span><span class="sxs-lookup"><span data-stu-id="143d9-216">3</span></span> |

<span data-ttu-id="143d9-217">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="143d9-218">**Wyjaśnienie**: hello **INTO** klauzuli informuje usługi analiza strumienia, który hello generuje toowrite hello danych toofrom tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="143d9-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="143d9-219">Witaj pierwszego zapytania jest przekazywanie danych hello Otrzymaliśmy wynik tooan nasze konto nazywa się **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="143d9-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="143d9-220">Witaj drugiego zapytania jest niektórych prostych agregacji i filtrowanie i wysyła wyników hello tooa podrzędne system alertów.</span><span class="sxs-lookup"><span data-stu-id="143d9-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="143d9-221">Możesz również użyć hello wyniki hello wspólnych wyrażeniach tabel (wyrażeń CTE) Uwaga (takich jak **WITH** instrukcje) w wielu deklaracjach danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="143d9-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="143d9-222">Ta opcja ma hello dodatkowa korzyść otwarcia mniej źródło danych wejściowych toohello czytników.</span><span class="sxs-lookup"><span data-stu-id="143d9-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="143d9-223">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="143d9-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="143d9-224">Przykład zapytania: liczba unikatowych wartości</span><span class="sxs-lookup"><span data-stu-id="143d9-224">Query example: Count unique values</span></span>
<span data-ttu-id="143d9-225">**Opis elementu**: liczba hello liczbę unikatowych wartości pól wyświetlanych w strumieniu hello w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="143d9-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="143d9-226">Na przykład ile unikatowy sprawia, że przekazywane stoisku przez hello w oknie 2 sekundy samochodów?</span><span class="sxs-lookup"><span data-stu-id="143d9-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="143d9-227">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-227">**Input**:</span></span>

| <span data-ttu-id="143d9-228">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-228">Make</span></span> | <span data-ttu-id="143d9-229">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-230">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-230">Honda</span></span> |<span data-ttu-id="143d9-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-232">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-232">Honda</span></span> |<span data-ttu-id="143d9-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-234">Toyota</span></span> |<span data-ttu-id="143d9-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-236">Toyota</span></span> |<span data-ttu-id="143d9-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-238">Toyota</span></span> |<span data-ttu-id="143d9-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="143d9-240">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="143d9-240">**Output:**</span></span>

| <span data-ttu-id="143d9-241">Licznik</span><span class="sxs-lookup"><span data-stu-id="143d9-241">Count</span></span> | <span data-ttu-id="143d9-242">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-243">2</span><span class="sxs-lookup"><span data-stu-id="143d9-243">2</span></span> |<span data-ttu-id="143d9-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="143d9-245">1</span><span class="sxs-lookup"><span data-stu-id="143d9-245">1</span></span> |<span data-ttu-id="143d9-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="143d9-247">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="143d9-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="143d9-248">**Wyjaśnienie:**
**COUNT (różne upewnij)** zwraca hello liczbę unikatowych wartości w hello **upewnij** kolumny w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="143d9-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="143d9-249">Przykład zapytania: ustalić, jeśli wartość została zmieniona</span><span class="sxs-lookup"><span data-stu-id="143d9-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="143d9-250">**Opis elementu**: przyjrzyj poprzedniej toodetermine wartość, jeśli jest inny niż bieżąca wartość hello.</span><span class="sxs-lookup"><span data-stu-id="143d9-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="143d9-251">Na przykład jest hello poprzedniej samochodu na powitania przez drogowej hello przez sam jako bieżący samochodu hello?</span><span class="sxs-lookup"><span data-stu-id="143d9-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="143d9-252">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-252">**Input**:</span></span>

| <span data-ttu-id="143d9-253">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-253">Make</span></span> | <span data-ttu-id="143d9-254">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-255">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-255">Honda</span></span> |<span data-ttu-id="143d9-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-257">Toyota</span></span> |<span data-ttu-id="143d9-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="143d9-259">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-259">**Output**:</span></span>

| <span data-ttu-id="143d9-260">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-260">Make</span></span> | <span data-ttu-id="143d9-261">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-262">Toyota</span></span> |<span data-ttu-id="143d9-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="143d9-264">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="143d9-265">**Wyjaśnienie**: Użyj **LAG** toopeek do hello wejściowy strumienia wstecz jedno zdarzenie i pobrać hello **upewnij** wartość.</span><span class="sxs-lookup"><span data-stu-id="143d9-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="143d9-266">Porównaj je po toohello **upewnij** wartość na powitania bieżącego zdarzenia i dane wyjściowe hello zdarzeń, gdy są one różne.</span><span class="sxs-lookup"><span data-stu-id="143d9-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="143d9-267">Przykład zapytania: Znajdź hello pierwszego zdarzenia w oknie</span><span class="sxs-lookup"><span data-stu-id="143d9-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="143d9-268">**Opis elementu**: Znajdź hello pierwszego samochodu w co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="143d9-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="143d9-269">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-269">**Input**:</span></span>

| <span data-ttu-id="143d9-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-270">LicensePlate</span></span> | <span data-ttu-id="143d9-271">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-271">Make</span></span> | <span data-ttu-id="143d9-272">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="143d9-273">DXE 5291</span></span> |<span data-ttu-id="143d9-274">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-274">Honda</span></span> |<span data-ttu-id="143d9-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="143d9-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="143d9-276">YZK 5704</span></span> |<span data-ttu-id="143d9-277">Ford</span><span class="sxs-lookup"><span data-stu-id="143d9-277">Ford</span></span> |<span data-ttu-id="143d9-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="143d9-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="143d9-279">RMV 8282</span></span> |<span data-ttu-id="143d9-280">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-280">Honda</span></span> |<span data-ttu-id="143d9-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="143d9-282">YHN 6970</span></span> |<span data-ttu-id="143d9-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-283">Toyota</span></span> |<span data-ttu-id="143d9-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="143d9-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="143d9-285">VFE 1616</span></span> |<span data-ttu-id="143d9-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-286">Toyota</span></span> |<span data-ttu-id="143d9-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="143d9-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="143d9-288">QYF 9358</span></span> |<span data-ttu-id="143d9-289">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-289">Honda</span></span> |<span data-ttu-id="143d9-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="143d9-291">MDR 6128</span></span> |<span data-ttu-id="143d9-292">BMW</span><span class="sxs-lookup"><span data-stu-id="143d9-292">BMW</span></span> |<span data-ttu-id="143d9-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="143d9-294">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-294">**Output**:</span></span>

| <span data-ttu-id="143d9-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-295">LicensePlate</span></span> | <span data-ttu-id="143d9-296">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-296">Make</span></span> | <span data-ttu-id="143d9-297">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="143d9-298">DXE 5291</span></span> |<span data-ttu-id="143d9-299">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-299">Honda</span></span> |<span data-ttu-id="143d9-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="143d9-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="143d9-301">QYF 9358</span></span> |<span data-ttu-id="143d9-302">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-302">Honda</span></span> |<span data-ttu-id="143d9-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="143d9-304">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="143d9-305">Teraz upewnijmy zmiany hello problemu i Znajdź hello pierwszego samochodu konkretnej co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="143d9-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="143d9-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-306">LicensePlate</span></span> | <span data-ttu-id="143d9-307">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-307">Make</span></span> | <span data-ttu-id="143d9-308">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="143d9-309">DXE 5291</span></span> |<span data-ttu-id="143d9-310">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-310">Honda</span></span> |<span data-ttu-id="143d9-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="143d9-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="143d9-312">YZK 5704</span></span> |<span data-ttu-id="143d9-313">Ford</span><span class="sxs-lookup"><span data-stu-id="143d9-313">Ford</span></span> |<span data-ttu-id="143d9-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="143d9-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="143d9-315">YHN 6970</span></span> |<span data-ttu-id="143d9-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-316">Toyota</span></span> |<span data-ttu-id="143d9-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="143d9-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="143d9-318">QYF 9358</span></span> |<span data-ttu-id="143d9-319">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-319">Honda</span></span> |<span data-ttu-id="143d9-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="143d9-321">MDR 6128</span></span> |<span data-ttu-id="143d9-322">BMW</span><span class="sxs-lookup"><span data-stu-id="143d9-322">BMW</span></span> |<span data-ttu-id="143d9-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="143d9-324">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="143d9-325">Przykład zapytania: hello Znajdź ostatnie zdarzenie w oknie</span><span class="sxs-lookup"><span data-stu-id="143d9-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="143d9-326">**Opis elementu**: Znajdź hello ostatniego samochodu w co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="143d9-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="143d9-327">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-327">**Input**:</span></span>

| <span data-ttu-id="143d9-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-328">LicensePlate</span></span> | <span data-ttu-id="143d9-329">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-329">Make</span></span> | <span data-ttu-id="143d9-330">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="143d9-331">DXE 5291</span></span> |<span data-ttu-id="143d9-332">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-332">Honda</span></span> |<span data-ttu-id="143d9-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="143d9-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="143d9-334">YZK 5704</span></span> |<span data-ttu-id="143d9-335">Ford</span><span class="sxs-lookup"><span data-stu-id="143d9-335">Ford</span></span> |<span data-ttu-id="143d9-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="143d9-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="143d9-337">RMV 8282</span></span> |<span data-ttu-id="143d9-338">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-338">Honda</span></span> |<span data-ttu-id="143d9-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="143d9-340">YHN 6970</span></span> |<span data-ttu-id="143d9-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-341">Toyota</span></span> |<span data-ttu-id="143d9-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="143d9-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="143d9-343">VFE 1616</span></span> |<span data-ttu-id="143d9-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-344">Toyota</span></span> |<span data-ttu-id="143d9-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="143d9-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="143d9-346">QYF 9358</span></span> |<span data-ttu-id="143d9-347">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-347">Honda</span></span> |<span data-ttu-id="143d9-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="143d9-349">MDR 6128</span></span> |<span data-ttu-id="143d9-350">BMW</span><span class="sxs-lookup"><span data-stu-id="143d9-350">BMW</span></span> |<span data-ttu-id="143d9-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="143d9-352">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-352">**Output**:</span></span>

| <span data-ttu-id="143d9-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-353">LicensePlate</span></span> | <span data-ttu-id="143d9-354">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-354">Make</span></span> | <span data-ttu-id="143d9-355">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="143d9-356">VFE 1616</span></span> |<span data-ttu-id="143d9-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-357">Toyota</span></span> |<span data-ttu-id="143d9-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="143d9-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="143d9-359">MDR 6128</span></span> |<span data-ttu-id="143d9-360">BMW</span><span class="sxs-lookup"><span data-stu-id="143d9-360">BMW</span></span> |<span data-ttu-id="143d9-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="143d9-362">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="143d9-363">**Wyjaśnienie**: istnieją dwa kroki w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="143d9-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="143d9-364">Hello pierwszy znalezione przez jeden hello najnowsze sygnatury czasowej w systemie windows 10 minut.</span><span class="sxs-lookup"><span data-stu-id="143d9-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="143d9-365">Witaj drugi krok sprzężenia hello wyniki hello pierwszego zapytania z hello oryginalnego strumienia toofind hello zdarzeń pasujących hello ostatniego sygnatury czasowe w każdym okna.</span><span class="sxs-lookup"><span data-stu-id="143d9-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="143d9-366">Przykład zapytania: wykrywanie hello braku zdarzeń</span><span class="sxs-lookup"><span data-stu-id="143d9-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="143d9-367">**Opis elementu**: Sprawdź, czy strumień nie ma wartości odpowiadający niektórych kryterium.</span><span class="sxs-lookup"><span data-stu-id="143d9-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="143d9-368">Na przykład 2 kolejnych samochodów z hello przez sam wprowadzony hello przez drogowej w hello ostatnich 90 sekund?</span><span class="sxs-lookup"><span data-stu-id="143d9-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="143d9-369">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-369">**Input**:</span></span>

| <span data-ttu-id="143d9-370">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-370">Make</span></span> | <span data-ttu-id="143d9-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-371">LicensePlate</span></span> | <span data-ttu-id="143d9-372">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-373">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-373">Honda</span></span> |<span data-ttu-id="143d9-374">ABC 123</span><span class="sxs-lookup"><span data-stu-id="143d9-374">ABC-123</span></span> |<span data-ttu-id="143d9-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="143d9-376">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-376">Honda</span></span> |<span data-ttu-id="143d9-377">AAA 999</span><span class="sxs-lookup"><span data-stu-id="143d9-377">AAA-999</span></span> |<span data-ttu-id="143d9-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="143d9-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-379">Toyota</span></span> |<span data-ttu-id="143d9-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="143d9-380">DEF-987</span></span> |<span data-ttu-id="143d9-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="143d9-382">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-382">Honda</span></span> |<span data-ttu-id="143d9-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="143d9-383">GHI-345</span></span> |<span data-ttu-id="143d9-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="143d9-385">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-385">**Output**:</span></span>

| <span data-ttu-id="143d9-386">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-386">Make</span></span> | <span data-ttu-id="143d9-387">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-387">Time</span></span> | <span data-ttu-id="143d9-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="143d9-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="143d9-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="143d9-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="143d9-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="143d9-391">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-391">Honda</span></span> |<span data-ttu-id="143d9-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="143d9-393">AAA 999</span><span class="sxs-lookup"><span data-stu-id="143d9-393">AAA-999</span></span> |<span data-ttu-id="143d9-394">ABC 123</span><span class="sxs-lookup"><span data-stu-id="143d9-394">ABC-123</span></span> |<span data-ttu-id="143d9-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="143d9-396">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="143d9-397">**Wyjaśnienie**: Użyj **LAG** toopeek do hello wejściowy strumienia wstecz jedno zdarzenie i pobrać hello **upewnij** wartość.</span><span class="sxs-lookup"><span data-stu-id="143d9-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="143d9-398">Porównaj je toohello **upewnij** wartości hello bieżącego zdarzenia i dane wyjściowe hello zdarzeń, jeśli są one hello takie same.</span><span class="sxs-lookup"><span data-stu-id="143d9-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="143d9-399">Można również użyć **LAG** tooget danych dotyczących samochodów poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="143d9-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="143d9-400">Przykład zapytania: wykrywanie hello czas między zdarzeniami</span><span class="sxs-lookup"><span data-stu-id="143d9-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="143d9-401">**Opis elementu**: Znajdź hello czasu trwania jednego z określonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="143d9-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="143d9-402">Podana clickstream sieci web, na przykład określić czas hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="143d9-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="143d9-403">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-403">**Input**:</span></span>  

| <span data-ttu-id="143d9-404">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="143d9-404">User</span></span> | <span data-ttu-id="143d9-405">Funkcja</span><span class="sxs-lookup"><span data-stu-id="143d9-405">Feature</span></span> | <span data-ttu-id="143d9-406">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="143d9-406">Event</span></span> | <span data-ttu-id="143d9-407">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="143d9-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="143d9-408">RightMenu</span></span> |<span data-ttu-id="143d9-409">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="143d9-409">Start</span></span> |<span data-ttu-id="143d9-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="143d9-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="143d9-411">RightMenu</span></span> |<span data-ttu-id="143d9-412">Koniec</span><span class="sxs-lookup"><span data-stu-id="143d9-412">End</span></span> |<span data-ttu-id="143d9-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="143d9-414">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-414">**Output**:</span></span>  

| <span data-ttu-id="143d9-415">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="143d9-415">User</span></span> | <span data-ttu-id="143d9-416">Funkcja</span><span class="sxs-lookup"><span data-stu-id="143d9-416">Feature</span></span> | <span data-ttu-id="143d9-417">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="143d9-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="143d9-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="143d9-418">RightMenu</span></span> |<span data-ttu-id="143d9-419">7</span><span class="sxs-lookup"><span data-stu-id="143d9-419">7</span></span> |

<span data-ttu-id="143d9-420">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="143d9-421">**Wyjaśnienie**: Użyj hello **ostatniego** ostatniego działać tooretrieve hello **czasu** wartość, gdy typ zdarzenia hello **Start**.</span><span class="sxs-lookup"><span data-stu-id="143d9-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="143d9-422">Witaj **ostatniego** używa **PARTITION BY [użytkownik]** tooindicate, który hello wyniku jest obliczany na unikatowy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="143d9-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="143d9-423">Zapytanie Hello ma maksymalną 1 godzina próg hello odstęp czasu między **Start** i **zatrzymać** zdarzenia, ale można skonfigurować zgodnie z potrzebami **(LIMIT DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="143d9-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="143d9-424">Przykład zapytania: wykrywanie czas trwania hello warunku</span><span class="sxs-lookup"><span data-stu-id="143d9-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="143d9-425">**Opis elementu**: Sprawdzanie, jak długo wystąpił warunek.</span><span class="sxs-lookup"><span data-stu-id="143d9-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="143d9-426">Na przykład załóżmy, że usterki spowodowała wszystkich samochodów niepoprawne ciężar (ponad 20 000 jednostkach funt).</span><span class="sxs-lookup"><span data-stu-id="143d9-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="143d9-427">Chcemy czas trwania hello toocompute hello usterek.</span><span class="sxs-lookup"><span data-stu-id="143d9-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="143d9-428">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-428">**Input**:</span></span>

| <span data-ttu-id="143d9-429">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="143d9-429">Make</span></span> | <span data-ttu-id="143d9-430">Time</span><span class="sxs-lookup"><span data-stu-id="143d9-430">Time</span></span> | <span data-ttu-id="143d9-431">Waga</span><span class="sxs-lookup"><span data-stu-id="143d9-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-432">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-432">Honda</span></span> |<span data-ttu-id="143d9-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="143d9-434">2000</span><span class="sxs-lookup"><span data-stu-id="143d9-434">2000</span></span> |
| <span data-ttu-id="143d9-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-435">Toyota</span></span> |<span data-ttu-id="143d9-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="143d9-437">25000</span><span class="sxs-lookup"><span data-stu-id="143d9-437">25000</span></span> |
| <span data-ttu-id="143d9-438">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-438">Honda</span></span> |<span data-ttu-id="143d9-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="143d9-440">26000</span><span class="sxs-lookup"><span data-stu-id="143d9-440">26000</span></span> |
| <span data-ttu-id="143d9-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-441">Toyota</span></span> |<span data-ttu-id="143d9-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="143d9-443">25000</span><span class="sxs-lookup"><span data-stu-id="143d9-443">25000</span></span> |
| <span data-ttu-id="143d9-444">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-444">Honda</span></span> |<span data-ttu-id="143d9-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="143d9-446">26000</span><span class="sxs-lookup"><span data-stu-id="143d9-446">26000</span></span> |
| <span data-ttu-id="143d9-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-447">Toyota</span></span> |<span data-ttu-id="143d9-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="143d9-449">25000</span><span class="sxs-lookup"><span data-stu-id="143d9-449">25000</span></span> |
| <span data-ttu-id="143d9-450">Honda</span><span class="sxs-lookup"><span data-stu-id="143d9-450">Honda</span></span> |<span data-ttu-id="143d9-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="143d9-452">26000</span><span class="sxs-lookup"><span data-stu-id="143d9-452">26000</span></span> |
| <span data-ttu-id="143d9-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="143d9-453">Toyota</span></span> |<span data-ttu-id="143d9-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="143d9-455">2000</span><span class="sxs-lookup"><span data-stu-id="143d9-455">2000</span></span> |

<span data-ttu-id="143d9-456">**Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-456">**Output**:</span></span>

| <span data-ttu-id="143d9-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="143d9-457">StartFault</span></span> | <span data-ttu-id="143d9-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="143d9-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="143d9-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="143d9-461">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="143d9-462">**Wyjaśnienie**: Użyj **LAG** strumień wejściowy hello tooview przez 24 godziny i wyszukać wystąpienia where **StartFault** i **StopFault** są objęte hello Waga < 20000.</span><span class="sxs-lookup"><span data-stu-id="143d9-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="143d9-463">Przykład zapytania: wypełnienie brakujących wartości</span><span class="sxs-lookup"><span data-stu-id="143d9-463">Query example: Fill missing values</span></span>
<span data-ttu-id="143d9-464">**Opis elementu**: hello strumienia zdarzeń, które nie mają wartości, można utworzyć w strumieniu zdarzeń o regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="143d9-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="143d9-465">Na przykład generują zdarzenie co 5 sekund, która raportuje hello ostatnio widoczne punktu danych.</span><span class="sxs-lookup"><span data-stu-id="143d9-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="143d9-466">**Dane wejściowe**:</span><span class="sxs-lookup"><span data-stu-id="143d9-466">**Input**:</span></span>

| <span data-ttu-id="143d9-467">T</span><span class="sxs-lookup"><span data-stu-id="143d9-467">t</span></span> | <span data-ttu-id="143d9-468">wartość</span><span class="sxs-lookup"><span data-stu-id="143d9-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="143d9-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="143d9-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="143d9-470">1</span><span class="sxs-lookup"><span data-stu-id="143d9-470">1</span></span> |
| <span data-ttu-id="143d9-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="143d9-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="143d9-472">2</span><span class="sxs-lookup"><span data-stu-id="143d9-472">2</span></span> |
| <span data-ttu-id="143d9-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="143d9-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="143d9-474">3</span><span class="sxs-lookup"><span data-stu-id="143d9-474">3</span></span> |
| <span data-ttu-id="143d9-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="143d9-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="143d9-476">4</span><span class="sxs-lookup"><span data-stu-id="143d9-476">4</span></span> |
| <span data-ttu-id="143d9-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="143d9-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="143d9-478">5</span><span class="sxs-lookup"><span data-stu-id="143d9-478">5</span></span> |
| <span data-ttu-id="143d9-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="143d9-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="143d9-480">6</span><span class="sxs-lookup"><span data-stu-id="143d9-480">6</span></span> |

<span data-ttu-id="143d9-481">**Dane wyjściowe (pierwszych 10 wierszy)**:</span><span class="sxs-lookup"><span data-stu-id="143d9-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="143d9-482">windowend</span><span class="sxs-lookup"><span data-stu-id="143d9-482">windowend</span></span> | <span data-ttu-id="143d9-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="143d9-483">lastevent.t</span></span> | <span data-ttu-id="143d9-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="143d9-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="143d9-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="143d9-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="143d9-487">1</span><span class="sxs-lookup"><span data-stu-id="143d9-487">1</span></span> |
| <span data-ttu-id="143d9-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="143d9-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="143d9-490">2</span><span class="sxs-lookup"><span data-stu-id="143d9-490">2</span></span> |
| <span data-ttu-id="143d9-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="143d9-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="143d9-493">3</span><span class="sxs-lookup"><span data-stu-id="143d9-493">3</span></span> |
| <span data-ttu-id="143d9-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="143d9-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="143d9-496">4</span><span class="sxs-lookup"><span data-stu-id="143d9-496">4</span></span> |
| <span data-ttu-id="143d9-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="143d9-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="143d9-499">4</span><span class="sxs-lookup"><span data-stu-id="143d9-499">4</span></span> |
| <span data-ttu-id="143d9-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="143d9-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="143d9-502">4</span><span class="sxs-lookup"><span data-stu-id="143d9-502">4</span></span> |
| <span data-ttu-id="143d9-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="143d9-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="143d9-505">5</span><span class="sxs-lookup"><span data-stu-id="143d9-505">5</span></span> |
| <span data-ttu-id="143d9-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="143d9-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="143d9-508">6</span><span class="sxs-lookup"><span data-stu-id="143d9-508">6</span></span> |
| <span data-ttu-id="143d9-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="143d9-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="143d9-511">6</span><span class="sxs-lookup"><span data-stu-id="143d9-511">6</span></span> |
| <span data-ttu-id="143d9-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="143d9-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="143d9-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="143d9-514">6</span><span class="sxs-lookup"><span data-stu-id="143d9-514">6</span></span> |

<span data-ttu-id="143d9-515">**Rozwiązanie**:</span><span class="sxs-lookup"><span data-stu-id="143d9-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="143d9-516">**Wyjaśnienie**: to zapytanie generuje zdarzenia co 5 sekund i dane wyjściowe hello ostatnie zdarzenie odebrany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="143d9-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="143d9-517">Witaj [okna Hopping](https://msdn.microsoft.com/library/dn835041.aspx "Hopping okno usługi Azure Stream Analytics") czas trwania określa, jak daleko wstecz hello zapytanie wygląda toofind hello najnowsze zdarzenie (300 sekund w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="143d9-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="143d9-518">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="143d9-518">Get help</span></span>
<span data-ttu-id="143d9-519">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="143d9-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="143d9-520">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="143d9-520">Next steps</span></span>
* [<span data-ttu-id="143d9-521">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="143d9-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="143d9-522">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="143d9-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="143d9-523">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="143d9-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="143d9-524">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="143d9-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="143d9-525">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="143d9-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

