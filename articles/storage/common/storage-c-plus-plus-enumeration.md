---
title: "zasoby usługi Azure Storage aaaList z hello biblioteki klienta usługi Storage dla języka C++ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse listę interfejsów API w biblioteki klienta usługi Microsoft Azure Storage dla języka C++ tooenumerate kontenerów, obiektów blob, kolejek, tabel i jednostek."
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
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="fea04-103">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="fea04-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="fea04-104">Operacje listy są scenariusze programowania toomany klucza z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fea04-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="fea04-105">W tym artykule opisano, jak toomost wydajnie wyliczanie obiektów w usłudze Azure Storage za pomocą hello listę interfejsów API dostarczonych w hello biblioteki klienta usługi Microsoft Azure Storage dla języka C++.</span><span class="sxs-lookup"><span data-stu-id="fea04-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="fea04-106">Ten przewodnik jest przeznaczony dla hello biblioteki klienta magazynu Azure dla języka C++ w wersji 2.x, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="fea04-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="fea04-107">Hello biblioteki klienta magazynu zapewnia różne metody toolist lub obiekty zapytania w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fea04-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="fea04-108">W tym artykule opisano hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="fea04-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="fea04-109">Kontenery listy konta</span><span class="sxs-lookup"><span data-stu-id="fea04-109">List containers in an account</span></span>
* <span data-ttu-id="fea04-110">Listy BLOB w kontenerze lub katalogu wirtualnego obiektów blob</span><span class="sxs-lookup"><span data-stu-id="fea04-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="fea04-111">Lista kolejek w ramach konta</span><span class="sxs-lookup"><span data-stu-id="fea04-111">List queues in an account</span></span>
* <span data-ttu-id="fea04-112">Listy tabel na koncie</span><span class="sxs-lookup"><span data-stu-id="fea04-112">List tables in an account</span></span>
* <span data-ttu-id="fea04-113">Jednostki zapytania w tabeli</span><span class="sxs-lookup"><span data-stu-id="fea04-113">Query entities in a table</span></span>

