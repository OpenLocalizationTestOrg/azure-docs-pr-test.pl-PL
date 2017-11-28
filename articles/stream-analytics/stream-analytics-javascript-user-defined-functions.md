---
title: "Funkcje zdefiniowane przez użytkownika Stream Analytics JavaScript aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="188c5-104">Azure Stream Analytics JavaScript funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="188c5-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="188c5-105">Usługa Azure Stream Analytics obsługuje funkcje zdefiniowane przez użytkownika napisane w języku JavaScript.</span><span class="sxs-lookup"><span data-stu-id="188c5-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="188c5-106">Z hello bogaty zestaw **ciąg**, **RegExp**, **matematyczne**, **tablicy**, i **data** metody który Udostępnia JavaScript, danych złożonych przekształceń zadania usługi analiza strumienia stają się łatwiejsze toocreate.</span><span class="sxs-lookup"><span data-stu-id="188c5-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="188c5-107">JavaScript — funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="188c5-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="188c5-108">Funkcje zdefiniowane przez użytkownika JavaScript obsługuje bezstanowych, tylko do obliczeń funkcje skalarne, które nie wymagają łączność zewnętrzną.</span><span class="sxs-lookup"><span data-stu-id="188c5-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="188c5-109">Witaj zwracać wartość funkcji może być tylko wartość skalarną (jeden).</span><span class="sxs-lookup"><span data-stu-id="188c5-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="188c5-110">Po dodaniu zadania JavaScript tooa funkcja zdefiniowana przez użytkownika funkcja hello dowolne miejsce w zapytaniu hello, takich jak wbudowanych funkcji skalarnej.</span><span class="sxs-lookup"><span data-stu-id="188c5-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="188c5-111">Poniżej przedstawiono kilka scenariuszy, w którym może być przydatne funkcje zdefiniowane przez użytkownika JavaScript:</span><span class="sxs-lookup"><span data-stu-id="188c5-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="188c5-112">Analizowanie i operowanie nimi ciągów, które mają funkcji wyrażenie regularne, na przykład **Regexp_Replace()** i **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="188c5-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="188c5-113">Dekodowanie i kodowania danych, na przykład konwersja binarny szesnastkowy</span><span class="sxs-lookup"><span data-stu-id="188c5-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="188c5-114">Wykonywanie obliczeń mathematic JavaScript **matematyczne** funkcji</span><span class="sxs-lookup"><span data-stu-id="188c5-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="188c5-115">Wykonywanie operacji na tablicy jak sortowania, sprzężenia, Znajdź i wypełnienia</span><span class="sxs-lookup"><span data-stu-id="188c5-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="188c5-116">Poniżej przedstawiono niektóre czynności, które nie można wykonać przy użyciu funkcji zdefiniowanej przez użytkownika JavaScript w Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="188c5-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="188c5-117">Wywołanie limit zewnętrzne punkty końcowe REST, na przykład wykonywania wstecznego wyszukiwania IP lub ściągania danych referencyjnych ze źródła zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="188c5-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="188c5-118">Przeprowadź niestandardowe zdarzenie format serializacji lub deserializacji w danych wejściowych/wyjściowych</span><span class="sxs-lookup"><span data-stu-id="188c5-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="188c5-119">Tworzenie wartości zagregowanych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="188c5-119">Create custom aggregates</span></span>

