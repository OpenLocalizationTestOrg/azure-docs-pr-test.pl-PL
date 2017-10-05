---
title: "Pomoc bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Przegląd sposobów zapewnienia bezpiecznej komunikacji dla niezawodnych usług, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure."
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
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="5ee12-103">Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="5ee12-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ee12-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="5ee12-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="5ee12-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5ee12-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="5ee12-106">Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi</span><span class="sxs-lookup"><span data-stu-id="5ee12-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="5ee12-107">Będziemy używać istniejącego [przykład](service-fabric-reliable-services-communication-remoting-java.md) który wyjaśnia, jak skonfigurować komunikację zdalną dla niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="5ee12-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="5ee12-108">Aby ułatwić zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ee12-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="5ee12-109">Tworzenie interfejsu `HelloWorldStateless`, który definiuje metody, które będą dostępne dla zdalnego wywołania procedury w usłudze.</span><span class="sxs-lookup"><span data-stu-id="5ee12-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="5ee12-110">Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakietu.</span><span class="sxs-lookup"><span data-stu-id="5ee12-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="5ee12-111">Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="5ee12-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="5ee12-112">Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5ee12-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="5ee12-113">Upewnij się, że certyfikat, który ma być używany do zabezpieczania komunikacji usługi jest zainstalowany na wszystkich węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="5ee12-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="5ee12-114">Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="5ee12-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="5ee12-115">Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="5ee12-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="5ee12-116">Dodaj `TransportSettings` sekcji w pliku settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5ee12-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="5ee12-117">W takim przypadku `createServiceInstanceListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="5ee12-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="5ee12-118">Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml bez żadnych prefiksów `FabricTransportListenerSettings` załaduje wszystkie ustawienia w tej sekcji ma domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5ee12-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="5ee12-119">W takim przypadku `CreateServiceInstanceListeners` metoda będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="5ee12-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="5ee12-120">Gdy wywoływać metod w usług zabezpieczonych przy użyciu stosu usług zdalnych, zamiast `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasę, aby utworzyć serwer proxy usługi, użyj `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="5ee12-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="5ee12-121">Jeśli kod klienta działa w ramach usługi, można załadować `FabricTransportSettings` z pliku settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5ee12-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="5ee12-122">Utwórz sekcję TransportSettings, która jest podobna do kodu usługi, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5ee12-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="5ee12-123">Wprowadź następujące zmiany w kodzie klienta:</span><span class="sxs-lookup"><span data-stu-id="5ee12-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
