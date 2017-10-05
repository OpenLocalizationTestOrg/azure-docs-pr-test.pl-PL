---
title: "Azure Service Fabric poprawki aranżacji aplikacji | Dokumentacja firmy Microsoft"
description: "Aplikacja do automatyzacji w klastrze usługi sieć szkieletowa stosowanie poprawek systemu operacyjnego."
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="97bd3-103">Poprawka systemu operacyjnego Windows w klastrze usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="97bd3-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="97bd3-104">Aplikacja orchestration poprawki jest aplikacja sieć szkieletowa usług Azure, która automatyzuje systemu operacyjnego stosowanie poprawek w klastrze usługi sieć szkieletowa usług Azure bez przestoju.</span><span class="sxs-lookup"><span data-stu-id="97bd3-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="97bd3-105">Poprawka aplikacji aranżacji zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="97bd3-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="97bd3-106">**Instalacja aktualizacji automatycznych systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="97bd3-107">Automatycznie pobierania i instalowania aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="97bd3-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="97bd3-108">Węzły klastra są ponownie uruchamiane zgodnie z potrzebami bez przestoju klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="97bd3-109">**Typu cluster-aware integracji stosowanie poprawek i kondycji**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="97bd3-110">Podczas stosowania aktualizacji, aplikacja orchestration poprawki monitoruje kondycję węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="97bd3-111">Węzły klastra są uaktualnionego jeden węzeł lub domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="97bd3-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="97bd3-112">Jeśli kondycji klaster przestanie działać z powodu proces stosowania poprawek, poprawki jest zatrzymana, aby zapobiec obciążające problem.</span><span class="sxs-lookup"><span data-stu-id="97bd3-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="97bd3-113">Wewnętrzny szczegóły aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-113">Internal details of the app</span></span>

