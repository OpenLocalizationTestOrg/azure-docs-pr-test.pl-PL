---
title: "aaaUpgrade autonomiczny sieć szkieletowa usług Azure klastra w systemie Windows Server | Dokumentacja firmy Microsoft"
description: "Uaktualnij hello sieć szkieletowa usług Azure kod i/lub konfigurację, która uruchamia autonomicznej klastra sieci szkieletowej usług, w tym ustawieniu trybu aktualizacji klastra hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="6eda1-103">Uaktualnienie z autonomicznej usługi sieć szkieletowa usług Azure w klastrze systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="6eda1-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6eda1-104">Klastrze platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6eda1-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="6eda1-105">Autonomiczny klastra</span><span class="sxs-lookup"><span data-stu-id="6eda1-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="6eda1-106">Systemu nowoczesnych tooupgrade możliwości hello został pomyślnie długoterminowej toohello klucza produktu.</span><span class="sxs-lookup"><span data-stu-id="6eda1-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="6eda1-107">Klastra usługi sieć szkieletowa usług Azure jest zasobem, którego jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="6eda1-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="6eda1-108">W tym artykule opisano, jak można upewnij się, że klastra hello jest zawsze uruchamiane w obsługiwanych wersjach programu kodu sieci szkieletowej usług i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6eda1-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="6eda1-109">Formant hello sieci szkieletowej usług wersji, która działa w klastrze</span><span class="sxs-lookup"><span data-stu-id="6eda1-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="6eda1-110">tooset aktualizuje toodownload Twojego klastra usługi sieć szkieletowa, gdy firma Microsoft publikuje nową wersję zestawu hello **fabricClusterAutoupgradeEnabled** tootrue konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="6eda1-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="6eda1-111">obsługiwana wersja usługi sieć szkieletowa usług, które mają toobe Twojego klastra na powitania zestaw tooselect **fabricClusterAutoupgradeEnabled** toofalse konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="6eda1-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="6eda1-112">Upewnij się, że klaster zawsze działa obsługiwana wersja usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6eda1-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="6eda1-113">Microsoft ogłasza hello wydaniu nowej wersji platformy Service Fabric, poprzedniej wersji hello jest oznaczony w celu obsługi po co najmniej 60 dni od daty hello hello anonsu.</span><span class="sxs-lookup"><span data-stu-id="6eda1-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="6eda1-114">Nowe wersje są ogłaszane [na blogu zespołu usługi sieć szkieletowa hello](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="6eda1-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="6eda1-115">nową wersję Hello jest toochoose dostępne w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="6eda1-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="6eda1-116">Klaster toohello nowej wersji można uaktualnić tylko wtedy, gdy używane są konfiguracji węzła stylu produkcji, gdzie każdy węzeł sieci szkieletowej usług jest przydzielane w oddzielnych maszyny fizycznej lub wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6eda1-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="6eda1-117">Jeśli masz klaster programowanie, gdzie więcej niż jeden węzeł sieci szkieletowej usług znajduje się na jednej maszynie fizycznej lub wirtualnej, należy ponownie utworzyć klaster hello hello nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="6eda1-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="6eda1-118">Dwa różne przepływów pracy można uaktualnić najnowszej wersji toohello klastra lub obsługiwana wersja usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6eda1-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="6eda1-119">Jeden przepływ pracy jest przeznaczony dla klastrów, które mają automatycznie łączności toodownload hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="6eda1-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="6eda1-120">Witaj inny przepływ pracy jest klastrów, które nie mają łączność toodownload hello sieci szkieletowej usług najnowszą.</span><span class="sxs-lookup"><span data-stu-id="6eda1-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="6eda1-121">Uaktualnij klastrów, które mają łączność toodownload hello najnowsze kod i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="6eda1-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="6eda1-122">Użyć wersji tooa obsługiwane klastra tooupgrade te kroki, jeśli węzły klastra jest połączony z Internetem za[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6eda1-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="6eda1-123">W przypadku klastrów połączeniem zbyt[http://download.microsoft.com](http://download.microsoft.com), Microsoft okresowo sprawdza dostępność nowych wersji platformy Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="6eda1-124">Dostępna jest nowa wersja usługi Service Fabric, pakietów hello jest pobierana lokalnie toohello klastra i udostępnione do uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="6eda1-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="6eda1-125">Ponadto tooinform powitania klienta z tej nowej wersji, hello system zawiera ostrzeżenia kondycji jawne klastra, która jest podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="6eda1-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="6eda1-126">"hello Obsługa bieżącej wersji wersja # klastra kończy [Date]".</span><span class="sxs-lookup"><span data-stu-id="6eda1-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="6eda1-127">Po uruchomieniu klastra hello hello najnowszej wersji ostrzeżenie hello zniknie.</span><span class="sxs-lookup"><span data-stu-id="6eda1-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="6eda1-128">Przepływ pracy uaktualniania klastra</span><span class="sxs-lookup"><span data-stu-id="6eda1-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="6eda1-129">Po zostanie wyświetlone ostrzeżenie dotyczące kondycji klastra hello, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6eda1-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="6eda1-130">Połącz toohello klastra z dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="6eda1-131">Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="6eda1-132">Pobierz listę hello można uaktualnić do wersji usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="6eda1-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="6eda1-133">Należy pobrać toothis podobne dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6eda1-133">You should get an output similar toothis:</span></span>

    ![Pobieranie wersji sieci szkieletowej][getfabversions]
3. <span data-ttu-id="6eda1-135">Uruchom wersji dostępnych tooan uaktualnienia klastra przy użyciu [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6eda1-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="6eda1-136">postęp hello toomonitor hello uaktualnienia, można użyć Eksploratora usługi sieć szkieletowa lub hello uruchom następujące polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eda1-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="6eda1-137">Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="6eda1-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="6eda1-138">zasady dotyczące kondycji niestandardowych toospecify dla hello **Start ServiceFabricClusterUpgrade** polecenia, zobacz dokumentację dla [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eda1-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="6eda1-139">Po rozwiązaniu problemów hello, które spowodowało wycofanie hello zainicjować ponownie uaktualnienie hello przez następujące hello opisanej wcześniej te same czynności.</span><span class="sxs-lookup"><span data-stu-id="6eda1-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="6eda1-140">Uaktualnij klastrów, które mają <U>bez łączności</u> toodownload hello najnowsze kodem i konfiguracją</span><span class="sxs-lookup"><span data-stu-id="6eda1-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="6eda1-141">Użyć wersji tooa obsługiwane klastra tooupgrade te kroki, jeśli węzły klastra nie ma łączności z Internetem za[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6eda1-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6eda1-142">Jeśli korzystasz z klastra, który nie jest połączony toohello Internet, trzeba będzie toomonitor hello sieci szkieletowej usług team blog toolearn o nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="6eda1-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="6eda1-143">Witaj systemu nie są wyświetlane tooalert ostrzeżenie kondycji klastra z nową wersją.</span><span class="sxs-lookup"><span data-stu-id="6eda1-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="6eda1-144">Automatycznego inicjowania obsługi administracyjnej vs ręcznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="6eda1-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="6eda1-145">automatyczne pobieranie tooenable i rejestracji hello najnowszą wersję kodu, należy skonfigurować usługi aktualizacji sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="6eda1-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="6eda1-146">Zobacz toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt wewnątrz hello [pakiet autonomiczny](service-fabric-cluster-standalone-package-contents.md) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="6eda1-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="6eda1-147">W przypadku ręczny proces wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="6eda1-148">Modyfikowanie użytkownika hello tooset konfiguracji klastra po toofalse właściwości przed rozpoczęciem uaktualniania programu configuration.</span><span class="sxs-lookup"><span data-stu-id="6eda1-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="6eda1-149">Odwołuje się zbyt[cmd PS Start ServiceFabricClusterConfigurationUpgrade ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) szczegóły użycia.</span><span class="sxs-lookup"><span data-stu-id="6eda1-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="6eda1-150">Przed rozpoczęciem uaktualniania konfiguracji hello, upewnij się, że tooupdate "clusterConfigurationVersion" w Twojej JSON.</span><span class="sxs-lookup"><span data-stu-id="6eda1-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="6eda1-151">Przepływ pracy uaktualniania klastra</span><span class="sxs-lookup"><span data-stu-id="6eda1-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="6eda1-152">Uruchom Get ServiceFabricClusterUpgrade w jednym z węzłów hello hello klastra i zanotuj hello TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="6eda1-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="6eda1-153">Witaj uruchom następujące polecenie w toolist maszyny połączenia internetowego uaktualnić wszystkie wersje zgodne z bieżącą wersją hello i Pobierz hello odpowiadającego pakietu z hello łączy do pobierania.</span><span class="sxs-lookup"><span data-stu-id="6eda1-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="6eda1-154">Połącz toohello klastra z dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="6eda1-155">Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello</span><span class="sxs-lookup"><span data-stu-id="6eda1-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="6eda1-156">Skopiuj pakiet hello pobrane do magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="6eda1-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="6eda1-157">Zarejestruj hello skopiować pakiet.</span><span class="sxs-lookup"><span data-stu-id="6eda1-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="6eda1-158">Uruchom tooan uaktualnienia klastra dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="6eda1-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="6eda1-159">Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer, lub uruchomić hello następującego polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eda1-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="6eda1-160">Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="6eda1-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="6eda1-161">zasady dotyczące kondycji niestandardowych toospecify dla hello **Start ServiceFabricClusterUpgrade** polecenia, zobacz dokumentację hello [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eda1-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="6eda1-162">Po rozwiązaniu problemów hello, które spowodowało wycofanie hello zainicjować ponownie uaktualnienie hello przez następujące hello opisanej wcześniej te same czynności.</span><span class="sxs-lookup"><span data-stu-id="6eda1-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="6eda1-163">Uaktualnij konfigurację klastra hello</span><span class="sxs-lookup"><span data-stu-id="6eda1-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="6eda1-164">Przed rozpoczęciem uaktualniania konfiguracji hello można sprawdzić czy nowy kod json konfiguracji klastra za pomocą skryptu powershell hello hello autonomicznych pakietu.</span><span class="sxs-lookup"><span data-stu-id="6eda1-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="6eda1-165">lub</span><span class="sxs-lookup"><span data-stu-id="6eda1-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="6eda1-166">Niektóre konfiguracje nie może zostać uaktualniony, takich jak punkty końcowe, nazwa klastra IP węzła itd. Spowoduje to test hello nowego klastra konfiguracji json przed hello stary i zgłoszenia błędów w oknie programu Powershell hello, jeśli istnieje jakikolwiek problem.</span><span class="sxs-lookup"><span data-stu-id="6eda1-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="6eda1-167">Uaktualnianie konfiguracji klastra hello tooupgrade, uruchom **Start ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="6eda1-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="6eda1-168">Uaktualnianie konfiguracji Hello jest przetworzonych domeny uaktualnień w domenie uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="6eda1-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="6eda1-169">Uaktualnianie konfiguracji certyfikatu klastra</span><span class="sxs-lookup"><span data-stu-id="6eda1-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="6eda1-170">Certyfikat klastra jest używany do uwierzytelniania między węzłami klastra, więc przerzucane hello certyfikatu należy wykonać z wyjątkową ostrożność ponieważ niepowodzenia zablokuje hello komunikacji między węzłami klastra.</span><span class="sxs-lookup"><span data-stu-id="6eda1-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="6eda1-171">Z technicznego punktu widzenia obsługiwane są trzy opcje:</span><span class="sxs-lookup"><span data-stu-id="6eda1-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="6eda1-172">Uaktualnienie jeden certyfikat: ścieżka uaktualnienia hello jest "certyfikat (podstawowy) -> B certyfikatu (podstawowy) -> C certyfikatu (podstawowy) ->...".</span><span class="sxs-lookup"><span data-stu-id="6eda1-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="6eda1-173">Double certyfikatu uaktualnienia: ścieżka uaktualnienia hello jest "B (pomocniczy) -> B certyfikatu (podstawowy) i certyfikatów (podstawowy) -> certyfikatów (podstawowy) -> B certyfikatu (podstawowy) i C (pomocniczy) -> C certyfikatu (podstawowy) ->...".</span><span class="sxs-lookup"><span data-stu-id="6eda1-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="6eda1-174">Uaktualnianie typu certyfikatu: Konfiguracja certyfikatów na podstawie CommonName configuration <> — na podstawie odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6eda1-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="6eda1-175">Na przykład odcisk palca certyfikatu (podstawowy) i certyfikatów CommonName C. -> B odcisk palca (pomocniczy)</span><span class="sxs-lookup"><span data-stu-id="6eda1-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6eda1-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6eda1-176">Next steps</span></span>
* <span data-ttu-id="6eda1-177">Dowiedz się, jak toocustomize niektórych [ustawienia klastra usługi sieć szkieletowa](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6eda1-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="6eda1-178">Dowiedz się, jak za[skalowanie klastra i wylogowywanie](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="6eda1-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="6eda1-179">Dowiedz się więcej o [uaktualnień aplikacji](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="6eda1-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
