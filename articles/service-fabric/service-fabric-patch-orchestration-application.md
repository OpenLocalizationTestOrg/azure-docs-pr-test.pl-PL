---
title: "aaaAzure aplikacji aranżacji poprawki usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Tooautomate aplikacji działających w systemie stosowanie poprawek w klastrze usługi sieć szkieletowa usług."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="995b6-103">Poprawka systemu operacyjnego Windows hello w klastrze usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="995b6-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="995b6-104">Witaj poprawki aranżacji aplikacja jest aplikacji sieci szkieletowej usług Azure, która automatyzuje systemu operacyjnego stosowanie poprawek w klastrze usługi sieć szkieletowa usług Azure bez przestoju.</span><span class="sxs-lookup"><span data-stu-id="995b6-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="995b6-105">Aplikacja orchestration poprawki Hello zapewnia następujące hello:</span><span class="sxs-lookup"><span data-stu-id="995b6-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="995b6-106">**Instalacja aktualizacji automatycznych systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="995b6-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="995b6-107">Automatycznie pobierania i instalowania aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="995b6-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="995b6-108">Węzły klastra są ponownie uruchamiane zgodnie z potrzebami bez przestoju klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="995b6-109">**Typu cluster-aware integracji stosowanie poprawek i kondycji**.</span><span class="sxs-lookup"><span data-stu-id="995b6-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="995b6-110">Podczas stosowania aktualizacji, aplikacja orchestration poprawki hello monitoruje kondycję hello hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="995b6-111">Węzły klastra są uaktualnionego jeden węzeł lub domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="995b6-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="995b6-112">Jeśli kondycji hello klastra hello przestanie działać z powodu toohello proces stosowania poprawek, poprawki jest zatrzymany tooprevent obciążające hello problem.</span><span class="sxs-lookup"><span data-stu-id="995b6-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="995b6-113">Szczegóły wewnętrznych aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-113">Internal details of hello app</span></span>

<span data-ttu-id="995b6-114">Aplikacja orchestration poprawki Hello składa się z hello następujące składniki podrzędne:</span><span class="sxs-lookup"><span data-stu-id="995b6-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="995b6-115">**Usługa koordynatora**: tej usługi stanowej jest odpowiedzialny za:</span><span class="sxs-lookup"><span data-stu-id="995b6-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="995b6-116">Koordynowanie zadanie aktualizacji systemu Windows hello na powitania całego klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="995b6-117">Przechowywanie wyniku hello ukończone operacje usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="995b6-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="995b6-118">**Usługa agenta węzła**: tej usługi bezstanowej działa we wszystkich węzłach klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="995b6-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="995b6-119">Witaj, usługa jest odpowiedzialna za:</span><span class="sxs-lookup"><span data-stu-id="995b6-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="995b6-120">Uruchamianie hello NTService agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="995b6-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="995b6-121">Monitorowanie hello NTService agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="995b6-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="995b6-122">**Węzeł agenta NTService**: Usługa ta systemu Windows NT jest uruchamiana na wyższym poziomie uprawnień (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="995b6-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="995b6-123">Z kolei hello Usługa agenta węzła i hello koordynatorem działać na niższym poziomie uprawnienia (Usługa sieciowa).</span><span class="sxs-lookup"><span data-stu-id="995b6-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="995b6-124">Usługa Hello jest wykonuje następujące zadania usługi Windows Update na wszystkich węzłach klastra hello hello:</span><span class="sxs-lookup"><span data-stu-id="995b6-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="995b6-125">Wyłączanie automatycznej aktualizacji systemu Windows w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="995b6-126">Zgodnie z toohello zasad hello użytkownik udostępnił pobieranie i instalowanie aktualizacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="995b6-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="995b6-127">Ponowne uruchamianie hello maszyny po instalacji usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="995b6-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="995b6-128">Przekazywanie hello wyniki toohello aktualizacje systemu Windows usługi koordynatora.</span><span class="sxs-lookup"><span data-stu-id="995b6-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="995b6-129">Raporty dotyczące raportowania kondycji, w przypadku, gdy operacja nie powiodła się po wykorzystaniu ponawiania prób.</span><span class="sxs-lookup"><span data-stu-id="995b6-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="995b6-130">Hello poprawki aranżacji aplikacja używa hello sieci szkieletowej usług naprawy Menedżera systemu usługi toodisable lub Włącz hello węzła i sprawdzania kondycji.</span><span class="sxs-lookup"><span data-stu-id="995b6-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="995b6-131">zadanie naprawy Hello utworzone przez hello poprawki aranżacji aplikacja ścieżki hello postęp aktualizacji systemu Windows dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="995b6-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="995b6-132">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="995b6-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="995b6-133">Minimalna obsługiwana wersja środowiska uruchomieniowego platformy Service Fabric</span><span class="sxs-lookup"><span data-stu-id="995b6-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="995b6-134">Klastry platformy Azure</span><span class="sxs-lookup"><span data-stu-id="995b6-134">Azure clusters</span></span>
<span data-ttu-id="995b6-135">Witaj poprawki aranżacji aplikacji musi być uruchamiane na Azure klastrów, które mają wersji środowiska uruchomieniowego platformy Service Fabric w wersji 5.5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="995b6-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="995b6-136">Autonomiczny lokalnymi klastrów</span><span class="sxs-lookup"><span data-stu-id="995b6-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="995b6-137">Witaj poprawki aranżacji aplikacji musi być uruchamiane na autonomicznych klastrów się v5.6 wersji środowiska uruchomieniowego platformy Service Fabric lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="995b6-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="995b6-138">Włącz usługę Menedżer naprawy hello (Jeśli nie jest już uruchomiona)</span><span class="sxs-lookup"><span data-stu-id="995b6-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="995b6-139">Witaj poprawki aranżacji aplikacja wymaga hello naprawy Menedżera systemu usługi toobe włączona w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="995b6-140">Klastry platformy Azure</span><span class="sxs-lookup"><span data-stu-id="995b6-140">Azure clusters</span></span>

