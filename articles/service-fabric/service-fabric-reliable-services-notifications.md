---
title: "powiadomienia usługi aaaReliable | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="9e52e-103">Niezawodne usługi powiadomień</span><span class="sxs-lookup"><span data-stu-id="9e52e-103">Reliable Services notifications</span></span>
<span data-ttu-id="9e52e-104">Powiadomienia Zezwalaj klientom tootrack hello zmiany, które są określane jako obiekt tooan interesują Cię.</span><span class="sxs-lookup"><span data-stu-id="9e52e-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="9e52e-105">Powiadomienia obsługuje dwa typy obiektów: *niezawodnej Menedżer stanu* i *niezawodnej słownika*.</span><span class="sxs-lookup"><span data-stu-id="9e52e-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="9e52e-106">Najczęstsze przyczyny przy użyciu powiadomienia są:</span><span class="sxs-lookup"><span data-stu-id="9e52e-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="9e52e-107">Budynek zmaterializowany widokach, takich jak indeksów pomocniczych lub agregowana filtrowane widoki stanu hello repliki.</span><span class="sxs-lookup"><span data-stu-id="9e52e-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="9e52e-108">Przykładem jest posortowana indeks wszystkie klucze w słowniku niezawodne.</span><span class="sxs-lookup"><span data-stu-id="9e52e-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="9e52e-109">Wysyłania danych monitorowania, takie jak liczba hello użytkowników dodanych w hello w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="9e52e-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="9e52e-110">Powiadomienia są uruchamiane w ramach stosowania operacji.</span><span class="sxs-lookup"><span data-stu-id="9e52e-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="9e52e-111">Z tego powodu powiadomienia powinien zostać obsłużony tak szybko, jak zdarzenia możliwe i synchroniczne nie powinna zawierać żadnych operacji kosztowne.</span><span class="sxs-lookup"><span data-stu-id="9e52e-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="9e52e-112">Stan niezawodny Menedżera powiadomień</span><span class="sxs-lookup"><span data-stu-id="9e52e-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="9e52e-113">Menedżer stanu niezawodny zapewnia powiadomienia o hello następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="9e52e-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="9e52e-114">Transakcji</span><span class="sxs-lookup"><span data-stu-id="9e52e-114">Transaction</span></span>
  * <span data-ttu-id="9e52e-115">Zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="9e52e-115">Commit</span></span>
* <span data-ttu-id="9e52e-116">Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="9e52e-116">State manager</span></span>
  * <span data-ttu-id="9e52e-117">Skompiluj ponownie</span><span class="sxs-lookup"><span data-stu-id="9e52e-117">Rebuild</span></span>
  * <span data-ttu-id="9e52e-118">Dodanie niezawodnej stanu</span><span class="sxs-lookup"><span data-stu-id="9e52e-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="9e52e-119">Usunięcie stanu niezawodnej</span><span class="sxs-lookup"><span data-stu-id="9e52e-119">Removal of a reliable state</span></span>

