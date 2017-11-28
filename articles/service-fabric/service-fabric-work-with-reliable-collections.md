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
# <a name="working-with-reliable-collections"></a><span data-ttu-id="831db-103">Praca z kolekcjami niezawodnej</span><span class="sxs-lookup"><span data-stu-id="831db-103">Working with Reliable Collections</span></span>
<span data-ttu-id="831db-104">Sieć szkieletowa usług oferuje stanowego programowania modelu deweloperzy too.NET dostępne za pośrednictwem niezawodnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="831db-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="831db-105">W szczególności usługa Service Fabric realizuje klasy kolejka niezawodnych i niezawodne słownika.</span><span class="sxs-lookup"><span data-stu-id="831db-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="831db-106">Korzystając z tych klas, swój stan jest podzielona na partycje (w przypadku skalowalności), replikowane (dostępność) i nietransakcyjnego partycji (w przypadku semantyki ACID).</span><span class="sxs-lookup"><span data-stu-id="831db-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="831db-107">Załóżmy Spójrz na typowy sposób obiekcie dictionary niezawodnych i zobacz, jakie jego faktycznego czynności.</span><span class="sxs-lookup"><span data-stu-id="831db-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

<span data-ttu-id="831db-108">Wszystkie operacje na obiektach niezawodnej słownika (z wyjątkiem ClearAsync, która jest nieodwracalna), wymagają ITransaction obiektu.</span><span class="sxs-lookup"><span data-stu-id="831db-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="831db-109">Ten obiekt skojarzone z nim i wszystkie zmiany w przypadku próby toomake tooany niezawodnej słownika i/lub obiektów niezawodnej kolejki w jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="831db-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="831db-110">W przypadku uzyskania ITransaction obiektu przez wywołanie metody partycji hello obiektu zabezpiecza CreateTransaction metody.</span><span class="sxs-lookup"><span data-stu-id="831db-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="831db-111">W powyższym kodzie hello obiekt ITransaction hello jest przekazywany metody AddAsync tooa niezawodnej słownika.</span><span class="sxs-lookup"><span data-stu-id="831db-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="831db-112">Wewnętrznie słownika metody, które akceptuje klucz zająć czytnika/blokadę skojarzoną z kluczem hello.</span><span class="sxs-lookup"><span data-stu-id="831db-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="831db-113">Jeśli metoda hello Modyfikuje wartość klucza hello, hello — metoda pobiera blokady zapisu na powitania klucza i jeśli hello metoda odczytuje jedynie z wartości klucza hello, następnie blokady odczytu są wykonywane na powitania klucza.</span><span class="sxs-lookup"><span data-stu-id="831db-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="831db-114">Ponieważ AddAsync modyfikuje toohello wartość klucza hello nowe, wartości przekazane blokady zapisu klucza hello jest zajęta.</span><span class="sxs-lookup"><span data-stu-id="831db-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="831db-115">Tak, jeśli tooadd wartościami hello wątków 2 (lub więcej) klucza na powitania sam jeden wątek będzie uzyskanie blokady zapisu hello i hello inne wątki zablokuje czasu.</span><span class="sxs-lookup"><span data-stu-id="831db-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="831db-116">Domyślnie blok metod blokadę too4 sekund tooacquire hello; po 4 sekundy metody hello throw TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="831db-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="831db-117">Przeciążenia metody istnieje dzięki czemu możesz toopass wartość limitu czasu jawne, jeśli chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="831db-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="831db-118">Zazwyczaj zapisu tooa tooreact Twojego kodu TimeoutException przez Przechwytywanie go i ponawianie operacji całego hello (jak pokazano w powyższym kodzie hello).</span><span class="sxs-lookup"><span data-stu-id="831db-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="831db-119">W kodzie proste wywoływany tylko Task.Delay przekazywanie każdorazowo 100 milisekund.</span><span class="sxs-lookup"><span data-stu-id="831db-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="831db-120">Ale w rzeczywistości może być lepiej zamiast określonego rodzaju wykładniczego wycofywania opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="831db-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="831db-121">Po hello blokada jest uzyskiwana, AddAsync dodaje klucz hello i tooan wewnętrzny słownika tymczasowego skojarzone z obiektem ITransaction hello odwołuje się do obiektu wartości.</span><span class="sxs-lookup"><span data-stu-id="831db-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="831db-122">Jest to realizowane tooprovide z semantyki odczytu your właścicielem zapisu.</span><span class="sxs-lookup"><span data-stu-id="831db-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="831db-123">Oznacza to, że po wywołaniu metody AddAsync, nowsze tooTryGetValueAsync wywołania (przy użyciu hello tego samego obiektu ITransaction) zwróci wartość hello, nawet jeśli nie zostały jeszcze przekazane hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="831db-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="831db-124">Następnie AddAsync serializuje klucz i wartość obiekty tablice toobyte i dołącza te pliku dziennika bajtów tablice tooa w węźle lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="831db-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="831db-125">Na koniec AddAsync wysyła hello bajtów tablice tooall hello replik pomocniczych tak ma hello tego samego klucza i wartości informacji.</span><span class="sxs-lookup"><span data-stu-id="831db-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="831db-126">Nawet jeśli informacje klucza i wartości hello został zapisany plik dziennika tooa, informacji hello jest uważana za część słownika hello przed przekazaniem hello transakcji, które są skojarzone.</span><span class="sxs-lookup"><span data-stu-id="831db-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="831db-127">W powyższym kodzie hello tooCommitAsync wywołania hello zatwierdza wszystkie operacje hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="831db-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="831db-128">W szczególności dołącza plik dziennika toohello zatwierdzania informacje w węźle lokalne powitania i wysyła również replikach pomocniczych hello tooall rekordu zatwierdzania hello.</span><span class="sxs-lookup"><span data-stu-id="831db-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="831db-129">Po odpowiedział kworum replik hello (większość), wszystkie dane zmiany są traktowane jako trwałe i wszystkie skojarzone z kluczy, które zostały manipulować za pośrednictwem obiektu ITransaction hello blokady są wydawane tak innych wątków/transakcji można manipulować hello tych samych kluczy i ich wartości.</span><span class="sxs-lookup"><span data-stu-id="831db-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="831db-130">Jeśli CommitAsync nie jest wywoływany (zazwyczaj powodu tooan zgłaszanego wyjątku), obiekt ITransaction hello pobiera usunięty.</span><span class="sxs-lookup"><span data-stu-id="831db-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="831db-131">Podczas usuwania obiektu ITransaction niezatwierdzone sieci szkieletowej usług dołącza przerwania informacji toohello węzła lokalnego w pliku dziennika i nic musi toobe wysyłane tooany hello replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="831db-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="831db-132">A następnie są wydawane wszystkie blokady związane z kluczy, które zostały manipulować za pośrednictwem hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="831db-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="831db-133">Typowych problemów i w jaki sposób tooavoid ich</span><span class="sxs-lookup"><span data-stu-id="831db-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="831db-134">Po zapoznaniu się z wewnętrznie działanie hello niezawodnej kolekcje, Spójrzmy na niektórych typowych wpływające.</span><span class="sxs-lookup"><span data-stu-id="831db-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="831db-135">Zobacz poniższy kod hello:</span><span class="sxs-lookup"><span data-stu-id="831db-135">See hello code below:</span></span>

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

