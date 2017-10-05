---
title: "Projektowanie zapytania wydajne listy — partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Zwiększyć wydajność przez filtrowanie zapytania, gdy żąda informacji na temat zasobów usługi partia zadań, takich jak pule, zadań, zadań i węzły obliczeniowe."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="d1078-103">Wydajnie tworzyć zapytania do listy zasobów usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="d1078-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="d1078-104">Tutaj dowiesz się, jak zwiększyć wydajność aplikacji partii zadań Azure dzięki zmniejszeniu ilości danych zwracanych przez usługę kwerend zadania, zadania i obliczeniowe węzłów o [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d1078-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="d1078-105">Prawie wszystkie aplikacje partii muszą wykonywać niektórych monitorowania lub innych operacji, który odpytuje usługa partia zadań, często w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="d1078-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="d1078-106">Na przykład aby ustalić, czy istnieją wszystkie zadania w kolejce pozostały w ramach zadania, należy uzyskać danych dla każdego zadania w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="d1078-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="d1078-107">Aby określić stan węzłów w puli, należy uzyskać dane na każdym węźle w puli.</span><span class="sxs-lookup"><span data-stu-id="d1078-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="d1078-108">W tym artykule opisano sposób wykonywania takich kwerend w najbardziej wydajny sposób.</span><span class="sxs-lookup"><span data-stu-id="d1078-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="d1078-109">Usługa partia zadań zapewnia obsługę interfejsu API specjalne typowy scenariusz inwentaryzacji zadań w ramach zadania.</span><span class="sxs-lookup"><span data-stu-id="d1078-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="d1078-110">Zamiast korzystać z zapytania listy tych, można wywołać [pobrać liczby zadań] [ rest_get_task_counts] operacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="d1078-111">Liczby zadań Get wskazuje, ile zadań oczekujących, uruchomiona lub Zakończ i ile zadań ma powodzeniem lub niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d1078-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="d1078-112">Liczba zadań Get jest bardziej efektywne niż zapytanie listy.</span><span class="sxs-lookup"><span data-stu-id="d1078-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="d1078-113">Aby uzyskać więcej informacji, zobacz [liczba zadań dla zadania według stanu (wersja zapoznawcza)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="d1078-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="d1078-114">Operacji Get liczby zadań nie jest starszy niż 2017-06-01.5.1 dostępne w wersjach usługi partii.</span><span class="sxs-lookup"><span data-stu-id="d1078-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="d1078-115">Jeśli używasz starszej wersji usługi użyć kwerendy listy, aby zamiast tego liczba zadań w ramach zadania.</span><span class="sxs-lookup"><span data-stu-id="d1078-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="d1078-116">Atrybut DetailLevel spełnia</span><span class="sxs-lookup"><span data-stu-id="d1078-116">Meet the DetailLevel</span></span>
<span data-ttu-id="d1078-117">W środowisku produkcyjnym aplikacji partii jednostek, takich jak zadania, zadania i węzły obliczeniowe można numerów w tysięcy.</span><span class="sxs-lookup"><span data-stu-id="d1078-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="d1078-118">Gdy użytkownik żąda informacji na temat tych zasobów, potencjalnie dużą ilość danych musi "przechodzą przewodowo" z usługi partia zadań do aplikacji w każdym zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="d1078-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="d1078-119">Poprzez ograniczenie liczby elementów i typu danych zwracane przez zapytanie, może zwiększyć szybkość zapytań i w związku z tym wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="d1078-120">To [partiami platformy .NET] [ api_net] list fragment kodu interfejsu API *co* zadanie, które jest skojarzone z zadaniem, wraz z *wszystkie* właściwości każdego zadania:</span><span class="sxs-lookup"><span data-stu-id="d1078-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="d1078-121">Jednak bardziej efektywnego zapytanie listy, można wykonać przez zastosowanie "poziom szczegółowości" do zapytania.</span><span class="sxs-lookup"><span data-stu-id="d1078-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="d1078-122">Aby to zrobić, podając [ODATADetailLevel] [ odata] do obiektu [JobOperations.ListTasks] [ net_list_tasks] metody.</span><span class="sxs-lookup"><span data-stu-id="d1078-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="d1078-123">Ta Wstawka kodu zwraca tylko identyfikator, wiersz polecenia i właściwości informacji węzła obliczeń zakończonych zadań:</span><span class="sxs-lookup"><span data-stu-id="d1078-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="d1078-124">W tym przykładowym scenariuszu, jeśli istnieją tysiące zadania, wyniki z drugiego zapytania zwykle powróci znacznie szybciej niż pierwszy.</span><span class="sxs-lookup"><span data-stu-id="d1078-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="d1078-125">Więcej informacji o używaniu ODATADetailLevel wśród elementów przy użyciu interfejsu API platformy .NET partii jest dołączony [poniżej](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="d1078-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1078-126">Zdecydowanie zalecamy, aby użytkownik *zawsze* podać ODATADetailLevel obiekt do listy połączeń interfejs API .NET w celu zapewnienia maksymalnej wydajności i wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="d1078-127">Umożliwia określenie poziomu szczegółowości, może pomóc zmniejszyć czasy odpowiedzi usługi partii, poprawić wykorzystanie sieci i zminimalizować użycie pamięci przez aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="d1078-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="d1078-128">Filtruj, wybierz i rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="d1078-128">Filter, select, and expand</span></span>
<span data-ttu-id="d1078-129">[Partiami platformy .NET] [ api_net] i [REST partii] [ api_rest] interfejsów API umożliwiają Zmniejsz liczbę elementów, które są zwracane w postaci listy, a także ilość informacji, która jest zwracana dla każdego.</span><span class="sxs-lookup"><span data-stu-id="d1078-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="d1078-130">Możesz to zrobić, określając **filtru**, **wybierz**, i **rozwiń ciągów** podczas wykonywania zapytania z listy.</span><span class="sxs-lookup"><span data-stu-id="d1078-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="d1078-131">Filtr</span><span class="sxs-lookup"><span data-stu-id="d1078-131">Filter</span></span>
<span data-ttu-id="d1078-132">Ciąg filtru jest wyrażenie, które zmniejsza liczbę elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="d1078-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="d1078-133">Na przykład listy zadania uruchomione zadania lub listy tylko węzły obliczeniowe, które są gotowe do uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="d1078-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="d1078-134">Ciąg filtru składa się z co najmniej jednego wyrażenia z wyrażeniem, które składa się z nazwy właściwości, operator i wartość.</span><span class="sxs-lookup"><span data-stu-id="d1078-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="d1078-135">Właściwości, które można określić są specyficzne dla poszczególnych typów jednostek, które można zbadać, jak operatory, które są obsługiwane dla każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d1078-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="d1078-136">Wiele wyrażeń można łączyć przy użyciu operatorów logicznych `and` i `or`.</span><span class="sxs-lookup"><span data-stu-id="d1078-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="d1078-137">W tym przykładzie filtrowanie list ciągów tylko zadania uruchamiania "renderowania": `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="d1078-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="d1078-138">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="d1078-138">Select</span></span>
<span data-ttu-id="d1078-139">Wybierz parametry ogranicza wartości właściwości, które są zwracane dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="d1078-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="d1078-140">Określ listę nazw właściwości, a dla elementów w wynikach zapytania są zwracane tylko wartości tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="d1078-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="d1078-141">Wybierz parametry składa się z listy rozdzielanej przecinkami nazw właściwości.</span><span class="sxs-lookup"><span data-stu-id="d1078-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="d1078-142">Można określić właściwości dla typu obiektu, który jest kwerenda.</span><span class="sxs-lookup"><span data-stu-id="d1078-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="d1078-143">Ten ciąg wybierz przykład określa, że powinny być zwracane tylko trzy wartości właściwości dla każdego zadania: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="d1078-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="d1078-144">Rozwiń</span><span class="sxs-lookup"><span data-stu-id="d1078-144">Expand</span></span>
<span data-ttu-id="d1078-145">Ciąg rozszerzenia zmniejsza liczbę wywołań interfejsu API, które są wymagane do uzyskania określonych informacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="d1078-146">Korzystając z ciągu Rozwiń, można uzyskać więcej informacji o każdym elemencie przy użyciu jednego wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d1078-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="d1078-147">Zamiast pierwszego uzyskiwania listy jednostek, następnie żąda informacji dla każdego elementu na liście ciągu rozwiń służy do uzyskania tych samych informacji w jednym wywołaniu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d1078-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="d1078-148">Mniej wywołań interfejsu API oznaczają lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="d1078-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="d1078-149">Podobnie jak wybierz ciąg, ciąg rozwiń Określa, czy niektóre dane są uwzględniane w wynikach zapytania listy.</span><span class="sxs-lookup"><span data-stu-id="d1078-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="d1078-150">Ciąg rozwiń jest obsługiwana tylko w przypadku, gdy jest używany w listę zadań, harmonogramy zadań, zadań i pul.</span><span class="sxs-lookup"><span data-stu-id="d1078-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="d1078-151">Obecnie obsługuje on tylko informacje statystyczne.</span><span class="sxs-lookup"><span data-stu-id="d1078-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="d1078-152">Gdy wszystkie właściwości są wymagane i nie wybierz podano ciągu, ciąg rozwiń *musi* można użyć, aby uzyskać informacje statystyczne.</span><span class="sxs-lookup"><span data-stu-id="d1078-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="d1078-153">Jeśli wybierz ciąg jest używany do uzyskania podzbiór właściwości, następnie `stats` można określić w ciągu wybierz i rozwiń ciągu nie muszą być określone.</span><span class="sxs-lookup"><span data-stu-id="d1078-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="d1078-154">W tym przykładzie rozwiń ciąg Określa, że dla każdego elementu na liście powinny być zwracane informacje statystyczne: `stats`.</span><span class="sxs-lookup"><span data-stu-id="d1078-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="d1078-155">Podczas konstruowania dowolnego typu ciąg zapytania trzy (filtrowanie, wybierz i rozwiń), należy upewnić się, że nazwy właściwości i litery zgodną ich odpowiedniki element interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="d1078-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="d1078-156">Na przykład podczas pracy z platformą .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasy, należy określić **stanu** zamiast **stanu**, nawet jeśli jest właściwości platformy .NET [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="d1078-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="d1078-157">Zobacz w poniższych tabelach mapowania właściwości między .NET i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="d1078-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="d1078-158">Reguły filtra wybierz i rozwiń ciągów</span><span class="sxs-lookup"><span data-stu-id="d1078-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="d1078-159">Nazwy właściwości w filtrze, wybierz i rozwiń ciągi powinny być wyświetlane, tak jak w [REST partii] [ api_rest] interfejsu API — nawet wtedy, gdy używasz [partiami platformy .NET] [ api_net] lub jednego z innych zestawów SDK usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d1078-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="d1078-160">Wszystkie nazwy właściwości jest rozróżniana wielkość liter, ale wartości właściwości są bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d1078-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="d1078-161">Data i godzina ciągów może być jednym z dwóch formatów i musi być poprzedzony `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="d1078-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="d1078-162">Przykładowy format W3C DTF:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="d1078-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="d1078-163">RFC 1123 Przykładowy format:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="d1078-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="d1078-164">Logiczna ciągi są albo `true` lub `false`.</span><span class="sxs-lookup"><span data-stu-id="d1078-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="d1078-165">Jeśli określono nieprawidłowe właściwości lub operatora `400 (Bad Request)` spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="d1078-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="d1078-166">Efektywne wykonywania zapytania w partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d1078-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="d1078-167">W ramach [partiami platformy .NET] [ api_net] interfejsu API, [ODATADetailLevel] [ odata] klasa jest używana do podawania filtru, wybierz i rozwiń ciągi do listy operacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="d1078-168">Klasa ODataDetailLevel ma trzy właściwości publicznych ciągów, które może być określony w konstruktorze lub ustawić bezpośrednio dla obiektu.</span><span class="sxs-lookup"><span data-stu-id="d1078-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="d1078-169">Można następnie przekazać obiekt ODataDetailLevel jako parametr do różnych operacji listy takich jak [ListPools][net_list_pools], [ListJobs][net_list_jobs], i [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="d1078-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="d1078-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: Ogranicz liczbę elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="d1078-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="d1078-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: Określ wartości właściwości, które są zwracane z każdym elementem.</span><span class="sxs-lookup"><span data-stu-id="d1078-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="d1078-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: pobieranie danych dla wszystkich elementów w jeden interfejs API Wywołaj zamiast wywołań dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="d1078-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="d1078-173">Poniższy fragment kodu używa interfejsu API programu .NET partii w celu wydajnego wykonywania zapytań usługi partia zadań dla statystyk określony zbiór pule.</span><span class="sxs-lookup"><span data-stu-id="d1078-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="d1078-174">W tym scenariuszu użytkownik partii ma pule zarówno testowego i produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d1078-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="d1078-175">Test puli identyfikatorów nazwy są poprzedzone ciągiem "test", a puli produkcji identyfikatory nazwy są poprzedzone ciągiem "produkcyjną".</span><span class="sxs-lookup"><span data-stu-id="d1078-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="d1078-176">We fragmencie *myBatchClient* jest prawidłowo zainicjowany wystąpieniem [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasy.</span><span class="sxs-lookup"><span data-stu-id="d1078-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="d1078-177">Wystąpienie [ODATADetailLevel] [ odata] skonfigurowanego wybierz i klauzule rozwiń mogą również zostać przekazane do odpowiedniej metody Get, takich jak [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), aby ograniczyć ilość danych, która jest zwracana.</span><span class="sxs-lookup"><span data-stu-id="d1078-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="d1078-178">Wsadowe REST do mapowania interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="d1078-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="d1078-179">Nazwy właściwości w filtrze, wybierz i rozwiń ciągów *musi* ich odpowiedniki interfejsu API REST, zarówno w nazwie i w przypadku uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="d1078-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="d1078-180">W poniższych tabelach zawierają mapowania między partnerami .NET i interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="d1078-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="d1078-181">Mapowania dla filtru ciągów</span><span class="sxs-lookup"><span data-stu-id="d1078-181">Mappings for filter strings</span></span>
* <span data-ttu-id="d1078-182">**Metody listy .NET**: każdej z metod interfejsu API platformy .NET w tej kolumnie akceptuje [ODATADetailLevel] [ odata] obiektu jako parametr.</span><span class="sxs-lookup"><span data-stu-id="d1078-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="d1078-183">**Żądania listy REST**: strona każdego interfejsu API REST powiązany z tej kolumny zawiera tabelę, która określa właściwości i operacje, które są dozwolone w *filtru* ciągów.</span><span class="sxs-lookup"><span data-stu-id="d1078-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="d1078-184">Użyjesz tych nazw właściwości i operacji utworzenia [ODATADetailLevel.FilterClause] [ odata_filter] ciąg.</span><span class="sxs-lookup"><span data-stu-id="d1078-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="d1078-185">Metody listy .NET</span><span class="sxs-lookup"><span data-stu-id="d1078-185">.NET list methods</span></span> | <span data-ttu-id="d1078-186">Żądania listy REST</span><span class="sxs-lookup"><span data-stu-id="d1078-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="d1078-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="d1078-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="d1078-188">[Lista certyfikatów dla konta][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="d1078-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="d1078-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="d1078-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="d1078-190">[Lista plików skojarzonych z zadania][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="d1078-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="d1078-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="d1078-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="d1078-192">[Lista stanu przygotowanie zadania i wersji zadania dla zadania][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="d1078-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="d1078-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="d1078-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="d1078-194">[Wyświetlić zadania konta][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="d1078-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="d1078-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="d1078-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="d1078-196">[Lista plików w węźle][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="d1078-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="d1078-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="d1078-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="d1078-198">[Lista zadań skojarzonych z zadaniem][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="d1078-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="d1078-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="d1078-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="d1078-200">[Lista harmonogramów zadań w ramach konta][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="d1078-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="d1078-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="d1078-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="d1078-202">[Listę zadań skojarzonych z harmonogramu zadań][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="d1078-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="d1078-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="d1078-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="d1078-204">[Listy węzłów obliczeniowych w puli][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="d1078-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="d1078-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="d1078-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="d1078-206">[Wyświetl listę pul konta][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="d1078-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="d1078-207">Mapowania dla wybierz ciągów</span><span class="sxs-lookup"><span data-stu-id="d1078-207">Mappings for select strings</span></span>
* <span data-ttu-id="d1078-208">**Typy .NET partii**: typy interfejsu API partii .NET.</span><span class="sxs-lookup"><span data-stu-id="d1078-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="d1078-209">**Interfejs API REST jednostek**: każdej strony w tej kolumnie zawiera co najmniej jednej tabeli, które listę nazw właściwości interfejsu API REST dla typu.</span><span class="sxs-lookup"><span data-stu-id="d1078-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="d1078-210">Te nazwy właściwości są używane podczas utworzymy *wybierz* ciągów.</span><span class="sxs-lookup"><span data-stu-id="d1078-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="d1078-211">Utworzenia użyje tych samych nazw właściwości [ODATADetailLevel.SelectClause] [ odata_select] ciąg.</span><span class="sxs-lookup"><span data-stu-id="d1078-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="d1078-212">Typy .NET partii</span><span class="sxs-lookup"><span data-stu-id="d1078-212">Batch .NET types</span></span> | <span data-ttu-id="d1078-213">Jednostki interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="d1078-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="d1078-214">[Certyfikat][net_cert]</span><span class="sxs-lookup"><span data-stu-id="d1078-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="d1078-215">[Uzyskiwanie informacji o certyfikacie][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="d1078-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="d1078-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="d1078-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="d1078-217">[Pobierz informacje o zadaniu][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="d1078-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="d1078-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="d1078-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="d1078-219">[Pobierz informacje o harmonogram zadań][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="d1078-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="d1078-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="d1078-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="d1078-221">[Pobierz informacje o węźle][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="d1078-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="d1078-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="d1078-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="d1078-223">[Pobierz informacje o puli][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="d1078-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="d1078-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="d1078-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="d1078-225">[Pobierz informacje o zadaniu][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="d1078-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="d1078-226">Przykład: skonstruować ciąg filtru</span><span class="sxs-lookup"><span data-stu-id="d1078-226">Example: construct a filter string</span></span>
<span data-ttu-id="d1078-227">Podczas konstruowania ciąg filtru dla [ODATADetailLevel.FilterClause][odata_filter], zapoznaj się w tabeli powyżej w "Mapowania dla filtru ciągów" stronę dokumentacji Znajdź interfejsu API REST, umożliwiająca operacja listy, który chcesz wykonać.</span><span class="sxs-lookup"><span data-stu-id="d1078-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="d1078-228">W pierwszej tabeli multirow na tej stronie znajdziesz filtrowanie właściwości i ich operatory obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d1078-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="d1078-229">Jeśli chcesz pobrać wszystkie zadania, którego kod zakończenia: różną od zera, na przykład ten wiersz na [listy zadania skojarzone z zadaniem] [ rest_list_tasks] Określa dozwolone operatory i odpowiednie właściwości ciągu:</span><span class="sxs-lookup"><span data-stu-id="d1078-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="d1078-230">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d1078-230">Property</span></span> | <span data-ttu-id="d1078-231">Operacje dozwolone</span><span class="sxs-lookup"><span data-stu-id="d1078-231">Operations allowed</span></span> | <span data-ttu-id="d1078-232">Typ</span><span class="sxs-lookup"><span data-stu-id="d1078-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="d1078-233">W związku z tym będzie ciąg filtru, aby uzyskać listę wszystkich zadań z kodem zakończenia różną od zera:</span><span class="sxs-lookup"><span data-stu-id="d1078-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="d1078-234">Przykład: skonstruować wybierz ciąg</span><span class="sxs-lookup"><span data-stu-id="d1078-234">Example: construct a select string</span></span>
<span data-ttu-id="d1078-235">Aby utworzyć [ODATADetailLevel.SelectClause][odata_select], zapoznaj się z powyższej tabeli, w obszarze "Mapowania dla ciągów select" i przejdź do strony interfejsu API REST, który odpowiada typowi obiektu, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="d1078-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="d1078-236">W pierwszej tabeli multirow na tej stronie można znaleźć właściwości selectable i ich operatory obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d1078-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="d1078-237">Jeśli chcesz pobrać tylko identyfikator i wiersz polecenia dla każdego zadania na liście, na przykład można znaleźć te wiersze w tabeli stosowanych w [uzyskać informacje o zadaniu][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="d1078-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="d1078-238">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d1078-238">Property</span></span> | <span data-ttu-id="d1078-239">Typ</span><span class="sxs-lookup"><span data-stu-id="d1078-239">Type</span></span> | <span data-ttu-id="d1078-240">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d1078-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="d1078-241">Następnie będzie wybierz ciąg tylko identyfikator i wiersza polecenia do każdego zadania wymienione w tym:</span><span class="sxs-lookup"><span data-stu-id="d1078-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="d1078-242">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="d1078-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="d1078-243">Przykładowy kod zapytania wydajne listy</span><span class="sxs-lookup"><span data-stu-id="d1078-243">Efficient list queries code sample</span></span>
<span data-ttu-id="d1078-244">Zapoznaj się z [EfficientListQueries] [ efficient_query_sample] przykładowy projekt w witrynie GitHub, aby zobaczyć, jak skuteczne zapytań listy może wpłynąć na wydajność w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="d1078-245">Tę aplikację konsolową C# tworzy i dodaje dużej liczby zadań do zadania.</span><span class="sxs-lookup"><span data-stu-id="d1078-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="d1078-246">Następnie należy go wielu wywołań do [JobOperations.ListTasks] [ net_list_tasks] — metoda i przekazuje [ODATADetailLevel] [ odata] obiektów, które są skonfigurowane przy użyciu wartości różnych właściwości różnią się ilość danych do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="d1078-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="d1078-247">Generuje dane wyjściowe podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="d1078-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="d1078-248">Jak pokazano na czas, można znacznie zmniejszyć czas odpowiedzi na zapytania, ograniczając właściwości oraz liczbę elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="d1078-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="d1078-249">Można znaleźć to i inne przykładowych projektach w [azure partii próbek] [ github_samples] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1078-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="d1078-250">BatchMetrics biblioteki i kod przykładowy</span><span class="sxs-lookup"><span data-stu-id="d1078-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="d1078-251">Oprócz powyższych przykładowy kod EfficientListQueries można znaleźć [BatchMetrics] [ batch_metrics] projektu w [azure partii próbek] [ github_samples] repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1078-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="d1078-252">Przykładowy projekt BatchMetrics pokazano, jak skutecznie monitorować postęp zadania partii zadań Azure za pomocą interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="d1078-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="d1078-253">[BatchMetrics] [ batch_metrics] próbki obejmuje projektu biblioteki klas .NET, które można zastosować do własnych projektów i prosty program wiersza polecenia do wykonywania i przedstawiają sposób używania biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d1078-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="d1078-254">Przykładową aplikację w projekcie przedstawiono następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="d1078-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="d1078-255">Wybieranie określonych atrybutów w celu pobrania właściwości, które są potrzebne</span><span class="sxs-lookup"><span data-stu-id="d1078-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="d1078-256">Filtrowanie na czas przejścia stanu w celu pobrania tylko zmiany od czasu ostatniej kwerendy</span><span class="sxs-lookup"><span data-stu-id="d1078-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="d1078-257">Na przykład następująca metoda pojawia się w bibliotece BatchMetrics.</span><span class="sxs-lookup"><span data-stu-id="d1078-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="d1078-258">Zwraca ODATADetailLevel, która określa, że tylko `id` i `state` właściwości mają być uzyskiwane dla jednostek, które będą pytani.</span><span class="sxs-lookup"><span data-stu-id="d1078-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="d1078-259">On również określa, że tylko jednostki, w których stan zmienił się od określonego `DateTime` parametr ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="d1078-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="d1078-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1078-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="d1078-261">Zadania równoległych węzła</span><span class="sxs-lookup"><span data-stu-id="d1078-261">Parallel node tasks</span></span>
<span data-ttu-id="d1078-262">[Maksymalizowanie użycia zasobów obliczeniowych partii zadań Azure z węzła równoczesnych zadań](batch-parallel-node-tasks.md) inny artykuł dotyczy partii wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="d1078-263">Niektóre rodzaje obciążeń mogą korzystać z wykonywanych zadań równoległych na większych — ale mniej — węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d1078-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="d1078-264">Zapoznaj się z [przykładowy scenariusz](batch-parallel-node-tasks.md#example-scenario) w artykule, aby uzyskać szczegółowe informacje o takiej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="d1078-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="d1078-265">Forum usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="d1078-265">Batch Forum</span></span>
<span data-ttu-id="d1078-266">[Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym miejscem do omówienia partii i zadać pytania dotyczące usługi.</span><span class="sxs-lookup"><span data-stu-id="d1078-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="d1078-267">HEAD na za pośrednictwem przydatne Posty "trwałe" i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="d1078-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job