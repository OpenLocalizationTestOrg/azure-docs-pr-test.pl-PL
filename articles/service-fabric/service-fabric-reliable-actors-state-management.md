---
title: "Podmiotów aaaReliable stanu zarządzania | Dokumentacja firmy Microsoft"
description: "Opisuje sposób Reliable Actors stanu jest zarządzany, utrwalenia i replikacji wysokiej dostępności."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a>Zarządzanie stanem podmiotów niezawodnej
Reliable Actors są jednowątkowych obiektów hermetyzacji zarówno logiki i stanu. Ponieważ podmioty są uruchamiane na niezawodne usługi, ich można zachować stanu niezawodnie przy użyciu hello same utrwalanie i replikację mechanizmy, które używa niezawodne usługi. W ten sposób złośliwych użytkowników nie utracili ich stanu po awariach po ponownej aktywacji po wyrzucanie elementów bezużytecznych lub po przeniesieniu ich między węzłami w klastrze równoważenia tooresource lub uaktualnień.

## <a name="state-persistence-and-replication"></a>Trwałość stanu i replikacji
Uwzględniane są wszystkie Reliable Actors *stateful* ponieważ każde wystąpienie aktora mapuje tooa unikatowego identyfikatora. Oznacza to, że toohello powtarzane wywołania są w tym samym identyfikatorze aktora kierowane toohello tego samego wystąpienia aktora. W systemie bezstanowych, natomiast wywołań klienta nie ma gwarancji toohello toobe kierowane tym samym serwerze co czasu. Z tego powodu usługi aktora są zawsze usług stanowych.

Mimo że podmioty są traktowane jako wartość, która oznacza to, że ich musi niezawodne przechowywanie stanu. Złośliwych użytkowników można wybrać hello poziom trwałości stanu i replikacji na podstawie ich danych wymagania dotyczące magazynu:

* **Stan utrwalony**: stanu utrwalonego toodisk i jest replikowany too3 lub więcej repliki. To hello najbardziej niezawodna opcji magazynu stanu, gdy stan może się powtarzać, za pośrednictwem awarii całego klastra.
* **Stan volatile**: stan jest replikowany too3 lub więcej repliki i tylko przechowywany w pamięci. Zapewnia odporność względem awarii węzła i niepowodzenie aktora oraz podczas uaktualniania i równoważenia zasobów. Stan nie jest jednak toodisk utrwalonych. Jeśli więc wszystkie repliki zostaną utracone na raz, stan hello utracone również.
* **Nie stanu utrwalonego**: stan nie jest replikowany lub zapisywane toodisk. Ten poziom jest osób, które po prostu nie wymagają niezawodnie toomaintain stanu.

Każdy poziom trwałości jest po prostu inną *dostawcy stanu* i *replikacji* konfiguracji usługi. Czy stan jest zapisywany toodisk zależy od dostawcy stanu hello — składnik hello w niezawodnej usługi, która przechowuje stan. Zależy od liczby replikami usługa jest wdrażana z replikacji. Podobnie jak w przypadku niezawodne usługi zarówno hello dostawcy stanu i liczby replik można łatwo ręcznie skonfigurować. Witaj aktora framework zapewnia atrybutu, gdy jest używany na aktora automatycznie wybiera domyślny dostawca stanu i automatycznie generuje ustawienia tooachieve liczby replik, jednego z tych trzech ustawień trwałości. Atrybut StatePersistence Hello nie jest dziedziczone przez klasy pochodnej, podać jego poziom StatePersistence każdego typu aktora.

### <a name="persisted-state"></a>Stan utrwalony
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
To ustawienie powoduje użycie dostawcy stanu, który przechowuje dane na dysku i automatycznie ustawia too3 liczby replik usługi hello.

### <a name="volatile-state"></a>Stan nietrwałe
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
To ustawienie powoduje użycie dostawcy stanu w pamięci wyłącznie- i ustawia hello too3 liczby replik.

### <a name="no-persisted-state"></a>Nie stanu utrwalonego
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
To ustawienie powoduje użycie dostawcy stanu w pamięci wyłącznie- i ustawia hello too1 liczby replik.

### <a name="defaults-and-generated-settings"></a>Wygenerowany ustawienia i wartości domyślnych
Jeśli używasz hello `StatePersistence` atrybutu, dostawcy stanu jest automatycznie wybrana w czasie wykonywania podczas uruchamiania usługi aktora hello. liczba replik Hello, jednak jest ustawiony w czasie kompilacji przez hello aktora Visual Studio narzędzia kompilacji. Witaj narzędzia kompilacji automatycznego generowania *usługi domyślnej* hello usługi aktora w pliku ApplicationManifest.xml. Parametry są tworzone dla **rozmiar zestawu replik min** i **rozmiar zestawu replik docelowej**.