<span data-ttu-id="995b6-141">Azure klastrów w warstwie srebrny trwałości hello ma hello napraw program service manager domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="995b6-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="995b6-142">Azure klastrów w warstwie gold trwałości hello może lub nie mieć hello naprawy Menedżera usługi w zależności od tego, kiedy te klastry zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="995b6-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="995b6-143">Azure klastrów w warstwie brązową trwałości hello, domyślnie nie mają hello napraw włączona usługa menedżera.</span><span class="sxs-lookup"><span data-stu-id="995b6-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="995b6-144">Jeśli usługa hello jest już włączony, widoczny będzie działać w sekcji usług systemu hello hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="995b6-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="995b6-145">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="995b6-145">Azure portal</span></span>
<span data-ttu-id="995b6-146">Napraw manager z portalu Azure można włączyć w czasie hello konfigurowania klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="995b6-147">Wybierz `Include Repair Manager` opcję w obszarze `Add on features` w czasie hello konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="995b6-148">![Obraz Menedżera naprawy włączenie z portalu Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="995b6-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="995b6-149">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="995b6-149">Azure Resource Manager template</span></span>
<span data-ttu-id="995b6-150">Możesz też użyć hello [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello naprawy Menedżera usługi na nowych i istniejących klastrów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="995b6-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="995b6-151">Pobierz szablon hello hello klastra, które mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="995b6-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="995b6-152">Można użyć hello przykładowych szablonów lub utworzyć niestandardowy szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="995b6-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="995b6-153">tooenable hello naprawy Menedżera usługi przy użyciu [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="995b6-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="995b6-154">Najpierw sprawdź, że hello `apiversion` ustawiono zbyt`2017-07-01-preview` dla hello `Microsoft.ServiceFabric/clusters` zasobów, jak pokazano w hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="995b6-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="995b6-155">Jeśli jest inny, a następnie należy tooupdate hello `apiVersion` toohello wartość `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="995b6-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="995b6-156">Teraz włączyć hello naprawy Menedżera usługi, dodając następujące hello `addonFeatures` sekcji po hello `fabricSettings` sekcji:</span><span class="sxs-lookup"><span data-stu-id="995b6-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="995b6-157">Po zaktualizowaniu szablonu klastra wprowadzone zmiany ich zastosowania i umożliwić zakończenie uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="995b6-158">Możesz teraz przeglądać hello naprawy Menedżera systemu usługa jest uruchomiona w klastrze.</span><span class="sxs-lookup"><span data-stu-id="995b6-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="995b6-159">Jest to `fabric:/System/RepairManagerService` w sekcji usług systemu hello hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="995b6-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="995b6-160">Autonomiczny lokalnymi klastrów</span><span class="sxs-lookup"><span data-stu-id="995b6-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="995b6-161">Można użyć hello [ustawienia konfiguracji dla klastra systemu Windows autonomiczny](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello naprawy Menedżera usługi na nowych i istniejących klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="995b6-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="995b6-162">Usługa Menedżera naprawy hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="995b6-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="995b6-163">Najpierw sprawdź, że hello `apiversion` w [konfiguracje klastrów ogólne](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) ustawiono zbyt`04-2017` lub nowszy:</span><span class="sxs-lookup"><span data-stu-id="995b6-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="995b6-164">Teraz włączyć naprawy Menedżera usługi, dodając następujące hello `addonFeaturres` sekcji po hello `fabricSettings` sekcji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="995b6-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="995b6-165">Zaktualizuj manifeście klastra za pomocą tych zmian, za pomocą hello zaktualizować manifestu klastra [Utwórz nowy klaster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) lub [konfiguracji klastra hello uaktualnienia](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="995b6-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="995b6-166">Po hello klastra został uruchomiony z manifestu klastra zaktualizowane, można przeglądać hello naprawy Menedżera systemu usługa jest uruchomiona w klastrze, która jest wywoływana `fabric:/System/RepairManagerService`w obszarze części hello Eksploratora usługi sieć szkieletowa usług systemowych.</span><span class="sxs-lookup"><span data-stu-id="995b6-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="995b6-167">Wyłącz automatyczną aktualizację systemu Windows na wszystkich węzłach</span><span class="sxs-lookup"><span data-stu-id="995b6-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="995b6-168">Aktualizacje automatyczne systemu Windows może prowadzić utraty tooavailability, ponieważ wiele węzłów klastra można ponownie uruchomić na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="995b6-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="995b6-169">Aplikacja orchestration poprawki Hello, domyślnie toodisable prób hello automatycznej aktualizacji systemu Windows w każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="995b6-170">Jednak jeśli hello ustawienia są zarządzane przez administratora lub zasad grupy, zaleca się ustawienie hello zasad zbyt "powiadamiania przed pobraniem" jawnie usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="995b6-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="995b6-171">Opcjonalnie: Włącz diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="995b6-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="995b6-172">Klastry z systemem wersja środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i loguje się powyżej Dzienniki aplikacji aranżacji zbieranie poprawki w ramach sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="995b6-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="995b6-173">Ten krok można pominąć, jeśli klaster jest uruchomiony na wersji środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i powyżej.</span><span class="sxs-lookup"><span data-stu-id="995b6-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="995b6-174">W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki aplikacji aranżacji poprawki hello są gromadzone lokalnie na każdym z węzłów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="995b6-175">Zaleca się skonfigurowanie diagnostyki Azure dzienniki tooupload wszystkie węzły tooa centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="995b6-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="995b6-176">Aby uzyskać informacje na temat włączania diagnostyki Azure, zobacz [zbierania dzienników przy użyciu diagnostyki Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="995b6-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="995b6-177">Dzienniki hello poprawki aranżacji aplikacji są generowane na powitania po stałej dostawcy identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="995b6-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="995b6-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="995b6-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="995b6-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="995b6-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="995b6-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="995b6-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="995b6-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="995b6-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="995b6-182">W instrukcji goto szablonu usługi Resource Manager `EtwEventSourceProviderConfiguration` w obszarze `WadCfg` i Dodaj hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="995b6-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="995b6-183">Jeśli klaster sieci szkieletowej usług ma wiele typów węzeł, a następnie hello w poprzedniej sekcji, należy dodać do wszystkich hello `WadCfg` sekcje.</span><span class="sxs-lookup"><span data-stu-id="995b6-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="995b6-184">Pobierz pakiet aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-184">Download hello app package</span></span>

<span data-ttu-id="995b6-185">Pobieranie aplikacji hello z hello [pobrać link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="995b6-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="995b6-186">Konfigurowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-186">Configure hello app</span></span>

<span data-ttu-id="995b6-187">Witaj zachowanie hello poprawki aranżacji aplikacji może być skonfigurowany toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="995b6-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="995b6-188">Zastąpić wartości domyślne hello przez przekazywanie parametrów aplikacji hello podczas tworzenia aplikacji lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="995b6-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="995b6-189">Można podać parametry aplikacji, określając `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` lub `New-ServiceFabricApplication` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="995b6-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="995b6-190">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="995b6-190">**Parameter**</span></span>        |<span data-ttu-id="995b6-191">**Typ**</span><span class="sxs-lookup"><span data-stu-id="995b6-191">**Type**</span></span>                          | <span data-ttu-id="995b6-192">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="995b6-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="995b6-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="995b6-193">MaxResultsToCache</span></span>    |<span data-ttu-id="995b6-194">Długie</span><span class="sxs-lookup"><span data-stu-id="995b6-194">Long</span></span>                              | <span data-ttu-id="995b6-195">Maksymalna liczba wyników aktualizacji systemu Windows, które mają być buforowane.</span><span class="sxs-lookup"><span data-stu-id="995b6-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="995b6-196">Wartość domyślna to 3000 zakładając, że:</span><span class="sxs-lookup"><span data-stu-id="995b6-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="995b6-197">-Liczba węzłów to 20.</span><span class="sxs-lookup"><span data-stu-id="995b6-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="995b6-198">-Liczba aktualizacji pojawia się w węźle miesięcznie wynosi pięć.</span><span class="sxs-lookup"><span data-stu-id="995b6-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="995b6-199">-Liczba wyników dla operacji może być 10.</span><span class="sxs-lookup"><span data-stu-id="995b6-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="995b6-200">— Powinny być przechowywane wyniki hello ostatnich trzech miesięcy.</span><span class="sxs-lookup"><span data-stu-id="995b6-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="995b6-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="995b6-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="995b6-202">wyliczenia</span><span class="sxs-lookup"><span data-stu-id="995b6-202">Enum</span></span> <br> <span data-ttu-id="995b6-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="995b6-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="995b6-204">TaskApprovalPolicy wskazuje hello zasady, które jest używane przez aktualizacje systemu Windows tooinstall koordynatorem hello na węzłach klastra usługi sieć szkieletowa hello toobe.</span><span class="sxs-lookup"><span data-stu-id="995b6-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="995b6-205">Dozwolone wartości to:</span><span class="sxs-lookup"><span data-stu-id="995b6-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="995b6-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="995b6-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="995b6-207">Windows Update jest zainstalowany jeden węzeł naraz.</span><span class="sxs-lookup"><span data-stu-id="995b6-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="995b6-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="995b6-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="995b6-209">Windows Update jest zainstalowanych domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="995b6-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="995b6-210">(Na powitania maksymalnej, dla usługi Windows Update można przejść wszystkie węzły hello należących do domeny uaktualnienia tooan).</span><span class="sxs-lookup"><span data-stu-id="995b6-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="995b6-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="995b6-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="995b6-212">Długie</span><span class="sxs-lookup"><span data-stu-id="995b6-212">Long</span></span>  <br> <span data-ttu-id="995b6-213">(Domyślnie: 1024)</span><span class="sxs-lookup"><span data-stu-id="995b6-213">(Default: 1024)</span></span>               |<span data-ttu-id="995b6-214">Maksymalny rozmiar poprawki aplikacji aranżacji loguje MB, co może trwale znajdować się lokalnie w węzłach.</span><span class="sxs-lookup"><span data-stu-id="995b6-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="995b6-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="995b6-215">WUQuery</span></span>               | <span data-ttu-id="995b6-216">Ciąg</span><span class="sxs-lookup"><span data-stu-id="995b6-216">string</span></span><br><span data-ttu-id="995b6-217">(Domyślnie: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="995b6-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="995b6-218">Zapytanie tooget aktualizacje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="995b6-218">Query tooget Windows updates.</span></span> <span data-ttu-id="995b6-219">Aby uzyskać więcej informacji, zobacz [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="995b6-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="995b6-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="995b6-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="995b6-221">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="995b6-221">Bool</span></span> <br> <span data-ttu-id="995b6-222">(domyślne: True)</span><span class="sxs-lookup"><span data-stu-id="995b6-222">(default: True)</span></span>                 | <span data-ttu-id="995b6-223">Ta flaga umożliwia system operacyjny zainstalowany toobe aktualizacje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="995b6-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="995b6-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="995b6-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="995b6-225">int</span><span class="sxs-lookup"><span data-stu-id="995b6-225">Int</span></span> <br><span data-ttu-id="995b6-226">(Domyślnie: 90).</span><span class="sxs-lookup"><span data-stu-id="995b6-226">(Default: 90)</span></span>                   | <span data-ttu-id="995b6-227">Określa limit czasu hello do żadnej operacji usługi Windows Update (wyszukiwania lub pobierania lub instalacji).</span><span class="sxs-lookup"><span data-stu-id="995b6-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="995b6-228">Jeśli operacja hello nie zostało ukończone w ciągu hello określony limit czasu, jest zostało przerwane.</span><span class="sxs-lookup"><span data-stu-id="995b6-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="995b6-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="995b6-229">WURescheduleCount</span></span>     | <span data-ttu-id="995b6-230">int</span><span class="sxs-lookup"><span data-stu-id="995b6-230">Int</span></span> <br> <span data-ttu-id="995b6-231">(Domyślne: 5).</span><span class="sxs-lookup"><span data-stu-id="995b6-231">(Default: 5)</span></span>                  | <span data-ttu-id="995b6-232">Hello maksymalną liczbę razy hello zmienia harmonogram hello usługi Windows update w przypadku, gdy operacja trwale kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="995b6-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="995b6-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="995b6-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="995b6-234">int</span><span class="sxs-lookup"><span data-stu-id="995b6-234">Int</span></span> <br><span data-ttu-id="995b6-235">(Domyślnie: 30).</span><span class="sxs-lookup"><span data-stu-id="995b6-235">(Default: 30)</span></span> | <span data-ttu-id="995b6-236">Interwał powitania, w których hello usługi zmienia harmonogram aktualizacji systemu Windows hello w przypadku, gdy błąd będzie się powtarzać.</span><span class="sxs-lookup"><span data-stu-id="995b6-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="995b6-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="995b6-237">WUFrequency</span></span>           | <span data-ttu-id="995b6-238">Ciąg rozdzielony przecinkami (domyślne: "Co tydzień, środę, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="995b6-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="995b6-239">częstotliwość Hello instalacji usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="995b6-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="995b6-240">Witaj format i możliwe wartości to:</span><span class="sxs-lookup"><span data-stu-id="995b6-240">hello format and possible values are:</span></span> <br><span data-ttu-id="995b6-241">— Co miesiąc, DD gg, na przykład, co miesiąc, 5, 12: 22:32.</span><span class="sxs-lookup"><span data-stu-id="995b6-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="995b6-242">— Gg co tydzień i dzień, na przykład, co tydzień, Wtorek, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="995b6-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="995b6-243">-Codziennie, ss, na przykład codziennie, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="995b6-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="995b6-244">-Wskazuje brak, nie można wykonać aktualizacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="995b6-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="995b6-245">Należy pamiętać, że cały czas hello są w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="995b6-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="995b6-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="995b6-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="995b6-247">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="995b6-247">Bool</span></span> <br><span data-ttu-id="995b6-248">(Domyślnie: true)</span><span class="sxs-lookup"><span data-stu-id="995b6-248">(Default: true)</span></span> | <span data-ttu-id="995b6-249">Ustawiając tę flagę aplikacji hello akceptuje hello użytkownika końcowego licencji umowy dla usługi Windows Update w imieniu właściciela hello hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="995b6-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="995b6-250">Jeśli chcesz od razu toohappen usługi Windows Update, ustaw `WUFrequency` czasu wdrożenia aplikacji toohello względną.</span><span class="sxs-lookup"><span data-stu-id="995b6-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="995b6-251">Na przykład załóżmy, że ma pięcioma węzłami klastra i plan toodeploy hello aplikacji testów przy około 17:00:00 czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="995b6-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="995b6-252">Jeśli założono, że wdrożenie lub uaktualniania aplikacji hello ma 30 minut w hello maksymalna, ustaw hello WUFrequency jako "Codziennie, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="995b6-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="995b6-253">Wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-253">Deploy hello app</span></span>

1. <span data-ttu-id="995b6-254">Zakończ wszystkie hello wstępnie wymagane kroki tooprepare hello klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="995b6-255">Wdróż hello poprawki aranżacji aplikacji, takich jak każda inna aplikacja usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="995b6-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="995b6-256">Aplikacja hello można wdrożyć przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="995b6-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="995b6-257">Wykonaj kroki hello w [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="995b6-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="995b6-258">tooconfigure aplikacji hello w czasie hello wdrożenia, hello przebiegu `ApplicationParamater` toohello `New-ServiceFabricApplication` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="995b6-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="995b6-259">Dla wygody przygotowaliśmy hello skryptu Deploy.ps1 wraz z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="995b6-260">skrypt hello toouse:</span><span class="sxs-lookup"><span data-stu-id="995b6-260">toouse hello script:</span></span>

    - <span data-ttu-id="995b6-261">Połącz klaster sieci szkieletowej usług tooa przy użyciu `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="995b6-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="995b6-262">Wykonanie skryptu PowerShell hello Deploy.ps1 hello odpowiednie `ApplicationParameter` wartość.</span><span class="sxs-lookup"><span data-stu-id="995b6-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="995b6-263">Utrzymaj hello hello skrypt i folder aplikacji hello PatchOrchestrationApplication tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="995b6-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="995b6-264">Uaktualnienie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-264">Upgrade hello app</span></span>

<span data-ttu-id="995b6-265">tooupgrade istniejącej aplikacji aranżacji poprawki przy użyciu programu PowerShell, wykonaj kroki hello w [uaktualniania aplikacji sieci szkieletowej usług za pomocą programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="995b6-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="995b6-266">Usuwanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-266">Remove hello app</span></span>

<span data-ttu-id="995b6-267">Aplikacja hello tooremove, wykonaj kroki hello w [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="995b6-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="995b6-268">Dla wygody przygotowaliśmy hello skryptu Undeploy.ps1 wraz z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="995b6-269">skrypt hello toouse:</span><span class="sxs-lookup"><span data-stu-id="995b6-269">toouse hello script:</span></span>

  - <span data-ttu-id="995b6-270">Połącz klaster sieci szkieletowej usług tooa przy użyciu ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="995b6-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="995b6-271">Uruchom skrypt programu PowerShell hello Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="995b6-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="995b6-272">Utrzymaj hello hello skrypt i folder aplikacji hello PatchOrchestrationApplication tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="995b6-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="995b6-273">Wyświetl wyniki aktualizacji systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="995b6-273">View hello Windows Update results</span></span>

<span data-ttu-id="995b6-274">Aplikacja orchestration poprawki Hello uwidacznia interfejsów API REST toodisplay hello historycznymi toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="995b6-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="995b6-275">Przykład Witaj wyniku JSON:</span><span class="sxs-lookup"><span data-stu-id="995b6-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="995b6-276">Jeśli aktualizacja nie jest jeszcze zaplanowane, wynik hello JSON jest pusta.</span><span class="sxs-lookup"><span data-stu-id="995b6-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="995b6-277">Zaloguj się za toohello tooquery klastra usługi Windows Update wyników.</span><span class="sxs-lookup"><span data-stu-id="995b6-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="995b6-278">Dowiedz się hello repliki adres podstawowy hello hello koordynatorem i trafień hello URL z przeglądarki hello: http://&lt;IP REPLIKI&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="995b6-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="995b6-279">punkt końcowy REST Hello hello koordynatorem ma portów dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="995b6-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="995b6-280">toocheck hello dokładny adres URL, zobacz toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="995b6-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="995b6-281">Na przykład wyniki hello są dostępne pod adresem `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="995b6-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Obraz końcowy REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="995b6-283">Hello zwrotnego serwera proxy jest włączona w klastrze hello, można uzyskać dostępu do adresu URL hello z poza również hello klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="995b6-284">Witaj punktu końcowego, który wymaga toobe trafień jest http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="995b6-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="995b6-285">tooenable hello zwrotnego serwera proxy na powitania klastra, wykonaj kroki hello w [odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="995b6-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="995b6-286">Po skonfigurowaniu hello zwrotnego serwera proxy, wszystkie usługi micro hello klastra, które ujawniać punkt końcowy HTTP adresowane z poza hello klastra.</span><span class="sxs-lookup"><span data-stu-id="995b6-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="995b6-287">Diagnostyka kondycji zdarzenia</span><span class="sxs-lookup"><span data-stu-id="995b6-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="995b6-288">Aplikacja orchestration poprawki zbieranie dzienników</span><span class="sxs-lookup"><span data-stu-id="995b6-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="995b6-289">Dzienniki aplikacji aranżacji poprawki są zbierane w ramach dzienników sieci szkieletowej usług z wersji środowiska uruchomieniowego `5.6.220.9494` i powyżej.</span><span class="sxs-lookup"><span data-stu-id="995b6-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="995b6-290">W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki mogą być zbierane przy użyciu jednej z następujących metod hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="995b6-291">Lokalnie na każdym węźle</span><span class="sxs-lookup"><span data-stu-id="995b6-291">Locally on each node</span></span>

<span data-ttu-id="995b6-292">Dzienniki są gromadzone lokalnie na każdym węźle klastra sieci szkieletowej usług w przypadku wersji środowiska uruchomieniowego usługi sieć szkieletowa usług mniej niż `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="995b6-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="995b6-293">Witaj dzienniki hello tooaccess lokalizacji jest \[sieci szkieletowej usług\_instalacji\_dysków\]:\\PatchOrchestrationApplication\\dzienniki.</span><span class="sxs-lookup"><span data-stu-id="995b6-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="995b6-294">Na przykład, jeśli usługa sieć szkieletowa jest zainstalowany na dysku D, ścieżka hello jest D:\\PatchOrchestrationApplication\\dzienniki.</span><span class="sxs-lookup"><span data-stu-id="995b6-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="995b6-295">Centralnej lokalizacji</span><span class="sxs-lookup"><span data-stu-id="995b6-295">Central location</span></span>

<span data-ttu-id="995b6-296">Jeśli diagnostyki Azure jest skonfigurowany jako część wstępnie wymagane kroki, dzienniki hello poprawki aranżacji aplikacji są dostępne w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="995b6-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="995b6-297">Raportów o kondycji</span><span class="sxs-lookup"><span data-stu-id="995b6-297">Health reports</span></span>

<span data-ttu-id="995b6-298">Aplikacja orchestration poprawki Hello publikuje również raportów o kondycji względem hello koordynatorem lub hello Usługa agenta węzła w hello w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="995b6-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="995b6-299">Operacja usługi Windows Update, nie powiodła się</span><span class="sxs-lookup"><span data-stu-id="995b6-299">A Windows Update operation failed</span></span>

<span data-ttu-id="995b6-300">W przypadku niepowodzenia operacji usługi Windows Update w węźle raport o kondycji jest generowany przed hello węzła usługi agenta.</span><span class="sxs-lookup"><span data-stu-id="995b6-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="995b6-301">Szczegóły hello raport o kondycji zawiera nazwy węzła problematyczne hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="995b6-302">Po pomyślnym węzła problematyczne hello zakończeniu stosowanie poprawek, raport hello są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="995b6-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="995b6-303">Witaj NTService agenta węzła nie działa</span><span class="sxs-lookup"><span data-stu-id="995b6-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="995b6-304">Jeśli hello NTService agenta węzeł nie działa w węźle, przed hello Usługa agenta węzła generowany jest raport o kondycji poziom ostrzeżeń.</span><span class="sxs-lookup"><span data-stu-id="995b6-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="995b6-305">Usługa Menedżera naprawy Hello nie jest włączona</span><span class="sxs-lookup"><span data-stu-id="995b6-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="995b6-306">Jeśli hello naprawy Menedżera usługi nie zostanie znaleziony w klastrze hello, zostanie wygenerowany raport dotyczący kondycji poziom ostrzeżeń hello usługę koordynatora.</span><span class="sxs-lookup"><span data-stu-id="995b6-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="995b6-307">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="995b6-307">Frequently asked questions</span></span>

<span data-ttu-id="995b6-308">Q.</span><span class="sxs-lookup"><span data-stu-id="995b6-308">Q.</span></span> <span data-ttu-id="995b6-309">**Dlaczego wyświetlać Mój klastra w stanie błędu, gdy aplikacja orchestration poprawki hello jest uruchomiona?**</span><span class="sxs-lookup"><span data-stu-id="995b6-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="995b6-310">A.</span><span class="sxs-lookup"><span data-stu-id="995b6-310">A.</span></span> <span data-ttu-id="995b6-311">W procesie instalacji hello aplikacja orchestration poprawki hello wyłącza lub ponownego uruchomienia węzłów, które mogą skutkować tymczasowo kondycji hello klastra hello przechodzi w dół.</span><span class="sxs-lookup"><span data-stu-id="995b6-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="995b6-312">Na podstawie hello zasad dla aplikacji hello, albo jeden węzeł może przejść w dół podczas operacji stosowania poprawek *lub* całej domeny uaktualnienia można przestaną działać jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="995b6-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="995b6-313">Końca hello hello instalacji usługi Windows Update powitalne węzły są reenabled po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="995b6-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="995b6-314">W hello poniższy przykład klaster hello zakończył się, że stan błędu tooan tymczasowo ponieważ dwa węzły zostały w dół i hello MaxPercentageUnhealthNodes zasad zostało naruszone.</span><span class="sxs-lookup"><span data-stu-id="995b6-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="995b6-315">Błąd Hello jest tymczasowy do momentu hello poprawki operacja jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="995b6-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Obraz zła klastra](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="995b6-317">Jeśli hello problem będzie się powtarzać, zapoznaj się toohello sekcji rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="995b6-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="995b6-318">Q.</span><span class="sxs-lookup"><span data-stu-id="995b6-318">Q.</span></span> <span data-ttu-id="995b6-319">**Aplikacja orchestration poprawki jest w stanie ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="995b6-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="995b6-320">A.</span><span class="sxs-lookup"><span data-stu-id="995b6-320">A.</span></span> <span data-ttu-id="995b6-321">Sprawdź toosee, jeśli raport o kondycji zaksięgowany względem aplikacji hello hello główną przyczynę.</span><span class="sxs-lookup"><span data-stu-id="995b6-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="995b6-322">Zazwyczaj ostrzeżenie hello zawiera szczegółowe informacje o problemie hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="995b6-323">W przypadku przejściowy problem hello aplikacji hello jest oczekiwany Odzyskaj tooauto z tego stanu.</span><span class="sxs-lookup"><span data-stu-id="995b6-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="995b6-324">Q.</span><span class="sxs-lookup"><span data-stu-id="995b6-324">Q.</span></span> <span data-ttu-id="995b6-325">**Co można zrobić, jeśli mojego klastra jest zła i toodo aktualizację pilnych systemu operacyjnego jest potrzebna?**</span><span class="sxs-lookup"><span data-stu-id="995b6-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="995b6-326">A.</span><span class="sxs-lookup"><span data-stu-id="995b6-326">A.</span></span> <span data-ttu-id="995b6-327">Aplikacja orchestration poprawki Hello nie można zainstalować aktualizacji podczas klastra hello jest zła.</span><span class="sxs-lookup"><span data-stu-id="995b6-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="995b6-328">Spróbuj toobring klastra tooa dobrej kondycji toounblock hello poprawki aranżacji aplikacji przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="995b6-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="995b6-329">Q.</span><span class="sxs-lookup"><span data-stu-id="995b6-329">Q.</span></span> <span data-ttu-id="995b6-330">**Dlaczego poprawki w klastrach podąża tak długo toorun?**</span><span class="sxs-lookup"><span data-stu-id="995b6-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="995b6-331">A.</span><span class="sxs-lookup"><span data-stu-id="995b6-331">A.</span></span> <span data-ttu-id="995b6-332">Hello czas potrzebny aplikacji aranżacji poprawki hello zależy przede wszystkim hello następujące czynniki:</span><span class="sxs-lookup"><span data-stu-id="995b6-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="995b6-333">zasady Hello hello usługę koordynatora.</span><span class="sxs-lookup"><span data-stu-id="995b6-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="995b6-334">Witaj domyślne zasady `NodeWise`, powoduje stosowanie poprawek tylko jeden węzeł naraz.</span><span class="sxs-lookup"><span data-stu-id="995b6-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="995b6-335">Szczególnie w przypadku hello większe klastry, zalecane jest użycie hello `UpgradeDomainWise` tooachieve zasad szybsze poprawki w klastrach.</span><span class="sxs-lookup"><span data-stu-id="995b6-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="995b6-336">Witaj liczba dostępnych do pobrania i zainstalowania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="995b6-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="995b6-337">Witaj toodownload Średni czas potrzebny i zainstalować aktualizację, który nie powinien przekraczać po kilku godzinach.</span><span class="sxs-lookup"><span data-stu-id="995b6-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="995b6-338">Witaj wydajności hello maszyny Wirtualnej i przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="995b6-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="995b6-339">Q.</span><span class="sxs-lookup"><span data-stu-id="995b6-339">Q.</span></span> <span data-ttu-id="995b6-340">**Dlaczego widzę niektórych aktualizacji w wynikach usługi Windows Update uzyskany za pośrednictwem interfejsu api REST, ale nie w ramach hello historii usługi Windows Update na komputerze?**</span><span class="sxs-lookup"><span data-stu-id="995b6-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="995b6-341">A.</span><span class="sxs-lookup"><span data-stu-id="995b6-341">A.</span></span> <span data-ttu-id="995b6-342">Niektóre aktualizacje produktu muszą toobe zaewidencjonowany historii odpowiednich aktualizacji/poprawki.</span><span class="sxs-lookup"><span data-stu-id="995b6-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="995b6-343">Przykład: Usługa Windows Defender aktualizacje nie są wyświetlane w historii usługi Windows Update w systemie Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="995b6-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="995b6-344">Zastrzeżenia</span><span class="sxs-lookup"><span data-stu-id="995b6-344">Disclaimers</span></span>

- <span data-ttu-id="995b6-345">Aplikacja orchestration poprawki Hello akceptuje hello użytkownika końcowego licencji umowy z usługi Windows Update w imieniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="995b6-346">Opcjonalnie ustawienie hello, można wyłączyć w konfiguracji hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="995b6-347">Aplikacja orchestration poprawki Hello zbiera dane telemetryczne tootrack użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="995b6-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="995b6-348">dane telemetryczne aplikacji Hello następuje ustawienie hello ustawienia telemetrii hello sieci szkieletowej usług runtime, (która jest domyślnie włączona).</span><span class="sxs-lookup"><span data-stu-id="995b6-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="995b6-349">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="995b6-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="995b6-350">Węzeł jest nie powracające tooup stanu</span><span class="sxs-lookup"><span data-stu-id="995b6-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="995b6-351">**węzeł Hello mogła zostać zablokowana na wyłączenie stanu, ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="995b6-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="995b6-352">Trwa oczekiwanie na sprawdzenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="995b6-352">A safety check is pending.</span></span> <span data-ttu-id="995b6-353">tooremedy tej sytuacji, upewnij się, że wystarczającej liczby węzłów są dostępne w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="995b6-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="995b6-354">**węzeł Hello mogła zostać zablokowana w stanie wyłączenia, ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="995b6-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="995b6-355">Witaj węzeł został wyłączony ręcznie.</span><span class="sxs-lookup"><span data-stu-id="995b6-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="995b6-356">węzeł Hello został wyłączony z powodu tooan zadania trwającą infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="995b6-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="995b6-357">węzeł Hello zostało wyłączone tymczasowo przez hello poprawki aranżacji aplikacji toopatch hello węzła.</span><span class="sxs-lookup"><span data-stu-id="995b6-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="995b6-358">**Hello węzeł może zostać zatrzymane w stanie down ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="995b6-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="995b6-359">węzeł Hello została umieszczona w stanie down ręcznie.</span><span class="sxs-lookup"><span data-stu-id="995b6-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="995b6-360">węzeł Hello jest w trakcie ponownego uruchomienia (które może zostać wyzwolone przez hello poprawki aranżacji aplikacji).</span><span class="sxs-lookup"><span data-stu-id="995b6-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="995b6-361">węzeł Hello jest wyłączony powodu tooa błędny maszyny Wirtualnej lub maszyny lub sieci problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="995b6-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="995b6-362">Aktualizacje zostały pominięte na niektóre węzły</span><span class="sxs-lookup"><span data-stu-id="995b6-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="995b6-363">Aplikacja orchestration poprawki Hello próbuje tooinstall zasad systemu Windows update zgodnie z toohello planowaniem mogą.</span><span class="sxs-lookup"><span data-stu-id="995b6-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="995b6-364">Usługa Hello próbuje toorecover hello węzła i Pomiń hello aktualizacji zgodnie z toohello aplikacji zasad.</span><span class="sxs-lookup"><span data-stu-id="995b6-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="995b6-365">W takim przypadku raport dotyczący kondycji poziom ostrzeżeń jest generowany przed hello węzła usługi agenta.</span><span class="sxs-lookup"><span data-stu-id="995b6-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="995b6-366">wynik Hello aktualizacji systemu Windows zawiera także hello możliwych przyczyn niepowodzenia hello.</span><span class="sxs-lookup"><span data-stu-id="995b6-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="995b6-367">kondycji Hello klastra hello przechodzi tooerror podczas instalacji aktualizacji hello</span><span class="sxs-lookup"><span data-stu-id="995b6-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="995b6-368">Błędny usługi Windows update można obniżyć hello kondycji aplikacji lub klastra w określonym węźle lub domena uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="995b6-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="995b6-369">Aplikacja orchestration poprawki Hello zaprzestaje wszelkie kolejne operacje usługi Windows Update, dopóki hello klastra jest w dobrej kondycji ponownie.</span><span class="sxs-lookup"><span data-stu-id="995b6-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="995b6-370">Administrator musi interweniować i ustalić, dlaczego aplikacja hello lub klastra stał się nieprawidłowy, ponieważ tooWindows aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="995b6-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="995b6-371">Informacje o wersji:</span><span class="sxs-lookup"><span data-stu-id="995b6-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="995b6-372">Wersja 1.1.0</span><span class="sxs-lookup"><span data-stu-id="995b6-372">Version 1.1.0</span></span>
- <span data-ttu-id="995b6-373">Publiczny zlecenia</span><span class="sxs-lookup"><span data-stu-id="995b6-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="995b6-374">Wersja 1.1.1</span><span class="sxs-lookup"><span data-stu-id="995b6-374">Version 1.1.1</span></span>
- <span data-ttu-id="995b6-375">Rozwiązane usterki w SetupEntryPoint z NodeAgentService uniemożliwiający instalacji NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="995b6-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="995b6-376">Wersji 1.2.0 (Najnowsza wersja)</span><span class="sxs-lookup"><span data-stu-id="995b6-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="995b6-377">Poprawki błędów wokół systemu ponownie uruchomić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="995b6-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="995b6-378">Poprawka błędu podczas tworzenia zadania RM powodu sprawdzenie kondycji toowhich podczas przygotowywania zadań naprawy nie pojawia się zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="995b6-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="995b6-379">Zmienione hello tryb uruchamiania usługi windows POANodeSvc z automatycznego toodelayed-auto.</span><span class="sxs-lookup"><span data-stu-id="995b6-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
