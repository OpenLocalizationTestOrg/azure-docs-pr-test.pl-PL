---
title: "stosu komunikacji usług WCF aaaReliable | Dokumentacja firmy Microsoft"
description: "Hello wbudowanych WCF komunikacji stosu w sieci szkieletowej usług zawiera Usługa klienta WCF komunikacji niezawodnej usług."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Komunikacja oparta na WCF stos niezawodne usługi
Niezawodne usługi Hello pozwala usługi autorów toochoose hello stosu komunikacji mają toouse dla usługi. Można podłączyć stosu komunikacji hello wybranych przez nich za pośrednictwem hello **ICommunicationListener** zwrócony z hello [CreateServiceReplicaListeners lub CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) metody. Witaj framework zapewnia implementacji stosu komunikacji hello oparte na powitania Windows Communication Foundation (WCF) dla autorów usług, którzy chcą toouse komunikacji usługi WCF.

## <a name="wcf-communication-listener"></a>Odbiornik komunikacji usługi WCF
Implementacja Hello specyficzne dla usługi WCF **ICommunicationListener** są dostarczane przez hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** klasy.

Co najmniej powiedz mamy typu kontraktu usługi`ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Można utworzyć odbiornik komunikacji usługi WCF w hello usługi powitania po sposób.

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Pisanie klientów dla stosu komunikacji hello WCF
Do pisania klientów toocommunicate z usługami przy użyciu usługi WCF, hello framework zapewnia **WcfClientCommunicationFactory**, która jest implementacją hello specyficzne dla usługi WCF [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

kanał komunikacyjny WCF Hello są dostępne z hello **WcfCommunicationClient** utworzone przez hello **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Kod klienta można użyć hello **WcfCommunicationClientFactory** wraz z hello **WcfCommunicationClient** z zaimplementowanym **ServicePartitionClient** toodetermine Witaj punktu końcowego usługi i komunikować się z usługą hello.

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> domyślne Hello ServicePartitionResolver przyjęto założenie, że klient hello jest uruchomiona w tym samym klastrze jako usługa hello. Jeśli to znaczy nie hello case, Utwórz obiekt ServicePartitionResolver i podaj punkty końcowe połączenia klastra hello.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Wywołanie procedury zdalnej komunikacji zdalnej niezawodne usługi](service-fabric-reliable-services-communication-remoting.md)
* [Interfejs API OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Zabezpieczenia komunikacji niezawodnej usług](service-fabric-reliable-services-secure-communication.md)

