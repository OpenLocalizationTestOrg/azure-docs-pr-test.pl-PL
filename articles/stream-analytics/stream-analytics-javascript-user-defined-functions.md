---
title: "Azure Stream Analytics JavaScript funkcje zdefiniowane przez użytkownika | Dokumentacja firmy Microsoft"
description: "Wykonaj mechanika zaawansowanych zapytań z języka JavaScript funkcje zdefiniowane przez użytkownika"
keywords: "JavaScript, funkcje udf zdefiniowane przez użytkownika"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="840b2-104">Azure Stream Analytics JavaScript funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="840b2-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="840b2-105">Usługa Azure Stream Analytics obsługuje funkcje zdefiniowane przez użytkownika napisane w języku JavaScript.</span><span class="sxs-lookup"><span data-stu-id="840b2-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="840b2-106">Z zaawansowanej zestaw **ciąg**, **RegExp**, **matematyczne**, **tablicy**, i **data** metod tego JavaScript zawiera, danych złożonych przekształceń analiza strumienia zadania stają się łatwiejsze do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="840b2-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="840b2-107">JavaScript — funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="840b2-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="840b2-108">Funkcje zdefiniowane przez użytkownika JavaScript obsługuje bezstanowych, tylko do obliczeń funkcje skalarne, które nie wymagają łączność zewnętrzną.</span><span class="sxs-lookup"><span data-stu-id="840b2-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="840b2-109">Wartość zwracana funkcji można tylko wartość skalarną (jeden).</span><span class="sxs-lookup"><span data-stu-id="840b2-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="840b2-110">Po dodaniu funkcji zdefiniowanej przez użytkownika JavaScript do zadania, funkcja dowolne miejsce w zapytaniu, takich jak wbudowanych funkcji skalarnej.</span><span class="sxs-lookup"><span data-stu-id="840b2-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="840b2-111">Poniżej przedstawiono kilka scenariuszy, w którym może być przydatne funkcje zdefiniowane przez użytkownika JavaScript:</span><span class="sxs-lookup"><span data-stu-id="840b2-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="840b2-112">Analizowanie i operowanie nimi ciągów, które mają funkcji wyrażenie regularne, na przykład **Regexp_Replace()** i **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="840b2-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="840b2-113">Dekodowanie i kodowania danych, na przykład konwersja binarny szesnastkowy</span><span class="sxs-lookup"><span data-stu-id="840b2-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="840b2-114">Wykonywanie obliczeń mathematic JavaScript **matematyczne** funkcji</span><span class="sxs-lookup"><span data-stu-id="840b2-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="840b2-115">Wykonywanie operacji na tablicy jak sortowania, sprzężenia, Znajdź i wypełnienia</span><span class="sxs-lookup"><span data-stu-id="840b2-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="840b2-116">Poniżej przedstawiono niektóre czynności, które nie można wykonać przy użyciu funkcji zdefiniowanej przez użytkownika JavaScript w Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="840b2-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="840b2-117">Wywołanie limit zewnętrzne punkty końcowe REST, na przykład wykonywania wstecznego wyszukiwania IP lub ściągania danych referencyjnych ze źródła zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="840b2-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="840b2-118">Przeprowadź niestandardowe zdarzenie format serializacji lub deserializacji w danych wejściowych/wyjściowych</span><span class="sxs-lookup"><span data-stu-id="840b2-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="840b2-119">Tworzenie wartości zagregowanych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="840b2-119">Create custom aggregates</span></span>

