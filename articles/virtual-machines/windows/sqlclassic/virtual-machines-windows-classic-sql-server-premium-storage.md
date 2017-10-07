---
title: "Usługa Azure Premium Storage z programem SQL Server aaaUse | Dokumentacja firmy Microsoft"
description: "W tym artykule używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania oraz zapewnia wskazówki na temat używania usługi Azure Premium Storage z programem SQL Server uruchomiony na maszynach wirtualnych platformy Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="fc0db-103">Korzystanie z usługi Azure Premium Storage z programem SQL Server na maszynach wirtualnych</span><span class="sxs-lookup"><span data-stu-id="fc0db-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="fc0db-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fc0db-104">Overview</span></span>
<span data-ttu-id="fc0db-105">[Usługa Azure Premium Storage](../../../storage/common/storage-premium-storage.md) jest hello generacji magazynu, który zapewnia małe opóźnienia i wysokiej wydajności we/wy.</span><span class="sxs-lookup"><span data-stu-id="fc0db-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="fc0db-106">Najlepsza dla klucza obciążeń intensywnie wykorzystujących we/wy, takich jak program SQL Server na IaaS [maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="fc0db-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc0db-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc0db-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc0db-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fc0db-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc0db-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="fc0db-110">Ten artykuł zawiera wskazówki dotyczące migrowania maszyny wirtualnej z systemem toouse programu SQL Server magazyn w warstwie Premium i planowania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="fc0db-111">W tym infrastruktury platformy Azure (sieci, magazynu) i kroki maszyny Wirtualnej systemu Windows gościa.</span><span class="sxs-lookup"><span data-stu-id="fc0db-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="fc0db-112">przykład Witaj w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) przedstawia migrację tooend zakończenia pełnej kompleksowe jak zwiększona toomove większych maszyn wirtualnych tootake korzystać z lokalnego magazynu SSD przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0db-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="fc0db-113">Jest ważne toounderstand hello end-to-end proces pomocą usługi Azure Premium Storage z programem SQL Server na maszynach wirtualnych IAAS.</span><span class="sxs-lookup"><span data-stu-id="fc0db-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="fc0db-114">Obejmuje to:</span><span class="sxs-lookup"><span data-stu-id="fc0db-114">This includes:</span></span>

* <span data-ttu-id="fc0db-115">Identyfikacja toouse wymagania wstępne hello magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="fc0db-116">Przykłady wdrażanie programu SQL Server na IaaS tooPremium magazynu dla nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="fc0db-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="fc0db-117">Przykłady Migrowanie istniejących wdrożeń zarówno serwerów autonomicznych, jak i wdrożeń przy użyciu SQL zawsze włączonych grup dostępności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="fc0db-118">Podejścia możliwej migracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-118">Possible migration approaches.</span></span>
* <span data-ttu-id="fc0db-119">Pełne end-to-end przykład Azure, Windows i program SQL Server kroki hello migrację z istniejącej implementacji zawsze włączony.</span><span class="sxs-lookup"><span data-stu-id="fc0db-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="fc0db-120">Aby uzyskać więcej informacji o tła w programie SQL Server w maszynach wirtualnych platformy Azure, zobacz [programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc0db-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="fc0db-121">**Autor:** Sol Danielowi **recenzenci techniczni:** Śledź Vargas Artur Luis, Sanjay Mishra, Pravin Mital, blogu Thomasa Juergen, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="fc0db-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="fc0db-122">Wymagania wstępne dotyczące magazyn w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="fc0db-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="fc0db-123">Istnieje kilka wymagań wstępnych dotyczących używania magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="fc0db-124">Rozmiar maszyny</span><span class="sxs-lookup"><span data-stu-id="fc0db-124">Machine size</span></span>
<span data-ttu-id="fc0db-125">Dla magazynu Premium należy toouse DS serii maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="fc0db-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="fc0db-126">Jeśli nie używasz maszyny serii DS w usługi w chmurze przed, należy usunąć hello istniejącej maszyny Wirtualnej, zachowanie hello dołączonych dysków i następnie utwórz nową usługę w chmurze przed ponownym utworzeniem hello maszyny Wirtualnej jako DS * rozmiaru roli.</span><span class="sxs-lookup"><span data-stu-id="fc0db-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="fc0db-127">Aby uzyskać więcej informacji na temat rozmiarów maszyny wirtualnej, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc0db-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="fc0db-128">Usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-128">Cloud services</span></span>
<span data-ttu-id="fc0db-129">Po utworzeniu nowej usługi w chmurze tylko można DS * maszyn wirtualnych z magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="fc0db-130">Jeśli używasz programu SQL Server zawsze na platformie Azure, hello zawsze na odbiornika będzie odnosić się toohello Azure wewnętrznego lub zewnętrznego adresu IP usługi równoważenia obciążenia adres skojarzony z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="fc0db-131">Ten artykuł skupia się na temat toomigrate przy zachowaniu dostępności w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-132">Serii DS * musi być hello pierwsza maszyna wirtualna, który jest wdrożony toohello nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="fc0db-133">Regionalnych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="fc0db-133">Regional VNETS</span></span>
<span data-ttu-id="fc0db-134">Dla maszyn wirtualnych DS * należy skonfigurować hello sieci wirtualnych (VNET) hosting sieci regionalnych toobe maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="fc0db-135">To "rozszerzenie" hello sieci Wirtualnej jest tooallow hello większych maszyn wirtualnych toobe udostępnione w innych klastrach i umożliwić komunikację między nimi.</span><span class="sxs-lookup"><span data-stu-id="fc0db-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="fc0db-136">W hello następującego zrzutu ekranu hello wyróżnioną lokalizację pokazuje regionalnych sieci wirtualnych, hello pierwszego wyniku pokazuje "wąskie" sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="fc0db-138">Zostanie podniesiony Microsoft obsługi biletów toomigrate tooa regionalnej sieci Wirtualnej, Microsoft będzie zmiany, a następnie toocomplete hello migracji tooregional sieci wirtualnych, zmień właściwość hello AffinityGroup w konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="fc0db-139">Najpierw wyeksportować hello konfigurację sieci w programie PowerShell, a następnie zastąp hello **AffinityGroup** właściwości w hello **VirtualNetworkSite** element z **lokalizacji** Właściwość.</span><span class="sxs-lookup"><span data-stu-id="fc0db-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="fc0db-140">Określ `Location = XXXX` gdzie `XXXX` jest region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0db-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="fc0db-141">Następnie można zaimportować hello nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-141">Then import hello new configuration.</span></span>

