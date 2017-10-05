---
title: "Zarządzanie wiele środowisk w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "W klastrach, w zakresie rozmiaru maszyn z jednego komputera można uruchomić aplikacji sieci szkieletowej usług. W niektórych przypadkach należy skonfigurować aplikację inaczej w przypadku tych środowisk zróżnicowane. W tym artykule opisano sposób definiowania parametry różnych aplikacji dla środowiska."
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
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="aaace-105">Parametry aplikacji dla wielu środowisk zarządzania</span><span class="sxs-lookup"><span data-stu-id="aaace-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="aaace-106">Można utworzyć klastry z sieci szkieletowej usług Azure przy użyciu dowolnej lokalizacji z jednego do wielu tysięcy komputerów.</span><span class="sxs-lookup"><span data-stu-id="aaace-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="aaace-107">Podczas plików binarnych aplikacji można uruchomić bez żadnych modyfikacji w tym szerokie spektrum środowisk, często chcesz skonfigurować aplikację różnie w zależności od liczby maszyn, które wdrażasz do.</span><span class="sxs-lookup"><span data-stu-id="aaace-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="aaace-108">Jako przykład prostego, należy wziąć pod uwagę `InstanceCount` usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="aaace-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="aaace-109">Po uruchomieniu aplikacji na platformie Azure mają zwykle Ustaw ten parametr przyjmuje wartość specjalną-"1".</span><span class="sxs-lookup"><span data-stu-id="aaace-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="aaace-110">Taka konfiguracja powoduje, że usługa działa na każdym węźle w klastrze (lub każdego węzła w typu węzła, jeśli ustawiono ograniczenia umieszczania).</span><span class="sxs-lookup"><span data-stu-id="aaace-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="aaace-111">Jednak ta konfiguracja nie jest odpowiednia dla klastra pojedynczego komputera, ponieważ nie może mieć wiele procesów, które nasłuchują na tym samym punkcie końcowym na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="aaace-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="aaace-112">Zamiast tego należy zwykle ustawić `InstanceCount` "1".</span><span class="sxs-lookup"><span data-stu-id="aaace-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="aaace-113">Określanie parametrów określonego środowiska</span><span class="sxs-lookup"><span data-stu-id="aaace-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="aaace-114">Rozwiązanie tego problemu konfiguracji to zestaw usług domyślnych sparametryzowanych i pliki parametrów aplikacji, które wypełnić wartości tych parametrów dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="aaace-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="aaace-115">Parametry aplikacji i usług domyślnych są konfigurowane w manifestów aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="aaace-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="aaace-116">Definicja schematu dla plików ServiceManifest.xml i ApplicationManifest.xml jest instalowany z zestawu SDK sieci szkieletowej usług i narzędzi do *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="aaace-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="aaace-117">Domyślne usługi</span><span class="sxs-lookup"><span data-stu-id="aaace-117">Default services</span></span>
<span data-ttu-id="aaace-118">Aplikacje usługi sieć szkieletowa składają się z kolekcji wystąpień usługi.</span><span class="sxs-lookup"><span data-stu-id="aaace-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="aaace-119">Gdy to możliwe, należy utworzyć pustą aplikację, a następnie utwórz dynamicznie wszystkich wystąpień usługi, większość aplikacji ma zestaw podstawowe usługi, które należy zawsze utworzyć podczas tworzenia wystąpienia klasy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="aaace-120">Te są określane jako "domyślne usługi".</span><span class="sxs-lookup"><span data-stu-id="aaace-120">These are referred to as "default services".</span></span> <span data-ttu-id="aaace-121">Są one określone w manifeście aplikacji z symbole zastępcze-środowisko konfiguracji zawarte w nawiasach kwadratowych:</span><span class="sxs-lookup"><span data-stu-id="aaace-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="aaace-122">Każdy nazwane parametry muszą być zdefiniowane w elemencie parametry dla manifest aplikacji:</span><span class="sxs-lookup"><span data-stu-id="aaace-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="aaace-123">Atrybut DefaultValue określa wartość do użycia w przypadku braku parametru bardziej specyficzne dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="aaace-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="aaace-124">Nie wszystkie parametry wystąpienia usługi są odpowiednie dla konfiguracji poszczególnych środowiska.</span><span class="sxs-lookup"><span data-stu-id="aaace-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="aaace-125">W powyższym przykładzie LowKey i HighKey wartości schemat partycjonowania usługi są jawnie zdefiniowany dla wszystkich wystąpień usługi, ponieważ zakres partycji jest funkcją domeny danych, nie środowiska.</span><span class="sxs-lookup"><span data-stu-id="aaace-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="aaace-126">Ustawienia konfiguracji usługi na środowisko</span><span class="sxs-lookup"><span data-stu-id="aaace-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="aaace-127">[Model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) umożliwia usługom zawierać pakiety konfiguracji, które zawierają niestandardowe pary klucz wartość, które są do odczytu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="aaace-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="aaace-128">Wartości tych ustawień można również zróżnicowane przez środowisko, określając `ConfigOverride` w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="aaace-129">Załóżmy, że zostały następujące ustawienia w pliku Config\Settings.xml `Stateful1` usługi:</span><span class="sxs-lookup"><span data-stu-id="aaace-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="aaace-130">Aby zastąpić tę wartość dla określonej aplikacji środowiskową pary, Utwórz `ConfigOverride` podczas importowania manifestu usługi w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

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
<span data-ttu-id="aaace-131">Ten parametr może zostać następnie skonfigurowane przez środowisko zgodnie z powyższym.</span><span class="sxs-lookup"><span data-stu-id="aaace-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="aaace-132">Można to zrobić, deklarowanie go w sekcji parametrów w manifeście aplikacji i określając wartości określonego środowiska w pliki parametrów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="aaace-133">W przypadku ustawienia konfiguracji usługi, istnieją trzy miejsca, w którym można ustawić wartość klucza: pakiet konfiguracji usługi, manifest aplikacji i pliku parametrów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="aaace-134">Zawsze wybierze sieci szkieletowej usług z pliku parametrów aplikacji pierwszego (Jeśli określono), następnie manifest aplikacji, a na końcu pakiet konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="aaace-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="aaace-135">Ustawianie i za pomocą zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="aaace-135">Setting and using environment variables</span></span> 
<span data-ttu-id="aaace-136">Można określić i ustaw zmienne środowiskowe w pliku ServiceManifest.xml i następnie zastąpić je w pliku ApplicationManifest.xml dla poszczególnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="aaace-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="aaace-137">W poniższym przykładzie przedstawiono dwie zmienne środowiskowe, jeden zestaw wartości, a druga zostanie zastąpiona.</span><span class="sxs-lookup"><span data-stu-id="aaace-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="aaace-138">Można ustawić wartości zmiennych środowiskowych w taki sam sposób, jak te były używane dla zastąpień konfiguracji, mogą używać parametrów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="aaace-139">Aby zastąpić zmienne środowiskowe w pliku ApplicationManifest.xml, odwoływania się do pakietu kodu w ServiceManifest z `EnvironmentOverrides` elementu.</span><span class="sxs-lookup"><span data-stu-id="aaace-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="aaace-140">Po utworzeniu wystąpienia usługi o nazwie można uzyskać dostępu do zmiennych środowiskowych, z kodu.</span><span class="sxs-lookup"><span data-stu-id="aaace-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="aaace-141">np. W C# możesz wykonać następujące czynności</span><span class="sxs-lookup"><span data-stu-id="aaace-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="aaace-142">Zmienne środowiskowe sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="aaace-142">Service Fabric environment variables</span></span>
<span data-ttu-id="aaace-143">Sieć szkieletowa usług są wbudowane zmienne środowiskowe ustawione dla każdego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="aaace-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="aaace-144">Pełną listę zmiennych środowiskowych poniżej, gdzie pogrubioną czcionką w podane w są te, które będą używane w usłudze innych używane przez środowisko uruchomieniowe usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="aaace-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="aaace-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="aaace-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="aaace-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="aaace-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="aaace-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="aaace-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="aaace-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="aaace-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="aaace-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="aaace-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="aaace-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="aaace-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="aaace-151">**TypeEndpoint Fabric_Endpoint_ [YourServiceName]**</span><span class="sxs-lookup"><span data-stu-id="aaace-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="aaace-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="aaace-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="aaace-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="aaace-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="aaace-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="aaace-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="aaace-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="aaace-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="aaace-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="aaace-156">Fabric_NodeId</span></span>
* <span data-ttu-id="aaace-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="aaace-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="aaace-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="aaace-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="aaace-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="aaace-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="aaace-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="aaace-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="aaace-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="aaace-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="aaace-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="aaace-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="aaace-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="aaace-163">FabricPackageFileName</span></span>

