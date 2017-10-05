---
title: "Pomoc bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Przegląd sposobów zapewnienia bezpiecznej komunikacji dla niezawodnych usług, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="e4074-103">Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="e4074-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4074-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="e4074-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="e4074-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4074-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="e4074-106">Zabezpieczeń jest jednym z najważniejszych aspektów komunikacji.</span><span class="sxs-lookup"><span data-stu-id="e4074-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="e4074-107">Struktura aplikacji niezawodne usługi zapewnia kilka stosy wbudowane komunikacji i narzędzi, których można użyć w celu poprawy bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="e4074-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="e4074-108">Ten artykuł zawiera informacje o sposób poprawiania zabezpieczeń podczas korzystania z usług zdalnych i stosu komunikacji usługi Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="e4074-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="e4074-109">Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="e4074-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="e4074-110">Używamy istniejącej [przykład](service-fabric-reliable-services-communication-remoting.md) który wyjaśnia, jak skonfigurować komunikację zdalną dla niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="e4074-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="e4074-111">Aby ułatwić zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e4074-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="e4074-112">Tworzenie interfejsu `IHelloWorldStateful`, który definiuje metody, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e4074-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="e4074-113">Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="e4074-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="e4074-114">Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="e4074-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="e4074-115">Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e4074-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="e4074-116">Upewnij się, że certyfikat, który ma być używany do zabezpieczania komunikacji usługi jest zainstalowany na wszystkich węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e4074-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="e4074-117">Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="e4074-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="e4074-118">Podaj je bezpośrednio w kodzie usługi:</span><span class="sxs-lookup"><span data-stu-id="e4074-118">Provide them directly in the service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="e4074-119">Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="e4074-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="e4074-120">Dodaj `TransportSettings` sekcji w pliku settings.xml.</span><span class="sxs-lookup"><span data-stu-id="e4074-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="e4074-121">W takim przypadku `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e4074-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="e4074-122">Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml `FabricTransportRemotingListenerSettings ` załaduje wszystkie ustawienia w tej sekcji ma domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4074-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="e4074-123">W takim przypadku `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e4074-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="e4074-124">Gdy wywoływać metod w usług zabezpieczonych przy użyciu stosu usług zdalnych, zamiast `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasę, aby utworzyć serwer proxy usługi, użyj `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="e4074-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="e4074-125">Przekazywanie `FabricTransportRemotingSettings`, który zawiera `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="e4074-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="e4074-126">Jeśli kod klienta działa w ramach usługi, można załadować `FabricTransportRemotingSettings` z pliku settings.xml.</span><span class="sxs-lookup"><span data-stu-id="e4074-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="e4074-127">Utwórz sekcję HelloWorldClientTransportSettings, która jest podobna do kodu usługi, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e4074-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="e4074-128">Wprowadź następujące zmiany w kodzie klienta:</span><span class="sxs-lookup"><span data-stu-id="e4074-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="e4074-129">Jeśli klient nie jest uruchomiony jako część usługi, można utworzyć plik client_name.settings.xml w tej samej lokalizacji, gdzie jest client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="e4074-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="e4074-130">Następnie można utworzyć sekcji TransportSettings w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="e4074-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="e4074-131">Podobnie jak usługa, jeśli dodasz `TransportSettings` części settings.xml/client_name.settings.xml klienta `FabricTransportRemotingSettings` ładuje wszystkie ustawienia w tej sekcji ma domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4074-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="e4074-132">W takim przypadku jeszcze bardziej jest uproszczone wcześniejszych kodu:</span><span class="sxs-lookup"><span data-stu-id="e4074-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="e4074-133">Zabezpieczanie usługi podczas korzystania z stosu komunikacji usługi WCF</span><span class="sxs-lookup"><span data-stu-id="e4074-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="e4074-134">Używamy istniejącej [przykład](service-fabric-reliable-services-communication-wcf.md) który wyjaśnia, jak skonfigurować stosu WCF komunikacji niezawodnej usług.</span><span class="sxs-lookup"><span data-stu-id="e4074-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="e4074-135">Aby ułatwić zabezpieczanie usługi podczas korzystania z stosu komunikacji usługi WCF, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e4074-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="e4074-136">Dla usługi, należy zabezpieczyć odbiornik komunikacji WCF (`WcfCommunicationListener`) utworzony.</span><span class="sxs-lookup"><span data-stu-id="e4074-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="e4074-137">Aby to zrobić, należy zmodyfikować `CreateServiceReplicaListeners` metody.</span><span class="sxs-lookup"><span data-stu-id="e4074-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in the ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="e4074-138">W kliencie `WcfCommunicationClient` klasy, który został utworzony w poprzedniej [przykład](service-fabric-reliable-services-communication-wcf.md) pozostaje niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="e4074-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="e4074-139">Jednak należy zastąpić `CreateClientAsync` metody `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="e4074-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="e4074-140">Użyj `SecureWcfCommunicationClientFactory` można utworzyć klienta WCF komunikacji (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="e4074-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="e4074-141">Korzystając z klienta do wywołania metody usługi.</span><span class="sxs-lookup"><span data-stu-id="e4074-141">Use the client to invoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="e4074-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4074-142">Next steps</span></span>
* [<span data-ttu-id="e4074-143">Interfejs API OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e4074-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
