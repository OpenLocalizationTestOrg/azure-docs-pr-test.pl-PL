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
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="42004-103">Komunikacja oparta na WCF stos niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="42004-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="42004-104">Niezawodne usługi Hello pozwala usługi autorów toochoose hello stosu komunikacji mają toouse dla usługi.</span><span class="sxs-lookup"><span data-stu-id="42004-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="42004-105">Można podłączyć stosu komunikacji hello wybranych przez nich za pośrednictwem hello **ICommunicationListener** zwrócony z hello [CreateServiceReplicaListeners lub CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) metody.</span><span class="sxs-lookup"><span data-stu-id="42004-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="42004-106">Witaj framework zapewnia implementacji stosu komunikacji hello oparte na powitania Windows Communication Foundation (WCF) dla autorów usług, którzy chcą toouse komunikacji usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="42004-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="42004-107">Odbiornik komunikacji usługi WCF</span><span class="sxs-lookup"><span data-stu-id="42004-107">WCF Communication Listener</span></span>
<span data-ttu-id="42004-108">Implementacja Hello specyficzne dla usługi WCF **ICommunicationListener** są dostarczane przez hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** klasy.</span><span class="sxs-lookup"><span data-stu-id="42004-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="42004-109">Co najmniej powiedz mamy typu kontraktu usługi`ICalculator`</span><span class="sxs-lookup"><span data-stu-id="42004-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="42004-110">Można utworzyć odbiornik komunikacji usługi WCF w hello usługi powitania po sposób.</span><span class="sxs-lookup"><span data-stu-id="42004-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="42004-111">Pisanie klientów dla stosu komunikacji hello WCF</span><span class="sxs-lookup"><span data-stu-id="42004-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="42004-112">Do pisania klientów toocommunicate z usługami przy użyciu usługi WCF, hello framework zapewnia **WcfClientCommunicationFactory**, która jest implementacją hello specyficzne dla usługi WCF [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="42004-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="42004-113">kanał komunikacyjny WCF Hello są dostępne z hello **WcfCommunicationClient** utworzone przez hello **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="42004-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="42004-114">Kod klienta można użyć hello **WcfCommunicationClientFactory** wraz z hello **WcfCommunicationClient** z zaimplementowanym **ServicePartitionClient** toodetermine Witaj punktu końcowego usługi i komunikować się z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="42004-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

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
> <span data-ttu-id="42004-115">domyślne Hello ServicePartitionResolver przyjęto założenie, że klient hello jest uruchomiona w tym samym klastrze jako usługa hello.</span><span class="sxs-lookup"><span data-stu-id="42004-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="42004-116">Jeśli to znaczy nie hello case, Utwórz obiekt ServicePartitionResolver i podaj punkty końcowe połączenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="42004-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="42004-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42004-117">Next steps</span></span>
* [<span data-ttu-id="42004-118">Wywołanie procedury zdalnej komunikacji zdalnej niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="42004-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="42004-119">Interfejs API OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="42004-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="42004-120">Zabezpieczenia komunikacji niezawodnej usług</span><span class="sxs-lookup"><span data-stu-id="42004-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

