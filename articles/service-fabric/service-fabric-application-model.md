---
title: "Model aplikacji sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Informacje o modelu i opisano aplikacji i usług w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="99a03-103">Model aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="99a03-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="99a03-104">Ten artykuł zawiera omówienie modelu aplikacji sieci szkieletowej usług Azure i sposobu definiowania aplikacji i usług za pośrednictwem plików manifestu.</span><span class="sxs-lookup"><span data-stu-id="99a03-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="99a03-105">Zrozumienie model aplikacji</span><span class="sxs-lookup"><span data-stu-id="99a03-105">Understand the application model</span></span>
<span data-ttu-id="99a03-106">Aplikacja jest kolekcja składników usług, które wykonywać niektórych funkcji lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="99a03-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="99a03-107">Usługa działa pełny i autonomiczne i można uruchomić i uruchomić niezależnie od innych usług.</span><span class="sxs-lookup"><span data-stu-id="99a03-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="99a03-108">Usługa składa się z kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="99a03-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="99a03-109">Dla każdej usługi kod składa się z pliku wykonywalnego plików binarnych, konfiguracja obejmuje ustawienia usługi, które mogą zostać załadowane w czasie wykonywania i danych składa się z dowolnego statycznych danych do użycia przez usługę.</span><span class="sxs-lookup"><span data-stu-id="99a03-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="99a03-110">Każdego składnika w tym modelu hierarchiczne aplikacji może być niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="99a03-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Model aplikacji sieci szkieletowej usług][appmodel-diagram]

<span data-ttu-id="99a03-112">Typ aplikacji kategoryzacji aplikacji i składa się z pakietem typu usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="99a03-113">Typ usługi jest kategoryzacji usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="99a03-114">Klasyfikacja może mieć różne ustawienia i konfiguracje, ale do podstawowych funkcji jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="99a03-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="99a03-115">Wystąpień usługi są zmian konfiguracji innej usługi typu usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="99a03-116">Klasy (lub "typów") aplikacji i usług opisanych za pomocą plików XML (manifestów aplikacji i manifestów usługi).</span><span class="sxs-lookup"><span data-stu-id="99a03-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="99a03-117">Manifesty są szablony, które można wdrożyć aplikacji z magazynu obrazu klastra.</span><span class="sxs-lookup"><span data-stu-id="99a03-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="99a03-118">Definicja schematu dla pliku ServiceManifest.xml i ApplicationManifest.xml jest instalowany z zestawu SDK sieci szkieletowej usług i narzędzi do *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="99a03-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="99a03-119">Kod dla różnych aplikacji wystąpień Uruchom jako osobne procesy nawet wtedy, gdy pracujących na tym samym węźle sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="99a03-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="99a03-120">Ponadto można zarządzać cyklem życia każdego wystąpienia aplikacji (na przykład uaktualnić) niezależnie.</span><span class="sxs-lookup"><span data-stu-id="99a03-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="99a03-121">Na poniższym diagramie przedstawiono, jak typy aplikacji składają się z typów usług, które z kolei składają się z kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="99a03-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="99a03-122">Aby uprościć na diagramie, pakietami tylko/config/danych kodu `ServiceType4` są wyświetlane, że każdy typ usługi to niektórych lub wszystkich tych typów pakietów.</span><span class="sxs-lookup"><span data-stu-id="99a03-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Typy aplikacji usługi Service Fabric i usługi][cluster-imagestore-apptypes]

