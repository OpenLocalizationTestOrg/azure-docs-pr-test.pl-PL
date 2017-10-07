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
# <a name="reliable-services-notifications"></a>Niezawodne usługi powiadomień
Powiadomienia Zezwalaj klientom tootrack hello zmiany, które są określane jako obiekt tooan interesują Cię. Powiadomienia obsługuje dwa typy obiektów: *niezawodnej Menedżer stanu* i *niezawodnej słownika*.

Najczęstsze przyczyny przy użyciu powiadomienia są:

* Budynek zmaterializowany widokach, takich jak indeksów pomocniczych lub agregowana filtrowane widoki stanu hello repliki. Przykładem jest posortowana indeks wszystkie klucze w słowniku niezawodne.
* Wysyłania danych monitorowania, takie jak liczba hello użytkowników dodanych w hello w ciągu ostatniej godziny.

Powiadomienia są uruchamiane w ramach stosowania operacji. Z tego powodu powiadomienia powinien zostać obsłużony tak szybko, jak zdarzenia możliwe i synchroniczne nie powinna zawierać żadnych operacji kosztowne.

## <a name="reliable-state-manager-notifications"></a>Stan niezawodny Menedżera powiadomień
Menedżer stanu niezawodny zapewnia powiadomienia o hello następujące zdarzenia:

* Transakcji
  * Zatwierdzenie
* Menedżer stanu
  * Skompiluj ponownie
  * Dodanie niezawodnej stanu
  * Usunięcie stanu niezawodnej

Menedżer stanu niezawodny śledzi hello bieżącej transakcji porządkowych. Zmiana tylko Hello w stanie transakcji, które powoduje, że toobe powiadomień, uruchamiany jest Trwa zatwierdzanie transakcji.

Menedżer stanu niezawodny przechowuje kolekcję stanów niezawodna jak słownik niezawodnych i niezawodne kolejki. Menedżer stanu niezawodny generowane powiadomienia, gdy zmienia się tej kolekcji: dodano lub usunięto niezawodnej stanu lub odbudowaniu hello całą kolekcję.
Hello kolekcji niezawodnej Menedżer stanów jest ponownie skompilowany w trzech przypadkach:

* Odzyskiwanie: Po uruchomieniu repliki odzyskuje poprzedniego stanu z dysku hello. Na końcu hello odzyskiwania, używa **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello odzyskane niezawodnej stanów.
* Pełna kopia: przed repliki można przyłączyć hello konfiguracji, ma toobe skompilowany. Czasami wymaga pełną kopię stanu niezawodnej Menedżer stanu z hello repliki podstawowej toobe toohello zastosowane bezczynności repliki pomocniczej. Menedżer stanu niezawodny na powitania repliki pomocniczej używa **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello niezawodnej stanów, które uzyskał z hello repliki podstawowej.
* Przywracanie: W przypadku scenariuszy odzyskiwania po awarii repliki hello stan można przywrócić z kopii zapasowej za pomocą **RestoreAsync**. W takich przypadkach używa niezawodnej Menedżer stanu w replice podstawowej hello **NotifyStateManagerChangedEventArgs** toofire zdarzenie, które zawiera zestaw hello niezawodnej stanów, które go przywrócić z kopii zapasowej hello.

tooregister dla transakcji powiadomienia i/lub powiadomienia menedżera stanu, należy tooregister z hello **TransactionChanged** lub **StateManagerChanged** zdarzeń w niezawodnej Menedżer stanów. Spójne tooregister z tych programów obsługi zdarzeń jest konstruktor hello stanowe usługi. Po zarejestrowaniu się w Konstruktorze hello nie utracić wszystkich powiadomień, który jest spowodowany przez zmianę w okresie istnienia hello **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Witaj **TransactionChanged** korzysta z programu obsługi zdarzeń **NotifyTransactionChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello. Zawiera właściwość action hello (na przykład **NotifyTransactionChangedAction.Commit**), który określa typ hello zmiany. Zawiera ona także hello transakcji właściwość, która zapewnia zmieniający transakcji toohello odwołania.

> [!NOTE]
> Obecnie **TransactionChanged** zdarzenia są generowane tylko wtedy, gdy transakcja hello została przekazana. Hello akcji jest następnie równy za**NotifyTransactionChangedAction.Commit**. Jednak w przyszłości hello, zdarzeń może zostać wywołane dla innych typów zmian stanu transakcji. Firma Microsoft zaleca sprawdzenie hello akcji i przetwarzania zdarzeń hello tylko wtedy, gdy jest to jeden, który będzie.
> 
> 

Poniżej przedstawiono przykładowy **TransactionChanged** obsługi zdarzeń.

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

Witaj **StateManagerChanged** korzysta z programu obsługi zdarzeń **NotifyStateManagerChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello.
**NotifyStateManagerChangedEventArgs** ma dwa podklas: **NotifyStateManagerRebuildEventArgs** i **NotifyStateManagerSingleEntityChangedEventArgs**.
Użyj właściwości akcji hello w **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** podklasy poprawne toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** i **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Poniżej przedstawiono przykładowy **StateManagerChanged** obsługi powiadomień.

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

