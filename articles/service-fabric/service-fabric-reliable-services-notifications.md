---
title: "Niezawodne usługi powiadomień | Dokumentacja firmy Microsoft"
description: "Dokumentacja koncepcyjna powiadomień usługi sieć szkieletowa niezawodne usługi"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="09e12-103">Niezawodne usługi powiadomień</span><span class="sxs-lookup"><span data-stu-id="09e12-103">Reliable Services notifications</span></span>
<span data-ttu-id="09e12-104">Powiadomienia Zezwalaj klientom na śledzić zmiany wprowadzone do obiektu, który interesują Cię.</span><span class="sxs-lookup"><span data-stu-id="09e12-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="09e12-105">Powiadomienia obsługuje dwa typy obiektów: *niezawodnej Menedżer stanu* i *niezawodnej słownika*.</span><span class="sxs-lookup"><span data-stu-id="09e12-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="09e12-106">Najczęstsze przyczyny przy użyciu powiadomienia są:</span><span class="sxs-lookup"><span data-stu-id="09e12-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="09e12-107">Budynek zmaterializowany widokach, takich jak indeksów pomocniczych lub agregowana filtrowane widoki stanu repliki.</span><span class="sxs-lookup"><span data-stu-id="09e12-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="09e12-108">Przykładem jest posortowana indeks wszystkie klucze w słowniku niezawodne.</span><span class="sxs-lookup"><span data-stu-id="09e12-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="09e12-109">Wysyłanie danych monitorowania, takie jak liczba użytkowników dodanych w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="09e12-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="09e12-110">Powiadomienia są uruchamiane w ramach stosowania operacji.</span><span class="sxs-lookup"><span data-stu-id="09e12-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="09e12-111">Z tego powodu powiadomienia powinien zostać obsłużony tak szybko, jak zdarzenia możliwe i synchroniczne nie powinna zawierać żadnych operacji kosztowne.</span><span class="sxs-lookup"><span data-stu-id="09e12-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="09e12-112">Stan niezawodny Menedżera powiadomień</span><span class="sxs-lookup"><span data-stu-id="09e12-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="09e12-113">Menedżer stanu niezawodny zapewnia powiadomienia o następujących zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="09e12-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="09e12-114">Transakcji</span><span class="sxs-lookup"><span data-stu-id="09e12-114">Transaction</span></span>
  * <span data-ttu-id="09e12-115">Zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="09e12-115">Commit</span></span>
* <span data-ttu-id="09e12-116">Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="09e12-116">State manager</span></span>
  * <span data-ttu-id="09e12-117">Skompiluj ponownie</span><span class="sxs-lookup"><span data-stu-id="09e12-117">Rebuild</span></span>
  * <span data-ttu-id="09e12-118">Dodanie niezawodnej stanu</span><span class="sxs-lookup"><span data-stu-id="09e12-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="09e12-119">Usunięcie stanu niezawodnej</span><span class="sxs-lookup"><span data-stu-id="09e12-119">Removal of a reliable state</span></span>

