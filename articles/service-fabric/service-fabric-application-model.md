---
title: "model aplikacji usługi sieć szkieletowa aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak toomodel i opisz aplikacji i usług w sieci szkieletowej usług."
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="794f0-103">Model aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="794f0-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="794f0-104">Ten artykuł zawiera omówienie modelu aplikacji hello sieć szkieletowa usług Azure oraz jak toodefine aplikacji i usług za pośrednictwem plików manifestu.</span><span class="sxs-lookup"><span data-stu-id="794f0-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="794f0-105">Zrozumienie modelu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="794f0-105">Understand hello application model</span></span>
<span data-ttu-id="794f0-106">Aplikacja jest kolekcja składników usług, które wykonywać niektórych funkcji lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="794f0-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="794f0-107">Usługa działa pełny i autonomiczne i można uruchomić i uruchomić niezależnie od innych usług.</span><span class="sxs-lookup"><span data-stu-id="794f0-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="794f0-108">Usługa składa się z kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="794f0-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="794f0-109">Dla każdej usługi kod składa się z plików binarnych wykonywalnego hello, konfiguracja obejmuje ustawienia usługi, które mogą zostać załadowane w czasie wykonywania i danych składa się z używane przez usługę hello toobe dowolne dane statyczne.</span><span class="sxs-lookup"><span data-stu-id="794f0-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="794f0-110">Każdego składnika w tym modelu hierarchiczne aplikacji może być niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="794f0-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![model aplikacji Hello sieci szkieletowej usług][appmodel-diagram]

<span data-ttu-id="794f0-112">Typ aplikacji kategoryzacji aplikacji i składa się z pakietem typu usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="794f0-113">Typ usługi jest kategoryzacji usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="794f0-114">kategoryzacji Hello może mieć różne ustawienia i konfiguracje, ale pozostaje funkcje podstawowe hello hello takie same.</span><span class="sxs-lookup"><span data-stu-id="794f0-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="794f0-115">Witaj wystąpień usługi są zmian konfiguracji usługi różnych hello z hello sam typ usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="794f0-116">Klasy (lub "typów") aplikacji i usług opisanych za pomocą plików XML (manifestów aplikacji i manifestów usługi).</span><span class="sxs-lookup"><span data-stu-id="794f0-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="794f0-117">manifesty Hello są hello szablony, które można wdrożyć aplikacji z magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="794f0-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="794f0-118">Witaj definicji schematu dla pliku ServiceManifest.xml i ApplicationManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="794f0-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="794f0-119">Hello kodu dla różnych aplikacji wystąpień Uruchom jako osobne procesy nawet wtedy, gdy jest to obsługiwane przez hello tego samego węzła sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="794f0-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="794f0-120">Ponadto hello cyklem życia każdego wystąpienia aplikacji mogą być zarządzane (na przykład uaktualnić) niezależnie.</span><span class="sxs-lookup"><span data-stu-id="794f0-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="794f0-121">Witaj poniższym diagramie przedstawiono sposób typy aplikacji składają się z typów usług, które z kolei składają się z kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="794f0-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="794f0-122">diagram hello toosimplify, tylko hello pakietów kodu/config/data dla `ServiceType4` są wyświetlane, że każdy typ usługi to niektórych lub wszystkich tych typów pakietów.</span><span class="sxs-lookup"><span data-stu-id="794f0-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Typy aplikacji usługi Service Fabric i usługi][cluster-imagestore-apptypes]

