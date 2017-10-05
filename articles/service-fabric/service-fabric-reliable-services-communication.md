---
title: "Komunikacji niezawodnej usługi — omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie modelu komunikacji niezawodnej usługi, tym odbiorników otwierania w usługach, rozpoznawania punktów końcowych i komunikacji między usługami."
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
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="62df7-103">Jak używać komunikacji niezawodnej usługi interfejsów API</span><span class="sxs-lookup"><span data-stu-id="62df7-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="62df7-104">Azure Service Fabric jako platformę jest całkowicie niezależny o komunikacji między usługami.</span><span class="sxs-lookup"><span data-stu-id="62df7-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="62df7-105">Wszystkie protokoły i stosy są dopuszczalne, z UDP HTTP.</span><span class="sxs-lookup"><span data-stu-id="62df7-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="62df7-106">To dewelopera usługi, aby wybrać komunikowania usług.</span><span class="sxs-lookup"><span data-stu-id="62df7-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="62df7-107">Struktura aplikacji niezawodne usługi zawiera komunikacji wbudowanej stosach, a także interfejsów API, który można wykorzystać do tworzenia składników niestandardowych komunikacji.</span><span class="sxs-lookup"><span data-stu-id="62df7-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="62df7-108">Konfigurowanie komunikacji usługi</span><span class="sxs-lookup"><span data-stu-id="62df7-108">Set up service communication</span></span>
<span data-ttu-id="62df7-109">Niezawodne interfejsu API usług używa prosty interfejs do komunikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="62df7-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="62df7-110">Aby otworzyć punktu końcowego usługi, po prostu zaimplementować ten interfejs:</span><span class="sxs-lookup"><span data-stu-id="62df7-110">To open an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="62df7-111">Następnie można dodać implementacji odbiornik komunikacji, przywracając jego zastąpienie metody klasy oparta na usłudze.</span><span class="sxs-lookup"><span data-stu-id="62df7-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="62df7-112">Dla usługi bezstanowej:</span><span class="sxs-lookup"><span data-stu-id="62df7-112">For stateless services:</span></span>

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

