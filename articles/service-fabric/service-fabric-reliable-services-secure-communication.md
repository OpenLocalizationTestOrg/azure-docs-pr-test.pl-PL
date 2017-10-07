---
title: "aaaHelp bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Omówienie jak toohelp bezpiecznej komunikacji niezawodnej usług które są uruchomione w klastrze usługi sieć szkieletowa usług Azure."
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
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="4d12d-103">Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="4d12d-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d12d-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="4d12d-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="4d12d-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4d12d-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="4d12d-106">Zabezpieczeń jest jednym z najważniejszych aspektów komunikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4d12d-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="4d12d-107">Struktura aplikacji Hello niezawodne usługi zapewnia kilka stosy wbudowane komunikacji i narzędzia, których można używać tooimprove zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4d12d-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="4d12d-108">Ten artykuł zawiera informacje o jak tooimprove zabezpieczeń podczas korzystania z usług zdalnych i hello stosu komunikacji usługi Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="4d12d-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="4d12d-109">Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="4d12d-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="4d12d-110">Używamy istniejącej [przykład](service-fabric-reliable-services-communication-remoting.md) objaśniający sposób tooset się komunikację zdalną dla niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="4d12d-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="4d12d-111">toohelp Zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d12d-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="4d12d-112">Tworzenie interfejsu `IHelloWorldStateful`, który definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="4d12d-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="4d12d-113">Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4d12d-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="4d12d-114">Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="4d12d-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="4d12d-115">Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4d12d-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="4d12d-116">Upewnij się, które mają toohelp toouse bezpiecznej komunikacji usługi jest zainstalowany we wszystkich węzłach klastra hello hello certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="4d12d-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="4d12d-117">Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="4d12d-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="4d12d-118">Podaj je bezpośrednio w kodzie usługi hello:</span><span class="sxs-lookup"><span data-stu-id="4d12d-118">Provide them directly in hello service code:</span></span>

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
   2. <span data-ttu-id="4d12d-119">Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="4d12d-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="4d12d-120">Dodaj `TransportSettings` sekcji w pliku settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="4d12d-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="4d12d-121">W takim przypadku hello `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4d12d-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="4d12d-122">Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml hello `FabricTransportRemotingListenerSettings ` załaduje wszystkie ustawienia hello w tej sekcji ma domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4d12d-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="4d12d-123">W takim przypadku hello `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4d12d-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="4d12d-124">Podczas wywoływania metody zabezpieczonych usługi przy użyciu hello stosu usług zdalnych, zamiast hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate klasy serwera proxy usługi, użyj `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="4d12d-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="4d12d-125">Przekazywanie `FabricTransportRemotingSettings`, który zawiera `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4d12d-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="4d12d-126">Jeśli kod klienta hello jest uruchomiony jako część usługi, można załadować `FabricTransportRemotingSettings` z pliku settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="4d12d-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="4d12d-127">Sekcja HelloWorldClientTransportSettings, która jest podobny kod usługi toohello, należy utworzyć, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4d12d-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="4d12d-128">Wprowadź hello następującego kodu klienta toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="4d12d-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="4d12d-129">Powitania klienta nie jest uruchomiony jako część usługi, należy utworzyć plik client_name.settings.xml w hello tej samej lokalizacji, gdzie jest hello client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="4d12d-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="4d12d-130">Następnie można utworzyć sekcji TransportSettings w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="4d12d-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="4d12d-131">Podobne toohello usługi, jeśli dodasz `TransportSettings` części settings.xml/client_name.settings.xml klienta `FabricTransportRemotingSettings` ładuje wszystkie ustawienia hello z tej sekcji domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4d12d-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="4d12d-132">W takim przypadku hello wcześniej kod jest jeszcze bardziej uproszczone:</span><span class="sxs-lookup"><span data-stu-id="4d12d-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="4d12d-133">Zabezpieczanie usługi podczas korzystania z stosu komunikacji usługi WCF</span><span class="sxs-lookup"><span data-stu-id="4d12d-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="4d12d-134">Używamy istniejącej [przykład](service-fabric-reliable-services-communication-wcf.md) objaśniający sposób tooset się komunikacji WCF stosu niezawodnych usług.</span><span class="sxs-lookup"><span data-stu-id="4d12d-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="4d12d-135">toohelp Zabezpieczanie usługi, gdy używasz stosu komunikacji usługi WCF, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d12d-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="4d12d-136">Dla usługi hello należy toohelp bezpiecznego hello WCF komunikacji odbiornika (`WcfCommunicationListener`) utworzony.</span><span class="sxs-lookup"><span data-stu-id="4d12d-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="4d12d-137">toodo, zmodyfikuj hello `CreateServiceReplicaListeners` metody.</span><span class="sxs-lookup"><span data-stu-id="4d12d-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in hello ServiceHost credentials.
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
2. <span data-ttu-id="4d12d-138">W kliencie hello hello `WcfCommunicationClient` klasy, który został utworzony w hello poprzedniej [przykład](service-fabric-reliable-services-communication-wcf.md) pozostaje niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="4d12d-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="4d12d-139">Jednak toooverride hello `CreateClientAsync` metody `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="4d12d-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
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

    <span data-ttu-id="4d12d-140">Użyj `SecureWcfCommunicationClientFactory` toocreate komunikacji klienta WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="4d12d-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="4d12d-141">Za pomocą powitania klienta tooinvoke usługi metod.</span><span class="sxs-lookup"><span data-stu-id="4d12d-141">Use hello client tooinvoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4d12d-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d12d-142">Next steps</span></span>
* [<span data-ttu-id="4d12d-143">Interfejs API OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4d12d-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
