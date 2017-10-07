---
title: "aaaDesign wydajne listy kwerend - partii zadań Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a><span data-ttu-id="b2932-103">Tworzenie zapytań wydajnie toolist partii zasobów</span><span class="sxs-lookup"><span data-stu-id="b2932-103">Create queries toolist Batch resources efficiently</span></span>

<span data-ttu-id="b2932-104">Tutaj dowiesz się, jak tooincrease aplikacji partii zadań Azure wydajność dzięki zmniejszeniu hello ilość danych zwracanych przez usługę hello kwerendy zadania, zadania i węzły obliczeniowe z hello [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b2932-104">Here you'll learn how tooincrease your Azure Batch application's performance by reducing hello amount of data that is returned by hello service when you query jobs, tasks, and compute nodes with hello [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="b2932-105">Prawie wszystkie aplikacje partii muszą tooperform pewien typ monitorowania lub innych operacji, który odpytuje hello usługa partia zadań, często w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="b2932-105">Nearly all Batch applications need tooperform some type of monitoring or other operation that queries hello Batch service, often at regular intervals.</span></span> <span data-ttu-id="b2932-106">Na przykład toodetermine czy są dostępne w kolejce zadań pozostały w ramach zadania, dla każdego zadania w zadaniu hello musi pobrać dane.</span><span class="sxs-lookup"><span data-stu-id="b2932-106">For example, toodetermine whether there are any queued tasks remaining in a job, you must get data on every task in hello job.</span></span> <span data-ttu-id="b2932-107">Stan hello toodetermine węzłów w puli, w każdym węźle w puli hello musi pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="b2932-107">toodetermine hello status of nodes in your pool, you must get data on every node in hello pool.</span></span> <span data-ttu-id="b2932-108">W tym artykule opisano, jak tooexecute takie zapytania w programie hello najbardziej wydajny sposób.</span><span class="sxs-lookup"><span data-stu-id="b2932-108">This article explains how tooexecute such queries in hello most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="b2932-109">Witaj usługa partia zadań zapewnia obsługę interfejsu API specjalne hello typowy scenariusz inwentaryzacji zadań w ramach zadania.</span><span class="sxs-lookup"><span data-stu-id="b2932-109">hello Batch service provides special API support for hello common scenario of counting tasks in a job.</span></span> <span data-ttu-id="b2932-110">Zamiast korzystać z zapytania listy tych, należy wywołać hello [pobrać liczby zadań] [ rest_get_task_counts] operacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-110">Instead of using a list query for these, you can call hello [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="b2932-111">Liczby zadań Get wskazuje, ile zadań oczekujących, uruchomiona lub Zakończ i ile zadań ma powodzeniem lub niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="b2932-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="b2932-112">Liczba zadań Get jest bardziej efektywne niż zapytanie listy.</span><span class="sxs-lookup"><span data-stu-id="b2932-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="b2932-113">Aby uzyskać więcej informacji, zobacz [liczba zadań dla zadania według stanu (wersja zapoznawcza)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="b2932-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="b2932-114">Hello operacji Get liczby zadań nie jest starszy niż 2017-06-01.5.1 dostępne w wersjach usługi partii.</span><span class="sxs-lookup"><span data-stu-id="b2932-114">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="b2932-115">Jeśli używasz starszej wersji usługi hello, następnie użyć listy zadań toocount zapytania w ramach zadania.</span><span class="sxs-lookup"><span data-stu-id="b2932-115">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span>
>
> 

## <a name="meet-hello-detaillevel"></a><span data-ttu-id="b2932-116">Spełnia hello atrybut DetailLevel</span><span class="sxs-lookup"><span data-stu-id="b2932-116">Meet hello DetailLevel</span></span>
<span data-ttu-id="b2932-117">W środowisku produkcyjnym aplikacji partii jednostek, takich jak zadania, zadania i węzły obliczeniowe można numerów w hello tysięcy.</span><span class="sxs-lookup"><span data-stu-id="b2932-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in hello thousands.</span></span> <span data-ttu-id="b2932-118">Gdy użytkownik żąda informacji na temat tych zasobów, potencjalnie dużą ilość danych musi "przechodzą przewodowy hello" z aplikacji tooyour usługi partii hello w każdym zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="b2932-118">When you request information on these resources, a potentially large amount of data must "cross hello wire" from hello Batch service tooyour application on each query.</span></span> <span data-ttu-id="b2932-119">Ograniczając hello liczbę elementów i typ danych zwróconych przez zapytanie wykonywane jest przyspieszenie hello zapytań i w związku z tym hello wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-119">By limiting hello number of items and type of information that is returned by a query, you can increase hello speed of your queries, and therefore hello performance of your application.</span></span>

<span data-ttu-id="b2932-120">To [partiami platformy .NET] [ api_net] list fragment kodu interfejsu API *co* zadanie, które jest skojarzone z zadaniem, wraz z *wszystkie* hello właściwości każdego z nich zadania:</span><span class="sxs-lookup"><span data-stu-id="b2932-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of hello properties of each task:</span></span>

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="b2932-121">Jednak bardziej efektywnego zapytanie listy, można wykonać przez zastosowanie kwerendy tooyour "poziom szczegółów".</span><span class="sxs-lookup"><span data-stu-id="b2932-121">You can perform a much more efficient list query, however, by applying a "detail level" tooyour query.</span></span> <span data-ttu-id="b2932-122">Aby to zrobić, podając [ODATADetailLevel] [ odata] obiekt toohello [JobOperations.ListTasks] [ net_list_tasks] metody.</span><span class="sxs-lookup"><span data-stu-id="b2932-122">You do this by supplying an [ODATADetailLevel][odata] object toohello [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="b2932-123">Ta Wstawka kodu zwraca identyfikator hello, wiersz polecenia i właściwości informacji węzła obliczeń zakończonych zadań:</span><span class="sxs-lookup"><span data-stu-id="b2932-123">This snippet returns only hello ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="b2932-124">W tym przykładowym scenariuszu, jeśli istnieją tysiące zadań w zadaniu hello hello wyniki z drugiego zapytania hello zwykle będą najpierw znacznie szybszy niż hello zwracane.</span><span class="sxs-lookup"><span data-stu-id="b2932-124">In this example scenario, if there are thousands of tasks in hello job, hello results from hello second query will typically be returned much quicker than hello first.</span></span> <span data-ttu-id="b2932-125">Więcej informacji o używaniu ODATADetailLevel wśród elementów z hello interfejs API .NET partii jest dołączony [poniżej](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="b2932-125">More information about using ODATADetailLevel when you list items with hello Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2932-126">Zdecydowanie zalecamy, aby użytkownik *zawsze* dostawy ODATADetailLevel obiektu tooyour interfejs API .NET listy wywołuje tooensure maksymalnej wydajności i wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-126">We highly recommend that you *always* supply an ODATADetailLevel object tooyour .NET API list calls tooensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="b2932-127">Umożliwia określenie poziomu szczegółowości, może pomóc toolower partii czasy odpowiedzi usługi, poprawić wykorzystanie sieci i zminimalizować użycie pamięci przez aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="b2932-127">By specifying a detail level, you can help toolower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="b2932-128">Filtruj, wybierz i rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="b2932-128">Filter, select, and expand</span></span>
<span data-ttu-id="b2932-129">Witaj [partiami platformy .NET] [ api_net] i [REST partii] [ api_rest] API stanowią tooreduce możliwości hello zarówno hello liczba elementów, które są zwracane w postaci listy a także hello ilość informacji, która jest zwracana dla każdego.</span><span class="sxs-lookup"><span data-stu-id="b2932-129">hello [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide hello ability tooreduce both hello number of items that are returned in a list, as well as hello amount of information that is returned for each.</span></span> <span data-ttu-id="b2932-130">Możesz to zrobić, określając **filtru**, **wybierz**, i **rozwiń ciągów** podczas wykonywania zapytania z listy.</span><span class="sxs-lookup"><span data-stu-id="b2932-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="b2932-131">Filtr</span><span class="sxs-lookup"><span data-stu-id="b2932-131">Filter</span></span>
<span data-ttu-id="b2932-132">ciąg filtru Hello jest wyrażenie, które zmniejsza hello liczbę elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="b2932-132">hello filter string is an expression that reduces hello number of items that are returned.</span></span> <span data-ttu-id="b2932-133">Na przykład listy tylko hello uruchomionych zadań dla zadania lub listy tylko węzły obliczeniowe, które są gotowe toorun zadania.</span><span class="sxs-lookup"><span data-stu-id="b2932-133">For example, list only hello running tasks for a job, or list only compute nodes that are ready toorun tasks.</span></span>

* <span data-ttu-id="b2932-134">ciąg filtru Hello składa się z co najmniej jednego wyrażenia z wyrażeniem, które składa się z nazwy właściwości, operator i wartość.</span><span class="sxs-lookup"><span data-stu-id="b2932-134">hello filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="b2932-135">Witaj właściwości, które można określić są tooeach określonych typów jednostek, które można zbadać są hello operatory, które są obsługiwane dla każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="b2932-135">hello properties that can be specified are specific tooeach entity type that you query, as are hello operators that are supported for each property.</span></span>
* <span data-ttu-id="b2932-136">Wiele wyrażeń można łączyć przy użyciu operatorów logicznych hello `and` i `or`.</span><span class="sxs-lookup"><span data-stu-id="b2932-136">Multiple expressions can be combined by using hello logical operators `and` and `or`.</span></span>
* <span data-ttu-id="b2932-137">W tym przykładzie filtrowanie list ciągów tylko zadania hello uruchomiona "renderowania": `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="b2932-137">This example filter string lists only hello running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="b2932-138">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="b2932-138">Select</span></span>
<span data-ttu-id="b2932-139">Wybierz ciąg Hello ogranicza hello wartości właściwości, które są zwracane dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="b2932-139">hello select string limits hello property values that are returned for each item.</span></span> <span data-ttu-id="b2932-140">Określ listę nazw właściwości, a dla elementów hello w wynikach zapytania hello są zwracane tylko wartości tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="b2932-140">You specify a list of property names, and only those property values are returned for hello items in hello query results.</span></span>

* <span data-ttu-id="b2932-141">Wybierz ciąg Hello składa się z listy rozdzielanej przecinkami nazw właściwości.</span><span class="sxs-lookup"><span data-stu-id="b2932-141">hello select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="b2932-142">Można określić właściwości powitania dla typu jednostki hello jest kwerenda.</span><span class="sxs-lookup"><span data-stu-id="b2932-142">You can specify any of hello properties for hello entity type you are querying.</span></span>
* <span data-ttu-id="b2932-143">Ten ciąg wybierz przykład określa, że powinny być zwracane tylko trzy wartości właściwości dla każdego zadania: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="b2932-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="b2932-144">Rozwiń</span><span class="sxs-lookup"><span data-stu-id="b2932-144">Expand</span></span>
<span data-ttu-id="b2932-145">Witaj rozwiń ciąg zmniejsza hello liczbę wywołań interfejsu API, które są wymagane tooobtain pewne informacje.</span><span class="sxs-lookup"><span data-stu-id="b2932-145">hello expand string reduces hello number of API calls that are required tooobtain certain information.</span></span> <span data-ttu-id="b2932-146">Korzystając z ciągu Rozwiń, można uzyskać więcej informacji o każdym elemencie przy użyciu jednego wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b2932-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="b2932-147">Zamiast pierwszego uzyskania hello listę jednostek, a następnie podać informacje dla każdego elementu na liście hello, użyj ciągu rozwiń tooobtain hello tych samych informacji w jednym wywołaniu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b2932-147">Rather than first obtaining hello list of entities, then requesting information for each item in hello list, you use an expand string tooobtain hello same information in a single API call.</span></span> <span data-ttu-id="b2932-148">Mniej wywołań interfejsu API oznaczają lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="b2932-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="b2932-149">Podobne toohello wybierz ciąg hello rozwiń formanty ciąg czy niektórych danych znajduje się w wynikach zapytania listy.</span><span class="sxs-lookup"><span data-stu-id="b2932-149">Similar toohello select string, hello expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="b2932-150">ciąg rozwiń Hello jest obsługiwana tylko gdy jest używany w listę zadań, harmonogramy zadań, zadań i pul.</span><span class="sxs-lookup"><span data-stu-id="b2932-150">hello expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="b2932-151">Obecnie obsługuje on tylko informacje statystyczne.</span><span class="sxs-lookup"><span data-stu-id="b2932-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="b2932-152">Gdy wszystkie właściwości są wymagane, a nie wybierz podano ciągu, hello rozwiń ciąg *musi* tooget używane statystyki informacje.</span><span class="sxs-lookup"><span data-stu-id="b2932-152">When all properties are required and no select string is specified, hello expand string *must* be used tooget statistics information.</span></span> <span data-ttu-id="b2932-153">Jeśli wybierz ciąg jest używany tooobtain podzbiór właściwości, następnie `stats` można określić w ciągu wybierz hello i hello rozwiń ciąg nie jest konieczne toobe określony.</span><span class="sxs-lookup"><span data-stu-id="b2932-153">If a select string is used tooobtain a subset of properties, then `stats` can be specified in hello select string, and hello expand string does not need toobe specified.</span></span>
* <span data-ttu-id="b2932-154">W tym przykładzie rozwiń ciąg Określa, że informacje statystyczne powinny być zwracane dla każdego elementu na liście hello: `stats`.</span><span class="sxs-lookup"><span data-stu-id="b2932-154">This example expand string specifies that statistics information should be returned for each item in hello list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="b2932-155">Podczas konstruowania żadnego hello trzy typy ciągów zapytań (filtrowanie, wybierz i rozwiń), należy upewnić się, że hello nazwy i właściwości przypadku odpowiadają ich odpowiedniki element interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b2932-155">When constructing any of hello three query string types (filter, select, and expand), you must ensure that hello property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="b2932-156">Na przykład podczas pracy z hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasy, należy określić **stanu** zamiast **stanu**, nawet jeśli jest hello właściwości platformy .NET [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="b2932-156">For example, when working with hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though hello .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="b2932-157">Zobacz poniższych tabelach hello mapowania właściwości między hello .NET i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="b2932-157">See hello tables below for property mappings between hello .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="b2932-158">Reguły filtra wybierz i rozwiń ciągów</span><span class="sxs-lookup"><span data-stu-id="b2932-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="b2932-159">Nazwy właściwości w filtrze, wybierz i rozwiń ciągi powinny być wyświetlane, tak jak w hello [REST partii] [ api_rest] interfejsu API — nawet wtedy, gdy używasz [partiami platformy .NET] [ api_net] lub jednego z hello innych zestawów SDK usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="b2932-159">Properties names in filter, select, and expand strings should appear as they do in hello [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of hello other Batch SDKs.</span></span>
* <span data-ttu-id="b2932-160">Wszystkie nazwy właściwości jest rozróżniana wielkość liter, ale wartości właściwości są bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="b2932-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="b2932-161">Data i godzina ciągów może być jednym z dwóch formatów i musi być poprzedzony `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="b2932-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="b2932-162">Przykładowy format W3C DTF:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="b2932-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="b2932-163">RFC 1123 Przykładowy format:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="b2932-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="b2932-164">Logiczna ciągi są albo `true` lub `false`.</span><span class="sxs-lookup"><span data-stu-id="b2932-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="b2932-165">Jeśli określono nieprawidłowe właściwości lub operatora `400 (Bad Request)` spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="b2932-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="b2932-166">Efektywne wykonywania zapytania w partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b2932-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="b2932-167">W ramach hello [partiami platformy .NET] [ api_net] interfejsu API, hello [ODATADetailLevel] [ odata] klasa jest używana do podawania filtru, wybierz i rozwiń ciągów operacje toolist.</span><span class="sxs-lookup"><span data-stu-id="b2932-167">Within hello [Batch .NET][api_net] API, hello [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings toolist operations.</span></span> <span data-ttu-id="b2932-168">Witaj ODataDetailLevel klasa ma trzy właściwości publicznych parametrów, które mogą być określony w Konstruktorze hello lub ustawić bezpośrednio dla obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="b2932-168">hello ODataDetailLevel class has three public string properties that can be specified in hello constructor, or set directly on hello object.</span></span> <span data-ttu-id="b2932-169">Można następnie przekazać hello ODataDetailLevel obiektu jako toohello parametru różne operacje listy takich jak [ListPools][net_list_pools], [ListJobs][net_list_jobs], i [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="b2932-169">You then pass hello ODataDetailLevel object as a parameter toohello various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="b2932-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: Ogranicz hello liczbę elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="b2932-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit hello number of items that are returned.</span></span>
* <span data-ttu-id="b2932-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: Określ wartości właściwości, które są zwracane z każdym elementem.</span><span class="sxs-lookup"><span data-stu-id="b2932-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="b2932-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: pobieranie danych dla wszystkich elementów w jeden interfejs API Wywołaj zamiast wywołań dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="b2932-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="b2932-173">Witaj poniższy fragment kodu używa hello interfejs API partii .NET tooefficiently zapytania hello partii usługi statystyki hello zestawu pul.</span><span class="sxs-lookup"><span data-stu-id="b2932-173">hello following code snippet uses hello Batch .NET API tooefficiently query hello Batch service for hello statistics of a specific set of pools.</span></span> <span data-ttu-id="b2932-174">W tym scenariuszu użytkownik partii hello ma pule zarówno testowego i produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b2932-174">In this scenario, hello Batch user has both test and production pools.</span></span> <span data-ttu-id="b2932-175">Hello testu puli identyfikatorów nazwy są poprzedzone ciągiem "test", a nazwy są poprzedzone ciągiem "produkcyjną" hello produkcji puli identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="b2932-175">hello test pool IDs are prefixed with "test", and hello production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="b2932-176">We fragmencie hello *myBatchClient* jest prawidłowo zainicjowany wystąpieniem hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasy.</span><span class="sxs-lookup"><span data-stu-id="b2932-176">In hello snippet, *myBatchClient* is a properly initialized instance of hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="b2932-177">Wystąpienie [ODATADetailLevel] [ odata] skonfigurowanego wybierz i rozwiń klauzule mogą również zostać przekazana tooappropriate metody Get, takich jak [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello ilość danych, która jest zwracana.</span><span class="sxs-lookup"><span data-stu-id="b2932-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed tooappropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), toolimit hello amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a><span data-ttu-id="b2932-178">Mapowania partii interfejsu API REST too.NET</span><span class="sxs-lookup"><span data-stu-id="b2932-178">Batch REST too.NET API mappings</span></span>
<span data-ttu-id="b2932-179">Nazwy właściwości w filtrze, wybierz i rozwiń ciągów *musi* ich odpowiedniki interfejsu API REST, zarówno w nazwie i w przypadku uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="b2932-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="b2932-180">w poniższych tabelach Hello zawierają mapowania między hello .NET i odpowiedników interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b2932-180">hello tables below provide mappings between hello .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="b2932-181">Mapowania dla filtru ciągów</span><span class="sxs-lookup"><span data-stu-id="b2932-181">Mappings for filter strings</span></span>
* <span data-ttu-id="b2932-182">**Metody listy .NET**: każdej z metod interfejsu API platformy .NET hello w tej kolumnie akceptuje [ODATADetailLevel] [ odata] obiektu jako parametr.</span><span class="sxs-lookup"><span data-stu-id="b2932-182">**.NET list methods**: Each of hello .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="b2932-183">**Żądania listy REST**: każdy interfejsu API REST strony połączonego tooin ta kolumna zawiera tabelę, która określa właściwości hello i operacji, które są dozwolone w *filtru* ciągów.</span><span class="sxs-lookup"><span data-stu-id="b2932-183">**REST list requests**: Each REST API page linked tooin this column contains a table that specifies hello properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="b2932-184">Użyjesz tych nazw właściwości i operacji utworzenia [ODATADetailLevel.FilterClause] [ odata_filter] ciąg.</span><span class="sxs-lookup"><span data-stu-id="b2932-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="b2932-185">Metody listy .NET</span><span class="sxs-lookup"><span data-stu-id="b2932-185">.NET list methods</span></span> | <span data-ttu-id="b2932-186">Żądania listy REST</span><span class="sxs-lookup"><span data-stu-id="b2932-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="b2932-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="b2932-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="b2932-188">[Wyświetl certyfikaty hello konta][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="b2932-188">[List hello certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="b2932-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="b2932-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="b2932-190">[Lista hello pliki skojarzone z zadaniem][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="b2932-190">[List hello files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="b2932-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="b2932-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="b2932-192">[Stan listy hello hello zadanie przygotowanie i zadania zlecenia zadań dla zadania][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="b2932-192">[List hello status of hello job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="b2932-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="b2932-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="b2932-194">[Lista hello zadania konta][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="b2932-194">[List hello jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="b2932-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="b2932-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="b2932-196">[Lista plików hello w węźle][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="b2932-196">[List hello files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="b2932-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="b2932-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="b2932-198">[Lista zadań hello skojarzone z zadaniem][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="b2932-198">[List hello tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="b2932-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="b2932-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="b2932-200">[Harmonogramy zadań hello listy konta][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="b2932-200">[List hello job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="b2932-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="b2932-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="b2932-202">[Lista hello zadań skojarzonych z harmonogramu zadań][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="b2932-202">[List hello jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="b2932-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="b2932-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="b2932-204">[Lista hello obliczeniowe węzłów w puli][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="b2932-204">[List hello compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="b2932-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="b2932-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="b2932-206">[Lista pul hello konta][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="b2932-206">[List hello pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="b2932-207">Mapowania dla wybierz ciągów</span><span class="sxs-lookup"><span data-stu-id="b2932-207">Mappings for select strings</span></span>
* <span data-ttu-id="b2932-208">**Typy .NET partii**: typy interfejsu API partii .NET.</span><span class="sxs-lookup"><span data-stu-id="b2932-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="b2932-209">**Interfejs API REST jednostek**: każdej strony w tej kolumnie zawiera co najmniej jednej tabeli, które listę nazw właściwości interfejsu API REST hello hello typu.</span><span class="sxs-lookup"><span data-stu-id="b2932-209">**REST API entities**: Each page in this column contains one or more tables that list hello REST API property names for hello type.</span></span> <span data-ttu-id="b2932-210">Te nazwy właściwości są używane podczas utworzymy *wybierz* ciągów.</span><span class="sxs-lookup"><span data-stu-id="b2932-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="b2932-211">Utworzenia użyje tych samych nazw właściwości [ODATADetailLevel.SelectClause] [ odata_select] ciąg.</span><span class="sxs-lookup"><span data-stu-id="b2932-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="b2932-212">Typy .NET partii</span><span class="sxs-lookup"><span data-stu-id="b2932-212">Batch .NET types</span></span> | <span data-ttu-id="b2932-213">Jednostki interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b2932-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="b2932-214">[Certyfikat][net_cert]</span><span class="sxs-lookup"><span data-stu-id="b2932-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="b2932-215">[Uzyskiwanie informacji o certyfikacie][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="b2932-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="b2932-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="b2932-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="b2932-217">[Pobierz informacje o zadaniu][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="b2932-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="b2932-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="b2932-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="b2932-219">[Pobierz informacje o harmonogram zadań][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="b2932-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="b2932-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="b2932-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="b2932-221">[Pobierz informacje o węźle][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="b2932-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="b2932-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="b2932-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="b2932-223">[Pobierz informacje o puli][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="b2932-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="b2932-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="b2932-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="b2932-225">[Pobierz informacje o zadaniu][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="b2932-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="b2932-226">Przykład: skonstruować ciąg filtru</span><span class="sxs-lookup"><span data-stu-id="b2932-226">Example: construct a filter string</span></span>
<span data-ttu-id="b2932-227">Podczas konstruowania ciąg filtru dla [ODATADetailLevel.FilterClause][odata_filter], zapoznaj się z powyższej tabeli hello w obszarze "Mapowania dla filtru ciągów" toofind hello interfejsu API REST stronę dokumentacji odpowiadający Operacja listy toohello, że chcesz tooperform.</span><span class="sxs-lookup"><span data-stu-id="b2932-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult hello table above under "Mappings for filter strings" toofind hello REST API documentation page that corresponds toohello list operation that you wish tooperform.</span></span> <span data-ttu-id="b2932-228">W pierwszej tabeli multirow hello na tej stronie znajdziesz hello filtrowanie właściwości i ich operatory obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b2932-228">You will find hello filterable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="b2932-229">Jeśli chcesz tooretrieve wszystkie zadania, którego kod zakończenia: różną od zera, na przykład to wiersz na [listy zadań hello skojarzonych z zadaniem] [ rest_list_tasks] Określa ciąg odpowiednie właściwości hello i dozwolone operatory:</span><span class="sxs-lookup"><span data-stu-id="b2932-229">If you wish tooretrieve all tasks whose exit code was nonzero, for example, this row on [List hello tasks associated with a job][rest_list_tasks] specifies hello applicable property string and allowable operators:</span></span>

| <span data-ttu-id="b2932-230">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b2932-230">Property</span></span> | <span data-ttu-id="b2932-231">Operacje dozwolone</span><span class="sxs-lookup"><span data-stu-id="b2932-231">Operations allowed</span></span> | <span data-ttu-id="b2932-232">Typ</span><span class="sxs-lookup"><span data-stu-id="b2932-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="b2932-233">W związku z tym będzie hello ciąg filtru wyświetlania list wszystkie zadania z kodem zakończenia różną od zera:</span><span class="sxs-lookup"><span data-stu-id="b2932-233">Thus, hello filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="b2932-234">Przykład: skonstruować wybierz ciąg</span><span class="sxs-lookup"><span data-stu-id="b2932-234">Example: construct a select string</span></span>
<span data-ttu-id="b2932-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], zapoznaj się z powyższej tabeli hello w obszarze "Mapowania dla ciągów select" i przejdź toohello strony interfejsu API REST, która odpowiada toohello typ jednostki, które Lista.</span><span class="sxs-lookup"><span data-stu-id="b2932-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], consult hello table above under "Mappings for select strings" and navigate toohello REST API page that corresponds toohello type of entity that you are listing.</span></span> <span data-ttu-id="b2932-236">W pierwszej tabeli multirow hello na tej stronie można znaleźć właściwości selectable hello i ich operatory obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b2932-236">You will find hello selectable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="b2932-237">Jeśli chcesz tylko identyfikator hello tooretrieve i wiersz polecenia dla każdego zadania na liście, na przykład można znaleźć te wiersze w tabeli dotyczy hello w [uzyskać informacje o zadaniu][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="b2932-237">If you wish tooretrieve only hello ID and command line for each task in a list, for example, you will find these rows in hello applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="b2932-238">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b2932-238">Property</span></span> | <span data-ttu-id="b2932-239">Typ</span><span class="sxs-lookup"><span data-stu-id="b2932-239">Type</span></span> | <span data-ttu-id="b2932-240">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b2932-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

<span data-ttu-id="b2932-241">następnie będzie wybierz ciąg Hello tylko identyfikator hello i wiersza polecenia do każdego zadania wymienione w tym:</span><span class="sxs-lookup"><span data-stu-id="b2932-241">hello select string for including only hello ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="b2932-242">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="b2932-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="b2932-243">Przykładowy kod zapytania wydajne listy</span><span class="sxs-lookup"><span data-stu-id="b2932-243">Efficient list queries code sample</span></span>
<span data-ttu-id="b2932-244">Zapoznaj się z hello [EfficientListQueries] [ efficient_query_sample] przykładowy projekt w sposób wydajny toosee GitHub zapytań listy może wpłynąć na wydajność w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-244">Check out hello [EfficientListQueries][efficient_query_sample] sample project on GitHub toosee how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="b2932-245">Tę aplikację konsolową C#, tworzy i dodaje dużej liczby zadań tooa zadania.</span><span class="sxs-lookup"><span data-stu-id="b2932-245">This C# console application creates and adds a large number of tasks tooa job.</span></span> <span data-ttu-id="b2932-246">Następnie, ułatwia wielu wywołań toohello [JobOperations.ListTasks] [ net_list_tasks] — metoda i przekazuje [ODATADetailLevel] [ odata] obiektów, które są skonfigurowane przy użyciu różnych właściwości wartości toovary hello ilość danych toobe zwrócony.</span><span class="sxs-lookup"><span data-stu-id="b2932-246">Then, it makes multiple calls toohello [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values toovary hello amount of data toobe returned.</span></span> <span data-ttu-id="b2932-247">Generuje dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b2932-247">It produces output similar toohello following:</span></span>

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

<span data-ttu-id="b2932-248">Jak pokazano na czas hello, można znacznie obniżyć czas odpowiedzi na zapytania, ograniczając hello właściwości i hello liczba elementów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="b2932-248">As shown in hello elapsed times, you can greatly lower query response times by limiting hello properties and hello number of items that are returned.</span></span> <span data-ttu-id="b2932-249">Możesz znaleźć tego i innych przykładowych projektach w hello [azure partii próbek] [ github_samples] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2932-249">You can find this and other sample projects in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="b2932-250">BatchMetrics biblioteki i kod przykładowy</span><span class="sxs-lookup"><span data-stu-id="b2932-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="b2932-251">Ponadto toohello EfficientListQueries przykładowym kodzie powyżej można znaleźć hello [BatchMetrics] [ batch_metrics] projektu w hello [azure partii próbek] [ github_samples] Repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2932-251">In addition toohello EfficientListQueries code sample above, you can find hello [BatchMetrics][batch_metrics] project in hello [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="b2932-252">Witaj BatchMetrics przykładowy projekt pokazano, jak tooefficiently monitorować postęp zadania partii zadań Azure za pomocą hello interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="b2932-252">hello BatchMetrics sample project demonstrates how tooefficiently monitor Azure Batch job progress using hello Batch API.</span></span>

<span data-ttu-id="b2932-253">Hello [BatchMetrics] [ batch_metrics] próbki obejmuje projektu biblioteki klas .NET, które można zastosować do własnych projektów i prostą wiersza polecenia programu tooexercise i Wykaż hello stosowania hello Biblioteka.</span><span class="sxs-lookup"><span data-stu-id="b2932-253">hello [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program tooexercise and demonstrate hello use of hello library.</span></span>

<span data-ttu-id="b2932-254">aplikacja przykładowa Hello w projekcie hello prezentuje hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="b2932-254">hello sample application within hello project demonstrates hello following operations:</span></span>

1. <span data-ttu-id="b2932-255">Wybranie określonych atrybutów w kolejności toodownload tylko właściwości hello należy</span><span class="sxs-lookup"><span data-stu-id="b2932-255">Selecting specific attributes in order toodownload only hello properties you need</span></span>
2. <span data-ttu-id="b2932-256">Filtrowanie na czas przejścia stanu w kolejności toodownload zmienia tylko od czasu ostatniej kwerendy hello</span><span class="sxs-lookup"><span data-stu-id="b2932-256">Filtering on state transition times in order toodownload only changes since hello last query</span></span>

<span data-ttu-id="b2932-257">Na przykład następujące metody hello pojawia się w hello BatchMetrics biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b2932-257">For example, hello following method appears in hello BatchMetrics library.</span></span> <span data-ttu-id="b2932-258">Zwraca ODATADetailLevel, która określa, że tylko hello `id` i `state` właściwości mają być uzyskiwane dla hello jednostek, które będą pytani.</span><span class="sxs-lookup"><span data-stu-id="b2932-258">It returns an ODATADetailLevel that specifies that only hello `id` and `state` properties should be obtained for hello entities that are queried.</span></span> <span data-ttu-id="b2932-259">On również określa, że tylko obiektów, których stan zmienił się od hello określony `DateTime` parametr ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="b2932-259">It also specifies that only entities whose state has changed since hello specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="b2932-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2932-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="b2932-261">Zadania równoległych węzła</span><span class="sxs-lookup"><span data-stu-id="b2932-261">Parallel node tasks</span></span>
<span data-ttu-id="b2932-262">[Maksymalizowanie użycia zasobów obliczeniowych partii zadań Azure z węzła równoczesnych zadań](batch-parallel-node-tasks.md) jest inny artykuł powiązane tooBatch wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related tooBatch application performance.</span></span> <span data-ttu-id="b2932-263">Niektóre rodzaje obciążeń mogą korzystać z wykonywanych zadań równoległych na większych — ale mniej — węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="b2932-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="b2932-264">Zapoznaj się z hello [przykładowy scenariusz](batch-parallel-node-tasks.md#example-scenario) w artykule hello, aby uzyskać szczegółowe informacje o takiej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="b2932-264">Check out hello [example scenario](batch-parallel-node-tasks.md#example-scenario) in hello article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="b2932-265">Forum usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="b2932-265">Batch Forum</span></span>
<span data-ttu-id="b2932-266">Witaj [Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello.</span><span class="sxs-lookup"><span data-stu-id="b2932-266">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="b2932-267">HEAD na za pośrednictwem przydatne Posty "trwałe" i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="b2932-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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