<span data-ttu-id="831db-136">Podczas pracy ze słownikiem regularne .NET, można dodać słownika toohello klucza i wartości, a następnie zmień hello wartość właściwości (na przykład LastLogin).</span><span class="sxs-lookup"><span data-stu-id="831db-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="831db-137">Jednak ten kod nie będzie pracował prawidłowo niezawodnej słownika.</span><span class="sxs-lookup"><span data-stu-id="831db-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="831db-138">Pamiętaj na powitania dyskusji wcześniej, wywołanie hello tooAddAsync serializuje hello klucza i wartości obiektów, tablic toobyte i następnie zapisuje hello stałych tooa pliku lokalnego, a także przesyła je toohello replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="831db-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="831db-139">Jeśli później zmienić właściwość, spowoduje to zmianę wartości właściwości hello w pamięci. nie ma ona wpływu pliku lokalnego hello lub hello dane przesyłane toohello repliki.</span><span class="sxs-lookup"><span data-stu-id="831db-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="831db-140">Jeśli proces hello ulegnie awarii, co znajduje się w pamięci jest odrzucone.</span><span class="sxs-lookup"><span data-stu-id="831db-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="831db-141">Podczas uruchamiania nowego procesu, lub jeśli inny replika staje się podstawowym, hello stara wartość właściwości jest, co jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="831db-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="831db-142">Nie można podkreślają, wystarczająco jak łatwo jest toomake hello rodzaju błędu przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="831db-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="831db-143">I uzyskasz tylko informacje na temat błędu hello Jeśli się się, że proces hello przestanie działać.</span><span class="sxs-lookup"><span data-stu-id="831db-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="831db-144">Kod hello toowrite prawidłowy sposób Hello jest po prostu tooreverse hello dwa wiersze:</span><span class="sxs-lookup"><span data-stu-id="831db-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="831db-145">Inny przykład przedstawiający powszechnym błędem jest następujący:</span><span class="sxs-lookup"><span data-stu-id="831db-145">Here is another example showing a common mistake:</span></span>

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

