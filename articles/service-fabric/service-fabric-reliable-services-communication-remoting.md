---
title: "Usługa zdalnych w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług zdalnych umożliwia klientów i usług do komunikowania się z usługami za pomocą zdalnego wywołania procedury."
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
# <a name="service-remoting-with-reliable-services"></a>Komunikacji zdalnej usługi z usługami Reliable Services
Dla usług, które nie są związane z protokołu komunikacyjnego konkretnego lub stosu, takie jak WebAPI, Windows Communication Foundation (WCF) lub innych osób, w ramach niezawodnej usługi udostępnia mechanizm komunikacji zdalnej szybkie i łatwe Konfigurowanie zdalnego wywołania procedury dla usługi.

## <a name="set-up-remoting-on-a-service"></a>Konfigurowanie komunikacji zdalnej usługi
Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:

1. Utwórz interfejs do implementacji usługi. Ten interfejs definiuje metody, które będą dostępne dla zdalnego wywołania procedury w usłudze. Metody muszą być zwracanie zadań metod asynchronicznych. Musi implementować interfejs `Microsoft.ServiceFabric.Services.Remoting.IService` sygnalizują, że usługa ma interfejs usług zdalnych.
2. Użyj odbiornika usługi zdalne w usłudze. Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej. `Microsoft.ServiceFabric.Services.Remoting.Runtime` Przestrzeń nazw zawiera metody rozszerzenia`CreateServiceRemotingListener` dla usług zarówno bezstanowe i stanowe, które mogą służyć do tworzenia odbiornik komunikacji zdalnej przy użyciu protokołu transportu domyślnego komunikacji zdalnej.

Uwaga: `Remoting` przestrzeń nazw jest dostępna jako pakietu nuget oddzielne o nazwie`Microsoft.ServiceFabric.Services.Remoting` 

Na przykład następującej usługi bezstanowej przedstawia jedną metodę można uzyskać za pośrednictwem zdalnego wywołania procedury "Hello World".

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
> Argumenty i typy zwracane w interfejsie usługi może być żadnych typów prosty, złożonych lub niestandardowy, ale musi być serializację za pomocą programu .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Wywołanie metody zdalnej usługi
Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej odbywa się za pomocą lokalnego serwera proxy do usługi za pośrednictwem `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasy. `ServiceProxy` Metoda tworzy lokalny serwer proxy przy użyciu tego samego interfejsu, który implementuje usługę. Z tego serwera proxy możesz po prostu wywołać metod w interfejsie zdalnie.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

W ramach usług zdalnych propaguje wyjątków zgłaszanych na usługę do klienta. Logika sposób obsługi wyjątków po stronie klienta przy użyciu `ServiceProxy` bezpośrednio może obsłużyć wyjątki, które usługa zgłasza wyjątek.

## <a name="service-proxy-lifetime"></a>Okres istnienia usługi serwera Proxy
Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem. Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go. Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku. Każdy ServiceProxy zawiera komunikacji klienta używany do wysyłania wiadomości przez sieć. Podczas wywoływania interfejsu API, mamy wewnętrzny Sprawdź, czy komunikacji klient jest prawidłowy. Na podstawie tego wyniku, możemy ponownie utworzyć klienta komunikacji. Dlatego użytkownik musi ponownie utworzyć serviceproxy w przypadku wyjątku.

### <a name="serviceproxyfactory-lifetime"></a>Okres istnienia ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów. Jeśli używasz ServiceProxy.Create interfejsu API tworzenia serwera proxy, framework tworzy singelton ServiceProxyFactory.
Warto utworzyć jedną ręcznie, gdy trzeba zastąpić [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) właściwości.
Fabryka jest kosztowna operacja. ServiceProxyFactory przechowuje w pamięci podręcznej klienta komunikacji.
Najlepszym rozwiązaniem jest pamięci podręcznej ServiceProxyFactory tak długo, jak to możliwe.

## <a name="remoting-exception-handling"></a>Obsługa wyjątków komunikacji zdalnej
Zdalne wyjątek zgłoszony przez interfejs API usługi, są wysyłane do klienta jako AggregateException. RemoteExceptions powinien podlegać serializacji DataContract w przeciwnym razie [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) jest zgłaszany do interfejsu API serwera proxy z powodu błędu serializacji w nim.

ServiceProxy obsłużyć wszystkie wyjątki trybu Failover jest tworzony dla partycji usługi. Umożliwia rozwiązanie ponownie punkty końcowe w przypadku Exceptions(Non-Transient Exceptions) trybu Failover i ponowi próbę połączenia z właściwego punktu końcowego. Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.
W przypadku TransientExceptions tylko ponowną wywołania.

Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Użytkownik może skonfigurować te wartości przez przekazanie obiektu OperationRetrySettings ServiceProxyFactory konstruktora.

## <a name="next-steps"></a>Następne kroki
* [Interfejs API OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Komunikacyjny WCF z usługami Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Zabezpieczenia komunikacji niezawodnej usług](service-fabric-reliable-services-secure-communication.md)
