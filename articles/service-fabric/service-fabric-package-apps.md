---
title: "aaaPackage aplikację usługi Azure Service Fabric | Dokumentacja firmy Microsoft"
description: "Jak toopackage aplikacji usługi Service Fabric, przed wdrożeniem tooa klastra."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="e650b-103">Pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="e650b-103">Package an application</span></span>
<span data-ttu-id="e650b-104">W tym artykule opisano sposób toopackage aplikacji usługi Service Fabric i przygotowania do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e650b-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="e650b-105">Układ pakietu</span><span class="sxs-lookup"><span data-stu-id="e650b-105">Package layout</span></span>
<span data-ttu-id="e650b-106">manifest aplikacji Hello, co najmniej jeden manifestów usługi i inne niezbędne pliki muszą być zorganizowane w układzie określonej dla wdrożenia do klastra usługi sieć szkieletowa pakiet.</span><span class="sxs-lookup"><span data-stu-id="e650b-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="e650b-107">manifesty przykład Hello w tym artykule wymagałoby toobe podzielone na powitania po strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="e650b-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="e650b-108">foldery Hello są nazywane toomatch hello **nazwa** atrybuty każdego odpowiadającego mu elementu.</span><span class="sxs-lookup"><span data-stu-id="e650b-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="e650b-109">Na przykład, jeśli hello manifestu usługi zawiera dwa pakiety kodu z nazwami hello **MyCodeA** i **MyCodeB**, a następnie dwa foldery z hello zawierałoby tych samych nazw hello niezbędne pliki binarne dla każdego kodu pakiet.</span><span class="sxs-lookup"><span data-stu-id="e650b-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="e650b-110">Użyj elementu SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="e650b-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="e650b-111">Typowe scenariusze korzystania **SetupEntryPoint** są, gdy potrzebujesz toorun pliku wykonywalnego przed uruchomieniem usługi hello lub należy tooperform operacji z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="e650b-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="e650b-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e650b-112">For example:</span></span>

