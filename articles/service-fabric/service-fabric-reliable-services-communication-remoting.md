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
# <a name="service-remoting-with-reliable-services"></a>Komunikacji zdalnej usługi z usługami Reliable Services
Dla usług, które nie są powiązane protokołu komunikacyjnego określonego tooa lub stosu, takie jak WebAPI, Windows Communication Foundation (WCF) lub innych osób, hello niezawodne usługi framework zapewnia tooquickly mechanizm komunikacji zdalnej i łatwe Konfigurowanie zdalnego wywołania procedury dla usługi.

## <a name="set-up-remoting-on-a-service"></a>Konfigurowanie komunikacji zdalnej usługi
Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:

1. Utwórz interfejs dla tooimplement Twojej usługi. Ten interfejs definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze. metody Hello muszą być zwracanie zadań metod asynchronicznych. musi implementować interfejs Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal, który hello usługi ma interfejs usług zdalnych.
2. Użyj odbiornika usługi zdalne w usłudze. Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej. Witaj `Microsoft.ServiceFabric.Services.Remoting.Runtime` przestrzeń nazw zawiera metody rozszerzenia`CreateServiceRemotingListener` zarówno bezstanowych i stanowych usług, które można można używane toocreate odbiornika usługi zdalne za pomocą hello domyślny zdalnych protokołu transportowego.

Uwaga: hello `Remoting` przestrzeń nazw jest dostępna jako pakietu nuget oddzielne o nazwie`Microsoft.ServiceFabric.Services.Remoting` 

Na przykład hello następującej usługi bezstanowej przedstawia tooget pojedynczej metody "Hello World" za pośrednictwem zdalnego wywołania procedury.

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
> Witaj argumentów i hello zwracać typów w interfejsie usługi hello mogą znajdować się wszystkie typy proste, złożonych lub niestandardowego, ale musi być możliwy do serializacji przez hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Wywołanie metody zdalnej usługi
Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej hello odbywa się przy użyciu usługi toohello lokalnego serwera proxy za pośrednictwem hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasy. Witaj `ServiceProxy` metoda tworzy lokalny serwer proxy przy użyciu hello implementuje tego samego interfejsu, który hello usługi. Z tego serwera proxy możesz po prostu wywołać metod w interfejsie hello zdalnie.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Hello remoting framework propaguje wyjątków zgłaszanych na powitania usługi toohello klienta. Logika sposób obsługi wyjątków na powitania klienta przy użyciu `ServiceProxy` może bezpośrednio obsługi wyjątków, które hello zgłasza usługi.

## <a name="service-proxy-lifetime"></a>Okres istnienia usługi serwera Proxy
Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem. Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go. Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku hello. Każdy ServiceProxy zawiera komunikacji klienta używany toosend wiadomości za pośrednictwem przewodowy hello. Podczas wywoływania interfejsu API, mamy toosee wewnętrznego sprawdzania Jeśli komunikacja klient jest prawidłowy. Na podstawie tego wyniku, utworzymy ponownie powitania klienta komunikacji. Dlatego użytkownik nie ma potrzeby serviceproxy toorecreate w przypadku wyjątku.

### <a name="serviceproxyfactory-lifetime"></a>Okres istnienia ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów. Jeśli używasz ServiceProxy.Create interfejsu API tworzenia serwera proxy, framework tworzy hello singelton ServiceProxyFactory.
Ręcznie jest przydatne toocreate, co w przypadku należy toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) właściwości.
Fabryka jest kosztowna operacja. ServiceProxyFactory przechowuje w pamięci podręcznej klienta komunikacji.
Najlepszym rozwiązaniem jest toocache ServiceProxyFactory tak długo, jak to możliwe.

## <a name="remoting-exception-handling"></a>Obsługa wyjątków komunikacji zdalnej
Wszystkie hello zdalnego został zwrócony wyjątek przez interfejs API usługi, są wysyłane wstecz toohello klienta jako AggregateException. RemoteExceptions powinien podlegać serializacji DataContract w przeciwnym razie [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) jest zgłaszany toohello proxy interfejsu API z powodu błędu serializacji hello w nim.

ServiceProxy obsłużyć wszystkie wyjątki trybu Failover dla partycji usługi hello, jest tworzona dla. Rozpoznaje ponownie hello punktów końcowych, jeśli wywołanie hello Exceptions(Non-Transient Exceptions) trybu Failover i ponownych prób hello właściwego punktu końcowego. Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.
W przypadku TransientExceptions tylko ponowną hello wywołania.

Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Użytkownik może skonfigurować te wartości, przekazując OperationRetrySettings obiektu tooServiceProxyFactory konstruktora.

## <a name="next-steps"></a>Następne kroki
* [Interfejs API OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Komunikacyjny WCF z usługami Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Zabezpieczenia komunikacji niezawodnej usług](service-fabric-reliable-services-secure-communication.md)
