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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Jak toouse hello komunikacji niezawodnej usługi interfejsów API
Azure Service Fabric jako platformę jest całkowicie niezależny o komunikacji między usługami. Wszystkie protokoły i stosy są dopuszczalne, z UDP tooHTTP. Jest zapasowej toochoose dewelopera usługi toohello komunikowania usług. Struktura aplikacji Hello niezawodne usługi zawiera komunikacji wbudowanej stosów oraz interfejsów API, których można używać toobuild składniki niestandardowe komunikacji w sieci.

## <a name="set-up-service-communication"></a>Konfigurowanie komunikacji usługi
Hello niezawodnej usługi interfejsu API używa prosty interfejs do komunikacji usługi. tooopen punktu końcowego usługi, po prostu zaimplementować ten interfejs.

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

Następnie można dodać implementacji odbiornik komunikacji, przywracając jego zastąpienie metody klasy oparta na usłudze.

Dla usługi bezstanowej:

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

Dla stanowych usług:

> [!NOTE]
> Niezawodne usługi stanowej nie są obsługiwane w języku Java jeszcze.
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

W obu przypadkach należy zwracać kolekcja odbiorników. Dzięki temu toolisten Twojego usługi na wiele punktów końcowych potencjalnie przy użyciu różnych protokołów, za pomocą wielu odbiorników. Na przykład może mieć odbiornik HTTP i oddzielne odbiornika protokołu WebSocket. Każdy odbiornik pobiera nazwę i hello wynikowy zbiór *Nazwa: adres* pary są reprezentowane jako obiekt JSON, gdy klient żąda hello adres nasłuchiwania dla wystąpienia usługi lub partycji.

Usługi bezstanowej zastąpienie hello zwraca kolekcję ServiceInstanceListeners. A `ServiceInstanceListener` zawiera toocreate funkcja `ICommunicationListener(C#) / CommunicationListener(Java)` i nadaje mu nazwę. W przypadku usług stanowych zastąpienie hello zwraca kolekcję ServiceReplicaListeners. To jest nieco inne niż jego odpowiednik bezstanowych, ponieważ `ServiceReplicaListener` ma tooopen opcji `ICommunicationListener` w replikach pomocniczych. Nie można użyć wielu odbiorników komunikacji w usłudze tylko można również określić które odbiorników akceptowania żądań w replikach pomocniczych i te, które nasłuchuje repliki podstawowej.

Na przykład może mieć ServiceRemotingListener, pobierającej wywołania RPC tylko na podstawowym repliki, a drugi, niestandardowe odbiornik, który przyjmuje odczytu żądań w replikach pomocniczych za pośrednictwem protokołu HTTP:

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
> Podczas tworzenia wiele odbiorników dla usługi, każdy odbiornika **musi** należy nadać unikatową nazwę.
>
>

Ponadto opisano hello punktów końcowych, które są wymagane dla usługi hello w hello [manifestu usługi](service-fabric-application-model.md) sekcji hello w punktach końcowych.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

odbiornik komunikacji Hello dostęp do zasobów punktu końcowego hello przydzielony tooit z hello `CodePackageActivationContext` w hello `ServiceContext`. odbiornik Hello następnie można uruchomić nasłuchiwanie żądań, gdy jest otwarty.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Punkt końcowy zasoby są typowe toohello całej usługi pakietu, a po aktywowaniu pakiet usługi hello są przydzielone przez sieć szkieletowa usług. Wiele replik usługi hostowanej w hello tego samego elementu ServiceHost może udostępniać hello sam port. Oznacza to, że odbiornik komunikacji hello powinna obsługiwać Udostępnianie portów. Hello zaleca się, jak to zrobić to dla hello komunikacji odbiornika toouse hello partycji identyfikator i identyfikator repliki i wystąpienia podczas generowania hello nasłuchiwania adresów.
>
>

### <a name="service-address-registration"></a>Rejestracja adres usługi
Usługa systemowa o nazwie hello *Naming Service* działa w klastrze usługi sieć szkieletowa usług. Witaj Naming Service jest rejestratora dla usług i ich adresów, które każdego wystąpienia lub repliki usługi hello nasłuchuje. Gdy hello `OpenAsync(C#) / openAsync(Java)` metody `ICommunicationListener(C#) / CommunicationListener(Java)` zakończeniu jego powrotu wartość pobiera zarejestrowane w hello Naming Service. To zwrócić wartość, która pobiera ciąg, którego wartość może być dowolna na wszystkich opublikowanych w powitalne jest Naming Service. Ta wartość ciągu jest, jakie klientów wyświetlać, gdy został poproszony o adres dla usługi hello z hello Naming Service.

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

