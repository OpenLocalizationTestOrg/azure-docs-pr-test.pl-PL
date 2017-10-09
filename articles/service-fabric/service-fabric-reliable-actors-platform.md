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
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Jak używać platformy Service Fabric hello w Reliable Actors
W tym artykule opisano, jak Reliable Actors działają na platformie Azure Service Fabric hello. Reliable Actors uruchomienia w ramach obsługiwanej w implementacji stanowe niezawodnej usługi o nazwie hello *usługi aktora*. Usługa aktora Hello zawiera wszystkie hello składniki niezbędne toomanage hello w cyklu życia i komunikat podczas wysyłania do sieci złośliwych użytkowników:

* Hello aktora środowiska uruchomieniowego umożliwia zarządzanie cyklem, wyrzucanie elementów bezużytecznych i wymusza jednowątkowe dostęp.
* Odbiornik komunikacji zdalnej usługi aktora akceptuje tooactors połączeń dostępu zdalnego i wysyła je tooa dyspozytora tooroute toohello aktora odpowiednie wystąpienie.
* Hello dostawcy stanu aktora opakowuje dostawców stanu (na przykład dostawcy stanu niezawodnej kolekcje hello) i udostępnia adapter dla zarządzania stanem aktora.

Te składniki współpracują formularza hello niezawodnego aktora framework.

## <a name="service-layering"></a>Tworzenie warstw usługi
Ponieważ sama usługa aktora hello jest niezawodnej usługi, wszystkie hello [model aplikacji](service-fabric-application-model.md), cykl życia, [pakowania](service-fabric-package-apps.md), [wdrożenia](service-fabric-deploy-remove-applications.md), uaktualniania i skalowanie pojęcia związane z Niezawodne usługi zastosować hello tej samej usługi tooactor sposób. 

![Tworzenie warstw usługi aktora][1]

Witaj wcześniejszym diagramie przedstawiono hello relacje struktur aplikacji hello sieci szkieletowej usług i kod użytkownika. Niebieski elementy reprezentują struktury aplikacji hello niezawodne usługi framework niezawodnego aktora hello reprezentuje kolor pomarańczowy i zielony reprezentuje kod użytkownika.

W usługach niezawodnej usługi dziedziczy hello `StatefulService` klasy. Ta klasa jest pochodną `StatefulServiceBase` (lub `StatelessService` usług bezstanowych). W Reliable Actors należy użyć hello usługi aktora. Usługa aktora Hello jest inną implementację hello `StatefulServiceBase` klasy tego wzorca aktora hello implementuje gdzie uruchomić sieci złośliwych użytkowników. Ponieważ właśnie implementacja jest sama usługa aktora hello `StatefulServiceBase`, można napisać własne usługi, która pochodzi z `ActorService` i funkcje na poziomie usługi wdrożenie hello sam sposób jak w przypadku dziedziczenia `StatefulService`, takich jak:

* Usługa tworzenia kopii zapasowej i przywracania.
* Udostępnione funkcji dla wszystkich podmiotów, na przykład wyłącznika.
* Zdalne wywoływanie procedur w samej usługi aktora hello i na każdym poszczególnych aktora.

> [!NOTE]
> Stanowe usług nie są obecnie obsługiwane w języku Java/Linux.

### <a name="using-hello-actor-service"></a>Przy użyciu usługi aktora hello
Wystąpienia aktora mają dostęp toohello aktora usługi, w którym jest uruchomiony. Za pośrednictwem usługi aktora hello wystąpień aktora programowo można uzyskać hello usługi kontekstu. Kontekst usługi Hello ma identyfikator partycji: hello, nazwę usługi, nazwa aplikacji i inne informacje specyficzne dla platformy Service Fabric:

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


Podobnie jak wszystkie niezawodnej usługi usługi aktora hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi. Dla usługi aktora hello toorun swoich wystąpień aktora, danego typu aktora również musi być zarejestrowane w usłudze aktora hello. Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób. W przypadku najprostszym hello można zarejestrować tylko danego typu aktora i usługi aktora hello z ustawieniami domyślnymi niejawnie będą używane:

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

Alternatywnie można użyć wyrażenia lambda udostępniane przez usługa aktora hello tooconstruct hello rejestracji — metoda. Można następnie skonfigurować usługi aktora hello i utworzenia jawnie swoich wystąpień aktora, w którym można wstrzyknięcia zależności tooyour aktora za pośrednictwem jej konstruktora:

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