<span data-ttu-id="188c5-120">Mimo że funkcje takie jak **Date.GetDate()** lub **Math.random()** nie są blokowane w definicji funkcji hello, należy unikać używania ich.</span><span class="sxs-lookup"><span data-stu-id="188c5-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="188c5-121">Te funkcje **nie** zwracany hello sam powoduje za każdym razem należy wywołać i hello usługi Azure Stream Analytics nie przechowuje dziennika wywołania funkcji i zwróciło wyników.</span><span class="sxs-lookup"><span data-stu-id="188c5-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="188c5-122">Jeśli funkcja zwraca różne wyniki na powitania same zdarzenia, powtarzalność nie jest gwarantowana po ponownym uruchomieniu zadania przez Ciebie lub hello usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="188c5-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="188c5-123">Dodawanie funkcji zdefiniowanej przez użytkownika JavaScript w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="188c5-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="188c5-124">toocreate proste funkcji zdefiniowanej przez użytkownika JavaScript w obszarze na istniejące zadanie usługi Stream Analytics, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="188c5-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="188c5-125">W portalu Azure hello Znajdź zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="188c5-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="188c5-126">W obszarze **TOPOLOGII zadania**, wybierz funkcji.</span><span class="sxs-lookup"><span data-stu-id="188c5-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="188c5-127">Zostanie wyświetlona pusta lista funkcji.</span><span class="sxs-lookup"><span data-stu-id="188c5-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="188c5-128">toocreate nowych funkcji zdefiniowanej przez użytkownika, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="188c5-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="188c5-129">Na powitania **nową funkcję** bloku dla **typu funkcji**, wybierz pozycję **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="188c5-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="188c5-130">Domyślny szablon funkcji zostanie wyświetlony w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="188c5-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="188c5-131">Dla hello **UDF alias**, wprowadź **hex2Int**i zmień implementację funkcji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="188c5-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="188c5-132">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="188c5-132">Select **Save**.</span></span> <span data-ttu-id="188c5-133">Funkcji pojawia się na liście hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="188c5-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="188c5-134">Wybierz nowe hello **hex2Int** funkcji i sprawdź hello definicji funkcji.</span><span class="sxs-lookup"><span data-stu-id="188c5-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="188c5-135">Wszystkie funkcje mają **UDF** alias funkcja toohello dodany prefiks.</span><span class="sxs-lookup"><span data-stu-id="188c5-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="188c5-136">Należy zbyt*zawierać prefiks hello* podczas wywołania funkcji hello w kwerendzie Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="188c5-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="188c5-137">W takim przypadku należy wywołać **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="188c5-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="188c5-138">Wywoływanie funkcji zdefiniowanej przez użytkownika JavaScript w kwerendzie</span><span class="sxs-lookup"><span data-stu-id="188c5-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="188c5-139">W hello zapytania edytora, w obszarze **TOPOLOGII zadania**, wybierz pozycję **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="188c5-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="188c5-140">Edytuj zapytanie, a następnie wywołać hello — funkcja zdefiniowana przez użytkownika, takie jak to:</span><span class="sxs-lookup"><span data-stu-id="188c5-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="188c5-141">tooupload hello przykładowy plik danych, kliknij prawym przyciskiem myszy hello zadania w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="188c5-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="188c5-142">tootest kwerendy, wybierz opcję **testu**.</span><span class="sxs-lookup"><span data-stu-id="188c5-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="188c5-143">Obsługiwane obiektów JavaScript</span><span class="sxs-lookup"><span data-stu-id="188c5-143">Supported JavaScript objects</span></span>
<span data-ttu-id="188c5-144">Funkcje zdefiniowane przez użytkownika JavaScript analiza strumienia Azure obsługuje standardowego, wbudowanego obiektów JavaScript.</span><span class="sxs-lookup"><span data-stu-id="188c5-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="188c5-145">Aby uzyskać listę tych obiektów, zobacz [obiektów globalnych](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="188c5-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="188c5-146">Konwersja typu Stream Analytics i języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="188c5-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="188c5-147">Ma różnic w typach hello, które obsługują język zapytań usługi Stream Analytics hello i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="188c5-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="188c5-148">Poniższa tabela zawiera hello konwersji mapowań między hello dwóch:</span><span class="sxs-lookup"><span data-stu-id="188c5-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="188c5-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="188c5-149">Stream Analytics</span></span> | <span data-ttu-id="188c5-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="188c5-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="188c5-151">bigint</span><span class="sxs-lookup"><span data-stu-id="188c5-151">bigint</span></span> | <span data-ttu-id="188c5-152">Numer (JavaScript może reprezentować tylko liczby całkowite się tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="188c5-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="188c5-153">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="188c5-153">DateTime</span></span> | <span data-ttu-id="188c5-154">Data (JavaScript tylko obsługuje w milisekundach)</span><span class="sxs-lookup"><span data-stu-id="188c5-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="188c5-155">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="188c5-155">double</span></span> | <span data-ttu-id="188c5-156">Liczba</span><span class="sxs-lookup"><span data-stu-id="188c5-156">Number</span></span>
<span data-ttu-id="188c5-157">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="188c5-157">nvarchar(MAX)</span></span> | <span data-ttu-id="188c5-158">Ciąg</span><span class="sxs-lookup"><span data-stu-id="188c5-158">String</span></span>
<span data-ttu-id="188c5-159">rekord</span><span class="sxs-lookup"><span data-stu-id="188c5-159">Record</span></span> | <span data-ttu-id="188c5-160">Obiekt</span><span class="sxs-lookup"><span data-stu-id="188c5-160">Object</span></span>
<span data-ttu-id="188c5-161">Tablica</span><span class="sxs-lookup"><span data-stu-id="188c5-161">Array</span></span> | <span data-ttu-id="188c5-162">Tablica</span><span class="sxs-lookup"><span data-stu-id="188c5-162">Array</span></span>
<span data-ttu-id="188c5-163">WARTOŚĆ NULL</span><span class="sxs-lookup"><span data-stu-id="188c5-163">NULL</span></span> | <span data-ttu-id="188c5-164">Wartość null</span><span class="sxs-lookup"><span data-stu-id="188c5-164">Null</span></span>


<span data-ttu-id="188c5-165">Poniżej przedstawiono konwersje JavaScript do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="188c5-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="188c5-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="188c5-166">JavaScript</span></span> | <span data-ttu-id="188c5-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="188c5-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="188c5-168">Liczba</span><span class="sxs-lookup"><span data-stu-id="188c5-168">Number</span></span> | <span data-ttu-id="188c5-169">Bigint (jeśli jest to liczba hello jest okrągłych i między long. Wartość MinValue i długi. MaxValue; w przeciwnym razie jest podwójny)</span><span class="sxs-lookup"><span data-stu-id="188c5-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="188c5-170">Date</span><span class="sxs-lookup"><span data-stu-id="188c5-170">Date</span></span> | <span data-ttu-id="188c5-171">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="188c5-171">DateTime</span></span>
<span data-ttu-id="188c5-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="188c5-172">String</span></span> | <span data-ttu-id="188c5-173">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="188c5-173">nvarchar(MAX)</span></span>
<span data-ttu-id="188c5-174">Obiekt</span><span class="sxs-lookup"><span data-stu-id="188c5-174">Object</span></span> | <span data-ttu-id="188c5-175">rekord</span><span class="sxs-lookup"><span data-stu-id="188c5-175">Record</span></span>
<span data-ttu-id="188c5-176">Tablica</span><span class="sxs-lookup"><span data-stu-id="188c5-176">Array</span></span> | <span data-ttu-id="188c5-177">Tablica</span><span class="sxs-lookup"><span data-stu-id="188c5-177">Array</span></span>
<span data-ttu-id="188c5-178">Wartość null, niezdefiniowane</span><span class="sxs-lookup"><span data-stu-id="188c5-178">Null, Undefined</span></span> | <span data-ttu-id="188c5-179">WARTOŚĆ NULL</span><span class="sxs-lookup"><span data-stu-id="188c5-179">NULL</span></span>
<span data-ttu-id="188c5-180">Innego typu (na przykład funkcja lub błąd)</span><span class="sxs-lookup"><span data-stu-id="188c5-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="188c5-181">Nieobsługiwane (powoduje błąd czasu wykonywania)</span><span class="sxs-lookup"><span data-stu-id="188c5-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="188c5-182">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="188c5-182">Troubleshooting</span></span>
<span data-ttu-id="188c5-183">Błędy środowiska wykonawczego języka JavaScript są traktowane jako błąd krytyczny i są udostępniane za pośrednictwem hello dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="188c5-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="188c5-184">tooretrieve hello logowania, hello portalu Azure, przejdź tooyour zadania i wybierz **dziennik aktywności**.</span><span class="sxs-lookup"><span data-stu-id="188c5-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="188c5-185">Innymi wzorami zdefiniowane przez użytkownika funkcja JavaScript</span><span class="sxs-lookup"><span data-stu-id="188c5-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="188c5-186">Zapis zagnieżdżonych toooutput JSON</span><span class="sxs-lookup"><span data-stu-id="188c5-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="188c5-187">Jeśli masz krok przetwarzania monitowania, który używa jako dane wejściowe zadania usługi analiza strumienia wyjściowego i wymaga formatu JSON, można napisać toooutput ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="188c5-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="188c5-188">Witaj w następnym przykładzie wywołuje hello **JSON.stringify()** funkcji toopack wszystkich par nazwa/wartość hello danych wejściowych, a następnie zapisać je jako pojedynczy ciąg w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="188c5-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="188c5-189">**Definicja funkcji zdefiniowanej przez użytkownika JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="188c5-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="188c5-190">**Przykładowe zapytanie:**</span><span class="sxs-lookup"><span data-stu-id="188c5-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="188c5-191">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="188c5-191">Get help</span></span>
<span data-ttu-id="188c5-192">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="188c5-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="188c5-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="188c5-193">Next steps</span></span>
* [<span data-ttu-id="188c5-194">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="188c5-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="188c5-195">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="188c5-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="188c5-196">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="188c5-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="188c5-197">Dokumentacja języka zapytań usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="188c5-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="188c5-198">Usługa Azure Stream Analytics management dokumentacji interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="188c5-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