<span data-ttu-id="9e52e-120">Menedżer stanu niezawodny śledzi hello bieżącej transakcji porządkowych.</span><span class="sxs-lookup"><span data-stu-id="9e52e-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="9e52e-121">Zmiana tylko Hello w stanie transakcji, które powoduje, że toobe powiadomień, uruchamiany jest Trwa zatwierdzanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="9e52e-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="9e52e-122">Menedżer stanu niezawodny przechowuje kolekcję stanów niezawodna jak słownik niezawodnych i niezawodne kolejki.</span><span class="sxs-lookup"><span data-stu-id="9e52e-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="9e52e-123">Menedżer stanu niezawodny generowane powiadomienia, gdy zmienia się tej kolekcji: dodano lub usunięto niezawodnej stanu lub odbudowaniu hello całą kolekcję.</span><span class="sxs-lookup"><span data-stu-id="9e52e-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="9e52e-124">Hello kolekcji niezawodnej Menedżer stanów jest ponownie skompilowany w trzech przypadkach:</span><span class="sxs-lookup"><span data-stu-id="9e52e-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="9e52e-125">Odzyskiwanie: Po uruchomieniu repliki odzyskuje poprzedniego stanu z dysku hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="9e52e-126">Na końcu hello odzyskiwania, używa **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello odzyskane niezawodnej stanów.</span><span class="sxs-lookup"><span data-stu-id="9e52e-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="9e52e-127">Pełna kopia: przed repliki można przyłączyć hello konfiguracji, ma toobe skompilowany.</span><span class="sxs-lookup"><span data-stu-id="9e52e-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="9e52e-128">Czasami wymaga pełną kopię stanu niezawodnej Menedżer stanu z hello repliki podstawowej toobe toohello zastosowane bezczynności repliki pomocniczej.</span><span class="sxs-lookup"><span data-stu-id="9e52e-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="9e52e-129">Menedżer stanu niezawodny na powitania repliki pomocniczej używa **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello niezawodnej stanów, które uzyskał z hello repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="9e52e-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="9e52e-130">Przywracanie: W przypadku scenariuszy odzyskiwania po awarii repliki hello stan można przywrócić z kopii zapasowej za pomocą **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="9e52e-131">W takich przypadkach używa niezawodnej Menedżer stanu w replice podstawowej hello **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello niezawodnej stanów, które go przywrócić z kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="9e52e-132">tooregister dla transakcji powiadomienia i/lub powiadomienia menedżera stanu, należy tooregister z hello **TransactionChanged** lub **StateManagerChanged** zdarzeń w niezawodnej Menedżer stanów.</span><span class="sxs-lookup"><span data-stu-id="9e52e-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="9e52e-133">Spójne tooregister z tych programów obsługi zdarzeń jest konstruktor hello stanowe usługi.</span><span class="sxs-lookup"><span data-stu-id="9e52e-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="9e52e-134">Po zarejestrowaniu się w Konstruktorze hello nie utracić wszystkich powiadomień, który jest spowodowany przez zmianę w okresie istnienia hello **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="9e52e-135">Witaj **TransactionChanged** korzysta z programu obsługi zdarzeń **NotifyTransactionChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="9e52e-136">Zawiera właściwość action hello (na przykład **NotifyTransactionChangedAction.Commit**), który określa typ hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="9e52e-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="9e52e-137">Zawiera ona także hello transakcji właściwość, która zapewnia zmieniający transakcji toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="9e52e-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="9e52e-138">Obecnie **TransactionChanged** zdarzenia są generowane tylko wtedy, gdy transakcja hello została przekazana.</span><span class="sxs-lookup"><span data-stu-id="9e52e-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="9e52e-139">Hello akcji jest następnie równy za**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="9e52e-140">Jednak w przyszłości hello, zdarzeń może zostać wywołane dla innych typów zmian stanu transakcji.</span><span class="sxs-lookup"><span data-stu-id="9e52e-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="9e52e-141">Firma Microsoft zaleca sprawdzenie hello akcji i przetwarzania zdarzeń hello tylko wtedy, gdy jest to jeden, który będzie.</span><span class="sxs-lookup"><span data-stu-id="9e52e-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="9e52e-142">Poniżej przedstawiono przykładowy **TransactionChanged** obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9e52e-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="9e52e-143">Witaj **StateManagerChanged** korzysta z programu obsługi zdarzeń **NotifyStateManagerChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="9e52e-144">**NotifyStateManagerChangedEventArgs** ma dwa podklas: **NotifyStateManagerRebuildEventArgs** i **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="9e52e-145">Użyj właściwości akcji hello w **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** podklasy poprawne toohello:</span><span class="sxs-lookup"><span data-stu-id="9e52e-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="9e52e-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="9e52e-147">**NotifyStateManagerChangedAction.Add** i **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="9e52e-148">Poniżej przedstawiono przykładowy **StateManagerChanged** obsługi powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9e52e-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="9e52e-149">Niezawodne powiadomienia słownik</span><span class="sxs-lookup"><span data-stu-id="9e52e-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="9e52e-150">Słownik niezawodnej zapewnia powiadomienia o hello następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="9e52e-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="9e52e-151">Rekompiluj: Wywoływane, gdy **ReliableDictionary** odzyskał z kopii zapasowej odzyskana lub skopiowane stanu lokalnego lub jego stan.</span><span class="sxs-lookup"><span data-stu-id="9e52e-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="9e52e-152">Wyczyść: Wywoływane, gdy hello stan **ReliableDictionary** został wyczyszczony za pośrednictwem hello **ClearAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="9e52e-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="9e52e-153">Dodaj: Wywoływane, gdy element został dodany za**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="9e52e-154">Aktualizacja: Wywoływane, gdy element **IReliableDictionary** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="9e52e-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="9e52e-155">Usuń: Wywoływane, gdy element **IReliableDictionary** został usunięty.</span><span class="sxs-lookup"><span data-stu-id="9e52e-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="9e52e-156">tooget niezawodnej słownika powiadomienia, należy tooregister z hello **DictionaryChanged** obsługi zdarzeń na **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="9e52e-157">Spójne tooregister z tych programów obsługi zdarzeń jest hello **ReliableStateManager.StateManagerChanged** dodać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9e52e-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="9e52e-158">Podczas rejestrowania **IReliableDictionary** dodaniu zbyt**IReliableStateManager** gwarantuje, że nie utracić żadnych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9e52e-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="9e52e-159">**ProcessStateManagerSingleEntityNotification** jest hello przykładowa metoda tego hello poprzedniego **OnStateManagerChangedHandler** przykład wywołania.</span><span class="sxs-lookup"><span data-stu-id="9e52e-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="9e52e-160">Witaj poprzedni kod ustawia hello **IReliableNotificationAsyncCallback** interfejsu, wraz z **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="9e52e-161">Ponieważ **NotifyDictionaryRebuildEventArgs** zawiera **IAsyncEnumerable** interfejsu — co wymaga toobe wyliczyć asynchronicznie — Odbuduj powiadomienia są uruchamiane przy użyciu  **RebuildNotificationAsyncCallback** zamiast **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="9e52e-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="9e52e-162">W hello poprzedzających kodu, w ramach przetwarzania hello Odbuduj powiadomień pierwszy hello utrzymane, zagregowany stan jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="9e52e-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="9e52e-163">Ponieważ kolekcji niezawodnej hello odbudowaniu trwa o nowy stan wszystkich powiadomienia nie mają znaczenia.</span><span class="sxs-lookup"><span data-stu-id="9e52e-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="9e52e-164">Witaj **DictionaryChanged** korzysta z programu obsługi zdarzeń **NotifyDictionaryChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="9e52e-165">**NotifyDictionaryChangedEventArgs** ma pięć podklas.</span><span class="sxs-lookup"><span data-stu-id="9e52e-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="9e52e-166">Użyj właściwości akcji hello w **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** podklasy poprawne toohello:</span><span class="sxs-lookup"><span data-stu-id="9e52e-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="9e52e-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="9e52e-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="9e52e-169">**NotifyDictionaryChangedAction.Add** i **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="9e52e-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="9e52e-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9e52e-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="9e52e-172">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="9e52e-172">Recommendations</span></span>
* <span data-ttu-id="9e52e-173">*Czy* zakończenie zdarzenia powiadomień tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="9e52e-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="9e52e-174">*Nie* wykonać wszystkie operacje kosztowne (na przykład operacji We/Wy) jako część zdarzenia synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="9e52e-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="9e52e-175">*Czy* Sprawdź typ akcji hello, aby przetworzyć zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="9e52e-176">Nowe typy akcji mogą być dodane w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="9e52e-177">Poniżej przedstawiono niektóre tookeep rzeczy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="9e52e-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="9e52e-178">Powiadomienia są uruchamiane jako część hello wykonanie operacji.</span><span class="sxs-lookup"><span data-stu-id="9e52e-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="9e52e-179">Na przykład powiadomienia przywracania jest uruchamiany jako ostatni krok hello operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="9e52e-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="9e52e-180">Przywracanie nie zostanie zakończony, dopóki zdarzenia z powiadomieniem o hello jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="9e52e-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="9e52e-181">Ponieważ powiadomienia są uruchamiane jako część hello operacji stosowania, klientów, zobacz tylko powiadomień dla operacji lokalnie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="9e52e-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="9e52e-182">Ponieważ operacje dotrą tylko toobe lokalnie zadeklarowane (innymi słowy, rejestrowane), może lub nie mogą zostać cofnięte w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="9e52e-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="9e52e-183">W ścieżce Powtórz hello pojedyncze powiadomienia jest generowane dla każdej operacji zastosowane.</span><span class="sxs-lookup"><span data-stu-id="9e52e-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="9e52e-184">Oznacza to, że jeśli transakcja T1 zawiera Create(X), Delete(X) i Create(X), otrzymają jedno powiadomienie tworzenie hello x, co do usunięcia hello i jeden dla tworzenia hello ponownie, w tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="9e52e-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="9e52e-185">Dla transakcji, które zawierają wiele operacji operacji są stosowane w kolejności hello otrzymano w replice podstawowej hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e52e-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="9e52e-186">W ramach przetwarzania postępu false niektóre operacje mogą być cofnąć.</span><span class="sxs-lookup"><span data-stu-id="9e52e-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="9e52e-187">Powiadomienia są zgłaszane dla takich operacji cofania, wycofanie stanu hello hello repliki wstecz tooa stabilna punktu.</span><span class="sxs-lookup"><span data-stu-id="9e52e-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="9e52e-188">Jedną istotną różnicą powiadomienia cofania jest, że zdarzenia, które mają zduplikowane klucze są agregowane.</span><span class="sxs-lookup"><span data-stu-id="9e52e-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="9e52e-189">Na przykład jeśli to Trwa wycofywanie transakcji T1, zobaczysz tooDelete(X) pojedyncze powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9e52e-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e52e-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e52e-190">Next steps</span></span>
* [<span data-ttu-id="9e52e-191">Elementy Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="9e52e-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="9e52e-192">Niezawodne usługi szybki start</span><span class="sxs-lookup"><span data-stu-id="9e52e-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="9e52e-193">Niezawodne usługi Kopia zapasowa i przywracanie (odzyskiwania po awarii)</span><span class="sxs-lookup"><span data-stu-id="9e52e-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="9e52e-194">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="9e52e-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

