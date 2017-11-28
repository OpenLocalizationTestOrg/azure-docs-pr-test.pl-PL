---
title: "aaaReliableConcurrentQueue w sieci szkieletowej usług Azure"
description: "ReliableConcurrentQueue jest kolejką wysokiej przepustowości, co umożliwia równoległe enqueues i dequeues."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="14687-103">Wprowadzenie tooReliableConcurrentQueue w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="14687-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="14687-104">Niezawodne równoczesnych kolejka jest asynchroniczne, transakcyjne i replikowane kolejki które concurrency wysokiej funkcji umieścić w kolejce i usuwania z kolejki operacji.</span><span class="sxs-lookup"><span data-stu-id="14687-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="14687-105">Jest zaprojektowana toodeliver wysokiej przepływności i małe opóźnienia przez złagodzeniu hello strict FIFO porządkowanie udostępniane przez [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) i przekazuje optymalnych porządkowania.</span><span class="sxs-lookup"><span data-stu-id="14687-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="14687-106">Interfejsy API</span><span class="sxs-lookup"><span data-stu-id="14687-106">APIs</span></span>

|<span data-ttu-id="14687-107">Współbieżne kolejki</span><span class="sxs-lookup"><span data-stu-id="14687-107">Concurrent Queue</span></span>                |<span data-ttu-id="14687-108">Niezawodne równoczesnych kolejki</span><span class="sxs-lookup"><span data-stu-id="14687-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="14687-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="14687-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="14687-110">Zadanie EnqueueAsync (tx ITransaction elementu T)</span><span class="sxs-lookup"><span data-stu-id="14687-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="14687-111">wartość logiczna TryDequeue (out wynik T)</span><span class="sxs-lookup"><span data-stu-id="14687-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="14687-112">Zadanie < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="14687-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="14687-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="14687-113">int Count()</span></span>                    | <span data-ttu-id="14687-114">długie Count()</span><span class="sxs-lookup"><span data-stu-id="14687-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="14687-115">Porównanie z [niezawodnej kolejki](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="14687-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="14687-116">Niezawodne równoczesnych kolejki jest oferowany jako alternatywę zbyt[kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="14687-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="14687-117">Tej opcji należy używać w przypadku, gdy strict kolejności FIFO nie jest wymagane, jako gwarantujących FIFO wymaga zależnościami z współbieżności.</span><span class="sxs-lookup"><span data-stu-id="14687-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="14687-118">[Kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) używa blokad tooenforce FIFO kolejności, o co najwyżej jedna transakcja dozwolone tooenqueue i najwyżej jedna transakcja w danym momencie dozwolona toodequeue.</span><span class="sxs-lookup"><span data-stu-id="14687-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="14687-119">W porównaniu niezawodnej kolejki równoczesnych zwalnia hello porządkowanie ograniczenia i umożliwia żadnych liczba równoczesnych transakcji toointerleave ich umieścić w kolejce i usuwania z kolejki operacji.</span><span class="sxs-lookup"><span data-stu-id="14687-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="14687-120">Porządkowanie optymalnych została podana, jednak hello względne uporządkowanie dwóch wartości w niezawodnej kolejki równoczesnych nigdy nie można zagwarantować.</span><span class="sxs-lookup"><span data-stu-id="14687-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="14687-121">Niezawodne kolejki równoczesnych zapewnia wyższą przepływność i mniejsze opóźnienia niż [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) zawsze, gdy istnieje wiele równoczesnych transakcji wykonywania enqueues i/lub dequeues.</span><span class="sxs-lookup"><span data-stu-id="14687-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="14687-122">Przypadek użycia próbkę hello ReliableConcurrentQueue jest hello [kolejki komunikatów](https://en.wikipedia.org/wiki/Message_queue) scenariusza.</span><span class="sxs-lookup"><span data-stu-id="14687-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="14687-123">W tym scenariuszu jeden lub więcej komunikatów producentów Utwórz i Dodaj elementy toohello kolejki, a co najmniej jednego odbiorcy wiadomości ściągać komunikaty z kolejki hello i ich przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="14687-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="14687-124">Wiele producenci i konsumenci może pracować wielel osób, w kolejności tooprocess hello kolejki przy użyciu równoczesnych transakcji.</span><span class="sxs-lookup"><span data-stu-id="14687-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="14687-125">Wskazówki dotyczące użycia</span><span class="sxs-lookup"><span data-stu-id="14687-125">Usage Guidelines</span></span>
* <span data-ttu-id="14687-126">kolejki Hello oczekuje, że hello elementów w kolejce hello mają okres przechowywania niski.</span><span class="sxs-lookup"><span data-stu-id="14687-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="14687-127">Oznacza to, że elementy hello nie będzie pozostają w kolejce hello przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="14687-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="14687-128">kolejki Hello nie gwarantuje kolejności FIFO strict.</span><span class="sxs-lookup"><span data-stu-id="14687-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="14687-129">kolejki Hello nie odczytuje własną zapisów.</span><span class="sxs-lookup"><span data-stu-id="14687-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="14687-130">Jeśli element jest dodawanych do kolejki w ramach transakcji, nie będzie widoczne tooa dequeuer w hello tej samej transakcji.</span><span class="sxs-lookup"><span data-stu-id="14687-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="14687-131">Dequeues nie są od siebie odizolowane.</span><span class="sxs-lookup"><span data-stu-id="14687-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="14687-132">Jeśli element *A* jest usuniętej w transakcji *txnA*, nawet jeśli *txnA* nie została przekazana, element *A* nie będą widoczne tooa jednoczesnych Transakcja *txnB*.</span><span class="sxs-lookup"><span data-stu-id="14687-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="14687-133">Jeśli *txnA* przerywa, *A* stają się widoczne zbyt*txnB* natychmiast.</span><span class="sxs-lookup"><span data-stu-id="14687-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="14687-134">*TryPeekAsync* zachowanie można zaimplementować przy użyciu *TryDequeueAsync* , a następnie Przerywanie transakcji hello.</span><span class="sxs-lookup"><span data-stu-id="14687-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="14687-135">Na przykład można znaleźć w sekcji wzorce programowania hello.</span><span class="sxs-lookup"><span data-stu-id="14687-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="14687-136">Liczba jest nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="14687-136">Count is non-transactional.</span></span> <span data-ttu-id="14687-137">Może być używane tooget pomysł hello liczba elementów w kolejce hello, ale reprezentuje punkt w czasie i nie może opierać się.</span><span class="sxs-lookup"><span data-stu-id="14687-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="14687-138">Kosztowna przetwarzania na powitania usuniętej elementy nie powinny być wykonywane podczas hello transakcji jest aktywny, tooavoid długotrwałe transakcje, które mogą mieć negatywny wpływ na wydajność w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="14687-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="14687-139">Wstawki kodu</span><span class="sxs-lookup"><span data-stu-id="14687-139">Code Snippets</span></span>
<span data-ttu-id="14687-140">Daj nam przyjrzeć się kilka fragmentów kodu i ich oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="14687-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="14687-141">Obsługa wyjątków jest ignorowany w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="14687-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="14687-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="14687-142">EnqueueAsync</span></span>
<span data-ttu-id="14687-143">Poniżej przedstawiono kilka fragmenty kodu przy użyciu EnqueueAsync następuje ich oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="14687-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="14687-144">*Przypadek 1: Pojedynczy umieścić w kolejce zadań*</span><span class="sxs-lookup"><span data-stu-id="14687-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="14687-145">Siebie to zadanie hello zakończyła się pomyślnie, a które nie było żadnych równoczesnych transakcji modyfikowanie hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="14687-146">Witaj użytkownik może spodziewać się hello kolejki toocontain hello elementów w żadnym hello następujących zleceń:</span><span class="sxs-lookup"><span data-stu-id="14687-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="14687-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="14687-147">10, 20</span></span>

> <span data-ttu-id="14687-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="14687-148">20, 10</span></span>


- <span data-ttu-id="14687-149">*Przypadek 2: Równoległe umieścić w kolejce zadań*</span><span class="sxs-lookup"><span data-stu-id="14687-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="14687-150">Załóżmy, czy zadania hello zakończyła się pomyślnie, czy zadania hello uruchomiło równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="14687-151">Brak wnioskowania nie jest możliwe o hello kolejność elementów w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="14687-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="14687-152">Na poniższym przykładzie hello elementy są w żadnym hello 4!</span><span class="sxs-lookup"><span data-stu-id="14687-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="14687-153">możliwe uporządkowania.</span><span class="sxs-lookup"><span data-stu-id="14687-153">possible orderings.</span></span>  <span data-ttu-id="14687-154">kolejki Hello podejmie elementów hello tookeep hello oryginalnego zamówienia (umieszczonych w kolejce), ale może być wymuszone tooreorder ich ukończenia operacji tooconcurrent lub błędów.</span><span class="sxs-lookup"><span data-stu-id="14687-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="14687-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="14687-155">DequeueAsync</span></span>
<span data-ttu-id="14687-156">Poniżej przedstawiono kilka fragmenty kodu przy użyciu TryDequeueAsync następuje hello oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="14687-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="14687-157">Przyjęto założenie, że tej kolejki hello jest już wypełniony hello następujących elementów w kolejce hello:</span><span class="sxs-lookup"><span data-stu-id="14687-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="14687-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="14687-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="14687-159">*Przypadek 1: Jednym usuwania z kolejki zadań*</span><span class="sxs-lookup"><span data-stu-id="14687-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="14687-160">Siebie to zadanie hello zakończyła się pomyślnie, a które nie było żadnych równoczesnych transakcji modyfikowanie hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="14687-161">Ponieważ żadne wnioskowania nie jest możliwe o zamówieniu hello hello elementów w kolejce hello, wszystkie trzy elementy hello może być usunięty z kolejki, w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="14687-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="14687-162">kolejki Hello podejmie elementów hello tookeep hello oryginalnego zamówienia (umieszczonych w kolejce), ale może być wymuszone tooreorder ich ukończenia operacji tooconcurrent lub błędów.</span><span class="sxs-lookup"><span data-stu-id="14687-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="14687-163">*Przypadek 2: Dequeue równoległych zadań*</span><span class="sxs-lookup"><span data-stu-id="14687-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="14687-164">Załóżmy, czy zadania hello zakończyła się pomyślnie, czy zadania hello uruchomiło równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="14687-165">Ponieważ żadne wnioskowania nie jest możliwe o zamówieniu hello hello elementów w kolejce hello, hello list *dequeue1* i *dequeue2* każdy będzie zawierać dwa elementy, w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="14687-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="14687-166">Hello będzie tym samym elemencie *nie* są wyświetlane na listach obu.</span><span class="sxs-lookup"><span data-stu-id="14687-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="14687-167">W związku z tym jeśli dequeue1 *10*, *30*, następnie byłyby dequeue2 *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="14687-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="14687-168">*Przypadek 3: Usuwania z kolejki w kolejności z przerwać transakcji*</span><span class="sxs-lookup"><span data-stu-id="14687-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="14687-169">Przerywanie transakcji z locie dequeues naraża hello elementy z powrotem na powitania head hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="14687-170">kolejność Hello, w którym elementy hello są odłożyć na powitania head hello kolejki nie jest gwarantowana.</span><span class="sxs-lookup"><span data-stu-id="14687-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="14687-171">Daj nam przyjrzeć się hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="14687-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="14687-172">Załóżmy, że elementy hello zostały usuniętej w następującej kolejności hello:</span><span class="sxs-lookup"><span data-stu-id="14687-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="14687-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="14687-173">10, 20</span></span>

<span data-ttu-id="14687-174">Gdy firma Microsoft przerwać transakcji hello, elementy hello zostanie dodany head wstecz toohello kolejki hello w żadnym hello następujących zleceń:</span><span class="sxs-lookup"><span data-stu-id="14687-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="14687-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="14687-175">10, 20</span></span>

> <span data-ttu-id="14687-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="14687-176">20, 10</span></span>

<span data-ttu-id="14687-177">Witaj dotyczy to wszystkich przypadkach, gdy hello transakcja nie została pomyślnie *zatwierdzone*.</span><span class="sxs-lookup"><span data-stu-id="14687-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="14687-178">Wzorce programowania</span><span class="sxs-lookup"><span data-stu-id="14687-178">Programming Patterns</span></span>
<span data-ttu-id="14687-179">W tej sekcji Sprawdź Daj nam kilka programowania w języku wzorców, które mogą być przydatne przy użyciu ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="14687-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="14687-180">Dequeues partii</span><span class="sxs-lookup"><span data-stu-id="14687-180">Batch Dequeues</span></span>
<span data-ttu-id="14687-181">A zalecane programowania wzorzec jest na powitania klienta zadań toobatch jego dequeues zamiast wykonaj jedną usuwania z kolejki w czasie.</span><span class="sxs-lookup"><span data-stu-id="14687-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="14687-182">Witaj, użytkownik może wybrać toothrottle opóźnienia między każdej partii lub hello rozmiar partii.</span><span class="sxs-lookup"><span data-stu-id="14687-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="14687-183">Witaj poniższy fragment kodu przedstawia ten model programowania.</span><span class="sxs-lookup"><span data-stu-id="14687-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="14687-184">Należy pamiętać, że w tym przykładzie hello przetwarzania odbywa się po dba hello transakcji, jeśli błąd był toooccur podczas przetwarzania, hello nieprzetworzone elementy zostaną utracone bez przetworzeniu.</span><span class="sxs-lookup"><span data-stu-id="14687-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="14687-185">Alternatywnie przetwarzania hello może odbywać się w zakresie transakcji hello, jednak to może mieć negatywny wpływ na wydajność i wymaga obsługi elementów hello przetworzone.</span><span class="sxs-lookup"><span data-stu-id="14687-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="14687-186">Przetwarzanie powiadomień na podstawie optymalnych</span><span class="sxs-lookup"><span data-stu-id="14687-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="14687-187">Inny interesujące wzorzec programowania używa hello liczba interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="14687-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="14687-188">W tym miejscu możemy wdrożyć optymalnych powiadomień na podstawie przetwarzania hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="14687-189">kolejki Hello liczba może być toothrottle używane jako umieścić w kolejce "lub" task kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="14687-190">Należy pamiętać, że jak w poprzednim przykładzie hello, ponieważ przetwarzanie hello odbywa się poza transakcji hello nieprzetworzone elementy mogą zostać utracone jeśli wystąpi błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="14687-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="14687-191">Optymalny opróżniania</span><span class="sxs-lookup"><span data-stu-id="14687-191">Best-Effort Drain</span></span>
<span data-ttu-id="14687-192">Nie można zagwarantować opróżniania kolejki hello powodu toohello równoczesnych rodzaj hello struktury danych.</span><span class="sxs-lookup"><span data-stu-id="14687-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="14687-193">Jest to możliwe, że nawet jeśli nie ma operacji użytkownika w kolejce hello jest aktywny, tooTryDequeueAsync rozmowy określonym nie może zwracać element, który został wcześniej umieszczonych w kolejce i zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="14687-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="14687-194">Element umieszczonych w kolejce Hello jest gwarantowana zbyt*ostatecznie* stają się widoczne toodequeue, jednak bez mechanizm komunikacji poza pasmem konsumenta niezależne nie może znać tej kolejki hello osiągnęła nawet jeśli stan wszystkich Producenci została zatrzymana, a nie ma nowych umieścić w kolejce operacji jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="14687-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="14687-195">W związku z tym Operacja opróżniania hello jest optymalnych zgodnie z implementacją poniżej.</span><span class="sxs-lookup"><span data-stu-id="14687-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="14687-196">Hello użytkownika należy zatrzymać dalsze producentów i zadania odbiorców i poczekaj, aż wszystkie transakcje locie toocommit lub Przerwij, przed podjęciem próby wykonania toodrain hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="14687-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="14687-197">Jeśli użytkownik hello zna hello oczekiwana liczba elementów w kolejce hello, można skonfigurować powiadomienia, która sygnalizuje, że wszystkie elementy zostały usuniętej.</span><span class="sxs-lookup"><span data-stu-id="14687-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="14687-198">Peek</span><span class="sxs-lookup"><span data-stu-id="14687-198">Peek</span></span>
<span data-ttu-id="14687-199">ReliableConcurrentQueue nie zapewnia hello *TryPeekAsync* interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="14687-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="14687-200">Użytkownicy mogą uzyskać wglądu hello semantycznych przy użyciu *TryDequeueAsync* , a następnie Przerywanie transakcji hello.</span><span class="sxs-lookup"><span data-stu-id="14687-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="14687-201">W tym przykładzie dequeues są przetwarzane tylko wtedy, gdy jest większa niż wartość elementu hello *10*.</span><span class="sxs-lookup"><span data-stu-id="14687-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="14687-202">Należy odczytać</span><span class="sxs-lookup"><span data-stu-id="14687-202">Must Read</span></span>
* [<span data-ttu-id="14687-203">Niezawodne usługi Szybki Start</span><span class="sxs-lookup"><span data-stu-id="14687-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="14687-204">Praca z elementami Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="14687-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="14687-205">Niezawodne usługi powiadomień</span><span class="sxs-lookup"><span data-stu-id="14687-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="14687-206">Niezawodne usługi tworzenia kopii zapasowej i przywracania (odzyskiwania po awarii)</span><span class="sxs-lookup"><span data-stu-id="14687-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="14687-207">Niezawodne stanu Menedżera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="14687-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="14687-208">Wprowadzenie do usług interfejsu API sieci Web sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="14687-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="14687-209">Zaawansowanego wykorzystania hello niezawodnej modelu programowania usług</span><span class="sxs-lookup"><span data-stu-id="14687-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="14687-210">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="14687-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