<span data-ttu-id="840b2-120">Mimo że funkcje takie jak **Date.GetDate()** lub **Math.random()** nie są blokowane w definicji funkcji, należy unikać używania ich.</span><span class="sxs-lookup"><span data-stu-id="840b2-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="840b2-121">Te funkcje **nie** zwracać ten sam rezultat za każdym razem należy wywołać i usługą Azure Stream Analytics nie przechowuje dziennika wywołania funkcji i zwróciło wyników.</span><span class="sxs-lookup"><span data-stu-id="840b2-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="840b2-122">Jeśli funkcja zwraca różne wyniki na same zdarzenia, powtarzalność nie jest gwarantowana po ponownym uruchomieniu zadania przez Ciebie lub usługa Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="840b2-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="840b2-123">Dodaj funkcję JavaScript zdefiniowane przez użytkownika w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="840b2-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="840b2-124">Aby utworzyć prosty funkcji zdefiniowanej przez użytkownika JavaScript w obszarze na istniejące zadanie usługi Stream Analytics, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="840b2-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="840b2-125">W portalu Azure Znajdź zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="840b2-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="840b2-126">W obszarze **TOPOLOGII zadania**, wybierz funkcji.</span><span class="sxs-lookup"><span data-stu-id="840b2-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="840b2-127">Zostanie wyświetlona pusta lista funkcji.</span><span class="sxs-lookup"><span data-stu-id="840b2-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="840b2-128">Aby utworzyć nową funkcję zdefiniowane przez użytkownika, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="840b2-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="840b2-129">Na **nową funkcję** bloku dla **typu funkcji**, wybierz pozycję **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="840b2-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="840b2-130">Domyślny szablon funkcji zostanie wyświetlony w edytorze.</span><span class="sxs-lookup"><span data-stu-id="840b2-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="840b2-131">Dla **UDF alias**, wprowadź **hex2Int**i zmień implementację funkcji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="840b2-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="840b2-132">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="840b2-132">Select **Save**.</span></span> <span data-ttu-id="840b2-133">Funkcja zostanie wyświetlony na liście funkcji.</span><span class="sxs-lookup"><span data-stu-id="840b2-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="840b2-134">Wybierz nową **hex2Int** funkcji i sprawdź definicję funkcji.</span><span class="sxs-lookup"><span data-stu-id="840b2-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="840b2-135">Wszystkie funkcje mają **UDF** Prefiks dodawany do aliasu funkcji.</span><span class="sxs-lookup"><span data-stu-id="840b2-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="840b2-136">Musisz *zawierać prefiks* gdy wywołanie funkcji w zapytaniu Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="840b2-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="840b2-137">W takim przypadku należy wywołać **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="840b2-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="840b2-138">Wywoływanie funkcji zdefiniowanej przez użytkownika JavaScript w kwerendzie</span><span class="sxs-lookup"><span data-stu-id="840b2-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="840b2-139">W edytorze zapytań w obszarze **TOPOLOGII zadania**, wybierz pozycję **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="840b2-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="840b2-140">Edytuj zapytanie, a następnie wywołania funkcji zdefiniowanej przez użytkownika, jak to:</span><span class="sxs-lookup"><span data-stu-id="840b2-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="840b2-141">Aby przekazać przykładowy plik danych, kliknij prawym przyciskiem myszy dane wejściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="840b2-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="840b2-142">Aby przetestować zapytanie, wybierz **testu**.</span><span class="sxs-lookup"><span data-stu-id="840b2-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="840b2-143">Obsługiwane obiektów JavaScript</span><span class="sxs-lookup"><span data-stu-id="840b2-143">Supported JavaScript objects</span></span>
<span data-ttu-id="840b2-144">Funkcje zdefiniowane przez użytkownika JavaScript analiza strumienia Azure obsługuje standardowego, wbudowanego obiektów JavaScript.</span><span class="sxs-lookup"><span data-stu-id="840b2-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="840b2-145">Aby uzyskać listę tych obiektów, zobacz [obiektów globalnych](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="840b2-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="840b2-146">Konwersja typu Stream Analytics i języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="840b2-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="840b2-147">Ma różnic w typach, że analiza strumienia zapytania języka i obsługi języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="840b2-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="840b2-148">Poniższa tabela zawiera mapowania konwersji między nimi:</span><span class="sxs-lookup"><span data-stu-id="840b2-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="840b2-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="840b2-149">Stream Analytics</span></span> | <span data-ttu-id="840b2-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="840b2-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="840b2-151">bigint</span><span class="sxs-lookup"><span data-stu-id="840b2-151">bigint</span></span> | <span data-ttu-id="840b2-152">Numer (JavaScript może reprezentować tylko liczby całkowite maksymalnie dokładnie 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="840b2-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="840b2-153">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="840b2-153">DateTime</span></span> | <span data-ttu-id="840b2-154">Data (JavaScript tylko obsługuje w milisekundach)</span><span class="sxs-lookup"><span data-stu-id="840b2-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="840b2-155">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="840b2-155">double</span></span> | <span data-ttu-id="840b2-156">Numer</span><span class="sxs-lookup"><span data-stu-id="840b2-156">Number</span></span>
<span data-ttu-id="840b2-157">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="840b2-157">nvarchar(MAX)</span></span> | <span data-ttu-id="840b2-158">Ciąg</span><span class="sxs-lookup"><span data-stu-id="840b2-158">String</span></span>
<span data-ttu-id="840b2-159">rekord</span><span class="sxs-lookup"><span data-stu-id="840b2-159">Record</span></span> | <span data-ttu-id="840b2-160">Obiekt</span><span class="sxs-lookup"><span data-stu-id="840b2-160">Object</span></span>
<span data-ttu-id="840b2-161">Tablica</span><span class="sxs-lookup"><span data-stu-id="840b2-161">Array</span></span> | <span data-ttu-id="840b2-162">Tablica</span><span class="sxs-lookup"><span data-stu-id="840b2-162">Array</span></span>
<span data-ttu-id="840b2-163">WARTOŚĆ NULL</span><span class="sxs-lookup"><span data-stu-id="840b2-163">NULL</span></span> | <span data-ttu-id="840b2-164">Wartość null</span><span class="sxs-lookup"><span data-stu-id="840b2-164">Null</span></span>


<span data-ttu-id="840b2-165">Poniżej przedstawiono konwersje JavaScript do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="840b2-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="840b2-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="840b2-166">JavaScript</span></span> | <span data-ttu-id="840b2-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="840b2-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="840b2-168">Numer</span><span class="sxs-lookup"><span data-stu-id="840b2-168">Number</span></span> | <span data-ttu-id="840b2-169">Bigint (Jeśli liczba jest okrągłych i między long. Wartość MinValue i długi. MaxValue; w przeciwnym razie jest podwójny)</span><span class="sxs-lookup"><span data-stu-id="840b2-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="840b2-170">Date</span><span class="sxs-lookup"><span data-stu-id="840b2-170">Date</span></span> | <span data-ttu-id="840b2-171">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="840b2-171">DateTime</span></span>
<span data-ttu-id="840b2-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="840b2-172">String</span></span> | <span data-ttu-id="840b2-173">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="840b2-173">nvarchar(MAX)</span></span>
<span data-ttu-id="840b2-174">Obiekt</span><span class="sxs-lookup"><span data-stu-id="840b2-174">Object</span></span> | <span data-ttu-id="840b2-175">rekord</span><span class="sxs-lookup"><span data-stu-id="840b2-175">Record</span></span>
<span data-ttu-id="840b2-176">Tablica</span><span class="sxs-lookup"><span data-stu-id="840b2-176">Array</span></span> | <span data-ttu-id="840b2-177">Tablica</span><span class="sxs-lookup"><span data-stu-id="840b2-177">Array</span></span>
<span data-ttu-id="840b2-178">Wartość null, niezdefiniowane</span><span class="sxs-lookup"><span data-stu-id="840b2-178">Null, Undefined</span></span> | <span data-ttu-id="840b2-179">WARTOŚĆ NULL</span><span class="sxs-lookup"><span data-stu-id="840b2-179">NULL</span></span>
<span data-ttu-id="840b2-180">Innego typu (na przykład funkcja lub błąd)</span><span class="sxs-lookup"><span data-stu-id="840b2-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="840b2-181">Nieobsługiwane (powoduje błąd czasu wykonywania)</span><span class="sxs-lookup"><span data-stu-id="840b2-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="840b2-182">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="840b2-182">Troubleshooting</span></span>
<span data-ttu-id="840b2-183">Błędy środowiska wykonawczego języka JavaScript są traktowane jako błąd krytyczny i są udostępniane za pośrednictwem dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="840b2-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="840b2-184">Aby uzyskać dostęp do dziennika, w portalu Azure, przejdź do zadania i wybierz **dziennik aktywności**.</span><span class="sxs-lookup"><span data-stu-id="840b2-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="840b2-185">Innymi wzorami zdefiniowane przez użytkownika funkcja JavaScript</span><span class="sxs-lookup"><span data-stu-id="840b2-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="840b2-186">Zapis zagnieżdżonych JSON do danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="840b2-186">Write nested JSON to output</span></span>
<span data-ttu-id="840b2-187">Jeśli masz krok przetwarzania monitowania, który używa jako dane wejściowe zadania usługi analiza strumienia wyjściowego i wymaga formatu JSON, może zapisać ciąg JSON do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="840b2-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="840b2-188">Następnym przykładzie wywołuje **JSON.stringify()** funkcja pakietu wszystkie pary nazwa/wartość w danych wejściowych, a następnie zapisać je jako pojedynczy ciąg w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="840b2-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="840b2-189">**Definicja funkcji zdefiniowanej przez użytkownika JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="840b2-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="840b2-190">**Przykładowe zapytanie:**</span><span class="sxs-lookup"><span data-stu-id="840b2-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="840b2-191">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="840b2-191">Get help</span></span>
<span data-ttu-id="840b2-192">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="840b2-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="840b2-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="840b2-193">Next steps</span></span>
* [<span data-ttu-id="840b2-194">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="840b2-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="840b2-195">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="840b2-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="840b2-196">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="840b2-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="840b2-197">Dokumentacja języka zapytań usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="840b2-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="840b2-198">Usługa Azure Stream Analytics management dokumentacji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="840b2-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
