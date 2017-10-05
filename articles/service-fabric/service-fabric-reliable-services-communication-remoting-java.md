---
title: "Usługa zdalnych w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług zdalnych umożliwia klientów i usług do komunikowania się z usługami za pomocą zdalnego wywołania procedury."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="15b20-103">Komunikacji zdalnej usługi z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="15b20-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15b20-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="15b20-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="15b20-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="15b20-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="15b20-106">Niezawodne usługi framework udostępnia mechanizm komunikacji zdalnej szybkie i łatwe Konfigurowanie zdalnego wywołania procedury dla usług.</span><span class="sxs-lookup"><span data-stu-id="15b20-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="15b20-107">Konfigurowanie komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="15b20-107">Set up remoting on a service</span></span>
<span data-ttu-id="15b20-108">Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="15b20-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="15b20-109">Utwórz interfejs do implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="15b20-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="15b20-110">Ten interfejs definiuje metody, które są dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="15b20-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="15b20-111">Metody muszą być zwracanie zadań metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="15b20-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="15b20-112">Musi implementować interfejs `microsoft.serviceFabric.services.remoting.Service` sygnalizują, że usługa ma interfejs usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="15b20-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="15b20-113">Użyj odbiornika usługi zdalne w usłudze.</span><span class="sxs-lookup"><span data-stu-id="15b20-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="15b20-114">Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="15b20-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="15b20-115">`FabricTransportServiceRemotingListener`można utworzyć odbiornik komunikacji zdalnej przy użyciu protokołu transportu domyślnego komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="15b20-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="15b20-116">Na przykład następującej usługi bezstanowej przedstawia jedną metodę można uzyskać za pośrednictwem zdalnego wywołania procedury "Hello World".</span><span class="sxs-lookup"><span data-stu-id="15b20-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="15b20-117">Argumenty i typy zwracane w interfejsie usługi może być żadnych typów prosty, złożonych lub niestandardowy, ale musi być możliwy do serializacji.</span><span class="sxs-lookup"><span data-stu-id="15b20-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="15b20-118">Wywołanie metody zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="15b20-118">Call remote service methods</span></span>
<span data-ttu-id="15b20-119">Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej odbywa się za pomocą lokalnego serwera proxy do usługi za pośrednictwem `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasy.</span><span class="sxs-lookup"><span data-stu-id="15b20-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="15b20-120">`ServiceProxyBase` Metoda tworzy lokalny serwer proxy przy użyciu tego samego interfejsu, który implementuje usługę.</span><span class="sxs-lookup"><span data-stu-id="15b20-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="15b20-121">Z tego serwera proxy możesz po prostu wywołać metod w interfejsie zdalnie.</span><span class="sxs-lookup"><span data-stu-id="15b20-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="15b20-122">W ramach usług zdalnych propaguje wyjątków zgłaszanych na usługę do klienta.</span><span class="sxs-lookup"><span data-stu-id="15b20-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="15b20-123">Logika sposób obsługi wyjątków po stronie klienta przy użyciu `ServiceProxyBase` bezpośrednio może obsłużyć wyjątki, które usługa zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="15b20-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="15b20-124">Okres istnienia usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="15b20-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="15b20-125">Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem.</span><span class="sxs-lookup"><span data-stu-id="15b20-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="15b20-126">Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go.</span><span class="sxs-lookup"><span data-stu-id="15b20-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="15b20-127">Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="15b20-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="15b20-128">Każdy ServiceProxy zawiera komunikacji klienta używany do wysyłania wiadomości przez sieć.</span><span class="sxs-lookup"><span data-stu-id="15b20-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="15b20-129">Podczas wywoływania interfejsu API, mamy wewnętrzny Sprawdź, czy komunikacji klient jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="15b20-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="15b20-130">Na podstawie tego wyniku, możemy ponownie utworzyć klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="15b20-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="15b20-131">Dlatego użytkownik musi ponownie utworzyć serviceproxy w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="15b20-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="15b20-132">Okres istnienia ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="15b20-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="15b20-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="15b20-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="15b20-134">Jeśli używasz interfejsu API `ServiceProxyBase.create` tworzenia serwera proxy, framework utworzy `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="15b20-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="15b20-135">Warto utworzyć jedną ręcznie, gdy trzeba zastąpić [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) właściwości.</span><span class="sxs-lookup"><span data-stu-id="15b20-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="15b20-136">Fabryka jest kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="15b20-136">Factory is an expensive operation.</span></span> <span data-ttu-id="15b20-137">`FabricServiceProxyFactory`obsługuje pamięć podręczną komunikacji klientów.</span><span class="sxs-lookup"><span data-stu-id="15b20-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="15b20-138">Najlepszym rozwiązaniem jest pamięć podręczna `FabricServiceProxyFactory` tak długo, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="15b20-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="15b20-139">Obsługa wyjątków komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="15b20-139">Remoting Exception Handling</span></span>
<span data-ttu-id="15b20-140">Zdalne wyjątek zgłoszony przez interfejs API usługi, są wysyłane do klienta jako runtimeexception — lub FabricException.</span><span class="sxs-lookup"><span data-stu-id="15b20-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="15b20-141">ServiceProxy obsłużyć wszystkie wyjątki trybu Failover jest tworzony dla partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="15b20-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="15b20-142">Umożliwia rozwiązanie ponownie punkty końcowe w przypadku Exceptions(Non-Transient Exceptions) trybu Failover i ponowi próbę połączenia z właściwego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="15b20-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="15b20-143">Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.</span><span class="sxs-lookup"><span data-stu-id="15b20-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="15b20-144">W przypadku TransientExceptions tylko ponowną wywołania.</span><span class="sxs-lookup"><span data-stu-id="15b20-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="15b20-145">Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="15b20-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="15b20-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Użytkownik może skonfigurować te wartości przez przekazanie obiektu OperationRetrySettings ServiceProxyFactory konstruktora.</span><span class="sxs-lookup"><span data-stu-id="15b20-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b20-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15b20-147">Next steps</span></span>
* [<span data-ttu-id="15b20-148">Zabezpieczenia komunikacji niezawodnej usług</span><span class="sxs-lookup"><span data-stu-id="15b20-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
