---
title: "aaaManage wiele środowisk w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług aplikacji może działać w klastrach, w zakresie rozmiaru z jednego komputera toothousands maszyn. W niektórych przypadkach można tooconfigure aplikacji inaczej w przypadku tych środowisk zróżnicowane. W tym artykule opisano sposób toodefine parametry różnych aplikacji dla środowiska."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="5de0e-105">Parametry aplikacji dla wielu środowisk zarządzania</span><span class="sxs-lookup"><span data-stu-id="5de0e-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="5de0e-106">Można utworzyć klastry z sieci szkieletowej usług Azure przy użyciu dowolnego miejsca, z jedną toomany tysięcy komputerów.</span><span class="sxs-lookup"><span data-stu-id="5de0e-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="5de0e-107">Podczas plików binarnych aplikacji można uruchomić bez żadnych modyfikacji w tym szerokie spektrum środowisk, często mają aplikacji hello tooconfigure inaczej, w zależności od numer hello maszyny, które jest wdrażany do.</span><span class="sxs-lookup"><span data-stu-id="5de0e-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="5de0e-108">Jako przykład prostego, należy wziąć pod uwagę `InstanceCount` usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="5de0e-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="5de0e-109">Po uruchomieniu aplikacji na platformie Azure, zazwyczaj mają tooset wartości tego parametru toohello specjalne-"1".</span><span class="sxs-lookup"><span data-stu-id="5de0e-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="5de0e-110">Taka konfiguracja powoduje, że usługa działa na każdym węźle w klastrze hello (lub każdego węzła w hello typu węzła, jeśli ustawiono ograniczenia umieszczania).</span><span class="sxs-lookup"><span data-stu-id="5de0e-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="5de0e-111">Jednak ta konfiguracja nie jest odpowiedni dla pojedynczego komputera klastrów, ponieważ nie może mieć wiele procesów nasłuchiwania na powitania sam punkt końcowy na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5de0e-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="5de0e-112">Zamiast tego należy zwykle ustawić `InstanceCount` zbyt "1".</span><span class="sxs-lookup"><span data-stu-id="5de0e-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="5de0e-113">Określanie parametrów określonego środowiska</span><span class="sxs-lookup"><span data-stu-id="5de0e-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="5de0e-114">problem z konfiguracją toothis Hello rozwiązanie to zestaw usług domyślnych sparametryzowanych i pliki parametrów aplikacji, które wypełnić wartości tych parametrów dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5de0e-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="5de0e-115">Parametry aplikacji i usług domyślnych są konfigurowane w aplikacji hello i manifestów usługi.</span><span class="sxs-lookup"><span data-stu-id="5de0e-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="5de0e-116">Witaj definicji schematu dla plików ServiceManifest.xml i ApplicationManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="5de0e-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="5de0e-117">Domyślne usługi</span><span class="sxs-lookup"><span data-stu-id="5de0e-117">Default services</span></span>
<span data-ttu-id="5de0e-118">Aplikacje usługi sieć szkieletowa składają się z kolekcji wystąpień usługi.</span><span class="sxs-lookup"><span data-stu-id="5de0e-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="5de0e-119">Podczas umożliwiające toocreate pustą aplikację, a następnie dynamicznie utworzyć wszystkich wystąpień usługi, większość aplikacji ma zestaw podstawowe usługi, które należy zawsze utworzyć podczas tworzenia wystąpienia klasy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5de0e-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="5de0e-120">Są to określonego tooas "domyślne usługi".</span><span class="sxs-lookup"><span data-stu-id="5de0e-120">These are referred tooas "default services".</span></span> <span data-ttu-id="5de0e-121">Są one określone w manifeście aplikacji hello z symbole zastępcze-środowisko konfiguracji zawarte w nawiasach kwadratowych:</span><span class="sxs-lookup"><span data-stu-id="5de0e-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="5de0e-122">Każdy z hello nazwanych parametrów musi być zdefiniowana w elemencie parametry hello manifestu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="5de0e-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="5de0e-123">Atrybut DefaultValue Hello określa toobe wartość hello używane w braku hello parametru bardziej specyficzne dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5de0e-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="5de0e-124">Nie wszystkie parametry wystąpienia usługi są odpowiednie dla konfiguracji poszczególnych środowiska.</span><span class="sxs-lookup"><span data-stu-id="5de0e-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="5de0e-125">W powyższym przykładzie hello hello LowKey i HighKey dla schemat partycjonowania usługi hello są jawnie zdefiniowane wartości dla wszystkich wystąpień usługi hello ponieważ zakres partycji hello jest funkcją hello danych domeny, nie hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="5de0e-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="5de0e-126">Ustawienia konfiguracji usługi na środowisko</span><span class="sxs-lookup"><span data-stu-id="5de0e-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="5de0e-127">Witaj [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) umożliwia usług tooinclude konfiguracji pakiety, które zawierają niestandardowe pary klucz wartość, które są do odczytu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5de0e-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="5de0e-128">Witaj wartości tych ustawień można również zróżnicowane przez środowisko, określając `ConfigOverride` w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5de0e-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="5de0e-129">Załóżmy, że masz następujące ustawienia w pliku Config\Settings.xml hello hello hello `Stateful1` usługi:</span><span class="sxs-lookup"><span data-stu-id="5de0e-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="5de0e-130">Utwórz tę wartość dla pary określonych aplikacji środowiskową toooverride `ConfigOverride` podczas importowania manifestu usługi hello w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5de0e-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="5de0e-131">Ten parametr może zostać następnie skonfigurowane przez środowisko zgodnie z powyższym.</span><span class="sxs-lookup"><span data-stu-id="5de0e-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="5de0e-132">Można to zrobić, deklarowanie go w sekcji parametrów hello manifest aplikacji hello i określając wartości określonego środowiska w pliki parametrów aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5de0e-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="5de0e-133">W przypadku hello ustawienia konfiguracji usługi, istnieją trzy miejsca, w którym można ustawić wartości hello klucza: pakiet konfiguracji usługi hello manifest aplikacji hello i pliku parametrów aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5de0e-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="5de0e-134">Sieci szkieletowej usług będzie zawsze wybierz z pliku parametrów aplikacji hello najpierw (Jeśli określono), następnie hello manifest aplikacji, a na koniec hello pakiet konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5de0e-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="5de0e-135">Ustawianie i za pomocą zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="5de0e-135">Setting and using environment variables</span></span> 
<span data-ttu-id="5de0e-136">Można określić i ustaw zmienne środowiskowe w pliku ServiceManifest.xml hello i następnie zastąpić je w pliku ApplicationManifest.xml powitania dla poszczególnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="5de0e-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="5de0e-137">Witaj w poniższym przykładzie przedstawiono dwie zmienne środowiskowe, ustawić jedną z wartości i hello innych zostanie zastąpiona.</span><span class="sxs-lookup"><span data-stu-id="5de0e-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="5de0e-138">Można używać parametrów aplikacji, zmienne środowiskowe tooset wartości w hello sam sposób że powyższe użyto do konfiguracji zastąpień.</span><span class="sxs-lookup"><span data-stu-id="5de0e-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
<span data-ttu-id="5de0e-139">zmienne środowiskowe hello toooverride w pliku ApplicationManifest.xml, pakiet kodu hello odwołania w hello ServiceManifest z hello hello `EnvironmentOverrides` elementu.</span><span class="sxs-lookup"><span data-stu-id="5de0e-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="5de0e-140">Po utworzeniu hello nazwane wystąpienie usługi dostępne zmienne środowiskowe hello z kodu.</span><span class="sxs-lookup"><span data-stu-id="5de0e-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="5de0e-141">np. W języku C# można wykonać następujące hello</span><span class="sxs-lookup"><span data-stu-id="5de0e-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="5de0e-142">Zmienne środowiskowe sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="5de0e-142">Service Fabric environment variables</span></span>
<span data-ttu-id="5de0e-143">Sieć szkieletowa usług są wbudowane zmienne środowiskowe ustawione dla każdego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="5de0e-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="5de0e-144">Witaj pełną listę zmiennych środowiskowych jest poniżej, gdzie hello tych w są pogrubione hello używanych w usłudze hello innych są używane przez środowisko uruchomieniowe usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="5de0e-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="5de0e-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="5de0e-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="5de0e-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="5de0e-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="5de0e-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="5de0e-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="5de0e-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="5de0e-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="5de0e-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="5de0e-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="5de0e-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="5de0e-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="5de0e-151">**TypeEndpoint Fabric_Endpoint_ [YourServiceName]**</span><span class="sxs-lookup"><span data-stu-id="5de0e-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="5de0e-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="5de0e-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="5de0e-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="5de0e-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="5de0e-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="5de0e-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="5de0e-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="5de0e-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="5de0e-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="5de0e-156">Fabric_NodeId</span></span>
* <span data-ttu-id="5de0e-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="5de0e-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="5de0e-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="5de0e-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="5de0e-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="5de0e-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="5de0e-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="5de0e-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="5de0e-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="5de0e-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="5de0e-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="5de0e-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="5de0e-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="5de0e-163">FabricPackageFileName</span></span>

