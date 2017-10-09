---
title: "aaaAdd lub usuń węzły tooa autonomicznej klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd lub usuń węzły tooan sieć szkieletowa usług Azure klastra na fizyczne lub maszyny wirtualnej z systemem Windows Server, który może być lokalnym lub w dowolnej chmury."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="b09ce-103">Dodawanie lub usuwanie węzłów tooa autonomicznej klastra sieci szkieletowej usług w systemie Windows Server</span><span class="sxs-lookup"><span data-stu-id="b09ce-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="b09ce-104">Po utworzeniu [utworzone autonomicznej klastra sieci szkieletowej usług na komputerach z systemem Windows Server](service-fabric-cluster-creation-for-windows-server.md), może zmieniających się potrzeb biznesowych i może być konieczne tooadd lub usunąć węzły klastra tooyour.</span><span class="sxs-lookup"><span data-stu-id="b09ce-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="b09ce-105">Ten artykuł zawiera szczegółowy opis kroków tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="b09ce-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="b09ce-106">Należy pamiętać, że dodawania i usuwania węzła funkcjonalność nie jest obsługiwana w klastrach rozwoju lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b09ce-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="b09ce-107">Dodaj węzły klastra tooyour</span><span class="sxs-lookup"><span data-stu-id="b09ce-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="b09ce-108">Witaj przygotowanie wirtualna/machine ma tooadd tooyour klastra, wykonując kroki hello wspomnianego hello [hello przygotowanie maszyny toomeet hello z wymagań wstępnych dotyczących wdrażania klastra](service-fabric-cluster-creation-for-windows-server.md) sekcji</span><span class="sxs-lookup"><span data-stu-id="b09ce-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="b09ce-109">Identyfikowanie które domeny błędów i są tooadd będzie tej maszyny Wirtualnej/maszyny do domeny uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="b09ce-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="b09ce-110">Pulpitu zdalnego (RDP) do hello maszyny Wirtualnej/maszyny, które mają tooadd toohello klastra</span><span class="sxs-lookup"><span data-stu-id="b09ce-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="b09ce-111">Kopiowanie lub [Pobierz autonomiczny hello sieci szkieletowej usług w systemie Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello maszyny Wirtualnej/machine i Rozpakuj pakiet hello</span><span class="sxs-lookup"><span data-stu-id="b09ce-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="b09ce-112">Uruchom program Powershell z podwyższonym poziomem uprawnień i przejdź toohello lokalizacji rozpakowanej pakietu hello</span><span class="sxs-lookup"><span data-stu-id="b09ce-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="b09ce-113">Uruchom hello *AddNode.ps1* skryptu z parametrami hello opisujące hello nowego węzła tooadd.</span><span class="sxs-lookup"><span data-stu-id="b09ce-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="b09ce-114">w poniższym przykładzie Hello dodaje nowy węzeł o nazwie VM5, z typem NodeType0 i adresów IP 182.17.34.52, UD1 i fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="b09ce-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="b09ce-115">Hello *ExistingClusterConnectionEndPoint* punktu końcowego połączenia dla węzła jest już hello istniejącego klastra, które mogą być hello adres IP *żadnych* węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b09ce-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="b09ce-116">Po zakończeniu hello skryptu można sprawdzić, czy nowy węzeł hello został dodany przez uruchomienie hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b09ce-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="b09ce-117">tooensure spójności w różnych węzłach w klastrze hello, musisz zainicjować uaktualnienie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b09ce-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="b09ce-118">Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello najnowszego pliku konfiguracji i Dodaj hello nowo dodany węzeł zbyt sekcji "Węzłów".</span><span class="sxs-lookup"><span data-stu-id="b09ce-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="b09ce-119">Zalecane jest również, tooalways hello najnowsze klastra konfiguracja jest dostępna w przypadku hello konieczność tooredploy klastra z hello tej samej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b09ce-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="b09ce-120">Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="b09ce-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b09ce-121">Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b09ce-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b09ce-122">Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b09ce-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="b09ce-123">Dodaj węzły tooclusters skonfigurowaną przy użyciu usługi zarządzane przez grupę zabezpieczeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b09ce-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="b09ce-124">W przypadku klastrów skonfigurowano Account(gMSA) usług zarządzanych grupy (https://technet.microsoft.com/library/hh831782.aspx) przy użyciu uaktualniania programu configuration można dodać nowego węzła:</span><span class="sxs-lookup"><span data-stu-id="b09ce-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="b09ce-125">Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) na żadnym z istniejących węzłów hello tooget hello najnowszego pliku konfiguracji i Dodaj szczegóły dotyczące hello nowy węzeł ma tooadd w sekcji węzły"hello".</span><span class="sxs-lookup"><span data-stu-id="b09ce-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="b09ce-126">Upewnij się, że hello nowy węzeł jest częścią programu hello zarządzanego konta sam grupy.</span><span class="sxs-lookup"><span data-stu-id="b09ce-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="b09ce-127">To konto powinno mieć uprawnienia administratora na wszystkich komputerach.</span><span class="sxs-lookup"><span data-stu-id="b09ce-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="b09ce-128">Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="b09ce-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="b09ce-129">Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b09ce-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b09ce-130">Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b09ce-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="b09ce-131">Dodaj węzły klastra tooyour typów</span><span class="sxs-lookup"><span data-stu-id="b09ce-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="b09ce-132">Kolejność tooadd nowego typu węzła, zmodyfikuj konfigurację tooinclude hello nowego węzła typu w sekcji "Elementów NodeType" w obszarze "Właściwości" i rozpocząć konfigurację aktualizację, używając [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b09ce-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="b09ce-133">Po zakończeniu uaktualniania hello, możesz dodać nowy klaster tooyour węzły z tym typem węzła.</span><span class="sxs-lookup"><span data-stu-id="b09ce-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="b09ce-134">Usuń węzły z klastra</span><span class="sxs-lookup"><span data-stu-id="b09ce-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="b09ce-135">Można usunąć węzła z klastra przy użyciu uaktualniania konfiguracji, w następujące sposób hello:</span><span class="sxs-lookup"><span data-stu-id="b09ce-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="b09ce-136">Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello najnowszego pliku konfiguracji i *Usuń* hello węzła z sekcji "Węzłów".</span><span class="sxs-lookup"><span data-stu-id="b09ce-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="b09ce-137">Dodaj hello "NodesToBeRemoved" parametr zbyt "ustawienia" sekcji wewnątrz sekcji "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="b09ce-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="b09ce-138">Witaj "wartość" powinna być rozdzielana przecinkami lista nazwy węzła węzłów, które wymagają toobe usunięte.</span><span class="sxs-lookup"><span data-stu-id="b09ce-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="b09ce-139">Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="b09ce-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b09ce-140">Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b09ce-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b09ce-141">Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="b09ce-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="b09ce-142">Usuwanie węzłów może zainicjować kilku uaktualnień.</span><span class="sxs-lookup"><span data-stu-id="b09ce-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="b09ce-143">Niektóre węzły są oznaczone ikoną z `IsSeedNode=”true”` tagu i mogą zostać zidentyfikowane przez wysyłanie zapytań klastra hello manifestu przy użyciu `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="b09ce-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="b09ce-144">Usunięcie tych węzłów może trwać dłużej niż inne, ponieważ hello inicjatora węzły będą mieć toobe przenoszenia w takich scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="b09ce-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="b09ce-145">Hello klastra musi obsługiwać co najmniej 3 węzłach typu węzła podstawowego.</span><span class="sxs-lookup"><span data-stu-id="b09ce-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="b09ce-146">Usuń typy węzłów z klastra</span><span class="sxs-lookup"><span data-stu-id="b09ce-146">Remove node types from your cluster</span></span>
<span data-ttu-id="b09ce-147">Przed usunięciem typu węzła, sprawdź występują we wszystkich węzłach, odwołuje się do typu węzła hello.</span><span class="sxs-lookup"><span data-stu-id="b09ce-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="b09ce-148">Usuń te węzły przed usunięciem hello odpowiedniego typu węzła.</span><span class="sxs-lookup"><span data-stu-id="b09ce-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="b09ce-149">Po usunięciu wszystkich odpowiadających im węzłów, musisz usunąć hello NodeType z konfiguracji klastra hello i zacząć od konfiguracji aktualizację, używając [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b09ce-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="b09ce-150">Zastąp głównej węzłów w klastrze</span><span class="sxs-lookup"><span data-stu-id="b09ce-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="b09ce-151">zastąpienie Hello głównej węzłów powinny być wykonywane jeden węzeł po kolei, zamiast usuwania, a następnie dodanie w partiach.</span><span class="sxs-lookup"><span data-stu-id="b09ce-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b09ce-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b09ce-152">Next steps</span></span>
* [<span data-ttu-id="b09ce-153">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b09ce-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="b09ce-154">Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów</span><span class="sxs-lookup"><span data-stu-id="b09ce-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="b09ce-155">Tworzenie klastra usługi sieć szkieletowa autonomiczny z systemem Windows maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b09ce-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

