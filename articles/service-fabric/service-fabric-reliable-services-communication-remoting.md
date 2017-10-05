---
title: "<span data-ttu-id=\"0c308-101\">Usługa zdalnych w sieci szkieletowej usług | Dokumentacja firmy Microsoft</span><span class=\"sxs-lookup\"><span data-stu-id=\"0c308-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"0c308-102\">Sieć szkieletowa usług zdalnych umożliwia klientów i usług do komunikowania się z usługami za pomocą zdalnego wywołania procedury.</span><span class=\"sxs-lookup\"><span data-stu-id=\"0c308-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="0c308-103">Komunikacji zdalnej usługi z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0c308-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="0c308-104">Dla usług, które nie są związane z protokołu komunikacyjnego konkretnego lub stosu, takie jak WebAPI, Windows Communication Foundation (WCF) lub innych osób, w ramach niezawodnej usługi udostępnia mechanizm komunikacji zdalnej szybkie i łatwe Konfigurowanie zdalnego wywołania procedury dla usługi.</span><span class="sxs-lookup"><span data-stu-id="0c308-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="0c308-105">Konfigurowanie komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="0c308-105">Set up remoting on a service</span></span>
<span data-ttu-id="0c308-106">Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="0c308-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="0c308-107">Utwórz interfejs do implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="0c308-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="0c308-108">Ten interfejs definiuje metody, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="0c308-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="0c308-109">Metody muszą być zwracanie zadań metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="0c308-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="0c308-110">Musi implementować interfejs `Microsoft.ServiceFabric.Services.Remoting.IService` sygnalizują, że usługa ma interfejs usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="0c308-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="0c308-111">Użyj odbiornika usługi zdalne w usłudze.</span><span class="sxs-lookup"><span data-stu-id="0c308-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="0c308-112">Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="0c308-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="0c308-113">`Microsoft.ServiceFabric.Services.Remoting.Runtime` Przestrzeń nazw zawiera metody rozszerzenia`CreateServiceRemotingListener` dla usług zarówno bezstanowe i stanowe, które mogą służyć do tworzenia odbiornik komunikacji zdalnej przy użyciu protokołu transportu domyślnego komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="0c308-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="0c308-114">Uwaga: `Remoting` przestrzeń nazw jest dostępna jako pakietu nuget oddzielne o nazwie`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="0c308-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="0c308-115">Na przykład następującej usługi bezstanowej przedstawia jedną metodę można uzyskać za pośrednictwem zdalnego wywołania procedury "Hello World".</span><span class="sxs-lookup"><span data-stu-id="0c308-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="0c308-116">Argumenty i typy zwracane w interfejsie usługi może być żadnych typów prosty, złożonych lub niestandardowy, ale musi być serializację za pomocą programu .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c308-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="0c308-117">Wywołanie metody zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="0c308-117">Call remote service methods</span></span>
<span data-ttu-id="0c308-118">Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej odbywa się za pomocą lokalnego serwera proxy do usługi za pośrednictwem `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="0c308-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="0c308-119">`ServiceProxy` Metoda tworzy lokalny serwer proxy przy użyciu tego samego interfejsu, który implementuje usługę.</span><span class="sxs-lookup"><span data-stu-id="0c308-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="0c308-120">Z tego serwera proxy możesz po prostu wywołać metod w interfejsie zdalnie.</span><span class="sxs-lookup"><span data-stu-id="0c308-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="0c308-121">W ramach usług zdalnych propaguje wyjątków zgłaszanych na usługę do klienta.</span><span class="sxs-lookup"><span data-stu-id="0c308-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="0c308-122">Logika sposób obsługi wyjątków po stronie klienta przy użyciu `ServiceProxy` bezpośrednio może obsłużyć wyjątki, które usługa zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="0c308-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="0c308-123">Okres istnienia usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="0c308-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="0c308-124">Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem.</span><span class="sxs-lookup"><span data-stu-id="0c308-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="0c308-125">Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go.</span><span class="sxs-lookup"><span data-stu-id="0c308-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="0c308-126">Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="0c308-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="0c308-127">Każdy ServiceProxy zawiera komunikacji klienta używany do wysyłania wiadomości przez sieć.</span><span class="sxs-lookup"><span data-stu-id="0c308-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="0c308-128">Podczas wywoływania interfejsu API, mamy wewnętrzny Sprawdź, czy komunikacji klient jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="0c308-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="0c308-129">Na podstawie tego wyniku, możemy ponownie utworzyć klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0c308-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="0c308-130">Dlatego użytkownik musi ponownie utworzyć serviceproxy w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="0c308-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="0c308-131">Okres istnienia ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="0c308-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="0c308-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="0c308-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="0c308-133">Jeśli używasz ServiceProxy.Create interfejsu API tworzenia serwera proxy, framework tworzy singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="0c308-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="0c308-134">Warto utworzyć jedną ręcznie, gdy trzeba zastąpić [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) właściwości.</span><span class="sxs-lookup"><span data-stu-id="0c308-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="0c308-135">Fabryka jest kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="0c308-135">Factory is an expensive operation.</span></span> <span data-ttu-id="0c308-136">ServiceProxyFactory przechowuje w pamięci podręcznej klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0c308-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="0c308-137">Najlepszym rozwiązaniem jest pamięci podręcznej ServiceProxyFactory tak długo, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="0c308-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="0c308-138">Obsługa wyjątków komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="0c308-138">Remoting Exception Handling</span></span>
<span data-ttu-id="0c308-139">Zdalne wyjątek zgłoszony przez interfejs API usługi, są wysyłane do klienta jako AggregateException.</span><span class="sxs-lookup"><span data-stu-id="0c308-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="0c308-140">RemoteExceptions powinien podlegać serializacji DataContract w przeciwnym razie [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) jest zgłaszany do interfejsu API serwera proxy z powodu błędu serializacji w nim.</span><span class="sxs-lookup"><span data-stu-id="0c308-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="0c308-141">ServiceProxy obsłużyć wszystkie wyjątki trybu Failover jest tworzony dla partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="0c308-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="0c308-142">Umożliwia rozwiązanie ponownie punkty końcowe w przypadku Exceptions(Non-Transient Exceptions) trybu Failover i ponowi próbę połączenia z właściwego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="0c308-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="0c308-143">Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.</span><span class="sxs-lookup"><span data-stu-id="0c308-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="0c308-144">W przypadku TransientExceptions tylko ponowną wywołania.</span><span class="sxs-lookup"><span data-stu-id="0c308-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="0c308-145">Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="0c308-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="0c308-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Użytkownik może skonfigurować te wartości przez przekazanie obiektu OperationRetrySettings ServiceProxyFactory konstruktora.</span><span class="sxs-lookup"><span data-stu-id="0c308-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c308-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c308-147">Next steps</span></span>
* [<span data-ttu-id="0c308-148">Interfejs API OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="0c308-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="0c308-149">Komunikacyjny WCF z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0c308-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="0c308-150">Zabezpieczenia komunikacji niezawodnej usług</span><span class="sxs-lookup"><span data-stu-id="0c308-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
