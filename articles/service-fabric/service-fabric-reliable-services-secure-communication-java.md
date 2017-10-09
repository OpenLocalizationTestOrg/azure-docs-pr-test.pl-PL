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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Pomoc w bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java w systemie Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi
Będziemy używać istniejącego [przykład](service-fabric-reliable-services-communication-remoting-java.md) objaśniający sposób tooset się komunikację zdalną dla niezawodne usługi. toohelp Zabezpieczanie usługi podczas korzystania z usługi komunikacji zdalnej, wykonaj następujące kroki:

1. Tworzenie interfejsu `HelloWorldStateless`, który definiuje metody hello, które będą dostępne dla zdalnego wywołania procedury w usłudze. Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakietu. Jest to `CommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.

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
2. Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.

    Upewnij się, które mają toohelp toouse bezpiecznej komunikacji usługi jest zainstalowany we wszystkich węzłach klastra hello hello certyfikatu hello. Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:

   1. Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-model.md):

       Dodaj `TransportSettings` sekcji w pliku settings.xml hello.

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

       W takim przypadku hello `createServiceInstanceListeners` metoda będzie wyglądać następująco:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml hello bez żadnych prefiksów `FabricTransportListenerSettings` załaduje wszystkie ustawienia hello w tej sekcji ma domyślnie.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        W takim przypadku hello `CreateServiceInstanceListeners` metoda będzie wyglądać następująco:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Podczas wywoływania metody zabezpieczonych usługi przy użyciu hello stosu usług zdalnych, zamiast hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate klasy serwera proxy usługi, użyj `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Jeśli kod klienta hello jest uruchomiony jako część usługi, można załadować `FabricTransportSettings` z pliku settings.xml hello. Sekcja TransportSettings, która jest podobny kod usługi toohello, należy utworzyć, jak pokazano wcześniej. Wprowadź hello następującego kodu klienta toohello zmiany:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