<span data-ttu-id="831db-146">Ponownie z regularne .NET słowników, powyższym kodzie hello działa prawidłowo i jest wspólnym wzorcem: hello deweloperów używa klucza toolook wartości.</span><span class="sxs-lookup"><span data-stu-id="831db-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="831db-147">Jeśli istnieje wartość hello, deweloperów hello zmieni się wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="831db-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="831db-148">Jednak z kolekcjami niezawodne, ten kod wykazuje hello sam problem jak już omówione: **nie należy zmodyfikować obiekt po hrweb przekazali tooa niezawodnej kolekcji.**</span><span class="sxs-lookup"><span data-stu-id="831db-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="831db-149">Witaj poprawne tooupdate sposób wartości w zbiorze niezawodnej jest tooget toohello odwołania istniejącą wartość i należy wziąć pod uwagę hello obiektu określonego tooby to odwołanie niezmienialny.</span><span class="sxs-lookup"><span data-stu-id="831db-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="831db-150">Następnie utwórz nowy obiekt, który jest dokładna kopia oryginalnego obiektu hello.</span><span class="sxs-lookup"><span data-stu-id="831db-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="831db-151">Teraz można zmodyfikować hello stan tego nowego obiektu i zapisu hello nowego obiektu do kolekcji hello tak, aby go serializowana toobyte stałych toohello dołączany plik lokalny i wysyłane toohello repliki.</span><span class="sxs-lookup"><span data-stu-id="831db-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="831db-152">Po zatwierdzania hello zmiany hello obiektów w pamięci, hello lokalnego pliku i wszystkie repliki hello mają hello dokładnie takie same stanu.</span><span class="sxs-lookup"><span data-stu-id="831db-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="831db-153">Wszystko to dobry!</span><span class="sxs-lookup"><span data-stu-id="831db-153">All is good!</span></span>

<span data-ttu-id="831db-154">Witaj poniższy kod tooupdate prawidłowy sposób hello wartość w niezawodnej kolekcji:</span><span class="sxs-lookup"><span data-stu-id="831db-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="831db-155">Zdefiniuj błąd programisty tooprevent typy niezmienne danych</span><span class="sxs-lookup"><span data-stu-id="831db-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="831db-156">Najlepiej, jeśli chcemy hello tooreport błędów podczas przypadkowo tworzy kod, który mutuje stan obiektu czy możesz powinni tooconsider niezmienialny.</span><span class="sxs-lookup"><span data-stu-id="831db-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="831db-157">Jednak hello kompilator języka C# nie ma toodo możliwości hello to.</span><span class="sxs-lookup"><span data-stu-id="831db-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="831db-158">Tak, tooavoid potencjalnych programisty usterki, zdecydowanie zaleca się zdefiniowanie typów hello, używanego z typami niezmienne kolekcje niezawodnej toobe.</span><span class="sxs-lookup"><span data-stu-id="831db-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="831db-159">W szczególności oznacza to, że trzymaj toocore typy wartości (takie jak numery [Int32, UInt64, itp.], DateTime, Guid, TimeSpan i hello, takich jak).</span><span class="sxs-lookup"><span data-stu-id="831db-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="831db-160">A, można również użyć ciągu.</span><span class="sxs-lookup"><span data-stu-id="831db-160">And, of course, you can also use String.</span></span> <span data-ttu-id="831db-161">Jest on właściwości kolekcji tooavoid najlepszego jako serializacji i deserializacji je można często może pogarszać wydajność.</span><span class="sxs-lookup"><span data-stu-id="831db-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="831db-162">Jednak jeśli chcesz toouse właściwości kolekcji, zdecydowanie zaleca się użycie hello. Biblioteka obsługi kolekcji niezmienialnych w sieci ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="831db-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="831db-163">Ta biblioteka jest dostępny do pobrania http://nuget.org. Zalecamy również pieczętowania klas i oznaczanie pola tylko do odczytu, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="831db-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="831db-164">Hello typ informacji o użytkowniku poniżej pokazano, jak toodefine jako niezmienialny wpisz, korzystając z wyżej wymienionych zalecenia.</span><span class="sxs-lookup"><span data-stu-id="831db-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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

