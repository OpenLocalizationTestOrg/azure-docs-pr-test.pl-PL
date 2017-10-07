---
title: "aaaDeploy istniejącego pliku wykonywalnego tooAzure sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Przewodnik dotyczący jak toopackage istniejącej aplikacji jako pliku wykonywalnego gościa, dlatego można ją wdrożyć tooa klastra sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="418e4-103">Wdrażanie gościa tooService wykonywalnego sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="418e4-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="418e4-104">Możesz uruchomić dowolnego typu kodu, np. Node.js, Java lub C++ w sieci szkieletowej usług Azure, jako usługa.</span><span class="sxs-lookup"><span data-stu-id="418e4-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="418e4-105">Sieć szkieletowa usług odnosi się toothese typów usług jako pliki wykonywalne gościa.</span><span class="sxs-lookup"><span data-stu-id="418e4-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="418e4-106">Pliki wykonywalne gościa są traktowane przez sieć szkieletowa usług takich jak usług bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="418e4-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="418e4-107">W związku z tym są umieszczane w węzłach w klastrze, w oparciu o dostępności i inne metryki.</span><span class="sxs-lookup"><span data-stu-id="418e4-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="418e4-108">W tym artykule opisano sposób toopackage i wdrażanie klastra usługi sieć szkieletowa tooa pliku wykonywalnego gościa za pomocą programu Visual Studio lub narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="418e4-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="418e4-109">W tym artykule firma Microsoft obejmuje hello kroki toopackage pliku wykonywalnego gościa i wdrożyć ją tooService sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="418e4-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="418e4-110">Zalety uruchamiania Gość pliku wykonywalnego w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="418e4-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="418e4-111">Istnieje kilka toorunning zalety Gość pliku wykonywalnego w klastrze usługi sieć szkieletowa usług:</span><span class="sxs-lookup"><span data-stu-id="418e4-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="418e4-112">Wysoka dostępność.</span><span class="sxs-lookup"><span data-stu-id="418e4-112">High availability.</span></span> <span data-ttu-id="418e4-113">Aplikacje uruchamiane w sieci szkieletowej usług są zyskuje dużą dostępność.</span><span class="sxs-lookup"><span data-stu-id="418e4-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="418e4-114">Sieć szkieletowa usług zapewnia uruchomionych wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="418e4-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="418e4-115">Monitorowanie kondycji.</span><span class="sxs-lookup"><span data-stu-id="418e4-115">Health monitoring.</span></span> <span data-ttu-id="418e4-116">Monitorowanie kondycji sieci szkieletowej usług wykrywa, czy aplikacja działa i udostępnia informacje diagnostyczne, w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="418e4-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="418e4-117">Zarządzanie cyklem życia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="418e4-117">Application lifecycle management.</span></span> <span data-ttu-id="418e4-118">Oprócz zapewnienia uaktualnienia bez przestojów, usługi Service Fabric zawiera automatycznego wycofania toohello poprzedniej wersji, jeśli istnieje zdarzenie kondycji zły zgłoszone podczas uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="418e4-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="418e4-119">Gęstości.</span><span class="sxs-lookup"><span data-stu-id="418e4-119">Density.</span></span> <span data-ttu-id="418e4-120">Wiele aplikacji można uruchomić w klastrze, która eliminuje potrzebę hello toorun każdej aplikacji na własnych sprzętu.</span><span class="sxs-lookup"><span data-stu-id="418e4-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="418e4-121">Odnajdowanie: Za pomocą usługi REST można wywołać toofind Usługa nazewnictwa sieci szkieletowej usług hello innych usług w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="418e4-122">Przykłady</span><span class="sxs-lookup"><span data-stu-id="418e4-122">Samples</span></span>
* [<span data-ttu-id="418e4-123">Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa</span><span class="sxs-lookup"><span data-stu-id="418e4-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="418e4-124">Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="418e4-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="418e4-125">Omówienie aplikacji i pliki manifestu usługi</span><span class="sxs-lookup"><span data-stu-id="418e4-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="418e4-126">W ramach wdrażania pliku wykonywalnego gościa, jest przydatne toounderstand hello sieci szkieletowej usług pakowania i wdrażania modelu zgodnie z opisem w [model aplikacji](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="418e4-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="418e4-127">Hello sieci szkieletowej usług pakowania modelu opiera się na dwa pliki XML: hello manifestów aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="418e4-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="418e4-128">Witaj definicji schematu dla hello pliki ApplicationManifest.xml i ServiceManifest.xml jest instalowany z hello zestawu SDK sieci szkieletowej usług do *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="418e4-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="418e4-129">**Manifest aplikacji** manifest aplikacji hello jest używany toodescribe aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="418e4-130">Przedstawia on hello usług, które go tworzą i innych parametrów, które są używane toodefine jak co najmniej jednej usługi powinny zostać wdrożone, takich jak hello liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="418e4-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="418e4-131">W sieci szkieletowej usług aplikacji jest jednostką wdrożenia i uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="418e4-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="418e4-132">Aplikację można aktualizować jako pojedyncza jednostka, w której zarządzane potencjalnych awarii i wycofywanie potencjalne zmian.</span><span class="sxs-lookup"><span data-stu-id="418e4-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="418e4-133">Sieć szkieletowa usług gwarantuje, że proces uaktualniania hello jest pomyślnie, lub jeśli hello uaktualnienie nie powiedzie się, nie pozostawi aplikacji hello w stan nieznany lub niestabilny.</span><span class="sxs-lookup"><span data-stu-id="418e4-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="418e4-134">**Manifest usługi** manifestu usługi hello w tym artykule opisano składniki hello usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="418e4-135">Zawiera dane, takie jak nazwa hello i typ usługi, a jego kod i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="418e4-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="418e4-136">Witaj manifestu usługi zawiera również pewne dodatkowe parametry, które mogą być używane tooconfigure hello usługi po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="418e4-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="418e4-137">Struktura pliku pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="418e4-137">Application package file structure</span></span>
<span data-ttu-id="418e4-138">toodeploy tooService aplikacji sieci szkieletowej aplikacji hello należy stosować struktury katalogów wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="418e4-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="418e4-139">Witaj poniżej znajduje się przykład tej struktury.</span><span class="sxs-lookup"><span data-stu-id="418e4-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="418e4-140">Witaj ApplicationPackageRoot zawiera pliku ApplicationManifest.xml hello, który definiuje aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="418e4-141">Podkatalog dla poszczególnych usług zawartych w aplikacji hello jest używany toocontain hello wszystkie artefakty, które usługa hello wymaga.</span><span class="sxs-lookup"><span data-stu-id="418e4-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="418e4-142">Te podkatalogi są hello ServiceManifest.xml i zazwyczaj hello następujące:</span><span class="sxs-lookup"><span data-stu-id="418e4-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="418e4-143">*Kod*.</span><span class="sxs-lookup"><span data-stu-id="418e4-143">*Code*.</span></span> <span data-ttu-id="418e4-144">Ten katalog zawiera hello kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="418e4-145">*Config*. Ten katalog zawiera pliku Settings.xml (i innych plików, jeśli to konieczne) czy hello usługa może uzyskać dostęp w środowiska uruchomieniowego tooretrieve określonych ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="418e4-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="418e4-146">*Dane*.</span><span class="sxs-lookup"><span data-stu-id="418e4-146">*Data*.</span></span> <span data-ttu-id="418e4-147">To dodatkowe toostore dodatkowe lokalne dane katalogu hello usługi może być konieczne.</span><span class="sxs-lookup"><span data-stu-id="418e4-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="418e4-148">Dane powinny być używane toostore tylko tymczasowych danych.</span><span class="sxs-lookup"><span data-stu-id="418e4-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="418e4-149">Sieć szkieletowa usług pojawia się kopiuje lub replicate katalog danych toohello zmiany Usługa hello musi toobe przeniesiony (na przykład w trybie failover).</span><span class="sxs-lookup"><span data-stu-id="418e4-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="418e4-150">Nie masz toocreate hello `config` i `data` katalogów, jeśli nie są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="418e4-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="418e4-151">Pakiet istniejącego pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="418e4-151">Package an existing executable</span></span>
<span data-ttu-id="418e4-152">Podczas pakowania pliku wykonywalnego gościa, można wybrać obu toouse szablon projektu Visual Studio lub zbyt[ręcznie utworzyć pakiet aplikacji hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="418e4-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="418e4-153">Za pomocą programu Visual Studio, hello struktury pakietu aplikacji i pliki manifestu zostają utworzone przez hello nowego szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="418e4-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="418e4-154">Witaj Najprostszym sposobem toopackage Windows istniejącego pliku wykonywalnego do usługi jest toouse programu Visual Studio i w systemie Linux toouse narzędzia Yeoman</span><span class="sxs-lookup"><span data-stu-id="418e4-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="418e4-155">Korzystając z programu Visual Studio toopackage oraz wdrożyć istniejącego pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="418e4-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="418e4-156">Program Visual Studio udostępnia usługi sieć szkieletowa toohelp szablonu usługi, w przypadku wdrażania klastra usługi sieć szkieletowa tooa pliku wykonywalnego gościa.</span><span class="sxs-lookup"><span data-stu-id="418e4-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="418e4-157">Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="418e4-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="418e4-158">Wybierz **pliku wykonywalnego gościa** jako hello szablonu usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="418e4-159">Kliknij przycisk **Przeglądaj** tooselect hello folder, plik wykonywalny i wypełnij rest hello hello parametry toocreate hello usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="418e4-160">*Zachowanie pakietu kodu*.</span><span class="sxs-lookup"><span data-stu-id="418e4-160">*Code Package Behavior*.</span></span> <span data-ttu-id="418e4-161">Może być toocopy zestaw wszystkich zawartość hello toohello Twojego folderu projektu programu Visual Studio, co jest przydatne, jeśli hello pliku wykonywalnego nie ulega zmianie.</span><span class="sxs-lookup"><span data-stu-id="418e4-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="418e4-162">Jeśli oczekiwać hello toochange pliku wykonywalnego i chcesz dynamicznie hello możliwości toopick się nowych kompilacji, zamiast tego można wybrać toolink toohello folder.</span><span class="sxs-lookup"><span data-stu-id="418e4-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="418e4-163">Podczas tworzenia projektu aplikacji hello w programie Visual Studio, można użyć połączonego folderów.</span><span class="sxs-lookup"><span data-stu-id="418e4-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="418e4-164">W ten sposób toohello lokalizacji źródła z projektu hello, umożliwiając możesz tooupdate hello gościa pliku wykonywalnego w jego miejsce docelowe źródło.</span><span class="sxs-lookup"><span data-stu-id="418e4-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="418e4-165">Aktualizacje mogące spowodować staną się częścią pakietu aplikacji hello podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="418e4-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="418e4-166">*Program* Określa plik wykonywalny hello, która powinna być uruchomiona usługa hello toostart.</span><span class="sxs-lookup"><span data-stu-id="418e4-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="418e4-167">*Argumenty* Określa argumenty hello, które powinny być przekazywane wykonywalnego toohello.</span><span class="sxs-lookup"><span data-stu-id="418e4-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="418e4-168">Może być lista parametrów z argumentami.</span><span class="sxs-lookup"><span data-stu-id="418e4-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="418e4-169">*WorkingFolder* Określa katalog roboczy hello hello procesu, który będzie toobe uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="418e4-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="418e4-170">Można określić trzy wartości:</span><span class="sxs-lookup"><span data-stu-id="418e4-170">You can specify three values:</span></span>
     * <span data-ttu-id="418e4-171">`CodeBase`Określa, że katalog roboczy hello będzie toobe Ustaw katalog kodów toohello w pakiecie aplikacji hello (`Code` katalogu pokazano hello poprzedzających struktury plików).</span><span class="sxs-lookup"><span data-stu-id="418e4-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="418e4-172">`CodePackage`Określa, że katalog roboczy hello przechodzi toobe ustawić głównego toohello pakietu aplikacji hello (`GuestService1Pkg` pokazano hello poprzedzających struktury plików).</span><span class="sxs-lookup"><span data-stu-id="418e4-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="418e4-173">`Work`Określa, że pliki hello są umieszczane w podkatalogu o nazwie pracy.</span><span class="sxs-lookup"><span data-stu-id="418e4-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="418e4-174">Nadaj nazwę usłudze i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="418e4-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="418e4-175">Jeśli usługa wymaga punktu końcowego do komunikacji, można teraz dodawać hello protokół, port i plik ServiceManifest.xml toohello typu.</span><span class="sxs-lookup"><span data-stu-id="418e4-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="418e4-176">Na przykład: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="418e4-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="418e4-177">Można teraz używać pakietu hello i opublikować akcji względem klastra lokalnego przez debugowanie rozwiązania hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="418e4-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="418e4-178">Po wykonaniu tych czynności można publikować klastra zdalnego tooa aplikacji hello lub zaewidencjonować hello rozwiązania toosource formantu.</span><span class="sxs-lookup"><span data-stu-id="418e4-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="418e4-179">Jak przejść toohello na końcu tego artykułu toosee tooview Twojego usługa wykonywalna gościa w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="418e4-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="418e4-180">Użyj Yoeman toopackage i wdrażanie istniejącego pliku wykonywalnego w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="418e4-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="418e4-181">Witaj procedura tworzenia i wdrażania Gość pliku wykonywalnego w systemie Linux jest hello taki sam jak wdrażanie aplikacji csharp lub java.</span><span class="sxs-lookup"><span data-stu-id="418e4-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="418e4-182">Na terminalu wpisz `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="418e4-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="418e4-183">Nadaj nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="418e4-183">Name your application.</span></span>
3. <span data-ttu-id="418e4-184">Nazwę usługi i podaj szczegóły hello, w tym ścieżki hello pliku wykonywalnego i parametrów hello, które muszą być wywoływane z.</span><span class="sxs-lookup"><span data-stu-id="418e4-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="418e4-185">Narzędzia yeoman tworzy pakiet aplikacji z odpowiedniej aplikacji hello i pliki manifestu wraz z instalowania i odinstalowywania skryptów.</span><span class="sxs-lookup"><span data-stu-id="418e4-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="418e4-186">Ręcznie pakietów i wdrożyć istniejącego pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="418e4-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="418e4-187">proces Hello ręcznie pakowania pliku wykonywalnego gościa jest oparta na powitania następujące ogólne kroki:</span><span class="sxs-lookup"><span data-stu-id="418e4-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="418e4-188">Utwórz strukturę katalogów hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="418e4-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="418e4-189">Dodawanie aplikacji hello kodu i plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="418e4-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="418e4-190">Edytuj hello pliku manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="418e4-191">Edytuj plik manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="418e4-192">Utwórz strukturę katalogów hello pakietu</span><span class="sxs-lookup"><span data-stu-id="418e4-192">Create hello package directory structure</span></span>
<span data-ttu-id="418e4-193">Możesz uruchomić tworzenie hello struktury katalogów, zgodnie z opisem w powyższej sekcji hello "Struktura pliku pakietu aplikacji".</span><span class="sxs-lookup"><span data-stu-id="418e4-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="418e4-194">Dodawanie plików kodu i konfiguracji aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="418e4-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="418e4-195">Po utworzeniu hello struktury katalogów, możesz dodać pliki kodu i konfiguracji aplikacji hello w obszarze hello katalogów kodu i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="418e4-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="418e4-196">Można również utworzyć dodatkowe katalogi lub podkatalogi w obszarze hello kodu lub config katalogów.</span><span class="sxs-lookup"><span data-stu-id="418e4-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="418e4-197">Sieć szkieletowa usług jest `xcopy` hello zawartości hello katalogu, więc nie ma żadnych toouse struktury wstępnie zdefiniowanych innych niż tworzenie dwa katalogi top, kodu i ustawienia.</span><span class="sxs-lookup"><span data-stu-id="418e4-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="418e4-198">(Można wybrać różne nazwy elementu, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="418e4-198">(You can pick different names if you want.</span></span> <span data-ttu-id="418e4-199">Bardziej szczegółowe informacje znajdują się w następnej sekcji hello.)</span><span class="sxs-lookup"><span data-stu-id="418e4-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="418e4-200">Upewnij się, czy zawiera wszystkie pliki hello i zależności, które hello potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="418e4-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="418e4-201">Sieć szkieletowa usług kopiuje hello zawartości pakietu aplikacji hello we wszystkich węzłach w klastrze hello, gdzie usługi aplikacji hello są wdrożone toobe będzie.</span><span class="sxs-lookup"><span data-stu-id="418e4-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="418e4-202">Witaj pakiet powinien zawierać wszystkie kodu hello, że aplikacja hello musi toorun.</span><span class="sxs-lookup"><span data-stu-id="418e4-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="418e4-203">Zakłada się, że zależności hello są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="418e4-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="418e4-204">Zmodyfikuj plik manifestu usługi hello</span><span class="sxs-lookup"><span data-stu-id="418e4-204">Edit hello service manifest file</span></span>
<span data-ttu-id="418e4-205">Witaj następnym krokiem jest tooedit hello usługi pliku manifestu tooinclude hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="418e4-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="418e4-206">Nazwa Hello hello typu usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-206">hello name of hello service type.</span></span> <span data-ttu-id="418e4-207">To jest identyfikator używany tooidentify usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="418e4-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="418e4-208">Witaj polecenia toouse toolaunch hello aplikacji (w elemencie ExeHost).</span><span class="sxs-lookup"><span data-stu-id="418e4-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="418e4-209">Dowolny skrypt, który wymaga toobe Uruchom tooset zapasowej aplikacji hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="418e4-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="418e4-210">Witaj poniżej przedstawiono przykład `ServiceManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="418e4-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="418e4-211">Witaj następujące sekcje zapoznać się z różnych części pliku hello konieczność tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="418e4-212">Serivcetype aktualizacji</span><span class="sxs-lookup"><span data-stu-id="418e4-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="418e4-213">Można wybrać dowolną nazwę, która ma `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="418e4-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="418e4-214">wartość Hello jest używany w hello `ApplicationManifest.xml` tooidentify hello usługa plików.</span><span class="sxs-lookup"><span data-stu-id="418e4-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="418e4-215">Określ `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="418e4-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="418e4-216">Ten atrybut informuje usługi Service Fabric, że usługa hello opiera się na autonomiczną aplikację, więc wszystkie usługi sieć szkieletowa usług musi toodo toolaunch go jako proces i monitorowanie jej kondycji.</span><span class="sxs-lookup"><span data-stu-id="418e4-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="418e4-217">Aktualizowanie elementu CodePackage</span><span class="sxs-lookup"><span data-stu-id="418e4-217">Update CodePackage</span></span>
<span data-ttu-id="418e4-218">element elementu CodePackage Hello Określa lokalizację, hello (i wersji) hello usługi kodu.</span><span class="sxs-lookup"><span data-stu-id="418e4-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="418e4-219">Witaj `Name` element jest używany toospecify hello nazwę katalogu hello w pakiecie aplikacji hello, który zawiera kod hello usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="418e4-220">`CodePackage`ma również hello `version` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="418e4-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="418e4-221">To może być używane toospecify hello wersja hello kodu i może też być używany kod tooupgrade hello usługi przy użyciu infrastruktury zarządzania cyklem życia aplikacji hello w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="418e4-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="418e4-222">Opcjonalnie: SetupEntrypoint aktualizacji</span><span class="sxs-lookup"><span data-stu-id="418e4-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="418e4-223">Hello SetupEntryPoint element jest używany toospecify żadnych plik wykonywalny lub plik wsadowy który ma być wykonany przed uruchomieniem kodu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="418e4-224">Krok opcjonalny, jest więc nie musi toobe włączone, jeśli nie wymagają inicjalizacji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="418e4-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="418e4-225">Witaj SetupEntryPoint jest wykonywane przy każdym uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="418e4-226">Nie tylko jeden element SetupEntryPoint, więc skrypty instalacyjne wymagają toobe zgrupowane w pliku wsadowym pojedynczego, jeśli wiele skryptów wymaga ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="418e4-227">Witaj SetupEntryPoint można wykonywać dowolny typ pliku: pliki wykonywalne, pliki wsadowe i poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="418e4-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="418e4-228">Aby uzyskać więcej informacji, zobacz [skonfigurować SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="418e4-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="418e4-229">W hello poprzedzających przykład, hello SetupEntryPoint uruchamia plik wsadowy o nazwie `LaunchConfig.cmd` czyli znajduje się w hello `scripts` podkatalogu w katalogu kodu hello (przy założeniu, hello WorkingFolder element jest ustawiony tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="418e4-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="418e4-230">Aktualizowanie punktu wejścia</span><span class="sxs-lookup"><span data-stu-id="418e4-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="418e4-231">Witaj `EntryPoint` elementu w pliku manifestu usługi hello jest używany toospecify jak toolaunch hello usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="418e4-232">Witaj `ExeHost` element określa hello pliku wykonywalnego (i argumenty) powinny być używane toolaunch hello usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="418e4-233">`Program`Określa nazwę pliku wykonywalnego hello, który należy uruchomić usługę hello hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="418e4-234">`Arguments`Określa argumenty hello, które powinny być przekazywane wykonywalnego toohello.</span><span class="sxs-lookup"><span data-stu-id="418e4-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="418e4-235">Może być lista parametrów z argumentami.</span><span class="sxs-lookup"><span data-stu-id="418e4-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="418e4-236">`WorkingFolder`Określa katalog roboczy hello hello procesu, który będzie toobe uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="418e4-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="418e4-237">Można określić trzy wartości:</span><span class="sxs-lookup"><span data-stu-id="418e4-237">You can specify three values:</span></span>
  * <span data-ttu-id="418e4-238">`CodeBase`Określa, że katalog roboczy hello będzie toobe Ustaw katalog kodów toohello w pakiecie aplikacji hello (`Code` katalogu w hello poprzedzających struktury plików).</span><span class="sxs-lookup"><span data-stu-id="418e4-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="418e4-239">`CodePackage`Określa, że katalog roboczy hello przechodzi toobe ustawić głównego toohello pakietu aplikacji hello (`GuestService1Pkg` w hello poprzedzających struktury plików).</span><span class="sxs-lookup"><span data-stu-id="418e4-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="418e4-240">`Work`Określa, że pliki hello są umieszczane w podkatalogu o nazwie pracy.</span><span class="sxs-lookup"><span data-stu-id="418e4-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="418e4-241">Witaj WorkingFolder jest przydatne tooset hello poprawny katalog roboczy, aby ścieżek względnych mogą być używane przez skrypty albo hello aplikacji lub inicjowania.</span><span class="sxs-lookup"><span data-stu-id="418e4-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="418e4-242">Zaktualizuj punktów końcowych i zarejestrować w usłudze nazewnictwa do komunikacji</span><span class="sxs-lookup"><span data-stu-id="418e4-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="418e4-243">W hello poprzedzających przykład, hello `Endpoint` element określa hello punkty końcowe, które można nasłuchiwać aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="418e4-244">W tym przykładzie hello aplikacji Node.js nasłuchuje http na porcie 3000.</span><span class="sxs-lookup"><span data-stu-id="418e4-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="418e4-245">Ponadto można zadawać toopublish sieci szkieletowej usług toohello tego punktu końcowego usługi nazewnictwa, inne usługi umożliwia odnalezienie usługi toothis adresu punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="418e4-246">Dzięki temu toobe toocommunicate stanie między usługami, które są pliki wykonywalne gościa.</span><span class="sxs-lookup"><span data-stu-id="418e4-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="418e4-247">Witaj adres punktu końcowego opublikowanych ma formę hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="418e4-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="418e4-248">`UriScheme`i `PathSuffix` są opcjonalne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="418e4-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="418e4-249">`IPAddressOrFQDN`jest hello adresu IP lub nazwy FQDN węzła hello dotyczącymi pobiera tego pliku wykonywalnego i jest obliczana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="418e4-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="418e4-250">W hello poniższy przykład, jeden raz hello usługi jest wdrażana, w narzędziu Service Fabric Explorer wyświetlone podobne punktu końcowego za`http://10.1.4.92:3000/myapp/` opublikowane hello wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="418e4-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="418e4-251">Lub jeśli jest to komputer lokalny, zobacz `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="418e4-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="418e4-252">Korzystając z tych adresów z [odwrotny serwer proxy](service-fabric-reverseproxy.md) toocommunicate między usługami.</span><span class="sxs-lookup"><span data-stu-id="418e4-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="418e4-253">Edytowanie pliku manifestu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="418e4-253">Edit hello application manifest file</span></span>
<span data-ttu-id="418e4-254">Po skonfigurowaniu hello `Servicemanifest.xml` pliku, należy toomake toohello niektóre zmiany `ApplicationManifest.xml` pliku tooensure, który hello poprawny typ usługi i nazwy są używane.</span><span class="sxs-lookup"><span data-stu-id="418e4-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="418e4-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="418e4-255">ServiceManifestImport</span></span>
<span data-ttu-id="418e4-256">W hello `ServiceManifestImport` elementu, można określić jedną lub kilka usług, które mają tooinclude w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="418e4-257">Usługi są przywoływane z `ServiceManifestName`, który określa nazwę hello hello katalogu, gdzie hello `ServiceManifest.xml` znajduje się plik.</span><span class="sxs-lookup"><span data-stu-id="418e4-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="418e4-258">Konfigurowanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="418e4-258">Set up logging</span></span>
<span data-ttu-id="418e4-259">Pliki wykonywalne gościa jest przydatne toobe stanie toosee konsoli Dzienniki toofind limit Jeśli skryptów aplikacji i konfiguracji hello wyświetlać żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="418e4-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="418e4-260">Przekierowywanie konsoli można skonfigurować w hello `ServiceManifest.xml` plik przy użyciu hello `ConsoleRedirection` elementu.</span><span class="sxs-lookup"><span data-stu-id="418e4-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="418e4-261">Nigdy nie używaj zasad przekierowania konsoli hello w aplikacji, która jest wdrożony w środowisku produkcyjnym, ponieważ może to mieć wpływ na powitania aplikacji w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="418e4-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="418e4-262">*Tylko* użyć tej funkcji dla rozwoju lokalnych i debugowania.</span><span class="sxs-lookup"><span data-stu-id="418e4-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="418e4-263">`ConsoleRedirection`może to być katalog roboczy tooa tooredirect używane Konsola danych wyjściowych (stdout i stderr).</span><span class="sxs-lookup"><span data-stu-id="418e4-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="418e4-264">Udostępnia hello możliwości tooverify, że nie ma żadnych błędów podczas instalacji hello lub wykonywanie aplikacji hello w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="418e4-265">`FileRetentionCount`Określa, ile plików są zapisywane w katalogu roboczym hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="418e4-266">Na przykład wartość 5, oznacza, że hello pliki dziennika poprzedniego wykonaniami pięć hello są przechowywane w katalogu roboczym hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="418e4-267">`FileMaxSizeInKb`Określa maksymalny rozmiar plików dziennika hello hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="418e4-268">Pliki dziennika są zapisywane w jednym z katalogów roboczych usługi hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="418e4-269">toodetermine, w którym znajdują się, hello pliki za pomocą Eksploratora usługi sieć szkieletowa toodetermine usługi hello węzła, która jest uruchomiona na i katalog roboczy, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="418e4-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="418e4-270">Ten proces jest uwzględnione w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="418e4-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="418e4-271">Wdrożenie</span><span class="sxs-lookup"><span data-stu-id="418e4-271">Deployment</span></span>
<span data-ttu-id="418e4-272">ostatni krok Hello jest zbyt[wdrożyć aplikację](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="418e4-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="418e4-273">Witaj, jak po pokazuje skrypt programu PowerShell toodeploy Twojej aplikacji toohello lokalnego klastra projektowego i rozpocząć nową usługę sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="418e4-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="418e4-274">[Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów, jeśli pakietów hello jest długa lub zawiera wiele plików.</span><span class="sxs-lookup"><span data-stu-id="418e4-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="418e4-275">Dowiedz się więcej [tutaj](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="418e4-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="418e4-276">Usługa sieci szkieletowej usług można wdrożyć w różnych "konfiguracji."</span><span class="sxs-lookup"><span data-stu-id="418e4-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="418e4-277">Na przykład można wdrożyć jako jednego lub wielu wystąpień lub mogą być wdrażane w taki sposób, że istnieje jedno wystąpienie usługi hello w każdym węźle klastra sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="418e4-278">Witaj `InstanceCount` parametru hello `New-ServiceFabricService` polecenia cmdlet jest używane toospecify jak wiele wystąpień usługi hello powinna być uruchamiana w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="418e4-279">Można ustawić hello `InstanceCount` wartość, w zależności od typu hello aplikacji, która jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="418e4-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="418e4-280">Witaj dwie najczęstsze scenariusze są następujące:</span><span class="sxs-lookup"><span data-stu-id="418e4-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="418e4-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="418e4-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="418e4-282">W takim przypadku tylko jedno wystąpienie usługi hello jest wdrażane w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="418e4-283">Harmonogram usługi sieć szkieletowa określa usługi hello węzła, która będzie toobe wdrożone na.</span><span class="sxs-lookup"><span data-stu-id="418e4-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="418e4-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="418e4-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="418e4-285">W takim przypadku jednego wystąpienia usługi hello jest wdrażana na każdym węźle w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="418e4-286">wynik Hello ma jeden (i tylko jeden) wystąpienia usługi powitania dla każdego węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="418e4-287">Jest to przydatne w konfiguracji dla aplikacji frontonu (na przykład punkt końcowy REST), ponieważ aplikacje klienckie wymagają zbyt "connect" tooany hello węzłów hello punktu końcowego hello toouse dla klastra.</span><span class="sxs-lookup"><span data-stu-id="418e4-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="418e4-288">Tę konfigurację można również w przypadku, na przykład wszystkie węzły klastra sieci szkieletowej usług hello tooa podłączonej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="418e4-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="418e4-289">Ruch klientów następnie mogą być rozproszone na powitania usługa, która jest uruchomiona na wszystkich węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="418e4-290">Sprawdź uruchomionej aplikacji</span><span class="sxs-lookup"><span data-stu-id="418e4-290">Check your running application</span></span>
<span data-ttu-id="418e4-291">W narzędziu Service Fabric Explorer Zidentyfikuj węzła hello, w którym jest uruchomiona usługa hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="418e4-292">W tym przykładzie jest uruchamiany na Node1:</span><span class="sxs-lookup"><span data-stu-id="418e4-292">In this example, it runs on Node1:</span></span>

![Węzeł, na którym jest uruchomiona usługa](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="418e4-294">Jeśli przejdź do węzła toohello i Przeglądaj toohello aplikacji, zobaczysz hello węzła istotne informacje, w tym lokalizacji na dysku.</span><span class="sxs-lookup"><span data-stu-id="418e4-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Miejsce na dysku](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="418e4-296">Przeglądaj katalog toohello za pomocą Eksploratora serwera można znaleźć folderu dziennika hello usługi i katalog roboczy hello, zgodnie z powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="418e4-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Lokalizacja dziennika](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="418e4-298">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="418e4-298">Next steps</span></span>
<span data-ttu-id="418e4-299">W tym artykule wiesz już, jak toopackage pliku wykonywalnego gościa i wdróż je tooService sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="418e4-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="418e4-300">Zobacz następujące artykuły powiązane informacje i zadań hello.</span><span class="sxs-lookup"><span data-stu-id="418e4-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="418e4-301">[Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), łącznie z łącza toohello wstępnej wersji narzędzia do tworzenia pakietów hello</span><span class="sxs-lookup"><span data-stu-id="418e4-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="418e4-302">Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="418e4-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="418e4-303">Wdrażanie wielu aplikacji wykonywalnych gości</span><span class="sxs-lookup"><span data-stu-id="418e4-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="418e4-304">Tworzenie pierwszej aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="418e4-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
