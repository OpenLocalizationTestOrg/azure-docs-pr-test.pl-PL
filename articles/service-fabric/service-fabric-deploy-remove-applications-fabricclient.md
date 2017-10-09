---
title: "aaaAzure wdrożenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Użyj hello toodeploy interfejsów API klienta fabricclient z rolą i usunąć aplikacje w sieci szkieletowej usług."
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
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="71ffc-103">Wdrażanie i usunąć aplikacje przy użyciu klienta fabricclient z rolą</span><span class="sxs-lookup"><span data-stu-id="71ffc-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71ffc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71ffc-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="71ffc-105">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71ffc-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="71ffc-106">Interfejsy API FabricClient</span><span class="sxs-lookup"><span data-stu-id="71ffc-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="71ffc-107">Raz [typu aplikacji zostały opakowane][10], jest ono gotowe do wdrożenia do klastra usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="71ffc-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="71ffc-108">Wdrożenie obejmuje hello następujące trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="71ffc-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="71ffc-109">Przekaż magazynu obrazów toohello pakietu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="71ffc-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="71ffc-110">Rejestracja typu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="71ffc-110">Register hello application type</span></span>
3. <span data-ttu-id="71ffc-111">Tworzenie wystąpienia aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="71ffc-111">Create hello application instance</span></span>