<span data-ttu-id="5de0e-164">Witaj belows kodu pokazuje, jak toolist hello zmiennych środowiskowych sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="5de0e-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="5de0e-165">Witaj poniżej przedstawiono przykłady zmiennych środowiskowych dla typu aplikacji o nazwie `GuestExe.Application` z typem usługi o nazwie `FrontEndService` uruchomienia na komputerze deweloperskim lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5de0e-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="5de0e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="5de0e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="5de0e-167">**Fabric_CodePackageName = kod**</span><span class="sxs-lookup"><span data-stu-id="5de0e-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="5de0e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="5de0e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="5de0e-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="5de0e-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="5de0e-170">**Fabric_NodeName = to węzeł _Node_2**</span><span class="sxs-lookup"><span data-stu-id="5de0e-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="5de0e-171">Pliki parametrów aplikacji</span><span class="sxs-lookup"><span data-stu-id="5de0e-171">Application parameter files</span></span>
<span data-ttu-id="5de0e-172">Projekt aplikacji Hello sieci szkieletowej usług mogą zawierać jeden lub więcej plików parametr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5de0e-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="5de0e-173">Każde z nich definiuje hello określonych wartości dla parametrów hello, które są zdefiniowane w manifeście aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="5de0e-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="5de0e-174">Domyślnie nowa aplikacja obejmuje trzy pliki parametrów aplikacji, o nazwie Local.1Node.xml, Local.5Node.xml i Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="5de0e-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Pliki parametrów aplikacji w Eksploratorze rozwiązań][app-parameters-solution-explorer]