Sieć szkieletowa usług zawiera interfejsy API umożliwiające klientów i innych usług toothen poprosić dla tego adresu według nazwy usługi. Jest to ważne, ponieważ adres usługi hello nie jest statyczne. Usługi są przenoszone w klastrze hello do celów dostępności i równoważenia zasobów. Jest to mechanizm hello Zezwalaj klientom Witaj tooresolve nasłuchiwania adresów dla usługi.

> [!NOTE]
> Do ukończenia toowrite odbiornik komunikacji, zobacz temat Omówienie [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md) dla C#, natomiast dla języka Java można napisać własny implementację serwera HTTP, zobacz EchoServer aplikacji przykład: w https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Podczas komunikacji z usługą
Hello niezawodnej interfejsu API usług zawiera hello następujące biblioteki toowrite klientów, które komunikują się z usługami.

### <a name="service-endpoint-resolution"></a>Rozpoznanie punktu końcowego usługi
Witaj pierwszy krok toocommunication z usługą jest tooresolve adresu punktu końcowego hello partycji lub wystąpienie usługi hello, który ma tootalk do. Witaj `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` klasy narzędzie jest właściwością pierwotną podstawowe, ułatwiająca klientów, określenia hello punkt końcowy usługi w czasie wykonywania. W terminologii usługi sieć szkieletowa hello proces określania hello punkt końcowy usługi jest hello określonego tooas *usługi rozpoznawania punktu końcowego*.

tooservices tooconnect w klastrze, ServicePartitionResolver mogą być tworzone przy użyciu ustawień domyślnych. Jest to zalecane użycie w większości sytuacji hello:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooservices tooconnect w innym klastrze, ServicePartitionResolver mogą być tworzone przy użyciu zestawu punktów końcowych klastra bramy. Pamiętaj, że punkty końcowe bramy jest po prostu różnych punktów końcowych do łączenia toohello tego samego klastra. Na przykład:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Alternatywnie `ServicePartitionResolver` można przydzielić funkcję do tworzenia `FabricClient` toouse wewnętrznie:

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

`FabricClient`jest hello obiekt, który jest używany toocommunicate z klastrem usługi sieć szkieletowa hello różnych operacji zarządzania w klastrze hello. Jest to przydatne, jeśli chcesz mieć większą kontrolę nad jak program rozpoznawania nazw partycji usługi współdziała z klastra. `FabricClient`buforuje wewnętrznie i jest zwykle kosztowne toocreate, dlatego jest ważne tooreuse `FabricClient` wystąpień, jak to możliwe.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Metody rozpoznawania jest używane tooretrieve hello adresu usługi lub partycji usługi dla usług podzielonym na partycje.

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

Adres usługi można rozwiązać za pomocą ServicePartitionResolver, ale wymagane jest więcej pracy tooensure hello rozpoznać adresu można poprawnie. Klient musi toodetect czy hello próba połączenia nie powiodła się z powodu błędu przejściowego i można ponowić (np. usługi przenieść lub jest tymczasowo niedostępny), lub trwały błąd (np. usługa została usunięta lub hello żądany zasób nie istnieje). Wystąpienie usługi lub repliki można przenosić z węzła toonode w dowolnym momencie kilka przyczyn. adres usługi Hello rozpoznawane za pomocą ServicePartitionResolver może być przestarzały czasu hello tooconnect prób kodu klienta. W takim przypadku ponownie powitania klienta wymaga adresu hello toore rozwiązanie. Zapewnianie hello poprzedniej `ResolvedServicePartition` wskazuje, że Witaj ponownie program rozpoznawania nazw musi tootry zamiast po prostu pobrać adres pamięci podręcznej.

Zazwyczaj powitania klienta kodu muszą działa z hello ServicePartitionResolver bezpośrednio. Jest tworzony i przekazywane fabryki klienta toocommunication w hello niezawodnej usługi interfejsu API. fabryki Hello korzystanie z mechanizmu rozpoznawania hello toogenerate obiektu klienta, które mogą być używane toocommunicate z usługami.