## <a name="reliable-dictionary-notifications"></a>Niezawodne powiadomienia słownik
Słownik niezawodnej zapewnia powiadomienia o hello następujące zdarzenia:

* Rekompiluj: Wywoływane, gdy **ReliableDictionary** odzyskał z kopii zapasowej odzyskana lub skopiowane stanu lokalnego lub jego stan.
* Wyczyść: Wywoływane, gdy hello stan **ReliableDictionary** został wyczyszczony za pośrednictwem hello **ClearAsync** metody.
* Dodaj: Wywoływane, gdy element został dodany za**ReliableDictionary**.
* Aktualizacja: Wywoływane, gdy element **IReliableDictionary** została zaktualizowana.
* Usuń: Wywoływane, gdy element **IReliableDictionary** został usunięty.

tooget niezawodnej słownika powiadomienia, należy tooregister z hello **DictionaryChanged** obsługi zdarzeń na **IReliableDictionary**. Spójne tooregister z tych programów obsługi zdarzeń jest hello **ReliableStateManager.StateManagerChanged** dodać powiadomienia.
Podczas rejestrowania **IReliableDictionary** dodaniu zbyt**IReliableStateManager** gwarantuje, że nie utracić żadnych powiadomień.

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
> **ProcessStateManagerSingleEntityNotification** jest hello przykładowa metoda tego hello poprzedniego **OnStateManagerChangedHandler** przykład wywołania.
> 
> 

Witaj poprzedni kod ustawia hello **IReliableNotificationAsyncCallback** interfejsu, wraz z **DictionaryChanged**. Ponieważ **NotifyDictionaryRebuildEventArgs** zawiera **IAsyncEnumerable** interfejsu — co wymaga toobe wyliczyć asynchronicznie — Odbuduj powiadomienia są uruchamiane przy użyciu  **RebuildNotificationAsyncCallback** zamiast **OnDictionaryChangedHandler**.

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
> W hello poprzedzających kodu, w ramach przetwarzania hello Odbuduj powiadomień pierwszy hello utrzymane, zagregowany stan jest usuwany. Ponieważ kolekcji niezawodnej hello odbudowaniu trwa o nowy stan wszystkich powiadomienia nie mają znaczenia.
> 
> 

Witaj **DictionaryChanged** korzysta z programu obsługi zdarzeń **NotifyDictionaryChangedEventArgs** tooprovide szczegóły dotyczące zdarzenia hello.
**NotifyDictionaryChangedEventArgs** ma pięć podklas. Użyj właściwości akcji hello w **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** podklasy poprawne toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** i **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>Zalecenia
* *Czy* zakończenie zdarzenia powiadomień tak szybko jak to możliwe.
* *Nie* wykonać wszystkie operacje kosztowne (na przykład operacji We/Wy) jako część zdarzenia synchroniczne.
* *Czy* Sprawdź typ akcji hello, aby przetworzyć zdarzenie hello. Nowe typy akcji mogą być dodane w przyszłości hello.

Poniżej przedstawiono niektóre tookeep rzeczy pamiętać:

* Powiadomienia są uruchamiane jako część hello wykonanie operacji. Na przykład powiadomienia przywracania jest uruchamiany jako ostatni krok hello operacji przywracania. Przywracanie nie zostanie zakończony, dopóki zdarzenia z powiadomieniem o hello jest przetwarzany.
* Ponieważ powiadomienia są uruchamiane jako część hello operacji stosowania, klientów, zobacz tylko powiadomień dla operacji lokalnie zatwierdzone. Ponieważ operacje dotrą tylko toobe lokalnie zadeklarowane (innymi słowy, rejestrowane), może lub nie mogą zostać cofnięte w przyszłości hello.
* W ścieżce Powtórz hello pojedyncze powiadomienia jest generowane dla każdej operacji zastosowane. Oznacza to, że jeśli transakcja T1 zawiera Create(X), Delete(X) i Create(X), otrzymają jedno powiadomienie tworzenie hello x, co do usunięcia hello i jeden dla tworzenia hello ponownie, w tej kolejności.
* Dla transakcji, które zawierają wiele operacji operacji są stosowane w kolejności hello otrzymano w replice podstawowej hello hello użytkownika.
* W ramach przetwarzania postępu false niektóre operacje mogą być cofnąć. Powiadomienia są zgłaszane dla takich operacji cofania, wycofanie stanu hello hello repliki wstecz tooa stabilna punktu. Jedną istotną różnicą powiadomienia cofania jest, że zdarzenia, które mają zduplikowane klucze są agregowane. Na przykład jeśli to Trwa wycofywanie transakcji T1, zobaczysz tooDelete(X) pojedyncze powiadomienia.

## <a name="next-steps"></a>Następne kroki
* [Elementy Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
* [Niezawodne usługi Kopia zapasowa i przywracanie (odzyskiwania po awarii)](service-fabric-reliable-services-backup-restore.md)
* [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