<span data-ttu-id="fc0db-142">Na przykład biorąc pod uwagę powitania po konfigurację sieci Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="fc0db-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="fc0db-143">toomove tego tooa regionalnej sieci Wirtualnej w Europa Zachodnia, zmienić toohello konfiguracji powitania po:</span><span class="sxs-lookup"><span data-stu-id="fc0db-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="fc0db-144">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fc0db-144">Storage accounts</span></span>
<span data-ttu-id="fc0db-145">Konieczne będzie toocreate nowe konto magazynu, który jest skonfigurowany dla usługi Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="fc0db-146">Należy zauważyć, że użycie hello magazyn w warstwie Premium jest hello konta magazynu, nie dla poszczególnych dysków VHD, jednak podczas korzystania z maszyny Wirtualnej serii DS * możesz dołączyć pliki VHD z konta Premium i standardowa magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="fc0db-147">Może to rozważyć, jeśli nie chcesz, aby tooplace hello wirtualnego dysku twardego systemu operacyjnego na toohello konta Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="fc0db-148">następujące Hello **AzureStorageAccountPowerShell nowy** z hello "Premium_LRS" **typu** tworzy konto magazynu Premium:</span><span class="sxs-lookup"><span data-stu-id="fc0db-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="fc0db-149">Ustawienia pamięci podręcznej wirtualne dyski twarde</span><span class="sxs-lookup"><span data-stu-id="fc0db-149">VHDs Cache Settings</span></span>
<span data-ttu-id="fc0db-150">Witaj podstawowa różnica między tworzenie dysków, które są częścią konta Premium Storage jest ustawienie hello dyskowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="fc0db-151">Dla danych programu SQL Server woluminu dyski go zaleca się użycie "**buforowania odczytu**".</span><span class="sxs-lookup"><span data-stu-id="fc0db-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="fc0db-152">W przypadku woluminów dziennika transakcji hello dysku pamięci podręcznej ustawienie zbyt "**Brak**".</span><span class="sxs-lookup"><span data-stu-id="fc0db-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="fc0db-153">To jest inna niż hello zalecenia dotyczące kont magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="fc0db-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="fc0db-154">Po dołączeniu hello wirtualne dyski twarde nie można zmienić ustawienia pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="fc0db-155">Czy należy toodetach i ponownie dołączyć hello wirtualnego dysku twardego z ustawieniem zaktualizowano pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="fc0db-156">Miejsca do magazynowania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fc0db-156">Windows storage spaces</span></span>
<span data-ttu-id="fc0db-157">Można użyć [miejsca do magazynowania systemu Windows](https://technet.microsoft.com/library/hh831739.aspx) tak samo jak z poprzedniego magazynu w warstwie standardowa, umożliwi toomigrate maszynę Wirtualną, która jest już przy użyciu funkcji miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="fc0db-158">przykład Witaj w [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (krok 9 i do przodu) pokazuje hello tooextract kodu programu Powershell i zaimportuj maszynę Wirtualną za pomocą wielu dołączonych dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="fc0db-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="fc0db-159">Pule magazynu były używane z przepływności tooenhance konta magazynu Azure standardowe i zmniejszenia opóźnień.</span><span class="sxs-lookup"><span data-stu-id="fc0db-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="fc0db-160">Wartość można znaleźć w testowanie pod kątem nowych wdrożeń pul magazynu z atrybutem magazyn w warstwie Premium, ale co zwiększa stopnia złożoności z instalacji magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="fc0db-161">Jak toofind które dyski wirtualne Azure mapowania pul toostorage</span><span class="sxs-lookup"><span data-stu-id="fc0db-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="fc0db-162">Ponieważ istnieją różne pamięci podręcznej ustawienie zalecenia dotyczące dołączonych dysków VHD, można zdecydować toocopy hello wirtualne dyski twarde tooa konta Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="fc0db-163">Jednak gdy użytkownik przyłącz je ponownie toohello nowej serii DS maszyny Wirtualnej, może być konieczne ustawienia pamięci podręcznej hello tooalter.</span><span class="sxs-lookup"><span data-stu-id="fc0db-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="fc0db-164">Jest prostsze powitalne tooapply magazyn w warstwie Premium zalecanych ustawień pamięci podręcznej, jeśli masz oddzielnych dysków VHD dla hello danych SQL plików i dziennika plików (zamiast pojedynczego wirtualnego dysku twardego, który zawiera zarówno).</span><span class="sxs-lookup"><span data-stu-id="fc0db-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-165">Jeśli masz pliki danych i dziennika programu SQL Server na powitania na powitania wzorce dostępu we/wy dla obciążeń bazy danych zależy od tego samego woluminu, hello buforowanie wybranej opcji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="fc0db-166">Tylko testowania wykaże buforowania, która opcja jest najlepsza w przypadku tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="fc0db-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="fc0db-167">Miejsca do magazynowania systemu Windows, które składają się z wielu dysków VHD, konieczne będzie toolook w przypadku korzystania z oryginalnego tooidentify skrypty, które wirtualne dyski twarde dołączonych są jednak w określonej puli, więc można zdefiniować ustawienia pamięci podręcznej hello odpowiednio dla każdego dysku.</span><span class="sxs-lookup"><span data-stu-id="fc0db-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="fc0db-168">Jeśli nie masz oryginalnego tooshow dostępne skryptu można, które wirtualne dyski twarde mapy toohello puli magazynu, można użyć hello następujące kroki toodetermine hello magazynowania dysku puli mapowania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="fc0db-169">Dla każdego dysku Użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fc0db-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="fc0db-170">Pobranie listy dysków dołączonych tooVM z hello **Get-AzureVM** polecenia:</span><span class="sxs-lookup"><span data-stu-id="fc0db-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="fc0db-171">Get-AzureVM - ServiceName <servicename> — nazwa <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="fc0db-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="fc0db-172">Uwaga hello Diskname i jednostki LUN.</span><span class="sxs-lookup"><span data-stu-id="fc0db-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="fc0db-174">Pulpit zdalny na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="fc0db-175">Następnie przejdź zbyt**Zarządzanie komputerem** | **Menedżera urządzeń** | **dysków**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="fc0db-176">Przyjrzyj się hello właściwości każdego hello "Microsoft dysków wirtualnych"</span><span class="sxs-lookup"><span data-stu-id="fc0db-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="fc0db-178">w tym miejscu numer LUN Hello jest numer LUN toohello odwołania podane podczas podłączania hello toohello wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="fc0db-179">Dla hello "Microsoft Virtual Disk" Przejdź toohello **szczegóły** na karcie następnie hello **właściwości** listy znajduje się zbyt**klucz sterownika**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="fc0db-180">W hello **wartość**, hello Uwaga **przesunięcia**, który jest 0002 w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="fc0db-181">Witaj 0002 oznacza hello Dysk_fizyczny_2 hello odwołań do puli magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="fc0db-183">Dla każdej puli magazynów zrzutu limit hello skojarzone dyski:</span><span class="sxs-lookup"><span data-stu-id="fc0db-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="fc0db-184">Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="fc0db-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="fc0db-186">Teraz można używać tego tooassociate informacji dołączonych dysków tooPhysical wirtualnych dysków twardych w pule magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="fc0db-187">Zmapowaniu wirtualne dyski twarde tooPhysical dysków w pule magazynu można następnie odłączyć i skopiuj je za pośrednictwem tooa konta Premium Storage, a następnie dołącz je z poprawne ustawienie pamięci podręcznej w hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="fc0db-188">Zobacz przykład Witaj w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), kroki od 8 do 12.</span><span class="sxs-lookup"><span data-stu-id="fc0db-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="fc0db-189">Te kroki pokazują, jak tooextract plik wirtualnego dysku twardego maszyny Wirtualnej, dołączyć dysku konfiguracji tooa CSV kopiowanie hello wirtualne dyski twarde, zmiany ustawień pamięci podręcznej konfiguracji dysku hello i na koniec ponownie wdrożyć hello wirtualna serii DS maszyny Wirtualnej z hello wszystkie dołączone dyski.</span><span class="sxs-lookup"><span data-stu-id="fc0db-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="fc0db-190">Maszyna wirtualna magazynu przepustowość i przepływność magazynu wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="fc0db-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="fc0db-191">Witaj wydajność magazynu zależy hello rozmiar maszyny Wirtualnej DS * określone i hello rozmiary dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="fc0db-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="fc0db-192">maszyny wirtualne Hello mają różne przydziały hello liczba wirtualnych dysków twardych, które można dołączać i hello maksymalnej przepustowości, obsługują one (MB/s).</span><span class="sxs-lookup"><span data-stu-id="fc0db-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="fc0db-193">Hello przepustowości określonych liczb, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc0db-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fc0db-194">Zwiększona IOPS są osiągane o dużym rozmiarze dysku.</span><span class="sxs-lookup"><span data-stu-id="fc0db-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="fc0db-195">Należy rozważyć to Zastanawiając się ścieżki migracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="fc0db-196">Aby uzyskać szczegółowe informacje [można znaleźć tabeli hello IOPS i typów dysków](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="fc0db-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="fc0db-197">Na koniec należy rozważyć, czy maszyny wirtualne mają inny dysk maksymalnej przepustowości, które wspierają dla wszystkich dysków dołączonych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="fc0db-198">Wysokie obciążenie może nasycenia hello dysku maksymalna przepustowość dostępną dla tego rozmiaru roli maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="fc0db-199">Na przykład Standard_DS14 będzie obsługuje konto too512MB/s; w związku z tym z trzech dysków P30 można nasycenia przepustowości dysku hello hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="fc0db-200">Jednak w tym przykładzie limit przepływności hello może zostać przekroczona w zależności od różnych hello odczytu i zapisu z systemem IOs.</span><span class="sxs-lookup"><span data-stu-id="fc0db-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="fc0db-201">Nowych wdrożeń</span><span class="sxs-lookup"><span data-stu-id="fc0db-201">New deployments</span></span>
<span data-ttu-id="fc0db-202">Witaj w dwóch następnych sekcjach pokazują, jak można wdrożyć maszyn wirtualnych programu SQL Server tooPremium magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="fc0db-203">Jak wspomniano wcześniej, niekoniecznie niepotrzebne dysk systemu operacyjnego hello tooplace na magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="fc0db-204">Możesz wybrać toodo to jeśli zostanie są mają zostać tooplace żadnych intensywnych obciążeń we/wy na powitania wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc0db-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="fc0db-205">Witaj w pierwszym przykładzie pokazano, przy użyciu istniejących obrazów w galerii Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0db-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="fc0db-206">Witaj drugi przykład przedstawia sposób toouse niestandardowych maszyny Wirtualnej obrazu, który ma w istniejącego konta magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="fc0db-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-207">Tych przykładów założono, że utworzono już regionalnej sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="fc0db-208">Utwórz nową maszynę Wirtualną z magazynu Premium z galerii</span><span class="sxs-lookup"><span data-stu-id="fc0db-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="fc0db-209">w poniższym przykładzie Hello pokazuje, jak tooplace hello wirtualnego dysku twardego systemu operacyjnego na magazyn w warstwie premium i Dołącz wirtualne dyski twarde Premium magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="fc0db-210">Można jednak również umieścić hello dysk systemu operacyjnego w ramach konta Standard Storage, a następnie dołącz wirtualne dyski twarde, które znajdują się na koncie magazynu Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="fc0db-211">Przedstawiono oba scenariusze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="fc0db-212">Krok 1: Tworzenie konta magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="fc0db-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="fc0db-213">Krok 2: Tworzenie nowej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="fc0db-214">Krok 3: Reserve VIP usługi chmury (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="fc0db-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="fc0db-215">Krok 4: Tworzenie kontenera maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc0db-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="fc0db-216">Krok 5: Wprowadzenie do wirtualnego dysku twardego systemu operacyjnego na Standard lub Premium Storage</span><span class="sxs-lookup"><span data-stu-id="fc0db-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="fc0db-217">Krok 6: Tworzenie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc0db-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="fc0db-218">Utwórz nowy toouse maszyny Wirtualnej — wersja Premium magazynu z niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="fc0db-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="fc0db-219">W tym scenariuszu pokazano, gdzie masz istniejących dostosowanych obrazów, które znajdują się na koncie magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="fc0db-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="fc0db-220">Jak wspomniano, jeśli chcesz hello tooplace wirtualnego dysku twardego systemu operacyjnego na magazyn w warstwie Premium należy toocopy hello obrazu, który istnieje w hello konta Standard Storage i przenieść je tooa magazyn w warstwie Premium, zanim będzie można go używać.</span><span class="sxs-lookup"><span data-stu-id="fc0db-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="fc0db-221">Jeśli masz obrazu lokalnej, możesz także użyć tej metody toocopy który bezpośrednio toohello konta Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="fc0db-222">Krok 1: Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fc0db-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="fc0db-223">Krok 2 Tworzenie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="fc0db-224">Krok 3: Użyj istniejącego obrazu</span><span class="sxs-lookup"><span data-stu-id="fc0db-224">Step 3: Use existing image</span></span>
<span data-ttu-id="fc0db-225">Można użyć istniejącego obrazu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-225">You can use an existing image.</span></span> <span data-ttu-id="fc0db-226">Można też [zająć obraz istniejącej maszyny](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc0db-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="fc0db-227">Uwaga hello maszyny, które utworzeniem obrazu nie ma toobe DS * maszyny.</span><span class="sxs-lookup"><span data-stu-id="fc0db-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="fc0db-228">Po utworzeniu obrazu hello hello po Pokaż kroki jak toocopy on toohello konta Premium Storage z hello **Start AzureStorageBlobCopy** polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc0db-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="fc0db-229">Krok 4: Kopię Blob między kontami magazynu</span><span class="sxs-lookup"><span data-stu-id="fc0db-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="fc0db-230">Krok 5: Regularne sprawdzanie stanu kopiowania:</span><span class="sxs-lookup"><span data-stu-id="fc0db-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="fc0db-231">Krok 6: Dodawanie tooAzure repozytorium obrazu dysku w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fc0db-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="fc0db-232">Może się okazać, nawet jeśli raporty o stanie hello jako Powodzenie, można nadal uzyskanie błąd dzierżawy dysku.</span><span class="sxs-lookup"><span data-stu-id="fc0db-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="fc0db-233">W takim przypadku poczekaj około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="fc0db-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="fc0db-234">Krok 7: Tworzenie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc0db-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="fc0db-235">W tym miejscu tworzysz hello maszyny Wirtualnej z obrazu i dołączanie dwóch dysków VHD magazynu Premium:</span><span class="sxs-lookup"><span data-stu-id="fc0db-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="fc0db-236">Istniejące wdrożenia, które nie należy używać zawsze włączonych grup dostępności</span><span class="sxs-lookup"><span data-stu-id="fc0db-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="fc0db-237">Istniejące wdrożenia, najpierw Zobacz hello [wymagania wstępne](#prerequisites-for-premium-storage) tego tematu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="fc0db-238">Istnieją różne zagadnienia dotyczące wdrożenia programu SQL Server, których nie należy używać zawsze włączonych grup dostępności i tych, które wykonują.</span><span class="sxs-lookup"><span data-stu-id="fc0db-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="fc0db-239">Jeśli nie jest używana zawsze włączone i mieć istniejących autonomicznego serwera SQL, możesz uaktualnić tooPremium magazynu przy użyciu nowego konta magazyn i usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="fc0db-240">Należy wziąć pod uwagę hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="fc0db-240">Consider hello following options:</span></span>

* <span data-ttu-id="fc0db-241">**Tworzenie nowej maszyny Wirtualnej serwera SQL**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="fc0db-242">Można utworzyć nowego programu SQL Server maszynę Wirtualną, która używa konta Premium Storage, zgodnie z opisem w nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="fc0db-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="fc0db-243">Następnie kopia zapasowa i przywracanie baz danych konfiguracji i użytkownika programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fc0db-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="fc0db-244">Witaj, aplikacja musi mieć toobe zaktualizowane tooreference hello nowego programu SQL Server, gdy dostęp jest uzyskiwany wewnętrznie i zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="fc0db-245">Będzie potrzebny toocopy wszystkie obiekty "poza db" tak, jakby wcześniej zadania migracji serwera SQL (SxS) obok siebie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="fc0db-246">Obejmuje to obiekty, takie jak nazwy logowania, certyfikaty i połączone serwery.</span><span class="sxs-lookup"><span data-stu-id="fc0db-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="fc0db-247">**Migrowanie istniejących maszyn wirtualnych serwera SQL**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="fc0db-248">Będzie to wymagało przełączania w tryb offline hello maszyny Wirtualnej programu SQL Server, a następnie przenoszenia go tooa nową usługę w chmurze, która obejmuje kopiowanie wszystkich jego toohello wirtualne dyski twarde dołączonych konta Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="fc0db-249">Gdy hello maszyny Wirtualnej do trybu online, aplikacja hello będzie odwoływać hello nazwa hosta serwera jako przed.</span><span class="sxs-lookup"><span data-stu-id="fc0db-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="fc0db-250">Należy pamiętać, że rozmiar hello hello istniejącego dysku będzie miało wpływ na powitania charakterystyki wydajności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="fc0db-251">Na przykład dysk 400 GB pobiera zaokrąglona tooa P20.</span><span class="sxs-lookup"><span data-stu-id="fc0db-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="fc0db-252">Jeśli znasz nie wymagają tego wydajności dysku, można odtworzyć hello maszyny Wirtualnej jako wirtualna serii DS i Dołącz wirtualne dyski twarde specyfikacji wydajności rozmiar hello, które są wymagane na magazynu Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="fc0db-253">Następnie można odłączyć i ponownie dołączyć hello pliki bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0db-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-254">Podczas kopiowania dysków VHD hello należy pamiętać o rozmiarze hello, w zależności od wielkości hello oznacza typ dysku magazynu Premium dzielą się na, określa specyfikacji wydajności dysku.</span><span class="sxs-lookup"><span data-stu-id="fc0db-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="fc0db-255">Azure zaokrągli się toohello najbliższej dysku rozmiar, jeśli dysk GB, 400, to zostanie zaokrąglona tooa P20.</span><span class="sxs-lookup"><span data-stu-id="fc0db-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="fc0db-256">W zależności od istniejącego we/wy wymagań z hello wirtualnego dysku twardego systemu operacyjnego nie trzeba toomigrate tego tooa konta Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="fc0db-257">Jeśli program SQL Server jest dostępny zewnętrznie, VIP usługi chmury hello zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="fc0db-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="fc0db-258">Będą także mieć tooupdate punktów końcowych, listy ACL i DNS ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fc0db-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="fc0db-259">Istniejące wdrożenia, które używają zawsze włączone grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="fc0db-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="fc0db-260">Istniejące wdrożenia, najpierw Zobacz hello [wymagania wstępne](#prerequisites-for-premium-storage) tego tematu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="fc0db-261">Początkowo w tej sekcji przedstawiono, jak zawsze na współdziała z sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0db-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="fc0db-262">Firma Microsoft będzie następnie rozbić migracje w scenariuszach tootwo: migracje, w którym mogą następować Przestój i migracje, w którym należy osiągnąć minimalnym czasem przestojów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="fc0db-263">Lokalnego programu SQL Server zawsze włączonych grup dostępności Użyj odbiornika lokalnych, które rejestruje wirtualnego nazwę DNS oraz adres IP, który jest współużytkowana przez jeden lub więcej serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0db-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="fc0db-264">Jeżeli klienci łączą się routingu hello odbiornik IP toohello podstawowego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0db-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="fc0db-265">Jest to serwer hello, będący właścicielem hello zawsze na IP zasobu w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways na][6]

<span data-ttu-id="fc0db-267">W systemie Microsoft Azure może mieć tooa adres przypisany tylko jeden IP karty Sieciowej na powitania maszyny Wirtualnej, dlatego w kolejności tooachieve hello samą warstwę abstrakcji jako lokalną, hello adres IP, który jest przypisywany toohello wewnętrzne/zewnętrzne moduły równoważenia obciążenia (ILB/ELB) korzysta z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fc0db-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="fc0db-268">Witaj IP zasobu, który jest udostępniana między serwerami hello ustawiono toohello tego samego adresu IP jako hello ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="fc0db-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="fc0db-269">Ta jest publikowana w hello DNS, a ruch klientów jest przekazywana hello ILB/ELB toohello podstawowego serwera SQL repliki.</span><span class="sxs-lookup"><span data-stu-id="fc0db-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="fc0db-270">Witaj ILB/ELB wie, która programu SQL Server jest podstawowego, ponieważ używa sond tooprobe hello zawsze na IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="fc0db-271">W poprzednim przykładzie hello go sondy w każdym węźle, który ma punkt końcowy odwołuje się hello ELB/ILB, zależności odpowiada jest hello podstawowego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0db-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-272">Witaj ILB i ELB mają przypisaną tooa określonej usługi w chmurze Azure, w związku z tym wszelkie migracja do chmury na platformie Azure najprawdopodobniej oznacza że powitalne zmieni IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fc0db-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="fc0db-273">Migrowanie zawsze na wdrożenia, które umożliwiają Przestój</span><span class="sxs-lookup"><span data-stu-id="fc0db-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="fc0db-274">Istnieją dwa strategii toomigrate zawsze na wdrożenia, które umożliwiają przestój:</span><span class="sxs-lookup"><span data-stu-id="fc0db-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="fc0db-275">**Dodaj więcej tooan replikach pomocniczych istniejących zawsze na klaster**</span><span class="sxs-lookup"><span data-stu-id="fc0db-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="fc0db-276">**Migrowanie tooa nowy zawsze na klaster**</span><span class="sxs-lookup"><span data-stu-id="fc0db-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="fc0db-277">1. Dodaj więcej tooan replikach pomocniczych istniejący zawsze na klaster</span><span class="sxs-lookup"><span data-stu-id="fc0db-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="fc0db-278">Jedną ze strategii jest tooadd więcej toohello pomocnicze bazy danych zawsze włączonej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="fc0db-279">Należy tooadd na nową usługę w chmurze i zaktualizować odbiornika hello hello nowych IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fc0db-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fc0db-280">Punkty przestój:</span><span class="sxs-lookup"><span data-stu-id="fc0db-280">Points of downtime:</span></span>
* <span data-ttu-id="fc0db-281">Sprawdzanie poprawności klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-281">Cluster Validation.</span></span>
* <span data-ttu-id="fc0db-282">Test trybu failover zawsze na nowe pomocnicze bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="fc0db-283">Jeśli używane są pule magazynu systemu Windows w ramach hello maszyny Wirtualnej dla wyższej przepustowości we/wy, następnie te zostaną przełączone do trybu offline podczas pełnej weryfikacji klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="fc0db-284">test weryfikacji Hello jest wymagana podczas dodawania węzłów toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="fc0db-285">czas trwania testu hello toorun Hello może być inna, więc należy przetestować to w Twojej tooget środowiska testowego reprezentatywny Przybliżona godzina, o ile to może potrwać.</span><span class="sxs-lookup"><span data-stu-id="fc0db-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="fc0db-286">Należy udostępnić czasu, gdzie można wykonywać ręcznego przełączania trybu failover i chaos testowania na powitania nowo dodany węzłów tooensure zawsze o wysokiej dostępności funkcji, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="fc0db-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="fc0db-288">Należy zatrzymać wszystkie wystąpienia programu SQL Server, której pule magazynów hello są używane przed hello weryfikacji uruchamia.</span><span class="sxs-lookup"><span data-stu-id="fc0db-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="fc0db-289">Ogólne kroki</span><span class="sxs-lookup"><span data-stu-id="fc0db-289">High-level steps</span></span>
>

1. <span data-ttu-id="fc0db-290">Utwórz dwóch nowych serwerów SQL w nową usługę w chmurze z dołączonym magazynem Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="fc0db-291">Skopiuj przez pełne kopie zapasowe i przywracanie z **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="fc0db-292">Skopiuj za pośrednictwem "poza użytkownik bazy danych" obiekty zależne, takie jak nazwy logowania itp.</span><span class="sxs-lookup"><span data-stu-id="fc0db-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="fc0db-293">Utworzenie nowego wewnętrznego obciążenia równoważenia (ILB) lub Użyj zewnętrznego modułu równoważenia obciążenia (ELB), a następnie skonfigurować końcowych równoważenia obciążenia w obu węzłach nowego.</span><span class="sxs-lookup"><span data-stu-id="fc0db-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fc0db-294">Sprawdź, czy przed kontynuowaniem na wszystkich węzłach jest hello prawidłowej konfiguracji punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="fc0db-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="fc0db-295">Zatrzymaj toohello dostępu użytkownika/aplikacji SQL Server (Jeśli używane są pule magazynu).</span><span class="sxs-lookup"><span data-stu-id="fc0db-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="fc0db-296">Zatrzymaj usługi aparatu programu SQL Server na wszystkich węzłach (Jeśli używane są pule magazynu).</span><span class="sxs-lookup"><span data-stu-id="fc0db-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="fc0db-297">Dodaj nowe węzły toocluster i pełna weryfikacja została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fc0db-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="fc0db-298">Po sprawdzania poprawności zakończy się pomyślnie, należy uruchomić wszystkie usługi serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="fc0db-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="fc0db-299">Dzienniki transakcji i przywracania kopii zapasowych baz danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fc0db-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="fc0db-300">Dodaj nowe węzły do hello zawsze włączonej grupy dostępności i umieścić replikacji do **synchroniczne**.</span><span class="sxs-lookup"><span data-stu-id="fc0db-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="fc0db-301">Dodaj adres IP hello zasób Adres hello nowe chmury usługi ILB/ELB za pomocą programu PowerShell dla zawsze włączone oparte na przykład Witaj obejmujący wiele lokacji w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fc0db-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="fc0db-302">Usługa klastrowania systemu Windows hello zbioru **możliwych właścicieli** z hello **adres IP** zasobów toohello nowe węzły stary.</span><span class="sxs-lookup"><span data-stu-id="fc0db-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="fc0db-303">W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fc0db-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="fc0db-304">Tooone pracy awaryjnej hello nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="fc0db-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="fc0db-305">Należy hello nowe węzły automatycznej pracy awaryjnej partnerów i testy trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="fc0db-306">Usuń węzły oryginalnego z grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="fc0db-307">Zalety</span><span class="sxs-lookup"><span data-stu-id="fc0db-307">Advantages</span></span>
* <span data-ttu-id="fc0db-308">Nowe serwery SQL mogą być testowane (SQL Server i aplikacji), zanim zostaną one dodane tooAlways na.</span><span class="sxs-lookup"><span data-stu-id="fc0db-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="fc0db-309">Można zmienić rozmiar maszyny Wirtualnej hello i dostosowywać hello tooyour dokładne wymagania dotyczące magazynu w.</span><span class="sxs-lookup"><span data-stu-id="fc0db-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="fc0db-310">Jednakże może być korzystne tookeep wszystkich ścieżek plików SQL hello hello takie same.</span><span class="sxs-lookup"><span data-stu-id="fc0db-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="fc0db-311">Można kontrolować uruchomienia hello transferu toohello kopii zapasowych bazy danych hello replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="fc0db-312">Ta różni się od przy użyciu usługi Azure **Start AzureStorageBlobCopy** toocopy polecenia wirtualne dyski twarde, ponieważ jest to kopia asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="fc0db-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fc0db-313">Wady</span><span class="sxs-lookup"><span data-stu-id="fc0db-313">Disadvantages</span></span>
* <span data-ttu-id="fc0db-314">Gdy używane są pule magazynu systemu Windows, brak przestoju klastra podczas hello pełnej weryfikacji klastra dla hello nowe dodatkowe węzły.</span><span class="sxs-lookup"><span data-stu-id="fc0db-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="fc0db-315">W zależności od hello wersja programu SQL Server oraz hello istniejących liczby replik pomocniczych, możesz nie być możliwe tooadd więcej replikach pomocniczych bez usuwania istniejących replik pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="fc0db-316">Może być długi czas transferu danych SQL podczas konfigurowania hello pomocnicze bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="fc0db-317">Brak dodatkowych kosztów podczas migracji, gdy zostały uruchomione równolegle nowej maszyny.</span><span class="sxs-lookup"><span data-stu-id="fc0db-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="fc0db-318">2. Migrowanie tooa nowy zawsze na klaster</span><span class="sxs-lookup"><span data-stu-id="fc0db-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="fc0db-319">Kolejną strategią jest toocreate całkowicie nowe zawsze na klastrze z całkiem nowe węzły w nową usługę w chmurze, a następnie toouse klientom Witaj przekierowania go.</span><span class="sxs-lookup"><span data-stu-id="fc0db-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fc0db-320">Punkty przestoju</span><span class="sxs-lookup"><span data-stu-id="fc0db-320">Points of downtime</span></span>
<span data-ttu-id="fc0db-321">Brak przestoju podczas przenoszenia aplikacji i użytkowników toohello nowe zawsze na odbiornika.</span><span class="sxs-lookup"><span data-stu-id="fc0db-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="fc0db-322">Przestój Hello zależy od:</span><span class="sxs-lookup"><span data-stu-id="fc0db-322">hello downtime depends on:</span></span>

* <span data-ttu-id="fc0db-323">Witaj czas toodatabases kopie zapasowe dziennika transakcji końcowej toorestore na nowych serwerach.</span><span class="sxs-lookup"><span data-stu-id="fc0db-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="fc0db-324">Hello czas tooupdate klienta aplikacji toouse nowe zawsze na odbiornika.</span><span class="sxs-lookup"><span data-stu-id="fc0db-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="fc0db-325">Zalety</span><span class="sxs-lookup"><span data-stu-id="fc0db-325">Advantages</span></span>
* <span data-ttu-id="fc0db-326">Można przetestować środowiska produkcyjnego rzeczywiste hello, SQL Server, a zmiany kompilacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc0db-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="fc0db-327">Masz hello opcja toocustomize hello magazynu i toopotentially zmniejszyć rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="fc0db-328">Może to spowodować zmniejszenie kosztów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="fc0db-329">W trakcie tego procesu można aktualizacji kompilacji programu SQL Server lub wersji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="fc0db-330">Możesz również uaktualnić hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc0db-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="fc0db-331">powitalne poprzedniego zawsze na klastra może działać jako cel stałe wycofywania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fc0db-332">Wady</span><span class="sxs-lookup"><span data-stu-id="fc0db-332">Disadvantages</span></span>
* <span data-ttu-id="fc0db-333">Należy nazwę DNS hello toochange hello odbiornika, jeśli chcesz, aby obie zawsze na klastry z systemem jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="fc0db-334">Spowoduje to dodanie administracji obciążenie podczas migracji hello jako ciągi aplikacji klienta musi odzwierciedlać nową nazwę odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="fc0db-335">Musisz zaimplementować mechanizm synchronizacji między dwa tookeep środowisk hello, zamknij je jako jako możliwych toominimize hello wykonana końcowa synchronizacja wymagania przed migracją.</span><span class="sxs-lookup"><span data-stu-id="fc0db-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="fc0db-336">Zostanie dodany koszt podczas migracji ma hello nowego środowiska uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="fc0db-337">Migrowanie zawsze na wdrożeń minimalizująca przestoje</span><span class="sxs-lookup"><span data-stu-id="fc0db-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="fc0db-338">Minimalizująca przestoje istnieją dwa strategii migracji wdrożeń zawsze włączone:</span><span class="sxs-lookup"><span data-stu-id="fc0db-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="fc0db-339">**Korzystanie z istniejących pomocniczy: pojedynczej lokacji**</span><span class="sxs-lookup"><span data-stu-id="fc0db-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="fc0db-340">**Korzystanie z istniejących dodatkowej Replica(s): obejmujący wiele lokacji**</span><span class="sxs-lookup"><span data-stu-id="fc0db-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="fc0db-341">1. Korzystanie z istniejących pomocniczy: pojedynczej lokacji</span><span class="sxs-lookup"><span data-stu-id="fc0db-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="fc0db-342">Jedną ze strategii minimalizująca przestoje jest tootake istniejącej chmurze dodatkowej i usunąć go z hello bieżącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="fc0db-343">Następnie skopiuj hello wirtualne dyski twarde toohello nowe konto magazynu Premium i Utwórz hello maszyny Wirtualnej w hello nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="fc0db-344">Następnie zaktualizuj odbiornika hello w klaster i pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fc0db-345">Punkty przestoju</span><span class="sxs-lookup"><span data-stu-id="fc0db-345">Points of downtime</span></span>
* <span data-ttu-id="fc0db-346">Brak przestoju podczas aktualizowania hello ostatni węzeł z punktem końcowym hello o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="fc0db-347">Ponowne połączenie z klienta może być opóźnione w zależności od konfiguracji klienta/serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="fc0db-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="fc0db-348">Jeśli wybierzesz tootake hello zawsze na klastrze grupy w trybie offline tooswap się adresy IP hello jest dodatkowy Przestój.</span><span class="sxs-lookup"><span data-stu-id="fc0db-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="fc0db-349">Można tego uniknąć przy użyciu zależności lub i możliwych właścicieli hello dodany adres IP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="fc0db-350">W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fc0db-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="fc0db-351">Witaj toopartake dodanego węzła w jako zawsze na partnerski trybu Failover, należy należy tooadd punktu końcowego platformy Azure z toohello odwołania, ustaw równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fc0db-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="fc0db-352">Po uruchomieniu hello **AzureEndpoint Dodaj** polecenia toodo tego bieżącego tooremain połączenia, Otwórz, ale nowych połączeń toohello odbiornika nie będzie możliwe toobe do czasu hello modułu równoważenia obciążenia został zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="fc0db-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="fc0db-353">Podczas testowania to widziany toolast 90-120seconds, to powinno zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="fc0db-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="fc0db-354">Zalety</span><span class="sxs-lookup"><span data-stu-id="fc0db-354">Advantages</span></span>
* <span data-ttu-id="fc0db-355">Bez dodatkowych kosztów ponoszonych podczas migracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="fc0db-356">Jeden do jednego migracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-356">A one-to-one migration.</span></span>
* <span data-ttu-id="fc0db-357">Złożoności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-357">Reduced complexity.</span></span>
* <span data-ttu-id="fc0db-358">Pozwala na zwiększenie IOPS przez jednostki SKU magazynu Premium.</span><span class="sxs-lookup"><span data-stu-id="fc0db-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="fc0db-359">Jeśli strona 3rd hello dyski są odłączone od hello maszyny Wirtualnej i skopiowany toohello nową usługę w chmurze, narzędzie może być rozmiaru wirtualnego dysku twardego hello tooincrease używane, co zapewnia wyższej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="fc0db-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="fc0db-360">Aby zwiększyć rozmiar wirtualnego dysku twardego, zobacz [dyskusjach prowadzonych na forum](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="fc0db-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fc0db-361">Wady</span><span class="sxs-lookup"><span data-stu-id="fc0db-361">Disadvantages</span></span>
* <span data-ttu-id="fc0db-362">Podczas migracji jest do tymczasowej utraty wysokiej dostępności i odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="fc0db-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="fc0db-363">Jak jest to migracji 1:1, konieczne będzie toouse minimalny rozmiar maszyny Wirtualnej, która będzie obsługiwać numer wirtualne dyski twarde, więc może nie być możliwe toodownsize maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="fc0db-364">W tym scenariuszu użyje hello Azure **Start AzureStorageBlobCopy** polecenia, które jest asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="fc0db-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="fc0db-365">Na zakończenie kopiowania nie ma żadnych umowy SLA.</span><span class="sxs-lookup"><span data-stu-id="fc0db-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="fc0db-366">czas Hello kopii hello różni się podczas zależy to od oczekiwania w kolejce, również będą zależą hello ilość danych tootransfer.</span><span class="sxs-lookup"><span data-stu-id="fc0db-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="fc0db-367">czas kopiowania Hello zwiększa hello transfer jest zazwyczaj tooanother centrum danych Azure, który obsługuje magazyn w warstwie Premium w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="fc0db-368">Jeśli masz tylko węzły 2, należy wziąć pod uwagę możliwe środki zaradcze w przypadku kopiowania hello trwa dłużej niż w trakcie testów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="fc0db-369">Może to być powitania po pomysłów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="fc0db-370">Dodać tymczasowego 3 węzła programu SQL Server dla wysokiej dostępności, przed migracją hello uzgodnionych przestojów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="fc0db-371">Uruchom migrację hello poza Azure zaplanowanej konserwacji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="fc0db-372">Upewnij się, że zostały prawidłowo skonfigurowane z kworum klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="fc0db-373">Ogólne kroki</span><span class="sxs-lookup"><span data-stu-id="fc0db-373">High-level steps</span></span>
<span data-ttu-id="fc0db-374">Ten dokument nie wykazują jest przykład tooend pełną zakończenia jednak hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) zawiera szczegółowe informacje, które można wykorzystać tooperform, to.</span><span class="sxs-lookup"><span data-stu-id="fc0db-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="fc0db-376">Zbieranie konfiguracji dysku i Usuń węzeł hello (nie należy usuwać dołączonych dysków VHD).</span><span class="sxs-lookup"><span data-stu-id="fc0db-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="fc0db-377">Utwórz konto magazynu Premium i skopiuj wirtualne dyski twarde z hello konta magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="fc0db-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="fc0db-378">Utwórz nową usługę w chmurze i wdrożenie hello SQL2 maszyny Wirtualnej w tej usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="fc0db-379">Utwórz hello maszyny Wirtualnej przy użyciu hello skopiowane oryginalny wirtualny dysk twardy systemu operacyjnego i dołączanie hello skopiowane wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="fc0db-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="fc0db-380">Skonfiguruj ILB / ELB i dodać punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="fc0db-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="fc0db-381">Aktualizacja odbiornika przez:</span><span class="sxs-lookup"><span data-stu-id="fc0db-381">Update Listener by either:</span></span>
  * <span data-ttu-id="fc0db-382">Biorąc hello zawsze w grupie w trybie offline i aktualizowania hello zawsze na odbiornik o nowe ILB / adresu ELB IP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="fc0db-383">Lub dodawanie zasobu adresu IP hello z nowego chmury usługi ILB/ELB za pomocą programu PowerShell do klastra systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="fc0db-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="fc0db-384">Następnie zestaw hello możliwych właścicieli hello adresu IP zasobu toohello migracji węzła, SQL2 i Ustaw jako zależności lub w hello nazwy sieciowej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="fc0db-385">W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fc0db-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="fc0db-386">Sprawdź klientów toohello propagowania/konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="fc0db-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="fc0db-387">Migrowanie maszyny Wirtualnej SQL1 i kroków 2 – 4.</span><span class="sxs-lookup"><span data-stu-id="fc0db-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="fc0db-388">Jeśli przy użyciu kroków 5ii, Dodaj SQL1 możliwych właścicieli dla hello dodawania zasobu adresu IP</span><span class="sxs-lookup"><span data-stu-id="fc0db-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="fc0db-389">Testy trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="fc0db-390">2. Korzystanie z istniejących dodatkowej replica(s): obejmujący wiele lokacji</span><span class="sxs-lookup"><span data-stu-id="fc0db-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="fc0db-391">Jeśli niektóre węzły w więcej niż jednego centrum danych Azure (DC) lub w przypadku środowiska hybrydowego, można użyć konfiguracji zawsze włączone, w tym przestoju toominimize środowiska.</span><span class="sxs-lookup"><span data-stu-id="fc0db-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="fc0db-392">Metoda Hello jest toochange hello zawsze włączony synchronizacja tooSynchronous lokalne powitania lub dodatkowej Azure kontrolera domeny, a następnie trybu failover za pośrednictwem toothat programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fc0db-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="fc0db-393">Następnie skopiuj hello wirtualne dyski twarde tooa konta Premium Storage i Wdróż ponownie hello maszyny do nowej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fc0db-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="fc0db-394">Zaktualizuj hello odbiornika, a następnie wykonaj powrót po awarii.</span><span class="sxs-lookup"><span data-stu-id="fc0db-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fc0db-395">Punkty przestoju</span><span class="sxs-lookup"><span data-stu-id="fc0db-395">Points of downtime</span></span>
<span data-ttu-id="fc0db-396">Przestój Hello składa się z hello czasu toofailover toohello zamiast kontrolera domeny i z powrotem.</span><span class="sxs-lookup"><span data-stu-id="fc0db-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="fc0db-397">Zależy także od konfiguracji klienta/serwera DNS i ponowne połączenie z klienta mogą być opóźnione.</span><span class="sxs-lookup"><span data-stu-id="fc0db-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="fc0db-398">Należy wziąć pod uwagę hello poniższy przykład hybrydowego zawsze w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fc0db-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="fc0db-400">Zalety</span><span class="sxs-lookup"><span data-stu-id="fc0db-400">Advantages</span></span>
* <span data-ttu-id="fc0db-401">Można korzystać z istniejącej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="fc0db-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="fc0db-402">Najpierw mieć hello opcji uaktualniania toopre hello magazynu Azure na hello DR Azure kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="fc0db-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="fc0db-403">można tak skonfigurować Hello magazynu DR Azure kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="fc0db-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="fc0db-404">Brak co najmniej dwóch przechodzenia w tryb failover podczas migracji, wyłączając testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="fc0db-405">Nie należy toomove danych programu SQL Server z kopii zapasowej i przywracania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fc0db-406">Wady</span><span class="sxs-lookup"><span data-stu-id="fc0db-406">Disadvantages</span></span>
* <span data-ttu-id="fc0db-407">W zależności od tooSQL dostępu klienta serwera może występować większe opóźnienia, gdy serwer SQL jest uruchomiony w aplikacji alternatywnych toohello kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="fc0db-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="fc0db-408">Hello czasu kopiowania wirtualnych dysków twardych tooPremium przechowywania może trwać długo.</span><span class="sxs-lookup"><span data-stu-id="fc0db-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="fc0db-409">Może to mieć wpływ na na decyzję dotyczącą tego, czy tookeep hello węzła w hello grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="fc0db-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="fc0db-410">Należy wziąć pod uwagę to po dziennika pracy intensywnych obciążeń uruchomionych podczas migracji hello jest wymagane, ponieważ węzeł podstawowy hello będzie mieć tookeep hello Niezreplikowane transakcje w jego dzienniku transakcji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="fc0db-411">W związku z tym to można powiększać znacznie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="fc0db-412">W tym scenariuszu użyje hello Azure **Start AzureStorageBlobCopy** polecenia, które jest asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="fc0db-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="fc0db-413">Na zakończenie nie ma żadnych umowy dotyczącej poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="fc0db-413">There is no SLA on completion.</span></span> <span data-ttu-id="fc0db-414">Witaj czasu kopii hello różni się podczas zależy to od oczekiwania w kolejce, również będzie zależeć hello ilość tootransfer danych.</span><span class="sxs-lookup"><span data-stu-id="fc0db-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="fc0db-415">W związku z tym istnieje tylko jeden węzeł 2 centrum danych, należy podjąć kroki zaradcze w przypadku kopiowania hello trwa dłużej niż w trakcie testów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="fc0db-416">Może to być powitania po pomysłów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="fc0db-417">Dodaj węzeł tymczasowy SQL 2 dla HA przed migracją hello uzgodnionych przestojów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="fc0db-418">Uruchom migrację hello poza Azure zaplanowanej konserwacji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="fc0db-419">Upewnij się, że zostały prawidłowo skonfigurowane z kworum klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="fc0db-420">W tym scenariuszu założono, że udokumentowanych instalacji i wiedzieć odwzorowania hello magazynu w kolejności toomake zmiany ustawień pamięci podręcznej dysku optymalne.</span><span class="sxs-lookup"><span data-stu-id="fc0db-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="fc0db-421">Ogólne kroki</span><span class="sxs-lookup"><span data-stu-id="fc0db-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="fc0db-423">Upewnij się, hello lokalnymi / alternatywny hello Azure kontrolera domeny głównej serwera SQL i dołączyć je hello innych automatycznej pracy awaryjnej partnera (AFP).</span><span class="sxs-lookup"><span data-stu-id="fc0db-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="fc0db-424">Zbierz informacje o konfiguracji dysków z SQL2 i Usuń węzeł hello (nie należy usuwać dołączonych dysków VHD).</span><span class="sxs-lookup"><span data-stu-id="fc0db-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="fc0db-425">Utwórz konto magazynu Premium i skopiuj wirtualne dyski twarde z hello konta Standard Storage.</span><span class="sxs-lookup"><span data-stu-id="fc0db-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="fc0db-426">Utwórz nową usługę w chmurze a hello SQL2 maszyny Wirtualnej z jej dołączone dyski magazynu dodatków.</span><span class="sxs-lookup"><span data-stu-id="fc0db-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="fc0db-427">Skonfiguruj ILB / ELB i dodać punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="fc0db-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="fc0db-428">Aktualizacja hello zawsze na odbiornik o nowe ILB / ELB IP adres i testowania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="fc0db-429">Sprawdź konfigurację DNS hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="fc0db-430">Zmień hello AFP tooSQL2 migracji SQL1 i przejść przez kroki od 2 do 5.</span><span class="sxs-lookup"><span data-stu-id="fc0db-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="fc0db-431">Testy trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-431">Test failovers.</span></span>
* <span data-ttu-id="fc0db-432">Przełącz hello AFP tooSQL1 Wstecz i SQL2</span><span class="sxs-lookup"><span data-stu-id="fc0db-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="fc0db-433">Dodatek: Migrowanie tooPremium wdrożenia w wielu lokacjach zawsze na klaster Magazyn</span><span class="sxs-lookup"><span data-stu-id="fc0db-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="fc0db-434">Witaj pozostałej części tego tematu zawiera szczegółowy przykład konwersji obejmujący wiele lokacji zawsze na tooPremium magazynu klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="fc0db-435">Ponadto konwertuje hello odbiornika z za pomocą zewnętrznego obciążenia (ELB) usługi równoważenia tooan wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="fc0db-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="fc0db-436">Środowisko</span><span class="sxs-lookup"><span data-stu-id="fc0db-436">Environment</span></span>
* <span data-ttu-id="fc0db-437">Windows 2k 12 / SQL 2k 12</span><span class="sxs-lookup"><span data-stu-id="fc0db-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="fc0db-438">Pliki 1 DB na SP</span><span class="sxs-lookup"><span data-stu-id="fc0db-438">1 DB Files on SP</span></span>
* <span data-ttu-id="fc0db-439">2 x pule magazynu w każdym węźle</span><span class="sxs-lookup"><span data-stu-id="fc0db-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="fc0db-441">MASZYNY WIRTUALNEJ:</span><span class="sxs-lookup"><span data-stu-id="fc0db-441">VM:</span></span>
<span data-ttu-id="fc0db-442">W tym przykładzie zamierzamy toodemonstrate przenoszenie z tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="fc0db-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="fc0db-443">ELB nie była dostępna przed ILB, więc ten pokazuje, jak toothis tooswitch podczas hello migracji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="fc0db-445">Kroki przed: TooSubscription połączyć</span><span class="sxs-lookup"><span data-stu-id="fc0db-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="fc0db-446">Krok 1: Utwórz nowe konto magazynu i usługa w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="fc0db-447">Krok 2: Zwiększ hello dozwolonych błędów na zasoby<Optional></span><span class="sxs-lookup"><span data-stu-id="fc0db-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="fc0db-448">W niektórych zasobów, które należą tooyour zawsze włączonej grupy dostępności, istnieją ograniczenia na liczbę błędów, które mogą wystąpić w okresie, w którym usługa klastrowania hello podejmie grupy zasobów hello toorestart.</span><span class="sxs-lookup"><span data-stu-id="fc0db-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="fc0db-449">Zaleca się, że możesz zwiększyć to o ile Instruktaż tej procedury, ponieważ w przeciwnym razie ręcznie trybu failover i wyzwalacza przechodzenia w tryb failover przez zamknięcie maszyny można uzyskać limit toothis Zamknij.</span><span class="sxs-lookup"><span data-stu-id="fc0db-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="fc0db-450">Będzie go można toodouble rozsądne hello awarii dodatku, toodo to w Menedżerze klastra trybu Failover, przejdź toohello właściwości hello zawsze włączone grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="fc0db-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="fc0db-452">Zmień hello too6 maksymalna liczba awarii.</span><span class="sxs-lookup"><span data-stu-id="fc0db-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="fc0db-453">Krok 3: Dodawanie adresu IP zasobu dla grupy klastra<Optional></span><span class="sxs-lookup"><span data-stu-id="fc0db-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="fc0db-454">Jeśli masz tylko jeden adres IP dla hello Grupa klastra i jest wyrównany toohello chmury podsieci, należy pamiętać, jeśli przypadkowo w tryb offline wszystkich węzłów klastra w chmurze hello czy sieci, a następnie hello IP klastra zasobu i nazwa sieciowa klastra nie będzie możliwe toocome online.</span><span class="sxs-lookup"><span data-stu-id="fc0db-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="fc0db-455">W hello zdarzenia o tym, które uniemożliwi aktualizuje tooother zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="fc0db-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="fc0db-456">Krok 4: Konfiguracja DNS</span><span class="sxs-lookup"><span data-stu-id="fc0db-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="fc0db-457">tooimplement przejścia zależy od tego, jak DNS są wykorzystywane i zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="fc0db-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="fc0db-458">Zawsze włączone jest zainstalowany, tworzy grupy zasobów klastra z systemem Windows, otwórz Menedżera klastra trybu Failover, będzie mógł przeglądać czy co najmniej trzy zasoby będą dostępne, Witaj dwie hello dokument odwołuje się tooare:</span><span class="sxs-lookup"><span data-stu-id="fc0db-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="fc0db-459">Wirtualnej nazwy sieciowej (VNN) — jest to hello DNS nazwy tego klienta połączenia toowhen pożądane tooSQL tooconnect serwerach za pośrednictwem zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="fc0db-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="fc0db-460">Zasób adres IP — jest hello adresów IP skojarzonych z hello VNN, może mieć więcej niż jeden, i w wielu lokacjach konfiguracji będzie mieć adres IP według podsieci/lokacji.</span><span class="sxs-lookup"><span data-stu-id="fc0db-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="fc0db-461">Podczas łączenia tooSQL serwera i sterownik SQL Server Client hello będzie pobrać rekordy DNS hello skojarzone z odbiornika hello i spróbuj tooconnect tooeach zawsze na skojarzony adres IP, poniżej omówiono niektóre czynników, które wpływają na to.</span><span class="sxs-lookup"><span data-stu-id="fc0db-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="fc0db-462">Hello liczba równoczesnych rekordy DNS, które są skojarzone z nazwą odbiornika hello zależy nie tylko hello liczba adresów IP skojarzonych, ale hello "RegisterAllIpProviders'setting w klastrze trybu Failover dla hello zawsze ON VNN zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc0db-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="fc0db-463">Podczas wdrażania zawsze na platformie Azure istnieją inne czynności toocreate hello odbiornika i adresy IP, są toomanually skonfigurować too1 "RegisterAllIpProviders" hello, to jest wdrożenie zawsze na lokalnej różnych tooan gdzie too1 jest już ustawiona.</span><span class="sxs-lookup"><span data-stu-id="fc0db-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="fc0db-464">Jeśli "RegisterAllIpProviders" ma wartość 0, a następnie zostanie wyświetlony tylko jeden rekord DNS w systemie DNS skojarzone z hello odbiornika:</span><span class="sxs-lookup"><span data-stu-id="fc0db-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="fc0db-466">Jeśli 'RegisterAllIpProviders' to 1:</span><span class="sxs-lookup"><span data-stu-id="fc0db-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="fc0db-468">Poniższy kod Hello będzie zrzutu limit hello VNN ustawienia i ustaw ją automatycznie, należy Uwaga dla hello zmienić efekt tootake należy tootake hello VNN w trybie offline i włącz je ponownie w trybie online, biorąc to pod hello odbiornika w trybie offline powoduje klienta łączności przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="fc0db-469">W kolejnych kroków migracji konieczne będzie tooupdate hello zawsze na odbiornik o aktualizacja adresu IP, który będzie odwoływać się do modułu równoważenia obciążenia, te obejmują usunięcie zasobu adresu IP i dodawania.</span><span class="sxs-lookup"><span data-stu-id="fc0db-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="fc0db-470">Po aktualizacji IP hello należy tooensure hello nowy adres IP został zaktualizowany w strefie DNS i klientom Witaj aktualizowania ich lokalnej pamięci podręcznej DNS.</span><span class="sxs-lookup"><span data-stu-id="fc0db-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="fc0db-471">Jeśli klienci znajdują się w segmencie inną sieć i referencyjne z innego serwera DNS, należy tooconsider, co się stanie o Transfer strefy DNS podczas migracji hello jako hello aplikacji ponownego połączenia czas będzie ograniczone przez co najmniej hello czas transferu strefy żadnych nowych adresów IP dla odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="fc0db-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="fc0db-472">Podlegają ograniczenia czasu, w tym miejscu, należy omówienia i przetestować wymuszania przyrostowy transfer strefy z zespołów systemu Windows, i również umieścić hello DNS tooa rekordów hosta zmniejszyć czasu tooLive (TTL), z więc klientom Witaj aktualizację.</span><span class="sxs-lookup"><span data-stu-id="fc0db-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="fc0db-473">Aby uzyskać więcej informacji, zobacz [przyrostowych transferów stref](https://technet.microsoft.com/library/cc958973.aspx) i [Start DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc0db-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="fc0db-474">Witaj domyślny czas TTL rekord DNS, który jest skojarzony z hello odbiornika zawsze na platformie Azure to 1200 sekund.</span><span class="sxs-lookup"><span data-stu-id="fc0db-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="fc0db-475">Możesz tooreduce to jeśli podczas aktualizacji klientom Witaj tooensure migracji adresu ich DNS hello zaktualizowane protokołu IP dla odbiornika hello podlegają ograniczenia czasu.</span><span class="sxs-lookup"><span data-stu-id="fc0db-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="fc0db-476">Możesz wyświetlić i zmodyfikować konfigurację hello przez zrzucanie limit konfiguracji hello hello VNN:</span><span class="sxs-lookup"><span data-stu-id="fc0db-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="fc0db-477">Należy pamiętać, hello niższe hello "HostRecordTTL" wyższy stopień ruch DNS zostanie przeprowadzona.</span><span class="sxs-lookup"><span data-stu-id="fc0db-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="fc0db-478">Ustawienia aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="fc0db-478">Client application settings</span></span>
<span data-ttu-id="fc0db-479">Jeśli Twoje aplikacja obsługuje klienta SQL hello .net 4.5 SQLClient, możesz użyć "MULTISUBNETFAILOVER = TRUE" — słowo kluczowe, jest to zalecane toobe stosowane zgodnie z umożliwia szybsze połączenia tooSQL zawsze włączonej grupy dostępności podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="fc0db-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="fc0db-480">Wylicza wszystkie adresy IP skojarzone z hello zawsze na odbiornika równolegle i wykonuje skuteczniejsze szybkość ponów próbę połączenia TCP w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="fc0db-481">Aby uzyskać więcej informacji na temat ustawień hello powyżej, zobacz [MultiSubnetFailover — słowo kluczowe i skojarzonych z funkcji](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="fc0db-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="fc0db-482">Zobacz też [SqlClient obsługę wysokiej dostępności, odzyskiwania po awarii](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="fc0db-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="fc0db-483">Krok 5: Ustawienia kworum klastra</span><span class="sxs-lookup"><span data-stu-id="fc0db-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="fc0db-484">Jak ma toobe pobieranie co najmniej jeden serwer SQL nie działa w czasie, należy zmodyfikować konfigurację kworum klastra hello, jeśli za pomocą monitora udziału plików (FSW) z węzłami 2, należy ustawić Większość węzłów tooallow kworum hello i korzystać z dynamicznych głosowania, a to tooallow dla stałą tooremain jednego węzła.</span><span class="sxs-lookup"><span data-stu-id="fc0db-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="fc0db-485">Aby uzyskać więcej informacji dotyczących zarządzania oraz konfigurowania kworum klastra hello, zobacz [Konfigurowanie i zarządzanie kworum w klastrze pracy awaryjnej systemu Windows Server 2012 hello](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc0db-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="fc0db-486">Krok 6: Wyodrębnianie istniejące punkty końcowe i listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="fc0db-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="fc0db-487">Zapisz te tooa plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="fc0db-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="fc0db-488">Krok 7: Zmień partnerskich trybu Failover i tryby replikacji</span><span class="sxs-lookup"><span data-stu-id="fc0db-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="fc0db-489">Jeśli masz więcej niż 2 serwery SQL, możesz zmienić hello pracy awaryjnej, innym pomocniczej w innego kontrolera domeny lub too'Synchronous lokalnymi i nadać mu automatycznego partnera pracy awaryjnej (AFP), jest więc zachowują HA podczas wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="fc0db-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="fc0db-490">Można to zrobić przy użyciu języka TSQL z jednak modyfikować SSMS:</span><span class="sxs-lookup"><span data-stu-id="fc0db-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="fc0db-492">Krok 8: Usuń dodatkowej maszyny Wirtualnej z usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="fc0db-493">Należy się przygotować toomigrate chmury węzła pomocniczego, jeśli jest to obecnie podstawowego, powinien zainicjowaniu ręcznego przełączania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fc0db-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="fc0db-494">Krok 9: Zmień ustawienia w pliku CSV pamięci podręcznej dysku i Zapisz</span><span class="sxs-lookup"><span data-stu-id="fc0db-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="fc0db-495">Woluminy danych te należy ustawić tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="fc0db-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="fc0db-496">W przypadku woluminów TLOG te należy ustawić tooNONE.</span><span class="sxs-lookup"><span data-stu-id="fc0db-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="fc0db-498">Krok 10: Kopiowanie dysków VHD</span><span class="sxs-lookup"><span data-stu-id="fc0db-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="fc0db-499">Można sprawdzić stan kopiowania hello hello wirtualne dyski twarde toohello konta Premium Storage:</span><span class="sxs-lookup"><span data-stu-id="fc0db-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="fc0db-501">Poczekaj, aż wszystkie one są rejestrowane jako Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="fc0db-502">Aby uzyskać informacje dotyczące poszczególnych obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="fc0db-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="fc0db-503">Krok 11: Dysk systemu operacyjnego rejestru</span><span class="sxs-lookup"><span data-stu-id="fc0db-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="fc0db-504">Krok 12: Zaimportuj dodatkowej do nowej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fc0db-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="fc0db-505">Kod Hello poniżej również używa hello dodać opcję tutaj można zaimportować maszynę hello i korzystać z hello retainable adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="fc0db-506">Krok 13: Tworzenie ILB na nowe usługi chmury, Dodaj obciążenia zrównoważonym punktów końcowych i listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="fc0db-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="fc0db-507">Krok 14: Zawsze aktualizacji</span><span class="sxs-lookup"><span data-stu-id="fc0db-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="fc0db-509">Teraz Usuń hello starego usługi w chmurze adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="fc0db-511">Krok 15: Sprawdzanie aktualizacji DNS</span><span class="sxs-lookup"><span data-stu-id="fc0db-511">Step 15: DNS update check</span></span>
<span data-ttu-id="fc0db-512">Teraz należy sprawdzić serwery DNS w sieci klienta programu SQL Server i upewnij się, że klaster został dodany hello rekord hosta dodatkowe hello dodany adres IP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="fc0db-513">Jeśli te serwery DNS nie zostały zaktualizowane, należy wziąć pod uwagę wymuszania transferu strefy DNS i upewnij się, że hello klienci w podsieci są możliwe tooresolve tooboth zawsze na adresy IP, jest więc nie trzeba toowait automatyczne replikacja DNS.</span><span class="sxs-lookup"><span data-stu-id="fc0db-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="fc0db-514">Krok 16: Skonfiguruj ponownie zawsze na</span><span class="sxs-lookup"><span data-stu-id="fc0db-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="fc0db-515">W tym momencie poczekać hello dodatkowej tego węzła, który był migrowanych toofully ponownego zsynchronizowania jej z węzła lokalne powitania przełącznika toosynchronous węzła replikacji i stał się hello AFP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="fc0db-516">Kroku 17: Drugi węzeł migracji</span><span class="sxs-lookup"><span data-stu-id="fc0db-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="fc0db-517">Krok 18: Zmień ustawienia w pliku CSV pamięci podręcznej dysku i Zapisz</span><span class="sxs-lookup"><span data-stu-id="fc0db-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="fc0db-518">Woluminy danych te należy ustawić tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="fc0db-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="fc0db-519">W przypadku woluminów TLOG te należy ustawić tooNONE.</span><span class="sxs-lookup"><span data-stu-id="fc0db-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="fc0db-521">Krok 19: Utwórz nowe konto magazynu niezależnie od przypadku węzła pomocniczego</span><span class="sxs-lookup"><span data-stu-id="fc0db-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="fc0db-522">Krok 20: Kopiowanie dysków VHD</span><span class="sxs-lookup"><span data-stu-id="fc0db-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="fc0db-523">Można sprawdzić stan kopiowania hello wirtualnego dysku twardego dla wszystkich dysków VHD: ForEach ($disk w $diskobjects) {$lun = $disk. Jednostka LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Etykieta_dysku $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="fc0db-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="fc0db-525">Poczekaj, aż wszystkie one są rejestrowane jako Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="fc0db-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="fc0db-526">Aby uzyskać informacje dotyczące poszczególnych obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="fc0db-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="fc0db-527">Krok 21: Dysk rejestru systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="fc0db-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="fc0db-528">Krok 22: Dodawanie obciążenia zrównoważonym punktów końcowych i listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="fc0db-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="fc0db-529">Krok 23: Test trybu failover</span><span class="sxs-lookup"><span data-stu-id="fc0db-529">Step 23: Test failover</span></span>
<span data-ttu-id="fc0db-530">Należy umożliwiają teraz węzła migrowanych hello synchronizacji z lokalnymi hello zawsze na węźle, umieść go w tryb replikacji toosynchronous i poczekaj, aż został zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="fc0db-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="fc0db-531">Następnie w tryb failover z lokalnego toohello pierwszego węzła migracji, która jest hello AFP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="fc0db-532">Po którym pracuje, zmień hello ostatnio migracji AFP toohello węzła.</span><span class="sxs-lookup"><span data-stu-id="fc0db-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="fc0db-533">Należy testy trybu failover pomiędzy wszystkimi węzłami i uruchamiania, ale oczekiwano testy chaos tooensure przechodzenia w tryb failover działa jako i w odpowiednim manor.</span><span class="sxs-lookup"><span data-stu-id="fc0db-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="fc0db-534">Krok 24: Odłożyć ustawienia kworum klastra / czas wygaśnięcia DNS / Pntrs pracy awaryjnej / ustawienia synchronizacji</span><span class="sxs-lookup"><span data-stu-id="fc0db-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="fc0db-535">Dodawanie zasobu adresu IP na tej samej podsieci</span><span class="sxs-lookup"><span data-stu-id="fc0db-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="fc0db-536">Jeśli masz tylko 2 serwery SQL i chcesz toomigrate ich tooa nowe usługi chmury, ale mają tookeep hello ich w tej samej podsieci, można uniknąć, biorąc hello odbiornika zawsze w trybie offline toodelete hello oryginalnego adresu IP i dodać hello nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fc0db-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="fc0db-537">W przypadku migracji hello maszyn wirtualnych tooanother podsieci, nie należy toodo to sposób będzie sieć dodatkowe klastra, która będzie odwoływać się do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="fc0db-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="fc0db-538">Po ma włączane hello migracji pomocniczy, a także dodać hello nowego adresu IP zasobu hello nową usługę w chmurze przed trybu failover hello istniejącą główną, należy wykonać następujące czynności, w ramach hello Menedżera klastra trybu Failover:</span><span class="sxs-lookup"><span data-stu-id="fc0db-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="fc0db-539">tooadd adres IP, zobacz hello [dodatku](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), krok 14.</span><span class="sxs-lookup"><span data-stu-id="fc0db-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="fc0db-540">Hello bieżącego adresu IP zasobu, można zmienić w too'Existing możliwych właścicieli hello podstawowego serwera SQL ", w przykładzie hello poniżej"dansqlams4":</span><span class="sxs-lookup"><span data-stu-id="fc0db-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="fc0db-542">Hello nowego adresu IP zasobu, można zmienić w too'Migrated możliwych właścicieli hello pomocniczym programu SQL Server ", w przykładzie hello poniżej"dansqlams5":</span><span class="sxs-lookup"><span data-stu-id="fc0db-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="fc0db-544">Gdy ta opcja jest ustawiona można trybu failover i w przypadku migrowania hello ostatniego węzła hello możliwych właścicieli można edytować, że węzeł zostanie dodany jako możliwego właściciela:</span><span class="sxs-lookup"><span data-stu-id="fc0db-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="fc0db-546">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fc0db-546">Additional resources</span></span>
* [<span data-ttu-id="fc0db-547">Magazyn w warstwie Premium systemu Azure</span><span class="sxs-lookup"><span data-stu-id="fc0db-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="fc0db-548">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="fc0db-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="fc0db-549">SQL Server na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="fc0db-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
