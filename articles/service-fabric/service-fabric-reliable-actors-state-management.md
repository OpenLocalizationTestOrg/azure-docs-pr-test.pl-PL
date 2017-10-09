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
# <a name="reliable-actors-state-management"></a><span data-ttu-id="0ae2a-103">Zarządzanie stanem podmiotów niezawodnej</span><span class="sxs-lookup"><span data-stu-id="0ae2a-103">Reliable Actors state management</span></span>
<span data-ttu-id="0ae2a-104">Reliable Actors są jednowątkowych obiektów hermetyzacji zarówno logiki i stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="0ae2a-105">Ponieważ podmioty są uruchamiane na niezawodne usługi, ich można zachować stanu niezawodnie przy użyciu hello same utrwalanie i replikację mechanizmy, które używa niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="0ae2a-106">W ten sposób złośliwych użytkowników nie utracili ich stanu po awariach po ponownej aktywacji po wyrzucanie elementów bezużytecznych lub po przeniesieniu ich między węzłami w klastrze równoważenia tooresource lub uaktualnień.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="0ae2a-107">Trwałość stanu i replikacji</span><span class="sxs-lookup"><span data-stu-id="0ae2a-107">State persistence and replication</span></span>
<span data-ttu-id="0ae2a-108">Uwzględniane są wszystkie Reliable Actors *stateful* ponieważ każde wystąpienie aktora mapuje tooa unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="0ae2a-109">Oznacza to, że toohello powtarzane wywołania są w tym samym identyfikatorze aktora kierowane toohello tego samego wystąpienia aktora.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="0ae2a-110">W systemie bezstanowych, natomiast wywołań klienta nie ma gwarancji toohello toobe kierowane tym samym serwerze co czasu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="0ae2a-111">Z tego powodu usługi aktora są zawsze usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="0ae2a-112">Mimo że podmioty są traktowane jako wartość, która oznacza to, że ich musi niezawodne przechowywanie stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="0ae2a-113">Złośliwych użytkowników można wybrać hello poziom trwałości stanu i replikacji na podstawie ich danych wymagania dotyczące magazynu:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="0ae2a-114">**Stan utrwalony**: stanu utrwalonego toodisk i jest replikowany too3 lub więcej repliki.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="0ae2a-115">To hello najbardziej niezawodna opcji magazynu stanu, gdy stan może się powtarzać, za pośrednictwem awarii całego klastra.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="0ae2a-116">**Stan volatile**: stan jest replikowany too3 lub więcej repliki i tylko przechowywany w pamięci.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="0ae2a-117">Zapewnia odporność względem awarii węzła i niepowodzenie aktora oraz podczas uaktualniania i równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="0ae2a-118">Stan nie jest jednak toodisk utrwalonych.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="0ae2a-119">Jeśli więc wszystkie repliki zostaną utracone na raz, stan hello utracone również.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="0ae2a-120">**Nie stanu utrwalonego**: stan nie jest replikowany lub zapisywane toodisk.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="0ae2a-121">Ten poziom jest osób, które po prostu nie wymagają niezawodnie toomaintain stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="0ae2a-122">Każdy poziom trwałości jest po prostu inną *dostawcy stanu* i *replikacji* konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="0ae2a-123">Czy stan jest zapisywany toodisk zależy od dostawcy stanu hello — składnik hello w niezawodnej usługi, która przechowuje stan.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="0ae2a-124">Zależy od liczby replikami usługa jest wdrażana z replikacji.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="0ae2a-125">Podobnie jak w przypadku niezawodne usługi zarówno hello dostawcy stanu i liczby replik można łatwo ręcznie skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="0ae2a-126">Witaj aktora framework zapewnia atrybutu, gdy jest używany na aktora automatycznie wybiera domyślny dostawca stanu i automatycznie generuje ustawienia tooachieve liczby replik, jednego z tych trzech ustawień trwałości.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="0ae2a-127">Atrybut StatePersistence Hello nie jest dziedziczone przez klasy pochodnej, podać jego poziom StatePersistence każdego typu aktora.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="0ae2a-128">Stan utrwalony</span><span class="sxs-lookup"><span data-stu-id="0ae2a-128">Persisted state</span></span>
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
<span data-ttu-id="0ae2a-129">To ustawienie powoduje użycie dostawcy stanu, który przechowuje dane na dysku i automatycznie ustawia too3 liczby replik usługi hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="0ae2a-130">Stan nietrwałe</span><span class="sxs-lookup"><span data-stu-id="0ae2a-130">Volatile state</span></span>
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
<span data-ttu-id="0ae2a-131">To ustawienie powoduje użycie dostawcy stanu w pamięci wyłącznie- i ustawia hello too3 liczby replik.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="0ae2a-132">Nie stanu utrwalonego</span><span class="sxs-lookup"><span data-stu-id="0ae2a-132">No persisted state</span></span>
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
<span data-ttu-id="0ae2a-133">To ustawienie powoduje użycie dostawcy stanu w pamięci wyłącznie- i ustawia hello too1 liczby replik.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="0ae2a-134">Wygenerowany ustawienia i wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="0ae2a-134">Defaults and generated settings</span></span>
<span data-ttu-id="0ae2a-135">Jeśli używasz hello `StatePersistence` atrybutu, dostawcy stanu jest automatycznie wybrana w czasie wykonywania podczas uruchamiania usługi aktora hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="0ae2a-136">liczba replik Hello, jednak jest ustawiony w czasie kompilacji przez hello aktora Visual Studio narzędzia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="0ae2a-137">Witaj narzędzia kompilacji automatycznego generowania *usługi domyślnej* hello usługi aktora w pliku ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="0ae2a-138">Parametry są tworzone dla **rozmiar zestawu replik min** i **rozmiar zestawu replik docelowej**.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="0ae2a-139">Te parametry można zmienić ręcznie.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-139">You can change these parameters manually.</span></span> <span data-ttu-id="0ae2a-140">Ale każdego hello czasu `StatePersistence` zmiany atrybutu, hello parametry zostały ustawione toohello repliki Ustaw rozmiar wartości domyślne hello wybrane `StatePersistence` atrybutu zastąpienie poprzedniej wartości.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="0ae2a-141">Innymi słowy, są hello wartości, które można ustawić w pliku ServiceManifest.xml *tylko* zastąpione w czasie kompilacji zmiana hello `StatePersistence` wartość atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="0ae2a-142">Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="0ae2a-142">State manager</span></span>
<span data-ttu-id="0ae2a-143">Każde wystąpienie aktora ma własną Menedżer stanu: struktura typu słownika danych, która w niezawodny sposób przechowuje par klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="0ae2a-144">Menedżer stanu Hello jest otokę dostawcy stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="0ae2a-145">Służy on toostore danych niezależnie od ustawień trwałości jest używany.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="0ae2a-146">Nie zapewnia się, że ustawienia stanu za pomocą uaktualnienia stopniowego przy zachowaniu danych utrwalone żadnej gwarancji, że uruchomionej usługi aktora można zmienić z tooa ustawienie volatile stanu (w pamięci wyłącznie-).</span><span class="sxs-lookup"><span data-stu-id="0ae2a-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="0ae2a-147">Jest jednak możliwe toochange liczba replik dla uruchomionej usługi.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="0ae2a-148">Menedżer stanu klucze muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-148">State manager keys must be strings.</span></span> <span data-ttu-id="0ae2a-149">Wartości są ogólne i mogą być dowolnego typu, łącznie z niestandardowych typów.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="0ae2a-150">Wartości przechowywane w Menedżerze stanu hello musi być kontraktu danych, które można serializować, ponieważ mogą zostać przesłane przez węzły tooother sieci hello podczas replikacji i mogą być zapisane toodisk, w zależności od ustawienia trwałości stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="0ae2a-151">Menedżer stanu Hello opisuje typowe metody słownika stan, podobne toothose znaleziony w słowniku niezawodnej zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="0ae2a-152">Uzyskiwanie dostępu do stanu</span><span class="sxs-lookup"><span data-stu-id="0ae2a-152">Accessing state</span></span>
<span data-ttu-id="0ae2a-153">Stan jest możliwy za pośrednictwem Menedżera stanu hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="0ae2a-154">Metody menedżera stanu są wszystkie asynchronicznego, ponieważ może wymagać We/Wy dysku, gdy podmiotów utrwalonych stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="0ae2a-155">Po pierwszym dostępie obiekty stanu są buforowane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="0ae2a-156">Powtórz uzyskiwanie dostępu do operacji dostępu do obiektów bezpośrednio z pamięci i zwracany synchronicznie, bez ponoszenia We/Wy dysku lub asynchroniczne przełączania kontekstu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="0ae2a-157">Obiekt stanu jest usuwane z pamięci podręcznej hello w hello w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="0ae2a-158">Metoda aktora zgłasza nieobsługiwany wyjątek, po jego pobiera obiekt z hello Menedżer stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="0ae2a-159">Uaktywnieniu aktora, po dezaktywowany lub po awarii.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="0ae2a-160">stron dostawcy stanu Hello stanu toodisk.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="0ae2a-161">To zachowanie zależy od implementacji dostawcy stanu hello.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="0ae2a-162">Witaj domyślnego dostawcę stanu hello `Persisted` ma to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="0ae2a-163">Stan można pobrać za pomocą standardowego *uzyskać* operacja, która zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java), jeśli wpis nie istnieje dla klucza hello:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="0ae2a-164">Stan można również pobrać za pomocą *TryGet* metodę, która nie zgłasza, jeśli wpis nie istnieje dla klucza:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="0ae2a-165">Zapisywanie stanu</span><span class="sxs-lookup"><span data-stu-id="0ae2a-165">Saving state</span></span>
<span data-ttu-id="0ae2a-166">metody pobierania menedżera stanu Hello zwraca obiekt tooan odwołania w lokalnej pamięci.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="0ae2a-167">Modyfikowanie tego obiektu w pamięci lokalnej wyłącznie nie powoduje jego toobe trwale zapisać.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="0ae2a-168">Gdy obiekt jest pobierane z Menedżera stanu hello i modyfikować, należy ponownie wstawić do toobe menedżera stanu hello trwale zapisać.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="0ae2a-169">Stan można wstawić za pomocą bezwarunkowe *ustawić*, jest hello odpowiednik hello `dictionary["key"] = value` składni:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="0ae2a-170">Stan można dodać za pomocą *Dodaj* metody.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="0ae2a-171">Ta metoda zgłasza `InvalidOperationException`(C#) lub `IllegalStateException`(Java) próbuje tooadd klucz, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="0ae2a-172">Stan można również dodać za pomocą *TryAdd* metody.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="0ae2a-173">Ta metoda nie zgłasza podczas próby tooadd klucz, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="0ae2a-174">Na końcu hello metodę aktora Menedżer stanu hello automatycznie zapisuje wartości, które zostały dodane lub zmodyfikowane przez operacji insert lub update.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="0ae2a-175">"Zapisz" może zawierać toodisk utrwalanie i replikację, w zależności od ustawienia hello używane.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="0ae2a-176">Wartości, które nie zostały zmodyfikowane nie są zachowywane lub replikowane.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="0ae2a-177">Jeśli wartości nie zostały zmodyfikowane, hello operacji zapisywania nie działa.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="0ae2a-178">Jeśli zapiszesz kończy się niepowodzeniem, hello stanu modyfikacji zostaną odrzucone i załadowaniu hello pierwotnego stanu.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="0ae2a-179">Można także zapisać stan ręcznie przez wywołanie hello `SaveStateAsync` metoda aktora hello podstawowej:</span><span class="sxs-lookup"><span data-stu-id="0ae2a-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="0ae2a-180">Usuwanie stanu</span><span class="sxs-lookup"><span data-stu-id="0ae2a-180">Removing state</span></span>
<span data-ttu-id="0ae2a-181">Możesz usunąć stan trwale z Menedżer stanu aktora przez wywołanie hello *Usuń* metody.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="0ae2a-182">Ta metoda zgłasza `KeyNotFoundException`(C#) lub `NoSuchElementException`(Java) próbuje tooremove klucz, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="0ae2a-183">Można również usunąć stan trwale przy użyciu hello *TryRemove* metody.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="0ae2a-184">Ta metoda nie zgłasza podczas próby tooremove klucz, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0ae2a-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ae2a-185">Next steps</span></span>

<span data-ttu-id="0ae2a-186">Stan, który jest przechowywany w Reliable Actors należy serializacji przed jego toodisk zapisywane i replikowane wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="0ae2a-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="0ae2a-187">Dowiedz się więcej o [serializacji typu aktora](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="0ae2a-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="0ae2a-188">Następnie Dowiedz się więcej o [aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0ae2a-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