<span data-ttu-id="794f0-124">Dwa różne pliki manifestu są używane toodescribe aplikacji i usług: hello manifestu usługi i manifest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="794f0-125">Manifesty są tu szczegółowo hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="794f0-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="794f0-126">Może istnieć co najmniej jedno wystąpienie typu usługi active w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="794f0-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="794f0-127">Na przykład wystąpienie usługi stanowej lub replik, osiągnąć wysoką niezawodnością poprzez replikację stanu między replikami znajdujących się w różnych węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="794f0-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="794f0-128">Replikacji zasadniczo zapewnia nadmiarowość toobe usługi hello jest dostępne, nawet w przypadku awarii jednego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="794f0-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="794f0-129">A [podzielona na partycje usługi](service-fabric-concepts-partitioning.md) dalsze bez reszty jego stan (i stanu toothat wzorce dostępu) na węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="794f0-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="794f0-130">Witaj Poniższy diagram przedstawia hello relacji między aplikacjami i wystąpień usług, partycji i replik.</span><span class="sxs-lookup"><span data-stu-id="794f0-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Partycji i replik w ramach usługi][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="794f0-132">Układ aplikacji hello można wyświetlić w klastrze za pomocą narzędzia Service Fabric Explorer hello jest dostępne w http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="794f0-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="794f0-133">Aby uzyskać więcej informacji, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="794f0-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="794f0-134">Opis usługi</span><span class="sxs-lookup"><span data-stu-id="794f0-134">Describe a service</span></span>
<span data-ttu-id="794f0-135">manifest usługi Hello deklaratywnie definiuje hello usługi typu i wersji.</span><span class="sxs-lookup"><span data-stu-id="794f0-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="794f0-136">Określa usługę metadane, takie jak typ usługi, właściwości kondycji metryki równoważenia obciążenia, pliki binarne usługi i pliki konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="794f0-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="794f0-137">Innymi słowy, opisuje pakiety kodu, konfiguracji i danych hello tworzące toosupport pakietu usługi co najmniej jeden typ usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="794f0-138">Poniżej przedstawiono prosty przykład manifest usługi:</span><span class="sxs-lookup"><span data-stu-id="794f0-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="794f0-139">**Wersja** atrybuty są ciągami bez struktury i nie zostały przeanalizowane przez hello systemu.</span><span class="sxs-lookup"><span data-stu-id="794f0-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="794f0-140">Wersja atrybuty są używane tooversion każdy składnik do uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="794f0-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="794f0-141">**Serivcetype** deklaruje, jakie typy usługi są obsługiwane przez **CodePackages** w tym manifeście.</span><span class="sxs-lookup"><span data-stu-id="794f0-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="794f0-142">Usługa jest uruchomione na jednym z następujących typów usługi, wszystkie pakiety kodu zadeklarowany w tym manifeście zostaną aktywowane przez uruchomienie ich punktów wejścia.</span><span class="sxs-lookup"><span data-stu-id="794f0-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="794f0-143">procesy wynikowy Hello są oczekiwanego tooregister hello obsługiwane usługi typów w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="794f0-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="794f0-144">Typy usług są deklarowane jako hello manifestu poziomie i nie hello kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="794f0-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="794f0-145">Dlatego w przypadku wielu pakietów kodu ich wszystkich aktywacji zawsze, gdy hello system wyszukuje dowolny hello zadeklarowany typów usług.</span><span class="sxs-lookup"><span data-stu-id="794f0-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="794f0-146">**Element SetupEntryPoint** punkt wejścia uprzywilejowanych uruchamiane przy użyciu hello same poświadczenia jako sieci szkieletowej usług (zwykle hello *LocalSystem* konta) przed innymi punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="794f0-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="794f0-147">plik wykonywalny Hello określony przez **punktu wejścia** jest zazwyczaj hello długotrwałe usługi hosta.</span><span class="sxs-lookup"><span data-stu-id="794f0-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="794f0-148">obecności Hello osobnych ustawieniach punktu wejścia pozwala uniknąć konieczności hosta usługi hello toorun z wysokiego poziomu uprawnień przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="794f0-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="794f0-149">plik wykonywalny Hello określony przez **punktu wejścia** po zakończeniu **SetupEntryPoint** kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="794f0-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="794f0-150">Jeśli kiedykolwiek hello proces kończy lub ulegnie awarii, monitorowania i ponowne uruchomienie procesu wynikowy hello (począwszy od ponownie **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="794f0-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="794f0-151">Typowe scenariusze korzystania **SetupEntryPoint** są podczas uruchomienia pliku wykonywalnego przed uruchomieniem usługi hello lub wykonać operację z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="794f0-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="794f0-152">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="794f0-152">For example:</span></span>

* <span data-ttu-id="794f0-153">Konfigurowanie i Inicjowanie zmiennych środowiskowych, które hello potrzeb pliku wykonywalnego usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="794f0-154">To nie jest ograniczona tooonly pliki wykonywalne napisane przez modele programowania hello sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="794f0-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="794f0-155">Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.</span><span class="sxs-lookup"><span data-stu-id="794f0-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="794f0-156">Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="794f0-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="794f0-157">Aby uzyskać więcej informacji na temat tooconfigure hello **SetupEntryPoint** zobacz [hello zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="794f0-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="794f0-158">**EnvironmentVariables** zawiera listę zmiennych środowiskowych, które są ustawione dla tego pakietu kodu.</span><span class="sxs-lookup"><span data-stu-id="794f0-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="794f0-159">Zmienne Environmentment może zostać zastąpiona w hello `ApplicationManifest.xml` tooprovide różne wartości dla wystąpień innej usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="794f0-160">**DataPackage** deklaruje folder o nazwie hello **nazwa** atrybutu, zawierającego toobe dowolne dane statyczne, używane przez proces hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="794f0-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="794f0-161">**Lokalizacji ConfigPackage** deklaruje folder o nazwie hello **nazwa** atrybut, który zawiera *Settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="794f0-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="794f0-162">Plik ustawień Hello zawiera sekcje ustawień pary klucz wartość, zdefiniowanych przez użytkownika, które odczytuje procesu hello Wstecz w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="794f0-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="794f0-163">Podczas uaktualniania, jeśli tylko hello **lokalizacji ConfigPackage** **wersji** została zmieniona, a następnie hello uruchomiony proces nie zostanie ponownie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="794f0-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="794f0-164">Zamiast tego wywołania zwrotnego powiadamia hello procesu, który zmieniono ustawienia konfiguracji, mogą być ładowane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="794f0-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="794f0-165">Oto przykład *Settings.xml* pliku:</span><span class="sxs-lookup"><span data-stu-id="794f0-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="794f0-166">Manifest usługi może zawierać wiele kodu, konfiguracji i danych.</span><span class="sxs-lookup"><span data-stu-id="794f0-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="794f0-167">Każdy z tych może być kontrolą wersji niezależnie.</span><span class="sxs-lookup"><span data-stu-id="794f0-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="794f0-168">Opis aplikacji</span><span class="sxs-lookup"><span data-stu-id="794f0-168">Describe an application</span></span>
<span data-ttu-id="794f0-169">manifest aplikacji Hello deklaratywnie opisuje hello typ i wersja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="794f0-170">Określa usługę kompozycji metadane, takie jak nazwy stabilny oraz schemat partycji, współczynnik liczby/replikacji wystąpienia, zasady zabezpieczeń i izolacji, ograniczenia umieszczania, operacje zastępowania konfiguracji, typów usług składowych.</span><span class="sxs-lookup"><span data-stu-id="794f0-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="794f0-171">opisano również Hello domen równoważenia obciążenia w których znajduje się aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="794f0-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="794f0-172">W związku z tym manifest aplikacji zawiera opis elementów na poziomie aplikacji hello i odwołuje się do jednego lub więcej usługi manifesty toocompose typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="794f0-173">Poniżej przedstawiono prosty przykład manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="794f0-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="794f0-174">Manifesty usługi, takich jak **wersji** atrybuty są ciągami bez struktury i nie są analizowane przez hello systemu.</span><span class="sxs-lookup"><span data-stu-id="794f0-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="794f0-175">Atrybuty wersji są również używane tooversion każdy składnik do uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="794f0-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="794f0-176">**ServiceManifestImport** zawiera odwołania do tooservice manifestów, które tworzą ten typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="794f0-177">Manifesty importowanych usługi określają, jakie typy usługi są prawidłowe w ramach tego typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="794f0-178">W ramach hello ServiceManifestImport można zastąpić wartości konfiguracji w pliku Settings.xml i środowiska zmiennych w plikach pliku ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="794f0-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="794f0-179">**DefaultServices** deklaruje wystąpień usług, które są tworzone automatycznie, gdy aplikacja zostanie uruchomiony przed tego typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794f0-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="794f0-180">Domyślne usługi są po prostu udogodnienie i zachowywać się jak normalne usług w każdym względem po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="794f0-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="794f0-181">One są uaktualniane wraz z innymi usługami w wystąpienia aplikacji hello i można również usunąć.</span><span class="sxs-lookup"><span data-stu-id="794f0-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="794f0-182">Manifest aplikacji może zawierać wiele importów manifestu usługi i usług domyślnych.</span><span class="sxs-lookup"><span data-stu-id="794f0-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="794f0-183">Niezależnie może być wersjonowany każdego importu manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="794f0-184">jak wyświetlić toomaintain różnych aplikacji i parametrów usługi dla poszczególnych środowisk toolearn [Zarządzanie parametry aplikacji dla wielu środowiskach](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="794f0-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="794f0-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="794f0-185">Next steps</span></span>
<span data-ttu-id="794f0-186">[Pakiet aplikacji](service-fabric-package-apps.md) i zapewnić ich toodeploy gotowe.</span><span class="sxs-lookup"><span data-stu-id="794f0-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="794f0-187">[Wdrażanie i usunąć aplikacje] [ 10] w tym artykule opisano sposób toouse PowerShell toomanage aplikacji wystąpień.</span><span class="sxs-lookup"><span data-stu-id="794f0-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="794f0-188">[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] w tym artykule opisano sposób tooconfigure parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="794f0-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="794f0-189">[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] w tym artykule opisano, jak toorun usług pod dostępu toorestrict zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="794f0-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="794f0-190">[Hosting modeli aplikacji] [ 13] opis relacji między repliki (lub wystąpień) wdrożonej usługi i procesu hosta usługi.</span><span class="sxs-lookup"><span data-stu-id="794f0-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