* <span data-ttu-id="e650b-113">Konfigurowanie i Inicjowanie zmiennych środowiskowych, które hello potrzeb pliku wykonywalnego usługi.</span><span class="sxs-lookup"><span data-stu-id="e650b-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="e650b-114">Nie jest ograniczona tooonly pliki wykonywalne napisane przez modele programowania hello sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e650b-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="e650b-115">Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.</span><span class="sxs-lookup"><span data-stu-id="e650b-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="e650b-116">Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e650b-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="e650b-117">Aby uzyskać więcej informacji na temat tooconfigure hello **SetupEntryPoint**, zobacz [hello zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="e650b-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="e650b-118">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="e650b-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="e650b-119">Tworzenie pakietu przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e650b-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="e650b-120">Jeśli używasz programu Visual Studio 2015 toocreate aplikacji, można użyć hello pakietu tooautomatically polecenia utworzyć pakietu, który odpowiada układu hello opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="e650b-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="e650b-121">toocreate pakiet, kliknij prawym przyciskiem myszy projekt aplikacji hello w Eksploratorze rozwiązań i wybierz polecenie pakietu hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e650b-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Pakowanie aplikacji przy użyciu programu Visual Studio][vs-package-command]

<span data-ttu-id="e650b-123">Po zakończeniu tworzenia pakietów można znaleźć lokalizacji hello hello pakietu w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="e650b-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="e650b-124">krok pakietów Hello odbywa się automatycznie podczas wdrażania lub debugowania aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e650b-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="e650b-125">Tworzenie pakietu przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e650b-125">Build a package by command line</span></span>
<span data-ttu-id="e650b-126">Możliwe jest również możliwe tooprogrammatically pakietu przy użyciu aplikacji `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="e650b-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="e650b-127">Pod maską hello Visual Studio jest uruchomiony, dane wyjściowe hello jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="e650b-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="e650b-128">Pakiet hello testowy</span><span class="sxs-lookup"><span data-stu-id="e650b-128">Test hello package</span></span>
<span data-ttu-id="e650b-129">Struktura pakietu hello lokalnie za pomocą programu PowerShell można sprawdzić za pomocą hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e650b-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="e650b-130">To polecenie sprawdza dla manifest analizowania problemów i sprawdź wszystkie odwołania.</span><span class="sxs-lookup"><span data-stu-id="e650b-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="e650b-131">To polecenie weryfikuje tylko hello poprawności strukturalnych hello katalogów i plików w pakiecie hello.</span><span class="sxs-lookup"><span data-stu-id="e650b-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="e650b-132">Nie Sprawdź dowolne hello zawartość pakietu kodu lub danych poza sprawdzanie, czy wszystkie niezbędne pliki są obecne.</span><span class="sxs-lookup"><span data-stu-id="e650b-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="e650b-133">Ten błąd pokazuje tego hello *MySetup.bat* pliku, do którego odwołuje się hello manifestu usługi **SetupEntryPoint** brakuje hello pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="e650b-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="e650b-134">Po dodaniu hello brakujący plik przekazuje weryfikacji aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="e650b-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="e650b-135">Jeśli aplikacja ma [parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) zdefiniowane, można przekazać je w [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) do właściwego weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e650b-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="e650b-136">Jeśli znasz klastra hello wdrożonym aplikacji hello, zalecane jest przekazywane w hello `ImageStoreConnectionString` parametru.</span><span class="sxs-lookup"><span data-stu-id="e650b-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="e650b-137">W takim przypadku pakietów hello jest również weryfikacji względem poprzedniej wersji aplikacji hello już uruchomione w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="e650b-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="e650b-138">Na przykład weryfikacji hello może wykryć, czy pakiet z hello tej samej wersji, ale inną zawartość została już wdrożona.</span><span class="sxs-lookup"><span data-stu-id="e650b-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="e650b-139">Gdy aplikacja hello jest dostarczana poprawnie i pozytywnej weryfikacji, oceny na podstawie rozmiaru hello i hello liczbę plików, jeśli kompresji nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="e650b-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="e650b-140">Kompresuj pakietu</span><span class="sxs-lookup"><span data-stu-id="e650b-140">Compress a package</span></span>
<span data-ttu-id="e650b-141">Gdy pakiet jest duży lub ma wiele plików, można skompresować je szybciej wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e650b-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="e650b-142">Kompresja zmniejsza hello liczbę plików i hello rozmiar pakietu.</span><span class="sxs-lookup"><span data-stu-id="e650b-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="e650b-143">Dla pakietu aplikacji skompresowany [pakiet aplikacji hello przekazywanie](service-fabric-deploy-remove-applications.md#upload-the-application-package) może potrwać już porównaniu toouploading hello nieskompresowanych pakietu (Jeśli specjalnie czasu kompresji jest brana pod uwagę), ale [rejestrowanie](service-fabric-deploy-remove-applications.md#register-the-application-package) i [wyrejestrowanie typ aplikacji hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) są szybsze dla pakietu aplikacji skompresowane.</span><span class="sxs-lookup"><span data-stu-id="e650b-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="e650b-144">mechanizm wdrażania Hello jest takie samo skompresowanym i nieskompresowanym pakietów.</span><span class="sxs-lookup"><span data-stu-id="e650b-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="e650b-145">Jeśli pakiet hello jest skompresowany, są przechowywane jako takie magazynu obrazu klastra hello i przed uruchomieniem aplikacji hello jest dekompresowane w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="e650b-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="e650b-146">Kompresja Hello zastępuje hello skompresowanej wersji hello prawidłowy pakiet sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e650b-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="e650b-147">Hello folder muszą zezwalać na uprawnienia do zapisu.</span><span class="sxs-lookup"><span data-stu-id="e650b-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="e650b-148">Systemem kompresji już skompresowanym pakietem daje żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="e650b-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="e650b-149">Pakiet można skompresować, uruchamiając polecenie programu Powershell hello [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) z `CompressPackage` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="e650b-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="e650b-150">Można zdekompresować hello pakiet o hello same polecenia przy użyciu `UncompressPackage` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="e650b-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="e650b-151">Witaj następujące polecenie kompresuje pakietu hello bez go kopiować toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="e650b-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="e650b-152">Możesz skopiować tooone skompresowany pakiet lub więcej klastrów sieci szkieletowej usług, zgodnie z potrzebami, za pomocą [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) bez hello `SkipCopy` flagi.</span><span class="sxs-lookup"><span data-stu-id="e650b-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="e650b-153">Pakiet HELLO zawiera teraz pliki zip hello `code`, `config`, i `data` pakietów.</span><span class="sxs-lookup"><span data-stu-id="e650b-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="e650b-154">Witaj w manifeście aplikacji i manifestów usługi hello są nie zip, ponieważ są potrzebne do wielu operacji wewnętrznych (takie jak udostępnianie aplikacji wyodrębniania nazwy i wersji typu dla niektórych operacji sprawdzania poprawności pakietu).</span><span class="sxs-lookup"><span data-stu-id="e650b-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="e650b-155">Kompresja manifestów hello spowodowałoby te operacje, nieefektywne.</span><span class="sxs-lookup"><span data-stu-id="e650b-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="e650b-156">Alternatywnie można kompresować i skopiować hello pakietu z [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="e650b-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="e650b-157">Jeśli hello pakiet jest duży, podaj wystarczająco wysoka, limit czasu czas tooallow hello pakietu kompresję i hello przekazywania toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="e650b-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="e650b-158">Wewnętrznie Service Fabric oblicza sumy kontrolne dla pakietów aplikacji hello do weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e650b-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="e650b-159">Korzystając z kompresji, sum kontrolnych hello są obliczane na powitania zip wersje każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e650b-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="e650b-160">Jeśli skopiowane nieskompresowanych wersji pakietu aplikacji, i chcesz toouse kompresja hello tego samego pakietu, należy zmienić hello wersje hello `code`, `config`, i `data` pakiety tooavoid błąd sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="e650b-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="e650b-161">Jeśli pakietów hello uległy zmianie, a zmiana wersji hello, możesz użyć [różnic inicjowania obsługi administracyjnej](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="e650b-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="e650b-162">Po wybraniu tej opcji nie ma pakietu niezmienione hello zamiast niej odwołania z hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="e650b-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="e650b-163">Podobnie jeśli przekazać skompresowaną wersję pakietu hello i chcesz toouse nieskompresowanych pakietu, należy zaktualizować hello wersji tooavoid hello błąd sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="e650b-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="e650b-164">Hello pakietu jest teraz spakowane poprawnie zweryfikowane i skompresowane (w razie potrzeby), aby była gotowa do [wdrożenia](service-fabric-deploy-remove-applications.md) klastrów tooone lub więcej sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e650b-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="e650b-165">Kompresuj pakiety, w przypadku wdrażania przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e650b-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="e650b-166">Możesz wydać pakietów toocompress Visual Studio podczas wdrażania, dodając hello `CopyPackageParameters` tooyour elementu profilu publikowania i ustaw hello `CompressPackage` atrybutu zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="e650b-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="e650b-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e650b-167">Next steps</span></span>
<span data-ttu-id="e650b-168">[Wdrażanie i usunąć aplikacje] [ 10] w tym artykule opisano sposób wystąpień aplikacji toomanage PowerShell toouse</span><span class="sxs-lookup"><span data-stu-id="e650b-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="e650b-169">[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] w tym artykule opisano sposób tooconfigure parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="e650b-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="e650b-170">[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] w tym artykule opisano, jak toorun usług pod dostępu toorestrict zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e650b-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
