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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Wprowadzenie tooReliableConcurrentQueue w sieci szkieletowej usług Azure
Niezawodne równoczesnych kolejka jest asynchroniczne, transakcyjne i replikowane kolejki które concurrency wysokiej funkcji umieścić w kolejce i usuwania z kolejki operacji. Jest zaprojektowana toodeliver wysokiej przepływności i małe opóźnienia przez złagodzeniu hello strict FIFO porządkowanie udostępniane przez [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) i przekazuje optymalnych porządkowania.

## <a name="apis"></a>Interfejsy API

|Współbieżne kolejki                |Niezawodne równoczesnych kolejki                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Zadanie EnqueueAsync (tx ITransaction elementu T)                       |
| wartość logiczna TryDequeue (out wynik T)  | Zadanie < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)  |
| int Count()                    | długie Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Porównanie z [niezawodnej kolejki](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Niezawodne równoczesnych kolejki jest oferowany jako alternatywę zbyt[kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx). Tej opcji należy używać w przypadku, gdy strict kolejności FIFO nie jest wymagane, jako gwarantujących FIFO wymaga zależnościami z współbieżności.  [Kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) używa blokad tooenforce FIFO kolejności, o co najwyżej jedna transakcja dozwolone tooenqueue i najwyżej jedna transakcja w danym momencie dozwolona toodequeue. W porównaniu niezawodnej kolejki równoczesnych zwalnia hello porządkowanie ograniczenia i umożliwia żadnych liczba równoczesnych transakcji toointerleave ich umieścić w kolejce i usuwania z kolejki operacji. Porządkowanie optymalnych została podana, jednak hello względne uporządkowanie dwóch wartości w niezawodnej kolejki równoczesnych nigdy nie można zagwarantować.

Niezawodne kolejki równoczesnych zapewnia wyższą przepływność i mniejsze opóźnienia niż [kolejka niezawodnych](https://msdn.microsoft.com/library/azure/dn971527.aspx) zawsze, gdy istnieje wiele równoczesnych transakcji wykonywania enqueues i/lub dequeues.

Przypadek użycia próbkę hello ReliableConcurrentQueue jest hello [kolejki komunikatów](https://en.wikipedia.org/wiki/Message_queue) scenariusza. W tym scenariuszu jeden lub więcej komunikatów producentów Utwórz i Dodaj elementy toohello kolejki, a co najmniej jednego odbiorcy wiadomości ściągać komunikaty z kolejki hello i ich przetworzenia. Wiele producenci i konsumenci może pracować wielel osób, w kolejności tooprocess hello kolejki przy użyciu równoczesnych transakcji.

## <a name="usage-guidelines"></a>Wskazówki dotyczące użycia
* kolejki Hello oczekuje, że hello elementów w kolejce hello mają okres przechowywania niski. Oznacza to, że elementy hello nie będzie pozostają w kolejce hello przez długi czas.
* kolejki Hello nie gwarantuje kolejności FIFO strict.
* kolejki Hello nie odczytuje własną zapisów. Jeśli element jest dodawanych do kolejki w ramach transakcji, nie będzie widoczne tooa dequeuer w hello tej samej transakcji.
* Dequeues nie są od siebie odizolowane. Jeśli element *A* jest usuniętej w transakcji *txnA*, nawet jeśli *txnA* nie została przekazana, element *A* nie będą widoczne tooa jednoczesnych Transakcja *txnB*.  Jeśli *txnA* przerywa, *A* stają się widoczne zbyt*txnB* natychmiast.
* *TryPeekAsync* zachowanie można zaimplementować przy użyciu *TryDequeueAsync* , a następnie Przerywanie transakcji hello. Na przykład można znaleźć w sekcji wzorce programowania hello.
* Liczba jest nietransakcyjnej. Może być używane tooget pomysł hello liczba elementów w kolejce hello, ale reprezentuje punkt w czasie i nie może opierać się.
* Kosztowna przetwarzania na powitania usuniętej elementy nie powinny być wykonywane podczas hello transakcji jest aktywny, tooavoid długotrwałe transakcje, które mogą mieć negatywny wpływ na wydajność w systemie hello.

## <a name="code-snippets"></a>Wstawki kodu
Daj nam przyjrzeć się kilka fragmentów kodu i ich oczekiwane dane wyjściowe. Obsługa wyjątków jest ignorowany w tej sekcji.

### <a name="enqueueasync"></a>EnqueueAsync
Poniżej przedstawiono kilka fragmenty kodu przy użyciu EnqueueAsync następuje ich oczekiwane dane wyjściowe.

- *Przypadek 1: Pojedynczy umieścić w kolejce zadań*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Siebie to zadanie hello zakończyła się pomyślnie, a które nie było żadnych równoczesnych transakcji modyfikowanie hello kolejki. Witaj użytkownik może spodziewać się hello kolejki toocontain hello elementów w żadnym hello następujących zleceń:

> 10, 20

> 20, 10


- *Przypadek 2: Równoległe umieścić w kolejce zadań*

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

Załóżmy, czy zadania hello zakończyła się pomyślnie, czy zadania hello uruchomiło równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie hello kolejki. Brak wnioskowania nie jest możliwe o hello kolejność elementów w kolejce hello. Na poniższym przykładzie hello elementy są w żadnym hello 4! możliwe uporządkowania.  kolejki Hello podejmie elementów hello tookeep hello oryginalnego zamówienia (umieszczonych w kolejce), ale może być wymuszone tooreorder ich ukończenia operacji tooconcurrent lub błędów.


### <a name="dequeueasync"></a>DequeueAsync
Poniżej przedstawiono kilka fragmenty kodu przy użyciu TryDequeueAsync następuje hello oczekiwane dane wyjściowe. Przyjęto założenie, że tej kolejki hello jest już wypełniony hello następujących elementów w kolejce hello:
> 10, 20, 30, 40, 50, 60

- *Przypadek 1: Jednym usuwania z kolejki zadań*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Siebie to zadanie hello zakończyła się pomyślnie, a które nie było żadnych równoczesnych transakcji modyfikowanie hello kolejki. Ponieważ żadne wnioskowania nie jest możliwe o zamówieniu hello hello elementów w kolejce hello, wszystkie trzy elementy hello może być usunięty z kolejki, w dowolnej kolejności. kolejki Hello podejmie elementów hello tookeep hello oryginalnego zamówienia (umieszczonych w kolejce), ale może być wymuszone tooreorder ich ukończenia operacji tooconcurrent lub błędów.  

- *Przypadek 2: Dequeue równoległych zadań*

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

Załóżmy, czy zadania hello zakończyła się pomyślnie, czy zadania hello uruchomiło równolegle i że nie wystąpiły żadne inne transakcje równoczesnych modyfikowanie hello kolejki. Ponieważ żadne wnioskowania nie jest możliwe o zamówieniu hello hello elementów w kolejce hello, hello list *dequeue1* i *dequeue2* każdy będzie zawierać dwa elementy, w dowolnej kolejności.

Hello będzie tym samym elemencie *nie* są wyświetlane na listach obu. W związku z tym jeśli dequeue1 *10*, *30*, następnie byłyby dequeue2 *20*, *40*.

- *Przypadek 3: Usuwania z kolejki w kolejności z przerwać transakcji*

Przerywanie transakcji z locie dequeues naraża hello elementy z powrotem na powitania head hello kolejki. kolejność Hello, w którym elementy hello są odłożyć na powitania head hello kolejki nie jest gwarantowana. Daj nam przyjrzeć się hello następującego kodu:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Załóżmy, że elementy hello zostały usuniętej w następującej kolejności hello:
> 10, 20

Gdy firma Microsoft przerwać transakcji hello, elementy hello zostanie dodany head wstecz toohello kolejki hello w żadnym hello następujących zleceń:
> 10, 20

> 20, 10

Witaj dotyczy to wszystkich przypadkach, gdy hello transakcja nie została pomyślnie *zatwierdzone*.

## <a name="programming-patterns"></a>Wzorce programowania
W tej sekcji Sprawdź Daj nam kilka programowania w języku wzorców, które mogą być przydatne przy użyciu ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Dequeues partii
A zalecane programowania wzorzec jest na powitania klienta zadań toobatch jego dequeues zamiast wykonaj jedną usuwania z kolejki w czasie. Witaj, użytkownik może wybrać toothrottle opóźnienia między każdej partii lub hello rozmiar partii. Witaj poniższy fragment kodu przedstawia ten model programowania.  Należy pamiętać, że w tym przykładzie hello przetwarzania odbywa się po dba hello transakcji, jeśli błąd był toooccur podczas przetwarzania, hello nieprzetworzone elementy zostaną utracone bez przetworzeniu.  Alternatywnie przetwarzania hello może odbywać się w zakresie transakcji hello, jednak to może mieć negatywny wpływ na wydajność i wymaga obsługi elementów hello przetworzone.

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

### <a name="best-effort-notification-based-processing"></a>Przetwarzanie powiadomień na podstawie optymalnych
Inny interesujące wzorzec programowania używa hello liczba interfejsu API. W tym miejscu możemy wdrożyć optymalnych powiadomień na podstawie przetwarzania hello kolejki. kolejki Hello liczba może być toothrottle używane jako umieścić w kolejce "lub" task kolejki.  Należy pamiętać, że jak w poprzednim przykładzie hello, ponieważ przetwarzanie hello odbywa się poza transakcji hello nieprzetworzone elementy mogą zostać utracone jeśli wystąpi błąd podczas przetwarzania.

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

### <a name="best-effort-drain"></a>Optymalny opróżniania
Nie można zagwarantować opróżniania kolejki hello powodu toohello równoczesnych rodzaj hello struktury danych.  Jest to możliwe, że nawet jeśli nie ma operacji użytkownika w kolejce hello jest aktywny, tooTryDequeueAsync rozmowy określonym nie może zwracać element, który został wcześniej umieszczonych w kolejce i zatwierdzone.  Element umieszczonych w kolejce Hello jest gwarantowana zbyt*ostatecznie* stają się widoczne toodequeue, jednak bez mechanizm komunikacji poza pasmem konsumenta niezależne nie może znać tej kolejki hello osiągnęła nawet jeśli stan wszystkich Producenci została zatrzymana, a nie ma nowych umieścić w kolejce operacji jest niedozwolone. W związku z tym Operacja opróżniania hello jest optymalnych zgodnie z implementacją poniżej.

Hello użytkownika należy zatrzymać dalsze producentów i zadania odbiorców i poczekaj, aż wszystkie transakcje locie toocommit lub Przerwij, przed podjęciem próby wykonania toodrain hello kolejki.  Jeśli użytkownik hello zna hello oczekiwana liczba elementów w kolejce hello, można skonfigurować powiadomienia, która sygnalizuje, że wszystkie elementy zostały usuniętej.

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

### <a name="peek"></a>Peek
ReliableConcurrentQueue nie zapewnia hello *TryPeekAsync* interfejsu api. Użytkownicy mogą uzyskać wglądu hello semantycznych przy użyciu *TryDequeueAsync* , a następnie Przerywanie transakcji hello. W tym przykładzie dequeues są przetwarzane tylko wtedy, gdy jest większa niż wartość elementu hello *10*.

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

## <a name="must-read"></a>Należy odczytać
* [Niezawodne usługi Szybki Start](service-fabric-reliable-services-quick-start.md)
* [Praca z elementami Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Niezawodne usługi powiadomień](service-fabric-reliable-services-notifications.md)
* [Niezawodne usługi tworzenia kopii zapasowej i przywracania (odzyskiwania po awarii)](service-fabric-reliable-services-backup-restore.md)
* [Niezawodne stanu Menedżera konfiguracji](service-fabric-reliable-services-configuration.md)
* [Wprowadzenie do usług interfejsu API sieci Web sieci szkieletowej usług](service-fabric-reliable-services-communication-webapi.md)
* [Zaawansowanego wykorzystania hello niezawodnej modelu programowania usług](service-fabric-reliable-services-advanced-usage.md)
* [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
