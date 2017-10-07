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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java w systemie Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

Zabezpieczeń jest jednym z najważniejszych aspektów komunikacji hello. Struktura aplikacji Hello niezawodne usługi zapewnia kilka stosy wbudowane komunikacji i narzędzia, których można używać tooimprove zabezpieczeń. Ten artykuł zawiera informacje o jak tooimprove zabezpieczeń podczas korzystania z usług zdalnych i hello stosu komunikacji usługi Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi
Używamy istniejącej [przykład](service-fabric-reliable-services-communication-remoting.md) objaśniający sposób tooset się komunikację zdalną dla niezawodne usługi. toohelp Zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:

1. Tworzenie interfejsu `IHelloWorldStateful`, który definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze. Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` przestrzeni nazw. Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.

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
2. Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.

    Upewnij się, które mają toohelp toouse bezpiecznej komunikacji usługi jest zainstalowany we wszystkich węzłach klastra hello hello certyfikatu hello. Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:

   1. Podaj je bezpośrednio w kodzie usługi hello:

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
   2. Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):

       Dodaj `TransportSettings` sekcji w pliku settings.xml hello.

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

       W takim przypadku hello `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:

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

        Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml hello `FabricTransportRemotingListenerSettings ` załaduje wszystkie ustawienia hello w tej sekcji ma domyślnie.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        W takim przypadku hello `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:

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
3. Podczas wywoływania metody zabezpieczonych usługi przy użyciu hello stosu usług zdalnych, zamiast hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate klasy serwera proxy usługi, użyj `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Przekazywanie `FabricTransportRemotingSettings`, który zawiera `SecurityCredentials`.

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

    Jeśli kod klienta hello jest uruchomiony jako część usługi, można załadować `FabricTransportRemotingSettings` z pliku settings.xml hello. Sekcja HelloWorldClientTransportSettings, która jest podobny kod usługi toohello, należy utworzyć, jak pokazano wcześniej. Wprowadź hello następującego kodu klienta toohello zmiany:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Powitania klienta nie jest uruchomiony jako część usługi, należy utworzyć plik client_name.settings.xml w hello tej samej lokalizacji, gdzie jest hello client_name.exe. Następnie można utworzyć sekcji TransportSettings w tym pliku.

    Podobne toohello usługi, jeśli dodasz `TransportSettings` części settings.xml/client_name.settings.xml klienta `FabricTransportRemotingSettings` ładuje wszystkie ustawienia hello z tej sekcji domyślnie.

    W takim przypadku hello wcześniej kod jest jeszcze bardziej uproszczone:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Zabezpieczanie usługi podczas korzystania z stosu komunikacji usługi WCF
Używamy istniejącej [przykład](service-fabric-reliable-services-communication-wcf.md) objaśniający sposób tooset się komunikacji WCF stosu niezawodnych usług. toohelp Zabezpieczanie usługi, gdy używasz stosu komunikacji usługi WCF, wykonaj następujące kroki:

1. Dla usługi hello należy toohelp bezpiecznego hello WCF komunikacji odbiornika (`WcfCommunicationListener`) utworzony. toodo, zmodyfikuj hello `CreateServiceReplicaListeners` metody.

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
2. W kliencie hello hello `WcfCommunicationClient` klasy, który został utworzony w hello poprzedniej [przykład](service-fabric-reliable-services-communication-wcf.md) pozostaje niezmieniona. Jednak toooverride hello `CreateClientAsync` metody `WcfCommunicationClientFactory`:

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

    Użyj `SecureWcfCommunicationClientFactory` toocreate komunikacji klienta WCF (`WcfCommunicationClient`). Za pomocą powitania klienta tooinvoke usługi metod.

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

## <a name="next-steps"></a>Następne kroki
* [Interfejs API OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
