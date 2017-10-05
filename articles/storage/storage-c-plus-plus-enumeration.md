---
title: "Lista zasobami magazynu platformy Azure za pomocą biblioteki klienta usługi Storage dla języka C++ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wyliczyć kontenerów, obiektów blob, kolejek, tabel i jednostek za pomocą listy interfejsów API w Biblioteka klienta usługi Microsoft Azure Storage dla języka C++."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 4a4ac7938989f821c092379aff3085f5e440d1c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="b684b-103">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="b684b-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="b684b-104">Lista operacji są kluczem do wielu scenariuszy programowania z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b684b-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="b684b-105">W tym artykule opisano, jak najbardziej efektywne wyliczyć obiektów w usłudze Azure Storage za pomocą listy interfejsów API dostarczonych w biblioteki klienta usługi Microsoft Azure Storage dla języka C++.</span><span class="sxs-lookup"><span data-stu-id="b684b-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="b684b-106">Ten przewodnik jest przeznaczony dla biblioteki klienta usługi Azure Storage dla języka C++ w wersji 2.x, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="b684b-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="b684b-107">Biblioteka klienta magazynu zapewnia różne metody do listy lub kwerendy obiektów w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b684b-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="b684b-108">W tym artykule opisano następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="b684b-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="b684b-109">Kontenery listy konta</span><span class="sxs-lookup"><span data-stu-id="b684b-109">List containers in an account</span></span>
* <span data-ttu-id="b684b-110">Listy BLOB w kontenerze lub katalogu wirtualnego obiektów blob</span><span class="sxs-lookup"><span data-stu-id="b684b-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="b684b-111">Lista kolejek w ramach konta</span><span class="sxs-lookup"><span data-stu-id="b684b-111">List queues in an account</span></span>
* <span data-ttu-id="b684b-112">Listy tabel na koncie</span><span class="sxs-lookup"><span data-stu-id="b684b-112">List tables in an account</span></span>
* <span data-ttu-id="b684b-113">Jednostki zapytania w tabeli</span><span class="sxs-lookup"><span data-stu-id="b684b-113">Query entities in a table</span></span>

