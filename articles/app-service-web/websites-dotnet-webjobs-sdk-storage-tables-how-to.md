---
title: "toouse aaaHow magazynu tabel platformy Azure z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob. Tworzenie tabel, Dodaj tootables jednostek, a istniejące tabele do odczytu."
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="a358b-104">Jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="a358b-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="a358b-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a358b-105">Overview</span></span>
<span data-ttu-id="a358b-106">Ten przewodnik zawiera przykłady kodu w języku C# przedstawiające sposób zapisu magazynu Azure i tooread tabel za pomocą [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="a358b-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="a358b-107">Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="a358b-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="a358b-108">Niektóre fragmentów kodu hello widoczne hello `Table` atrybutu używanego w funkcje, które są [wywołuje ręcznie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), oznacza to, nie za pomocą jednego z atrybutów wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="a358b-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="a358b-109"><a id="ingress"></a>Jak tooadd jednostek tooa tabeli</span><span class="sxs-lookup"><span data-stu-id="a358b-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="a358b-110">tooadd jednostek tooa tabeli, użyj hello `Table` atrybutem `ICollector<T>` lub `IAsyncCollector<T>` parametru gdzie `T` Określa schemat hello jednostek hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="a358b-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="a358b-111">Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="a358b-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="a358b-112">Witaj Poniższy przykładowy kod dodaje `Person` jednostek tooa tabeli o nazwie *wejściowych*.</span><span class="sxs-lookup"><span data-stu-id="a358b-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="a358b-113">Zwykle hello typu używających `ICollector` pochodną `TableEntity` lub implementuje `ITableEntity`, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="a358b-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="a358b-114">Jedną z następujących hello `Person` klasy Praca z kodem hello pokazano w poprzednim hello `Ingress` metody.</span><span class="sxs-lookup"><span data-stu-id="a358b-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="a358b-115">Jeśli chcesz toowork bezpośrednio z hello magazynu Azure, interfejsu API, można dodać `CloudStorageAccount` podpis metody toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="a358b-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="a358b-116"><a id="monitor"></a>Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="a358b-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="a358b-117">Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, hello zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="a358b-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="a358b-118">Witaj **dziennika wywołania** sekcji informuje, czy funkcja hello nadal działa.</span><span class="sxs-lookup"><span data-stu-id="a358b-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="a358b-120">Hello **szczegóły wywołania** raporty strony hello funkcji postępu (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość tooabort go.</span><span class="sxs-lookup"><span data-stu-id="a358b-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="a358b-122">Gdy funkcja hello zakończeniu hello **szczegóły wywołania** hello liczbę wierszy, zapisany raporty strony.</span><span class="sxs-lookup"><span data-stu-id="a358b-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Transfer danych przychodzących Zakończono — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="a358b-124"><a id="multiple"></a>Jak tooread wiele jednostek z tabeli</span><span class="sxs-lookup"><span data-stu-id="a358b-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="a358b-125">tooread tabelę, użyj hello `Table` atrybutem `IQueryable<T>` parametru wpisuje `T` pochodną `TableEntity` lub implementuje `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="a358b-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="a358b-126">Witaj Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z hello `Ingress` tabeli:</span><span class="sxs-lookup"><span data-stu-id="a358b-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="a358b-127"><a id="readone"></a>Jak tooread pojedyncza jednostka z tabeli</span><span class="sxs-lookup"><span data-stu-id="a358b-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="a358b-128">Brak `Table` konstruktora atrybutu z dwóch dodatkowych parametrów, które umożliwiają określenie hello klucz partycji i klucz wiersza, jeśli chcesz toobind tooa pojedynczej tabeli jednostki.</span><span class="sxs-lookup"><span data-stu-id="a358b-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="a358b-129">Witaj Poniższy przykładowy kod odczytuje wiersz tabeli `Person` jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:</span><span class="sxs-lookup"><span data-stu-id="a358b-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="a358b-130">Witaj `Person` klasy w tym przykładzie nie ma tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="a358b-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="a358b-131"><a id="storageapi"></a>Jak toouse hello interfejsu API magazynu .NET bezpośrednio toowork z tabeli</span><span class="sxs-lookup"><span data-stu-id="a358b-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="a358b-132">Można również użyć hello `Table` atrybutem `CloudTable` obiektu dla większą elastyczność podczas pracy z tabelą.</span><span class="sxs-lookup"><span data-stu-id="a358b-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="a358b-133">Witaj poniższy kod używa próbki `CloudTable` obiekt tooadd toohello pojedynczej jednostki *wejściowych* tabeli.</span><span class="sxs-lookup"><span data-stu-id="a358b-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="a358b-134">Aby uzyskać więcej informacji na temat toouse hello `CloudTable` obiektów, zobacz [jak toouse magazynu tabel w .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a358b-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="a358b-135"><a id="queues"></a>Tematy pokrewne objętych kolejek hello jak tooarticle</span><span class="sxs-lookup"><span data-stu-id="a358b-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="a358b-136">Uzyskać informacji na temat sposobu przetwarzania tabeli toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tootable przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a358b-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="a358b-137">Tematy w tym artykule Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a358b-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="a358b-138">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="a358b-138">Async functions</span></span>
* <span data-ttu-id="a358b-139">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="a358b-139">Multiple instances</span></span>
* <span data-ttu-id="a358b-140">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="a358b-140">Graceful shutdown</span></span>
* <span data-ttu-id="a358b-141">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="a358b-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="a358b-142">Ustawianie parametrów połączenia SDK hello w kodzie</span><span class="sxs-lookup"><span data-stu-id="a358b-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="a358b-143">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="a358b-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="a358b-144">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="a358b-144">Trigger a function manually</span></span>
* <span data-ttu-id="a358b-145">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="a358b-145">Write logs</span></span>

## <span data-ttu-id="a358b-146"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a358b-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="a358b-147">W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a358b-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="a358b-148">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a358b-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

