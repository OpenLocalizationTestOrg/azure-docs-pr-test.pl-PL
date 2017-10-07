---
title: "Omówienie komunikacji usług aaaReliable | Dokumentacja firmy Microsoft"
description: "Przegląd hello niezawodne usługi komunikacji modelu, tym odbiorników otwierania w usługach, rozpoznawania punktów końcowych i komunikacji między usługami."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="36aba-103">Jak toouse hello komunikacji niezawodnej usługi interfejsów API</span><span class="sxs-lookup"><span data-stu-id="36aba-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="36aba-104">Azure Service Fabric jako platformę jest całkowicie niezależny o komunikacji między usługami.</span><span class="sxs-lookup"><span data-stu-id="36aba-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="36aba-105">Wszystkie protokoły i stosy są dopuszczalne, z UDP tooHTTP.</span><span class="sxs-lookup"><span data-stu-id="36aba-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="36aba-106">Jest zapasowej toochoose dewelopera usługi toohello komunikowania usług.</span><span class="sxs-lookup"><span data-stu-id="36aba-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="36aba-107">Struktura aplikacji Hello niezawodne usługi zawiera komunikacji wbudowanej stosów oraz interfejsów API, których można używać toobuild składniki niestandardowe komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="36aba-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="36aba-108">Konfigurowanie komunikacji usługi</span><span class="sxs-lookup"><span data-stu-id="36aba-108">Set up service communication</span></span>
<span data-ttu-id="36aba-109">Hello niezawodnej usługi interfejsu API używa prosty interfejs do komunikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="36aba-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="36aba-110">tooopen punktu końcowego usługi, po prostu zaimplementować ten interfejs.</span><span class="sxs-lookup"><span data-stu-id="36aba-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="36aba-111">Następnie można dodać implementacji odbiornik komunikacji, przywracając jego zastąpienie metody klasy oparta na usłudze.</span><span class="sxs-lookup"><span data-stu-id="36aba-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="36aba-112">Dla usługi bezstanowej:</span><span class="sxs-lookup"><span data-stu-id="36aba-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="36aba-113">Dla stanowych usług:</span><span class="sxs-lookup"><span data-stu-id="36aba-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="36aba-114">Niezawodne usługi stanowej nie są obsługiwane w języku Java jeszcze.</span><span class="sxs-lookup"><span data-stu-id="36aba-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="36aba-115">W obu przypadkach należy zwracać kolekcja odbiorników.</span><span class="sxs-lookup"><span data-stu-id="36aba-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="36aba-116">Dzięki temu toolisten Twojego usługi na wiele punktów końcowych potencjalnie przy użyciu różnych protokołów, za pomocą wielu odbiorników.</span><span class="sxs-lookup"><span data-stu-id="36aba-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="36aba-117">Na przykład może mieć odbiornik HTTP i oddzielne odbiornika protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="36aba-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="36aba-118">Każdy odbiornik pobiera nazwę i hello wynikowy zbiór *Nazwa: adres* pary są reprezentowane jako obiekt JSON, gdy klient żąda hello adres nasłuchiwania dla wystąpienia usługi lub partycji.</span><span class="sxs-lookup"><span data-stu-id="36aba-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="36aba-119">Usługi bezstanowej zastąpienie hello zwraca kolekcję ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="36aba-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="36aba-120">A `ServiceInstanceListener` zawiera toocreate funkcja `ICommunicationListener(C#) / CommunicationListener(Java)` i nadaje mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="36aba-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="36aba-121">W przypadku usług stanowych zastąpienie hello zwraca kolekcję ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="36aba-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="36aba-122">To jest nieco inne niż jego odpowiednik bezstanowych, ponieważ `ServiceReplicaListener` ma tooopen opcji `ICommunicationListener` w replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="36aba-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="36aba-123">Nie można użyć wielu odbiorników komunikacji w usłudze tylko można również określić które odbiorników akceptowania żądań w replikach pomocniczych i te, które nasłuchuje repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="36aba-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="36aba-124">Na przykład może mieć ServiceRemotingListener, pobierającej wywołania RPC tylko na podstawowym repliki, a drugi, niestandardowe odbiornik, który przyjmuje odczytu żądań w replikach pomocniczych za pośrednictwem protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="36aba-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="36aba-125">Podczas tworzenia wiele odbiorników dla usługi, każdy odbiornika **musi** należy nadać unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="36aba-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="36aba-126">Ponadto opisano hello punktów końcowych, które są wymagane dla usługi hello w hello [manifestu usługi](service-fabric-application-model.md) sekcji hello w punktach końcowych.</span><span class="sxs-lookup"><span data-stu-id="36aba-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="36aba-127">odbiornik komunikacji Hello dostęp do zasobów punktu końcowego hello przydzielony tooit z hello `CodePackageActivationContext` w hello `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="36aba-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="36aba-128">odbiornik Hello następnie można uruchomić nasłuchiwanie żądań, gdy jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="36aba-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="36aba-129">Punkt końcowy zasoby są typowe toohello całej usługi pakietu, a po aktywowaniu pakiet usługi hello są przydzielone przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="36aba-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="36aba-130">Wiele replik usługi hostowanej w hello tego samego elementu ServiceHost może udostępniać hello sam port.</span><span class="sxs-lookup"><span data-stu-id="36aba-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="36aba-131">Oznacza to, że odbiornik komunikacji hello powinna obsługiwać Udostępnianie portów.</span><span class="sxs-lookup"><span data-stu-id="36aba-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="36aba-132">Hello zaleca się, jak to zrobić to dla hello komunikacji odbiornika toouse hello partycji identyfikator i identyfikator repliki i wystąpienia podczas generowania hello nasłuchiwania adresów.</span><span class="sxs-lookup"><span data-stu-id="36aba-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="36aba-133">Rejestracja adres usługi</span><span class="sxs-lookup"><span data-stu-id="36aba-133">Service address registration</span></span>
<span data-ttu-id="36aba-134">Usługa systemowa o nazwie hello *Naming Service* działa w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="36aba-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="36aba-135">Witaj Naming Service jest rejestratora dla usług i ich adresów, które każdego wystąpienia lub repliki usługi hello nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="36aba-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="36aba-136">Gdy hello `OpenAsync(C#) / openAsync(Java)` metody `ICommunicationListener(C#) / CommunicationListener(Java)` zakończeniu jego powrotu wartość pobiera zarejestrowane w hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="36aba-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="36aba-137">To zwrócić wartość, która pobiera ciąg, którego wartość może być dowolna na wszystkich opublikowanych w powitalne jest Naming Service.</span><span class="sxs-lookup"><span data-stu-id="36aba-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="36aba-138">Ta wartość ciągu jest, jakie klientów wyświetlać, gdy został poproszony o adres dla usługi hello z hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="36aba-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="36aba-139">Sieć szkieletowa usług zawiera interfejsy API umożliwiające klientów i innych usług toothen poprosić dla tego adresu według nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="36aba-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="36aba-140">Jest to ważne, ponieważ adres usługi hello nie jest statyczne.</span><span class="sxs-lookup"><span data-stu-id="36aba-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="36aba-141">Usługi są przenoszone w klastrze hello do celów dostępności i równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="36aba-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="36aba-142">Jest to mechanizm hello Zezwalaj klientom Witaj tooresolve nasłuchiwania adresów dla usługi.</span><span class="sxs-lookup"><span data-stu-id="36aba-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="36aba-143">Do ukończenia toowrite odbiornik komunikacji, zobacz temat Omówienie [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md) dla C#, natomiast dla języka Java można napisać własny implementację serwera HTTP, zobacz EchoServer aplikacji przykład: w https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="36aba-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="36aba-144">Podczas komunikacji z usługą</span><span class="sxs-lookup"><span data-stu-id="36aba-144">Communicating with a service</span></span>
<span data-ttu-id="36aba-145">Hello niezawodnej interfejsu API usług zawiera hello następujące biblioteki toowrite klientów, które komunikują się z usługami.</span><span class="sxs-lookup"><span data-stu-id="36aba-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="36aba-146">Rozpoznanie punktu końcowego usługi</span><span class="sxs-lookup"><span data-stu-id="36aba-146">Service endpoint resolution</span></span>
<span data-ttu-id="36aba-147">Witaj pierwszy krok toocommunication z usługą jest tooresolve adresu punktu końcowego hello partycji lub wystąpienie usługi hello, który ma tootalk do.</span><span class="sxs-lookup"><span data-stu-id="36aba-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="36aba-148">Witaj `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` klasy narzędzie jest właściwością pierwotną podstawowe, ułatwiająca klientów, określenia hello punkt końcowy usługi w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="36aba-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="36aba-149">W terminologii usługi sieć szkieletowa hello proces określania hello punkt końcowy usługi jest hello określonego tooas *usługi rozpoznawania punktu końcowego*.</span><span class="sxs-lookup"><span data-stu-id="36aba-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="36aba-150">tooservices tooconnect w klastrze, ServicePartitionResolver mogą być tworzone przy użyciu ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="36aba-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="36aba-151">Jest to zalecane użycie w większości sytuacji hello:</span><span class="sxs-lookup"><span data-stu-id="36aba-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="36aba-152">tooservices tooconnect w innym klastrze, ServicePartitionResolver mogą być tworzone przy użyciu zestawu punktów końcowych klastra bramy.</span><span class="sxs-lookup"><span data-stu-id="36aba-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="36aba-153">Pamiętaj, że punkty końcowe bramy jest po prostu różnych punktów końcowych do łączenia toohello tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="36aba-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="36aba-154">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36aba-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="36aba-155">Alternatywnie `ServicePartitionResolver` można przydzielić funkcję do tworzenia `FabricClient` toouse wewnętrznie:</span><span class="sxs-lookup"><span data-stu-id="36aba-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="36aba-156">`FabricClient`jest hello obiekt, który jest używany toocommunicate z klastrem usługi sieć szkieletowa hello różnych operacji zarządzania w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="36aba-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="36aba-157">Jest to przydatne, jeśli chcesz mieć większą kontrolę nad jak program rozpoznawania nazw partycji usługi współdziała z klastra.</span><span class="sxs-lookup"><span data-stu-id="36aba-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="36aba-158">`FabricClient`buforuje wewnętrznie i jest zwykle kosztowne toocreate, dlatego jest ważne tooreuse `FabricClient` wystąpień, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="36aba-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="36aba-159">Metody rozpoznawania jest używane tooretrieve hello adresu usługi lub partycji usługi dla usług podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="36aba-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="36aba-160">Adres usługi można rozwiązać za pomocą ServicePartitionResolver, ale wymagane jest więcej pracy tooensure hello rozpoznać adresu można poprawnie.</span><span class="sxs-lookup"><span data-stu-id="36aba-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="36aba-161">Klient musi toodetect czy hello próba połączenia nie powiodła się z powodu błędu przejściowego i można ponowić (np. usługi przenieść lub jest tymczasowo niedostępny), lub trwały błąd (np. usługa została usunięta lub hello żądany zasób nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="36aba-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="36aba-162">Wystąpienie usługi lub repliki można przenosić z węzła toonode w dowolnym momencie kilka przyczyn.</span><span class="sxs-lookup"><span data-stu-id="36aba-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="36aba-163">adres usługi Hello rozpoznawane za pomocą ServicePartitionResolver może być przestarzały czasu hello tooconnect prób kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="36aba-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="36aba-164">W takim przypadku ponownie powitania klienta wymaga adresu hello toore rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="36aba-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="36aba-165">Zapewnianie hello poprzedniej `ResolvedServicePartition` wskazuje, że Witaj ponownie program rozpoznawania nazw musi tootry zamiast po prostu pobrać adres pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="36aba-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="36aba-166">Zazwyczaj powitania klienta kodu muszą działa z hello ServicePartitionResolver bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="36aba-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="36aba-167">Jest tworzony i przekazywane fabryki klienta toocommunication w hello niezawodnej usługi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="36aba-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="36aba-168">fabryki Hello korzystanie z mechanizmu rozpoznawania hello toogenerate obiektu klienta, które mogą być używane toocommunicate z usługami.</span><span class="sxs-lookup"><span data-stu-id="36aba-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="36aba-169">Komunikacja klientów i fabryki</span><span class="sxs-lookup"><span data-stu-id="36aba-169">Communication clients and factories</span></span>
<span data-ttu-id="36aba-170">Witaj komunikacji fabryki biblioteka zawiera typowy wzorzec ponownych prób obsługi błędów, który ułatwia ponawianie punktów końcowych usługi tooresolved połączenia.</span><span class="sxs-lookup"><span data-stu-id="36aba-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="36aba-171">Biblioteka fabryki Hello zapewnia mechanizm ponawiania hello podczas Podaj hello programy obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="36aba-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="36aba-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`definiuje interfejs podstawowy hello zaimplementowana przez fabrykę klienta komunikacji, który spowoduje utworzenie klientów, którzy mogą komunikować tooa usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="36aba-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="36aba-173">Witaj implementacji powitalne CommunicationClientFactory zależy od stosu komunikacji hello używane przez usługę sieć szkieletowa usług hello, w którym powitania klienta chce toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="36aba-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="36aba-174">Hello niezawodnej interfejsu API usług zawiera `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="36aba-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="36aba-175">Udostępnia podstawową implementację interfejsu CommunicationClientFactory hello i wykonuje zadania, które są typowe tooall hello komunikacji stosów.</span><span class="sxs-lookup"><span data-stu-id="36aba-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="36aba-176">(Te zadania obejmują przy użyciu punktu końcowego usługi hello toodetermine ServicePartitionResolver).</span><span class="sxs-lookup"><span data-stu-id="36aba-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="36aba-177">Klienci implementuje zwykle hello abstrakcyjny CommunicationClientFactoryBase klasy toohandle logiki określonej toohello stosu komunikacji.</span><span class="sxs-lookup"><span data-stu-id="36aba-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="36aba-178">Hello komunikacji klienta po prostu odbiera adres i używa go tooconnect tooa usługi.</span><span class="sxs-lookup"><span data-stu-id="36aba-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="36aba-179">Witaj, klient może używać niezależnie od protokołu chce.</span><span class="sxs-lookup"><span data-stu-id="36aba-179">hello client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="36aba-180">Fabryka klientów Hello jest głównie odpowiedzialną za tworzenie komunikacji klientów.</span><span class="sxs-lookup"><span data-stu-id="36aba-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="36aba-181">Dla klientów, którzy nie Obsługa połączenie trwałe, takich jak klient HTTP fabryki hello musi tylko toocreate i zwracany powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="36aba-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="36aba-182">Inne protokoły zapewniające połączenie trwałe, takie jak niektóre protokoły binarnego, również powinny zostać zatwierdzone przez toodetermine fabryki hello czy połączenia hello wymaga toobe utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="36aba-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="36aba-183">Ponadto program obsługi wyjątku jest odpowiedzialny za określenie, jakie tootake działania po wystąpieniu wyjątku.</span><span class="sxs-lookup"><span data-stu-id="36aba-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="36aba-184">Wyjątki są podzielone na **powtarzający operację** i **niepowtarzającego**.</span><span class="sxs-lookup"><span data-stu-id="36aba-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="36aba-185">**Niepowtarzającego** wyjątki po prostu pobrać zgłoszony wstecz toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="36aba-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="36aba-186">**powtarzający operację** dalsze wyjątki są dzielone na kategorie **przejściowa** i **nieprzejściowego**.</span><span class="sxs-lookup"><span data-stu-id="36aba-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="36aba-187">**Przejściowa** wyjątki są tymi, które można po prostu ponowione bez ponowne rozpoznanie adres punktu końcowego usługi hello.</span><span class="sxs-lookup"><span data-stu-id="36aba-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="36aba-188">Obejmują one przejściowych problemów z siecią lub odpowiedzi na błędy usług innych niż te, które wskazują adres punktu końcowego usługi hello nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="36aba-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="36aba-189">**Inne niż przejściowy** wyjątki są te, które wymagają hello usługi punktu końcowego adresu toobe ponownie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="36aba-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="36aba-190">Obejmują one wyjątki, które wskazują, że punkt końcowy usługi hello jest nieosiągalny, wskazujący, że usługa hello przeniósł tooa innego węzła.</span><span class="sxs-lookup"><span data-stu-id="36aba-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="36aba-191">Witaj `TryHandleException` sprawia, że decyzja o danego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="36aba-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="36aba-192">Jeśli go **nie zna** jakie toomake decyzji o wyjątku, powinien on zwrócić **false**.</span><span class="sxs-lookup"><span data-stu-id="36aba-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="36aba-193">Jeśli go **wiedzieć** jakie toomake decyzja powinna odpowiednio ustawić wynik hello i zwracać **true**.</span><span class="sxs-lookup"><span data-stu-id="36aba-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="36aba-194">Składanie wszystkiego razem</span><span class="sxs-lookup"><span data-stu-id="36aba-194">Putting it all together</span></span>
<span data-ttu-id="36aba-195">Z `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, i `IExceptionHandler(C#) / ExceptionHandler(Java)` zbudowana wokół protokołu komunikacyjnego, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` umieszczeniu wszystkich elementów i zapewnia odporność obsługi hello i usługi partycji adres rozpoznawania pętlę wokół tych składników.</span><span class="sxs-lookup"><span data-stu-id="36aba-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="36aba-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36aba-196">Next steps</span></span>
* <span data-ttu-id="36aba-197">Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt C# w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) lub [Java przykładowy projekt w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="36aba-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="36aba-198">Zdalne wywołania procedur z usług zdalnych niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="36aba-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="36aba-199">Interfejs API, który używa OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="36aba-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="36aba-200">Komunikacyjny WCF za pomocą niezawodnych usług</span><span class="sxs-lookup"><span data-stu-id="36aba-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
