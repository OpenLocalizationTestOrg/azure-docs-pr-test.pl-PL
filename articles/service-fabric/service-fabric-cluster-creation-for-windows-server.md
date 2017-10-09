---
title: "aaaCreate autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie klastra usługi sieć szkieletowa usług Azure na dowolnym komputerze (fizycznych lub wirtualnych) systemem Windows Server, czy jest lokalnie lub w dowolnym chmury."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="3189e-103">Tworzenie autonomicznych klastra w systemie Windows Server</span><span class="sxs-lookup"><span data-stu-id="3189e-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="3189e-104">Za pomocą usługi Azure Service Fabric toocreate sieci szkieletowej usług klastrów na dowolnym maszyn wirtualnych lub komputerach z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3189e-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="3189e-105">Oznacza to, można wdrażać i uruchamianie aplikacji platformy Service Fabric w dowolnym środowisku, które zawiera zestaw połączonych komputerów z systemem Windows Server, lokalnie i z każdego dostawcy chmury.</span><span class="sxs-lookup"><span data-stu-id="3189e-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="3189e-106">Sieć szkieletowa usług zawiera pakiet Windows Server autonomiczny hello o nazwie toocreate pakiet Instalatora, które klastrów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="3189e-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="3189e-107">W tym artykule przedstawiono kroki hello tworzenia klastra usługi sieć szkieletowa autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="3189e-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3189e-108">Ten pakiet Windows Server autonomiczny jest dostępnych na rynku, może być używany we wdrożeniach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="3189e-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="3189e-109">Ten pakiet może zawierać nowe funkcje sieci szkieletowej usług, które znajdują się w "W wersji zapoznawczej".</span><span class="sxs-lookup"><span data-stu-id="3189e-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="3189e-110">Przewiń w dół za"[Podgląd funkcje zawarte w tym pakiecie](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="3189e-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="3189e-111">sekcja listy hello hello funkcje w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="3189e-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="3189e-112">Możesz [Pobierz kopię hello umowy licencyjnej](http://go.microsoft.com/fwlink/?LinkID=733084) teraz.</span><span class="sxs-lookup"><span data-stu-id="3189e-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="3189e-113">Uzyskaj pomoc dotyczącą hello pakietu sieci szkieletowej usług dla systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="3189e-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="3189e-114">Zapytaj społeczności hello o pakiet autonomiczny hello sieci szkieletowej usług dla systemu Windows Server w hello [forum usługi Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="3189e-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="3189e-115">Otwórz bilet dla [Professional obsługę sieci szkieletowej usług](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="3189e-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="3189e-116">Dowiedz się więcej na temat pomocy technicznej Professional firmy Microsoft [tutaj](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="3189e-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="3189e-117">Można również uzyskać pomoc techniczną dla tego pakietu, jako część [pomocy technicznej Microsoft Premier](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="3189e-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="3189e-118">Aby uzyskać więcej informacji, zobacz [opcje pomocy technicznej usługi Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="3189e-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="3189e-119">Dzienniki toocollect na potrzeby obsługi Uruchom hello [logowania do usługi sieci szkieletowej autonomiczny moduł zbierający](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="3189e-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="3189e-120">Pobierz pakiet sieci szkieletowej usług dla systemu Windows Server hello</span><span class="sxs-lookup"><span data-stu-id="3189e-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="3189e-121">toocreate hello klastra, użyj pakietu sieci szkieletowej usług dla systemu Windows Server hello (Windows Server 2012 R2 i nowszych) znaleźć tutaj:</span><span class="sxs-lookup"><span data-stu-id="3189e-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="3189e-122">
[Pobierz Link - pakietu autonomicznego sieci szkieletowej usług - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="3189e-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="3189e-123">Znajduje szczegóły na zawartość pakietu hello [tutaj](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="3189e-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="3189e-124">Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierana podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3189e-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="3189e-125">Jeśli wdrażania na komputerze nie podłączony toohello Internetu, Pobierz pakiet środowiska uruchomieniowego hello poza pasmem w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="3189e-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="3189e-126">
[Pobierz łącze — środowisko uruchomieniowe usługi sieć szkieletowa - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="3189e-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="3189e-127">Szukaj przykładowych autonomicznej konfiguracji klastra na:</span><span class="sxs-lookup"><span data-stu-id="3189e-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="3189e-128">
[Przykłady konfiguracji autonomicznej klastra](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="3189e-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="3189e-129">Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="3189e-129">Create hello cluster</span></span>
<span data-ttu-id="3189e-130">Sieć szkieletowa usług może być klastrem programowanie jednej maszyny tooa wdrożone za pomocą hello *ClusterConfig.Unsecure.DevCluster.json* zawarte w pliku [przykłady](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="3189e-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="3189e-131">Rozpakuj hello autonomicznych pakietu tooyour maszyny, kopiowania hello przykładowej konfiguracji pliku toohello komputera lokalnego, a następnie uruchom hello *CreateServiceFabricCluster.ps1* skryptu za pomocą sesji programu PowerShell administratora z autonomicznego hello folder pakietu:</span><span class="sxs-lookup"><span data-stu-id="3189e-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="3189e-132">Krok 1A: tworzenie niezabezpieczona lokalnego klastra projektowego</span><span class="sxs-lookup"><span data-stu-id="3189e-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="3189e-133">Zobacz hello sekcji konfigurowania środowiska w [planowanie i przygotowanie wdrożenia klastra](service-fabric-cluster-standalone-deployment-preparation.md) dla szczegóły dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="3189e-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="3189e-134">Zakończeniu uruchomionych scenariusze programowania, można usunąć klastra sieci szkieletowej usług hello z hello maszyny, odwołując się toosteps w sekcji "[usunąć klaster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="3189e-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="3189e-135">Krok 1B: tworzenie obsługi wielu komputerów klastra</span><span class="sxs-lookup"><span data-stu-id="3189e-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="3189e-136">Po przejściu hello planowania, szczegółowe kroki przygotowania na powitania poniżej łącza, gotowe toocreate klastra produkcyjnego przy użyciu pliku konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="3189e-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="3189e-137">
[Planowanie i przygotowanie wdrożenia klastra](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="3189e-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="3189e-138">Sprawdzanie poprawności pliku konfiguracji hello zostały zapisane, uruchamiając hello *TestConfiguration.ps1* skryptu z folderu pakietu autonomicznego hello:</span><span class="sxs-lookup"><span data-stu-id="3189e-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="3189e-139">Powinny pojawić się dane wyjściowe, takich jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="3189e-139">You should see output like below.</span></span> <span data-ttu-id="3189e-140">Jeśli pole dolnej hello "Zakończony pomyślnie", jest zwracana jako "True", związane z poprawnością sprawdzenie powiodło się i hello klastra wygląda toobe do wdrożenia na podstawie konfiguracji wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="3189e-141">Tworzenie klastra hello: Uruchom hello *CreateServiceFabricCluster.ps1* klastra sieci szkieletowej usług hello toodeploy skrypt na każdej maszynie w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="3189e-142">Wdrożenie śledzenia są zapisywane toohello maszyny Wirtualnej/maszyny, na których uruchomiono skrypt programu PowerShell CreateServiceFabricCluster.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="3189e-143">Te znajdują się w podfolderze hello DeploymentTraces, na podstawie w katalogu hello, z których hello uruchomienia skryptu.</span><span class="sxs-lookup"><span data-stu-id="3189e-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="3189e-144">toosee, jeśli sieć szkieletowa usług został poprawnie wdrożony tooa maszyny, Znajdź hello zainstalowane pliki w katalogu zmiennej FabricDataRoot hello, zgodnie z opisem w pliku konfiguracji klastra hello sekcji FabricSettings (c:\ProgramData\SF domyślną).</span><span class="sxs-lookup"><span data-stu-id="3189e-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="3189e-145">Jak również procesy FabricHost.exe i Fabric.exe są widoczne w Menedżerze zadań.</span><span class="sxs-lookup"><span data-stu-id="3189e-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="3189e-146">Krok 1C: Tworzenie klastra w trybie offline (odłączony od Internetu)</span><span class="sxs-lookup"><span data-stu-id="3189e-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="3189e-147">Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierana podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3189e-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="3189e-148">Gdy wdrażanie toomachines klastra nie podłączone toohello internet, trzeba będzie hello toodownload sieci szkieletowej usług środowisko uruchomieniowe pakietu oddzielnie i podaj hello tooit ścieżki, podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3189e-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="3189e-149">Witaj środowisko uruchomieniowe pakietu można pobrać oddzielnie, z innego komputera podłączony toohello internet, w [łącze Pobierz — środowisko uruchomieniowe usługi sieć szkieletowa - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="3189e-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="3189e-150">Skopiuj hello środowisko uruchomieniowe pakietu toowhere wdrażasz hello klastra w trybie offline z i utworzyć klaster hello uruchamiając `CreateServiceFabricCluster.ps1` z hello `-FabricRuntimePackagePath` parametru, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="3189e-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="3189e-151">gdzie `.\ClusterConfig.json` i `.\MicrosoftAzureServiceFabric.cab` są odpowiednio hello ścieżki toohello konfiguracji klastra i pliku cab hello środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="3189e-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="3189e-152">Krok 2: Łączenie toohello klastra</span><span class="sxs-lookup"><span data-stu-id="3189e-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="3189e-153">tooconnect tooa bezpiecznego klastra, zobacz [sieci szkieletowej usług połączenia klastra toosecure](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3189e-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="3189e-154">tooconnect tooan niezabezpieczone klastra, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="3189e-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="3189e-155">Przykład:</span><span class="sxs-lookup"><span data-stu-id="3189e-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="3189e-156">Krok 3: Wywołaj okno Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="3189e-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="3189e-157">Teraz możesz połączyć toohello klastra z Eksploratora usługi sieć szkieletowa albo bezpośrednio z maszyn hello http://localhost:19080/Explorer/index.html lub zdalnie http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="3189e-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="3189e-158">Dodawanie i usuwanie węzłów</span><span class="sxs-lookup"><span data-stu-id="3189e-158">Add and remove nodes</span></span>
<span data-ttu-id="3189e-159">Można dodać lub usunąć klastra sieci szkieletowej usług autonomiczny tooyour węzłów, ponieważ zmieniających się potrzeb firmy.</span><span class="sxs-lookup"><span data-stu-id="3189e-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="3189e-160">Zobacz [dodać lub usunąć klaster autonomicznej usługi Service Fabric tooa węzłów](service-fabric-cluster-windows-server-add-remove-nodes.md) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="3189e-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="3189e-161">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="3189e-161">Remove a cluster</span></span>
<span data-ttu-id="3189e-162">tooremove klastra, uruchom hello *RemoveServiceFabricCluster.ps1* skrypt programu PowerShell z folderu pakietu hello i przekazać w pliku konfiguracji JSON hello ścieżki toohello.</span><span class="sxs-lookup"><span data-stu-id="3189e-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="3189e-163">Opcjonalnie można określić lokalizację dziennika hello hello usuwania.</span><span class="sxs-lookup"><span data-stu-id="3189e-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="3189e-164">Ten skrypt można uruchomić na dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w pliku konfiguracji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="3189e-165">Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="3189e-166">Dane telemetryczne zbierane i jak tooopt od niego</span><span class="sxs-lookup"><span data-stu-id="3189e-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="3189e-167">Domyślnie produktu hello zbiera dane telemetryczne hello sieci szkieletowej usług użycia tooimprove hello produktu.</span><span class="sxs-lookup"><span data-stu-id="3189e-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="3189e-168">Analizator najlepszych rozwiązań, który działa jako część instalacji hello sprawdza łączność za Hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="3189e-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="3189e-169">Jeśli nie jest dostępny, hello instalacja zakończy się niepowodzeniem, Jeśli zrezygnujesz z telemetrii.</span><span class="sxs-lookup"><span data-stu-id="3189e-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="3189e-170">Hello potoku telemetrii próbuje hello tooupload następujące dane zbyt[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) raz każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="3189e-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="3189e-171">Jest przekazywanie optymalnych i nie ma wpływu na funkcjonalność klastra hello.</span><span class="sxs-lookup"><span data-stu-id="3189e-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="3189e-172">telemetrii Hello jest wysyłane tylko z węzła hello czy działa hello podstawowy menedżera trybu failover.</span><span class="sxs-lookup"><span data-stu-id="3189e-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="3189e-173">Nie inne węzły wysłać dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="3189e-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="3189e-174">dane telemetryczne Hello składa się z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="3189e-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="3189e-175">Liczba usług</span><span class="sxs-lookup"><span data-stu-id="3189e-175">Number of services</span></span>
* <span data-ttu-id="3189e-176">Liczba Serivcetype</span><span class="sxs-lookup"><span data-stu-id="3189e-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="3189e-177">Liczba aplikacji</span><span class="sxs-lookup"><span data-stu-id="3189e-177">Number of Applications</span></span>
* <span data-ttu-id="3189e-178">Liczba ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="3189e-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="3189e-179">Liczba jednostek trybu failover</span><span class="sxs-lookup"><span data-stu-id="3189e-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="3189e-180">Liczba stanie Inbuild</span><span class="sxs-lookup"><span data-stu-id="3189e-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="3189e-181">Liczba UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="3189e-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="3189e-182">Liczba replik</span><span class="sxs-lookup"><span data-stu-id="3189e-182">Number of Replicas</span></span>
* <span data-ttu-id="3189e-183">Liczba InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="3189e-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="3189e-184">Liczba StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="3189e-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="3189e-185">Liczba OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="3189e-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="3189e-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="3189e-186">CommonQueueLength</span></span>
* <span data-ttu-id="3189e-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="3189e-187">QueryQueueLength</span></span>
* <span data-ttu-id="3189e-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="3189e-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="3189e-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="3189e-189">CommitQueueLength</span></span>
* <span data-ttu-id="3189e-190">Liczba węzłów</span><span class="sxs-lookup"><span data-stu-id="3189e-190">Number of Nodes</span></span>
* <span data-ttu-id="3189e-191">IsContextComplete: PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="3189e-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="3189e-192">ClusterId: Jest to identyfikator GUID generowany losowo dla każdego klastra</span><span class="sxs-lookup"><span data-stu-id="3189e-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="3189e-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="3189e-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="3189e-194">Adres IP maszyny wirtualnej hello lub komputera, z którym hello jest przekazywany telemetrii</span><span class="sxs-lookup"><span data-stu-id="3189e-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="3189e-195">telemetria toodisable dodaje hello zbyt*właściwości* w pliku config klastra: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="3189e-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="3189e-196">Funkcje w wersji zapoznawczej zawarte w tym pakiecie</span><span class="sxs-lookup"><span data-stu-id="3189e-196">Preview features included in this package</span></span>
<span data-ttu-id="3189e-197">Brak.</span><span class="sxs-lookup"><span data-stu-id="3189e-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="3189e-198">Zaczynając od nowego hello [wersją GA hello autonomiczny klastra w systemie Windows Server (wersja 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), Twojej wersji toofuture klastra, możesz uaktualnić ręcznie lub automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3189e-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="3189e-199">Odwołuje się zbyt[uaktualnienie wersji autonomicznej klastra sieci szkieletowej usług](service-fabric-cluster-upgrade-windows-server.md) dokumentu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3189e-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3189e-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3189e-200">Next steps</span></span>
* [<span data-ttu-id="3189e-201">Wdrażanie i usunąć aplikacje przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3189e-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="3189e-202">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3189e-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="3189e-203">Dodawanie lub usuwanie klastra sieci szkieletowej usług autonomiczny tooa węzłów</span><span class="sxs-lookup"><span data-stu-id="3189e-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="3189e-204">Uaktualnienie wersji autonomicznej klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="3189e-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="3189e-205">Tworzenie klastra usługi sieć szkieletowa autonomiczny z systemem Windows maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3189e-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="3189e-206">Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3189e-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="3189e-207">Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów</span><span class="sxs-lookup"><span data-stu-id="3189e-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
