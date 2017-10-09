---
title: "aaaReliable złośliwych użytkowników w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opisuje sposób Reliable Actors są warstwowego na niezawodne usługi i korzystać z funkcji hello hello platformy Service Fabric."
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
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="f37af-103">Jak używać platformy Service Fabric hello w Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f37af-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="f37af-104">W tym artykule opisano, jak Reliable Actors działają na platformie Azure Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f37af-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="f37af-105">Reliable Actors uruchomienia w ramach obsługiwanej w implementacji stanowe niezawodnej usługi o nazwie hello *usługi aktora*.</span><span class="sxs-lookup"><span data-stu-id="f37af-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="f37af-106">Usługa aktora Hello zawiera wszystkie hello składniki niezbędne toomanage hello w cyklu życia i komunikat podczas wysyłania do sieci złośliwych użytkowników:</span><span class="sxs-lookup"><span data-stu-id="f37af-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="f37af-107">Hello aktora środowiska uruchomieniowego umożliwia zarządzanie cyklem, wyrzucanie elementów bezużytecznych i wymusza jednowątkowe dostęp.</span><span class="sxs-lookup"><span data-stu-id="f37af-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="f37af-108">Odbiornik komunikacji zdalnej usługi aktora akceptuje tooactors połączeń dostępu zdalnego i wysyła je tooa dyspozytora tooroute toohello aktora odpowiednie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="f37af-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="f37af-109">Hello dostawcy stanu aktora opakowuje dostawców stanu (na przykład dostawcy stanu niezawodnej kolekcje hello) i udostępnia adapter dla zarządzania stanem aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="f37af-110">Te składniki współpracują formularza hello niezawodnego aktora framework.</span><span class="sxs-lookup"><span data-stu-id="f37af-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="f37af-111">Tworzenie warstw usługi</span><span class="sxs-lookup"><span data-stu-id="f37af-111">Service layering</span></span>
<span data-ttu-id="f37af-112">Ponieważ sama usługa aktora hello jest niezawodnej usługi, wszystkie hello [model aplikacji](service-fabric-application-model.md), cykl życia, [pakowania](service-fabric-package-apps.md), [wdrożenia](service-fabric-deploy-remove-applications.md), uaktualniania i skalowanie pojęcia związane z Niezawodne usługi zastosować hello tej samej usługi tooactor sposób.</span><span class="sxs-lookup"><span data-stu-id="f37af-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Tworzenie warstw usługi aktora][1]