### <a name="communication-clients-and-factories"></a>Komunikacja klientów i fabryki
Witaj komunikacji fabryki biblioteka zawiera typowy wzorzec ponownych prób obsługi błędów, który ułatwia ponawianie punktów końcowych usługi tooresolved połączenia. Biblioteka fabryki Hello zapewnia mechanizm ponawiania hello podczas Podaj hello programy obsługi błędów.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`definiuje interfejs podstawowy hello zaimplementowana przez fabrykę klienta komunikacji, który spowoduje utworzenie klientów, którzy mogą komunikować tooa usługi sieć szkieletowa usług. Witaj implementacji powitalne CommunicationClientFactory zależy od stosu komunikacji hello używane przez usługę sieć szkieletowa usług hello, w którym powitania klienta chce toocommunicate. Hello niezawodnej interfejsu API usług zawiera `CommunicationClientFactoryBase<TCommunicationClient>`. Udostępnia podstawową implementację interfejsu CommunicationClientFactory hello i wykonuje zadania, które są typowe tooall hello komunikacji stosów. (Te zadania obejmują przy użyciu punktu końcowego usługi hello toodetermine ServicePartitionResolver). Klienci implementuje zwykle hello abstrakcyjny CommunicationClientFactoryBase klasy toohandle logiki określonej toohello stosu komunikacji.

Hello komunikacji klienta po prostu odbiera adres i używa go tooconnect tooa usługi. Witaj, klient może używać niezależnie od protokołu chce.

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

Fabryka klientów Hello jest głównie odpowiedzialną za tworzenie komunikacji klientów. Dla klientów, którzy nie Obsługa połączenie trwałe, takich jak klient HTTP fabryki hello musi tylko toocreate i zwracany powitania klienta. Inne protokoły zapewniające połączenie trwałe, takie jak niektóre protokoły binarnego, również powinny zostać zatwierdzone przez toodetermine fabryki hello czy połączenia hello wymaga toobe utworzony ponownie.  

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

Ponadto program obsługi wyjątku jest odpowiedzialny za określenie, jakie tootake działania po wystąpieniu wyjątku. Wyjątki są podzielone na **powtarzający operację** i **niepowtarzającego**.

* **Niepowtarzającego** wyjątki po prostu pobrać zgłoszony wstecz toohello wywołującego.
* **powtarzający operację** dalsze wyjątki są dzielone na kategorie **przejściowa** i **nieprzejściowego**.
  * **Przejściowa** wyjątki są tymi, które można po prostu ponowione bez ponowne rozpoznanie adres punktu końcowego usługi hello. Obejmują one przejściowych problemów z siecią lub odpowiedzi na błędy usług innych niż te, które wskazują adres punktu końcowego usługi hello nie istnieje.
  * **Inne niż przejściowy** wyjątki są te, które wymagają hello usługi punktu końcowego adresu toobe ponownie rozwiązane. Obejmują one wyjątki, które wskazują, że punkt końcowy usługi hello jest nieosiągalny, wskazujący, że usługa hello przeniósł tooa innego węzła.

Witaj `TryHandleException` sprawia, że decyzja o danego wyjątku. Jeśli go **nie zna** jakie toomake decyzji o wyjątku, powinien on zwrócić **false**. Jeśli go **wiedzieć** jakie toomake decyzja powinna odpowiednio ustawić wynik hello i zwracać **true**.

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
### <a name="putting-it-all-together"></a>Składanie wszystkiego razem
Z `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, i `IExceptionHandler(C#) / ExceptionHandler(Java)` zbudowana wokół protokołu komunikacyjnego, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` umieszczeniu wszystkich elementów i zapewnia odporność obsługi hello i usługi partycji adres rozpoznawania pętlę wokół tych składników.

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

## <a name="next-steps"></a>Następne kroki
* Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt C# w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) lub [Java przykładowy projekt w witrynie GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Zdalne wywołania procedur z usług zdalnych niezawodne usługi](service-fabric-reliable-services-communication-remoting.md)
* [Interfejs API, który używa OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Komunikacyjny WCF za pomocą niezawodnych usług](service-fabric-reliable-services-communication-wcf.md)
