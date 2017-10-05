---
title: "Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs"
description: "Dowiedz się, jak używać magazynu tabel Azure przy użyciu zestawu SDK zadań Webjob. Tworzenie tabel, Dodaj jednostki do tabel i istniejące tabele do odczytu."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="cb763-104">Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs</span><span class="sxs-lookup"><span data-stu-id="cb763-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="cb763-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cb763-105">Overview</span></span>
<span data-ttu-id="cb763-106">Ten przewodnik zawiera C# przykładów kodu przedstawiają sposób odczytu i zapisu przy użyciu tabel magazynu Azure [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="cb763-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="cb763-107">Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md) lub [wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="cb763-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="cb763-108">Niektóre Pokaż wstawki kodu `Table` atrybutu używanego w funkcje, które są [wywołuje ręcznie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), oznacza to, nie za pomocą jednego z atrybutów wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="cb763-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="cb763-109"><a id="ingress"></a>Jak dodać jednostek do tabeli</span><span class="sxs-lookup"><span data-stu-id="cb763-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="cb763-110">Aby dodać jednostek do tabeli, należy użyć `Table` atrybutem `ICollector<T>` lub `IAsyncCollector<T>` parametru gdzie `T` Określa schemat jednostek, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="cb763-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="cb763-111">Konstruktor atrybutu ma parametr typu string, który określa nazwę tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb763-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="cb763-112">Poniższy przykładowy kod dodaje `Person` jednostek do tabeli o nazwie *wejściowych*.</span><span class="sxs-lookup"><span data-stu-id="cb763-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="cb763-113">Zwykle typ używających `ICollector` pochodną `TableEntity` lub implementuje `ITableEntity`, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="cb763-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="cb763-114">Jedną z następujących `Person` klasy pracy kodem przedstawionym w poprzednim `Ingress` metody.</span><span class="sxs-lookup"><span data-stu-id="cb763-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="cb763-115">Jeśli chcesz pracować bezpośrednio za pomocą interfejsu API magazynu Azure, można dodać `CloudStorageAccount` parametru w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="cb763-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="cb763-116"><a id="monitor"></a>Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="cb763-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="cb763-117">Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="cb763-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="cb763-118">**Dziennika wywołania** sekcji informuje, czy funkcja jest nadal uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="cb763-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="cb763-120">**Szczegóły wywołania** raporty strony postępu funkcji (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość jego przerwanie.</span><span class="sxs-lookup"><span data-stu-id="cb763-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="cb763-122">Po zakończeniu działania funkcji **szczegóły wywołania** liczbę wierszy, zapisany raporty strony.</span><span class="sxs-lookup"><span data-stu-id="cb763-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Transfer danych przychodzących Zakończono — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="cb763-124"><a id="multiple"></a>Jak można odczytać wiele jednostek z tabeli</span><span class="sxs-lookup"><span data-stu-id="cb763-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="cb763-125">Aby odczytać tabeli, należy użyć `Table` atrybutem `IQueryable<T>` parametru wpisuje `T` pochodną `TableEntity` lub implementuje `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="cb763-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="cb763-126">Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z `Ingress` tabeli:</span><span class="sxs-lookup"><span data-stu-id="cb763-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="cb763-127"><a id="readone"></a>Jak można odczytać pojedyncza jednostka z tabeli</span><span class="sxs-lookup"><span data-stu-id="cb763-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="cb763-128">Brak `Table` konstruktora atrybutu z dwóch dodatkowych parametrów, które pozwalają określić klucz partycji i klucz wiersza, jeśli chcesz powiązać jednostki pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb763-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="cb763-129">Poniższy przykładowy kod odczytuje wiersz tabeli `Person` jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:</span><span class="sxs-lookup"><span data-stu-id="cb763-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="cb763-130">`Person` Klasy w tym przykładzie nie musi implementować `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="cb763-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="cb763-131"><a id="storageapi"></a>Sposób użycia interfejsu API programu .NET magazynu bezpośrednio do pracy z tabeli</span><span class="sxs-lookup"><span data-stu-id="cb763-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="cb763-132">Można również użyć `Table` atrybutem `CloudTable` obiektu dla większą elastyczność podczas pracy z tabelą.</span><span class="sxs-lookup"><span data-stu-id="cb763-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="cb763-133">Poniższy kod przykładowy używa `CloudTable` obiekt do dodania do pojedynczej jednostki *wejściowych* tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb763-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="cb763-134">Aby uzyskać więcej informacji o sposobie używania `CloudTable` obiektów, zobacz [jak używać magazynu tabel w .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cb763-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="cb763-135"><a id="queues"></a>Tematy pokrewne objętych artykule kolejek</span><span class="sxs-lookup"><span data-stu-id="cb763-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="cb763-136">Informacje o sposobie obsługi przetwarzania tabeli wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob scenariusze nie są typowe dla przetwarzania tabeli, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="cb763-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="cb763-137">Tematy w tym artykule są następujące:</span><span class="sxs-lookup"><span data-stu-id="cb763-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="cb763-138">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="cb763-138">Async functions</span></span>
* <span data-ttu-id="cb763-139">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="cb763-139">Multiple instances</span></span>
* <span data-ttu-id="cb763-140">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="cb763-140">Graceful shutdown</span></span>
* <span data-ttu-id="cb763-141">Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji</span><span class="sxs-lookup"><span data-stu-id="cb763-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="cb763-142">Ustaw parametry połączenia SDK w kodzie</span><span class="sxs-lookup"><span data-stu-id="cb763-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="cb763-143">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="cb763-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="cb763-144">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="cb763-144">Trigger a function manually</span></span>
* <span data-ttu-id="cb763-145">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="cb763-145">Write logs</span></span>

## <span data-ttu-id="cb763-146"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb763-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="cb763-147">W tym przewodniku udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="cb763-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="cb763-148">Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="cb763-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

