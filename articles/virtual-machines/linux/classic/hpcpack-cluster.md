---
title: "Linux obliczeń maszyny wirtualne w klastrze HPC Pack | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i używać klastra HPC Pack Linux komputerowych o wysokiej wydajności (HPC) obciążeń na platformie Azure"
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
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="7857d-103">Rozpoczynanie pracy z węzłami obliczeniowymi systemu Linux w klastrze pakietu HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7857d-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="7857d-104">Konfigurowanie [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) klastra na platformie Azure, zawierającą węzła głównego z systemem Windows Server i kilka obliczeniowe węzłów z systemem obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7857d-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="7857d-105">Poznaj opcje przenoszenia danych między węzły systemu Linux i Windows węzłem głównym klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="7857d-106">Dowiedz się, jak można przesłać zadań HPC systemu Linux do klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7857d-107">Na wysokim poziomie na poniższym diagramie przedstawiono klastra HPC Pack, tworzenie i Praca z.</span><span class="sxs-lookup"><span data-stu-id="7857d-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![Klaster HPC Pack z węzłami systemu Linux][scenario]

<span data-ttu-id="7857d-109">Inne opcje do uruchamiania obciążeń HPC systemu Linux na platformie Azure, zobacz [zasobów technicznych partii i wysoką wydajność pracy](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7857d-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="7857d-110">Wdrożenie klastra HPC Pack z węzłami obliczeniowymi systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7857d-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="7857d-111">W tym artykule przedstawiono się, że możesz dwie opcje do wdrożenia klastra HPC Pack na platformie Azure z systemem Linux węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="7857d-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="7857d-112">Obie metody za pomocą obrazu systemu Windows Server z witryny Marketplace HPC Pack można utworzyć węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="7857d-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="7857d-113">**Szablonu usługi Azure Resource Manager** -Użyj szablonu z portalu Azure Marketplace, lub w szablonie Szybki Start od społeczności, można zautomatyzować tworzenie klastra w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7857d-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="7857d-114">Na przykład [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w portalu Azure Marketplace tworzy pełną infrastruktura klastra HPC Pack dla systemu Linux HPC obciążeń.</span><span class="sxs-lookup"><span data-stu-id="7857d-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="7857d-115">**Skrypt programu PowerShell** -użyj [skrypt wdrożenia Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**HpcIaaSCluster.ps1 nowy**) można zautomatyzować wdrożenie całego klastra w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7857d-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="7857d-116">Ten skrypt programu PowerShell usługi Azure używa obrazu maszyny Wirtualnej pakietu HPC w portalu Azure Marketplace do szybkiego wdrożenia i zapewnia rozbudowany zestaw parametrów konfiguracji, aby wdrożyć węzły obliczeniowe systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7857d-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="7857d-117">Aby uzyskać więcej informacji dotyczących opcji wdrażania klastrów HPC Pack na platformie Azure, zobacz [opcje tworzenia i zarządzania nimi, przetwarzanie o wysokiej wydajności (HPC) klastra na platformie Azure z pakietem Microsoft HPC](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7857d-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7857d-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7857d-118">Prerequisites</span></span>
* <span data-ttu-id="7857d-119">**Subskrypcja platformy Azure** — można użyć subskrypcji w usłudze Azure globalne lub chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7857d-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="7857d-120">Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7857d-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="7857d-121">**Limit przydziału rdzeni** — należy zwiększyć limit przydziału rdzeni, zwłaszcza, jeśli użytkownik chce wdrożyć kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7857d-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="7857d-122">Aby zwiększyć limit przydziału, otwórz żądanie pomocy technicznej online klienta bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="7857d-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="7857d-123">**Dystrybucje systemu Linux** — obecnie HPC Pack obsługuje następujące dystrybucje systemu Linux dla węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="7857d-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="7857d-124">Użyj wersji Marketplace tych dystrybucji, jeśli jest on dostępny lub Podaj własny.</span><span class="sxs-lookup"><span data-stu-id="7857d-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="7857d-125">**Na podstawie centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="7857d-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="7857d-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="7857d-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="7857d-127">**SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium), SLES 12 z dodatkiem SP1, SLES 12 z dodatkiem SP1 (Premium), SLES 12 dla HPC, SLES 12 dla HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="7857d-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="7857d-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="7857d-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="7857d-129">Aby użyć sieciowych Azure RDMA z jednym rozmiary maszyny Wirtualnej z funkcją RDMA, podaj SUSE Linux Enterprise Server 12 HPC lub na podstawie CentOS HPC obrazu z portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7857d-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="7857d-130">Aby uzyskać więcej informacji, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7857d-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="7857d-131">Dodatkowe wymagania wstępne dotyczące wdrażania klastra za pomocą skryptu wdrażania HPC Pack IaaS:</span><span class="sxs-lookup"><span data-stu-id="7857d-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="7857d-132">**Komputer kliencki** — należy komputer kliencki z systemem Windows uruchom skrypt wdrażania klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="7857d-133">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="7857d-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="7857d-134">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj najnowszej wersji skryptu z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="7857d-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="7857d-135">Wersja skryptu można sprawdzić, uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="7857d-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="7857d-136">Ten artykuł jest oparty na wersji 4.4.1 lub nowszej skryptu.</span><span class="sxs-lookup"><span data-stu-id="7857d-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="7857d-137">Opcja wdrażania 1.</span><span class="sxs-lookup"><span data-stu-id="7857d-137">Deployment option 1.</span></span> <span data-ttu-id="7857d-138">Użyj szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7857d-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="7857d-139">Przejdź do [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w portalu Azure Marketplace, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="7857d-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="7857d-140">W portalu Azure, przejrzyj informacje, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7857d-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Tworzenie portalu][portal]
3. <span data-ttu-id="7857d-142">Na **podstawy** bloku, wprowadź nazwę klastra, który także nazwy węzła głównego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7857d-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="7857d-143">Można wybrać istniejącą grupę zasobów lub Utwórz grupę wdrożenia w lokalizacji, która jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="7857d-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="7857d-144">Lokalizacja ma wpływ na dostępność niektórych rozmiarów maszyn wirtualnych i innymi usługami Azure (zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="7857d-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="7857d-145">Na **przejdź do węzła ustawienia** bloku, w przypadku pierwszego wdrożenia zazwyczaj można zaakceptować ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="7857d-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7857d-146">**Adresu URL skryptu pokonfiguracyjnego** jest ustawienie opcjonalne, aby określić publicznie dostępnych skrypt programu Windows PowerShell, który ma zostać uruchomione w węźle głównym maszyny Wirtualnej po jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="7857d-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="7857d-147">Na **obliczeniowe węzła ustawienia** bloku, wybierz wzorzec nazewnictwa dla węzłów, liczby i rozmiaru węzły i dystrybucja systemu Linux do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7857d-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="7857d-148">Na **ustawienia infrastruktury** bloku nazwy sieci wirtualnej i usługi Active Directory wprowadź domenę, domeny i poświadczenia administratora maszyny Wirtualnej i wzorzec nazewnictwa dla kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="7857d-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7857d-149">Do uwierzytelniania użytkowników klastra HPC Pack używane do domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7857d-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="7857d-150">Po uruchomieniu testów sprawdzania poprawności i zapoznaj się z warunkami użytkowania, kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="7857d-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="7857d-151">Opcja wdrażania 2.</span><span class="sxs-lookup"><span data-stu-id="7857d-151">Deployment option 2.</span></span> <span data-ttu-id="7857d-152">Użyj skryptu wdrożenia IaaS</span><span class="sxs-lookup"><span data-stu-id="7857d-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="7857d-153">Poniżej przedstawiono dodatkowe wymagania wstępne dotyczące wdrażania klastra za pomocą skryptu wdrażania HPC Pack IaaS:</span><span class="sxs-lookup"><span data-stu-id="7857d-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="7857d-154">**Komputer kliencki** — należy komputer kliencki z systemem Windows uruchom skrypt wdrażania klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="7857d-155">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="7857d-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="7857d-156">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj najnowszej wersji skryptu z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="7857d-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="7857d-157">Wersja skryptu można sprawdzić, uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="7857d-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="7857d-158">Ten artykuł jest oparty na wersji 4.4.1 lub nowszej skryptu.</span><span class="sxs-lookup"><span data-stu-id="7857d-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="7857d-159">**Plik konfiguracji XML**</span><span class="sxs-lookup"><span data-stu-id="7857d-159">**XML configuration file**</span></span>

<span data-ttu-id="7857d-160">Skrypt wdrażania HPC Pack IaaS używa pliku konfiguracji XML jako dane wejściowe do opisywania klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="7857d-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="7857d-161">Przykładowy plik konfiguracyjny określa mały składające się z węzłem głównym HPC Pack i dwa węzły obliczeniowe A7 CentOS 7.0 Linux rozmiar klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="7857d-162">Zmodyfikuj odpowiednio dla swojego środowiska i konfiguracji klastra, a następnie zapisz plik z nazwą, takich jak HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="7857d-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="7857d-163">Na przykład należy podać nazwę subskrypcji i nazwy konta magazynu unikatowy i nazwa usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7857d-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="7857d-164">Ponadto można wybrać inny obraz systemu Linux obsługiwane dla węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="7857d-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="7857d-165">Aby uzyskać więcej informacji na temat elementów w pliku konfiguracji, zobacz plik Manual.rtf w folderze skryptów i [utworzyć klaster HPC z skrypt wdrożenia HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7857d-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="7857d-166">**Aby uruchomić skrypt wdrażania HPC Pack IaaS**</span><span class="sxs-lookup"><span data-stu-id="7857d-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="7857d-167">Jako administrator Otwórz program Windows PowerShell na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="7857d-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="7857d-168">Zmień katalog na folder, w którym skrypt jest zainstalowany (E:\IaaSClusterScript w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="7857d-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="7857d-169">Uruchom następujące polecenie, aby wdrożyć klaster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="7857d-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="7857d-170">W tym przykładzie przyjęto założenie, że plik konfiguracji znajduje się w E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="7857d-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="7857d-171">a.</span><span class="sxs-lookup"><span data-stu-id="7857d-171">a.</span></span> <span data-ttu-id="7857d-172">Ponieważ **AdminPassword** nie została określona w poprzednim poleceniu, zostanie wyświetlony monit o wprowadzenie hasła dla użytkownika *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="7857d-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="7857d-173">b.</span><span class="sxs-lookup"><span data-stu-id="7857d-173">b.</span></span> <span data-ttu-id="7857d-174">Skrypt uruchamia następnie można sprawdzić poprawności pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7857d-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="7857d-175">Może potrwać kilka minut w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7857d-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Walidacja][validate]
   
    <span data-ttu-id="7857d-177">c.</span><span class="sxs-lookup"><span data-stu-id="7857d-177">c.</span></span> <span data-ttu-id="7857d-178">Po operacji sprawdzania poprawności przekazać, skrypt zawiera listę zasobów klastra do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="7857d-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="7857d-179">Wprowadź *Y* aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="7857d-179">Enter *Y* to continue.</span></span>
   
    ![Zasoby][resources]
   
    <span data-ttu-id="7857d-181">d.</span><span class="sxs-lookup"><span data-stu-id="7857d-181">d.</span></span> <span data-ttu-id="7857d-182">Skrypt rozpocznie wdrażanie klastra HPC Pack i kończy działanie konfiguracji bez dalszego wymagane ręczne wykonanie czynności.</span><span class="sxs-lookup"><span data-stu-id="7857d-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="7857d-183">Skrypt może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7857d-183">The script can run for several minutes.</span></span>
   
    ![Wdrażanie][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="7857d-185">W tym przykładzie skrypt generuje plik dziennika automatycznie ponieważ **- LogFile** parametr nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="7857d-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="7857d-186">Dzienniki nie są zapisywane w czasie rzeczywistym, ale są zbierane na końcu sprawdzania poprawności i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7857d-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="7857d-187">Jeśli proces programu PowerShell zostanie zatrzymana podczas wykonywania skryptu, niektóre dzienniki zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="7857d-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="7857d-188">Połączenie z węzłem głównym</span><span class="sxs-lookup"><span data-stu-id="7857d-188">Connect to the head node</span></span>
<span data-ttu-id="7857d-189">Po wdrożeniu klastra HPC Pack na platformie Azure, [połączenia przez pulpit zdalny](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) z węzłem głównym maszyny Wirtualnej przy użyciu domeny poświadczenia zostanie podane podczas wdrażania klastra (na przykład *hpc\\clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="7857d-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="7857d-190">Klaster zarządzania za pomocą węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="7857d-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="7857d-191">W węźle głównym Uruchom Menedżera klastra HPC, aby sprawdzić stan klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="7857d-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="7857d-192">Można zarządzać i węzły obliczeniowe monitor węzły obliczeniowe systemu Linux, ten sam sposób pracy z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="7857d-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="7857d-193">Na przykład, zobacz węzłów systemu Linux na liście **zarządzanie zasobami** (te węzły zostały wdrożone za pomocą **LinuxNode** szablonu).</span><span class="sxs-lookup"><span data-stu-id="7857d-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Zarządzanie węzła][management]

<span data-ttu-id="7857d-195">Zobacz też w węzłach Linux **Mapa cieplna** widoku.</span><span class="sxs-lookup"><span data-stu-id="7857d-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Mapa cieplna][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="7857d-197">Sposób przenoszenia danych w klastrze z węzłami systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7857d-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="7857d-198">Można wybrać kilka opcji do przenoszenia danych między węzłami Linux i Windows węzłem głównym klastra.</span><span class="sxs-lookup"><span data-stu-id="7857d-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="7857d-199">Poniżej przedstawiono trzy typowe metody opisane bardziej szczegółowo w następujących sekcjach:</span><span class="sxs-lookup"><span data-stu-id="7857d-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="7857d-200">**Plików na platformę Azure** — przedstawia zarządzany udział plików SMB do przechowywania plików danych w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="7857d-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="7857d-201">Węzłów z systemem Windows i Linux węzłów mogą zainstalować udział plików Azure jako dysku lub folderu w tym samym czasie, nawet jeśli są one wdrożone w różnych sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7857d-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="7857d-202">**Udział SMB węzła głównego** — instaluje standardowe folder udostępniony systemu Windows węzła głównego w węzłach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7857d-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="7857d-203">**Serwer systemu plików NFS węzła HEAD** — zapewnia rozwiązanie do udostępniania plików w środowisku mieszanym Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="7857d-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="7857d-204">Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="7857d-204">Azure File storage</span></span>
<span data-ttu-id="7857d-205">[Plików Azure](https://azure.microsoft.com/services/storage/files/) udziałami plików przy użyciu standardowego protokołu SMB 2.1 udostępnia usługi.</span><span class="sxs-lookup"><span data-stu-id="7857d-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="7857d-206">Maszyny wirtualne platformy Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji mają dostęp do danych plików w udziale za pośrednictwem interfejsu API magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="7857d-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="7857d-207">Aby uzyskać szczegółowy opis kroków utworzyć udział plików Azure i zainstalować go w węźle głównym, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7857d-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="7857d-208">Aby zainstalować udział plików Azure w węzłach Linux, zobacz [jak używać magazynu plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7857d-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="7857d-209">Aby skonfigurować utrwalanie połączeń, zobacz [połączeń Persisting pliki programu Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="7857d-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="7857d-210">W poniższym przykładzie należy utworzyć udział plików Azure na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="7857d-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="7857d-211">Aby zainstalować udział w węźle głównym, otwórz wiersz polecenia i wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="7857d-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="7857d-212">W tym przykładzie allvhdsje to nazwa konta magazynu, storageaccountkey jest klucz konta magazynu, a funkcja rdma jest nazwa udziału plików platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7857d-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="7857d-213">Udziału plików platformy Azure jest zainstalowany jako Z: węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="7857d-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="7857d-214">Aby zainstalować udział plików Azure w węzłach Linux, uruchom **clusrun** na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="7857d-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="7857d-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  stanowi przydatne narzędzie HPC Pack do wykonywania zadań administracyjnych na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="7857d-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="7857d-216">(Zobacz też [Clusrun dla systemu Linux węzłów](#Clusrun-for-Linux-nodes) w tym artykule.)</span><span class="sxs-lookup"><span data-stu-id="7857d-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="7857d-217">Otwórz okno programu Windows PowerShell i wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="7857d-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="7857d-218">Pierwsze polecenie tworzy folder o nazwie /rdma we wszystkich węzłach grupy LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="7857d-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="7857d-219">Drugie polecenie instaluje allvhdsjw.file.core.windows.net/rdma udziału plików platformy Azure na folder /rdma z katalogu i pliku bitów trybu ustawioną 777.</span><span class="sxs-lookup"><span data-stu-id="7857d-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="7857d-220">W drugim poleceniu allvhdsje jest nazwa konta magazynu i storageaccountkey jest klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7857d-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="7857d-221">"\\`" Symbol w drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7857d-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7857d-222">"\\`," oznacza, że "," (przecinek znak) jest częścią polecenia.</span><span class="sxs-lookup"><span data-stu-id="7857d-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="7857d-223">Udział węzła głównego</span><span class="sxs-lookup"><span data-stu-id="7857d-223">Head node share</span></span>
<span data-ttu-id="7857d-224">Można również zainstalować z węzłem głównym folderu udostępnionego na węzłów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7857d-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="7857d-225">Udział zapewnia Najprostszym sposobem udostępniania plików, ale węzła głównego i wszystkie węzły Linux należy wdrożyć w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7857d-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="7857d-226">Poniżej przedstawiono kroki.</span><span class="sxs-lookup"><span data-stu-id="7857d-226">Here are the steps.</span></span>

1. <span data-ttu-id="7857d-227">Utwórz folder w węźle głównym i udostępnić go dla wszystkich osób mających uprawnienia odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="7857d-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="7857d-228">Na przykład udostępnić D:\OpenFOAM w węźle głównym jako \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="7857d-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="7857d-229">W tym miejscu CentOS7RDMA HN jest nazwą hosta węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="7857d-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![Uprawnienia do udziału plików][fileshareperms]
   
    ![Udostępnianie plików][filesharing]
2. <span data-ttu-id="7857d-232">Otwórz okno programu Windows PowerShell i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="7857d-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="7857d-233">Pierwsze polecenie tworzy folder o nazwie /openfoam we wszystkich węzłach grupy LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="7857d-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="7857d-234">Drugie polecenie instaluje //CentOS7RDMA-HN/OpenFOAM folderu udostępnionego na folder z katalogu i pliku bitów trybu ustawioną 777.</span><span class="sxs-lookup"><span data-stu-id="7857d-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="7857d-235">Nazwa użytkownika i hasło w poleceniu powinna być nazwa użytkownika i hasło użytkownika klastra w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="7857d-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="7857d-236">(Zobacz [Dodaj lub usuń użytkowników klastra](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="7857d-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="7857d-237">"\\`" Symbol w drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7857d-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7857d-238">"\\`," oznacza, że "," (przecinek znak) jest częścią polecenia.</span><span class="sxs-lookup"><span data-stu-id="7857d-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="7857d-239">Serwer systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="7857d-239">NFS server</span></span>
<span data-ttu-id="7857d-240">Usługa systemu plików NFS umożliwia udostępnianie i migrować pliki komputerach działa system operacyjny Windows Server 2012 przy użyciu protokołu SMB i opartych na systemie Linux przy użyciu protokołu NFS.</span><span class="sxs-lookup"><span data-stu-id="7857d-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="7857d-241">Serwer systemu plików NFS i inne węzły ma zostać wdrożony w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7857d-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="7857d-242">Zapewnia lepszą zgodność z węzłami systemu Linux w porównaniu z udziału SMB.</span><span class="sxs-lookup"><span data-stu-id="7857d-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="7857d-243">Na przykład obsługuje łącza do plików.</span><span class="sxs-lookup"><span data-stu-id="7857d-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="7857d-244">Aby zainstalować i skonfigurować serwer NFS, postępuj zgodnie z instrukcjami [serwera dla systemu pierwszego udziału sieciowego na całej trasie](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="7857d-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="7857d-245">Na przykład można utworzyć udziału NFS o nazwie nfs z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="7857d-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![Autoryzacja systemu plików NFS][nfsauth]
   
    ![Uprawnienia udziału NFS][nfsshare]
   
    ![Uprawnienia NTFS systemu plików NFS][nfsperm]
   
    ![Właściwości zarządzania systemu plików NFS][nfsmanage]
2. <span data-ttu-id="7857d-250">Otwórz okno programu Windows PowerShell i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="7857d-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="7857d-251">Pierwsze polecenie tworzy folder o nazwie /nfsshared we wszystkich węzłach grupy LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="7857d-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="7857d-252">Drugie polecenie instaluje udziału NFS CentOS7RDMA HN: / systemu plików nfs na folder.</span><span class="sxs-lookup"><span data-stu-id="7857d-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="7857d-253">W tym miejscu CentOS7RDMA HN: / systemu plików nfs to ścieżka do zdalnego udziału NFS.</span><span class="sxs-lookup"><span data-stu-id="7857d-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="7857d-254">Temat dotyczący przesyłania zadań</span><span class="sxs-lookup"><span data-stu-id="7857d-254">How to submit jobs</span></span>
<span data-ttu-id="7857d-255">Istnieje kilka sposobów umożliwiają przesyłanie zadań do klastra HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="7857d-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="7857d-256">Menedżer klastrów HPC lub Menedżer zadań klastra HPC graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="7857d-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="7857d-257">Portalu internetowego HPC</span><span class="sxs-lookup"><span data-stu-id="7857d-257">HPC web portal</span></span>
* <span data-ttu-id="7857d-258">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7857d-258">REST API</span></span>

<span data-ttu-id="7857d-259">Przesyłanie zadań do klastra na platformie Azure za pomocą narzędzia HPC Pack graficznego interfejsu użytkownika i portalu internetowego HPC są takie same jak w przypadku systemu Windows węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="7857d-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="7857d-260">Zobacz [Menedżer zadań klastra HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) i [sposobu przesyłania zadań z komputera klienckiego lokalnymi](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7857d-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7857d-261">Aby przesłać zadania za pomocą interfejsu API REST, należy zapoznać się [tworzenie i przesyłanie zadań przy użyciu interfejsu API REST w Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="7857d-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="7857d-262">Do przesyłania zadań w kliencie systemu Linux, również dotyczyć próbki Python w [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="7857d-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="7857d-263">Clusrun dla węzłów systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7857d-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="7857d-264">HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) narzędzie może służyć do wykonywania poleceń w węzłach systemu Linux przy użyciu wiersza polecenia lub Menedżer klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="7857d-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="7857d-265">Poniżej przedstawiono niektóre podstawowe przykłady.</span><span class="sxs-lookup"><span data-stu-id="7857d-265">Following are some basic examples.</span></span>

* <span data-ttu-id="7857d-266">Pokaż bieżącej nazwy użytkownika na wszystkich węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="7857d-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="7857d-267">Zainstaluj **gdb** narzędzie debugera z **yum** na wszystkich węzłów w linuxnodes grupy, a następnie uruchom ponownie węzeł po 10 minutach.</span><span class="sxs-lookup"><span data-stu-id="7857d-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="7857d-268">Utwórz skrypt powłoki wyświetlania każdej liczby od 1 do 10 sekundy jeden w każdym węźle systemu Linux w klastrze, uruchom go i natychmiast wyświetlane dane wyjściowe z węzłów.</span><span class="sxs-lookup"><span data-stu-id="7857d-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="7857d-269">Konieczne może być użycia pewnych znaków ucieczki w **clusrun** poleceń.</span><span class="sxs-lookup"><span data-stu-id="7857d-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="7857d-270">Jak pokazano w tym przykładzie, użyj ^ w wierszu polecenia, aby wprowadzić ">" symbolu.</span><span class="sxs-lookup"><span data-stu-id="7857d-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7857d-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7857d-271">Next steps</span></span>
* <span data-ttu-id="7857d-272">Spróbuj skalowaniu większą liczbę węzłów klastra lub działających obciążeń systemu Linux w klastrze.</span><span class="sxs-lookup"><span data-stu-id="7857d-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="7857d-273">Na przykład zobacz [Uruchom NAMD z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="7857d-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="7857d-274">Spróbuj klaster z [maszyn wirtualnych z funkcją RDMA, obliczeniowych](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uruchamiać obciążenia na MPI.</span><span class="sxs-lookup"><span data-stu-id="7857d-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="7857d-275">Na przykład zobacz [klastra uruchom OpenFOAM z pakietem Microsoft HPC na RDMA systemu Linux na platformie Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="7857d-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="7857d-276">Jeśli interesuje Cię w pracy z Linux węzłów w klastrze HPC Pack lokalnych, zobacz [wskazówki TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="7857d-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