<span data-ttu-id="fea04-114">Każda z tych metod jest wyświetlany za pomocą innego przeciążenia dla różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="fea04-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="fea04-115">Asynchroniczne i synchroniczne</span><span class="sxs-lookup"><span data-stu-id="fea04-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="fea04-116">Ponieważ hello biblioteki klienta usługi Storage dla języka C++ jest oparty na powitania [biblioteki C++ REST](https://github.com/Microsoft/cpprestsdk), obsługujemy z założenia operacji asynchronicznych za pomocą [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="fea04-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="fea04-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fea04-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="fea04-118">Operacje synchroniczne zawijać hello odpowiednich operacji asynchronicznych:</span><span class="sxs-lookup"><span data-stu-id="fea04-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="fea04-119">Jeśli pracujesz z wielu wątków aplikacji lub usługi, zalecane jest użycie asynchronicznego hello interfejsów API bezpośrednio, zamiast tworzyć wątku synchronizacji hello toocall interfejsów API, które znacząco wpływa na wydajność.</span><span class="sxs-lookup"><span data-stu-id="fea04-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="fea04-120">Lista wybranych</span><span class="sxs-lookup"><span data-stu-id="fea04-120">Segmented listing</span></span>
<span data-ttu-id="fea04-121">skalę Hello magazynu w chmurze wymaga listy segmentu.</span><span class="sxs-lookup"><span data-stu-id="fea04-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="fea04-122">Na przykład można mieć w milion BLOB w kontenerze obiektów blob platformy Azure lub za pośrednictwem miliarda podmiotów w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fea04-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="fea04-123">Nie są teoretycznego cyfr, ale odbiorcy rzeczywistych przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="fea04-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="fea04-124">Dlatego jest niepraktyczne toolist wszystkie obiekty w pojedynczą odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="fea04-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="fea04-125">Zamiast tego można wyświetlić listę obiektów za pomocą stronicowania.</span><span class="sxs-lookup"><span data-stu-id="fea04-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="fea04-126">Każdy hello listę interfejsów API ma *segmentowanych* przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="fea04-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="fea04-127">Witaj odpowiedzi dla operacji segmentowanych listę obejmuje:</span><span class="sxs-lookup"><span data-stu-id="fea04-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="fea04-128"><i>_segment</i>, zawierającą hello zestaw wyników zwrócony dla toohello jednego wywołania interfejsu API wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="fea04-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="fea04-129">*continuation_token*, który jest przekazywany toohello następne wywołanie w kolejności tooget hello następnej strony wyników.</span><span class="sxs-lookup"><span data-stu-id="fea04-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="fea04-130">Jeśli nie ma żadnych więcej tooreturn wyników, token kontynuacji hello ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="fea04-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="fea04-131">Na przykład toolist Typowe wywołania wszystkie obiekty BLOB w kontenerze może wyglądać jak hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="fea04-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="fea04-132">Kod Hello jest dostępny w naszym [przykłady](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="fea04-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="fea04-133">Należy pamiętać, że hello liczbę wyników zwracanych na stronie można kontrolować przez parametr hello *max_results* w hello przeciążenia każdego interfejsu API, na przykład:</span><span class="sxs-lookup"><span data-stu-id="fea04-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="fea04-134">Jeśli nie określisz hello *max_results* parametru, domyślne hello maksymalną wartość zapasową too5000 wyników jest zwracany w jednej strony.</span><span class="sxs-lookup"><span data-stu-id="fea04-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="fea04-135">Należy również zauważyć, że zapytanie magazynu tabel Azure może zwracać żadnych rekordów lub mniej rekordów niż wartość hello hello *max_results* parametr, który jest określony, nawet jeśli token kontynuacji hello nie jest pusty.</span><span class="sxs-lookup"><span data-stu-id="fea04-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="fea04-136">Powodem może być się, że nie można ukończyć tej kwerendy hello w ciągu pięciu sekund.</span><span class="sxs-lookup"><span data-stu-id="fea04-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="fea04-137">Tak długo, jak token kontynuacji hello nie jest pusta, powinno być kontynuowane hello zapytania i kodu nie należy zakładać hello rozmiar segmentu wyników.</span><span class="sxs-lookup"><span data-stu-id="fea04-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="fea04-138">Witaj zalecane kodowania wzorca dla większości scenariuszy składa się z wyświetlania, zapewniające jawne postęp wyświetlania lub zapytań i jak usługa hello odpowiada tooeach żądania.</span><span class="sxs-lookup"><span data-stu-id="fea04-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="fea04-139">Szczególnie w przypadku aplikacji C++ lub usług niższego poziomu kontroli hello Wyświetlanie postępu mogą pomóc sterowania pamięcią i wydajnością.</span><span class="sxs-lookup"><span data-stu-id="fea04-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="fea04-140">Zachłanne listy</span><span class="sxs-lookup"><span data-stu-id="fea04-140">Greedy listing</span></span>
<span data-ttu-id="fea04-141">Wcześniejszych wersji hello biblioteki klienta usługi Storage dla języka C++ (Preview wersji 0.5.0 i starszych) uwzględnione niepodzielony listę interfejsów API dla tabel i kolejek, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fea04-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="fea04-142">Te metody zostały zaimplementowane jako otoki segmentowanych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fea04-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="fea04-143">Dla każdej odpowiedzi listę segmentu kod hello dołączany hello wyniki tooa wektora i zwrócone wszystkie wyniki Po przeskanowaniu były pełne kontenery hello.</span><span class="sxs-lookup"><span data-stu-id="fea04-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="fea04-144">Takie podejście może działać hello konta magazynu lub tabela zawiera niewielką liczbę obiektów.</span><span class="sxs-lookup"><span data-stu-id="fea04-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="fea04-145">Jednak wraz ze wzrostem hello liczba obiektów hello pamięci wymaganej można zwiększyć bez ograniczeń, ponieważ wszystkie wyniki pozostaje w pamięci.</span><span class="sxs-lookup"><span data-stu-id="fea04-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="fea04-146">Jedną operację wyświetlania listy może zająć bardzo dużo czasu, podczas których hello obiekt wywołujący nie zawierała informacji dotyczących o postępie.</span><span class="sxs-lookup"><span data-stu-id="fea04-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="fea04-147">Te intensywnie listę interfejsów API w hello zestawu SDK nie istnieje w języku C#, Java, lub hello środowiska JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="fea04-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="fea04-148">tooavoid hello potencjalne problemy związane z używaniem tych intensywnie interfejsów API, firma Microsoft usunęła je w wersji 0.6.0 podglądu.</span><span class="sxs-lookup"><span data-stu-id="fea04-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="fea04-149">Jeśli kod jest wywołanie te intensywnie interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="fea04-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="fea04-150">Następnie należy zmodyfikować kod toouse hello segmentem listę interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="fea04-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

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

<span data-ttu-id="fea04-151">Określając hello *max_results* parametru hello segmentu, można równoważyć między hello liczby żądań i zagadnienia dotyczące wydajności toomeet użycia pamięci dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fea04-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="fea04-152">Ponadto, jeśli jest przy użyciu wybranych listy interfejsów API, ale hello dane przechowywane w kolekcji lokalnej w stylu "zachłannego", również stanowczo zaleca się czy Refaktoryzuj toohandle Twojego kodu, przechowywanie danych w kolekcji lokalnej dokładnie na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="fea04-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="fea04-153">Lista opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="fea04-153">Lazy listing</span></span>
<span data-ttu-id="fea04-154">Chociaż intensywnie listę wywoływane potencjalne problemy, jest wygodne Jeśli nie ma zbyt wiele obiektów w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="fea04-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="fea04-155">Jeśli używasz również języka C# lub Oracle Java SDK, należy zapoznać się z hello Wyliczalny model programowania, który oferuje opóźnieniem styl — wyświetlanie, gdzie hello z niektórych przesunięciem jest tylko pobierane dane w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="fea04-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="fea04-156">W języku C++ szablonu na podstawie iteratora hello także podejście podobne.</span><span class="sxs-lookup"><span data-stu-id="fea04-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="fea04-157">Typowy interfejsu API, listę opóźnieniem przy użyciu **list_blobs** na przykład wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="fea04-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="fea04-158">Fragment kodu typowe, który korzysta ze wzorca opóźnieniem listę hello może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="fea04-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
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

<span data-ttu-id="fea04-159">Należy pamiętać, że lista opóźnieniem jest dostępna tylko w trybie synchronicznym.</span><span class="sxs-lookup"><span data-stu-id="fea04-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="fea04-160">W porównaniu z listą intensywnie opóźnieniem listę pobiera dane tylko wtedy, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fea04-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="fea04-161">W obszarze obejmuje hello go pobiera dane z usługi Azure Storage tylko wtedy, gdy iteratora dalej hello przenosi do następnego segmentu.</span><span class="sxs-lookup"><span data-stu-id="fea04-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="fea04-162">W związku z tym pamięć jest określana za pomocą ograniczonego rozmiar, a operacja hello jest szybkie.</span><span class="sxs-lookup"><span data-stu-id="fea04-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="fea04-163">Lista opóźnieniem interfejsy API są objęte hello biblioteki klienta usługi Storage dla języka C++ w wersji 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="fea04-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="fea04-164">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fea04-164">Conclusion</span></span>
<span data-ttu-id="fea04-165">W tym artykule omówiono różne przeciążenia do wyświetlania listy interfejsów API dla różnych obiektów w hello biblioteki klienta usługi Storage dla języka C++.</span><span class="sxs-lookup"><span data-stu-id="fea04-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="fea04-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="fea04-166">toosummarize:</span></span>

* <span data-ttu-id="fea04-167">Interfejsy API Async zdecydowanie zalecane jest używanie w wielu scenariuszach wątków.</span><span class="sxs-lookup"><span data-stu-id="fea04-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="fea04-168">Lista segmentu jest zalecane dla większości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="fea04-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="fea04-169">Opóźnieniem listy znajduje się w bibliotece hello jako otoka wygodny w scenariusze synchroniczne z.</span><span class="sxs-lookup"><span data-stu-id="fea04-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="fea04-170">Zachłanne lista nie jest zalecane i została usunięta z biblioteki hello.</span><span class="sxs-lookup"><span data-stu-id="fea04-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fea04-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fea04-171">Next steps</span></span>
<span data-ttu-id="fea04-172">Aby uzyskać więcej informacji o bibliotece klienta i usługi Azure Storage dla języka C++ zobacz następujące zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="fea04-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="fea04-173">Jak toouse magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="fea04-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="fea04-174">Jak toouse magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="fea04-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="fea04-175">Jak toouse magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="fea04-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="fea04-176">Biblioteki klienta usługi Azure Storage dokumentacji interfejsu API języka C++.</span><span class="sxs-lookup"><span data-stu-id="fea04-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="fea04-177">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fea04-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="fea04-178">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fea04-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