<span data-ttu-id="62df7-113">Dla stanowych usług:</span><span class="sxs-lookup"><span data-stu-id="62df7-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="62df7-114">Niezawodne usługi stanowej nie są obsługiwane w języku Java jeszcze.</span><span class="sxs-lookup"><span data-stu-id="62df7-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="62df7-115">W obu przypadkach należy zwracać kolekcja odbiorników.</span><span class="sxs-lookup"><span data-stu-id="62df7-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="62df7-116">Dzięki temu usługi do nasłuchiwania na wiele punktów końcowych potencjalnie przy użyciu różnych protokołów, za pomocą wielu odbiorników.</span><span class="sxs-lookup"><span data-stu-id="62df7-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="62df7-117">Na przykład może mieć odbiornik HTTP i oddzielne odbiornika protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="62df7-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="62df7-118">Każdy odbiornik pobiera nazwę, a wynikowy zbiór *Nazwa: adres* pary są reprezentowane jako obiekt JSON, gdy klient żąda nasłuchiwania adresów dla wystąpienia usługi lub partycji.</span><span class="sxs-lookup"><span data-stu-id="62df7-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="62df7-119">Usługi bezstanowej zastąpienie zwraca kolekcję ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="62df7-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="62df7-120">A `ServiceInstanceListener` zawiera funkcję, aby utworzyć `ICommunicationListener(C#) / CommunicationListener(Java)` i nadaje mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="62df7-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="62df7-121">W przypadku usług stanowych zastąpienie zwraca kolekcję ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="62df7-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="62df7-122">To jest nieco inne niż jego odpowiednik bezstanowych, ponieważ `ServiceReplicaListener` ma opcję, aby otworzyć `ICommunicationListener` w replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="62df7-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="62df7-123">Nie można użyć wielu odbiorników komunikacji w usłudze tylko można również określić które odbiorników akceptowania żądań w replikach pomocniczych i te, które nasłuchuje repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="62df7-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="62df7-124">Na przykład może mieć ServiceRemotingListener, pobierającej wywołania RPC tylko na podstawowym repliki, a drugi, niestandardowe odbiornik, który przyjmuje odczytu żądań w replikach pomocniczych za pośrednictwem protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="62df7-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="62df7-125">Podczas tworzenia wiele odbiorników dla usługi, każdy odbiornika **musi** należy nadać unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="62df7-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="62df7-126">Ponadto opisano punkty końcowe, które są wymagane dla usługi w [manifestu usługi](service-fabric-application-model.md) w sekcji dla punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="62df7-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="62df7-127">Odbiornik komunikacji może uzyskać dostęp do zasobów punktu końcowego przydzielone z nim `CodePackageActivationContext` w `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="62df7-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="62df7-128">Odbiornik może następnie uruchom nasłuchiwanie żądań, gdy jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="62df7-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="62df7-129">Zasoby punktu końcowego są wspólne dla pakietu całej usługi, a po aktywowaniu pakiet usługi są przydzielone przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="62df7-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="62df7-130">Wiele replik usługi hostowanej w tej samej ServiceHost może udostępniać tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="62df7-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="62df7-131">Oznacza to, że odbiornik komunikacji powinny obsługiwać Udostępnianie portów.</span><span class="sxs-lookup"><span data-stu-id="62df7-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="62df7-132">Zalecanym sposobem w ten sposób dotyczy odbiornik komunikacji do używania partycji identyfikator i identyfikator repliki i wystąpienia podczas generowania adresu nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="62df7-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="62df7-133">Rejestracja adres usługi</span><span class="sxs-lookup"><span data-stu-id="62df7-133">Service address registration</span></span>
<span data-ttu-id="62df7-134">Wywołuje się, usługa systemowa *Naming Service* działa w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="62df7-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="62df7-135">Usługa nazewnictwa jest rejestratora dla usług i ich adresów, które każdego wystąpienia lub repliki usługi nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="62df7-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="62df7-136">Gdy `OpenAsync(C#) / openAsync(Java)` metody `ICommunicationListener(C#) / CommunicationListener(Java)` zakończeniu jego powrotu wartość pobiera zarejestrowane w usłudze nazw.</span><span class="sxs-lookup"><span data-stu-id="62df7-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="62df7-137">Zwrócona wartość, która została opublikowana w usłudze nazewnictwa jest ciąg, którego wartość może być dowolna wcale.</span><span class="sxs-lookup"><span data-stu-id="62df7-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="62df7-138">Ta wartość ciągu jest co klientów podczas ich poprosić o adres usługi z usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="62df7-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

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

    // the string returned here will be published in the Naming Service.
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

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="62df7-139">Usługa Service Fabric realizuje interfejsów API, która pozwala klientów i innych usług, a następnie poprosić dla tego adresu według nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="62df7-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="62df7-140">Jest to ważne, ponieważ adres usługi nie jest statyczne.</span><span class="sxs-lookup"><span data-stu-id="62df7-140">This is important because the service address is not static.</span></span> <span data-ttu-id="62df7-141">Usługi są przenoszone w klastrze do celów dostępności i równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="62df7-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="62df7-142">Jest to mechanizm, który zezwala klientom na rozpoznawanie adresu nasłuchiwania dla usługi.</span><span class="sxs-lookup"><span data-stu-id="62df7-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="62df7-143">Aby uzyskać pełny przewodnik sposobu pisania odbiornik komunikacji, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md) dla C#, natomiast dla języka Java można napisać własny implementację serwera HTTP, zobacz EchoServer aplikacji przykład: w https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="62df7-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="62df7-144">Podczas komunikacji z usługą</span><span class="sxs-lookup"><span data-stu-id="62df7-144">Communicating with a service</span></span>
<span data-ttu-id="62df7-145">Niezawodne interfejsu API usług zawiera następujące biblioteki do zapisania klientów komunikujących się z usługami.</span><span class="sxs-lookup"><span data-stu-id="62df7-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="62df7-146">Rozpoznanie punktu końcowego usługi</span><span class="sxs-lookup"><span data-stu-id="62df7-146">Service endpoint resolution</span></span>
<span data-ttu-id="62df7-147">Pierwszy krok w celu komunikacji z usługą jest do rozpoznania adresu punktu końcowego, partycji lub wystąpienia usługi, którą chcesz rozmawiać z.</span><span class="sxs-lookup"><span data-stu-id="62df7-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="62df7-148">`ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` Klasy narzędzie jest właściwością pierwotną podstawowe, ułatwiająca klientów określić punkt końcowy usługi w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="62df7-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="62df7-149">W terminologii usługi sieć szkieletowa proces określania punktu końcowego usługi jest określana jako *usługi rozpoznawania punktu końcowego*.</span><span class="sxs-lookup"><span data-stu-id="62df7-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="62df7-150">Aby połączyć się z usługami w klastrze, ServicePartitionResolver mogą być tworzone przy użyciu ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="62df7-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="62df7-151">Jest to zalecane użycie w większości sytuacji:</span><span class="sxs-lookup"><span data-stu-id="62df7-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="62df7-152">Aby połączyć się z usługami w innym klastrze, ServicePartitionResolver mogą być tworzone przy użyciu zestawu punktów końcowych klastra bramy.</span><span class="sxs-lookup"><span data-stu-id="62df7-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="62df7-153">Należy pamiętać, że punkty końcowe bramy są po prostu różnych punktów końcowych do łączenia się z tym samym klastrze.</span><span class="sxs-lookup"><span data-stu-id="62df7-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="62df7-154">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="62df7-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="62df7-155">Alternatywnie `ServicePartitionResolver` można przydzielić funkcję do tworzenia `FabricClient` do wewnętrznego użycia:</span><span class="sxs-lookup"><span data-stu-id="62df7-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

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

<span data-ttu-id="62df7-156">`FabricClient`jest obiekt, który jest używany do komunikacji z klastrem usługi sieć szkieletowa usług dla różnych operacji zarządzania w klastrze.</span><span class="sxs-lookup"><span data-stu-id="62df7-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="62df7-157">Jest to przydatne, jeśli chcesz mieć większą kontrolę nad jak program rozpoznawania nazw partycji usługi współdziała z klastra.</span><span class="sxs-lookup"><span data-stu-id="62df7-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="62df7-158">`FabricClient`buforuje wewnętrznie i jest zwykle kosztowne, dlatego ważne jest, aby ponownie wykorzystać `FabricClient` wystąpień, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="62df7-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="62df7-159">Metoda resolve należy pobrać adres usługi lub partycji usługi dla usług podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="62df7-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="62df7-160">Adres usługi można rozwiązać za pomocą ServicePartitionResolver, ale więcej pracy wymagane jest zapewnienie, że poprawnie można rozpoznać adresu.</span><span class="sxs-lookup"><span data-stu-id="62df7-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="62df7-161">Klient musi wykryć, czy próba połączenia nie powiodła się z powodu błędu przejściowego i można ponowić (np. usługi przenieść lub jest tymczasowo niedostępny), lub trwały błąd (np. usługa została usunięta lub żądany zasób nie istnieje już).</span><span class="sxs-lookup"><span data-stu-id="62df7-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="62df7-162">Wystąpienie usługi lub repliki można przenosić z węzła do węzła w dowolnym momencie kilka przyczyn.</span><span class="sxs-lookup"><span data-stu-id="62df7-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="62df7-163">Adres usługi rozpoznawane za pomocą ServicePartitionResolver może być przestarzały przez kod klienta podejmuje próbę nawiązania połączenia czas.</span><span class="sxs-lookup"><span data-stu-id="62df7-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="62df7-164">W takim przypadku ponownie klient musi ponownie rozpoznania adresu.</span><span class="sxs-lookup"><span data-stu-id="62df7-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="62df7-165">Zapewnianie poprzedniej `ResolvedServicePartition` wskazuje, że program rozpoznawania nazw wymaga ponownej próby zamiast po prostu pobrać adres pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="62df7-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="62df7-166">Zazwyczaj kod klienta należy działa z ServicePartitionResolver bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="62df7-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="62df7-167">Jest tworzony i przekazywane do fabryki klienta komunikacji niezawodnej usługi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="62df7-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="62df7-168">Fabryk korzystanie z tym programem rozpoznawania nazw można wygenerować obiektu klienta, który może służyć do komunikacji z usługami.</span><span class="sxs-lookup"><span data-stu-id="62df7-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="62df7-169">Komunikacja klientów i fabryki</span><span class="sxs-lookup"><span data-stu-id="62df7-169">Communication clients and factories</span></span>
<span data-ttu-id="62df7-170">Biblioteka fabryki komunikacji zawiera typowe wzorzec ponownych prób obsługi błędów, który ułatwia ponawianie połączeń z punktami końcowymi usług rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="62df7-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="62df7-171">Biblioteka fabryki zapewnia mechanizm ponów próbę, gdy Podaj programy obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="62df7-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="62df7-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`definiuje interfejs podstawowy zaimplementowana przez fabrykę klienta komunikacji, który spowoduje utworzenie klientów, którzy mogą komunikować się z usługą sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="62df7-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="62df7-173">Implementacja CommunicationClientFactory zależy od stosu komunikacji używane przez usługę sieć szkieletowa usług, których chce komunikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="62df7-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="62df7-174">Zapewnia niezawodne interfejsu API usług `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="62df7-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="62df7-175">Udostępnia podstawową implementację interfejsu CommunicationClientFactory i wykonuje zadania, które są wspólne dla wszystkich stosy komunikacji.</span><span class="sxs-lookup"><span data-stu-id="62df7-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="62df7-176">(Te zadania obejmują przy użyciu ServicePartitionResolver w celu określenia punktu końcowego usługi).</span><span class="sxs-lookup"><span data-stu-id="62df7-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="62df7-177">Klienci zwykle zaimplementować klasy abstrakcyjnej CommunicationClientFactoryBase do obsługi logiki, które dotyczą stosu komunikacji.</span><span class="sxs-lookup"><span data-stu-id="62df7-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="62df7-178">Komunikacja klienta po prostu otrzymuje adres i używa go do łączenia się z usługą.</span><span class="sxs-lookup"><span data-stu-id="62df7-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="62df7-179">Klient może używać dowolnego protokołu chce.</span><span class="sxs-lookup"><span data-stu-id="62df7-179">The client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="62df7-180">Fabryka klientów jest głównie odpowiedzialną za tworzenie komunikacji klientów.</span><span class="sxs-lookup"><span data-stu-id="62df7-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="62df7-181">Dla klientów, którzy nie Obsługa połączenie trwałe, takich jak klient HTTP fabryka tylko musi utworzyć i zwracany do klienta.</span><span class="sxs-lookup"><span data-stu-id="62df7-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="62df7-182">Inne protokoły zapewniające połączenie trwałe, takie jak niektóre protokoły binarnego, również powinny zostać zatwierdzone przez fabrykę, aby określić, czy połączenie musi zostać ponownie utworzone.</span><span class="sxs-lookup"><span data-stu-id="62df7-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

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

<span data-ttu-id="62df7-183">Ponadto program obsługi wyjątku jest odpowiedzialny za określenie, jakie działania w sytuacji, gdy wystąpi wyjątek.</span><span class="sxs-lookup"><span data-stu-id="62df7-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="62df7-184">Wyjątki są podzielone na **powtarzający operację** i **niepowtarzającego**.</span><span class="sxs-lookup"><span data-stu-id="62df7-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="62df7-185">**Niepowtarzającego** wyjątki po prostu pobrać zgłoszony do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="62df7-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="62df7-186">**powtarzający operację** dalsze wyjątki są dzielone na kategorie **przejściowa** i **nieprzejściowego**.</span><span class="sxs-lookup"><span data-stu-id="62df7-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="62df7-187">**Przejściowa** wyjątki są tymi, które można po prostu ponowione bez ponowne rozpoznanie adres punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="62df7-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="62df7-188">Obejmują one przejściowe problemy z siecią lub odpowiedzi na błędy usług innych niż te, które wskazują, że adres punktu końcowego usługi nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="62df7-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="62df7-189">**Inne niż przejściowy** wyjątki są te, które wymagają adres punktu końcowego usługi mają zostać rozwiązane ponownie.</span><span class="sxs-lookup"><span data-stu-id="62df7-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="62df7-190">Obejmują one wyjątki, które wskazują, że nie można osiągnąć punktu końcowego usługi, wskazującą usługi została przeniesiona do innego węzła.</span><span class="sxs-lookup"><span data-stu-id="62df7-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="62df7-191">`TryHandleException` Sprawia, że decyzja o danego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="62df7-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="62df7-192">Jeśli go **nie zna** jakie należy podjąć decyzje dotyczące wyjątek, powinien on zwrócić **false**.</span><span class="sxs-lookup"><span data-stu-id="62df7-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="62df7-193">Jeśli go **wiedzieć** jakie decyzja podejmowana, należy odpowiednio ustawić wynik i zwróć **true**.</span><span class="sxs-lookup"><span data-stu-id="62df7-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
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

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="62df7-194">Składanie wszystkiego razem</span><span class="sxs-lookup"><span data-stu-id="62df7-194">Putting it all together</span></span>
<span data-ttu-id="62df7-195">Z `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, i `IExceptionHandler(C#) / ExceptionHandler(Java)` zbudowana wokół protokołu komunikacyjnego, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` umieszczeniu wszystkich elementów i zawiera pętlę rozpoznawania adresów partycji usługi i obsługi błędów wokół tych składników.</span><span class="sxs-lookup"><span data-stu-id="62df7-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
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
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="62df7-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62df7-196">Next steps</span></span>
* <span data-ttu-id="62df7-197">Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt C# w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) lub [Java przykładowy projekt w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="62df7-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="62df7-198">Zdalne wywołania procedur z usług zdalnych niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="62df7-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="62df7-199">Interfejs API, który używa OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="62df7-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="62df7-200">Komunikacyjny WCF za pomocą niezawodnych usług</span><span class="sxs-lookup"><span data-stu-id="62df7-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
