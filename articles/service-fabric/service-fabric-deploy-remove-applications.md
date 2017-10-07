---
title: "aaaAzure wdrożenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Jak toodeploy i usunąć aplikacje w sieci szkieletowej usług za pomocą programu PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="b028b-103">Wdrażanie i usunąć aplikacje przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b028b-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b028b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b028b-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="b028b-105">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b028b-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="b028b-106">Interfejsy API FabricClient</span><span class="sxs-lookup"><span data-stu-id="b028b-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="b028b-107">Raz [typu aplikacji zostały opakowane][10], jest ono gotowe do wdrożenia do klastra usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="b028b-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="b028b-108">Wdrożenie obejmuje hello następujące trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="b028b-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="b028b-109">Przekaż magazynu obrazów toohello pakietu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b028b-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="b028b-110">Rejestracja typu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b028b-110">Register hello application type</span></span>
3. <span data-ttu-id="b028b-111">Tworzenie wystąpienia aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b028b-111">Create hello application instance</span></span>

<span data-ttu-id="b028b-112">Po wdrożeniu aplikacji i wystąpienie jest uruchomione w klastrze hello, można usunąć wystąpienia aplikacji hello i typem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="b028b-113">Usuń toocompletely aplikacji z klastra hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b028b-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="b028b-114">Usuń (lub usunąć) hello uruchomione wystąpienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b028b-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="b028b-115">Wyrejestrowywanie typu aplikacji hello, jeśli nie są już potrzebne</span><span class="sxs-lookup"><span data-stu-id="b028b-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="b028b-116">Usuwanie pakietu aplikacji hello z magazynu obrazów hello</span><span class="sxs-lookup"><span data-stu-id="b028b-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="b028b-117">Jeśli używasz [programu Visual Studio umożliwiające wdrażanie i debugowanie aplikacji](service-fabric-publish-app-remote-cluster.md) na klaster lokalny rozwój hello wszystkich powyższych kroków obsługi automatycznie za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b028b-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="b028b-118">Skrypt ten znajduje się w hello *skryptów* folderu projekt aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="b028b-119">Ten artykuł zawiera tła na tego skryptu czynności, aby można było wykonać hello operacji poza Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b028b-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="b028b-120">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="b028b-120">Connect toohello cluster</span></span>
<span data-ttu-id="b028b-121">Przed uruchomieniem żadnych poleceń programu PowerShell w tym artykule należy uruchamiać przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) klastra sieci szkieletowej usług toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b028b-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="b028b-122">tooconnect toohello lokalnego klastra projektowego, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b028b-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="b028b-123">Przykłady połączeniu tooa zdalnego klastra lub klastra zabezpieczone przy użyciu usługi Azure Active Directory, X509 certyfikatów lub usługi Active Directory systemu Windows, zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b028b-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="b028b-124">Przekaż pakiet aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b028b-124">Upload hello application package</span></span>
<span data-ttu-id="b028b-125">Przekazywanie pakietu aplikacji hello umieszcza je w lokalizacji, który jest dostępny dla wewnętrznych składników usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b028b-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="b028b-126">Pakiet aplikacji hello tooverify lokalnie, należy użyć hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b028b-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b028b-127">Witaj [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia przekazywania hello sklepu z aplikacjami pakietu toohello klastra obrazu.</span><span class="sxs-lookup"><span data-stu-id="b028b-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="b028b-128">Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="b028b-129">tooimport hello zestawu SDK modułu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="b028b-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="b028b-130">Załóżmy, że kompilacji i pakietu aplikacji o nazwie *MyApplication* w programie Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b028b-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="b028b-131">Domyślnie nazwa typu aplikacji hello wymienione w pliku ApplicationManifest.xml hello jest "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="b028b-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="b028b-132">Witaj pakiet aplikacji, który zawiera manifest aplikacji konieczne hello, manifestów usługi i pakietów kodu/config/danych, znajduje się w *C:\Users\<username\>\Documents\Visual 2015\Projects\ w Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="b028b-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="b028b-133">Witaj następujące polecenie wyświetla listę hello zawartości pakietu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b028b-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="b028b-134">Jeśli pakiet aplikacji hello jest duży i/lub ma wiele plików, możesz [skompresować je](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="b028b-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="b028b-135">Witaj Kompresja zmniejsza rozmiar hello i hello liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="b028b-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="b028b-136">Witaj efektem ubocznym jest tym hello rejestrowania i wyrejestrowywania typ aplikacji są szybsze.</span><span class="sxs-lookup"><span data-stu-id="b028b-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="b028b-137">Czas przekazywania aktualnie może być mniejsza, zwłaszcza, Jeśli dołączysz hello czasu toocompress hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="b028b-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="b028b-138">toocompress pakiet, użyj hello sam [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="b028b-139">Kompresja może odbywać się oddzielne przesyłaniu, za pomocą hello `SkipCopy` flaga lub wraz z hello Przekaż operacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="b028b-140">Stosowanie kompresji na skompresowanym pakietem jest pusta.</span><span class="sxs-lookup"><span data-stu-id="b028b-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="b028b-141">toouncompress skompresowany pakiet, użyj hello sam [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) z hello `UncompressPackage` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="b028b-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="b028b-142">Witaj następującego polecenia cmdlet kompresuje pakietu hello bez go kopiować toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="b028b-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="b028b-143">Pakiet HELLO zawiera teraz pliki zip hello `Code` i `Config` pakietów.</span><span class="sxs-lookup"><span data-stu-id="b028b-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="b028b-144">Witaj aplikacji i manifestów usługi hello są nie zip, ponieważ są potrzebne do wielu operacji wewnętrznych (takie jak udostępnianie aplikacji wyodrębniania nazwy i wersji typu dla niektórych operacji sprawdzania poprawności pakietu).</span><span class="sxs-lookup"><span data-stu-id="b028b-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="b028b-145">Kompresja manifestów hello spowodowałoby te operacje, nieefektywne.</span><span class="sxs-lookup"><span data-stu-id="b028b-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="b028b-146">Dla dużych pakietów aplikacji kompresji hello jest czasochłonne.</span><span class="sxs-lookup"><span data-stu-id="b028b-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="b028b-147">Aby uzyskać najlepsze rezultaty należy użyć szybkiego dysk SSD.</span><span class="sxs-lookup"><span data-stu-id="b028b-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="b028b-148">czasy kompresji Hello i rozmiar hello hello skompresowanym pakietem również się różnić w zależności na powitania zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="b028b-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="b028b-149">Na przykład w tym miejscu jest statystyki kompresji niektórych pakietów, które Pokaż hello początkowej i hello rozmiar skompresowany pakiet z czasem kompresji hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="b028b-150">Początkowy rozmiar (MB)</span><span class="sxs-lookup"><span data-stu-id="b028b-150">Initial size (MB)</span></span>|<span data-ttu-id="b028b-151">Liczba plików</span><span class="sxs-lookup"><span data-stu-id="b028b-151">File count</span></span>|<span data-ttu-id="b028b-152">Czas kompresji</span><span class="sxs-lookup"><span data-stu-id="b028b-152">Compression Time</span></span>|<span data-ttu-id="b028b-153">Skompresowany pakiet rozmiar (MB)</span><span class="sxs-lookup"><span data-stu-id="b028b-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="b028b-154">100</span><span class="sxs-lookup"><span data-stu-id="b028b-154">100</span></span>|<span data-ttu-id="b028b-155">100</span><span class="sxs-lookup"><span data-stu-id="b028b-155">100</span></span>|<span data-ttu-id="b028b-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="b028b-156">00:00:03.3547592</span></span>|<span data-ttu-id="b028b-157">60</span><span class="sxs-lookup"><span data-stu-id="b028b-157">60</span></span>|
|<span data-ttu-id="b028b-158">512</span><span class="sxs-lookup"><span data-stu-id="b028b-158">512</span></span>|<span data-ttu-id="b028b-159">100</span><span class="sxs-lookup"><span data-stu-id="b028b-159">100</span></span>|<span data-ttu-id="b028b-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="b028b-160">00:00:16.3850303</span></span>|<span data-ttu-id="b028b-161">307</span><span class="sxs-lookup"><span data-stu-id="b028b-161">307</span></span>|
|<span data-ttu-id="b028b-162">1024</span><span class="sxs-lookup"><span data-stu-id="b028b-162">1024</span></span>|<span data-ttu-id="b028b-163">500</span><span class="sxs-lookup"><span data-stu-id="b028b-163">500</span></span>|<span data-ttu-id="b028b-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="b028b-164">00:00:32.5907950</span></span>|<span data-ttu-id="b028b-165">615</span><span class="sxs-lookup"><span data-stu-id="b028b-165">615</span></span>|
|<span data-ttu-id="b028b-166">2048</span><span class="sxs-lookup"><span data-stu-id="b028b-166">2048</span></span>|<span data-ttu-id="b028b-167">1000</span><span class="sxs-lookup"><span data-stu-id="b028b-167">1000</span></span>|<span data-ttu-id="b028b-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="b028b-168">00:01:04.3775554</span></span>|<span data-ttu-id="b028b-169">1231</span><span class="sxs-lookup"><span data-stu-id="b028b-169">1231</span></span>|
|<span data-ttu-id="b028b-170">5012</span><span class="sxs-lookup"><span data-stu-id="b028b-170">5012</span></span>|<span data-ttu-id="b028b-171">100</span><span class="sxs-lookup"><span data-stu-id="b028b-171">100</span></span>|<span data-ttu-id="b028b-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="b028b-172">00:02:45.2951288</span></span>|<span data-ttu-id="b028b-173">3074</span><span class="sxs-lookup"><span data-stu-id="b028b-173">3074</span></span>|

<span data-ttu-id="b028b-174">Gdy pakiet jest skompresowana, może być przekazana tooone lub sieci szkieletowej usług wielu klastrów zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b028b-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="b028b-175">mechanizm wdrażania Hello jest takie samo skompresowanym i nieskompresowanym pakietów.</span><span class="sxs-lookup"><span data-stu-id="b028b-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="b028b-176">Jeśli pakiet hello jest skompresowany, są przechowywane jako takie magazynu obrazu klastra hello i przed uruchomieniem aplikacji hello jest dekompresowane w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="b028b-177">Witaj poniższy przykład przekazuje hello magazynu obrazów toohello pakietu, do folderu o nazwie "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="b028b-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="b028b-178">Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="b028b-179">tooimport hello zestawu SDK modułu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="b028b-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="b028b-180">Jeśli nie określisz hello *- ApplicationPackagePathInImageStore* parametru, pakiet aplikacji hello jest kopiowany do folderu "Debug" hello w magazynie obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="b028b-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="b028b-181">Hello czas tooupload pakiet zależy od wielu czynników.</span><span class="sxs-lookup"><span data-stu-id="b028b-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="b028b-182">Niektóre z nich są hello liczba plików w hello pakietu, rozmiar pakietu hello i hello rozmiary plików.</span><span class="sxs-lookup"><span data-stu-id="b028b-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="b028b-183">szybkość sieci Hello między maszyną źródłową hello i hello klastra sieci szkieletowej usług ma wpływ również na czas przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="b028b-184">Witaj domyślny limit czasu dla [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) to 30 minut.</span><span class="sxs-lookup"><span data-stu-id="b028b-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="b028b-185">W zależności od hello opisane czynników, może być tooincrease hello przekroczenia limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="b028b-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="b028b-186">Jeśli są kompresowania hello pakietu w wywołaniu kopiowania hello, musisz tooalso należy wziąć pod uwagę czas kompresji hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="b028b-187">Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="b028b-188">Pakiet aplikacji hello rejestru</span><span class="sxs-lookup"><span data-stu-id="b028b-188">Register hello application package</span></span>
<span data-ttu-id="b028b-189">Witaj typ i wersja aplikacji zadeklarowane w manifeście aplikacji hello staną się dostępne po zarejestrowaniu pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="b028b-190">Hello system odczytuje przesłany w poprzednim kroku hello pakiet hello, sprawdza, czy pakiet hello przetwarza hello zawartość pakietu i kopiuje hello przetworzyć pakietu tooan wewnętrznego systemu lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="b028b-191">Uruchom hello [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister polecenia cmdlet hello typu aplikacji w klastrze hello i udostępnienie jej do wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="b028b-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="b028b-192">"MyApplicationV1" jest hello folder, w którym znajduje się pakiet aplikacji hello magazynu obrazów hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="b028b-193">Typ aplikacji Hello o nazwie "MyApplicationType" i wersji "1.0.0", (zarówno znajdują się w manifeście aplikacji hello) teraz jest zarejestrowany w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="b028b-194">Witaj [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenie zwraca tylko wtedy, gdy hello system hello pomyślnie zarejestrowano pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="b028b-195">Jak długo trwa rejestracji zależy od rozmiaru hello i zawartości pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="b028b-196">W razie potrzeby hello **- TimeoutSec** parametr może być używane toosupply dłuższego limitu czasu (hello domyślny limit czasu wynosi 60 sekund).</span><span class="sxs-lookup"><span data-stu-id="b028b-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="b028b-197">Jeśli masz aplikację duży pakiet lub jeśli występują przekroczenia limitu czasu, użyj hello **- Async** parametru.</span><span class="sxs-lookup"><span data-stu-id="b028b-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="b028b-198">polecenie Hello zwraca po klastra hello akceptuje polecenia register hello i hello przetwarzanie będzie kontynuowane zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b028b-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="b028b-199">Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b028b-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="b028b-200">Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.</span><span class="sxs-lookup"><span data-stu-id="b028b-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="b028b-201">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b028b-201">Create hello application</span></span>
<span data-ttu-id="b028b-202">Można utworzyć wystąpienia aplikacji z dowolnej wersji typu aplikacji, który został pomyślnie zarejestrowany za pomocą hello [ServiceFabricApplication nowy](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b028b-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b028b-203">nazwy poszczególnych aplikacji Hello musi rozpoczynać się od hello *"fabric:"* schemat i muszą być unikatowe dla każdego wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="b028b-204">Wszystkie usługi domyślne zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello są również tworzone.</span><span class="sxs-lookup"><span data-stu-id="b028b-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="b028b-205">Dla dowolnej wersji danego typu zarejestrowanej aplikacji można tworzyć wiele wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="b028b-206">Każde wystąpienie aplikacji jest uruchamiany w izolacji z katalogu roboczego i procesu.</span><span class="sxs-lookup"><span data-stu-id="b028b-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="b028b-207">toosee, który o nazwie aplikacje i usługi są uruchomione w klastrze hello, uruchom hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) i [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b028b-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="b028b-208">Usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b028b-208">Remove an application</span></span>
<span data-ttu-id="b028b-209">Gdy wystąpienie aplikacji nie jest już potrzebne, można trwale usunąć ją według nazwy przy użyciu hello [ServiceFabricApplication Usuń](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b028b-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b028b-210">[Usuń ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatycznie usuwa wszystkie usługi należące toohello aplikacji, jak również i stałe usunięcie wszystkich stan usługi.</span><span class="sxs-lookup"><span data-stu-id="b028b-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="b028b-211">Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b028b-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="b028b-212">Wyrejestrowywanie typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="b028b-212">Unregister an application type</span></span>
<span data-ttu-id="b028b-213">W przypadku konkretnej wersji typu aplikacji nie jest potrzebna, należy wyrejestrować typu aplikacji hello przy użyciu hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b028b-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b028b-214">Wyrejestrowanie nieużywane aplikacji typów wersjach miejsca do magazynowania używanych przez hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="b028b-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="b028b-215">Typ aplikacji można wyrejestrować tak długo, jak wystąpienia są tworzone na nim żadnych aplikacji, a nie do czasu aplikacji uaktualnień odwołuje się do niego.</span><span class="sxs-lookup"><span data-stu-id="b028b-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="b028b-216">Uruchom [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) typy aplikacji hello toosee obecnie zarejestrowany w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="b028b-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="b028b-217">Uruchom [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister określonych typów aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b028b-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="b028b-218">Usuwanie pakietu aplikacji ze sklepu obraz powitania</span><span class="sxs-lookup"><span data-stu-id="b028b-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="b028b-219">Gdy pakiet aplikacji nie jest potrzebna, należy ją usunąć z toofree magazynu obrazu hello zasobów systemowych.</span><span class="sxs-lookup"><span data-stu-id="b028b-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="b028b-220">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b028b-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="b028b-221">Element ImageStoreConnectionString wprowadza się ServiceFabricApplicationPackage kopiowania</span><span class="sxs-lookup"><span data-stu-id="b028b-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="b028b-222">środowisko zestawu SDK usług sieci szkieletowej Hello ma już hello jest poprawna, skonfigurować ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="b028b-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="b028b-223">A w razie potrzeby hello element ImageStoreConnectionString dla wszystkich poleceń powinny być zgodne wartość hello tego hello klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b028b-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="b028b-224">Hello element ImageStoreConnectionString można znaleźć w manifeście klastra hello pobrany przy użyciu hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) i polecenia Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="b028b-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="b028b-225">Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="b028b-226">tooimport hello zestawu SDK modułu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="b028b-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="b028b-227">Element ImageStoreConnectionString Hello zostanie znaleziony w manifeście klastra hello:</span><span class="sxs-lookup"><span data-stu-id="b028b-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="b028b-228">Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b028b-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="b028b-229">Wdrażanie pakietu dużych aplikacji</span><span class="sxs-lookup"><span data-stu-id="b028b-229">Deploy large application package</span></span>
<span data-ttu-id="b028b-230">Problem: [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) upłynie limit czasu dla pakietu aplikacji duże (kolejność GB).</span><span class="sxs-lookup"><span data-stu-id="b028b-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="b028b-231">Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="b028b-231">Try:</span></span>
- <span data-ttu-id="b028b-232">Określ większego limitu czasu dla [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenie z `TimeoutSec` parametru.</span><span class="sxs-lookup"><span data-stu-id="b028b-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="b028b-233">Domyślnie program hello limitu czasu wynosi 30 minut.</span><span class="sxs-lookup"><span data-stu-id="b028b-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="b028b-234">Sprawdź hello połączenie sieciowe między maszyną źródłową a klastra.</span><span class="sxs-lookup"><span data-stu-id="b028b-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="b028b-235">Jeśli hello połączenie jest powolne, rozważ użycie maszynę z lepszą połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b028b-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="b028b-236">Jeśli komputer kliencki hello w regionie innym niż klaster hello, należy rozważyć użycie komputerze klienckim w regionie bliżej lub tego samego jako klaster hello.</span><span class="sxs-lookup"><span data-stu-id="b028b-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="b028b-237">Sprawdź, czy osiągnięto ograniczania zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="b028b-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="b028b-238">Na przykład gdy hello obrazu magazyn jest skonfigurowany toouse azure magazynu, można ograniczenie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="b028b-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="b028b-239">Problem: Pakiet przekazywania została ukończona pomyślnie, ale [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) upłynie limit czasu. Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="b028b-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="b028b-240">[Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="b028b-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="b028b-241">Hello Kompresja zmniejsza rozmiar hello i wykonaj hello liczba plików, który z kolei ogranicza hello ilość ruchu sieciowego i działają w tej sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b028b-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="b028b-242">Operacja przekazywania Hello może przebiegać wolniej, (zwłaszcza, Jeśli dołączysz hello kompresji czasu), ale rejestrowania i wyrejestrowania typ aplikacji hello są szybsze.</span><span class="sxs-lookup"><span data-stu-id="b028b-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="b028b-243">Określ większego limitu czasu dla [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) z `TimeoutSec` parametru.</span><span class="sxs-lookup"><span data-stu-id="b028b-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="b028b-244">Określ `Async` przełączać [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b028b-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="b028b-245">polecenie Hello zwraca gdy klastra hello akceptuje polecenia hello i rejestracji hello typu aplikacji hello asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="b028b-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="b028b-246">Z tego powodu jest toospecify nie konieczności wyższe przekroczenia limitu czasu w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="b028b-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="b028b-247">Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b028b-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="b028b-248">Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.</span><span class="sxs-lookup"><span data-stu-id="b028b-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="b028b-249">Wdrażanie pakietu aplikacji z wielu plików</span><span class="sxs-lookup"><span data-stu-id="b028b-249">Deploy application package with many files</span></span>
<span data-ttu-id="b028b-250">Problem: [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) limitu czasu dla pakietu aplikacji z wielu plików (kolejność tysięcy).</span><span class="sxs-lookup"><span data-stu-id="b028b-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="b028b-251">Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="b028b-251">Try:</span></span>
- <span data-ttu-id="b028b-252">[Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="b028b-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="b028b-253">Kompresja Hello zmniejsza hello liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="b028b-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="b028b-254">Określ większego limitu czasu dla [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) z `TimeoutSec` parametru.</span><span class="sxs-lookup"><span data-stu-id="b028b-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="b028b-255">Określ `Async` przełączać [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b028b-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="b028b-256">polecenie Hello zwraca gdy klastra hello akceptuje polecenia hello i rejestracji hello typu aplikacji hello asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="b028b-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="b028b-257">Z tego powodu jest toospecify nie konieczności wyższe przekroczenia limitu czasu w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="b028b-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="b028b-258">Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b028b-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="b028b-259">Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.</span><span class="sxs-lookup"><span data-stu-id="b028b-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="b028b-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b028b-260">Next steps</span></span>
[<span data-ttu-id="b028b-261">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b028b-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="b028b-262">Wprowadzenie kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b028b-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="b028b-263">Diagnozowanie i rozwiązywanie problemów z usługą sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b028b-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="b028b-264">Model aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b028b-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
