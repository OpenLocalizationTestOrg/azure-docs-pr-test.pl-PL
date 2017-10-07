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
# <a name="service-remoting-with-reliable-services"></a>Komunikacji zdalnej usługi z usługami Reliable Services
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java w systemie Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Hello niezawodne usługi framework zapewnia tooquickly mechanizm komunikacji zdalnej i łatwe Konfigurowanie zdalnego wywołania procedury dla usług.

## <a name="set-up-remoting-on-a-service"></a>Konfigurowanie komunikacji zdalnej usługi
Konfigurowanie komunikacji zdalnej usługi odbywa się w dwóch prostych krokach:

1. Utwórz interfejs dla tooimplement Twojej usługi. Ten interfejs definiuje metody hello, które są dostępne dla zdalnego wywołania procedury w usłudze. metody Hello muszą być zwracanie zadań metod asynchronicznych. musi implementować interfejs Hello `microsoft.serviceFabric.services.remoting.Service` toosignal, który hello usługi ma interfejs usług zdalnych.
2. Użyj odbiornika usługi zdalne w usłudze. Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej. `FabricTransportServiceRemotingListener`może być używane toocreate odbiornika usługi zdalne, za pomocą protokołu transportowego remoting domyślne hello.

Na przykład hello następującej usługi bezstanowej przedstawia tooget pojedynczej metody "Hello World" za pośrednictwem zdalnego wywołania procedury.

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
> argumenty Hello i hello zwracać typów w interfejsie usługi hello mogą znajdować się wszystkie typy prosty, złożonych lub niestandardowy, ale musi być możliwy do serializacji.
>
>

## <a name="call-remote-service-methods"></a>Wywołanie metody zdalnej usługi
Wywołanie metod w usłudze przy użyciu stosu komunikacji zdalnej hello odbywa się przy użyciu usługi toohello lokalnego serwera proxy za pośrednictwem hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasy. Witaj `ServiceProxyBase` metoda tworzy lokalny serwer proxy przy użyciu hello implementuje tego samego interfejsu, który hello usługi. Z tego serwera proxy możesz po prostu wywołać metod w interfejsie hello zdalnie.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

Hello remoting framework propaguje wyjątków zgłaszanych na powitania usługi toohello klienta. Logika sposób obsługi wyjątków na powitania klienta przy użyciu `ServiceProxyBase` może bezpośrednio obsługi wyjątków, które hello zgłasza usługi.

## <a name="service-proxy-lifetime"></a>Okres istnienia usługi serwera Proxy
Tworzenie ServiceProxy jest operacją lekkie użytkownika można utworzyć dowolną liczbę, zgodnie z zapotrzebowaniem. Serwer Proxy usługi mogą być ponownie używane, tak długo, jak długo użytkownik musiał go. Użytkownik może ponownie użyć tego samego serwera proxy w przypadku wyjątku hello. Każdy ServiceProxy zawiera komunikacji klienta używany toosend wiadomości za pośrednictwem przewodowy hello. Podczas wywoływania interfejsu API, mamy toosee wewnętrznego sprawdzania Jeśli komunikacja klient jest prawidłowy. Na podstawie tego wyniku, utworzymy ponownie powitania klienta komunikacji. Dlatego użytkownik nie ma potrzeby serviceproxy toorecreate w przypadku wyjątku.

### <a name="serviceproxyfactory-lifetime"></a>Okres istnienia ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) fabryki, która tworzy proxy dla różnych usług zdalnych interfejsów. Jeśli używasz interfejsu API `ServiceProxyBase.create` tworzenia serwera proxy, framework utworzy `FabricServiceProxyFactory`.
Ręcznie jest przydatne toocreate, co w przypadku należy toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) właściwości.
Fabryka jest kosztowna operacja. `FabricServiceProxyFactory`obsługuje pamięć podręczną komunikacji klientów.
Najlepszym rozwiązaniem jest toocache `FabricServiceProxyFactory` tak długo, jak to możliwe.

## <a name="remoting-exception-handling"></a>Obsługa wyjątków komunikacji zdalnej
Wszystkie hello zdalnego został zwrócony wyjątek przez interfejs API usługi, są wysyłane jako runtimeexception — lub FabricException wstecz toohello klienta.

ServiceProxy obsłużyć wszystkie wyjątki trybu Failover dla partycji usługi hello, jest tworzona dla. Rozpoznaje ponownie hello punktów końcowych, jeśli wywołanie hello Exceptions(Non-Transient Exceptions) trybu Failover i ponownych prób hello właściwego punktu końcowego. Liczba ponownych prób dla trybu failover wyjątku jest nieokreślony.
W przypadku TransientExceptions tylko ponowną hello wywołania.

Domyślne parametry ponawiania są zachowywane przez [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Użytkownik może skonfigurować te wartości, przekazując OperationRetrySettings obiektu tooServiceProxyFactory konstruktora.

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczenia komunikacji niezawodnej usług](service-fabric-reliable-services-secure-communication.md)
