---
title: "aaaService zdalnych w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług zdalnych umożliwia klientom i usługami toocommunicate przy użyciu usługi za pomocą zdalnego wywołania procedury."
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="7ced3-103">Komunikacji zdalnej usługi z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7ced3-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ced3-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="7ced3-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="7ced3-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="7ced3-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="7ced3-106">Hello niezawodne usługi framework zapewnia tooquickly mechanizm komunikacji zdalnej i łatwe Konfigurowanie zdalnego wywołania procedury dla usług.</span><span class="sxs-lookup"><span data-stu-id="7ced3-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="7ced3-107">Konfigurowanie komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="7ced3-107">Set up remoting on a service</span></span>
<span data-ttu-id="7ced3-108">Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="7ced3-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="7ced3-109">Utwórz interfejs dla tooimplement Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="7ced3-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="7ced3-110">Ten interfejs definiuje metody hello, które są dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="7ced3-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="7ced3-111">metody Hello muszą być zwracanie zadań metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="7ced3-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="7ced3-112">musi implementować interfejs Hello `microsoft.serviceFabric.services.remoting.Service` toosignal, który hello usługi ma interfejs usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="7ced3-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="7ced3-113">Użyj odbiornika usługi zdalne w usłudze.</span><span class="sxs-lookup"><span data-stu-id="7ced3-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="7ced3-114">Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="7ced3-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="7ced3-115">`FabricTransportServiceRemotingListener`może być używane toocreate odbiornika usługi zdalne, za pomocą protokołu transportowego remoting domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="7ced3-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="7ced3-116">Na przykład hello następującej usługi bezstanowej przedstawia tooget pojedynczej metody "Hello World" za pośrednictwem zdalnego wywołania procedury.</span><span class="sxs-lookup"><span data-stu-id="7ced3-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="7ced3-117">argumenty Hello i hello zwracać typów w interfejsie usługi hello mogą znajdować się wszystkie typy prosty, złożonych lub niestandardowy, ale musi być możliwy do serializacji.</span><span class="sxs-lookup"><span data-stu-id="7ced3-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="7ced3-118">Wywołanie metody zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="7ced3-118">Call remote service methods</span></span>
<span data-ttu-id="7ced3-119">Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej hello odbywa się przy użyciu usługi toohello lokalnego serwera proxy za pośrednictwem hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasy.</span><span class="sxs-lookup"><span data-stu-id="7ced3-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="7ced3-120">Witaj `ServiceProxyBase` metoda tworzy lokalny serwer proxy przy użyciu hello implementuje tego samego interfejsu, który hello usługi.</span><span class="sxs-lookup"><span data-stu-id="7ced3-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="7ced3-121">Z tego serwera proxy możesz po prostu wywołać metod w interfejsie hello zdalnie.</span><span class="sxs-lookup"><span data-stu-id="7ced3-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="7ced3-122">Hello remoting framework propaguje wyjątków zgłaszanych na powitania usługi toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="7ced3-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="7ced3-123">Logika sposób obsługi wyjątków na powitania klienta przy użyciu `ServiceProxyBase` może bezpośrednio obsługi wyjątków, które hello zgłasza usługi.</span><span class="sxs-lookup"><span data-stu-id="7ced3-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="7ced3-124">Okres istnienia usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="7ced3-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="7ced3-125">Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem.</span><span class="sxs-lookup"><span data-stu-id="7ced3-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="7ced3-126">Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go.</span><span class="sxs-lookup"><span data-stu-id="7ced3-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="7ced3-127">Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku hello.</span><span class="sxs-lookup"><span data-stu-id="7ced3-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="7ced3-128">Każdy ServiceProxy zawiera komunikacji klienta używany toosend wiadomości za pośrednictwem przewodowy hello.</span><span class="sxs-lookup"><span data-stu-id="7ced3-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="7ced3-129">Podczas wywoływania interfejsu API, mamy toosee wewnętrznego sprawdzania Jeśli komunikacja klient jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="7ced3-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="7ced3-130">Na podstawie tego wyniku, utworzymy ponownie powitania klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="7ced3-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="7ced3-131">Dlatego użytkownik nie ma potrzeby serviceproxy toorecreate w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="7ced3-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="7ced3-132">Okres istnienia ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="7ced3-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="7ced3-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="7ced3-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="7ced3-134">Jeśli używasz interfejsu API `ServiceProxyBase.create` tworzenia serwera proxy, framework utworzy `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="7ced3-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="7ced3-135">Ręcznie jest przydatne toocreate, co w przypadku należy toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) właściwości.</span><span class="sxs-lookup"><span data-stu-id="7ced3-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="7ced3-136">Fabryka jest kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="7ced3-136">Factory is an expensive operation.</span></span> <span data-ttu-id="7ced3-137">`FabricServiceProxyFactory`obsługuje pamięć podręczną komunikacji klientów.</span><span class="sxs-lookup"><span data-stu-id="7ced3-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="7ced3-138">Najlepszym rozwiązaniem jest toocache `FabricServiceProxyFactory` tak długo, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="7ced3-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="7ced3-139">Obsługa wyjątków komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="7ced3-139">Remoting Exception Handling</span></span>
<span data-ttu-id="7ced3-140">Wszystkie hello zdalnego został zwrócony wyjątek przez interfejs API usługi, są wysyłane jako runtimeexception — lub FabricException wstecz toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="7ced3-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="7ced3-141">ServiceProxy obsłużyć wszystkie wyjątki trybu Failover dla partycji usługi hello, jest tworzona dla.</span><span class="sxs-lookup"><span data-stu-id="7ced3-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="7ced3-142">Rozpoznaje ponownie hello punktów końcowych, jeśli wywołanie hello Exceptions(Non-Transient Exceptions) trybu Failover i ponownych prób hello właściwego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="7ced3-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="7ced3-143">Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.</span><span class="sxs-lookup"><span data-stu-id="7ced3-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="7ced3-144">W przypadku TransientExceptions tylko ponowną hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="7ced3-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="7ced3-145">Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="7ced3-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="7ced3-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Użytkownik może skonfigurować te wartości, przekazując OperationRetrySettings obiektu tooServiceProxyFactory konstruktora.</span><span class="sxs-lookup"><span data-stu-id="7ced3-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ced3-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ced3-147">Next steps</span></span>
* [<span data-ttu-id="7ced3-148">Zabezpieczenia komunikacji niezawodnej usług</span><span class="sxs-lookup"><span data-stu-id="7ced3-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
