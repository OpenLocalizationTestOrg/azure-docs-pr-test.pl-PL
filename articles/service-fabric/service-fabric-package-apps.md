---
title: Pakiet Azure Service Fabric aplikacji | Dokumentacja firmy Microsoft
description: "Jak pakiet aplikacji usługi Service Fabric, przed wdrożeniem w klastrze."
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
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="03f9b-103">Pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="03f9b-103">Package an application</span></span>
<span data-ttu-id="03f9b-104">W tym artykule opisano sposób pakietu aplikacji usługi Service Fabric i przygotowania do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="03f9b-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="03f9b-105">Układ pakietu</span><span class="sxs-lookup"><span data-stu-id="03f9b-105">Package layout</span></span>
<span data-ttu-id="03f9b-106">Manifest aplikacji, co najmniej jeden manifestów usługi i inne pliki niezbędne pakietu muszą być zorganizowane w układzie określonej dla wdrożenia do klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="03f9b-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="03f9b-107">Przykład manifesty w tym artykule musi być podzielone na następującą strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="03f9b-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

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

<span data-ttu-id="03f9b-108">Foldery noszą nazwy odpowiadające **nazwa** atrybuty każdego odpowiadającego mu elementu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="03f9b-109">Na przykład, jeśli manifest usługi zawiera dwa pakiety kodu z nazwami **MyCodeA** i **MyCodeB**, a następnie dwa foldery z tymi samymi nazwami zawierałoby niezbędne pliki binarne dla każdego pakietu kodu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="03f9b-110">Użyj elementu SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="03f9b-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="03f9b-111">Typowe scenariusze korzystania **SetupEntryPoint** po należy uruchomić plik wykonywalny przed uruchomieniem usługi lub należy wykonać operację z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="03f9b-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="03f9b-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="03f9b-112">For example:</span></span>

* <span data-ttu-id="03f9b-113">Konfigurowanie i Inicjowanie zmiennych środowiskowych, które wymaga pliku wykonywalnego usługi.</span><span class="sxs-lookup"><span data-stu-id="03f9b-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="03f9b-114">Nie jest ograniczona do tylko pliki wykonywalne napisane przez modele programowania sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="03f9b-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="03f9b-115">Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.</span><span class="sxs-lookup"><span data-stu-id="03f9b-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="03f9b-116">Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="03f9b-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="03f9b-117">Aby uzyskać więcej informacji na temat konfigurowania **SetupEntryPoint**, zobacz [skonfigurować zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="03f9b-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="03f9b-118">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="03f9b-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="03f9b-119">Tworzenie pakietu przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03f9b-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="03f9b-120">Jeśli używasz programu Visual Studio 2015 do tworzenia aplikacji, służy polecenie pakietu do automatycznego tworzenia pakietu, który odpowiada układu opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="03f9b-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="03f9b-121">Aby utworzyć pakiet, kliknij prawym przyciskiem myszy projekt aplikacji w Eksploratorze rozwiązań i wybierz polecenie pakietu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="03f9b-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Pakowanie aplikacji przy użyciu programu Visual Studio][vs-package-command]