<span data-ttu-id="5de0e-176">toocreate pliku parametrów po prostu skopiuj i Wklej istniejący i nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="5de0e-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="5de0e-177">Identyfikowanie określonego środowiska parametrów podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="5de0e-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="5de0e-178">W czasie wdrażania należy toochoose hello odpowiedni parametr pliku tooapply z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="5de0e-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="5de0e-179">Można to zrobić za pomocą okna dialogowego publikowanie hello w programie Visual Studio lub za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5de0e-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="5de0e-180">Wdrażanie w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5de0e-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="5de0e-181">Można wybierać spośród hello listę dostępnych parametrów plików podczas publikowania aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5de0e-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Wybierz plik parametrów w oknie dialogowym Publikowanie hello][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="5de0e-183">Wdrażanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5de0e-183">Deploy from PowerShell</span></span>
<span data-ttu-id="5de0e-184">Witaj `Deploy-FabricApplication.ps1` profil publikowania, jako parametr akceptuje zawarte w szablonie projektu aplikacji hello skrypt programu PowerShell i hello PublishProfile zawiera plik parametrów aplikacji toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="5de0e-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="5de0e-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5de0e-185">Next steps</span></span>
<span data-ttu-id="5de0e-186">toolearn więcej informacji na temat niektórych hello podstawowe koncepcje, które zostały omówione w tym temacie, zobacz hello [omówienie techniczne sieci szkieletowej usług](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5de0e-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="5de0e-187">Aby uzyskać informacje o inne funkcje zarządzania aplikacjami, które są dostępne w programie Visual Studio, zobacz [Zarządzaj aplikacjami sieci szkieletowej usług w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5de0e-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