<span data-ttu-id="09e12-120">Menedżer stanu niezawodny śledzi bieżącej transakcji porządkowych.</span><span class="sxs-lookup"><span data-stu-id="09e12-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="09e12-121">Zmiana tylko w stanie transakcji, który powoduje, że powiadomienia wyzwalane jest Trwa zatwierdzanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="09e12-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="09e12-122">Menedżer stanu niezawodny przechowuje kolekcję stanów niezawodna jak słownik niezawodnych i niezawodne kolejki.</span><span class="sxs-lookup"><span data-stu-id="09e12-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="09e12-123">Menedżer stanu niezawodny generowane powiadomienia, gdy zmienia się tej kolekcji: dodano lub usunięto niezawodnej stanu lub odbudowaniu całą kolekcję.</span><span class="sxs-lookup"><span data-stu-id="09e12-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="09e12-124">Kolekcja niezawodnej Menedżer stanu zostanie odtworzony w trzech przypadkach:</span><span class="sxs-lookup"><span data-stu-id="09e12-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="09e12-125">Odzyskiwanie: Po uruchomieniu repliki odzyskuje poprzedniego stanu z dysku.</span><span class="sxs-lookup"><span data-stu-id="09e12-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="09e12-126">Po zakończeniu odzyskiwania używa **NotifyStateManagerChangedEventArgs** zdarzenia zawierający zestaw odzyskane niezawodnej stanów.</span><span class="sxs-lookup"><span data-stu-id="09e12-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="09e12-127">Pełna kopia: przed repliki może dołączyć do zestawu konfiguracji, ma ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="09e12-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="09e12-128">Czasami wymaga pełną kopię stanu niezawodnej Menedżer stanu z repliki podstawowej, która ma zostać zastosowany do repliki pomocniczej bezczynności.</span><span class="sxs-lookup"><span data-stu-id="09e12-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="09e12-129">Menedżer stanu niezawodny w replice pomocniczej używa **NotifyStateManagerChangedEventArgs** zdarzenia zawierający zestaw niezawodnej stanów, które uzyskał z repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="09e12-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="09e12-130">Przywracanie: W przypadku scenariuszy odzyskiwania po awarii repliki stan można przywrócić z kopii zapasowej za pomocą **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="09e12-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="09e12-131">W takich przypadkach używa niezawodnej Menedżer stanu w replice podstawowej **NotifyStateManagerChangedEventArgs** zdarzenia zawierający zestaw niezawodnej stanów, które go przywrócić z kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="09e12-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="09e12-132">Do zarejestrowania dla transakcji powiadomienia i/lub powiadomienia menedżera stanu, należy zarejestrować z **TransactionChanged** lub **StateManagerChanged** zdarzeń w niezawodnej Menedżer stanów.</span><span class="sxs-lookup"><span data-stu-id="09e12-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="09e12-133">Spójne rejestrowania z tych programów obsługi zdarzeń jest konstruktor stanowe usługi.</span><span class="sxs-lookup"><span data-stu-id="09e12-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="09e12-134">Gdy zarejestrujesz się w konstruktorze, nie będzie pominięcia wszystkich powiadomień, który jest spowodowany przez zmianę w czasie trwania **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="09e12-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="09e12-135">**TransactionChanged** korzysta z programu obsługi zdarzeń **NotifyTransactionChangedEventArgs** podać szczegóły dotyczące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="09e12-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="09e12-136">Zawiera właściwość action (na przykład **NotifyTransactionChangedAction.Commit**), który określa typ zmiany.</span><span class="sxs-lookup"><span data-stu-id="09e12-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="09e12-137">Zawiera także właściwości transakcji, zapewniający odniesienie transakcji zmienione.</span><span class="sxs-lookup"><span data-stu-id="09e12-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="09e12-138">Obecnie **TransactionChanged** zdarzenia są generowane tylko wtedy, gdy transakcja została przekazana.</span><span class="sxs-lookup"><span data-stu-id="09e12-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="09e12-139">Akcja będzie równa **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="09e12-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="09e12-140">Jednak w przyszłości zdarzeń może zostać wywołane dla innych typów zmian stanu transakcji.</span><span class="sxs-lookup"><span data-stu-id="09e12-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="09e12-141">Firma Microsoft zaleca sprawdzenie akcji i przetwarzania zdarzenia tylko wtedy, gdy jest to jeden, który będzie.</span><span class="sxs-lookup"><span data-stu-id="09e12-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="09e12-142">Poniżej przedstawiono przykładowy **TransactionChanged** obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="09e12-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="09e12-143">**StateManagerChanged** korzysta z programu obsługi zdarzeń **NotifyStateManagerChangedEventArgs** podać szczegóły dotyczące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="09e12-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="09e12-144">**NotifyStateManagerChangedEventArgs** ma dwa podklas: **NotifyStateManagerRebuildEventArgs** i **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="09e12-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="09e12-145">Użyj właściwości akcji w **NotifyStateManagerChangedEventArgs** można rzutować **NotifyStateManagerChangedEventArgs** do podklasy poprawne:</span><span class="sxs-lookup"><span data-stu-id="09e12-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="09e12-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="09e12-147">**NotifyStateManagerChangedAction.Add** i **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="09e12-148">Poniżej przedstawiono przykładowy **StateManagerChanged** obsługi powiadomień.</span><span class="sxs-lookup"><span data-stu-id="09e12-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="09e12-149">Niezawodne powiadomienia słownik</span><span class="sxs-lookup"><span data-stu-id="09e12-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="09e12-150">Słownik niezawodnej zapewnia powiadomienia o następujących zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="09e12-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="09e12-151">Rekompiluj: Wywoływane, gdy **ReliableDictionary** odzyskał z kopii zapasowej odzyskana lub skopiowane stanu lokalnego lub jego stan.</span><span class="sxs-lookup"><span data-stu-id="09e12-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="09e12-152">Wyczyść: Wywoływane, gdy stan **ReliableDictionary** został wyczyszczony za pośrednictwem **ClearAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="09e12-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="09e12-153">Dodaj: Wywoływane, gdy element został dodany do **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="09e12-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="09e12-154">Aktualizacja: Wywoływane, gdy element **IReliableDictionary** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="09e12-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="09e12-155">Usuń: Wywoływane, gdy element **IReliableDictionary** został usunięty.</span><span class="sxs-lookup"><span data-stu-id="09e12-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="09e12-156">Otrzymywać powiadomień niezawodnej słownika, musisz zarejestrować w usłudze **DictionaryChanged** obsługi zdarzeń na **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="09e12-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="09e12-157">Spójne rejestrowania z tych programów obsługi zdarzeń jest **ReliableStateManager.StateManagerChanged** dodać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="09e12-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="09e12-158">Podczas rejestrowania **IReliableDictionary** jest dodawany do **IReliableStateManager** gwarantuje, że nie utracić żadnych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="09e12-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="09e12-159">**ProcessStateManagerSingleEntityNotification** jest przykładowa metoda który poprzedniego **OnStateManagerChangedHandler** przykład wywołania.</span><span class="sxs-lookup"><span data-stu-id="09e12-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="09e12-160">Poprzedniego zestawu kodu **IReliableNotificationAsyncCallback** interfejsu, wraz z **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="09e12-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="09e12-161">Ponieważ **NotifyDictionaryRebuildEventArgs** zawiera **IAsyncEnumerable** interfejsu — które musi zostać wyliczone asynchronicznie — Odbuduj powiadomienia są uruchamiane przy użyciu  **RebuildNotificationAsyncCallback** zamiast **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="09e12-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="09e12-162">W poprzednim kodzie podczas przetwarzania powiadomienia o odbudowie, najpierw utrzymywana zagregowane stan jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="09e12-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="09e12-163">Ponieważ niezawodnej kolekcji odbudowaniu trwa o nowy stan wszystkich powiadomienia nie mają znaczenia.</span><span class="sxs-lookup"><span data-stu-id="09e12-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="09e12-164">**DictionaryChanged** korzysta z programu obsługi zdarzeń **NotifyDictionaryChangedEventArgs** podać szczegóły dotyczące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="09e12-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="09e12-165">**NotifyDictionaryChangedEventArgs** ma pięć podklas.</span><span class="sxs-lookup"><span data-stu-id="09e12-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="09e12-166">Użyj właściwości akcji w **NotifyDictionaryChangedEventArgs** można rzutować **NotifyDictionaryChangedEventArgs** do podklasy poprawne:</span><span class="sxs-lookup"><span data-stu-id="09e12-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="09e12-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="09e12-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="09e12-169">**NotifyDictionaryChangedAction.Add** i **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="09e12-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="09e12-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="09e12-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="09e12-172">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="09e12-172">Recommendations</span></span>
* <span data-ttu-id="09e12-173">*Czy* zakończenie zdarzenia powiadomień tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="09e12-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="09e12-174">*Nie* wykonać wszystkie operacje kosztowne (na przykład operacji We/Wy) jako część zdarzenia synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="09e12-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="09e12-175">*Czy* Sprawdź typ akcji, aby przetworzyć zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="09e12-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="09e12-176">Nowe typy akcji mogą być dodane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="09e12-176">New action types might be added in the future.</span></span>