### <a name="actor-service-methods"></a>Metody usługi aktora
Witaj implementuje usługi aktora `IActorService` (C#) lub `ActorService` (języka Java), który z kolei implementuje `IService` (C#) lub `Service` (Java). Jest to interfejs hello używany łącząc niezawodne usługi, co pozwala na metody usług zdalnych wywołań procedur. Zawiera metody poziomu usług, które może zostać wywołana zdalnie za pomocą usług zdalnych.

#### <a name="enumerating-actors"></a>Wyliczanie złośliwych użytkowników
Usługa aktora Hello umożliwia klientowi tooenumerate metadane dotyczące hello uczestników, obsługujące usługi hello. Ponieważ usługa aktora hello jest partycjonowany usługi stanowej, wyliczenie jest wykonywane dla każdej partycji. Ponieważ każda partycja może zawierać wiele osób, wyliczenie hello jest zwracana jako zestaw wyników stronicowania. strony Hello są zwracane przez zapoznaniem wszystkich stron. powitania po przykładzie pokazano, jak toocreate listę wszystkich podmiotów active w jednej partycji usługi aktora:

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

#### <a name="deleting-actors"></a>Usuwanie złośliwych użytkowników
Usługa aktora Hello udostępnia również funkcję usuwania złośliwych użytkowników:

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

Aby uzyskać więcej informacji na temat usuwania złośliwych użytkowników i ich stan, zobacz hello [dokumentacji cyklu życia aktora](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Usługa aktora niestandardowych
Za pomocą hello aktora rejestracji lambda, możesz zarejestrować własnej usługi aktora niestandardowej, która pochodzi z `ActorService` (C#) i `FabricActorService` (Java). W tej usłudze aktora niestandardowych można zaimplementować własnej funkcji poziomu usług pisząc klasy usługi, która dziedziczy `ActorService` (C#) lub `FabricActorService` (Java). Usługi aktora niestandardowych dziedziczy wszystkie funkcje środowiska uruchomieniowego aktora hello z `ActorService` (C#) lub `FabricActorService` (Java) i mogą być używane tooimplement metody usługi.

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

#### <a name="implementing-actor-backup-and-restore"></a>Implementowanie aktora kopii zapasowej i przywracania
 W hello poniższy przykład, usługa aktora niestandardowych hello przedstawia tooback metody zapasowych aktora dzięki wykorzystaniu odbiornika usługi zdalne hello znajduje się już w `ActorService`:

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


W tym przykładzie `IMyActorService` jest umowa komunikacji zdalnej, która implementuje `IService` (C#) i `Service` (języka Java), a następnie jest implementowany przez `MyActorService`. Dodanie tego kontraktu usługi zdalne metod na `IMyActorService` , są teraz dostępne tooa klienta przez utworzenie zdalnym obiektem pośredniczącym za pośrednictwem `ActorServiceProxy`:

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

## <a name="application-model"></a>Model aplikacji
Usługi aktora są niezawodne usługi, model aplikacji hello jest hello takie same. Jednak narzędzi kompilacji framework aktora hello wygenerować niektórych plików modelu aplikacji hello dla Ciebie.

### <a name="service-manifest"></a>Manifest usługi
narzędzia kompilacji framework aktora Hello automatycznie generować hello zawartość pliku ServiceManifest.xml usługi aktora. Ten plik zawiera:

* Typ usługi aktora. Nazwa typu Hello jest generowany na podstawie nazwy projektu z aktora. Na podstawie hello trwałości atrybutu na Twoje aktora, hello flagi HasPersistedState zostanie również ustawiona odpowiednio.
* Pakiet kodu.
* Pakiet konfiguracji.
* Zasoby i punktów końcowych.

### <a name="application-manifest"></a>Manifest aplikacji
narzędzia kompilacji framework aktora Hello automatyczne tworzenie definicji domyślnej usługi dla usługi aktora. narzędzia kompilacji Hello wypełniania właściwości usługi domyślne hello:

* Liczba zestawu replik jest określana przez atrybut trwałości hello aktora sieci. Każdy atrybut trwałości hello czas na Twoje aktora zostanie zmieniona, hello repliki zestawu w definicji usługi domyślne hello zostanie zresetowany odpowiednio.
* Schemat partycji i zakres są ustawione tooUniform Int64 z pełnego zakresu klucza hello Int64.

## <a name="service-fabric-partition-concepts-for-actors"></a>Pojęcia dotyczące partycji usługi sieć szkieletowa osób
Usługi aktora są podzielone na partycje usługi stanowej. Każda partycja usługi aktora zawiera zestaw złośliwych użytkowników. Partycji usługi są automatycznie dystrybuowane za pośrednictwem wiele węzłów w sieci szkieletowej usług. W związku z tym rozpowszechnianych wystąpień aktora.

![Aktora partycjonowania i dystrybucji][5]

Niezawodne usługi mogą być tworzone z różnych partycji, systemów i zakresami kluczy partycji. Usługa aktora Hello używa schemat partycjonowania Int64 hello z hello pełne Int64 zakresem kluczy toomap toopartitions złośliwych użytkowników.

### <a name="actor-id"></a>Identyfikator aktora
Każdy aktora utworzony w usłudze hello ma unikatowy identyfikator skojarzony z nim reprezentowany przez hello `ActorId` klasy. `ActorId`to wartość Identyfikatora nieprzezroczyste, która może służyć do dystrybucji uniform podmiotów między partycji usługi hello generując losowe identyfikatory:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Każdy `ActorId` jest skrótem tooan Int64. Jest to, dlaczego usługa aktora hello musi używać schemat partycjonowania Int64 z pełnego zakresu klucza hello Int64. Jednak można używać niestandardowej wartości Identyfikatora dla `ActorID`, w tym identyfikatory GUID/UUID, ciągi i Int64s.

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

Podczas korzystania z identyfikatorów GUID/UUID i ciągi, wartości hello są skrótem tooan Int64. Jednak gdy możesz jest jawnie dostarczanie tooan Int64 `ActorId`, hello Int64 przypisze bezpośrednio tooa partycji bez dalszego wyznaczania wartości skrótu. Możesz użyć tego toocontrol techniki, które podmioty hello partycji są umieszczane w.

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie stanem aktora](service-fabric-reliable-actors-state-management.md)
* [Aktora cykl życia i odzyskiwanie pamięci](service-fabric-reliable-actors-lifecycle.md)
* [Dokumentacji interfejsu API złośliwych użytkowników](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [.NET przykładowy kod](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Java przykładowy kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