<span data-ttu-id="99a03-124">Dwa różne pliki manifestu służą do opisywania aplikacji i usług: manifest usługi i manifest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="99a03-125">Manifesty są zostały szczegółowo opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="99a03-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="99a03-126">Może istnieć co najmniej jedno wystąpienie typu usługi active w klastrze.</span><span class="sxs-lookup"><span data-stu-id="99a03-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="99a03-127">Na przykład wystąpienie usługi stanowej lub replik, osiągnąć wysoką niezawodnością poprzez replikację stanu między replikami znajdujących się w różnych węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="99a03-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="99a03-128">Replikacja zasadniczo zapewnia nadmiarowość dla usługi, które mają być dostępne, nawet w przypadku awarii jednego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="99a03-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="99a03-129">A [podzielona na partycje usługi](service-fabric-concepts-partitioning.md) dalsze dzieli jego stan (i wzorce dostępu do tego stanu) w węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="99a03-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="99a03-130">Na poniższym diagramie przedstawiono związek między aplikacjami i wystąpień usług, partycji i replik.</span><span class="sxs-lookup"><span data-stu-id="99a03-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Partycji i replik w ramach usługi][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="99a03-132">Układ aplikacji można wyświetlić w klastrze za pomocą narzędzia Service Fabric Explorer dostępne w http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="99a03-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="99a03-133">Aby uzyskać więcej informacji, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="99a03-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="99a03-134">Opis usługi</span><span class="sxs-lookup"><span data-stu-id="99a03-134">Describe a service</span></span>
<span data-ttu-id="99a03-135">Manifest usługi deklaratywnie definiuje typ usługi i wersji.</span><span class="sxs-lookup"><span data-stu-id="99a03-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="99a03-136">Określa usługę metadane, takie jak typ usługi, właściwości kondycji metryki równoważenia obciążenia, pliki binarne usługi i pliki konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="99a03-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="99a03-137">Innymi słowy, opisuje pakiety kodu, konfiguracji i danych, które tworzą pakietu usług do obsługi co najmniej jeden typ usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="99a03-138">Poniżej przedstawiono prosty przykład manifest usługi:</span><span class="sxs-lookup"><span data-stu-id="99a03-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="99a03-139">**Wersja** atrybuty są ciągami bez struktury i nie zostały przeanalizowane przez system.</span><span class="sxs-lookup"><span data-stu-id="99a03-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="99a03-140">Wersja atrybuty są używane do wersji każdego składnika dla uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="99a03-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="99a03-141">**Serivcetype** deklaruje, jakie typy usługi są obsługiwane przez **CodePackages** w tym manifeście.</span><span class="sxs-lookup"><span data-stu-id="99a03-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="99a03-142">Usługa jest uruchomione na jednym z następujących typów usługi, wszystkie pakiety kodu zadeklarowany w tym manifeście zostaną aktywowane przez uruchomienie ich punktów wejścia.</span><span class="sxs-lookup"><span data-stu-id="99a03-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="99a03-143">Wynikowa procesów oczekuje się zarejestrować obsługiwanych typów usług w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="99a03-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="99a03-144">Typ usługi został zadeklarowany na poziomie manifestu i nie poziomu pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="99a03-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="99a03-145">Dlatego w przypadku wielu pakietów kodu ich wszystkich aktywacji zawsze, gdy system wyszukuje jeden z typów usług zadeklarowane.</span><span class="sxs-lookup"><span data-stu-id="99a03-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="99a03-146">**SetupEntryPoint** punkt wejścia uprzywilejowanych uruchamiane przy użyciu poświadczeń usługi sieć szkieletowa (zazwyczaj *LocalSystem* konta) przed innymi punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="99a03-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="99a03-147">Plik wykonywalny określony przez **punktu wejścia** jest zazwyczaj długotrwałe hosta usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="99a03-148">Obecność punktu wejścia instalacji oddzielnych pozwala uniknąć konieczności uruchamiania usługi hosta z wysokiego poziomu uprawnień przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="99a03-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="99a03-149">Plik wykonywalny określony przez **punktu wejścia** po zakończeniu **SetupEntryPoint** kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="99a03-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="99a03-150">Jeśli kiedykolwiek proces kończy lub ulegnie awarii, proces wynikowy jest monitorowane i ponownego uruchomienia (począwszy od ponownie **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="99a03-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="99a03-151">Typowe scenariusze korzystania **SetupEntryPoint** są podczas uruchomienia pliku wykonywalnego przed uruchomieniem usługi lub wykonać operację z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="99a03-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="99a03-152">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="99a03-152">For example:</span></span>

* <span data-ttu-id="99a03-153">Konfigurowanie i Inicjowanie zmiennych środowiskowych, które wymaga pliku wykonywalnego usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="99a03-154">To nie jest ograniczona do tylko pliki wykonywalne napisane przez modele programowania sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="99a03-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="99a03-155">Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.</span><span class="sxs-lookup"><span data-stu-id="99a03-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="99a03-156">Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="99a03-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="99a03-157">Aby uzyskać więcej informacji na temat konfigurowania **SetupEntryPoint** zobacz [skonfigurować zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="99a03-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="99a03-158">**EnvironmentVariables** zawiera listę zmiennych środowiskowych, które są ustawione dla tego pakietu kodu.</span><span class="sxs-lookup"><span data-stu-id="99a03-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="99a03-159">Zmienne Environmentment może zostać zastąpiona w `ApplicationManifest.xml` o podanie wartości różnych wystąpień innej usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="99a03-160">**DataPackage** deklaruje folder o nazwie **nazwa** atrybutu, zawierającego dowolne dane statyczne zużywanych przez proces w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="99a03-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="99a03-161">**Lokalizacji ConfigPackage** deklaruje folder o nazwie **nazwa** atrybut, który zawiera *Settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="99a03-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="99a03-162">Plik ustawień zawiera sekcje ustawień pary klucz wartość, zdefiniowanych przez użytkownika, które proces odczytuje Wstecz w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="99a03-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="99a03-163">Podczas uaktualniania, jeśli tylko **lokalizacji ConfigPackage** **wersji** została zmieniona, a następnie uruchomiony proces nie zostanie ponownie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="99a03-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="99a03-164">Zamiast tego wywołania zwrotnego powiadamia proces, który zmieniono ustawienia konfiguracji, mogą być ładowane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="99a03-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="99a03-165">Oto przykład *Settings.xml* pliku:</span><span class="sxs-lookup"><span data-stu-id="99a03-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="99a03-166">Manifest usługi może zawierać wiele kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="99a03-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="99a03-167">Każdy z tych może być kontrolą wersji niezależnie.</span><span class="sxs-lookup"><span data-stu-id="99a03-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="99a03-168">Opis aplikacji</span><span class="sxs-lookup"><span data-stu-id="99a03-168">Describe an application</span></span>
<span data-ttu-id="99a03-169">Manifest aplikacji zawiera opis deklaratywnie, typ i wersja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="99a03-170">Określa usługę kompozycji metadane, takie jak nazwy stabilny oraz schemat partycji, współczynnik liczby/replikacji wystąpienia, zasady zabezpieczeń i izolacji, ograniczenia umieszczania, operacje zastępowania konfiguracji, typów usług składowych.</span><span class="sxs-lookup"><span data-stu-id="99a03-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="99a03-171">Opisano również domen równoważenia obciążenia, w których znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="99a03-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="99a03-172">W związku z tym manifest aplikacji zawiera opis elementów na poziomie aplikacji i odwołuje się do co najmniej jeden manifestów usługi utworzenie typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="99a03-173">Poniżej przedstawiono prosty przykład manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="99a03-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="99a03-174">Manifesty usługi, takich jak **wersji** atrybuty są ciągami bez struktury i nie są analizowane przez system.</span><span class="sxs-lookup"><span data-stu-id="99a03-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="99a03-175">Atrybuty wersji są również używane do wersji każdego składnika dla uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="99a03-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="99a03-176">**ServiceManifestImport** zawiera odwołania do usługi manifestów, które tworzą ten typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="99a03-177">Manifesty importowanych usługi określają, jakie typy usługi są prawidłowe w ramach tego typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="99a03-178">W ramach ServiceManifestImport można zastąpić wartości konfiguracji w pliku Settings.xml i środowiska zmiennych w plikach pliku ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="99a03-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="99a03-179">**DefaultServices** deklaruje wystąpień usług, które są tworzone automatycznie, gdy aplikacja zostanie uruchomiony przed tego typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99a03-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="99a03-180">Domyślne usługi są po prostu udogodnienie i zachowywać się jak normalne usług w każdym względem po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="99a03-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="99a03-181">Uaktualnienia wraz z innych usług, w przypadku aplikacji, a można również usunąć.</span><span class="sxs-lookup"><span data-stu-id="99a03-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="99a03-182">Manifest aplikacji może zawierać wiele importów manifestu usługi i usług domyślnych.</span><span class="sxs-lookup"><span data-stu-id="99a03-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="99a03-183">Niezależnie może być wersjonowany każdego importu manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="99a03-184">Aby dowiedzieć się, jak należy dbać o różnych aplikacji i parametrów usługi dla poszczególnych środowisk, zobacz [Zarządzanie parametry aplikacji dla wielu środowiskach](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="99a03-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="99a03-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99a03-185">Next steps</span></span>
<span data-ttu-id="99a03-186">[Pakiet aplikacji](service-fabric-package-apps.md) i przygotowania do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="99a03-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="99a03-187">[Wdrażanie i usunąć aplikacje] [ 10] opisano, jak zarządzać wystąpień aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99a03-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="99a03-188">[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] opisano sposób konfigurowania parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="99a03-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="99a03-189">[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] opisuje sposób uruchamiania usługi na podstawie zasad zabezpieczeń w celu ograniczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="99a03-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="99a03-190">[Hosting modeli aplikacji] [ 13] opis relacji między repliki (lub wystąpień) wdrożonej usługi i procesu hosta usługi.</span><span class="sxs-lookup"><span data-stu-id="99a03-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
