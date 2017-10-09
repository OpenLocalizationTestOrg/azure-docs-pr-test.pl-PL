---
title: "aaaGetting uruchomiono z magazynu Azure i programu Visual Studio połączone usługi (zadania WebJob projekty)"
description: "Jak tooget pracy z magazynem tabel Azure w projekcie zadań Webjob Azure w programie Visual Studio, po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="d9635-103">Wprowadzenie do korzystania z usługi Azure magazynu (projekty zadanie WebJob platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="d9635-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d9635-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d9635-104">Overview</span></span>
<span data-ttu-id="d9635-105">Ten artykuł zawiera C# przykłady pokazujące Pokaż jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d9635-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="d9635-106">Przykłady kodu Hello Użyj hello [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="d9635-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="d9635-107">Usługa Azure Table storage Hello umożliwia toostore dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="d9635-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="d9635-108">Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="d9635-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="d9635-109">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d9635-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="d9635-110">Zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md#create-a-table) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d9635-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="d9635-111">Niektóre fragmentów kodu hello widoczne hello **tabeli** atrybutu używanego w funkcje, które są nazywane ręcznie, oznacza to, nie za pomocą jednego z atrybutów wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="d9635-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="d9635-112">Jak tooadd jednostek tooa tabeli</span><span class="sxs-lookup"><span data-stu-id="d9635-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="d9635-113">tooadd jednostek tooa tabeli, użyj hello **tabeli** atrybutem **ICollector<T>**  lub **IAsyncCollector<T>**  parametru gdzie **T** Określa schemat hello jednostek hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9635-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="d9635-114">Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d9635-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="d9635-115">Witaj Poniższy przykładowy kod dodaje **osoby** jednostek tooa tabeli o nazwie *wejściowych*.</span><span class="sxs-lookup"><span data-stu-id="d9635-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="d9635-116">Zwykle hello typu używających **ICollector** pochodną **TableEntity** lub implementuje **ITableEntity**, ale nie ma.</span><span class="sxs-lookup"><span data-stu-id="d9635-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="d9635-117">Jedną z następujących hello **osoby** klasy Praca z kodem hello pokazano w poprzednim hello **transfer danych przychodzących** metody.</span><span class="sxs-lookup"><span data-stu-id="d9635-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="d9635-118">Jeśli chcesz toowork bezpośrednio z hello magazynu Azure, interfejsu API, można dodać **CloudStorageAccount** podpis metody toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="d9635-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="d9635-119">Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d9635-119">Real-time monitoring</span></span>
<span data-ttu-id="d9635-120">Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, hello zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="d9635-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="d9635-121">Witaj **dziennika wywołania** sekcji informuje, czy funkcja hello nadal działa.</span><span class="sxs-lookup"><span data-stu-id="d9635-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="d9635-123">Hello **szczegóły wywołania** raporty strony hello funkcji postępu (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość tooabort go.</span><span class="sxs-lookup"><span data-stu-id="d9635-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="d9635-125">Gdy funkcja hello zakończeniu hello **szczegóły wywołania** hello liczbę wierszy, zapisany raporty strony.</span><span class="sxs-lookup"><span data-stu-id="d9635-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Transfer danych przychodzących Zakończono — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="d9635-127">Jak tooread wiele jednostek z tabeli</span><span class="sxs-lookup"><span data-stu-id="d9635-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="d9635-128">tooread tabelę, użyj hello **tabeli** atrybutem **IQueryable<T>**  parametru wpisuje **T** pochodną **TableEntity**lub implementuje **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d9635-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="d9635-129">Witaj Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z hello **wejściowych** tabeli:</span><span class="sxs-lookup"><span data-stu-id="d9635-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="d9635-130">Jak tooread pojedyncza jednostka z tabeli</span><span class="sxs-lookup"><span data-stu-id="d9635-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="d9635-131">Brak **tabeli** konstruktora atrybutu z dwóch dodatkowych parametrów, które umożliwiają określenie hello klucz partycji i klucz wiersza, jeśli chcesz toobind tooa pojedynczej tabeli jednostki.</span><span class="sxs-lookup"><span data-stu-id="d9635-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="d9635-132">Witaj Poniższy przykładowy kod odczytuje wiersz tabeli **osoby** jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:</span><span class="sxs-lookup"><span data-stu-id="d9635-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="d9635-133">Witaj **osoby** klasy w tym przykładzie nie ma tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d9635-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="d9635-134">Jak toouse hello interfejsu API magazynu .NET bezpośrednio toowork z tabeli</span><span class="sxs-lookup"><span data-stu-id="d9635-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="d9635-135">Można również użyć hello **tabeli** atrybutem **CloudTable** obiektu dla większą elastyczność podczas pracy z tabelą.</span><span class="sxs-lookup"><span data-stu-id="d9635-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="d9635-136">Witaj poniższy kod używa próbki **CloudTable** obiekt tooadd toohello pojedynczej jednostki *wejściowych* tabeli.</span><span class="sxs-lookup"><span data-stu-id="d9635-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="d9635-137">Aby uzyskać więcej informacji na temat toouse hello **CloudTable** obiektów, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d9635-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="d9635-138">Tematy pokrewne objętych kolejek hello jak tooarticle</span><span class="sxs-lookup"><span data-stu-id="d9635-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="d9635-139">Uzyskać informacji na temat sposobu przetwarzania tabeli toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tootable przetwarzania, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (zadania WebJob projekty) ](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d9635-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9635-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9635-140">Next steps</span></span>
<span data-ttu-id="d9635-141">W tym artykule dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d9635-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="d9635-142">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d9635-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