<span data-ttu-id="03f9b-123">Po zakończeniu tworzenia pakietów można znaleźć lokalizacji pakietu w **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="03f9b-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="03f9b-124">Krok pakowania odbywa się automatycznie podczas wdrażania lub debugowania aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03f9b-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="03f9b-125">Tworzenie pakietu przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="03f9b-125">Build a package by command line</span></span>
<span data-ttu-id="03f9b-126">Istnieje również możliwość spakować programowo przy użyciu aplikacji `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="03f9b-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="03f9b-127">Pod maską Visual Studio jest uruchomiony, dane wyjściowe jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="03f9b-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="03f9b-128">Testowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="03f9b-128">Test the package</span></span>
<span data-ttu-id="03f9b-129">Struktura pakietu lokalnie za pomocą programu PowerShell można sprawdzić za pomocą [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia.</span><span class="sxs-lookup"><span data-stu-id="03f9b-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="03f9b-130">To polecenie sprawdza dla manifest analizowania problemów i sprawdź wszystkie odwołania.</span><span class="sxs-lookup"><span data-stu-id="03f9b-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="03f9b-131">To polecenie weryfikuje tylko strukturalnych poprawność katalogów i plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="03f9b-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="03f9b-132">Nie Sprawdź dowolnej zawartości pakietu kodu lub danych poza sprawdzanie, czy wszystkie niezbędne pliki są obecne.</span><span class="sxs-lookup"><span data-stu-id="03f9b-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="03f9b-133">Ten błąd wskazuje, że *MySetup.bat* pliku, do którego odwołuje się manifestu usługi **SetupEntryPoint** brakuje pakietu kodu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="03f9b-134">Po dodaniu brakujący plik przekazuje weryfikacji aplikacji:</span><span class="sxs-lookup"><span data-stu-id="03f9b-134">After the missing file is added, the application verification passes:</span></span>

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

<span data-ttu-id="03f9b-135">Jeśli aplikacja ma [parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) zdefiniowane, można przekazać je w [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) do właściwego weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="03f9b-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="03f9b-136">Jeśli znasz klastra, gdzie aplikacja zostanie wdrożona, zalecane jest przekazywane w `ImageStoreConnectionString` parametru.</span><span class="sxs-lookup"><span data-stu-id="03f9b-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="03f9b-137">W takim przypadku pakiet również jest weryfikowany pod kątem poprzednie wersje aplikacji, które już są uruchomione w klastrze.</span><span class="sxs-lookup"><span data-stu-id="03f9b-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="03f9b-138">Na przykład walidacji może wykryć, czy pakiet o takiej samej wersji, ale inną zawartość została już wdrożona.</span><span class="sxs-lookup"><span data-stu-id="03f9b-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="03f9b-139">Gdy aplikacja jest poprawnie spakowany i pozytywnej weryfikacji, należy ocenić na podstawie rozmiaru i liczbę plików, jeśli kompresja nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="03f9b-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="03f9b-140">Kompresuj pakietu</span><span class="sxs-lookup"><span data-stu-id="03f9b-140">Compress a package</span></span>
<span data-ttu-id="03f9b-141">Gdy pakiet jest duży lub ma wiele plików, można skompresować je szybciej wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="03f9b-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="03f9b-142">Kompresja zmniejsza liczbę plików oraz rozmiar pakietu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="03f9b-143">Dla pakietu aplikacji skompresowany [przekazywanie pakietu aplikacji](service-fabric-deploy-remove-applications.md#upload-the-application-package) może trwać dłużej, w porównaniu do przekazywania nieskompresowanych pakietu (Jeśli specjalnie czasu kompresji jest brana pod uwagę), ale [rejestrowanie](service-fabric-deploy-remove-applications.md#register-the-application-package) i [wyrejestrowanie typ aplikacji](service-fabric-deploy-remove-applications.md#unregister-an-application-type) są szybsze dla pakietu aplikacji skompresowane.</span><span class="sxs-lookup"><span data-stu-id="03f9b-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="03f9b-144">Mechanizm wdrażania jest takie samo skompresowanym i nieskompresowanym pakietów.</span><span class="sxs-lookup"><span data-stu-id="03f9b-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="03f9b-145">Jeśli pakiet jest skompresowany, są przechowywane w związku z magazynu obrazu klastra i jest dekompresowane w węźle przed uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03f9b-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="03f9b-146">Kompresja zastępuje prawidłowy pakiet usługi sieć szkieletowa skompresowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="03f9b-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="03f9b-147">Folder muszą zezwalać na uprawnienia do zapisu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-147">The folder must allow write permissions.</span></span> <span data-ttu-id="03f9b-148">Systemem kompresji już skompresowanym pakietem daje żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="03f9b-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="03f9b-149">Pakiet można skompresować za pomocą polecenia programu Powershell [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) z `CompressPackage` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="03f9b-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="03f9b-150">Można zdekompresować pakietu z takimi samymi polecenia przy użyciu `UncompressPackage` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="03f9b-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="03f9b-151">Następujące polecenie kompresuje pakiet, bez kopiowania go do magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="03f9b-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="03f9b-152">Możesz skopiować skompresowany pakiet do co najmniej jeden klaster sieci szkieletowej usług, zgodnie z potrzebami, za pomocą [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) bez `SkipCopy` flagi.</span><span class="sxs-lookup"><span data-stu-id="03f9b-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="03f9b-153">Pakiet zawiera obecnie pliki zip `code`, `config`, i `data` pakietów.</span><span class="sxs-lookup"><span data-stu-id="03f9b-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="03f9b-154">Manifest aplikacji i manifestów usługi są nie zip, ponieważ są potrzebne do wielu operacji wewnętrznych (np. pakietu udostępniania, aplikacja nazwa i wersja wyodrębniania typu dla niektórych operacji sprawdzania poprawności).</span><span class="sxs-lookup"><span data-stu-id="03f9b-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="03f9b-155">Pakowanie manifesty spowodowałoby, te operacje nieefektywne.</span><span class="sxs-lookup"><span data-stu-id="03f9b-155">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="03f9b-156">Alternatywnie można kompresować i skopiować pakiet z [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="03f9b-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="03f9b-157">Jeśli pakiet jest duży, podaj wystarczająco duża limitu czasu należy przewidzieć czas kompresję pakietu i przekazywania do klastra.</span><span class="sxs-lookup"><span data-stu-id="03f9b-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="03f9b-158">Wewnętrznie Service Fabric oblicza sumy kontrolne dla pakietów aplikacji w celu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="03f9b-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="03f9b-159">Korzystając z kompresji, sum kontrolnych są obliczane w wersjach zip każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="03f9b-160">W przypadku kopiowania nieskompresowanych wersji pakietu aplikacji, i chcesz użyć kompresji dla tego samego pakietu, należy zmienić wersje `code`, `config`, i `data` pakietów, aby uniknąć błąd sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="03f9b-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="03f9b-161">Jeśli pakiety nie uległy zmianie, a zmiana wersji, można użyć [różnic inicjowania obsługi administracyjnej](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="03f9b-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="03f9b-162">Po wybraniu tej opcji nie dołączaj niezmienione pakietu zamiast niej odwołania z manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="03f9b-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="03f9b-163">Podobnie jeśli chcesz użyć pakietu nieskompresowanych przekazać skompresowaną wersję pakietu, musisz zaktualizować wersje, aby uniknąć błąd sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="03f9b-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="03f9b-164">Pakiet jest teraz spakowane poprawnie zweryfikowane i skompresowane (w razie potrzeby), aby była gotowa do [wdrożenia](service-fabric-deploy-remove-applications.md) do co najmniej jeden klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="03f9b-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="03f9b-165">Kompresuj pakiety, w przypadku wdrażania przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03f9b-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="03f9b-166">Możesz wydać Visual Studio, aby kompresować pakietów podczas wdrażania, dodając `CopyPackageParameters` elementu profil publikowania i ustaw `CompressPackage` atrybutu `true`.</span><span class="sxs-lookup"><span data-stu-id="03f9b-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="03f9b-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03f9b-167">Next steps</span></span>
<span data-ttu-id="03f9b-168">[Wdrażanie i usunąć aplikacje] [ 10] opisano, jak zarządzać wystąpień aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="03f9b-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="03f9b-169">[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] opisano sposób konfigurowania parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="03f9b-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="03f9b-170">[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] opisuje sposób uruchamiania usługi na podstawie zasad zabezpieczeń w celu ograniczenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="03f9b-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