<span data-ttu-id="b684b-114">Każda z tych metod jest wyświetlany za pomocą innego przeciążenia dla różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="b684b-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="b684b-115">Asynchroniczne i synchroniczne</span><span class="sxs-lookup"><span data-stu-id="b684b-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="b684b-116">Ponieważ biblioteki klienta usługi Storage dla języka C++ jest oparty na [biblioteki C++ REST](https://github.com/Microsoft/cpprestsdk), obsługujemy z założenia operacji asynchronicznych za pomocą [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="b684b-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="b684b-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b684b-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="b684b-118">Operacje synchroniczne zawijać odpowiednich operacji asynchronicznych:</span><span class="sxs-lookup"><span data-stu-id="b684b-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="b684b-119">Jeśli pracujesz z wielu wątków aplikacji lub usług, zalecane jest użycie async interfejsów API bezpośrednio, zamiast tworzyć wątku do wywołania synchronizacji interfejsów API, które znacząco wpływa na wydajność.</span><span class="sxs-lookup"><span data-stu-id="b684b-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="b684b-120">Lista wybranych</span><span class="sxs-lookup"><span data-stu-id="b684b-120">Segmented listing</span></span>
<span data-ttu-id="b684b-121">Skala magazynu w chmurze wymaga listy segmentu.</span><span class="sxs-lookup"><span data-stu-id="b684b-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="b684b-122">Na przykład można mieć w milion BLOB w kontenerze obiektów blob platformy Azure lub za pośrednictwem miliarda podmiotów w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b684b-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="b684b-123">Nie są teoretycznego cyfr, ale odbiorcy rzeczywistych przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="b684b-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="b684b-124">W związku z tym jest niemożliwe do wyświetlenia wszystkich obiektów w jednej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b684b-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="b684b-125">Zamiast tego można wyświetlić listę obiektów za pomocą stronicowania.</span><span class="sxs-lookup"><span data-stu-id="b684b-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="b684b-126">Z listy interfejsów API *segmentowanych* przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="b684b-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="b684b-127">Odpowiedź dla operacji segmentowanych lista zawiera:</span><span class="sxs-lookup"><span data-stu-id="b684b-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="b684b-128"><i>_segment</i>, który zawiera zbiór wyników zwróconych jednego wywołania interfejsu API listy.</span><span class="sxs-lookup"><span data-stu-id="b684b-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="b684b-129">*continuation_token*, który jest przekazywany do następnego wywołania w celu pobrania następnej strony wyników.</span><span class="sxs-lookup"><span data-stu-id="b684b-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="b684b-130">Jeśli nie ma żadnych innych wyników do zwrócenia, token kontynuacji jest pusty.</span><span class="sxs-lookup"><span data-stu-id="b684b-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="b684b-131">Na przykład typowe wywołania, aby wyświetlić listę wszystkich obiektów blob w kontenerze może wyglądać jak poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="b684b-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="b684b-132">Kod jest dostępny w naszym [przykłady](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="b684b-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="b684b-133">Należy pamiętać, że liczba wyników zwróconych w stronę można kontrolować przez parametr *max_results* w przeciążenia każdego interfejsu API, na przykład:</span><span class="sxs-lookup"><span data-stu-id="b684b-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="b684b-134">Jeśli nie określisz *max_results* parametr, domyślna wartość maksymalna maksymalnie 5000 wyników jest zwracany w jednej strony.</span><span class="sxs-lookup"><span data-stu-id="b684b-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="b684b-135">Należy również zauważyć, że zapytanie magazynu tabel Azure może zwracać żadnych rekordów i rekordów mniej niż wartość *max_results* parametr, który jest określony, nawet jeśli nie jest pusty token kontynuacji.</span><span class="sxs-lookup"><span data-stu-id="b684b-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="b684b-136">Powodem może być zapytania nie można ukończyć w ciągu pięciu sekund.</span><span class="sxs-lookup"><span data-stu-id="b684b-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="b684b-137">Tak długo, jak token kontynuacji nie jest pusta, zapytanie powinno być kontynuowane i kodu nie należy zakładać, rozmiar segmentu wyników.</span><span class="sxs-lookup"><span data-stu-id="b684b-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="b684b-138">Wzorcu kodowania zalecane dla większości scenariuszy składa się z wyświetlania, co umożliwia jawne postępu listy lub wyszukiwanie i jak usługa odpowiada na każde żądanie.</span><span class="sxs-lookup"><span data-stu-id="b684b-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="b684b-139">Szczególnie w przypadku aplikacji C++ lub usług niższego poziomu formantu postępu listy może pomóc sterowania pamięcią i wydajnością.</span><span class="sxs-lookup"><span data-stu-id="b684b-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="b684b-140">Zachłanne listy</span><span class="sxs-lookup"><span data-stu-id="b684b-140">Greedy listing</span></span>
<span data-ttu-id="b684b-141">Wcześniejszych wersji biblioteki klienta usługi Storage dla języka C++ (Preview wersji 0.5.0 i starszych) uwzględnione niepodzielony listę interfejsów API dla tabel i kolejek, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b684b-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="b684b-142">Te metody zostały zaimplementowane jako otoki segmentowanych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="b684b-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="b684b-143">Dla każdej odpowiedzi listę segmentu kod dołączany wyniki do wektora i zwrócone wszystkie wyniki Po przeskanowaniu były pełne kontenerów.</span><span class="sxs-lookup"><span data-stu-id="b684b-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="b684b-144">Takie podejście może działać konta magazynu lub tabela zawiera niewielką liczbę obiektów.</span><span class="sxs-lookup"><span data-stu-id="b684b-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="b684b-145">Jednak wraz ze wzrostem liczby obiektów pamięci wymaganej można zwiększyć bez ograniczeń, ponieważ wszystkie wyniki pozostaje w pamięci.</span><span class="sxs-lookup"><span data-stu-id="b684b-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="b684b-146">Jedną operację wyświetlania listy może zająć bardzo dużo czasu, w którym obiekt wywołujący nie zawierała informacji dotyczących o postępie.</span><span class="sxs-lookup"><span data-stu-id="b684b-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="b684b-147">Te listy intensywnie interfejsów API zestawu SDK nie istnieją w C#, Java lub środowiska JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="b684b-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="b684b-148">Aby uniknąć potencjalnych problemów z przy użyciu tych intensywnie interfejsów API, firma Microsoft usunęła je w wersji 0.6.0 podglądu.</span><span class="sxs-lookup"><span data-stu-id="b684b-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="b684b-149">Jeśli kod jest wywołanie te intensywnie interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="b684b-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="b684b-150">Następnie należy zmodyfikować kod, aby używał segmentowanych listę interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="b684b-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="b684b-151">Określając *max_results* parametru segmentu, można równoważyć między liczby żądań i użycie pamięci, aby spełnić zagadnienia dotyczące wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b684b-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="b684b-152">Ponadto, jeśli używasz segmentowanych listy interfejsów API, ale przechowywania danych w kolekcji lokalnej w stylu "zachłannego", również stanowczo zaleca się czy Refaktoryzuj swój kod obsługi, przechowywania danych w kolekcji lokalnej dokładnie na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="b684b-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="b684b-153">Lista opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="b684b-153">Lazy listing</span></span>
<span data-ttu-id="b684b-154">Chociaż intensywnie listę wywoływane potencjalne problemy, jest wygodne Jeśli nie ma zbyt wiele obiektów w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="b684b-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="b684b-155">Jeśli używasz również języka C# lub Oracle Java SDK, należy zapoznać się z wyliczenia modelu programowania oferuje opóźnieniem styl — wyświetlanie, gdzie dane z przesunięciem niektórych jest pobierana tylko jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="b684b-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="b684b-156">W języku C++ szablonu na podstawie iteratora także podejście podobne.</span><span class="sxs-lookup"><span data-stu-id="b684b-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="b684b-157">Typowy interfejsu API, listę opóźnieniem przy użyciu **list_blobs** na przykład wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="b684b-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="b684b-158">Fragment kodu typowe, który korzysta ze wzorca opóźnieniem listy może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b684b-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="b684b-159">Należy pamiętać, że lista opóźnieniem jest dostępna tylko w trybie synchronicznym.</span><span class="sxs-lookup"><span data-stu-id="b684b-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="b684b-160">W porównaniu z listą intensywnie opóźnieniem listę pobiera dane tylko wtedy, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b684b-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="b684b-161">W obszarze obejmuje on pobiera dane z usługi Azure Storage tylko wtedy, gdy następnym iteratora przenosi do następnego segmentu.</span><span class="sxs-lookup"><span data-stu-id="b684b-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="b684b-162">W związku z tym pamięć jest określana za pomocą ograniczonego rozmiar, a operacja jest szybkie.</span><span class="sxs-lookup"><span data-stu-id="b684b-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="b684b-163">Lista opóźnieniem interfejsy API są objęte biblioteki klienta usługi Storage dla języka C++ w wersji 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="b684b-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b684b-164">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b684b-164">Conclusion</span></span>
<span data-ttu-id="b684b-165">W tym artykule omówiono różne przeciążenia do wyświetlania listy interfejsów API dla różnych obiektów w bibliotece klienta usługi Storage dla języka C++.</span><span class="sxs-lookup"><span data-stu-id="b684b-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="b684b-166">Podsumowując:</span><span class="sxs-lookup"><span data-stu-id="b684b-166">To summarize:</span></span>

* <span data-ttu-id="b684b-167">Interfejsy API Async zdecydowanie zalecane jest używanie w wielu scenariuszach wątków.</span><span class="sxs-lookup"><span data-stu-id="b684b-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="b684b-168">Lista segmentu jest zalecane dla większości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="b684b-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="b684b-169">Listę opóźnieniem znajduje się w bibliotece jako otoka wygodny w scenariuszach synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="b684b-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="b684b-170">Zachłanne lista nie jest zalecane i została usunięta z biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b684b-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b684b-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b684b-171">Next steps</span></span>
<span data-ttu-id="b684b-172">Aby uzyskać więcej informacji o bibliotece klienta i usługi Azure Storage dla języka C++ zobacz następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="b684b-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="b684b-173">Jak używać magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="b684b-173">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="b684b-174">Jak używać magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="b684b-174">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="b684b-175">Jak używać magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="b684b-175">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b684b-176">Biblioteki klienta usługi Azure Storage dokumentacji interfejsu API języka C++.</span><span class="sxs-lookup"><span data-stu-id="b684b-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="b684b-177">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b684b-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="b684b-178">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b684b-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

