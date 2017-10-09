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
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="befa8-103">Określanie zasobów w manifeście usługi</span><span class="sxs-lookup"><span data-stu-id="befa8-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="befa8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="befa8-104">Overview</span></span>
<span data-ttu-id="befa8-105">manifest usługi Hello umożliwia zasobów używanych toobe usługi hello zadeklarowany zmienić bez konieczności zmieniania kodu hello skompilowany.</span><span class="sxs-lookup"><span data-stu-id="befa8-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="befa8-106">Sieć szkieletowa usług Azure obsługuje konfigurację punktu końcowego zasobów dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="befa8-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="befa8-107">Witaj dostęp do toohello zasobów, które są określone w manifeście usługi hello można sterować za pośrednictwem hello SecurityGroup w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="befa8-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="befa8-108">Deklaracja Hello zasobów umożliwia toobe tych zasobów, zmieniony w czasie wdrażania, co oznacza, że usługa hello nie wymaga toointroduce mechanizm nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="befa8-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="befa8-109">Witaj definicji schematu dla pliku ServiceManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="befa8-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="befa8-110">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="befa8-110">Endpoints</span></span>
<span data-ttu-id="befa8-111">Zdefiniowane w manifeście usługi hello zasobu punktu końcowego sieci szkieletowej usług przypisuje porty z zakresu portów aplikacji hello zastrzeżone, jeśli port nie jest jawnie określony.</span><span class="sxs-lookup"><span data-stu-id="befa8-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="befa8-112">Na przykład wyglądać w punkcie końcowym hello *ServiceEndpoint1* określony we fragmencie manifestu powitania po tym akapitu.</span><span class="sxs-lookup"><span data-stu-id="befa8-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="befa8-113">Ponadto usługi także mogą żądać w zasobie określonego portu.</span><span class="sxs-lookup"><span data-stu-id="befa8-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="befa8-114">Repliki usługi uruchomione w węzłach klastra różnych można przypisać różne numery portów, podczas repliki usługi uruchomionej na hello tego samego portu hello udziału węzła.</span><span class="sxs-lookup"><span data-stu-id="befa8-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="befa8-115">Witaj repliki usługi można użyć tych portów zgodnie z potrzebami dla replikacji i nasłuchuje żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="befa8-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="befa8-116">Odwołuje się zbyt[Konfigurowanie stanowych usług niezawodnej](service-fabric-reliable-services-configuration.md) tooread więcej informacji na temat odwołujące się do punktów końcowych z pliku ustawień pakietu konfiguracji hello (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="befa8-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="befa8-117">Przykład: określenie punktu końcowego HTTP dla usługi</span><span class="sxs-lookup"><span data-stu-id="befa8-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="befa8-118">Witaj następujące usługi manifest określa jeden zasób punktu końcowego TCP i dwa zasoby punkt końcowy HTTP w hello &lt;zasobów&gt; elementu.</span><span class="sxs-lookup"><span data-stu-id="befa8-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="befa8-119">Punkty końcowe HTTP są automatycznie ACL czy przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="befa8-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="befa8-120">Przykład: Określanie punkt końcowy HTTPS dla usługi</span><span class="sxs-lookup"><span data-stu-id="befa8-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="befa8-121">Hello protokołu HTTPS zapewnia uwierzytelnianie na serwerze i jest używany także do szyfrowania komunikacji klient serwer.</span><span class="sxs-lookup"><span data-stu-id="befa8-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="befa8-122">tooenable HTTPS w usłudze Service Fabric należy określić protokół hello w hello *zasoby -> punkty końcowe -> punktu końcowego* sekcji hello manifestu usługi, jak pokazano wcześniej dla punktu końcowego hello *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="befa8-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="befa8-123">Nie można zmienić protokołu usługi podczas uaktualniania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="befa8-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="befa8-124">Jeśli zostanie on zmieniony podczas uaktualniania, jest istotne zmiany.</span><span class="sxs-lookup"><span data-stu-id="befa8-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="befa8-125">Oto przykład ApplicationManifest muszą tooset dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="befa8-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="befa8-126">należy podać Hello odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="befa8-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="befa8-127">Witaj EndpointRef jest tooEndpointResource odwołania w ServiceManifest, dla której ustawiony hello protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="befa8-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="befa8-128">Można dodać więcej niż jeden EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="befa8-128">You can add more than one EndpointCertificate.</span></span>  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="befa8-129">Zastępowanie punktów końcowych w pliku ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="befa8-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="befa8-130">W hello ApplicationManifest Dodaj sekcję ResourceOverrides, co będzie równorzędny tooConfigOverrides sekcji.</span><span class="sxs-lookup"><span data-stu-id="befa8-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="befa8-131">W tej sekcji można określić hello zastąpienie hello punktów końcowych w sekcji hello zasobów określone w hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="befa8-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="befa8-132">W kolejności toooverride punktu końcowego w ServiceManifest przy użyciu zmian ApplicationParameters hello ApplicationManifest jako następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="befa8-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="befa8-133">W sekcji ServiceManifestImport hello dodania nowej sekcji "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="befa8-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="befa8-134">W powitalne parametry dodać poniżej:</span><span class="sxs-lookup"><span data-stu-id="befa8-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="befa8-135">Podczas wdrażania aplikacji hello teraz można przekazać te wartości jako ApplicationParameters na przykład:</span><span class="sxs-lookup"><span data-stu-id="befa8-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="befa8-136">Uwaga: Jeśli hello wartości umożliwiają hello ApplicationParameters jest pusty możemy wróć toohello domyślną wartość podana w hello ServiceManifest dla hello odpowiadającego EndPointName.</span><span class="sxs-lookup"><span data-stu-id="befa8-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="befa8-137">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="befa8-137">For example:</span></span>

<span data-ttu-id="befa8-138">Jeśli w hello ServiceManifest określonego</span><span class="sxs-lookup"><span data-stu-id="befa8-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="befa8-139">Witaj Port1 i Protocol1 wartości parametrów aplikacji ma wartość null lub pusty.</span><span class="sxs-lookup"><span data-stu-id="befa8-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="befa8-140">Hello port jest nadal decyzji ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="befa8-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="befa8-141">A hello protokołu tcp.</span><span class="sxs-lookup"><span data-stu-id="befa8-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="befa8-142">Załóżmy, że określasz niepoprawną wartość.</span><span class="sxs-lookup"><span data-stu-id="befa8-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="befa8-143">Podobnie jak Port podano wartość ciągu "Foo" zamiast int.  Nowe ServiceFabricApplication polecenia zakończy się niepowodzeniem z powodu błędu: hello zastąpienie parametr z atrybutem "ServiceEndpoint1" name "Port1" w sekcji "ResourceOverrides" jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="befa8-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="befa8-144">Określona wartość Hello jest "Foo" i wymagane jest "int".</span><span class="sxs-lookup"><span data-stu-id="befa8-144">hello value specified is 'Foo' and required is 'int'.</span></span>