<span data-ttu-id="831db-165">Hello ItemId typu jest również niezmiennego typu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="831db-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="831db-166">Przechowywanie wersji schematu (uaktualnienia)</span><span class="sxs-lookup"><span data-stu-id="831db-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="831db-167">Wewnętrznie niezawodne kolekcje serializować obiektów przy użyciu. DataContractSerializer w sieci.</span><span class="sxs-lookup"><span data-stu-id="831db-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="831db-168">Hello serializować obiektów są dysku lokalnym utrwalonego toohello repliki podstawowej i również przesyłane toohello replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="831db-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="831db-169">Miarę rozwoju usługi, prawdopodobnie będzie toochange hello rodzaj danych (schemat) wymaga Twoja usługa.</span><span class="sxs-lookup"><span data-stu-id="831db-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="831db-170">Przechowywanie wersji danych bardzo ostrożnie musi osiągają.</span><span class="sxs-lookup"><span data-stu-id="831db-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="831db-171">Najpierw i, musi być zawsze możliwe toodeserialize stare dane.</span><span class="sxs-lookup"><span data-stu-id="831db-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="831db-172">W szczególności, oznacza to, deserializacji kodu musi być nieograniczonej zapewniającej: wersja 333 kodu usługi musi być możliwe toooperate na dane umieszczone w niezawodnej kolekcji w wersji 1 kodu usługi 5 lat temu.</span><span class="sxs-lookup"><span data-stu-id="831db-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="831db-173">Ponadto kodu usługi jest uaktualniony jedną domenę uaktualnienia naraz.</span><span class="sxs-lookup"><span data-stu-id="831db-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="831db-174">Tak podczas uaktualniania, masz dwie różne wersje kodu usługi uruchomione jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="831db-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="831db-175">Należy uniknąć hello nową wersję kodu usługi Użyj nowego schematu hello jako stare wersje kodu usługi może nie być możliwe toohandle hello nowego schematu.</span><span class="sxs-lookup"><span data-stu-id="831db-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="831db-176">Jeśli to możliwe, należy projektować w każdej wersji usługi zgodne wprzód toobe w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="831db-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="831db-177">W szczególności, oznacza to, że V1 kodu usługi powinno być możliwe toosimply Ignoruj jawnie nie obsługuje elementów schematu.</span><span class="sxs-lookup"><span data-stu-id="831db-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="831db-178">Jednak musi być możliwe toosave, wszelkie dane nie jawnie wiedzieć o, a po prostu zapisać go z powrotem się podczas aktualizowania klucza słownika lub wartość.</span><span class="sxs-lookup"><span data-stu-id="831db-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="831db-179">Podczas gdy można zmodyfikować schematu hello klucza, należy się upewnić, skrótu swój klucz i algorytmy equals są stałe.</span><span class="sxs-lookup"><span data-stu-id="831db-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="831db-180">Jeśli zmienisz sposób działania albo te algorytmy, nie będzie możliwe toolook klucz hello w ramach niezawodnej słownika hello kiedykolwiek ponownie.</span><span class="sxs-lookup"><span data-stu-id="831db-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="831db-181">Alternatywnie można wykonywać, co jest zazwyczaj określonego tooas 2-etapowego uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="831db-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="831db-182">Uaktualnianie Faza 2, uaktualnij usługę z V1 tooV2: V2 zawiera hello kod, który zna jak toodeal z hello nowej zmiany schematu, ale ten kod nie jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="831db-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="831db-183">Gdy hello V2 kod odczytuje dane V1, działa na nim i zapisuje dane w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="831db-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="831db-184">Następnie po zakończeniu uaktualniania hello we wszystkich domenach uaktualnienia, możesz może jakiś sposób sygnał toohello uruchomionych wystąpień V2, że uaktualnienie hello jest pełny.</span><span class="sxs-lookup"><span data-stu-id="831db-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="831db-185">(Jednokierunkowej toosignal to tooroll się uaktualnienie konfiguracji; jest to, co sprawia, że to uaktualnienie fazy 2.) Teraz wystąpień V2 hello można odczytanie danych V1, przekonwertuj go tooV2 danych, wykonywać na nich operacje i zapisz je jako dane V2.</span><span class="sxs-lookup"><span data-stu-id="831db-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="831db-186">Jeśli inne wystąpienia odczytu danych V2, nie muszą oni tooconvert, po prostu działają na nim, a także zapisać danych w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="831db-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="831db-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="831db-187">Next Steps</span></span>
<span data-ttu-id="831db-188">Zobacz toolearn o tworzeniu kontrakty przekazywania danych zgodne [kontrakty danych zgodne z nowszymi](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="831db-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="831db-189">najlepsze praktyki toolearn na przechowywanie wersji kontraktów danych, zobacz [przechowywanie wersji kontraktów danych](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="831db-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="831db-190">toolearn umów tooimplement wersji na uszkodzenia danych, zobacz [wywołania zwrotne serializacji z tolerancją dla wersji](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="831db-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="831db-191">toolearn tooprovide to struktura danych, która może współdziałać w różnych wersjach, zobacz temat [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="831db-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
