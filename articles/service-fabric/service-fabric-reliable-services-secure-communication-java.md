---
title: "aaaHelp bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Omówienie jak toohelp bezpiecznej komunikacji niezawodnej usług które są uruchomione w klastrze usługi sieć szkieletowa usług Azure."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="47c03-103">Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="47c03-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47c03-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="47c03-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="47c03-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="47c03-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="47c03-106">Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="47c03-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="47c03-107">Będziemy używać istniejącego [przykład](service-fabric-reliable-services-communication-remoting-java.md) objaśniający sposób tooset się komunikację zdalną dla niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="47c03-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="47c03-108">toohelp Zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47c03-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="47c03-109">Tworzenie interfejsu `HelloWorldStateless`, który definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="47c03-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="47c03-110">Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakietu.</span><span class="sxs-lookup"><span data-stu-id="47c03-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="47c03-111">Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="47c03-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="47c03-112">Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="47c03-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="47c03-113">Upewnij się, które mają toohelp toouse bezpiecznej komunikacji usługi jest zainstalowany we wszystkich węzłach klastra hello hello certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="47c03-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="47c03-114">Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="47c03-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="47c03-115">Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="47c03-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="47c03-116">Dodaj `TransportSettings` sekcji w pliku settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="47c03-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="47c03-117">W takim przypadku hello `createServiceInstanceListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="47c03-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="47c03-118">Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml hello bez żadnych prefiksów `FabricTransportListenerSettings` załaduje wszystkie ustawienia hello w tej sekcji ma domyślnie.</span><span class="sxs-lookup"><span data-stu-id="47c03-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="47c03-119">W takim przypadku hello `CreateServiceInstanceListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="47c03-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="47c03-120">Podczas wywoływania metody zabezpieczonych usługi przy użyciu hello stosu usług zdalnych, zamiast hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate klasy serwera proxy usługi, użyj `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="47c03-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="47c03-121">Jeśli kod klienta hello jest uruchomiony jako część usługi, można załadować `FabricTransportSettings` z pliku settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="47c03-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="47c03-122">Sekcja TransportSettings, która jest podobny kod usługi toohello, należy utworzyć, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="47c03-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="47c03-123">Wprowadź hello następującego kodu klienta toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="47c03-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