<span data-ttu-id="aaace-164">Belows kod przedstawia sposób wyświetlania zmiennych środowiskowych sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="aaace-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="aaace-165">Poniżej podano przykłady zmiennych środowiskowych dla typu aplikacji o nazwie `GuestExe.Application` z typem usługi o nazwie `FrontEndService` uruchomienia na komputerze deweloperskim lokalnego.</span><span class="sxs-lookup"><span data-stu-id="aaace-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="aaace-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="aaace-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="aaace-167">**Fabric_CodePackageName = kod**</span><span class="sxs-lookup"><span data-stu-id="aaace-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="aaace-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="aaace-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="aaace-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="aaace-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="aaace-170">**Fabric_NodeName = to węzeł _Node_2**</span><span class="sxs-lookup"><span data-stu-id="aaace-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="aaace-171">Pliki parametrów aplikacji</span><span class="sxs-lookup"><span data-stu-id="aaace-171">Application parameter files</span></span>
<span data-ttu-id="aaace-172">Projekt aplikacji platformy Service Fabric może zawierać co najmniej jeden plik parametrów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="aaace-173">Każde z nich definiuje określone wartości parametrów, które są zdefiniowane w manifeście aplikacji:</span><span class="sxs-lookup"><span data-stu-id="aaace-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

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
<span data-ttu-id="aaace-174">Domyślnie nowa aplikacja obejmuje trzy pliki parametrów aplikacji, o nazwie Local.1Node.xml, Local.5Node.xml i Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="aaace-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Pliki parametrów aplikacji w Eksploratorze rozwiązań][app-parameters-solution-explorer]

