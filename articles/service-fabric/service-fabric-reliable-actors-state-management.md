---
title: "Zarządzanie stanem Reliable Actors | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="092e5-103">Zarządzanie stanem podmiotów niezawodnej</span><span class="sxs-lookup"><span data-stu-id="092e5-103">Reliable Actors state management</span></span>
<span data-ttu-id="092e5-104">Reliable Actors są jednowątkowych obiektów hermetyzacji zarówno logiki i stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="092e5-105">Ponieważ podmioty są uruchamiane na niezawodne usługi, ich niezawodnie zachowują stan, przy użyciu tego samego stanu trwałego i mechanizmów replikacji, które używa niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="092e5-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="092e5-106">W ten sposób złośliwych użytkowników nie utracili ich stanu po awariach po ponownej aktywacji po wyrzucanie elementów bezużytecznych lub po przeniesieniu ich między węzłami w klastrze równoważenia zasobów lub uaktualnień.</span><span class="sxs-lookup"><span data-stu-id="092e5-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="092e5-107">Trwałość stanu i replikacji</span><span class="sxs-lookup"><span data-stu-id="092e5-107">State persistence and replication</span></span>
<span data-ttu-id="092e5-108">Uwzględniane są wszystkie Reliable Actors *stateful* ponieważ każde wystąpienie aktora jest mapowany na unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="092e5-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="092e5-109">Oznacza to, że ten sam identyfikator aktora powtarzane wywołania są kierowane do tego samego wystąpienia aktora.</span><span class="sxs-lookup"><span data-stu-id="092e5-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="092e5-110">W systemie bezstanowych natomiast wywołań klienta nie ma gwarancji być kierowane do tego samego serwera zawsze.</span><span class="sxs-lookup"><span data-stu-id="092e5-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="092e5-111">Z tego powodu usługi aktora są zawsze usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="092e5-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="092e5-112">Mimo że podmioty są traktowane jako wartość, która oznacza to, że ich musi niezawodne przechowywanie stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="092e5-113">Złośliwych użytkowników można wybrać poziom trwałości stanu i replikacji na podstawie ich danych wymagania dotyczące magazynu:</span><span class="sxs-lookup"><span data-stu-id="092e5-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="092e5-114">**Stan utrwalony**: stan jest zachowywany na dysku i jest replikowany do replik 3 lub więcej.</span><span class="sxs-lookup"><span data-stu-id="092e5-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="092e5-115">Jest to najbardziej niezawodna opcji magazynu stanu gdzie stan może się powtarzać, za pośrednictwem awarii całego klastra.</span><span class="sxs-lookup"><span data-stu-id="092e5-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="092e5-116">**Stan volatile**: stan jest replikowana do replik 3 lub więcej i tylko przechowywany w pamięci.</span><span class="sxs-lookup"><span data-stu-id="092e5-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="092e5-117">Zapewnia odporność względem awarii węzła i niepowodzenie aktora oraz podczas uaktualniania i równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="092e5-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="092e5-118">Jednak stan nie jest zachowywany na dysku.</span><span class="sxs-lookup"><span data-stu-id="092e5-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="092e5-119">Jeśli więc wszystkie repliki zostaną utracone na raz, stan utracone również.</span><span class="sxs-lookup"><span data-stu-id="092e5-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="092e5-120">**Nie stanu utrwalonego**: stan nie jest replikowany lub zapisany na dysku.</span><span class="sxs-lookup"><span data-stu-id="092e5-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="092e5-121">Ten poziom jest osób, które nie wymagają po prostu do zarządzania stanem niezawodnie.</span><span class="sxs-lookup"><span data-stu-id="092e5-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="092e5-122">Każdy poziom trwałości jest po prostu inną *dostawcy stanu* i *replikacji* konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="092e5-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="092e5-123">Określa, czy stan jest zapisywany na dysku jest zależna od dostawcy stanu — składnik w niezawodnej usługi, która przechowuje stan.</span><span class="sxs-lookup"><span data-stu-id="092e5-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="092e5-124">Zależy od liczby replikami usługa jest wdrażana z replikacji.</span><span class="sxs-lookup"><span data-stu-id="092e5-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="092e5-125">Podobnie jak w przypadku niezawodne usługi dostawcy stanu i liczby replik można łatwo skonfigurować ręcznie.</span><span class="sxs-lookup"><span data-stu-id="092e5-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="092e5-126">Framework aktora udostępnia atrybut, gdy używany na aktora, automatycznie wybiera domyślny dostawca stanu i automatycznie generuje ustawienia liczby replik osiągnięcie jednego z tych trzech ustawień trwałości.</span><span class="sxs-lookup"><span data-stu-id="092e5-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="092e5-127">Atrybut StatePersistence nie jest dziedziczone przez klasy pochodnej, podać jego poziom StatePersistence każdego typu aktora.</span><span class="sxs-lookup"><span data-stu-id="092e5-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="092e5-128">Stan utrwalony</span><span class="sxs-lookup"><span data-stu-id="092e5-128">Persisted state</span></span>
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
<span data-ttu-id="092e5-129">To ustawienie powoduje użycie dostawcy stanu, która przechowuje dane na dysku i automatycznie ustawia liczbę repliki usługi do 3.</span><span class="sxs-lookup"><span data-stu-id="092e5-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="092e5-130">Stan nietrwałe</span><span class="sxs-lookup"><span data-stu-id="092e5-130">Volatile state</span></span>
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
<span data-ttu-id="092e5-131">To ustawienie korzysta z dostawcy stanu w pamięci wyłącznie- i ustawia liczby replik 3.</span><span class="sxs-lookup"><span data-stu-id="092e5-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="092e5-132">Nie stanu utrwalonego</span><span class="sxs-lookup"><span data-stu-id="092e5-132">No persisted state</span></span>
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
<span data-ttu-id="092e5-133">To ustawienie korzysta z dostawcy stanu w pamięci — tylko i ustawia liczbę replik równą 1.</span><span class="sxs-lookup"><span data-stu-id="092e5-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="092e5-134">Wygenerowany ustawienia i wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="092e5-134">Defaults and generated settings</span></span>
<span data-ttu-id="092e5-135">Jeśli używasz `StatePersistence` atrybutu, dostawcy stanu jest automatycznie wybrana w czasie wykonywania podczas uruchamiania usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="092e5-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="092e5-136">Liczba replik, jednak jest ustawiony w czasie kompilacji za pomocą narzędzi Visual Studio aktora kompilacji.</span><span class="sxs-lookup"><span data-stu-id="092e5-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="092e5-137">Narzędzia kompilacji automatycznego generowania *usługi domyślnej* usługi aktora w pliku ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="092e5-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="092e5-138">Parametry są tworzone dla **rozmiar zestawu replik min** i **rozmiar zestawu replik docelowej**.</span><span class="sxs-lookup"><span data-stu-id="092e5-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="092e5-139">Te parametry można zmienić ręcznie.</span><span class="sxs-lookup"><span data-stu-id="092e5-139">You can change these parameters manually.</span></span> <span data-ttu-id="092e5-140">Ale zawsze `StatePersistence` zmiany atrybutu, parametry zostaną ustawione na wartości domyślne rozmiar zestawu replik dla wybranego `StatePersistence` atrybutu zastąpienie poprzedniej wartości.</span><span class="sxs-lookup"><span data-stu-id="092e5-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="092e5-141">Innymi słowy, są ustawiane w pliku ServiceManifest.xml wartości *tylko* zastąpione w czasie kompilacji zmiana `StatePersistence` wartość atrybutu.</span><span class="sxs-lookup"><span data-stu-id="092e5-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="092e5-142">Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="092e5-142">State manager</span></span>
<span data-ttu-id="092e5-143">Każde wystąpienie aktora ma własną Menedżer stanu: struktura typu słownika danych, która w niezawodny sposób przechowuje par klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="092e5-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="092e5-144">Menedżer stanów jest otokę dostawcy stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="092e5-145">Można go użyć do przechowywania danych, niezależnie od tego, które jest używane ustawienie trwałości.</span><span class="sxs-lookup"><span data-stu-id="092e5-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="092e5-146">Nie ma żadnej gwarancji, że można zmienić uruchomionej usługi aktora z ustawienie volatile (w pamięci —) stanie tylko do ustawienia stanu utrwalonego za pomocą uaktualnienia stopniowego przy zachowaniu danych.</span><span class="sxs-lookup"><span data-stu-id="092e5-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="092e5-147">Istnieje możliwość zmiany liczby replik dla uruchomionej usługi.</span><span class="sxs-lookup"><span data-stu-id="092e5-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="092e5-148">Menedżer stanu klucze muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="092e5-148">State manager keys must be strings.</span></span> <span data-ttu-id="092e5-149">Wartości są ogólne i mogą być dowolnego typu, łącznie z niestandardowych typów.</span><span class="sxs-lookup"><span data-stu-id="092e5-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="092e5-150">Wartości przechowywane w Menedżerze stanu musi być kontraktu danych, które można serializować, ponieważ mogą być przesyłane przez sieć do innych węzłów podczas replikacji i mogą być zapisywane na dysku, w zależności od ustawienia trwałości stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="092e5-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="092e5-151">Menedżer stanu przedstawia stan podobne do tych znaleziony w słowniku niezawodnej zarządzania typowe metody słownika.</span><span class="sxs-lookup"><span data-stu-id="092e5-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="092e5-152">Uzyskiwanie dostępu do stanu</span><span class="sxs-lookup"><span data-stu-id="092e5-152">Accessing state</span></span>
<span data-ttu-id="092e5-153">Stan jest możliwy za pośrednictwem Menedżera stanu według klucza.</span><span class="sxs-lookup"><span data-stu-id="092e5-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="092e5-154">Metody menedżera stanu są wszystkie asynchronicznego, ponieważ może wymagać We/Wy dysku, gdy podmiotów utrwalonych stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="092e5-155">Po pierwszym dostępie obiekty stanu są buforowane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="092e5-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="092e5-156">Powtórz uzyskiwanie dostępu do operacji dostępu do obiektów bezpośrednio z pamięci i zwracany synchronicznie, bez ponoszenia We/Wy dysku lub asynchroniczne przełączania kontekstu.</span><span class="sxs-lookup"><span data-stu-id="092e5-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="092e5-157">Obiekt stanu zostanie usunięty z pamięci podręcznej w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="092e5-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="092e5-158">Metoda aktora zgłasza nieobsługiwany wyjątek, po jego pobiera obiekt przez menedżera stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="092e5-159">Uaktywnieniu aktora, po dezaktywowany lub po awarii.</span><span class="sxs-lookup"><span data-stu-id="092e5-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="092e5-160">Dostawca stanu strony stanu na dysku.</span><span class="sxs-lookup"><span data-stu-id="092e5-160">The state provider pages state to disk.</span></span> <span data-ttu-id="092e5-161">To zachowanie zależy od implementacji dostawcy stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="092e5-162">Domyślny dostawca stanu dla `Persisted` ma to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="092e5-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="092e5-163">Stan można pobrać za pomocą standardowego *uzyskać* operacja, która zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java), jeśli wpis nie istnieje dla klucza:</span><span class="sxs-lookup"><span data-stu-id="092e5-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

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

