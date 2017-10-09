---
title: "aaaService zdalnych w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług zdalnych umożliwia klientom i usługami toocommunicate przy użyciu usługi za pomocą zdalnego wywołania procedury."
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
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="2ad97-103">Komunikacji zdalnej usługi z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2ad97-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="2ad97-104">Dla usług, które nie są powiązane protokołu komunikacyjnego określonego tooa lub stosu, takie jak WebAPI, Windows Communication Foundation (WCF) lub innych osób, hello niezawodne usługi framework zapewnia tooquickly mechanizm komunikacji zdalnej i łatwe Konfigurowanie zdalnego wywołania procedury dla usługi.</span><span class="sxs-lookup"><span data-stu-id="2ad97-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="2ad97-105">Konfigurowanie komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="2ad97-105">Set up remoting on a service</span></span>
<span data-ttu-id="2ad97-106">Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="2ad97-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="2ad97-107">Utwórz interfejs dla tooimplement Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="2ad97-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="2ad97-108">Ten interfejs definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="2ad97-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="2ad97-109">metody Hello muszą być zwracanie zadań metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="2ad97-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="2ad97-110">musi implementować interfejs Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal, który hello usługi ma interfejs usług zdalnych.</span><span class="sxs-lookup"><span data-stu-id="2ad97-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="2ad97-111">Użyj odbiornika usługi zdalne w usłudze.</span><span class="sxs-lookup"><span data-stu-id="2ad97-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="2ad97-112">Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="2ad97-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="2ad97-113">Witaj `Microsoft.ServiceFabric.Services.Remoting.Runtime` przestrzeń nazw zawiera metody rozszerzenia`CreateServiceRemotingListener` zarówno bezstanowych i stanowych usług, które można można używane toocreate odbiornika usługi zdalne za pomocą hello domyślny zdalnych protokołu transportowego.</span><span class="sxs-lookup"><span data-stu-id="2ad97-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="2ad97-114">Uwaga: hello `Remoting` przestrzeń nazw jest dostępna jako pakietu nuget oddzielne o nazwie`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="2ad97-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="2ad97-115">Na przykład hello następującej usługi bezstanowej przedstawia tooget pojedynczej metody "Hello World" za pośrednictwem zdalnego wywołania procedury.</span><span class="sxs-lookup"><span data-stu-id="2ad97-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="2ad97-116">Witaj argumentów i hello zwracać typów w interfejsie usługi hello mogą znajdować się wszystkie typy proste, złożonych lub niestandardowego, ale musi być możliwy do serializacji przez hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ad97-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="2ad97-117">Wywołanie metody zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="2ad97-117">Call remote service methods</span></span>
<span data-ttu-id="2ad97-118">Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej hello odbywa się przy użyciu usługi toohello lokalnego serwera proxy za pośrednictwem hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="2ad97-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="2ad97-119">Witaj `ServiceProxy` metoda tworzy lokalny serwer proxy przy użyciu hello implementuje tego samego interfejsu, który hello usługi.</span><span class="sxs-lookup"><span data-stu-id="2ad97-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="2ad97-120">Z tego serwera proxy możesz po prostu wywołać metod w interfejsie hello zdalnie.</span><span class="sxs-lookup"><span data-stu-id="2ad97-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="2ad97-121">Hello remoting framework propaguje wyjątków zgłaszanych na powitania usługi toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="2ad97-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="2ad97-122">Logika sposób obsługi wyjątków na powitania klienta przy użyciu `ServiceProxy` może bezpośrednio obsługi wyjątków, które hello zgłasza usługi.</span><span class="sxs-lookup"><span data-stu-id="2ad97-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="2ad97-123">Okres istnienia usługi serwera Proxy</span><span class="sxs-lookup"><span data-stu-id="2ad97-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="2ad97-124">Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem.</span><span class="sxs-lookup"><span data-stu-id="2ad97-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="2ad97-125">Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go.</span><span class="sxs-lookup"><span data-stu-id="2ad97-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="2ad97-126">Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku hello.</span><span class="sxs-lookup"><span data-stu-id="2ad97-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="2ad97-127">Każdy ServiceProxy zawiera komunikacji klienta używany toosend wiadomości za pośrednictwem przewodowy hello.</span><span class="sxs-lookup"><span data-stu-id="2ad97-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="2ad97-128">Podczas wywoływania interfejsu API, mamy toosee wewnętrznego sprawdzania Jeśli komunikacja klient jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="2ad97-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="2ad97-129">Na podstawie tego wyniku, utworzymy ponownie powitania klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="2ad97-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="2ad97-130">Dlatego użytkownik nie ma potrzeby serviceproxy toorecreate w przypadku wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2ad97-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="2ad97-131">Okres istnienia ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="2ad97-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="2ad97-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="2ad97-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="2ad97-133">Jeśli używasz ServiceProxy.Create interfejsu API tworzenia serwera proxy, framework tworzy hello singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="2ad97-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="2ad97-134">Ręcznie jest przydatne toocreate, co w przypadku należy toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) właściwości.</span><span class="sxs-lookup"><span data-stu-id="2ad97-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="2ad97-135">Fabryka jest kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="2ad97-135">Factory is an expensive operation.</span></span> <span data-ttu-id="2ad97-136">ServiceProxyFactory przechowuje w pamięci podręcznej klienta komunikacji.</span><span class="sxs-lookup"><span data-stu-id="2ad97-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="2ad97-137">Najlepszym rozwiązaniem jest toocache ServiceProxyFactory tak długo, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="2ad97-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="2ad97-138">Obsługa wyjątków komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="2ad97-138">Remoting Exception Handling</span></span>
<span data-ttu-id="2ad97-139">Wszystkie hello zdalnego został zwrócony wyjątek przez interfejs API usługi, są wysyłane wstecz toohello klienta jako AggregateException.</span><span class="sxs-lookup"><span data-stu-id="2ad97-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="2ad97-140">RemoteExceptions powinien podlegać serializacji DataContract w przeciwnym razie [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) jest zgłaszany toohello proxy interfejsu API z powodu błędu serializacji hello w nim.</span><span class="sxs-lookup"><span data-stu-id="2ad97-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="2ad97-141">ServiceProxy obsłużyć wszystkie wyjątki trybu Failover dla partycji usługi hello, jest tworzona dla.</span><span class="sxs-lookup"><span data-stu-id="2ad97-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="2ad97-142">Rozpoznaje ponownie hello punktów końcowych, jeśli wywołanie hello Exceptions(Non-Transient Exceptions) trybu Failover i ponownych prób hello właściwego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="2ad97-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="2ad97-143">Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.</span><span class="sxs-lookup"><span data-stu-id="2ad97-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="2ad97-144">W przypadku TransientExceptions tylko ponowną hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="2ad97-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="2ad97-145">Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="2ad97-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="2ad97-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Użytkownik może skonfigurować te wartości, przekazując OperationRetrySettings obiektu tooServiceProxyFactory konstruktora.</span><span class="sxs-lookup"><span data-stu-id="2ad97-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ad97-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ad97-147">Next steps</span></span>
* [<span data-ttu-id="2ad97-148">Interfejs API OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="2ad97-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2ad97-149">Komunikacyjny WCF z usługami Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2ad97-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="2ad97-150">Zabezpieczenia komunikacji niezawodnej usług</span><span class="sxs-lookup"><span data-stu-id="2ad97-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