<span data-ttu-id="aaace-176">Aby utworzyć plik parametrów, po prostu skopiuj i Wklej istniejący i nadaj mu nazwę nowej.</span><span class="sxs-lookup"><span data-stu-id="aaace-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="aaace-177">Identyfikowanie określonego środowiska parametrów podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="aaace-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="aaace-178">W czasie wdrażania musisz wybrać plik odpowiedni parametr, aby zastosować z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="aaace-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="aaace-179">Można to zrobić za pomocą okna dialogowego publikowanie w programie Visual Studio lub za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aaace-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="aaace-180">Wdrażanie w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aaace-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="aaace-181">Można wybrać z listy dostępnych parametrów plików podczas publikowania aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aaace-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Wybierz plik parametrów w oknie dialogowym publikowania][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="aaace-183">Wdrażanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaace-183">Deploy from PowerShell</span></span>
<span data-ttu-id="aaace-184">`Deploy-FabricApplication.ps1` Skrypt programu PowerShell zawarte w szablonie projektu aplikacji akceptuje profil publikowania, jako parametr i PublishProfile zawiera odwołanie do pliku parametrów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaace-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="aaace-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aaace-185">Next steps</span></span>
<span data-ttu-id="aaace-186">Aby dowiedzieć się więcej na temat niektórych podstawowych pojęciach, które zostały omówione w tym temacie, zobacz [omówienie techniczne sieci szkieletowej usług](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aaace-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="aaace-187">Aby uzyskać informacje o inne funkcje zarządzania aplikacjami, które są dostępne w programie Visual Studio, zobacz [Zarządzaj aplikacjami sieci szkieletowej usług w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="aaace-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