<span data-ttu-id="092e5-164">Stan można również pobrać za pomocą *TryGet* metodę, która nie zgłasza, jeśli wpis nie istnieje dla klucza:</span><span class="sxs-lookup"><span data-stu-id="092e5-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="092e5-165">Zapisywanie stanu</span><span class="sxs-lookup"><span data-stu-id="092e5-165">Saving state</span></span>
<span data-ttu-id="092e5-166">Metody pobierania stanu Menedżera zwraca odwołanie do obiektu w pamięci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="092e5-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="092e5-167">Modyfikowanie tego obiektu w pamięci lokalnej wyłącznie nie powoduje jego zapisania trwałym.</span><span class="sxs-lookup"><span data-stu-id="092e5-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="092e5-168">Gdy obiekt jest pobierane z Menedżera stanu i modyfikować, należy ponownie wstawić do przez menedżera stanu można zapisać trwałym.</span><span class="sxs-lookup"><span data-stu-id="092e5-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="092e5-169">Stan można wstawić za pomocą bezwarunkowe *ustawić*, który jest odpowiednikiem `dictionary["key"] = value` składni:</span><span class="sxs-lookup"><span data-stu-id="092e5-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="092e5-170">Stan można dodać za pomocą *Dodaj* metody.</span><span class="sxs-lookup"><span data-stu-id="092e5-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="092e5-171">Ta metoda zgłasza `InvalidOperationException`(C#) lub `IllegalStateException`(Java) próbuje dodać klucz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="092e5-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="092e5-172">Stan można również dodać za pomocą *TryAdd* metody.</span><span class="sxs-lookup"><span data-stu-id="092e5-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="092e5-173">Ta metoda nie zgłasza, gdy próbuje dodać klucz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="092e5-173">This method does not throw when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="092e5-174">Na końcu metody aktora Menedżer stanu automatycznie zapisuje wartości, które zostały dodane lub zmodyfikowane przez operacji insert lub update.</span><span class="sxs-lookup"><span data-stu-id="092e5-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="092e5-175">"Zapisz" może zawierać przechowywanie na dysku i replikacji, w zależności od ustawienia używane.</span><span class="sxs-lookup"><span data-stu-id="092e5-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="092e5-176">Wartości, które nie zostały zmodyfikowane nie są zachowywane lub replikowane.</span><span class="sxs-lookup"><span data-stu-id="092e5-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="092e5-177">Jeśli wartości nie zostały zmodyfikowane, Zapisz działania nie działają.</span><span class="sxs-lookup"><span data-stu-id="092e5-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="092e5-178">Jeśli zapiszesz kończy się niepowodzeniem, zostanie odrzucony stanu modyfikacji i załadowaniu oryginalnego stanu.</span><span class="sxs-lookup"><span data-stu-id="092e5-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="092e5-179">Można także zapisać stan ręcznie przez wywołanie metody `SaveStateAsync` metody na podstawie aktora:</span><span class="sxs-lookup"><span data-stu-id="092e5-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="092e5-180">Usuwanie stanu</span><span class="sxs-lookup"><span data-stu-id="092e5-180">Removing state</span></span>
<span data-ttu-id="092e5-181">Możesz usunąć stan trwale z Menedżer stanu aktora wywołując *Usuń* metody.</span><span class="sxs-lookup"><span data-stu-id="092e5-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="092e5-182">Ta metoda zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java) podczas próby usunięcia klucz, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="092e5-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

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

<span data-ttu-id="092e5-183">Można również usunąć stan trwale przy użyciu *TryRemove* metody.</span><span class="sxs-lookup"><span data-stu-id="092e5-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="092e5-184">Ta metoda nie zgłasza podczas próby usunięcia klucza, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="092e5-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="092e5-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="092e5-185">Next steps</span></span>

<span data-ttu-id="092e5-186">Stan, który jest przechowywany w Reliable Actors musi być serializowany przed zapisany na dysku i replikowany wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="092e5-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="092e5-187">Dowiedz się więcej o [serializacji typu aktora](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="092e5-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="092e5-188">Następnie Dowiedz się więcej o [aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="092e5-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
