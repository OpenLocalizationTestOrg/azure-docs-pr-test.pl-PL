---
title: aaaWorking z kolekcjami niezawodnej | Dokumentacja firmy Microsoft
description: "Dowiedz się hello najlepsze rozwiązania dotyczące pracy z kolekcjami wiarygodne."
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>Praca z kolekcjami niezawodnej
Sieć szkieletowa usług oferuje stanowego programowania modelu deweloperzy too.NET dostępne za pośrednictwem niezawodnych kolekcji. W szczególności usługa Service Fabric realizuje klasy kolejka niezawodnych i niezawodne słownika. Korzystając z tych klas, swój stan jest podzielona na partycje (w przypadku skalowalności), replikowane (dostępność) i nietransakcyjnego partycji (w przypadku semantyki ACID). Załóżmy Spójrz na typowy sposób obiekcie dictionary niezawodnych i zobacz, jakie jego faktycznego czynności.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

Wszystkie operacje na obiektach niezawodnej słownika (z wyjątkiem ClearAsync, która jest nieodwracalna), wymagają ITransaction obiektu. Ten obiekt skojarzone z nim i wszystkie zmiany w przypadku próby toomake tooany niezawodnej słownika i/lub obiektów niezawodnej kolejki w jednej partycji. W przypadku uzyskania ITransaction obiektu przez wywołanie metody partycji hello obiektu zabezpiecza CreateTransaction metody.

W powyższym kodzie hello obiekt ITransaction hello jest przekazywany metody AddAsync tooa niezawodnej słownika. Wewnętrznie słownika metody, które akceptuje klucz zająć czytnika/blokadę skojarzoną z kluczem hello. Jeśli metoda hello Modyfikuje wartość klucza hello, hello — metoda pobiera blokady zapisu na powitania klucza i jeśli hello metoda odczytuje jedynie z wartości klucza hello, następnie blokady odczytu są wykonywane na powitania klucza. Ponieważ AddAsync modyfikuje toohello wartość klucza hello nowe, wartości przekazane blokady zapisu klucza hello jest zajęta. Tak, jeśli tooadd wartościami hello wątków 2 (lub więcej) klucza na powitania sam jeden wątek będzie uzyskanie blokady zapisu hello i hello inne wątki zablokuje czasu. Domyślnie blok metod blokadę too4 sekund tooacquire hello; po 4 sekundy metody hello throw TimeoutException. Przeciążenia metody istnieje dzięki czemu możesz toopass wartość limitu czasu jawne, jeśli chcesz użyć.

Zazwyczaj zapisu tooa tooreact Twojego kodu TimeoutException przez Przechwytywanie go i ponawianie operacji całego hello (jak pokazano w powyższym kodzie hello). W kodzie proste wywoływany tylko Task.Delay przekazywanie każdorazowo 100 milisekund. Ale w rzeczywistości może być lepiej zamiast określonego rodzaju wykładniczego wycofywania opóźnienia.

Po hello blokada jest uzyskiwana, AddAsync dodaje klucz hello i tooan wewnętrzny słownika tymczasowego skojarzone z obiektem ITransaction hello odwołuje się do obiektu wartości. Jest to realizowane tooprovide z semantyki odczytu your właścicielem zapisu. Oznacza to, że po wywołaniu metody AddAsync, nowsze tooTryGetValueAsync wywołania (przy użyciu hello tego samego obiektu ITransaction) zwróci wartość hello, nawet jeśli nie zostały jeszcze przekazane hello transakcji. Następnie AddAsync serializuje klucz i wartość obiekty tablice toobyte i dołącza te pliku dziennika bajtów tablice tooa w węźle lokalne powitania. Na koniec AddAsync wysyła hello bajtów tablice tooall hello replik pomocniczych tak ma hello tego samego klucza i wartości informacji. Nawet jeśli informacje klucza i wartości hello został zapisany plik dziennika tooa, informacji hello jest uważana za część słownika hello przed przekazaniem hello transakcji, które są skojarzone.

W powyższym kodzie hello tooCommitAsync wywołania hello zatwierdza wszystkie operacje hello transakcji. W szczególności dołącza plik dziennika toohello zatwierdzania informacje w węźle lokalne powitania i wysyła również replikach pomocniczych hello tooall rekordu zatwierdzania hello. Po odpowiedział kworum replik hello (większość), wszystkie dane zmiany są traktowane jako trwałe i wszystkie skojarzone z kluczy, które zostały manipulować za pośrednictwem obiektu ITransaction hello blokady są wydawane tak innych wątków/transakcji można manipulować hello tych samych kluczy i ich wartości.