Te parametry można zmienić ręcznie. Ale każdego hello czasu `StatePersistence` zmiany atrybutu, hello parametry zostały ustawione toohello repliki Ustaw rozmiar wartości domyślne hello wybrane `StatePersistence` atrybutu zastąpienie poprzedniej wartości. Innymi słowy, są hello wartości, które można ustawić w pliku ServiceManifest.xml *tylko* zastąpione w czasie kompilacji zmiana hello `StatePersistence` wartość atrybutu.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a>Menedżer stanu
Każde wystąpienie aktora ma własną Menedżer stanu: struktura typu słownika danych, która w niezawodny sposób przechowuje par klucz/wartość. Menedżer stanu Hello jest otokę dostawcy stanu. Służy on toostore danych niezależnie od ustawień trwałości jest używany. Nie zapewnia się, że ustawienia stanu za pomocą uaktualnienia stopniowego przy zachowaniu danych utrwalone żadnej gwarancji, że uruchomionej usługi aktora można zmienić z tooa ustawienie volatile stanu (w pamięci wyłącznie-). Jest jednak możliwe toochange liczba replik dla uruchomionej usługi.

Menedżer stanu klucze muszą być ciągami. Wartości są ogólne i mogą być dowolnego typu, łącznie z niestandardowych typów. Wartości przechowywane w Menedżerze stanu hello musi być kontraktu danych, które można serializować, ponieważ mogą zostać przesłane przez węzły tooother sieci hello podczas replikacji i mogą być zapisane toodisk, w zależności od ustawienia trwałości stanu aktora.

Menedżer stanu Hello opisuje typowe metody słownika stan, podobne toothose znaleziony w słowniku niezawodnej zarządzania.

### <a name="accessing-state"></a>Uzyskiwanie dostępu do stanu
Stan jest możliwy za pośrednictwem Menedżera stanu hello według klucza. Metody menedżera stanu są wszystkie asynchronicznego, ponieważ może wymagać We/Wy dysku, gdy podmiotów utrwalonych stanu. Po pierwszym dostępie obiekty stanu są buforowane w pamięci. Powtórz uzyskiwanie dostępu do operacji dostępu do obiektów bezpośrednio z pamięci i zwracany synchronicznie, bez ponoszenia We/Wy dysku lub asynchroniczne przełączania kontekstu. Obiekt stanu jest usuwane z pamięci podręcznej hello w hello w następujących przypadkach:

* Metoda aktora zgłasza nieobsługiwany wyjątek, po jego pobiera obiekt z hello Menedżer stanu.
* Uaktywnieniu aktora, po dezaktywowany lub po awarii.
* stron dostawcy stanu Hello stanu toodisk. To zachowanie zależy od implementacji dostawcy stanu hello. Witaj domyślnego dostawcę stanu hello `Persisted` ma to zachowanie.

Stan można pobrać za pomocą standardowego *uzyskać* operacja, która zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java), jeśli wpis nie istnieje dla klucza hello:

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

Stan można również pobrać za pomocą *TryGet* metodę, która nie zgłasza, jeśli wpis nie istnieje dla klucza:

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a>Zapisywanie stanu
metody pobierania menedżera stanu Hello zwraca obiekt tooan odwołania w lokalnej pamięci. Modyfikowanie tego obiektu w pamięci lokalnej wyłącznie nie powoduje jego toobe trwale zapisać. Gdy obiekt jest pobierane z Menedżera stanu hello i modyfikować, należy ponownie wstawić do toobe menedżera stanu hello trwale zapisać.

Stan można wstawić za pomocą bezwarunkowe *ustawić*, jest hello odpowiednik hello `dictionary["key"] = value` składni:

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

Stan można dodać za pomocą *Dodaj* metody. Ta metoda zgłasza `InvalidOperationException`(C#) lub `IllegalStateException`(Java) próbuje tooadd klucz, który już istnieje.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

Stan można również dodać za pomocą *TryAdd* metody. Ta metoda nie zgłasza podczas próby tooadd klucz, który już istnieje.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

Na końcu hello metodę aktora Menedżer stanu hello automatycznie zapisuje wartości, które zostały dodane lub zmodyfikowane przez operacji insert lub update. "Zapisz" może zawierać toodisk utrwalanie i replikację, w zależności od ustawienia hello używane. Wartości, które nie zostały zmodyfikowane nie są zachowywane lub replikowane. Jeśli wartości nie zostały zmodyfikowane, hello operacji zapisywania nie działa. Jeśli zapiszesz kończy się niepowodzeniem, hello stanu modyfikacji zostaną odrzucone i załadowaniu hello pierwotnego stanu.

Można także zapisać stan ręcznie przez wywołanie hello `SaveStateAsync` metoda aktora hello podstawowej:

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a>Usuwanie stanu
Możesz usunąć stan trwale z Menedżer stanu aktora przez wywołanie hello *Usuń* metody. Ta metoda zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java) próbuje tooremove klucz, który nie istnieje.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

Można również usunąć stan trwale przy użyciu hello *TryRemove* metody. Ta metoda nie zgłasza podczas próby tooremove klucz, który nie istnieje.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a>Następne kroki

Stan, który jest przechowywany w Reliable Actors należy serializacji przed jego toodisk zapisywane i replikowane wysokiej dostępności. Dowiedz się więcej o [serializacji typu aktora](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Następnie Dowiedz się więcej o [aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md).
