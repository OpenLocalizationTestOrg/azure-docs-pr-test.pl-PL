---
title: "ReliableConcurrentQueue w sieci szkieletowej usług Azure"
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
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="15348-103">Wprowadzenie do ReliableConcurrentQueue w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="15348-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="15348-104">Niezawodne równoczesnych kolejka jest asynchroniczne, transakcyjne i replikowane kolejki które concurrency wysokiej funkcji umieścić w kolejce i usuwania z kolejki operacji.</span><span class="sxs-lookup"><span data-stu-id="15348-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="15348-105">Został zaprojektowany w celu dostarczenia wysokiej przepływności i małe opóźnienia za mniejsze strict kolejności FIFO dostarczonych przez [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) i przekazuje optymalnych porządkowania.</span><span class="sxs-lookup"><span data-stu-id="15348-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="15348-106">Interfejsy API</span><span class="sxs-lookup"><span data-stu-id="15348-106">APIs</span></span>

|<span data-ttu-id="15348-107">Współbieżne kolejki</span><span class="sxs-lookup"><span data-stu-id="15348-107">Concurrent Queue</span></span>                |<span data-ttu-id="15348-108">Niezawodne równoczesnych kolejki</span><span class="sxs-lookup"><span data-stu-id="15348-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="15348-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="15348-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="15348-110">Zadanie EnqueueAsync (tx ITransaction elementu T)</span><span class="sxs-lookup"><span data-stu-id="15348-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="15348-111">wartość logiczna TryDequeue (out wynik T)</span><span class="sxs-lookup"><span data-stu-id="15348-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="15348-112">Zadanie < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="15348-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="15348-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="15348-113">int Count()</span></span>                    | <span data-ttu-id="15348-114">długie Count()</span><span class="sxs-lookup"><span data-stu-id="15348-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="15348-115">Porównanie z [niezawodnej kolejki](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="15348-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="15348-116">Niezawodne równoczesnych kolejki jest oferowany jako alternatywę do [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="15348-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="15348-117">Tej opcji należy używać w przypadku, gdy strict kolejności FIFO nie jest wymagane, jako gwarantujących FIFO wymaga zależnościami z współbieżności.</span><span class="sxs-lookup"><span data-stu-id="15348-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="15348-118">[Kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) używa blokad wymusić kolejności FIFO, co najwyżej jedna transakcja może umieścić w kolejce i możliwość usuwania z kolejki w czasie co najwyżej jedna transakcja.</span><span class="sxs-lookup"><span data-stu-id="15348-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="15348-119">Z kolei niezawodnej kolejki równoczesnych zwalnia ograniczenie porządkowania i umożliwia liczba równoczesnych transakcji interleave ich umieścić w kolejce do usuwania z kolejki operacji.</span><span class="sxs-lookup"><span data-stu-id="15348-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="15348-120">Porządkowanie optymalnych została podana, jednak względne uporządkowanie dwóch wartości w niezawodnej kolejki równoczesnych nigdy nie można zagwarantować.</span><span class="sxs-lookup"><span data-stu-id="15348-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="15348-121">Niezawodne kolejki równoczesnych zapewnia wyższą przepływność i mniejsze opóźnienia niż [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) zawsze, gdy istnieje wiele równoczesnych transakcji wykonywania enqueues i/lub dequeues.</span><span class="sxs-lookup"><span data-stu-id="15348-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="15348-122">Przypadek użycia próbki jest ReliableConcurrentQueue [kolejki komunikatów](https://en.wikipedia.org/wiki/Message_queue) scenariusza.</span><span class="sxs-lookup"><span data-stu-id="15348-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="15348-123">W tym scenariuszu jeden lub więcej komunikatów producentów tworzyć i Dodaj elementy do kolejki, a co najmniej jednego odbiorcy wiadomości ściągać komunikaty z kolejki i przetwarzanie ich.</span><span class="sxs-lookup"><span data-stu-id="15348-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="15348-124">Wiele producenci i konsumenci może pracować wielel osób, aby przetworzyć kolejki przy użyciu równoczesnych transakcji.</span><span class="sxs-lookup"><span data-stu-id="15348-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="15348-125">Wskazówki dotyczące użycia</span><span class="sxs-lookup"><span data-stu-id="15348-125">Usage Guidelines</span></span>
* <span data-ttu-id="15348-126">Kolejki oczekuje, że okres przechowywania mało elementów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="15348-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="15348-127">Oznacza to elementy nie może pozostać w kolejce przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="15348-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="15348-128">Kolejka nie gwarantuje kolejności FIFO strict.</span><span class="sxs-lookup"><span data-stu-id="15348-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="15348-129">Kolejka nie odczytuje własną zapisy.</span><span class="sxs-lookup"><span data-stu-id="15348-129">The queue does not read its own writes.</span></span> <span data-ttu-id="15348-130">Jeśli element jest dodawanych do kolejki w ramach transakcji, nie będą widoczne dla dequeuer w ramach tej samej transakcji.</span><span class="sxs-lookup"><span data-stu-id="15348-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="15348-131">Dequeues nie są od siebie odizolowane.</span><span class="sxs-lookup"><span data-stu-id="15348-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="15348-132">Jeśli element *A* jest usuniętej w transakcji *txnA*, nawet jeśli *txnA* nie została przekazana, element *A* nie będą widoczne dla równoczesne Transakcja *txnB*.</span><span class="sxs-lookup"><span data-stu-id="15348-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="15348-133">Jeśli *txnA* przerywa, *A* staną się widoczne dla *txnB* natychmiast.</span><span class="sxs-lookup"><span data-stu-id="15348-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="15348-134">*TryPeekAsync* zachowanie można zaimplementować przy użyciu *TryDequeueAsync* i Trwa przerywanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="15348-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="15348-135">Na przykład można znaleźć w sekcji wzorce programowania.</span><span class="sxs-lookup"><span data-stu-id="15348-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="15348-136">Liczba jest nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="15348-136">Count is non-transactional.</span></span> <span data-ttu-id="15348-137">Może służyć do poznać liczbę elementów w kolejce, ale reprezentuje punkt w czasie i nie może opierać się.</span><span class="sxs-lookup"><span data-stu-id="15348-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="15348-138">Nie ma zostać wykonane przetwarzanie kosztowne dequeued elementów, gdy transakcja jest aktywna, aby uniknąć długotrwałe transakcje, które mogą mieć wpływ na wydajność systemu.</span><span class="sxs-lookup"><span data-stu-id="15348-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="15348-139">Wstawki kodu</span><span class="sxs-lookup"><span data-stu-id="15348-139">Code Snippets</span></span>
<span data-ttu-id="15348-140">Daj nam przyjrzeć się kilka fragmentów kodu i ich oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="15348-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="15348-141">Obsługa wyjątków jest ignorowany w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="15348-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="15348-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="15348-142">EnqueueAsync</span></span>
<span data-ttu-id="15348-143">Poniżej przedstawiono kilka fragmenty kodu przy użyciu EnqueueAsync następuje ich oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="15348-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="15348-144">*Przypadek 1: Pojedynczy umieścić w kolejce zadań*</span><span class="sxs-lookup"><span data-stu-id="15348-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="15348-145">Załóżmy, że zadanie zostało pomyślnie zakończone i czy nie zostały żadne transakcje równoczesnych modyfikowanie kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="15348-146">Użytkownika można oczekiwać w kolejce zawierać elementów w jednym z następujących zleceń:</span><span class="sxs-lookup"><span data-stu-id="15348-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="15348-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="15348-147">10, 20</span></span>

> <span data-ttu-id="15348-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="15348-148">20, 10</span></span>


- <span data-ttu-id="15348-149">*Przypadek 2: Równoległe umieścić w kolejce zadań*</span><span class="sxs-lookup"><span data-stu-id="15348-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="15348-150">Załóżmy, czy zadania zakończyła się pomyślnie, że zadania uruchomione równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="15348-151">Brak wnioskowania nie jest możliwe o kolejności elementów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="15348-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="15348-152">Na poniższym przykładzie elementów może występować w żadnym z 4!</span><span class="sxs-lookup"><span data-stu-id="15348-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="15348-153">możliwe uporządkowania.</span><span class="sxs-lookup"><span data-stu-id="15348-153">possible orderings.</span></span>  <span data-ttu-id="15348-154">Kolejka będzie próbował zachować elementy w kolejności (umieszczonych w kolejce), ale można wymusić ponownie określić ich kolejność z powodu równoczesnych operacji lub błędów.</span><span class="sxs-lookup"><span data-stu-id="15348-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="15348-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="15348-155">DequeueAsync</span></span>
<span data-ttu-id="15348-156">Poniżej przedstawiono kilka fragmenty kodu przy użyciu TryDequeueAsync następuje oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="15348-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="15348-157">Załóżmy, że kolejka jest już wypełniony następujących elementów w kolejce:</span><span class="sxs-lookup"><span data-stu-id="15348-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="15348-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="15348-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="15348-159">*Przypadek 1: Jednym usuwania z kolejki zadań*</span><span class="sxs-lookup"><span data-stu-id="15348-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="15348-160">Załóżmy, że zadanie zostało pomyślnie zakończone i czy nie zostały żadne transakcje równoczesnych modyfikowanie kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="15348-161">Ponieważ żadne wnioskowania nie jest możliwe o kolejności elementów w kolejce, wszystkie trzy elementy może być usunięty z kolejki, w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="15348-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="15348-162">Kolejka będzie próbował zachować elementy w kolejności (umieszczonych w kolejce), ale można wymusić ponownie określić ich kolejność z powodu równoczesnych operacji lub błędów.</span><span class="sxs-lookup"><span data-stu-id="15348-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="15348-163">*Przypadek 2: Dequeue równoległych zadań*</span><span class="sxs-lookup"><span data-stu-id="15348-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="15348-164">Załóżmy, czy zadania zakończyła się pomyślnie, że zadania uruchomione równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="15348-165">Ponieważ żadne wnioskowania nie jest możliwe o kolejności elementów w kolejce listy *dequeue1* i *dequeue2* każdy będzie zawierać dwa elementy, w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="15348-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="15348-166">Taki sam element zostanie *nie* są wyświetlane na listach obu.</span><span class="sxs-lookup"><span data-stu-id="15348-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="15348-167">W związku z tym jeśli dequeue1 *10*, *30*, następnie byłyby dequeue2 *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="15348-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="15348-168">*Przypadek 3: Usuwania z kolejki w kolejności z przerwać transakcji*</span><span class="sxs-lookup"><span data-stu-id="15348-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="15348-169">Przerywanie transakcji z locie dequeues naraża elementy z powrotem na head kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="15348-170">Kolejność, w której elementy są odłożyć na head kolejki nie jest gwarantowana.</span><span class="sxs-lookup"><span data-stu-id="15348-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="15348-171">Daj nam przyjrzeć się następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="15348-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="15348-172">Załóżmy, że elementy zostały usuniętej w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="15348-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="15348-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="15348-173">10, 20</span></span>

<span data-ttu-id="15348-174">Gdy firma Microsoft przerwać transakcji, elementy zostanie dodany do head kolejki w jednym z następujących zleceń:</span><span class="sxs-lookup"><span data-stu-id="15348-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="15348-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="15348-175">10, 20</span></span>

> <span data-ttu-id="15348-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="15348-176">20, 10</span></span>

<span data-ttu-id="15348-177">To samo dotyczy wszystkich przypadkach, gdy transakcja nie została pomyślnie *zatwierdzone*.</span><span class="sxs-lookup"><span data-stu-id="15348-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="15348-178">Wzorce programowania</span><span class="sxs-lookup"><span data-stu-id="15348-178">Programming Patterns</span></span>
<span data-ttu-id="15348-179">W tej sekcji Sprawdź Daj nam kilka programowania w języku wzorców, które mogą być przydatne przy użyciu ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="15348-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="15348-180">Dequeues partii</span><span class="sxs-lookup"><span data-stu-id="15348-180">Batch Dequeues</span></span>
<span data-ttu-id="15348-181">A zalecane jest wzorzec programowania dla konsumentów zadania wsadowego jego dequeues zamiast wykonaj jedną usuwania z kolejki w czasie.</span><span class="sxs-lookup"><span data-stu-id="15348-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="15348-182">Użytkownik może wybrać ograniczać opóźnienia między każdej partii lub rozmiar partii.</span><span class="sxs-lookup"><span data-stu-id="15348-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="15348-183">Poniższy fragment kodu przedstawia ten model programowania.</span><span class="sxs-lookup"><span data-stu-id="15348-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="15348-184">Należy pamiętać, że w tym przykładzie przetwarzanie odbywa się po transakcja została zatwierdzona, tak jakby był błąd występuje podczas przetwarzania, nieprzetworzone elementy zostaną utracone bez przetworzeniu.</span><span class="sxs-lookup"><span data-stu-id="15348-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="15348-185">Alternatywnie przetwarzanie może odbywać się w zakresie transakcji, jednak to może mieć negatywny wpływ na wydajność i wymaga obsługi elementów już przetworzone.</span><span class="sxs-lookup"><span data-stu-id="15348-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="15348-186">Przetwarzanie powiadomień na podstawie optymalnych</span><span class="sxs-lookup"><span data-stu-id="15348-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="15348-187">Inny interesujące wzorzec programowania używa interfejsu API Count.</span><span class="sxs-lookup"><span data-stu-id="15348-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="15348-188">W tym miejscu możemy wdrożyć optymalnych powiadomień na podstawie przetwarzania dla kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="15348-189">Kolejki licznik może służyć do ograniczania umieścić w kolejce "lub" task kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="15348-190">Należy pamiętać, że co w poprzednim przykładzie, ponieważ przetwarzanie zachodzi poza transakcją, nieprzetworzone elementy mogą zostać utracone jeśli wystąpi błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="15348-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="15348-191">Optymalny opróżniania</span><span class="sxs-lookup"><span data-stu-id="15348-191">Best-Effort Drain</span></span>
<span data-ttu-id="15348-192">Nie można zagwarantować opróżniania kolejki z powodu równoczesnych charakter struktury danych.</span><span class="sxs-lookup"><span data-stu-id="15348-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="15348-193">Jest to możliwe, że nawet jeśli nie ma operacji użytkownika w kolejce znajdują się aktywny, określonego wywołania TryDequeueAsync nie może zwracać element, który został wcześniej umieszczonych w kolejce i zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="15348-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="15348-194">Jest gwarantowane elementu umieszczonych w kolejce *ostatecznie* stają się widoczne do usuwania z kolejki, bez mechanizm komunikacji poza pasmem konsumenta niezależne nie wiedzieć, że kolejka została osiągnięta nawet jeśli stan wszystkich producentów zostały zatrzymane, a nie nowy umieścić operacje są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="15348-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="15348-195">W związku z tym Operacja opróżniania jest optymalnych zgodnie z implementacją poniżej.</span><span class="sxs-lookup"><span data-stu-id="15348-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="15348-196">Użytkownik należy zatrzymać wszystkie dalsze producentów i zadania odbiorców i poczekaj, aż locie transakcji do zatwierdzenia lub przerwania, przed podjęciem próby opróżnienia kolejki.</span><span class="sxs-lookup"><span data-stu-id="15348-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="15348-197">Jeśli użytkownik zna oczekiwana liczba elementów w kolejce, można skonfigurować powiadomienia, która sygnalizuje, że wszystkie elementy zostały usuniętej.</span><span class="sxs-lookup"><span data-stu-id="15348-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="15348-198">Peek</span><span class="sxs-lookup"><span data-stu-id="15348-198">Peek</span></span>
<span data-ttu-id="15348-199">Nie ma ReliableConcurrentQueue *TryPeekAsync* interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="15348-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="15348-200">Użytkownicy mogą uzyskać wglądu semantycznych przy użyciu *TryDequeueAsync* i Trwa przerywanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="15348-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="15348-201">W tym przykładzie dequeues są przetwarzane tylko wtedy, gdy wartość elementu jest większa niż *10*.</span><span class="sxs-lookup"><span data-stu-id="15348-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
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

## <a name="must-read"></a><span data-ttu-id="15348-202">Należy odczytać</span><span class="sxs-lookup"><span data-stu-id="15348-202">Must Read</span></span>
* [<span data-ttu-id="15348-203">Niezawodne usługi Szybki Start</span><span class="sxs-lookup"><span data-stu-id="15348-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="15348-204">Praca z elementami Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="15348-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="15348-205">Niezawodne usługi powiadomień</span><span class="sxs-lookup"><span data-stu-id="15348-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="15348-206">Niezawodne usługi tworzenia kopii zapasowej i przywracania (odzyskiwania po awarii)</span><span class="sxs-lookup"><span data-stu-id="15348-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="15348-207">Niezawodne stanu Menedżera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="15348-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="15348-208">Wprowadzenie do usług interfejsu API sieci Web sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="15348-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="15348-209">Zaawansowanego wykorzystania niezawodnej Model programowania usług</span><span class="sxs-lookup"><span data-stu-id="15348-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="15348-210">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="15348-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