Jeśli CommitAsync nie jest wywoływany (zazwyczaj powodu tooan zgłaszanego wyjątku), obiekt ITransaction hello pobiera usunięty. Podczas usuwania obiektu ITransaction niezatwierdzone sieci szkieletowej usług dołącza przerwania informacji toohello węzła lokalnego w pliku dziennika i nic musi toobe wysyłane tooany hello replikach pomocniczych. A następnie są wydawane wszystkie blokady związane z kluczy, które zostały manipulować za pośrednictwem hello transakcji.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Typowych problemów i w jaki sposób tooavoid ich
Po zapoznaniu się z wewnętrznie działanie hello niezawodnej kolekcje, Spójrzmy na niektórych typowych wpływające. Zobacz poniższy kod hello:

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

Podczas pracy ze słownikiem regularne .NET, można dodać słownika toohello klucza i wartości, a następnie zmień hello wartość właściwości (na przykład LastLogin). Jednak ten kod nie będzie pracował prawidłowo niezawodnej słownika. Pamiętaj na powitania dyskusji wcześniej, wywołanie hello tooAddAsync serializuje hello klucza i wartości obiektów, tablic toobyte i następnie zapisuje hello stałych tooa pliku lokalnego, a także przesyła je toohello replikach pomocniczych. Jeśli później zmienić właściwość, spowoduje to zmianę wartości właściwości hello w pamięci. nie ma ona wpływu pliku lokalnego hello lub hello dane przesyłane toohello repliki. Jeśli proces hello ulegnie awarii, co znajduje się w pamięci jest odrzucone. Podczas uruchamiania nowego procesu, lub jeśli inny replika staje się podstawowym, hello stara wartość właściwości jest, co jest dostępne.

Nie można podkreślają, wystarczająco jak łatwo jest toomake hello rodzaju błędu przedstawionych powyżej. I uzyskasz tylko informacje na temat błędu hello Jeśli się się, że proces hello przestanie działać. Kod hello toowrite prawidłowy sposób Hello jest po prostu tooreverse hello dwa wiersze:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Inny przykład przedstawiający powszechnym błędem jest następujący:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

Ponownie z regularne .NET słowników, powyższym kodzie hello działa prawidłowo i jest wspólnym wzorcem: hello deweloperów używa klucza toolook wartości. Jeśli istnieje wartość hello, deweloperów hello zmieni się wartość właściwości. Jednak z kolekcjami niezawodne, ten kod wykazuje hello sam problem jak już omówione: **nie należy zmodyfikować obiekt po hrweb przekazali tooa niezawodnej kolekcji.**

Witaj poprawne tooupdate sposób wartości w zbiorze niezawodnej jest tooget toohello odwołania istniejącą wartość i należy wziąć pod uwagę hello obiektu określonego tooby to odwołanie niezmienialny. Następnie utwórz nowy obiekt, który jest dokładna kopia oryginalnego obiektu hello. Teraz można zmodyfikować hello stan tego nowego obiektu i zapisu hello nowego obiektu do kolekcji hello tak, aby go serializowana toobyte stałych toohello dołączany plik lokalny i wysyłane toohello repliki. Po zatwierdzania hello zmiany hello obiektów w pamięci, hello lokalnego pliku i wszystkie repliki hello mają hello dokładnie takie same stanu. Wszystko to dobry!

Witaj poniższy kod tooupdate prawidłowy sposób hello wartość w niezawodnej kolekcji:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Zdefiniuj błąd programisty tooprevent typy niezmienne danych
Najlepiej, jeśli chcemy hello tooreport błędów podczas przypadkowo tworzy kod, który mutuje stan obiektu czy możesz powinni tooconsider niezmienialny. Jednak hello kompilator języka C# nie ma toodo możliwości hello to. Tak, tooavoid potencjalnych programisty usterki, zdecydowanie zaleca się zdefiniowanie typów hello, używanego z typami niezmienne kolekcje niezawodnej toobe. W szczególności oznacza to, że trzymaj toocore typy wartości (takie jak numery [Int32, UInt64, itp.], DateTime, Guid, TimeSpan i hello, takich jak). A, można również użyć ciągu. Jest on właściwości kolekcji tooavoid najlepszego jako serializacji i deserializacji je można często może pogarszać wydajność. Jednak jeśli chcesz toouse właściwości kolekcji, zdecydowanie zaleca się użycie hello. Biblioteka obsługi kolekcji niezmienialnych w sieci ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Ta biblioteka jest dostępny do pobrania http://nuget.org. Zalecamy również pieczętowania klas i oznaczanie pola tylko do odczytu, jeśli to możliwe.

