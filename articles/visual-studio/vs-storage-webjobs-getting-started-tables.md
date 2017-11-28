---
title: "Wprowadzenie do magazynu Azure i programu Visual Studio połączone usługi (zadania WebJob projekty)"
description: "Jak rozpocząć pracę przy użyciu magazynu tabel Azure w projekcie zadań Webjob Azure w programie Visual Studio po połączeniu z kontem magazynu za pomocą programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 0bf51f9113c45c747cd4fd3f76bdabd4a4c1f8e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="1cb34-103">Wprowadzenie do korzystania z usługi Azure magazynu (projekty zadanie WebJob platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="1cb34-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="1cb34-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1cb34-104">Overview</span></span>
<span data-ttu-id="1cb34-105">Ten artykuł zawiera C# przykłady pokazujące pokazują, jak korzystać z wersji zestawu Azure WebJobs SDK 1.x z usługi Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb34-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="1cb34-106">Kod przykłady użycia [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="1cb34-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="1cb34-107">Usługa Azure Table storage umożliwia przechowywania dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="1cb34-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="1cb34-108">Usługa jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb34-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="1cb34-109">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="1cb34-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="1cb34-110">Zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1cb34-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="1cb34-111">Niektóre Pokaż wstawki kodu **tabeli** atrybutu używanego w funkcje, które są nazywane ręcznie, oznacza to, nie za pomocą jednego z atrybutów wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="1cb34-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="1cb34-112">Jak dodać jednostek do tabeli</span><span class="sxs-lookup"><span data-stu-id="1cb34-112">How to add entities to a table</span></span>
<span data-ttu-id="1cb34-113">Aby dodać jednostek do tabeli, należy użyć **tabeli** atrybutem **ICollector<T>**  lub **IAsyncCollector<T>**  parametru gdzie **T** Określa schemat jednostek, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="1cb34-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="1cb34-114">Konstruktor atrybutu ma parametr typu string, który określa nazwę tabeli.</span><span class="sxs-lookup"><span data-stu-id="1cb34-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="1cb34-115">Poniższy przykładowy kod dodaje **osoby** jednostek do tabeli o nazwie *wejściowych*.</span><span class="sxs-lookup"><span data-stu-id="1cb34-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="1cb34-116">Zwykle typ używających **ICollector** pochodną **TableEntity** lub implementuje **ITableEntity**, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="1cb34-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="1cb34-117">Jedną z następujących **osoby** klasy pracy kodem przedstawionym w poprzednim **wejściowych** — metoda.</span><span class="sxs-lookup"><span data-stu-id="1cb34-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="1cb34-118">Jeśli chcesz pracować bezpośrednio za pomocą interfejsu API magazynu Azure, można dodać **CloudStorageAccount** parametru w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="1cb34-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="1cb34-119">Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1cb34-119">Real-time monitoring</span></span>
<span data-ttu-id="1cb34-120">Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1cb34-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="1cb34-121">**Dziennika wywołania** sekcji informuje, czy funkcja jest nadal uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="1cb34-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="1cb34-123">**Szczegóły wywołania** raporty strony postępu funkcji (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość jego przerwanie.</span><span class="sxs-lookup"><span data-stu-id="1cb34-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="1cb34-125">Po zakończeniu działania funkcji **szczegóły wywołania** liczbę wierszy, zapisany raporty strony.</span><span class="sxs-lookup"><span data-stu-id="1cb34-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Transfer danych przychodzących Zakończono — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="1cb34-127">Jak można odczytać wiele jednostek z tabeli</span><span class="sxs-lookup"><span data-stu-id="1cb34-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="1cb34-128">Aby odczytać tabeli, należy użyć **tabeli** atrybutem **IQueryable<T>**  parametru wpisuje **T** pochodną **TableEntity** lub implementuje **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="1cb34-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="1cb34-129">Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z **wejściowych** tabeli:</span><span class="sxs-lookup"><span data-stu-id="1cb34-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="1cb34-130">Jak można odczytać pojedyncza jednostka z tabeli</span><span class="sxs-lookup"><span data-stu-id="1cb34-130">How to read a single entity from a table</span></span>
<span data-ttu-id="1cb34-131">Brak **tabeli** konstruktora atrybutu z dwóch dodatkowych parametrów, które pozwalają określić klucz partycji i klucz wiersza, jeśli chcesz powiązać jednostki pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="1cb34-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="1cb34-132">Poniższy przykładowy kod odczytuje wiersz tabeli **osoby** jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:</span><span class="sxs-lookup"><span data-stu-id="1cb34-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="1cb34-133">**Osoby** klasy w tym przykładzie nie musi implementować **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="1cb34-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="1cb34-134">Sposób użycia interfejsu API programu .NET magazynu bezpośrednio do pracy z tabeli</span><span class="sxs-lookup"><span data-stu-id="1cb34-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="1cb34-135">Można również użyć **tabeli** atrybutem **CloudTable** obiektu dla większą elastyczność podczas pracy z tabelą.</span><span class="sxs-lookup"><span data-stu-id="1cb34-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="1cb34-136">Poniższy kod przykładowy używa **CloudTable** obiekt do dodania do pojedynczej jednostki *wejściowych* tabeli.</span><span class="sxs-lookup"><span data-stu-id="1cb34-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="1cb34-137">Aby uzyskać więcej informacji o sposobie używania **CloudTable** obiektów, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="1cb34-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="1cb34-138">Tematy pokrewne objętych artykule kolejek</span><span class="sxs-lookup"><span data-stu-id="1cb34-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="1cb34-139">Informacje o sposobie obsługi przetwarzania tabeli wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob scenariusze nie są typowe dla przetwarzania tabeli, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (projekty zadania WebJob)](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1cb34-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cb34-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cb34-140">Next steps</span></span>
<span data-ttu-id="1cb34-141">W tym artykule udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb34-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="1cb34-142">Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="1cb34-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