<span data-ttu-id="71ffc-112">Po wdrożeniu aplikacji i wystąpienie jest uruchomione w klastrze hello, można usunąć wystąpienia aplikacji hello i typem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71ffc-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="71ffc-113">Usuń toocompletely aplikacji z klastra hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="71ffc-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="71ffc-114">Usuń (lub usunąć) hello uruchomione wystąpienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="71ffc-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="71ffc-115">Wyrejestrowywanie typu aplikacji hello, jeśli nie są już potrzebne</span><span class="sxs-lookup"><span data-stu-id="71ffc-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="71ffc-116">Usuwanie pakietu aplikacji hello z magazynu obrazów hello</span><span class="sxs-lookup"><span data-stu-id="71ffc-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="71ffc-117">Jeśli używasz [programu Visual Studio umożliwiające wdrażanie i debugowanie aplikacji](service-fabric-publish-app-remote-cluster.md) na klaster lokalny rozwój hello wszystkich powyższych kroków obsługi automatycznie za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71ffc-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="71ffc-118">Skrypt ten znajduje się w hello *skryptów* folderu projekt aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="71ffc-119">Ten artykuł zawiera tła na tego skryptu czynności, aby można było wykonać hello operacji poza Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ffc-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="71ffc-120">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="71ffc-120">Connect toohello cluster</span></span>
<span data-ttu-id="71ffc-121">Łączenie przez utworzenie klastra toohello [klienta fabricclient z rolą](/dotnet/api/system.fabric.fabricclient) wystąpienia przed uruchomieniem dowolnych hello przykłady kodu w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="71ffc-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="71ffc-122">Przykłady łączącego tooa lokalnego klastra projektowego zdalnego klastra lub klastra zabezpieczone przy użyciu usługi Azure Active Directory, X509 certyfikatów lub usługi Active Directory systemu Windows, zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="71ffc-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="71ffc-123">tooconnect toohello lokalnego klastra projektowego, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="71ffc-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="71ffc-124">Przekaż pakiet aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="71ffc-124">Upload hello application package</span></span>
<span data-ttu-id="71ffc-125">Załóżmy, że kompilacji i pakietu aplikacji o nazwie *MyApplication* w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ffc-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="71ffc-126">Domyślnie nazwa typu aplikacji hello wymienione w pliku ApplicationManifest.xml hello jest "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="71ffc-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="71ffc-127">Witaj pakiet aplikacji, który zawiera manifest aplikacji konieczne hello, manifestów usługi i pakietów kodu/config/danych, znajduje się w *C:\Users\&lt; nazwa użytkownika&gt;\Documents\Visual 2017\Projects\ w Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="71ffc-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="71ffc-128">Przekazywanie pakietu aplikacji hello umieszcza je w lokalizacji, który jest dostępny dla hello wewnętrznych składników usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="71ffc-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="71ffc-129">Sieć szkieletowa usług sprawdza, czy pakiet aplikacji hello podczas rejestracji hello pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="71ffc-130">Jednak jeśli chcesz pakiet aplikacji hello tooverify lokalnie (tj. przed przekazaniem), użyj hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71ffc-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="71ffc-131">Witaj [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) magazynu obrazów klastra toohello pakietu aplikacji hello przekazuje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="71ffc-132">Jeśli pakiet aplikacji hello jest duży i/lub ma wiele plików, możesz [skompresować je](service-fabric-package-apps.md#compress-a-package) i skopiować go toohello magazynu obrazów przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71ffc-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="71ffc-133">Witaj Kompresja zmniejsza rozmiar hello i hello liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="71ffc-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="71ffc-134">Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="71ffc-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="71ffc-135">Pakiet aplikacji hello rejestru</span><span class="sxs-lookup"><span data-stu-id="71ffc-135">Register hello application package</span></span>
<span data-ttu-id="71ffc-136">Witaj typ i wersja aplikacji zadeklarowane w manifeście aplikacji hello staną się dostępne po zarejestrowaniu pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="71ffc-137">Hello system odczytuje przesłany w poprzednim kroku hello pakiet hello, sprawdza, czy pakiet hello przetwarza hello zawartość pakietu i kopiuje hello przetworzyć pakietu tooan wewnętrznego systemu lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="71ffc-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="71ffc-138">Witaj [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) rejestrów interfejsu API hello typu aplikacji w klastrze hello i udostępnienie jej do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="71ffc-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="71ffc-139">Witaj [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) interfejsu API zawiera informacje o wszystkich typów aplikacji pomyślnie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="71ffc-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="71ffc-140">Po zakończeniu rejestracji hello, można użyć tego toodetermine interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="71ffc-141">Utwórz wystąpienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="71ffc-141">Create an application instance</span></span>
<span data-ttu-id="71ffc-142">Można utworzyć wystąpienia aplikacji z dowolnego typu aplikacji, który został pomyślnie zarejestrowany za pomocą hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="71ffc-143">nazwy poszczególnych aplikacji Hello musi rozpoczynać się od hello *"fabric:"* schemat i muszą być unikatowe dla każdego wystąpienia aplikacji (w ramach klastra).</span><span class="sxs-lookup"><span data-stu-id="71ffc-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="71ffc-144">Wszystkie usługi domyślne zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello są również tworzone.</span><span class="sxs-lookup"><span data-stu-id="71ffc-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="71ffc-145">Dla dowolnej wersji danego typu zarejestrowanej aplikacji można tworzyć wiele wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71ffc-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="71ffc-146">Każde wystąpienie aplikacji jest uruchamiany w izolacji z katalogu roboczego i zestaw procesów.</span><span class="sxs-lookup"><span data-stu-id="71ffc-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="71ffc-147">toosee, który o nazwie aplikacje i usługi są uruchomione w klastrze hello, uruchom hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) i [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="71ffc-148">Utwórz wystąpienie usługi</span><span class="sxs-lookup"><span data-stu-id="71ffc-148">Create a service instance</span></span>
<span data-ttu-id="71ffc-149">Można utworzyć wystąpienia usługi z typem usługi przy użyciu hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="71ffc-150">Jeśli usługa hello jest zadeklarowany jako domyślna usługa w manifeście aplikacji hello, hello usługi jest utworzona podczas tworzenia wystąpienia klasy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="71ffc-151">Wywoływanie hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) interfejsu API usługi, który już jest utworzone zwróci wyjątek typu FabricException zawierający kod błędu z wartością FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="71ffc-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="71ffc-152">Usuń wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="71ffc-152">Remove a service instance</span></span>
<span data-ttu-id="71ffc-153">Jeśli wystąpienie usługi nie jest już potrzebne, można usunąć go z hello uruchomione wystąpienie aplikacji przez wywołanie hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="71ffc-154">Ta operacja jest nieodwracalna i nie można odzyskać stan usługi.</span><span class="sxs-lookup"><span data-stu-id="71ffc-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="71ffc-155">Usuwanie wystąpienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="71ffc-155">Remove an application instance</span></span>
<span data-ttu-id="71ffc-156">Gdy wystąpienie aplikacji nie jest już potrzebne, można trwale usunąć ją według nazwy przy użyciu hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="71ffc-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatycznie usuwa wszystkie usługi należące toohello aplikacji, jak również i stałe usunięcie wszystkich stan usługi.</span><span class="sxs-lookup"><span data-stu-id="71ffc-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="71ffc-158">Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71ffc-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="71ffc-159">Wyrejestrowywanie typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="71ffc-159">Unregister an application type</span></span>
<span data-ttu-id="71ffc-160">W przypadku konkretnej wersji typu aplikacji nie jest potrzebna, należy wyrejestrować tej konkretnej wersji typu aplikacji hello przy użyciu hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="71ffc-161">Wyrejestrowywanie nieużywane wersje aplikacji typów wersjach miejsca do magazynowania używanego przez hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="71ffc-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="71ffc-162">Wersja typu aplikacji można wyrejestrować tak długo, jak przy użyciu wersji tego typu aplikacji hello wystąpienia są tworzone żadne aplikacje i żadnych uaktualnień aplikacji oczekujących odwołują się do tej wersji typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="71ffc-163">Usuwanie pakietu aplikacji ze sklepu obraz powitania</span><span class="sxs-lookup"><span data-stu-id="71ffc-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="71ffc-164">Gdy pakiet aplikacji nie jest potrzebna, należy ją usunąć z toofree magazynu obrazu hello zasobów systemowych przy użyciu hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="71ffc-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="71ffc-165">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="71ffc-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="71ffc-166">Element ImageStoreConnectionString wprowadza się ServiceFabricApplicationPackage kopiowania</span><span class="sxs-lookup"><span data-stu-id="71ffc-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="71ffc-167">środowisko zestawu SDK usług sieci szkieletowej Hello ma już hello jest poprawna, skonfigurować ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="71ffc-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="71ffc-168">A w razie potrzeby hello element ImageStoreConnectionString dla wszystkich poleceń powinny być zgodne wartość hello tego hello klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="71ffc-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="71ffc-169">Hello element ImageStoreConnectionString można znaleźć w manifeście klastra hello pobrany przy użyciu hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) i polecenia Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="71ffc-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="71ffc-170">Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="71ffc-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="71ffc-171">tooimport hello zestawu SDK modułu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="71ffc-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="71ffc-172">Element ImageStoreConnectionString Hello zostanie znaleziony w manifeście klastra hello:</span><span class="sxs-lookup"><span data-stu-id="71ffc-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="71ffc-173">Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="71ffc-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="71ffc-174">Wdrażanie pakietu dużych aplikacji</span><span class="sxs-lookup"><span data-stu-id="71ffc-174">Deploy large application package</span></span>
<span data-ttu-id="71ffc-175">Problem: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) interfejsu API upłynie limit czasu dla pakietu aplikacji duże (kolejność GB).</span><span class="sxs-lookup"><span data-stu-id="71ffc-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="71ffc-176">Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="71ffc-176">Try:</span></span>
- <span data-ttu-id="71ffc-177">Określ większego limitu czasu dla [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) metody z `timeout` parametru.</span><span class="sxs-lookup"><span data-stu-id="71ffc-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="71ffc-178">Domyślnie program hello limitu czasu wynosi 30 minut.</span><span class="sxs-lookup"><span data-stu-id="71ffc-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="71ffc-179">Sprawdź hello połączenie sieciowe między maszyną źródłową a klastra.</span><span class="sxs-lookup"><span data-stu-id="71ffc-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="71ffc-180">Jeśli hello połączenie jest powolne, rozważ użycie maszynę z lepszą połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="71ffc-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="71ffc-181">Jeśli komputer kliencki hello w regionie innym niż klaster hello, należy rozważyć użycie komputerze klienckim w regionie bliżej lub tego samego jako klaster hello.</span><span class="sxs-lookup"><span data-stu-id="71ffc-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="71ffc-182">Sprawdź, czy osiągnięto ograniczania zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="71ffc-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="71ffc-183">Na przykład gdy hello obrazu magazyn jest skonfigurowany toouse azure magazynu, można ograniczenie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="71ffc-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="71ffc-184">Problem: Pakiet przekazywania została ukończona pomyślnie, ale [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) limitu czasu interfejsu API. Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="71ffc-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="71ffc-185">[Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="71ffc-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="71ffc-186">Hello Kompresja zmniejsza rozmiar hello i wykonaj hello liczba plików, który z kolei ogranicza hello ilość ruchu sieciowego i działają w tej sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="71ffc-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="71ffc-187">Operacja przekazywania Hello może przebiegać wolniej, (zwłaszcza, Jeśli dołączysz hello kompresji czasu), ale rejestrowania i wyrejestrowania typ aplikacji hello są szybsze.</span><span class="sxs-lookup"><span data-stu-id="71ffc-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="71ffc-188">Określ większego limitu czasu dla [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) interfejsu API za pomocą `timeout` parametru.</span><span class="sxs-lookup"><span data-stu-id="71ffc-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="71ffc-189">Wdrażanie pakietu aplikacji z wielu plików</span><span class="sxs-lookup"><span data-stu-id="71ffc-189">Deploy application package with many files</span></span>
<span data-ttu-id="71ffc-190">Problem: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) limitu czasu dla pakietu aplikacji z wielu plików (kolejność tysięcy).</span><span class="sxs-lookup"><span data-stu-id="71ffc-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="71ffc-191">Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="71ffc-191">Try:</span></span>
- <span data-ttu-id="71ffc-192">[Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="71ffc-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="71ffc-193">Kompresja Hello zmniejsza hello liczbę plików.</span><span class="sxs-lookup"><span data-stu-id="71ffc-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="71ffc-194">Określ większego limitu czasu dla [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) z `timeout` parametru.</span><span class="sxs-lookup"><span data-stu-id="71ffc-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="71ffc-195">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="71ffc-195">Code example</span></span>
<span data-ttu-id="71ffc-196">Hello poniższy przykład umożliwia skopiowanie obrazu sklepu z aplikacjami pakietu toohello, przepisy typ aplikacji hello, tworzy wystąpienie aplikacji, tworzy wystąpienie usługi, usuwa wystąpienie aplikacji hello, un przepisy typ aplikacji hello i Usuwa pakiet aplikacji hello z hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="71ffc-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="71ffc-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71ffc-197">Next steps</span></span>
[<span data-ttu-id="71ffc-198">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="71ffc-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="71ffc-199">Wprowadzenie kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="71ffc-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="71ffc-200">Diagnozowanie i rozwiązywanie problemów z usługą sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="71ffc-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="71ffc-201">Model aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="71ffc-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
