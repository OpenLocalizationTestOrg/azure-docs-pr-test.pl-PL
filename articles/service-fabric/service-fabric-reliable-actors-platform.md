---
title: "Reliable Actors w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opisuje sposób Reliable Actors są warstwowy na niezawodne usługi i korzystać z funkcji platformy sieć szkieletowa usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="0de2d-103">Jak elementy Reliable Actors korzystają z platformy usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0de2d-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="0de2d-104">W tym artykule opisano, jak Reliable Actors działają na platformie Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0de2d-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="0de2d-105">Wywołuje Reliable Actors uruchomienia w ramach obsługiwanej w implementacji usługi stanowej niezawodnej *usługi aktora*.</span><span class="sxs-lookup"><span data-stu-id="0de2d-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="0de2d-106">Usługa aktora zawiera składniki niezbędne do zarządzania cyklem życia i komunikat podczas wysyłania do sieci złośliwych użytkowników:</span><span class="sxs-lookup"><span data-stu-id="0de2d-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="0de2d-107">Środowisko uruchomieniowe aktora zarządza cykl życia, wyrzucanie elementów bezużytecznych i wymusza jednowątkowe dostęp.</span><span class="sxs-lookup"><span data-stu-id="0de2d-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="0de2d-108">Odbiornik komunikacji zdalnej usługi aktora akceptuje wywołań złośliwych użytkowników dostępu zdalnego i wysyła je do dyspozytora rozesłać do wystąpienia odpowiednie aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="0de2d-109">Dostawca stanu aktora opakowuje dostawców stanu (na przykład dostawcy stanu niezawodnej kolekcje) i udostępnia adapter dla zarządzania stanem aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="0de2d-110">Te składniki tworzą razem framework niezawodnego aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="0de2d-111">Tworzenie warstw usługi</span><span class="sxs-lookup"><span data-stu-id="0de2d-111">Service layering</span></span>
<span data-ttu-id="0de2d-112">Ponieważ sama usługa aktora jest niezawodnej usługi, wszystkie [model aplikacji](service-fabric-application-model.md), cykl życia, [pakowania](service-fabric-package-apps.md), [wdrożenia](service-fabric-deploy-remove-applications.md), uaktualnianie i skalowanie pojęcia niezawodne usługi Zastosuj ten sam sposób, aby usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Tworzenie warstw usługi aktora][1]

