---
title: "aaaLinux obliczeń maszyny wirtualne w klastrze HPC Pack | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i użyj HPC Pack klastra w systemie Azure Linux komputerowych o wysokiej wydajności (HPC) obciążeń"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="0f5b6-103">Rozpoczynanie pracy z węzłami obliczeniowymi systemu Linux w klastrze pakietu HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0f5b6-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="0f5b6-104">Konfigurowanie [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) klastra na platformie Azure, zawierającą węzła głównego z systemem Windows Server i kilka obliczeniowe węzłów z systemem obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="0f5b6-105">Poznaj opcje toomove danych między hello węzłów systemu Linux i Windows hello węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="0f5b6-106">Dowiedz się, jak toosubmit HPC systemu Linux zadania toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0f5b6-107">Na wysokim poziomie hello Poniższy diagram przedstawia klastra HPC Pack hello tworzenie i Praca z.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Klaster HPC Pack z węzłami systemu Linux][scenario]

<span data-ttu-id="0f5b6-109">Dla innych opcji toorun HPC systemu Linux obciążeń na platformie Azure, zobacz [zasobów technicznych partii i wysoką wydajność pracy](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="0f5b6-110">Wdrożenie klastra HPC Pack z węzłami obliczeniowymi systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0f5b6-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="0f5b6-111">W tym artykule przedstawiono dwie opcje toodeploy klastra HPC Pack na platformie Azure z węzłami obliczeniowymi systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="0f5b6-112">Obie metody użyć obrazu z witryny Marketplace systemu Windows Server z węzłem głównym HPC Pack toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="0f5b6-113">**Szablonu usługi Azure Resource Manager** -Użyj szablonu z portalu Azure Marketplace hello, lub w szablonie Szybki Start społeczność hello, tooautomate tworzenia klastra hello w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="0f5b6-114">Na przykład Witaj [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w hello Azure Marketplace tworzy pełną infrastruktura klastra HPC Pack dla systemu Linux HPC obciążeń.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="0f5b6-115">**Skrypt programu PowerShell** -Użyj hello [skrypt wdrożenia Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**HpcIaaSCluster.ps1 nowy**) tooautomate wdrożenia całego klastra w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="0f5b6-116">Ten skrypt programu PowerShell usługi Azure używa obrazu maszyny Wirtualnej programu HPC Pack w hello Azure Marketplace do szybkiego wdrożenia i zapewnia rozbudowany zestaw toodeploy parametry konfiguracji węzły obliczeniowe systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="0f5b6-117">Aby uzyskać więcej informacji dotyczących opcji wdrażania klastrów HPC Pack na platformie Azure, zobacz [opcje toocreate i zarządzać klastrem wysokiej wydajności (HPC) na platformie Azure z pakietem Microsoft HPC](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0f5b6-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f5b6-118">Prerequisites</span></span>
* <span data-ttu-id="0f5b6-119">**Subskrypcja platformy Azure** -subskrypcji można używać w obu hello usługi Azure globalnym, ani w chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="0f5b6-120">Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="0f5b6-121">**Limit przydziału rdzeni** — może być konieczne tooincrease hello przydziału rdzeni, zwłaszcza jeśli toodeploy kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="0f5b6-122">tooincrease limit przydziału, otwórz żądanie pomocy technicznej online klienta bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="0f5b6-123">**Dystrybucje systemu Linux** — obecnie HPC Pack obsługuje powitania po dystrybucje systemu Linux dla węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="0f5b6-124">Użyj wersji Marketplace tych dystrybucji, jeśli jest on dostępny lub Podaj własny.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="0f5b6-125">**Na podstawie centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="0f5b6-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="0f5b6-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="0f5b6-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="0f5b6-127">**SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium), SLES 12 z dodatkiem SP1, SLES 12 z dodatkiem SP1 (Premium), SLES 12 dla HPC, SLES 12 dla HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="0f5b6-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="0f5b6-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="0f5b6-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="0f5b6-129">toouse hello Azure RDMA sieć z jedną rozmiarów maszyn wirtualnych z funkcją RDMA hello, Określ obraz systemu SUSE Linux Enterprise Server 12 HPC lub na podstawie CentOS HPC z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="0f5b6-130">Aby uzyskać więcej informacji, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="0f5b6-131">Dodatkowe wymagania wstępne toodeploy hello klastra za pomocą skryptu wdrażania HPC Pack IaaS hello:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="0f5b6-132">**Komputer kliencki** — należy skryptu wdrażania klienta z systemem Windows komputera toorun hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="0f5b6-133">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="0f5b6-134">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="0f5b6-135">Można sprawdzić wersji hello skryptu hello uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="0f5b6-136">Ten artykuł jest oparty na wersji 4.4.1 lub nowszej hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="0f5b6-137">Opcja wdrażania 1.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-137">Deployment option 1.</span></span> <span data-ttu-id="0f5b6-138">Użyj szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f5b6-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="0f5b6-139">Przejdź toohello [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w hello Azure Marketplace, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="0f5b6-140">W portalu Azure hello, przejrzyj informacje hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Tworzenie portalu][portal]
3. <span data-ttu-id="0f5b6-142">Na powitania **podstawy** bloku, wprowadź nazwę klastra hello, który także nazwy węzła głównego hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="0f5b6-143">Możesz wybrać istniejącą grupę zasobów lub Utwórz grupę wdrożenia hello w lokalizacji, która jest dostępna tooyou.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="0f5b6-144">Witaj lokalizacji ma wpływ na dostępność hello niektórych rozmiarów maszyn wirtualnych i innymi usługami Azure (zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="0f5b6-145">Na powitania **przejdź do węzła ustawienia** bloku, w przypadku pierwszego wdrożenia zazwyczaj można zaakceptować ustawienia domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f5b6-146">Witaj **adresu URL skryptu pokonfiguracyjnego** jest opcjonalne ustawienie toospecify publicznie dostępnych skrypt programu Windows PowerShell, które mają toorun na powitania węzła głównego maszyny Wirtualnej po jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="0f5b6-147">Na powitania **obliczeniowe węzła ustawienia** bloku, wybierz wzorzec nazewnictwa dla węzłów hello, hello liczby i rozmiaru hello węzłów i hello toodeploy dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="0f5b6-148">Na powitania **ustawienia infrastruktury** bloku, wprowadź nazwy sieci wirtualnej hello i usługi Active Directory domeny, domeny i poświadczenia administratora maszyny Wirtualnej i wzorzec nazewnictwa hello kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0f5b6-149">HPC Pack używa hello — użytkownicy klastra tooauthenticate domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="0f5b6-150">Po uruchomieniu testów sprawdzania poprawności hello i przejrzyj hello warunki użytkowania, kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="0f5b6-151">Opcja wdrażania 2.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-151">Deployment option 2.</span></span> <span data-ttu-id="0f5b6-152">Użyj skryptu wdrożenia IaaS hello</span><span class="sxs-lookup"><span data-stu-id="0f5b6-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="0f5b6-153">Poniżej przedstawiono dodatkowe wymagania wstępne toodeploy hello klastra za pomocą skryptu wdrażania HPC Pack IaaS hello:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="0f5b6-154">**Komputer kliencki** — należy skryptu wdrażania klienta z systemem Windows komputera toorun hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="0f5b6-155">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="0f5b6-156">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="0f5b6-157">Można sprawdzić wersji hello skryptu hello uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="0f5b6-158">Ten artykuł jest oparty na wersji 4.4.1 lub nowszej hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="0f5b6-159">**Plik konfiguracji XML**</span><span class="sxs-lookup"><span data-stu-id="0f5b6-159">**XML configuration file**</span></span>

<span data-ttu-id="0f5b6-160">Hello skrypt wdrożenia HPC Pack IaaS używa pliku konfiguracji XML jako klaster HPC hello toodescribe wejściowego.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="0f5b6-161">Witaj następujący przykładowy plik konfiguracyjny określa mały składające się z węzłem głównym HPC Pack i dwa węzły obliczeniowe A7 CentOS 7.0 Linux rozmiar klastra.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="0f5b6-162">Zmodyfikuj plik hello odpowiednio dla swojego środowiska i konfiguracji klastra, a następnie zapisz plik z nazwą, takich jak HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="0f5b6-163">Na przykład należy toosupply nazwę subskrypcji i nazwy konta magazynu unikatowy i nazwa usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="0f5b6-164">Ponadto można toochoose innej obsługiwane Linux obrazu dla węzłów obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="0f5b6-165">Aby uzyskać więcej informacji o elementach hello w pliku konfiguracyjnym hello, zobacz hello Manual.rtf plik w folderze skryptów hello i [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="0f5b6-166">**Witaj toorun skrypt wdrożenia HPC Pack IaaS**</span><span class="sxs-lookup"><span data-stu-id="0f5b6-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="0f5b6-167">Otwórz program Windows PowerShell na komputerze klienckim hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="0f5b6-168">Zmień folder toohello katalogu, w którym skrypt hello jest zainstalowany (E:\IaaSClusterScript w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="0f5b6-169">Uruchom powitania po klastra HPC Pack hello toodeploy polecenia.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="0f5b6-170">W tym przykładzie przyjęto założenie, że ten plik konfiguracji hello znajduje się w E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="0f5b6-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="0f5b6-171">a.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-171">a.</span></span> <span data-ttu-id="0f5b6-172">Ponieważ hello **AdminPassword** nie jest określona w hello poprzedzających polecenia, są hello tooenter zostanie wyświetlony monit o hasło użytkownika *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="0f5b6-173">b.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-173">b.</span></span> <span data-ttu-id="0f5b6-174">skrypt Hello następnie uruchamia plik konfiguracji hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="0f5b6-175">Tooseveral minut w zależności od połączenia sieciowego hello może potrwać.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Walidacja][validate]
   
    <span data-ttu-id="0f5b6-177">c.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-177">c.</span></span> <span data-ttu-id="0f5b6-178">Po operacji sprawdzania poprawności przekazać, skrypt hello wymieniono toocreate zasobów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="0f5b6-179">Wprowadź *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-179">Enter *Y* toocontinue.</span></span>
   
    ![Zasoby][resources]
   
    <span data-ttu-id="0f5b6-181">d.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-181">d.</span></span> <span data-ttu-id="0f5b6-182">skrypt Hello uruchamia klastra HPC Pack hello toodeploy i zakończeniu konfiguracji hello bez dalszego wymagane ręczne wykonanie czynności.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="0f5b6-183">skrypt Hello może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-183">hello script can run for several minutes.</span></span>
   
    ![Wdrażanie][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="0f5b6-185">W tym przykładzie hello skrypt generuje plik dziennika automatycznie od hello **- LogFile** parametr nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="0f5b6-186">Dzienniki Hello nie są zapisywane w czasie rzeczywistym, ale są zbierane na końcu hello hello weryfikacji i hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="0f5b6-187">Po zatrzymaniu hello proces PowerShell uruchomionej skryptu hello niektórych dzienników zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="0f5b6-188">Połącz toohello węzła głównego</span><span class="sxs-lookup"><span data-stu-id="0f5b6-188">Connect toohello head node</span></span>
<span data-ttu-id="0f5b6-189">Po wdrożeniu klastra HPC Pack hello na platformie Azure, [połączenia przez pulpit zdalny](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello węzła głównego maszynę Wirtualną przy użyciu hello podana podczas wdrażania klastra hello poświadczeń domeny (na przykład *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="0f5b6-190">Witaj klastra można zarządzać z węzła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="0f5b6-191">Na powitania węzła głównego Uruchom Menedżera klastra HPC toocheck hello stan klastra HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="0f5b6-192">Można zarządzać i monitorować węzły obliczeniowe Linux hello taki sam sposób pracy z systemem Windows węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="0f5b6-193">Na przykład, zobacz hello Linux węzły na liście **zarządzanie zasobami** (te węzły zostały wdrożone za pomocą hello **LinuxNode** szablonu).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Zarządzanie węzła][management]

<span data-ttu-id="0f5b6-195">Zobacz też węzłów Linux hello hello **Mapa cieplna** widoku.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Mapa cieplna][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="0f5b6-197">Jak dane toomove w klastrze z węzłami systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0f5b6-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="0f5b6-198">Masz kilka opcji toomove danych między węzłami systemu Linux i Windows hello węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="0f5b6-199">Poniżej przedstawiono trzy typowe metody opisane bardziej szczegółowo w hello następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="0f5b6-200">**Plików na platformę Azure** -ujawnia zarządzanych danych toostore udziałów plików SMB plików w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="0f5b6-201">Węzłów z systemem Windows i Linux węzłów mogą zainstalować udziały plików platformy Azure jako dysku lub folderu na powitania czasu takie same, nawet jeśli są one wdrożone w różnych sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="0f5b6-202">**Udział SMB węzła głównego** — instaluje standardowe folder udostępniony systemu Windows hello węzła głównego w węzłach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="0f5b6-203">**Serwer systemu plików NFS węzła HEAD** — zapewnia rozwiązanie do udostępniania plików w środowisku mieszanym Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="0f5b6-204">Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="0f5b6-204">Azure File storage</span></span>
<span data-ttu-id="0f5b6-205">Witaj [plików Azure](https://azure.microsoft.com/services/storage/files/) udziałami plików przy użyciu standardowego protokołu SMB 2.1 hello udostępnia usługi.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="0f5b6-206">Maszyny wirtualne platformy Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji mają dostęp do danych plików w udziale za pośrednictwem hello interfejsu API magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="0f5b6-207">Aby uzyskać szczegółowy opis kroków toocreate plików Azure udziału i zainstalować go na powitania węzła głównego, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="0f5b6-208">udział plików Azure hello toomount hello węzłach Linux, zobacz [jak toouse magazyn plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="0f5b6-209">Zobacz tooset utrwalanie połączenia [Persisting tooMicrosoft połączenia usługi pliki Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="0f5b6-210">W hello poniższy przykład należy utworzyć udział plików Azure na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="0f5b6-211">Witaj toomount udział na powitania węzła głównego, otwórz wiersz polecenia i wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="0f5b6-212">W tym przykładzie allvhdsje to nazwa konta magazynu, storageaccountkey jest klucz konta magazynu, a funkcja rdma jest nazwa udziału plików Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="0f5b6-213">udział plików Azure Hello jest zainstalowany jako Z: hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="0f5b6-214">udział plików Azure hello toomount w węzłach Linux, uruchom **clusrun** na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="0f5b6-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  jest przydatne toocarry narzędzie HPC Pack zadania administracyjne na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="0f5b6-216">(Zobacz też [Clusrun dla systemu Linux węzłów](#Clusrun-for-Linux-nodes) w tym artykule.)</span><span class="sxs-lookup"><span data-stu-id="0f5b6-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="0f5b6-217">Otwórz okno programu Windows PowerShell i wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="0f5b6-218">pierwsze polecenie Hello tworzy folder o nazwie /rdma we wszystkich węzłach grupy LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="0f5b6-219">drugie polecenie Hello instaluje allvhdsjw.file.core.windows.net/rdma udział plików Azure hello na powitania /rdma folder o dir i plików trybu too777 zestawu usługi bits.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="0f5b6-220">W hello drugiego polecenia allvhdsje jest nazwa konta magazynu i storageaccountkey jest klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="0f5b6-221">Witaj "\\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="0f5b6-222">"\\`,"oznacza, że hello"," (przecinek znak) jest częścią polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="0f5b6-223">Udział węzła głównego</span><span class="sxs-lookup"><span data-stu-id="0f5b6-223">Head node share</span></span>
<span data-ttu-id="0f5b6-224">Można również zainstalować hello węzła głównego folderu udostępnionego na węzłach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="0f5b6-225">Udział zapewnia hello najprostszy sposób tooshare plików, ale hello węzła głównego i na wszystkich węzłach Linux, musi być wdrażana w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="0f5b6-226">Poniżej przedstawiono kroki hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-226">Here are hello steps.</span></span>

1. <span data-ttu-id="0f5b6-227">Utwórz folder na powitania węzła głównego i udostępniać je tooEveryone uprawnienia odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="0f5b6-228">Na przykład udostępnić D:\OpenFOAM na powitania węzła głównego jako \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="0f5b6-229">W tym miejscu CentOS7RDMA HN jest hostname hello hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Uprawnienia do udziału plików][fileshareperms]
   
    ![Udostępnianie plików][filesharing]
2. <span data-ttu-id="0f5b6-232">Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="0f5b6-233">pierwsze polecenie Hello tworzy folder o nazwie /openfoam we wszystkich węzłach grupy LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="0f5b6-234">drugie polecenie Hello instaluje hello udostępnionego folderu //CentOS7RDMA-HN/OpenFOAM na powitania folder o dir i plików trybu too777 zestawu usługi bits.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="0f5b6-235">Witaj nazwę użytkownika i hasło w poleceniu hello powinna być hello nazwę użytkownika i hasło użytkownika klastra na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="0f5b6-236">(Zobacz [Dodaj lub usuń użytkowników klastra](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="0f5b6-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="0f5b6-237">Witaj "\\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="0f5b6-238">"\\`,"oznacza, że hello"," (przecinek znak) jest częścią polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="0f5b6-239">Serwer systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="0f5b6-239">NFS server</span></span>
<span data-ttu-id="0f5b6-240">Witaj usługi systemu plików NFS pozwala tooshare oraz migrację plików na komputerach przy użyciu protokołu SMB hello systemem operacyjnym hello systemu Windows Server 2012 i opartych na systemie Linux przy użyciu protokołu NFS hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="0f5b6-241">Witaj serwer systemu plików NFS i inne węzły mają toobe wdrożone w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="0f5b6-242">Zapewnia lepszą zgodność z węzłami systemu Linux w porównaniu z udziału SMB.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="0f5b6-243">Na przykład obsługuje łącza do plików.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="0f5b6-244">tooinstall i skonfigurować serwer NFS, wykonaj kroki hello w [serwera dla systemu pierwszego udziału sieciowego na całej trasie](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="0f5b6-245">Na przykład można utworzyć udziału NFS o nazwie systemu plików nfs, ze hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autoryzacja systemu plików NFS][nfsauth]
   
    ![Uprawnienia udziału NFS][nfsshare]
   
    ![Uprawnienia NTFS systemu plików NFS][nfsperm]
   
    ![Właściwości zarządzania systemu plików NFS][nfsmanage]
2. <span data-ttu-id="0f5b6-250">Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="0f5b6-251">pierwsze polecenie Hello tworzy folder o nazwie /nfsshared we wszystkich węzłach grupy LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="0f5b6-252">Witaj drugiego polecenia hello instalacji NFS udostępnianie CentOS7RDMA HN: / systemu plików nfs na hello folderu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="0f5b6-253">W tym miejscu CentOS7RDMA HN: / systemu plików nfs jest hello zdalnego ścieżka udziału NFS.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="0f5b6-254">Jak toosubmit zadania</span><span class="sxs-lookup"><span data-stu-id="0f5b6-254">How toosubmit jobs</span></span>
<span data-ttu-id="0f5b6-255">Istnieje kilka sposobów toosubmit zadania toohello HPC Pack klastra:</span><span class="sxs-lookup"><span data-stu-id="0f5b6-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="0f5b6-256">Menedżer klastrów HPC lub Menedżer zadań klastra HPC graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="0f5b6-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="0f5b6-257">Portalu internetowego HPC</span><span class="sxs-lookup"><span data-stu-id="0f5b6-257">HPC web portal</span></span>
* <span data-ttu-id="0f5b6-258">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="0f5b6-258">REST API</span></span>

<span data-ttu-id="0f5b6-259">Przesyłanie zadań do klastra toohello na platformie Azure za pomocą narzędzia HPC Pack graficznego interfejsu użytkownika i portalu internetowego HPC hello są hello takie same jak w przypadku systemu Windows węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="0f5b6-260">Zobacz [Menedżer zadań klastra HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) i [jak toosubmit zadania z komputera klienckiego lokalnymi](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0f5b6-261">zadania toosubmit za pośrednictwem interfejsu API REST, hello odwoływać się za[tworzenie i przesyłanie zadań za pomocą interfejsu API REST w Microsoft HPC Pack hello](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="0f5b6-262">zadania toosubmit w kliencie systemu Linux można znaleźć próbki Python toohello w hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="0f5b6-263">Clusrun dla węzłów systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0f5b6-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="0f5b6-264">Witaj HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) narzędzie może być używane tooexecute poleceń w węzłach systemu Linux przy użyciu wiersza polecenia lub Menedżer klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="0f5b6-265">Poniżej przedstawiono niektóre podstawowe przykłady.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-265">Following are some basic examples.</span></span>

* <span data-ttu-id="0f5b6-266">Pokaż bieżącej nazwy użytkownika na wszystkich węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="0f5b6-267">Zainstaluj hello **gdb** narzędzie debugera z **yum** we wszystkich węzłach hello linuxnodes grupy, a następnie ponownie uruchom węzłów powitania po 10 minutach.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="0f5b6-268">Utwórz skrypt powłoki wyświetlania każdej liczby od 1 do 10 sekundy jeden w każdym węźle systemu Linux w klastrze hello, uruchom go i natychmiast wyświetlane dane wyjściowe z węzłów hello.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="0f5b6-269">Może być konieczne toouse escape niektórych znaków w **clusrun** poleceń.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="0f5b6-270">Jak pokazano w tym przykładzie, użyj ^ w hello tooescape wiersza polecenia ">" symbolu.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0f5b6-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f5b6-271">Next steps</span></span>
* <span data-ttu-id="0f5b6-272">Spróbuj skalowaniu hello klastra tooa większą liczbę węzłów lub działających obciążeń systemu Linux na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="0f5b6-273">Na przykład zobacz [Uruchom NAMD z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="0f5b6-274">Spróbuj klaster z [maszyn wirtualnych z funkcją RDMA, obliczeniowych](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI obciążeń.</span><span class="sxs-lookup"><span data-stu-id="0f5b6-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="0f5b6-275">Na przykład zobacz [klastra uruchom OpenFOAM z pakietem Microsoft HPC na RDMA systemu Linux na platformie Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="0f5b6-276">Jeśli interesuje Cię w pracy z Linux węzłów w klastrze HPC Pack lokalnych, zobacz hello [wskazówki TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f5b6-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