Hello typ informacji o użytkowniku poniżej pokazano, jak toodefine jako niezmienialny wpisz, korzystając z wyżej wymienionych zalecenia.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

Hello ItemId typu jest również niezmiennego typu, jak pokazano poniżej:

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>Przechowywanie wersji schematu (uaktualnienia)
Wewnętrznie niezawodne kolekcje serializować obiektów przy użyciu. DataContractSerializer w sieci. Hello serializować obiektów są dysku lokalnym utrwalonego toohello repliki podstawowej i również przesyłane toohello replikach pomocniczych. Miarę rozwoju usługi, prawdopodobnie będzie toochange hello rodzaj danych (schemat) wymaga Twoja usługa. Przechowywanie wersji danych bardzo ostrożnie musi osiągają. Najpierw i, musi być zawsze możliwe toodeserialize stare dane. W szczególności, oznacza to, deserializacji kodu musi być nieograniczonej zapewniającej: wersja 333 kodu usługi musi być możliwe toooperate na dane umieszczone w niezawodnej kolekcji w wersji 1 kodu usługi 5 lat temu.

Ponadto kodu usługi jest uaktualniony jedną domenę uaktualnienia naraz. Tak podczas uaktualniania, masz dwie różne wersje kodu usługi uruchomione jednocześnie. Należy uniknąć hello nową wersję kodu usługi Użyj nowego schematu hello jako stare wersje kodu usługi może nie być możliwe toohandle hello nowego schematu. Jeśli to możliwe, należy projektować w każdej wersji usługi zgodne wprzód toobe w wersji 1. W szczególności, oznacza to, że V1 kodu usługi powinno być możliwe toosimply Ignoruj jawnie nie obsługuje elementów schematu. Jednak musi być możliwe toosave, wszelkie dane nie jawnie wiedzieć o, a po prostu zapisać go z powrotem się podczas aktualizowania klucza słownika lub wartość.

> [!WARNING]
> Podczas gdy można zmodyfikować schematu hello klucza, należy się upewnić, skrótu swój klucz i algorytmy equals są stałe. Jeśli zmienisz sposób działania albo te algorytmy, nie będzie możliwe toolook klucz hello w ramach niezawodnej słownika hello kiedykolwiek ponownie.
>
>

Alternatywnie można wykonywać, co jest zazwyczaj określonego tooas 2-etapowego uaktualnienia. Uaktualnianie Faza 2, uaktualnij usługę z V1 tooV2: V2 zawiera hello kod, który zna jak toodeal z hello nowej zmiany schematu, ale ten kod nie jest wykonywana. Gdy hello V2 kod odczytuje dane V1, działa na nim i zapisuje dane w wersji 1. Następnie po zakończeniu uaktualniania hello we wszystkich domenach uaktualnienia, możesz może jakiś sposób sygnał toohello uruchomionych wystąpień V2, że uaktualnienie hello jest pełny. (Jednokierunkowej toosignal to tooroll się uaktualnienie konfiguracji; jest to, co sprawia, że to uaktualnienie fazy 2.) Teraz wystąpień V2 hello można odczytanie danych V1, przekonwertuj go tooV2 danych, wykonywać na nich operacje i zapisz je jako dane V2. Jeśli inne wystąpienia odczytu danych V2, nie muszą oni tooconvert, po prostu działają na nim, a także zapisać danych w wersji 2.

## <a name="next-steps"></a>Następne kroki
Zobacz toolearn o tworzeniu kontrakty przekazywania danych zgodne [kontrakty danych zgodne z nowszymi](https://msdn.microsoft.com/library/ms731083.aspx).

najlepsze praktyki toolearn na przechowywanie wersji kontraktów danych, zobacz [przechowywanie wersji kontraktów danych](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn umów tooimplement wersji na uszkodzenia danych, zobacz [wywołania zwrotne serializacji z tolerancją dla wersji](https://msdn.microsoft.com/library/ms733734.aspx).

toolearn tooprovide to struktura danych, która może współdziałać w różnych wersjach, zobacz temat [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