<span data-ttu-id="09e12-177">Poniżej przedstawiono niektóre czynności, które należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="09e12-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="09e12-178">Powiadomienia są uruchamiane jako część wykonanie operacji.</span><span class="sxs-lookup"><span data-stu-id="09e12-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="09e12-179">Na przykład powiadomienia przywracania jest uruchamiany jako ostatni krok operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="09e12-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="09e12-180">Przywracanie nie zostanie zakończony, dopóki przetwarzania zdarzenia z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="09e12-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="09e12-181">Ponieważ powiadomienia są uruchamiane w ramach operacji stosowania, klientów, zobacz tylko powiadomień dla operacji lokalnie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="09e12-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="09e12-182">Ponieważ operacje są gwarancji tylko lokalnie zatwierdzone (innymi słowy, rejestrowane), mogą być lub może nie są zapisywane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="09e12-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="09e12-183">W ścieżce Powtórz pojedyncze powiadomienia jest generowane dla każdej operacji zastosowane.</span><span class="sxs-lookup"><span data-stu-id="09e12-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="09e12-184">Oznacza to, że jeśli transakcja T1 zawiera Create(X), Delete(X) i Create(X), otrzymasz jednego powiadomienia w celu utworzenia X, jeden do usunięcia, a drugi w celu utworzenia ponownie, w tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="09e12-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="09e12-185">Dla transakcji, które zawierają wiele operacji operacji są stosowane w kolejności, w jakiej zostały odebrane w replice podstawowej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09e12-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="09e12-186">W ramach przetwarzania postępu false niektóre operacje mogą być cofnąć.</span><span class="sxs-lookup"><span data-stu-id="09e12-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="09e12-187">Powiadomienia są zgłaszane dla takich operacji cofania, Przywracanie stanu repliki stabilna punktu.</span><span class="sxs-lookup"><span data-stu-id="09e12-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="09e12-188">Jedną istotną różnicą powiadomienia cofania jest, że zdarzenia, które mają zduplikowane klucze są agregowane.</span><span class="sxs-lookup"><span data-stu-id="09e12-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="09e12-189">Na przykład jeśli to Trwa wycofywanie transakcji T1, zobaczysz jednego powiadomienia Delete(X).</span><span class="sxs-lookup"><span data-stu-id="09e12-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e12-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09e12-190">Next steps</span></span>
* [<span data-ttu-id="09e12-191">Elementy Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="09e12-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="09e12-192">Niezawodne usługi szybki start</span><span class="sxs-lookup"><span data-stu-id="09e12-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="09e12-193">Niezawodne usługi Kopia zapasowa i przywracanie (odzyskiwania po awarii)</span><span class="sxs-lookup"><span data-stu-id="09e12-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="09e12-194">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="09e12-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