<span data-ttu-id="97bd3-114">Poprawka aplikacji orchestration składa się z następujących Podskładniki:</span><span class="sxs-lookup"><span data-stu-id="97bd3-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="97bd3-115">**Usługa koordynatora**: tej usługi stanowej jest odpowiedzialny za:</span><span class="sxs-lookup"><span data-stu-id="97bd3-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="97bd3-116">Koordynowanie zadania usługi Windows Update dla całego klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="97bd3-117">Przechowywanie wyniku ukończone operacje usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="97bd3-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="97bd3-118">**Usługa agenta węzła**: tej usługi bezstanowej działa we wszystkich węzłach klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="97bd3-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="97bd3-119">Usługa jest odpowiedzialna za:</span><span class="sxs-lookup"><span data-stu-id="97bd3-119">The service is responsible for:</span></span>
    - <span data-ttu-id="97bd3-120">Uruchamianie NTService agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="97bd3-121">Monitorowanie NTService agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="97bd3-122">**Węzeł agenta NTService**: Usługa ta systemu Windows NT jest uruchamiana na wyższym poziomie uprawnień (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="97bd3-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="97bd3-123">Z kolei usługę agenta węzła i usługę koordynatora działać na niższym poziomie uprawnienia (Usługa sieciowa).</span><span class="sxs-lookup"><span data-stu-id="97bd3-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="97bd3-124">Usługa jest odpowiedzialna za wykonywanie następujących zadań usługi Windows Update na wszystkich węzłach klastra:</span><span class="sxs-lookup"><span data-stu-id="97bd3-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="97bd3-125">Wyłączanie automatycznej aktualizacji systemu Windows w węźle.</span><span class="sxs-lookup"><span data-stu-id="97bd3-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="97bd3-126">Trwa pobieranie i instalowanie usługi Windows Update zgodnie z zasadami użytkownik udostępnił.</span><span class="sxs-lookup"><span data-stu-id="97bd3-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="97bd3-127">Ponowne uruchomienie komputera po instalacji usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="97bd3-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="97bd3-128">Przekazywanie wyniki aktualizacji systemu Windows z usługą koordynatora.</span><span class="sxs-lookup"><span data-stu-id="97bd3-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="97bd3-129">Raporty dotyczące raportowania kondycji, w przypadku, gdy operacja nie powiodła się po wykorzystaniu ponawiania prób.</span><span class="sxs-lookup"><span data-stu-id="97bd3-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="97bd3-130">Poprawki aplikacji orchestration korzysta z sieci szkieletowej usług naprawy Menedżera systemu usługi, aby wyłączyć lub włączyć węzeł i sprawdzania kondycji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="97bd3-131">Zadanie naprawy tworzonych przez aplikację aranżacji poprawki śledzi postęp procesu usługi Windows Update dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97bd3-132">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97bd3-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="97bd3-133">Minimalna obsługiwana wersja środowiska uruchomieniowego platformy Service Fabric</span><span class="sxs-lookup"><span data-stu-id="97bd3-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="97bd3-134">Klastry platformy Azure</span><span class="sxs-lookup"><span data-stu-id="97bd3-134">Azure clusters</span></span>
<span data-ttu-id="97bd3-135">Poprawka aplikacji aranżacji musi być uruchamiane na Azure klastrów, które mają wersji środowiska uruchomieniowego platformy Service Fabric w wersji 5.5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="97bd3-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="97bd3-136">Autonomiczny lokalnymi klastrów</span><span class="sxs-lookup"><span data-stu-id="97bd3-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="97bd3-137">Na autonomicznych klastrów się v5.6 wersji środowiska uruchomieniowego platformy Service Fabric musi być uruchomiona aplikacja orchestration poprawki lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="97bd3-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="97bd3-138">Włącz usługę Menedżer napraw (Jeśli nie jest już uruchomiona)</span><span class="sxs-lookup"><span data-stu-id="97bd3-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="97bd3-139">Aplikacja orchestration poprawki wymaga usługi repair Menedżera system zostać włączony w klastrze.</span><span class="sxs-lookup"><span data-stu-id="97bd3-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="97bd3-140">Klastry platformy Azure</span><span class="sxs-lookup"><span data-stu-id="97bd3-140">Azure clusters</span></span>

<span data-ttu-id="97bd3-141">Azure klastrów w warstwie srebrny trwałości ma usługę Menedżer naprawy domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="97bd3-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="97bd3-142">Azure klastrów w warstwie trwałości gold mogą lub nie mieć usługę Menedżer naprawy włączone, w zależności od tego, kiedy te klastry zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="97bd3-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="97bd3-143">Klastry platformy Azure w warstwie brązową trwałości, domyślnie nie być włączona usługa Menedżera naprawy.</span><span class="sxs-lookup"><span data-stu-id="97bd3-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="97bd3-144">Jeśli usługa jest już włączony, można to sprawdzić w sekcji system usługi Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="97bd3-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="97bd3-145">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="97bd3-145">Azure portal</span></span>
<span data-ttu-id="97bd3-146">Podczas konfigurowania klastra można włączyć naprawy menedżera z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97bd3-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="97bd3-147">Wybierz `Include Repair Manager` opcję w obszarze `Add on features` w czasie konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="97bd3-148">![Obraz Menedżera naprawy włączenie z portalu Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="97bd3-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="97bd3-149">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97bd3-149">Azure Resource Manager template</span></span>
<span data-ttu-id="97bd3-150">Możesz też użyć [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) Aby włączyć usługę Menedżer naprawy na nowych i istniejących klastrów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="97bd3-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="97bd3-151">Pobierz szablon dla klastra, który chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="97bd3-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="97bd3-152">Można korzystać z przykładowych szablonów lub utworzyć niestandardowy szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97bd3-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="97bd3-153">Aby włączyć naprawy Menedżera usługi przy użyciu [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="97bd3-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="97bd3-154">Najpierw sprawdź, czy `apiversion` ustawiono `2017-07-01-preview` dla `Microsoft.ServiceFabric/clusters` zasobów, jak pokazano w poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="97bd3-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="97bd3-155">Jeśli jest inny, musisz zaktualizować `apiVersion` wartość `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="97bd3-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="97bd3-156">Teraz Włącz usługę Menedżer naprawy przez dodanie poniższego `addonFeatures` sekcji po `fabricSettings` sekcji:</span><span class="sxs-lookup"><span data-stu-id="97bd3-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="97bd3-157">Po zaktualizowaniu szablonu klastra wprowadzone zmiany ich zastosowania i umożliwić zakończenie uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="97bd3-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="97bd3-158">Możesz teraz przeglądać usługi repair Menedżera system działające w klastrze.</span><span class="sxs-lookup"><span data-stu-id="97bd3-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="97bd3-159">Jest to `fabric:/System/RepairManagerService` w sekcji system usługi Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="97bd3-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="97bd3-160">Autonomiczny lokalnymi klastrów</span><span class="sxs-lookup"><span data-stu-id="97bd3-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="97bd3-161">Można użyć [ustawienia konfiguracji dla klastra systemu Windows autonomiczny](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) Aby włączyć usługę Menedżer naprawy na nowych i istniejących klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="97bd3-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="97bd3-162">Aby włączyć usługę Menedżer naprawy:</span><span class="sxs-lookup"><span data-stu-id="97bd3-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="97bd3-163">Najpierw sprawdź, czy `apiversion` w [konfiguracje klastrów ogólne](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) ma ustawioną wartość `04-2017` lub nowszy:</span><span class="sxs-lookup"><span data-stu-id="97bd3-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="97bd3-164">Teraz Włącz usługę Menedżer naprawy przez dodanie poniższego `addonFeaturres` sekcji po `fabricSettings` sekcji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="97bd3-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="97bd3-165">Zaktualizuj manifeście klastra za pomocą tych zmian przy użyciu manifest klastra o zaktualizowanych [Utwórz nowy klaster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) lub [Uaktualnij konfigurację klastra](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="97bd3-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="97bd3-166">Gdy w klastrze działa z manifestu klastra zaktualizowane, można przeglądać usługi repair Menedżera system działające w klastrze, która jest wywoływana `fabric:/System/RepairManagerService`w obszarze części Eksploratora usługi sieć szkieletowa usług systemowych.</span><span class="sxs-lookup"><span data-stu-id="97bd3-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="97bd3-167">Wyłącz automatyczną aktualizację systemu Windows na wszystkich węzłach</span><span class="sxs-lookup"><span data-stu-id="97bd3-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="97bd3-168">Aktualizacje automatyczne systemu Windows, mogą spowodować utratę dostępności, ponieważ wiele węzłów klastra można uruchomić ponownie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="97bd3-169">Poprawka aplikacji aranżacji, domyślnie próbuje wyłączania automatycznej aktualizacji systemu Windows w każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="97bd3-170">Jeśli ustawienia są zarządzane przez administratora lub zasad grupy, firma Microsoft zaleca jednak jawnie ustawienie zasad usługi Windows Update "Powiadom przed pobierania".</span><span class="sxs-lookup"><span data-stu-id="97bd3-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="97bd3-171">Opcjonalnie: Włącz diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="97bd3-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="97bd3-172">Klastry z systemem wersja środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i loguje się powyżej Dzienniki aplikacji aranżacji zbieranie poprawki w ramach sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="97bd3-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="97bd3-173">Ten krok można pominąć, jeśli klaster jest uruchomiony na wersji środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i powyżej.</span><span class="sxs-lookup"><span data-stu-id="97bd3-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="97bd3-174">W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki aplikacji aranżacji poprawki są gromadzone lokalnie na każdym z węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="97bd3-175">Firma Microsoft zaleca, aby skonfigurować diagnostyki Azure przekazywania dzienników z wszystkich węzłów w centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="97bd3-176">Aby uzyskać informacje na temat włączania diagnostyki Azure, zobacz [zbierania dzienników przy użyciu diagnostyki Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="97bd3-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="97bd3-177">Dzienniki aplikacji aranżacji poprawki są generowane dla następującego dostawcy stałym identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="97bd3-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="97bd3-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="97bd3-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="97bd3-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="97bd3-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="97bd3-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="97bd3-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="97bd3-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="97bd3-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="97bd3-182">W instrukcji goto szablonu usługi Resource Manager `EtwEventSourceProviderConfiguration` w obszarze `WadCfg` i dodaj następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="97bd3-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

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
> <span data-ttu-id="97bd3-183">Jeśli klaster sieci szkieletowej usług ma wiele typów węzeł, a następnie poprzedniej sekcji, należy dodać wszystkie `WadCfg` sekcje.</span><span class="sxs-lookup"><span data-stu-id="97bd3-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="97bd3-184">Pobierz pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-184">Download the app package</span></span>

<span data-ttu-id="97bd3-185">Pobierz aplikację z [pobrać link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="97bd3-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="97bd3-186">Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-186">Configure the app</span></span>

<span data-ttu-id="97bd3-187">Zachowanie aplikacji aranżacji poprawek można skonfigurować zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="97bd3-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="97bd3-188">Zastąpić wartości domyślne, przekazując w parametrze aplikacji podczas tworzenia aplikacji lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="97bd3-189">Można podać parametry aplikacji, określając `ApplicationParameter` do `Start-ServiceFabricApplicationUpgrade` lub `New-ServiceFabricApplication` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97bd3-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="97bd3-190">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="97bd3-190">**Parameter**</span></span>        |<span data-ttu-id="97bd3-191">**Typ**</span><span class="sxs-lookup"><span data-stu-id="97bd3-191">**Type**</span></span>                          | <span data-ttu-id="97bd3-192">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="97bd3-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="97bd3-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="97bd3-193">MaxResultsToCache</span></span>    |<span data-ttu-id="97bd3-194">Długie</span><span class="sxs-lookup"><span data-stu-id="97bd3-194">Long</span></span>                              | <span data-ttu-id="97bd3-195">Maksymalna liczba wyników aktualizacji systemu Windows, które mają być buforowane.</span><span class="sxs-lookup"><span data-stu-id="97bd3-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="97bd3-196">Wartość domyślna to 3000 zakładając, że:</span><span class="sxs-lookup"><span data-stu-id="97bd3-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="97bd3-197">-Liczba węzłów to 20.</span><span class="sxs-lookup"><span data-stu-id="97bd3-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="97bd3-198">-Liczba aktualizacji pojawia się w węźle miesięcznie wynosi pięć.</span><span class="sxs-lookup"><span data-stu-id="97bd3-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="97bd3-199">-Liczba wyników dla operacji może być 10.</span><span class="sxs-lookup"><span data-stu-id="97bd3-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="97bd3-200">— Powinny być przechowywane wyniki dla ostatnich trzech miesięcy.</span><span class="sxs-lookup"><span data-stu-id="97bd3-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="97bd3-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="97bd3-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="97bd3-202">wyliczenia</span><span class="sxs-lookup"><span data-stu-id="97bd3-202">Enum</span></span> <br> <span data-ttu-id="97bd3-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="97bd3-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="97bd3-204">TaskApprovalPolicy wskazuje zasad, który ma być używany przez usługę koordynatora instalowania aktualizacji systemu Windows w węzłach klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="97bd3-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="97bd3-205">Dozwolone wartości to:</span><span class="sxs-lookup"><span data-stu-id="97bd3-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="97bd3-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="97bd3-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="97bd3-207">Windows Update jest zainstalowany jeden węzeł naraz.</span><span class="sxs-lookup"><span data-stu-id="97bd3-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="97bd3-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="97bd3-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="97bd3-209">Windows Update jest zainstalowanych domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="97bd3-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="97bd3-210">(Maksymalnie, wszystkie węzły należące do domeny uaktualnienia można przejść do usługi Windows Update.)</span><span class="sxs-lookup"><span data-stu-id="97bd3-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="97bd3-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="97bd3-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="97bd3-212">Długie</span><span class="sxs-lookup"><span data-stu-id="97bd3-212">Long</span></span>  <br> <span data-ttu-id="97bd3-213">(Domyślnie: 1024)</span><span class="sxs-lookup"><span data-stu-id="97bd3-213">(Default: 1024)</span></span>               |<span data-ttu-id="97bd3-214">Maksymalny rozmiar poprawki aplikacji aranżacji loguje MB, co może trwale znajdować się lokalnie w węzłach.</span><span class="sxs-lookup"><span data-stu-id="97bd3-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="97bd3-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="97bd3-215">WUQuery</span></span>               | <span data-ttu-id="97bd3-216">Ciąg</span><span class="sxs-lookup"><span data-stu-id="97bd3-216">string</span></span><br><span data-ttu-id="97bd3-217">(Domyślnie: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="97bd3-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="97bd3-218">Zapytania w celu pobrania aktualizacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97bd3-218">Query to get Windows updates.</span></span> <span data-ttu-id="97bd3-219">Aby uzyskać więcej informacji, zobacz [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="97bd3-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="97bd3-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="97bd3-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="97bd3-221">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="97bd3-221">Bool</span></span> <br> <span data-ttu-id="97bd3-222">(domyślne: True)</span><span class="sxs-lookup"><span data-stu-id="97bd3-222">(default: True)</span></span>                 | <span data-ttu-id="97bd3-223">Ta flaga zezwala na instalację aktualizacji systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="97bd3-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="97bd3-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="97bd3-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="97bd3-225">int</span><span class="sxs-lookup"><span data-stu-id="97bd3-225">Int</span></span> <br><span data-ttu-id="97bd3-226">(Domyślnie: 90).</span><span class="sxs-lookup"><span data-stu-id="97bd3-226">(Default: 90)</span></span>                   | <span data-ttu-id="97bd3-227">Określa limit czasu do żadnej operacji usługi Windows Update (wyszukiwania lub pobierania lub instalacji).</span><span class="sxs-lookup"><span data-stu-id="97bd3-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="97bd3-228">Jeśli działanie nie zostało ukończone w określonym czasie, zostało przerwane.</span><span class="sxs-lookup"><span data-stu-id="97bd3-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="97bd3-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="97bd3-229">WURescheduleCount</span></span>     | <span data-ttu-id="97bd3-230">int</span><span class="sxs-lookup"><span data-stu-id="97bd3-230">Int</span></span> <br> <span data-ttu-id="97bd3-231">(Domyślne: 5).</span><span class="sxs-lookup"><span data-stu-id="97bd3-231">(Default: 5)</span></span>                  | <span data-ttu-id="97bd3-232">Maksymalna liczba usługi zmienia harmonogram systemu Windows aktualizacji w przypadku, gdy operacja trwale kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="97bd3-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="97bd3-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="97bd3-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="97bd3-234">int</span><span class="sxs-lookup"><span data-stu-id="97bd3-234">Int</span></span> <br><span data-ttu-id="97bd3-235">(Domyślnie: 30).</span><span class="sxs-lookup"><span data-stu-id="97bd3-235">(Default: 30)</span></span> | <span data-ttu-id="97bd3-236">Interwał, jaką usługa zmienia harmonogram aktualizacji systemu Windows w przypadku awaria nie zniknie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="97bd3-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="97bd3-237">WUFrequency</span></span>           | <span data-ttu-id="97bd3-238">Ciąg rozdzielony przecinkami (domyślne: "Co tydzień, środę, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="97bd3-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="97bd3-239">Częstotliwość instalacji usługi Windows Update.</span><span class="sxs-lookup"><span data-stu-id="97bd3-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="97bd3-240">Format i możliwe wartości to:</span><span class="sxs-lookup"><span data-stu-id="97bd3-240">The format and possible values are:</span></span> <br><span data-ttu-id="97bd3-241">— Co miesiąc, DD gg, na przykład, co miesiąc, 5, 12: 22:32.</span><span class="sxs-lookup"><span data-stu-id="97bd3-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="97bd3-242">— Gg co tydzień i dzień, na przykład, co tydzień, Wtorek, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="97bd3-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="97bd3-243">-Codziennie, ss, na przykład codziennie, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="97bd3-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="97bd3-244">-Wskazuje brak, nie można wykonać aktualizacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97bd3-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="97bd3-245">Należy pamiętać, że wszystkie godziny są w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="97bd3-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="97bd3-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="97bd3-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="97bd3-247">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="97bd3-247">Bool</span></span> <br><span data-ttu-id="97bd3-248">(Domyślnie: true)</span><span class="sxs-lookup"><span data-stu-id="97bd3-248">(Default: true)</span></span> | <span data-ttu-id="97bd3-249">Ustawiając tę flagę aplikacji akceptuje umowy licencyjnej użytkownika końcowego dla Windows Update w imieniu właściciela maszyny.</span><span class="sxs-lookup"><span data-stu-id="97bd3-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="97bd3-250">Jeśli chcesz usługi Windows Update, aby natychmiast ustawić `WUFrequency` względem czasu wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="97bd3-251">Na przykład klaster z pięcioma węzłami testu i Planowanie wdrażania aplikacji przy około 17:00:00 czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="97bd3-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="97bd3-252">Jeśli założono, że uaktualnienie aplikacji lub wdrożenia ma 30 minut maksymalnie, ustaw WUFrequency jako "Codziennie, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="97bd3-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="97bd3-253">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-253">Deploy the app</span></span>

1. <span data-ttu-id="97bd3-254">Zakończ wszystkie wstępnie wymagane kroki, aby przygotować klaster.</span><span class="sxs-lookup"><span data-stu-id="97bd3-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="97bd3-255">Wdrażanie aplikacji aranżacji poprawki, takich jak każda inna aplikacja usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97bd3-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="97bd3-256">Aplikację można wdrożyć przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97bd3-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="97bd3-257">Postępuj zgodnie z instrukcjami [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="97bd3-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="97bd3-258">Aby skonfigurować aplikację w czasie wdrażania, należy przekazać `ApplicationParamater` do `New-ServiceFabricApplication` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97bd3-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="97bd3-259">Dla wygody przygotowaliśmy skryptu Deploy.ps1 wraz z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="97bd3-260">Aby użyć skryptu:</span><span class="sxs-lookup"><span data-stu-id="97bd3-260">To use the script:</span></span>

    - <span data-ttu-id="97bd3-261">Ustanawianie połączenia z klastrem usługi sieć szkieletowa usług za pomocą `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="97bd3-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="97bd3-262">Uruchom skrypt programu PowerShell Deploy.ps1 z odpowiednią `ApplicationParameter` wartość.</span><span class="sxs-lookup"><span data-stu-id="97bd3-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="97bd3-263">Zachowaj skrypt i folder aplikacji PatchOrchestrationApplication w tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="97bd3-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="97bd3-264">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-264">Upgrade the app</span></span>

<span data-ttu-id="97bd3-265">Aby uaktualnić istniejącą aplikację aranżacji poprawki przy użyciu programu PowerShell, postępuj zgodnie z instrukcjami [uaktualniania aplikacji sieci szkieletowej usług za pomocą programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="97bd3-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="97bd3-266">Usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-266">Remove the app</span></span>

<span data-ttu-id="97bd3-267">Aby usunąć aplikację, postępuj zgodnie z instrukcjami [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="97bd3-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="97bd3-268">Dla wygody przygotowaliśmy skryptu Undeploy.ps1 wraz z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="97bd3-269">Aby użyć skryptu:</span><span class="sxs-lookup"><span data-stu-id="97bd3-269">To use the script:</span></span>

  - <span data-ttu-id="97bd3-270">Ustanawianie połączenia z klastrem usługi sieć szkieletowa usług za pomocą ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="97bd3-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="97bd3-271">Uruchom skrypt programu PowerShell Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="97bd3-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="97bd3-272">Zachowaj skrypt i folder aplikacji PatchOrchestrationApplication w tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="97bd3-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="97bd3-273">Wyświetl wyniki usługi Windows Update</span><span class="sxs-lookup"><span data-stu-id="97bd3-273">View the Windows Update results</span></span>

<span data-ttu-id="97bd3-274">Poprawka aplikacji aranżacji uwidacznia interfejsów API REST, aby wyświetlić wyniki historyczne dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97bd3-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="97bd3-275">Przykład wyniku JSON:</span><span class="sxs-lookup"><span data-stu-id="97bd3-275">An example of the result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
<span data-ttu-id="97bd3-276">Jeśli aktualizacja nie jest zaplanowane jeszcze, wyniku JSON nie jest pusty.</span><span class="sxs-lookup"><span data-stu-id="97bd3-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="97bd3-277">Zaloguj się do klastra zapytania usługi Windows Update wyników.</span><span class="sxs-lookup"><span data-stu-id="97bd3-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="97bd3-278">Następnie sprawdzić repliki adres podstawowy usługi koordynatora i kliknij adres URL z przeglądarki: http://&lt;IP REPLIKI&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="97bd3-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="97bd3-279">Punkt końcowy REST usługi Koordynator ma portów dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="97bd3-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="97bd3-280">Aby sprawdzić dokładny adres URL, zajrzyj do Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="97bd3-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="97bd3-281">Na przykład, wyniki są dostępne pod adresem `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="97bd3-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Obraz końcowy REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="97bd3-283">Zwrotny serwer proxy jest włączona w klastrze, można uzyskać dostępu do adresu URL z spoza klastra, a także.</span><span class="sxs-lookup"><span data-stu-id="97bd3-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="97bd3-284">Punkt końcowy, który musi być trafień jest http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="97bd3-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="97bd3-285">Aby włączyć zwrotnego serwera proxy w klastrze, wykonaj czynności opisane w [odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="97bd3-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="97bd3-286">Po skonfigurowaniu zwrotnego serwera proxy, wszystkie micro usługi w klastrze, które ujawniać punkt końcowy HTTP adresowane z spoza klastra.</span><span class="sxs-lookup"><span data-stu-id="97bd3-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="97bd3-287">Diagnostyka kondycji zdarzenia</span><span class="sxs-lookup"><span data-stu-id="97bd3-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="97bd3-288">Aplikacja orchestration poprawki zbieranie dzienników</span><span class="sxs-lookup"><span data-stu-id="97bd3-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="97bd3-289">Dzienniki aplikacji aranżacji poprawki są zbierane w ramach dzienników sieci szkieletowej usług z wersji środowiska uruchomieniowego `5.6.220.9494` i powyżej.</span><span class="sxs-lookup"><span data-stu-id="97bd3-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="97bd3-290">W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki mogą zostać pobrane za pomocą jednej z poniższych metod.</span><span class="sxs-lookup"><span data-stu-id="97bd3-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="97bd3-291">Lokalnie na każdym węźle</span><span class="sxs-lookup"><span data-stu-id="97bd3-291">Locally on each node</span></span>

<span data-ttu-id="97bd3-292">Dzienniki są gromadzone lokalnie na każdym węźle klastra sieci szkieletowej usług w przypadku wersji środowiska uruchomieniowego usługi sieć szkieletowa usług mniej niż `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="97bd3-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="97bd3-293">Lokalizacja dostępu do dzienników jest \[sieci szkieletowej usług\_instalacji\_dysków\]:\\PatchOrchestrationApplication\\dzienniki.</span><span class="sxs-lookup"><span data-stu-id="97bd3-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="97bd3-294">Na przykład, jeśli usługa sieć szkieletowa jest zainstalowany na dysku D, ścieżka jest D:\\PatchOrchestrationApplication\\dzienniki.</span><span class="sxs-lookup"><span data-stu-id="97bd3-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="97bd3-295">Centralnej lokalizacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-295">Central location</span></span>

<span data-ttu-id="97bd3-296">Jeśli diagnostyki Azure jest skonfigurowany jako część wstępnie wymagane kroki, dzienniki aplikacji aranżacji poprawki są dostępne w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="97bd3-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="97bd3-297">Raportów o kondycji</span><span class="sxs-lookup"><span data-stu-id="97bd3-297">Health reports</span></span>

<span data-ttu-id="97bd3-298">Poprawka aplikacji aranżacji publikuje również raporty kondycji względem usługi Koordynator lub agenta węzła w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="97bd3-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="97bd3-299">Operacja usługi Windows Update, nie powiodła się</span><span class="sxs-lookup"><span data-stu-id="97bd3-299">A Windows Update operation failed</span></span>

<span data-ttu-id="97bd3-300">W przypadku niepowodzenia operacji usługi Windows Update w węźle raport o kondycji jest generowany z usługą agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="97bd3-301">Szczegóły raport o kondycji zawiera nazwy węzła powodować problemy.</span><span class="sxs-lookup"><span data-stu-id="97bd3-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="97bd3-302">Po pomyślnym problematyczne węzła zakończeniu stosowanie poprawek, raportu są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="97bd3-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="97bd3-303">Węzeł NTService Agent nie działa</span><span class="sxs-lookup"><span data-stu-id="97bd3-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="97bd3-304">Jeśli węzeł NTService Agent działa w węźle, z usługą agenta węzła generowany jest raport dotyczący kondycji poziom ostrzeżeń.</span><span class="sxs-lookup"><span data-stu-id="97bd3-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="97bd3-305">Usługa Menedżera naprawy nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="97bd3-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="97bd3-306">Jeśli usługa Menedżera naprawy nie zostanie znaleziony w klastrze, usługi Koordynator generowany jest raport o kondycji poziom ostrzeżeń.</span><span class="sxs-lookup"><span data-stu-id="97bd3-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="97bd3-307">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="97bd3-307">Frequently asked questions</span></span>

<span data-ttu-id="97bd3-308">Q.</span><span class="sxs-lookup"><span data-stu-id="97bd3-308">Q.</span></span> <span data-ttu-id="97bd3-309">**Dlaczego wyświetlać Mój klastra w stanie błędu, gdy aplikacja orchestration poprawki działa?**</span><span class="sxs-lookup"><span data-stu-id="97bd3-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="97bd3-310">A.</span><span class="sxs-lookup"><span data-stu-id="97bd3-310">A.</span></span> <span data-ttu-id="97bd3-311">W procesie instalacji poprawki aplikacji aranżacji wyłącza lub ponownego uruchomienia węzłów, które mogą skutkować tymczasowo kondycji klastra, przechodząc w dół.</span><span class="sxs-lookup"><span data-stu-id="97bd3-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="97bd3-312">Na podstawie zasad dla aplikacji, albo jeden węzeł może przejść w dół podczas operacji stosowania poprawek *lub* całej domeny uaktualnienia można przestaną działać jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="97bd3-313">Na koniec instalacji usługi Windows Update są reenabled węzły po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="97bd3-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="97bd3-314">W poniższym przykładzie klastra przejścia do stanu błędu tymczasowo ponieważ dwa węzły zostały w dół, a zasady MaxPercentageUnhealthNodes zostało naruszone.</span><span class="sxs-lookup"><span data-stu-id="97bd3-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="97bd3-315">Błąd jest tymczasowy, dopóki trwa operacja stosowania poprawek.</span><span class="sxs-lookup"><span data-stu-id="97bd3-315">The error is temporary until the patching operation is ongoing.</span></span>

![Obraz zła klastra](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="97bd3-317">Jeśli problem będzie się powtarzać, zapoznaj się z rozdziałem Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="97bd3-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="97bd3-318">Q.</span><span class="sxs-lookup"><span data-stu-id="97bd3-318">Q.</span></span> <span data-ttu-id="97bd3-319">**Aplikacja orchestration poprawki jest w stanie ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="97bd3-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="97bd3-320">A.</span><span class="sxs-lookup"><span data-stu-id="97bd3-320">A.</span></span> <span data-ttu-id="97bd3-321">Sprawdź, czy raport o kondycji opublikowane w związku z aplikacją jest główną przyczynę.</span><span class="sxs-lookup"><span data-stu-id="97bd3-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="97bd3-322">Zazwyczaj ostrzeżenie zawiera szczegółowe informacje o problemie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="97bd3-323">W przypadku przejściowy problem aplikacji powinien automatycznego odzyskiwania z tego stanu.</span><span class="sxs-lookup"><span data-stu-id="97bd3-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="97bd3-324">Q.</span><span class="sxs-lookup"><span data-stu-id="97bd3-324">Q.</span></span> <span data-ttu-id="97bd3-325">**Co można zrobić, jeśli mój klastra jest nieprawidłowy i należy wykonać aktualizację pilnych systemu operacyjnego?**</span><span class="sxs-lookup"><span data-stu-id="97bd3-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="97bd3-326">A.</span><span class="sxs-lookup"><span data-stu-id="97bd3-326">A.</span></span> <span data-ttu-id="97bd3-327">Aplikacja orchestration poprawki nie można zainstalować aktualizacji klastra jest zła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="97bd3-328">Spróbuj przełączyć klastra do dobrej kondycji, aby odblokować przepływu pracy aplikacji aranżacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="97bd3-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="97bd3-329">Q.</span><span class="sxs-lookup"><span data-stu-id="97bd3-329">Q.</span></span> <span data-ttu-id="97bd3-330">**Dlaczego poprawki w klastrach podąża tak długo do uruchomienia?**</span><span class="sxs-lookup"><span data-stu-id="97bd3-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="97bd3-331">A.</span><span class="sxs-lookup"><span data-stu-id="97bd3-331">A.</span></span> <span data-ttu-id="97bd3-332">Czas potrzebny aplikacji aranżacji poprawki przede wszystkim jest zależna od następujących czynników:</span><span class="sxs-lookup"><span data-stu-id="97bd3-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="97bd3-333">Zasady usługi koordynatora.</span><span class="sxs-lookup"><span data-stu-id="97bd3-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="97bd3-334">Domyślne zasady `NodeWise`, powoduje stosowanie poprawek tylko jeden węzeł naraz.</span><span class="sxs-lookup"><span data-stu-id="97bd3-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="97bd3-335">Szczególnie w przypadku większych klastrów, firma Microsoft zaleca się używanie `UpgradeDomainWise` zasady w celu uzyskania szybszego poprawki w klastrach.</span><span class="sxs-lookup"><span data-stu-id="97bd3-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="97bd3-336">Liczba dostępnych do pobrania i zainstalowania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="97bd3-337">Średni czas potrzebny do pobrania i zainstalowania aktualizacji, który nie może przekraczać po kilku godzinach.</span><span class="sxs-lookup"><span data-stu-id="97bd3-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="97bd3-338">Wydajność maszyny Wirtualnej i sieci przepustowości.</span><span class="sxs-lookup"><span data-stu-id="97bd3-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="97bd3-339">Q.</span><span class="sxs-lookup"><span data-stu-id="97bd3-339">Q.</span></span> <span data-ttu-id="97bd3-340">**Dlaczego widzę niektórych aktualizacji w wynikach usługi Windows Update uzyskany za pośrednictwem interfejsu api REST, ale nie w historii usługi Windows Update na komputerze?**</span><span class="sxs-lookup"><span data-stu-id="97bd3-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="97bd3-341">A.</span><span class="sxs-lookup"><span data-stu-id="97bd3-341">A.</span></span> <span data-ttu-id="97bd3-342">Niektóre aktualizacje produktu muszą zostać zaewidencjonowane historii odpowiednich aktualizacji/poprawki.</span><span class="sxs-lookup"><span data-stu-id="97bd3-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="97bd3-343">Przykład: Usługa Windows Defender aktualizacje nie są wyświetlane w historii usługi Windows Update w systemie Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="97bd3-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="97bd3-344">Zastrzeżenia</span><span class="sxs-lookup"><span data-stu-id="97bd3-344">Disclaimers</span></span>

- <span data-ttu-id="97bd3-345">Poprawka aplikacji aranżacji akceptuje umowy licencyjnej użytkownika końcowego z Windows Update w imieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97bd3-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="97bd3-346">Opcjonalnie ustawienie może zostać wyłączone w konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="97bd3-347">Poprawka aplikacji aranżacji zbiera dane telemetryczne umożliwiający śledzenie użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="97bd3-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="97bd3-348">Dane telemetryczne aplikacji następuje ustawienie ustawienia telemetrii środowiska uruchomieniowego platformy Service Fabric, (która jest domyślnie włączona).</span><span class="sxs-lookup"><span data-stu-id="97bd3-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="97bd3-349">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="97bd3-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="97bd3-350">Węzeł nie jest powracające stanu w górę</span><span class="sxs-lookup"><span data-stu-id="97bd3-350">A node is not coming back to up state</span></span>

<span data-ttu-id="97bd3-351">**Węzeł może zostać zablokowana na wyłączenie stanu, ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="97bd3-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="97bd3-352">Trwa oczekiwanie na sprawdzenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="97bd3-352">A safety check is pending.</span></span> <span data-ttu-id="97bd3-353">Aby rozwiązać ten problem, upewnij się, że wystarczającej liczby węzłów są dostępne w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="97bd3-354">**Węzeł może zostać zatrzymane w stanie wyłączenia, ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="97bd3-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="97bd3-355">Węzeł został wyłączony ręcznie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-355">The node was disabled manually.</span></span>
- <span data-ttu-id="97bd3-356">Węzeł został wyłączony z powodu trwającej infrastruktury platformy Azure zadanie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="97bd3-357">Węzeł został wyłączony tymczasowo przez aplikację aranżacji poprawki do stosowania poprawek węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="97bd3-358">**Węzeł może zostać zatrzymane w stanie down ponieważ**:</span><span class="sxs-lookup"><span data-stu-id="97bd3-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="97bd3-359">Węzeł została umieszczona w stanie down ręcznie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="97bd3-360">Węzeł jest w trakcie ponownego uruchomienia (które może zostać wyzwolone przez aplikację aranżacji poprawki).</span><span class="sxs-lookup"><span data-stu-id="97bd3-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="97bd3-361">Węzeł nie działa z powodu błędny maszyny Wirtualnej lub problemy z połączeniem komputera lub sieci.</span><span class="sxs-lookup"><span data-stu-id="97bd3-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="97bd3-362">Aktualizacje zostały pominięte na niektóre węzły</span><span class="sxs-lookup"><span data-stu-id="97bd3-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="97bd3-363">Poprawka aplikacji aranżacji próbuje zainstalować Windows update zgodnie z zasadami planowaniem mogą.</span><span class="sxs-lookup"><span data-stu-id="97bd3-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="97bd3-364">Usługa próbuje odzyskać węzeł i Pomiń aktualizację zgodnie z zasadami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97bd3-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="97bd3-365">W takim przypadku generowany jest raport o kondycji poziom ostrzeżeń z usługą agenta węzła.</span><span class="sxs-lookup"><span data-stu-id="97bd3-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="97bd3-366">Wynik dla usługi Windows Update zawiera także możliwe przyczyny niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="97bd3-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="97bd3-367">Kondycja klastra przechodzi do błędu podczas instalacji aktualizacji</span><span class="sxs-lookup"><span data-stu-id="97bd3-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="97bd3-368">Błędny usługi Windows update można obniżyć kondycji aplikacji lub klastra w określonym węźle lub domena uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="97bd3-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="97bd3-369">Poprawka aplikacji aranżacji zaprzestaje wszelkie kolejne operacje usługi Windows Update, dopóki klastra jest w dobrej kondycji ponownie.</span><span class="sxs-lookup"><span data-stu-id="97bd3-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="97bd3-370">Administrator musi interweniować, aby ustalić, dlaczego aplikacja lub klastra stał się niezdrowe, ponieważ usługa Windows Update.</span><span class="sxs-lookup"><span data-stu-id="97bd3-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="97bd3-371">Informacje o wersji:</span><span class="sxs-lookup"><span data-stu-id="97bd3-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="97bd3-372">Wersja 1.1.0</span><span class="sxs-lookup"><span data-stu-id="97bd3-372">Version 1.1.0</span></span>
- <span data-ttu-id="97bd3-373">Publiczny zlecenia</span><span class="sxs-lookup"><span data-stu-id="97bd3-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="97bd3-374">Wersja 1.1.1</span><span class="sxs-lookup"><span data-stu-id="97bd3-374">Version 1.1.1</span></span>
- <span data-ttu-id="97bd3-375">Rozwiązane usterki w SetupEntryPoint z NodeAgentService uniemożliwiający instalacji NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="97bd3-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="97bd3-376">Wersji 1.2.0 (Najnowsza wersja)</span><span class="sxs-lookup"><span data-stu-id="97bd3-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="97bd3-377">Poprawki błędów wokół systemu ponownie uruchomić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="97bd3-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="97bd3-378">Poprawka błędu podczas tworzenia zadania Menedżera zasobów z powodu którego kondycji wyboru podczas przygotowywania zadań naprawy nie wykonywane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="97bd3-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="97bd3-379">Zmienić trybu uruchamiania usługi systemu windows POANodeSvc z automatycznego na opóźnione auto.</span><span class="sxs-lookup"><span data-stu-id="97bd3-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