<span data-ttu-id="0de2d-114">Na powyższym diagramie przedstawiono związek między struktur aplikacji usługi Service Fabric i kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0de2d-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="0de2d-115">Niebieski elementy reprezentują usługi niezawodnej struktury aplikacji, orange reprezentuje framework niezawodnego aktora i zielony reprezentuje kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0de2d-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="0de2d-116">W usługach niezawodnej usługi dziedziczy `StatefulService` klasy.</span><span class="sxs-lookup"><span data-stu-id="0de2d-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="0de2d-117">Ta klasa jest pochodną `StatefulServiceBase` (lub `StatelessService` usług bezstanowych).</span><span class="sxs-lookup"><span data-stu-id="0de2d-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="0de2d-118">W Reliable Actors możesz użyć usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="0de2d-119">Usługa aktora jest różne implementacje `StatefulServiceBase` klasy, która implementuje wzorca aktora, gdzie uruchomić sieci złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0de2d-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="0de2d-120">Ponieważ sama usługa aktora jest po prostu implementacją `StatefulServiceBase`, można napisać własne usługi, która pochodzi z `ActorService` i implementuje funkcje na poziomie usługi tak samo jak w przypadku dziedziczenia `StatefulService`, takich jak:</span><span class="sxs-lookup"><span data-stu-id="0de2d-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="0de2d-121">Usługa tworzenia kopii zapasowej i przywracania.</span><span class="sxs-lookup"><span data-stu-id="0de2d-121">Service backup and restore.</span></span>
* <span data-ttu-id="0de2d-122">Udostępnione funkcji dla wszystkich podmiotów, na przykład wyłącznika.</span><span class="sxs-lookup"><span data-stu-id="0de2d-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="0de2d-123">Zdalne wywoływanie procedur w samej usługi aktora i na każdym poszczególnych aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="0de2d-124">Stanowe usług nie są obecnie obsługiwane w języku Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="0de2d-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="0de2d-125">Przy użyciu usługi aktora</span><span class="sxs-lookup"><span data-stu-id="0de2d-125">Using the actor service</span></span>
<span data-ttu-id="0de2d-126">Wystąpienia aktora mają dostęp do usługi aktora, w którym jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="0de2d-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="0de2d-127">Za pośrednictwem usługi aktora wystąpień aktora programowo może uzyskać kontekstu usługi.</span><span class="sxs-lookup"><span data-stu-id="0de2d-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="0de2d-128">Kontekst usługi zawiera identyfikator partycji, nazwę usługi, nazwa aplikacji i inne informacje specyficzne dla platformy Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="0de2d-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="0de2d-129">Podobnie jak wszystkie niezawodnej usługi usługi aktora musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa typ usługi.</span><span class="sxs-lookup"><span data-stu-id="0de2d-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="0de2d-130">Dla usługi aktora do uruchomienia wystąpień z aktorem danego typu aktora musi być zarejestrowany w usłudze aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="0de2d-131">`ActorRuntime` Metoda rejestracji wykonuje tej pracy dla osób.</span><span class="sxs-lookup"><span data-stu-id="0de2d-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="0de2d-132">Ogólnie rzecz biorąc można zarejestrować tylko danego typu aktora i usługi aktora z ustawieniami domyślnymi niejawnie będą używane:</span><span class="sxs-lookup"><span data-stu-id="0de2d-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="0de2d-133">Alternatywnie można użyć wyrażenia lambda udostępniane przez metodę rejestracji do utworzenia usługi aktora samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="0de2d-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="0de2d-134">Można następnie skonfigurować usługi aktora i utworzenia jawnie swoich wystąpień aktora, w którym można wstrzyknięcia zależności do Twojej aktora za pośrednictwem jej konstruktora:</span><span class="sxs-lookup"><span data-stu-id="0de2d-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="0de2d-135">Metody usługi aktora</span><span class="sxs-lookup"><span data-stu-id="0de2d-135">Actor service methods</span></span>
<span data-ttu-id="0de2d-136">Implementuje usługi aktora `IActorService` (C#) lub `ActorService` (języka Java), który z kolei implementuje `IService` (C#) lub `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="0de2d-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="0de2d-137">Jest to interfejs używany przez niezawodnych usług zdalnych, co pozwala na metody usług zdalnych wywołań procedur.</span><span class="sxs-lookup"><span data-stu-id="0de2d-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="0de2d-138">Zawiera metody poziomu usług, które może zostać wywołana zdalnie za pomocą usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="0de2d-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="0de2d-139">Wyliczanie złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="0de2d-139">Enumerating actors</span></span>
<span data-ttu-id="0de2d-140">Usługa aktora umożliwia klientowi wyliczyć metadane dotyczące osób, które obsługuje usługę.</span><span class="sxs-lookup"><span data-stu-id="0de2d-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="0de2d-141">Ponieważ usługa aktora jest partycjonowany usługi stanowej, wyliczenie jest wykonywane dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="0de2d-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="0de2d-142">Ponieważ każda partycja może zawierać wiele osób, wyliczenia jest zwracana jako zestaw wyników stronicowania.</span><span class="sxs-lookup"><span data-stu-id="0de2d-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="0de2d-143">Strony są zwracane przez zapoznaniem wszystkich stron.</span><span class="sxs-lookup"><span data-stu-id="0de2d-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="0de2d-144">Poniższy przykład przedstawia sposób tworzenia listy wszystkich podmiotów active w jednej partycji usługi aktora:</span><span class="sxs-lookup"><span data-stu-id="0de2d-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="0de2d-145">Usuwanie złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="0de2d-145">Deleting actors</span></span>
<span data-ttu-id="0de2d-146">Usługa aktora udostępnia również funkcję usuwania złośliwych użytkowników:</span><span class="sxs-lookup"><span data-stu-id="0de2d-146">The actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="0de2d-147">Aby uzyskać więcej informacji na temat usuwania złośliwych użytkowników i ich stan, zobacz [dokumentacji cyklu życia aktora](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0de2d-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="0de2d-148">Usługa aktora niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0de2d-148">Custom actor service</span></span>
<span data-ttu-id="0de2d-149">Za pomocą aktora lambda rejestracji, możesz zarejestrować własnej usługi aktora niestandardowej, która pochodzi z `ActorService` (C#) i `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="0de2d-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="0de2d-150">W tej usłudze aktora niestandardowych można zaimplementować własnej funkcji poziomu usług pisząc klasy usługi, która dziedziczy `ActorService` (C#) lub `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="0de2d-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="0de2d-151">Usługi aktora niestandardowych dziedziczy wszystkie funkcje środowiska uruchomieniowego aktora z `ActorService` (C#) lub `FabricActorService` (Java) i może służyć do wykonania metody usługi.</span><span class="sxs-lookup"><span data-stu-id="0de2d-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="0de2d-152">Implementowanie aktora kopii zapasowej i przywracania</span><span class="sxs-lookup"><span data-stu-id="0de2d-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="0de2d-153">W poniższym przykładzie usługi aktora niestandardowych opisuje metodę kopii zapasowych danych aktora dzięki wykorzystaniu odbiornika usługi zdalne znajduje się już w `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="0de2d-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="0de2d-154">W tym przykładzie `IMyActorService` jest umowa komunikacji zdalnej, która implementuje `IService` (C#) i `Service` (języka Java), a następnie jest implementowany przez `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="0de2d-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="0de2d-155">Dodanie tego kontraktu usługi zdalne metod na `IMyActorService` są teraz dostępne do klienta przez utworzenie zdalnym obiektem pośredniczącym za pośrednictwem `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="0de2d-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="0de2d-156">Model aplikacji</span><span class="sxs-lookup"><span data-stu-id="0de2d-156">Application model</span></span>
<span data-ttu-id="0de2d-157">Usługi aktora są niezawodne usługi, więc model aplikacji jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="0de2d-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="0de2d-158">Jednak narzędzi kompilacji framework aktora Generowanie niektórych plików modelu aplikacji za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="0de2d-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="0de2d-159">Manifest usługi</span><span class="sxs-lookup"><span data-stu-id="0de2d-159">Service manifest</span></span>
<span data-ttu-id="0de2d-160">Narzędzia kompilacji framework aktora automatycznie generować zawartość pliku ServiceManifest.xml usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="0de2d-161">Ten plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="0de2d-161">This file includes:</span></span>

* <span data-ttu-id="0de2d-162">Typ usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-162">Actor service type.</span></span> <span data-ttu-id="0de2d-163">Nazwa typu jest generowany na podstawie nazwy projektu z aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="0de2d-164">Na podstawie trwałości atrybutu na Twoje aktora, HasPersistedState zostanie również ustawiona flaga odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="0de2d-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="0de2d-165">Pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="0de2d-165">Code package.</span></span>
* <span data-ttu-id="0de2d-166">Pakiet konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0de2d-166">Config package.</span></span>
* <span data-ttu-id="0de2d-167">Zasoby i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="0de2d-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="0de2d-168">Manifest aplikacji</span><span class="sxs-lookup"><span data-stu-id="0de2d-168">Application manifest</span></span>
<span data-ttu-id="0de2d-169">Narzędzia kompilacji framework aktora automatyczne tworzenie definicji domyślnej usługi dla usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="0de2d-170">Narzędzia kompilacji wypełniania właściwości usługi domyślne:</span><span class="sxs-lookup"><span data-stu-id="0de2d-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="0de2d-171">Liczba zestawu replik jest określana przez atrybut trwałości na Twoje aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="0de2d-172">Zawsze, gdy atrybut trwałości na Twoje aktora została zmieniona, liczba zestawu replik w definicji domyślnej usługi zostanie zresetowany odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="0de2d-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="0de2d-173">Schemat partycji i zakres są ustawione na jednolitych Int64 z pełnego zakresu klucza Int64.</span><span class="sxs-lookup"><span data-stu-id="0de2d-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="0de2d-174">Pojęcia dotyczące partycji usługi sieć szkieletowa osób</span><span class="sxs-lookup"><span data-stu-id="0de2d-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="0de2d-175">Usługi aktora są podzielone na partycje usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="0de2d-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="0de2d-176">Każda partycja usługi aktora zawiera zestaw złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0de2d-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="0de2d-177">Partycji usługi są automatycznie dystrybuowane za pośrednictwem wiele węzłów w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="0de2d-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="0de2d-178">W związku z tym rozpowszechnianych wystąpień aktora.</span><span class="sxs-lookup"><span data-stu-id="0de2d-178">Actor instances are distributed as a result.</span></span>

![Aktora partycjonowania i dystrybucji][5]

<span data-ttu-id="0de2d-180">Niezawodne usługi mogą być tworzone z różnych partycji, systemów i zakresami kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="0de2d-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="0de2d-181">Usługa aktora wykorzystuje schemat partycjonowania Int64 z pełnego zakresu klucza Int64 do mapowania złośliwych użytkowników do partycji.</span><span class="sxs-lookup"><span data-stu-id="0de2d-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="0de2d-182">Identyfikator aktora</span><span class="sxs-lookup"><span data-stu-id="0de2d-182">Actor ID</span></span>
<span data-ttu-id="0de2d-183">Każdy aktora utworzony w usłudze ma unikatowy identyfikator skojarzony z nim reprezentowany przez `ActorId` klasy.</span><span class="sxs-lookup"><span data-stu-id="0de2d-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="0de2d-184">`ActorId`to wartość Identyfikatora nieprzezroczyste, która może służyć do dystrybucji uniform podmiotów między partycji usługi przez Generowanie losowe identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="0de2d-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="0de2d-185">Każdy `ActorId` jest wartość skrótu do postaci liczby Int64.</span><span class="sxs-lookup"><span data-stu-id="0de2d-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="0de2d-186">Jest to, dlaczego usługa aktora musi używać schemat partycjonowania Int64 z pełnego zakresu klucza Int64.</span><span class="sxs-lookup"><span data-stu-id="0de2d-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="0de2d-187">Jednak można używać niestandardowej wartości Identyfikatora dla `ActorID`, w tym identyfikatory GUID/UUID, ciągi i Int64s.</span><span class="sxs-lookup"><span data-stu-id="0de2d-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="0de2d-188">Podczas korzystania z identyfikatorów GUID/UUID i ciągi, wartości są wartość skrótu do postaci liczby Int64.</span><span class="sxs-lookup"><span data-stu-id="0de2d-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="0de2d-189">Jednak gdy możesz jest jawnie dostarczanie Int64 do `ActorId`, Int64 przypisze bezpośrednio do partycji bez dalszego wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="0de2d-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="0de2d-190">Można użyć tej metody do partycji, których podmioty są umieszczane w kontroli.</span><span class="sxs-lookup"><span data-stu-id="0de2d-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0de2d-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0de2d-191">Next steps</span></span>
* [<span data-ttu-id="0de2d-192">Zarządzanie stanem aktora</span><span class="sxs-lookup"><span data-stu-id="0de2d-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="0de2d-193">Aktora cykl życia i odzyskiwanie pamięci</span><span class="sxs-lookup"><span data-stu-id="0de2d-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="0de2d-194">Dokumentacji interfejsu API złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="0de2d-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="0de2d-195">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="0de2d-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0de2d-196">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="0de2d-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