<span data-ttu-id="f37af-114">Witaj wcześniejszym diagramie przedstawiono hello relacje struktur aplikacji hello sieci szkieletowej usług i kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f37af-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="f37af-115">Niebieski elementy reprezentują struktury aplikacji hello niezawodne usługi framework niezawodnego aktora hello reprezentuje kolor pomarańczowy i zielony reprezentuje kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f37af-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="f37af-116">W usługach niezawodnej usługi dziedziczy hello `StatefulService` klasy.</span><span class="sxs-lookup"><span data-stu-id="f37af-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="f37af-117">Ta klasa jest pochodną `StatefulServiceBase` (lub `StatelessService` usług bezstanowych).</span><span class="sxs-lookup"><span data-stu-id="f37af-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="f37af-118">W Reliable Actors należy użyć hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="f37af-119">Usługa aktora Hello jest inną implementację hello `StatefulServiceBase` klasy tego wzorca aktora hello implementuje gdzie uruchomić sieci złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f37af-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="f37af-120">Ponieważ właśnie implementacja jest sama usługa aktora hello `StatefulServiceBase`, można napisać własne usługi, która pochodzi z `ActorService` i funkcje na poziomie usługi wdrożenie hello sam sposób jak w przypadku dziedziczenia `StatefulService`, takich jak:</span><span class="sxs-lookup"><span data-stu-id="f37af-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="f37af-121">Usługa tworzenia kopii zapasowej i przywracania.</span><span class="sxs-lookup"><span data-stu-id="f37af-121">Service backup and restore.</span></span>
* <span data-ttu-id="f37af-122">Udostępnione funkcji dla wszystkich podmiotów, na przykład wyłącznika.</span><span class="sxs-lookup"><span data-stu-id="f37af-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="f37af-123">Zdalne wywoływanie procedur w samej usługi aktora hello i na każdym poszczególnych aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="f37af-124">Stanowe usług nie są obecnie obsługiwane w języku Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="f37af-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="f37af-125">Przy użyciu usługi aktora hello</span><span class="sxs-lookup"><span data-stu-id="f37af-125">Using hello actor service</span></span>
<span data-ttu-id="f37af-126">Wystąpienia aktora mają dostęp toohello aktora usługi, w którym jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="f37af-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="f37af-127">Za pośrednictwem usługi aktora hello wystąpień aktora programowo można uzyskać hello usługi kontekstu.</span><span class="sxs-lookup"><span data-stu-id="f37af-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="f37af-128">Kontekst usługi Hello ma identyfikator partycji: hello, nazwę usługi, nazwa aplikacji i inne informacje specyficzne dla platformy Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="f37af-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="f37af-129">Podobnie jak wszystkie niezawodnej usługi usługi aktora hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi.</span><span class="sxs-lookup"><span data-stu-id="f37af-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="f37af-130">Dla usługi aktora hello toorun swoich wystąpień aktora, danego typu aktora również musi być zarejestrowane w usłudze aktora hello.</span><span class="sxs-lookup"><span data-stu-id="f37af-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="f37af-131">Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób.</span><span class="sxs-lookup"><span data-stu-id="f37af-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="f37af-132">W przypadku najprostszym hello można zarejestrować tylko danego typu aktora i usługi aktora hello z ustawieniami domyślnymi niejawnie będą używane:</span><span class="sxs-lookup"><span data-stu-id="f37af-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="f37af-133">Alternatywnie można użyć wyrażenia lambda udostępniane przez usługa aktora hello tooconstruct hello rejestracji — metoda.</span><span class="sxs-lookup"><span data-stu-id="f37af-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="f37af-134">Można następnie skonfigurować usługi aktora hello i utworzenia jawnie swoich wystąpień aktora, w którym można wstrzyknięcia zależności tooyour aktora za pośrednictwem jej konstruktora:</span><span class="sxs-lookup"><span data-stu-id="f37af-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="f37af-135">Metody usługi aktora</span><span class="sxs-lookup"><span data-stu-id="f37af-135">Actor service methods</span></span>
<span data-ttu-id="f37af-136">Witaj implementuje usługi aktora `IActorService` (C#) lub `ActorService` (języka Java), który z kolei implementuje `IService` (C#) lub `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="f37af-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="f37af-137">Jest to interfejs hello używany łącząc niezawodne usługi, co pozwala na metody usług zdalnych wywołań procedur.</span><span class="sxs-lookup"><span data-stu-id="f37af-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="f37af-138">Zawiera metody poziomu usług, które może zostać wywołana zdalnie za pomocą usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="f37af-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="f37af-139">Wyliczanie złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="f37af-139">Enumerating actors</span></span>
<span data-ttu-id="f37af-140">Usługa aktora Hello umożliwia klientowi tooenumerate metadane dotyczące hello uczestników, obsługujące usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f37af-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="f37af-141">Ponieważ usługa aktora hello jest partycjonowany usługi stanowej, wyliczenie jest wykonywane dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="f37af-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="f37af-142">Ponieważ każda partycja może zawierać wiele osób, wyliczenie hello jest zwracana jako zestaw wyników stronicowania.</span><span class="sxs-lookup"><span data-stu-id="f37af-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="f37af-143">strony Hello są zwracane przez zapoznaniem wszystkich stron.</span><span class="sxs-lookup"><span data-stu-id="f37af-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="f37af-144">powitania po przykładzie pokazano, jak toocreate listę wszystkich podmiotów active w jednej partycji usługi aktora:</span><span class="sxs-lookup"><span data-stu-id="f37af-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="f37af-145">Usuwanie złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="f37af-145">Deleting actors</span></span>
<span data-ttu-id="f37af-146">Usługa aktora Hello udostępnia również funkcję usuwania złośliwych użytkowników:</span><span class="sxs-lookup"><span data-stu-id="f37af-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="f37af-147">Aby uzyskać więcej informacji na temat usuwania złośliwych użytkowników i ich stan, zobacz hello [dokumentacji cyklu życia aktora](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="f37af-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="f37af-148">Usługa aktora niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f37af-148">Custom actor service</span></span>
<span data-ttu-id="f37af-149">Za pomocą hello aktora rejestracji lambda, możesz zarejestrować własnej usługi aktora niestandardowej, która pochodzi z `ActorService` (C#) i `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="f37af-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="f37af-150">W tej usłudze aktora niestandardowych można zaimplementować własnej funkcji poziomu usług pisząc klasy usługi, która dziedziczy `ActorService` (C#) lub `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="f37af-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="f37af-151">Usługi aktora niestandardowych dziedziczy wszystkie funkcje środowiska uruchomieniowego aktora hello z `ActorService` (C#) lub `FabricActorService` (Java) i mogą być używane tooimplement metody usługi.</span><span class="sxs-lookup"><span data-stu-id="f37af-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="f37af-152">Implementowanie aktora kopii zapasowej i przywracania</span><span class="sxs-lookup"><span data-stu-id="f37af-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="f37af-153">W hello poniższy przykład, usługa aktora niestandardowych hello przedstawia tooback metody zapasowych aktora dzięki wykorzystaniu odbiornika usługi zdalne hello znajduje się już w `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="f37af-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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
           // store hello contents of backupInfo.Directory
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
           // store hello contents of backupInfo.Directory
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


<span data-ttu-id="f37af-154">W tym przykładzie `IMyActorService` jest umowa komunikacji zdalnej, która implementuje `IService` (C#) i `Service` (języka Java), a następnie jest implementowany przez `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="f37af-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="f37af-155">Dodanie tego kontraktu usługi zdalne metod na `IMyActorService` , są teraz dostępne tooa klienta przez utworzenie zdalnym obiektem pośredniczącym za pośrednictwem `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="f37af-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="f37af-156">Model aplikacji</span><span class="sxs-lookup"><span data-stu-id="f37af-156">Application model</span></span>
<span data-ttu-id="f37af-157">Usługi aktora są niezawodne usługi, model aplikacji hello jest hello takie same.</span><span class="sxs-lookup"><span data-stu-id="f37af-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="f37af-158">Jednak narzędzi kompilacji framework aktora hello wygenerować niektórych plików modelu aplikacji hello dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f37af-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="f37af-159">Manifest usługi</span><span class="sxs-lookup"><span data-stu-id="f37af-159">Service manifest</span></span>
<span data-ttu-id="f37af-160">narzędzia kompilacji framework aktora Hello automatycznie generować hello zawartość pliku ServiceManifest.xml usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="f37af-161">Ten plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="f37af-161">This file includes:</span></span>

* <span data-ttu-id="f37af-162">Typ usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-162">Actor service type.</span></span> <span data-ttu-id="f37af-163">Nazwa typu Hello jest generowany na podstawie nazwy projektu z aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="f37af-164">Na podstawie hello trwałości atrybutu na Twoje aktora, hello flagi HasPersistedState zostanie również ustawiona odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f37af-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="f37af-165">Pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="f37af-165">Code package.</span></span>
* <span data-ttu-id="f37af-166">Pakiet konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f37af-166">Config package.</span></span>
* <span data-ttu-id="f37af-167">Zasoby i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="f37af-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="f37af-168">Manifest aplikacji</span><span class="sxs-lookup"><span data-stu-id="f37af-168">Application manifest</span></span>
<span data-ttu-id="f37af-169">narzędzia kompilacji framework aktora Hello automatyczne tworzenie definicji domyślnej usługi dla usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="f37af-170">narzędzia kompilacji Hello wypełniania właściwości usługi domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f37af-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="f37af-171">Liczba zestawu replik jest określana przez atrybut trwałości hello aktora sieci.</span><span class="sxs-lookup"><span data-stu-id="f37af-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="f37af-172">Każdy atrybut trwałości hello czas na Twoje aktora zostanie zmieniona, hello repliki zestawu w definicji usługi domyślne hello zostanie zresetowany odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f37af-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="f37af-173">Schemat partycji i zakres są ustawione tooUniform Int64 z pełnego zakresu klucza hello Int64.</span><span class="sxs-lookup"><span data-stu-id="f37af-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="f37af-174">Pojęcia dotyczące partycji usługi sieć szkieletowa osób</span><span class="sxs-lookup"><span data-stu-id="f37af-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="f37af-175">Usługi aktora są podzielone na partycje usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="f37af-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="f37af-176">Każda partycja usługi aktora zawiera zestaw złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f37af-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="f37af-177">Partycji usługi są automatycznie dystrybuowane za pośrednictwem wiele węzłów w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="f37af-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="f37af-178">W związku z tym rozpowszechnianych wystąpień aktora.</span><span class="sxs-lookup"><span data-stu-id="f37af-178">Actor instances are distributed as a result.</span></span>

![Aktora partycjonowania i dystrybucji][5]

<span data-ttu-id="f37af-180">Niezawodne usługi mogą być tworzone z różnych partycji, systemów i zakresami kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="f37af-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="f37af-181">Usługa aktora Hello używa schemat partycjonowania Int64 hello z hello pełne Int64 zakresem kluczy toomap toopartitions złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f37af-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="f37af-182">Identyfikator aktora</span><span class="sxs-lookup"><span data-stu-id="f37af-182">Actor ID</span></span>
<span data-ttu-id="f37af-183">Każdy aktora utworzony w usłudze hello ma unikatowy identyfikator skojarzony z nim reprezentowany przez hello `ActorId` klasy.</span><span class="sxs-lookup"><span data-stu-id="f37af-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="f37af-184">`ActorId`to wartość Identyfikatora nieprzezroczyste, która może służyć do dystrybucji uniform podmiotów między partycji usługi hello generując losowe identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="f37af-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="f37af-185">Każdy `ActorId` jest skrótem tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="f37af-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="f37af-186">Jest to, dlaczego usługa aktora hello musi używać schemat partycjonowania Int64 z pełnego zakresu klucza hello Int64.</span><span class="sxs-lookup"><span data-stu-id="f37af-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="f37af-187">Jednak można używać niestandardowej wartości Identyfikatora dla `ActorID`, w tym identyfikatory GUID/UUID, ciągi i Int64s.</span><span class="sxs-lookup"><span data-stu-id="f37af-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="f37af-188">Podczas korzystania z identyfikatorów GUID/UUID i ciągi, wartości hello są skrótem tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="f37af-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="f37af-189">Jednak gdy możesz jest jawnie dostarczanie tooan Int64 `ActorId`, hello Int64 przypisze bezpośrednio tooa partycji bez dalszego wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="f37af-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="f37af-190">Możesz użyć tego toocontrol techniki, które podmioty hello partycji są umieszczane w.</span><span class="sxs-lookup"><span data-stu-id="f37af-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f37af-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f37af-191">Next steps</span></span>
* [<span data-ttu-id="f37af-192">Zarządzanie stanem aktora</span><span class="sxs-lookup"><span data-stu-id="f37af-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="f37af-193">Aktora cykl życia i odzyskiwanie pamięci</span><span class="sxs-lookup"><span data-stu-id="f37af-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="f37af-194">Dokumentacji interfejsu API złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="f37af-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="f37af-195">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="f37af-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="f37af-196">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="f37af-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
