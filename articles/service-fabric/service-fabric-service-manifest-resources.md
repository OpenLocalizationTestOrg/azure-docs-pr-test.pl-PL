---
title: "punkty końcowe usługi sieć szkieletowa usług aaaSpecifying | Dokumentacja firmy Microsoft"
description: "Jak toodescribe zasobów punktu końcowego w usłudze manifestu, w tym jak tooset się punktów końcowych HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a>Określanie zasobów w manifeście usługi
## <a name="overview"></a>Omówienie
manifest usługi Hello umożliwia zasobów używanych toobe usługi hello zadeklarowany zmienić bez konieczności zmieniania kodu hello skompilowany. Sieć szkieletowa usług Azure obsługuje konfigurację punktu końcowego zasobów dla usługi hello. Witaj dostęp do toohello zasobów, które są określone w manifeście usługi hello można sterować za pośrednictwem hello SecurityGroup w manifeście aplikacji hello. Deklaracja Hello zasobów umożliwia toobe tych zasobów, zmieniony w czasie wdrażania, co oznacza, że usługa hello nie wymaga toointroduce mechanizm nowej konfiguracji. Witaj definicji schematu dla pliku ServiceManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Punkty końcowe
Zdefiniowane w manifeście usługi hello zasobu punktu końcowego sieci szkieletowej usług przypisuje porty z zakresu portów aplikacji hello zastrzeżone, jeśli port nie jest jawnie określony. Na przykład wyglądać w punkcie końcowym hello *ServiceEndpoint1* określony we fragmencie manifestu powitania po tym akapitu. Ponadto usługi także mogą żądać w zasobie określonego portu. Repliki usługi uruchomione w węzłach klastra różnych można przypisać różne numery portów, podczas repliki usługi uruchomionej na hello tego samego portu hello udziału węzła. Witaj repliki usługi można użyć tych portów zgodnie z potrzebami dla replikacji i nasłuchuje żądań klientów.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Odwołuje się zbyt[Konfigurowanie stanowych usług niezawodnej](service-fabric-reliable-services-configuration.md) tooread więcej informacji na temat odwołujące się do punktów końcowych z pliku ustawień pakietu konfiguracji hello (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Przykład: określenie punktu końcowego HTTP dla usługi
Witaj następujące usługi manifest określa jeden zasób punktu końcowego TCP i dwa zasoby punkt końcowy HTTP w hello &lt;zasobów&gt; elementu.

Punkty końcowe HTTP są automatycznie ACL czy przez sieć szkieletowa usług.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Przykład: Określanie punkt końcowy HTTPS dla usługi
Hello protokołu HTTPS zapewnia uwierzytelnianie na serwerze i jest używany także do szyfrowania komunikacji klient serwer. tooenable HTTPS w usłudze Service Fabric należy określić protokół hello w hello *zasoby -> punkty końcowe -> punktu końcowego* sekcji hello manifestu usługi, jak pokazano wcześniej dla punktu końcowego hello *ServiceEndpoint3* .

> [!NOTE]
> Nie można zmienić protokołu usługi podczas uaktualniania aplikacji. Jeśli zostanie on zmieniony podczas uaktualniania, jest istotne zmiany.
> 
> 

Oto przykład ApplicationManifest muszą tooset dla protokołu HTTPS. należy podać Hello odcisku palca certyfikatu. Witaj EndpointRef jest tooEndpointResource odwołania w ServiceManifest, dla której ustawiony hello protokołu HTTPS. Można dodać więcej niż jeden EndpointCertificate.  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Zastępowanie punktów końcowych w pliku ServiceManifest.xml

W hello ApplicationManifest Dodaj sekcję ResourceOverrides, co będzie równorzędny tooConfigOverrides sekcji. W tej sekcji można określić hello zastąpienie hello punktów końcowych w sekcji hello zasobów określone w hello manifestu usługi.

W kolejności toooverride punktu końcowego w ServiceManifest przy użyciu zmian ApplicationParameters hello ApplicationManifest jako następujące czynności:

W sekcji ServiceManifestImport hello dodania nowej sekcji "ResourceOverrides"

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

W powitalne parametry dodać poniżej:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Podczas wdrażania aplikacji hello teraz można przekazać te wartości jako ApplicationParameters na przykład:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Uwaga: Jeśli hello wartości umożliwiają hello ApplicationParameters jest pusty możemy wróć toohello domyślną wartość podana w hello ServiceManifest dla hello odpowiadającego EndPointName.

Na przykład:

Jeśli w hello ServiceManifest określonego

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Witaj Port1 i Protocol1 wartości parametrów aplikacji ma wartość null lub pusty. Hello port jest nadal decyzji ServiceFabric. A hello protokołu tcp.

Załóżmy, że określasz niepoprawną wartość. Podobnie jak Port podano wartość ciągu "Foo" zamiast int.  Nowe ServiceFabricApplication polecenia zakończy się niepowodzeniem z powodu błędu: hello zastąpienie parametr z atrybutem "ServiceEndpoint1" name "Port1" w sekcji "ResourceOverrides" jest nieprawidłowy. Określona wartość Hello jest "Foo" i wymagane jest "int".
