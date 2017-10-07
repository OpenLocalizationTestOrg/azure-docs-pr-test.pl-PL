---
title: aaaSQL Server FCI - maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób toocreate wystąpienie klastra pracy awaryjnej programu SQL Server na maszynach wirtualnych platformy Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="afda7-103">Skonfiguruj wystąpienie klastra pracy awaryjnej programu SQL Server na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="afda7-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="afda7-104">W tym artykule opisano, jak toocreate programu SQL Server klastra trybu Failover wystąpienia (FCI), maszynach wirtualnych Azure w modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afda7-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="afda7-105">To rozwiązanie wymaga [systemu Windows Server 2016 Datacenter edition bezpośrednie miejsca do magazynowania \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) jako opartych na oprogramowaniu wirtualnej sieci SAN synchronizujący hello magazynu (dysków danych) między hello węzłach (maszynach wirtualnych platformy Azure) Klaster systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="afda7-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="afda7-106">S2D stanowi nowość w systemie Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="afda7-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="afda7-107">Witaj Poniższy diagram przedstawia kompletnego rozwiązania hello na maszynach wirtualnych Azure:</span><span class="sxs-lookup"><span data-stu-id="afda7-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="afda7-109">Witaj poprzedzających diagramie przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="afda7-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="afda7-110">Dwóch maszyn wirtualnych platformy Azure w klastrze pracy awaryjnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="afda7-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="afda7-111">Maszyna wirtualna jest w klastrze pracy awaryjnej jest również nazywany *węzła klastra*, lub *węzłów*.</span><span class="sxs-lookup"><span data-stu-id="afda7-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="afda7-112">Każda maszyna wirtualna ma co najmniej dwa dyski danych.</span><span class="sxs-lookup"><span data-stu-id="afda7-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="afda7-113">S2D synchronizuje dane hello na dysku danych hello i przedstawia magazynu hello synchronizowane jako puli magazynów.</span><span class="sxs-lookup"><span data-stu-id="afda7-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="afda7-114">puli magazynu Hello przedstawia klastra pracy awaryjnej toohello (CSV) woluminu udostępnionego klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="afda7-115">rolę klastra programu SQL Server FCI Hello używa hello CSV hello dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="afda7-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="afda7-116">Azure adres usługi równoważenia obciążenia toohold hello IP dla hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="afda7-117">Zestaw dostępności Azure zawiera wszystkie zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="afda7-118">Wszystkie zasoby platformy Azure są na diagramie hello w hello tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="afda7-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="afda7-119">Aby uzyskać szczegółowe informacje o S2D, zobacz [systemu Windows Server 2016 Datacenter edition bezpośrednie miejsca do magazynowania \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="afda7-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="afda7-120">S2D obsługuje dwa typy architektury - konwergentnej i hiperkonwergentnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="afda7-121">Architektura Hello w tym dokumencie jest hiperkonwergentnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="afda7-122">Hiperkonwergentnych infrastruktury magazynu hello miejsca na hello samych serwerów w tej aplikacji hello w klastrze hosta.</span><span class="sxs-lookup"><span data-stu-id="afda7-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="afda7-123">W ramach tej architektury magazynu hello jest w każdym węźle SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="afda7-124">Przykład szablonu Azure</span><span class="sxs-lookup"><span data-stu-id="afda7-124">Example Azure template</span></span>

<span data-ttu-id="afda7-125">Można utworzyć hello całego rozwiązania na platformie Azure w ramach szablonu.</span><span class="sxs-lookup"><span data-stu-id="afda7-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="afda7-126">Przykład szablonu jest dostępny w hello GitHub [szablonów Szybki Start Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="afda7-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="afda7-127">W tym przykładzie nie jest przeznaczona lub sprawdzane pod kątem żadnych określonego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="afda7-128">Możesz uruchomić toocreate szablonu hello FCI serwera SQL z S2D magazynu podłączonego tooyour domeny.</span><span class="sxs-lookup"><span data-stu-id="afda7-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="afda7-129">Ocena hello szablonu i zmodyfikuj go do własnych celów.</span><span class="sxs-lookup"><span data-stu-id="afda7-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="afda7-130">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="afda7-130">Before you begin</span></span>

<span data-ttu-id="afda7-131">Jest kilka rzeczy, przed kontynuowaniem należy tooknow i kilka rzeczy, które są potrzebne w miejscu.</span><span class="sxs-lookup"><span data-stu-id="afda7-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="afda7-132">Jakie tooknow</span><span class="sxs-lookup"><span data-stu-id="afda7-132">What tooknow</span></span>
<span data-ttu-id="afda7-133">Musisz mieć operacyjne zrozumienia hello następujące technologie:</span><span class="sxs-lookup"><span data-stu-id="afda7-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="afda7-134">Technologie klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="afda7-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="afda7-135">[Wystąpienia klastra trybu Failover programu SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="afda7-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="afda7-136">Ponadto musisz mieć ogólną wiedzą hello następujące technologie:</span><span class="sxs-lookup"><span data-stu-id="afda7-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="afda7-137">Zbieżność Hyper rozwiązania przy użyciu bezpośrednie miejsca do magazynowania w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="afda7-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="afda7-138">Grup zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afda7-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="afda7-139">Jakie toohave</span><span class="sxs-lookup"><span data-stu-id="afda7-139">What toohave</span></span>

<span data-ttu-id="afda7-140">Przed rozpoczęciem powitalne instrukcje w tym artykule, należy:</span><span class="sxs-lookup"><span data-stu-id="afda7-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="afda7-141">Subskrypcja Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="afda7-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="afda7-142">Domena systemu Windows na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="afda7-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="afda7-143">Konto z obiektami toocreate uprawnień w hello maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afda7-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="afda7-144">Sieć wirtualna platformy Azure i podsieci z wystarczającą przestrzenią adresów IP dla hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="afda7-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="afda7-145">Obydwie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="afda7-145">Both virtual machines.</span></span>
   - <span data-ttu-id="afda7-146">Witaj adres IP klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="afda7-147">Adres IP dla każdego infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="afda7-148">DNS skonfigurowane na powitania sieci Azure, wskazując toohello kontrolerów domeny.</span><span class="sxs-lookup"><span data-stu-id="afda7-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="afda7-149">Z tych wymagań wstępnych w miejscu można kontynuować tworzenie klastra trybu failover.</span><span class="sxs-lookup"><span data-stu-id="afda7-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="afda7-150">pierwszym krokiem Hello jest maszyn wirtualnych hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="afda7-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="afda7-151">Krok 1: Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="afda7-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="afda7-152">Zaloguj się za toohello [portalu Azure](http://portal.azure.com) w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="afda7-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="afda7-153">[Tworzenie zestawu dostępności Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="afda7-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="afda7-154">dostępność Hello ustawienia grupy maszyn wirtualnych w domenach awarii lub uaktualnienia domen.</span><span class="sxs-lookup"><span data-stu-id="afda7-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="afda7-155">zestaw dostępności Hello upewnia się, że aplikacja nie ma wpływu na pojedyncze punkty awarii, takie jak przełącznik sieci hello lub jednostki zasilania hello stojak serwerów.</span><span class="sxs-lookup"><span data-stu-id="afda7-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="afda7-156">Jeśli nie utworzono hello grupy zasobów dla maszyn wirtualnych, należy to zrobić, podczas tworzenia zestawu dostępności Azure.</span><span class="sxs-lookup"><span data-stu-id="afda7-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="afda7-157">Jeśli używasz zestaw dostępności hello Azure toocreate portalu hello hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="afda7-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="afda7-158">W portalu Azure hello, kliknij przycisk  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="afda7-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="afda7-159">Wyszukaj **zestawu dostępności**.</span><span class="sxs-lookup"><span data-stu-id="afda7-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="afda7-160">Kliknij przycisk **zestawu dostępności**.</span><span class="sxs-lookup"><span data-stu-id="afda7-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="afda7-161">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afda7-161">Click **Create**.</span></span>
   - <span data-ttu-id="afda7-162">Na powitania **tworzenia zestawu dostępności** bloku hello ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="afda7-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="afda7-163">**Nazwa**: Nazwa zestawu dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="afda7-164">**Subskrypcja**: Azure Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="afda7-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="afda7-165">**Grupa zasobów**: toouse istniejącą grupę, kliknij przycisk **Użyj istniejącego** i hello wybierz grupę z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="afda7-166">W przeciwnym razie wybierz **Utwórz nowy** i wpisz nazwę grupy hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="afda7-167">**Lokalizacja**: Ustaw lokalizację hello, w którym planujesz toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="afda7-168">**Odporność domen**: używanie domyślnych hello (3).</span><span class="sxs-lookup"><span data-stu-id="afda7-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="afda7-169">**Aktualizowanie domeny**: Użyj domyślnej hello [5].</span><span class="sxs-lookup"><span data-stu-id="afda7-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="afda7-170">Kliknij przycisk **Utwórz** zestawu dostępności hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="afda7-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="afda7-171">Tworzenie maszyn wirtualnych hello hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="afda7-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="afda7-172">Umieszczanie dwóch maszyn wirtualnych programu SQL Server w zestawie dostępności Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="afda7-173">Aby uzyskać instrukcje, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="afda7-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="afda7-174">Umieść obydwie maszyny wirtualne:</span><span class="sxs-lookup"><span data-stu-id="afda7-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="afda7-175">W hello zestawu dostępności z tej samej grupy zasobów platformy Azure jest w.</span><span class="sxs-lookup"><span data-stu-id="afda7-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="afda7-176">Na powitania sam sieci jako kontroler domeny.</span><span class="sxs-lookup"><span data-stu-id="afda7-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="afda7-177">W podsieci z wystarczającą przestrzenią adresów IP dla maszyn wirtualnych i wszystkie wystąpienia, które użytkownik może użyć w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="afda7-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="afda7-178">W zestawie dostępności Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="afda7-179">Nie można ustawić lub zmienić dostępności ustawić po utworzeniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="afda7-180">Wybierz obraz z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="afda7-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="afda7-181">Korzystając z witryny Marketplace zawiera obraz z tym systemu Windows Server i SQL Server lub po prostu hello systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="afda7-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="afda7-182">Aby uzyskać więcej informacji, zobacz [Omówienie programu SQL Server na maszynach wirtualnych platformy Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="afda7-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="afda7-183">Hello oficjalnego obrazów programu SQL Server w galerii Azure hello obejmują zainstalowane wystąpienie programu SQL Server, oraz oprogramowanie instalacyjne programu SQL Server hello i hello wymaganego klucza.</span><span class="sxs-lookup"><span data-stu-id="afda7-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="afda7-184">Wybierz obraz prawym hello zgodnie z toohow, który ma toopay hello licencję programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="afda7-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="afda7-185">**Należy zwrócić na użycie licencjonowania**: hello na minutę koszt tych obrazów obejmuje hello licencjonowania programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="afda7-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="afda7-186">**SQL Server 2016 przedsiębiorstwa w systemie Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="afda7-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="afda7-187">**SQL Server 2016 Standard w systemie Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="afda7-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="afda7-188">**SQL Server 2016 Developer w systemie Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="afda7-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="afda7-189">**Przełącz your właścicielem licencji (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="afda7-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="afda7-190">**{BYOL} SQL Server 2016 przedsiębiorstwa w systemie Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="afda7-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="afda7-191">**{BYOL} SQL Server 2016 Standard w systemie Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="afda7-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="afda7-192">Po utworzeniu maszyny wirtualnej hello, należy usunąć wystąpienia programu SQL Server zainstalowane wcześniej autonomiczne hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="afda7-193">Po skonfigurowaniu klastra trybu failover hello i S2D użyjesz hello wstępnie zainstalowane programu SQL Server nośnika toocreate hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="afda7-194">Alternatywnie można użyć obrazów Azure Marketplace właśnie hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="afda7-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="afda7-195">Wybierz **systemu Windows Server 2016 Datacenter** obrazu i zainstaluj hello SQL Server FCI, po skonfigurowaniu klastra trybu failover hello i S2D.</span><span class="sxs-lookup"><span data-stu-id="afda7-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="afda7-196">Ten obraz zawiera nośnik instalacyjny programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afda7-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="afda7-197">Umieść nośnik instalacyjny hello w lokalizacji, w której można uruchamiać hello instalacji programu SQL Server dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="afda7-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="afda7-198">Po Azure utworzy maszyn wirtualnych, należy połączyć tooeach maszyny wirtualnej z protokołem RDP.</span><span class="sxs-lookup"><span data-stu-id="afda7-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="afda7-199">Podczas pierwszego łączenia tooa maszyny wirtualnej z protokołem RDP, komputer hello pyta użytkownika tooallow toobe tego komputera wykrywalny hello sieci.</span><span class="sxs-lookup"><span data-stu-id="afda7-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="afda7-200">Kliknij przycisk **Yes** (Tak).</span><span class="sxs-lookup"><span data-stu-id="afda7-200">Click **Yes**.</span></span>

1. <span data-ttu-id="afda7-201">Jeśli jeden z obrazów maszyny wirtualnej na serwerze SQL hello są używane, należy usunąć hello wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afda7-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="afda7-202">W **programy i funkcje**, kliknij prawym przyciskiem myszy **Microsoft SQL Server 2016 (64-bitowy)** i kliknij przycisk **Odinstaluj/Zmień**.</span><span class="sxs-lookup"><span data-stu-id="afda7-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="afda7-203">Kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="afda7-203">Click **Remove**.</span></span>
   - <span data-ttu-id="afda7-204">Wybierz wystąpienie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-204">Select hello default instance.</span></span>
   - <span data-ttu-id="afda7-205">Usuwanie wszystkich funkcji w obszarze **usługi aparatu bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="afda7-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="afda7-206">Nie usuwaj **wspólne funkcje**.</span><span class="sxs-lookup"><span data-stu-id="afda7-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="afda7-207">Zobacz hello poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="afda7-207">See hello following picture:</span></span>

      ![Usuwanie funkcji](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="afda7-209">Kliknij przycisk **dalej**, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="afda7-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="afda7-210"><a name="ports"></a>Otwórz porty zapory hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="afda7-211">Na każdej maszynie wirtualnej Otwórz hello następujących portów w Zaporze systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="afda7-212">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="afda7-212">Purpose</span></span> | <span data-ttu-id="afda7-213">TCP Port</span><span class="sxs-lookup"><span data-stu-id="afda7-213">TCP Port</span></span> | <span data-ttu-id="afda7-214">Uwagi</span><span class="sxs-lookup"><span data-stu-id="afda7-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="afda7-215">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="afda7-215">SQL Server</span></span> | <span data-ttu-id="afda7-216">1433</span><span class="sxs-lookup"><span data-stu-id="afda7-216">1433</span></span> | <span data-ttu-id="afda7-217">Normalne port dla domyślnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afda7-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="afda7-218">Jeśli używasz obrazu z galerii hello ten port jest automatycznie otwierane.</span><span class="sxs-lookup"><span data-stu-id="afda7-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="afda7-219">Badania kondycji</span><span class="sxs-lookup"><span data-stu-id="afda7-219">Health probe</span></span> | <span data-ttu-id="afda7-220">59999</span><span class="sxs-lookup"><span data-stu-id="afda7-220">59999</span></span> | <span data-ttu-id="afda7-221">Wszelkie Otwórz TCP port.</span><span class="sxs-lookup"><span data-stu-id="afda7-221">Any open TCP port.</span></span> <span data-ttu-id="afda7-222">W kolejnym kroku, należy skonfigurować usługi równoważenia obciążenia hello [sondy kondycji](#probe) i hello toouse klastra tego portu.</span><span class="sxs-lookup"><span data-stu-id="afda7-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="afda7-223">Dodaj maszynę wirtualną toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="afda7-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="afda7-224">Aby uzyskać szczegółowe informacje, zobacz [dodać magazyn](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="afda7-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="afda7-225">Dane co najmniej dwa dyski należy obie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="afda7-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="afda7-226">Dołącz raw dyski - dysków sformatowanych nie systemu plików NTFS.</span><span class="sxs-lookup"><span data-stu-id="afda7-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="afda7-227">Po dołączeniu dyski sformatowane przy użyciu systemu plików NTFS, można włączyć tylko S2D z bez sprawdzania kwalifikujące dysku.</span><span class="sxs-lookup"><span data-stu-id="afda7-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="afda7-228">Dołącz co najmniej dwóch tooeach magazyn w warstwie Premium (SSD dyski) maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="afda7-229">Zaleca się co najmniej P30 dysków (1 TB).</span><span class="sxs-lookup"><span data-stu-id="afda7-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="afda7-230">Zbyt buforowania hosta zestawu**tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="afda7-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="afda7-231">pojemność magazynu Hello używanego w środowiskach produkcyjnych zależy od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="afda7-232">wartości Hello opisanych w tym artykule dotyczą pokazu i testowania.</span><span class="sxs-lookup"><span data-stu-id="afda7-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="afda7-233">[Dodawanie domeny istniejące hello maszyn wirtualnych tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="afda7-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="afda7-234">Po hello maszyny wirtualne są tworzone i skonfigurowany, można skonfigurować hello klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="afda7-235">Krok 2: Konfigurowanie klastra trybu Failover systemu Windows hello z S2D</span><span class="sxs-lookup"><span data-stu-id="afda7-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="afda7-236">Witaj następnym krokiem jest klaster trybu failover hello tooconfigure S2D.</span><span class="sxs-lookup"><span data-stu-id="afda7-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="afda7-237">W tym kroku będziesz wykonywać hello następujących podetapów:</span><span class="sxs-lookup"><span data-stu-id="afda7-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="afda7-238">Dodaj funkcję Klaster pracy awaryjnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="afda7-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="afda7-239">Sprawdzanie poprawności klastra hello</span><span class="sxs-lookup"><span data-stu-id="afda7-239">Validate hello cluster</span></span>
1. <span data-ttu-id="afda7-240">Tworzenie klastra pracy awaryjnej hello</span><span class="sxs-lookup"><span data-stu-id="afda7-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="afda7-241">Tworzenie monitora chmury hello</span><span class="sxs-lookup"><span data-stu-id="afda7-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="afda7-242">Dodawanie magazynu</span><span class="sxs-lookup"><span data-stu-id="afda7-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="afda7-243">Dodaj funkcję Klaster pracy awaryjnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="afda7-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="afda7-244">toobegin, Połącz toohello pierwszej maszyny wirtualnej z protokołem RDP przy użyciu konta domeny, które jest członkiem grupy administratorów lokalnych i ma uprawnienia toocreate obiektów w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afda7-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="afda7-245">Konto służy do reszty hello hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afda7-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="afda7-246">[Dodaj klaster trybu Failover maszyny wirtualnej funkcji tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="afda7-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="afda7-247">Funkcja Klaster pracy awaryjnej tooinstall z interfejsu użytkownika, powitalne hello następujące kroki na obu maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="afda7-248">W **Menedżera serwera**, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **Dodaj role i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="afda7-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="afda7-249">W **Kreatora dodawania ról i funkcji**, kliknij przycisk **dalej** do momentu uzyskania zbyt**Wybieranie funkcji**.</span><span class="sxs-lookup"><span data-stu-id="afda7-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="afda7-250">W **Wybieranie funkcji**, kliknij przycisk **klaster pracy awaryjnej**.</span><span class="sxs-lookup"><span data-stu-id="afda7-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="afda7-251">Obejmują wszystkie wymagane funkcje i narzędzia do zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="afda7-252">Kliknij przycisk **dodawania funkcji**.</span><span class="sxs-lookup"><span data-stu-id="afda7-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="afda7-253">Kliknij przycisk **dalej** , a następnie kliknij przycisk **Zakończ** tooinstall hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="afda7-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="afda7-254">tooinstall hello funkcji Klaster trybu Failover przy użyciu programu PowerShell, uruchom hello następującego skryptu z sesji programu PowerShell administratora na jednym hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="afda7-255">Odwołania, kolejne kroki hello wykonaj instrukcje hello w kroku 3 [zbieżność Hyper rozwiązania przy użyciu bezpośrednie miejsca do magazynowania w systemie Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="afda7-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="afda7-256">Sprawdzanie poprawności klastra hello</span><span class="sxs-lookup"><span data-stu-id="afda7-256">Validate hello cluster</span></span>

<span data-ttu-id="afda7-257">Ten przewodnik odwołuje się tooinstructions w obszarze [weryfikacji klastra](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="afda7-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="afda7-258">Sprawdzanie poprawności klastra hello hello interfejsu użytkownika lub przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afda7-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="afda7-259">klaster hello toovalidate z interfejsu użytkownika, powitalne hello następujące kroki z jednej z maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="afda7-260">W **Menedżera serwera**, kliknij przycisk **narzędzia**, następnie kliknij przycisk **Menedżera klastra trybu Failover**.</span><span class="sxs-lookup"><span data-stu-id="afda7-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="afda7-261">W **Menedżera klastra trybu Failover**, kliknij przycisk **akcji**, następnie kliknij przycisk **Sprawdź poprawność konfiguracji...** .</span><span class="sxs-lookup"><span data-stu-id="afda7-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="afda7-262">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afda7-262">Click **Next**.</span></span>
1. <span data-ttu-id="afda7-263">Na **Wybieranie serwerów lub klastrów**, nazwa typu hello zarówno maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="afda7-264">Na **opcji testowania**, wybierz **uruchamianie tylko testów I wybrać**.</span><span class="sxs-lookup"><span data-stu-id="afda7-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="afda7-265">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afda7-265">Click **Next**.</span></span>
1. <span data-ttu-id="afda7-266">Na **Test wybór**, obejmują wszystkich testów oprócz **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="afda7-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="afda7-267">Zobacz hello poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="afda7-267">See hello following picture:</span></span>

   ![Zweryfikuj testy](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="afda7-269">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afda7-269">Click **Next**.</span></span>
1. <span data-ttu-id="afda7-270">Na **potwierdzenie**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afda7-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="afda7-271">Witaj **Kreator weryfikacji konfiguracji** uruchamia hello testów sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="afda7-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="afda7-272">toovalidate hello klastra przy użyciu programu PowerShell, uruchom hello następującego skryptu z sesji programu PowerShell administratora na jednym hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="afda7-273">Po sprawdzania poprawności klastra hello utworzyć hello klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="afda7-274">Tworzenie klastra pracy awaryjnej hello</span><span class="sxs-lookup"><span data-stu-id="afda7-274">Create hello failover cluster</span></span>

<span data-ttu-id="afda7-275">Ten przewodnik odwołuje się zbyt[Utwórz klaster pracy awaryjnej hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="afda7-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="afda7-276">toocreate hello klastra pracy awaryjnej, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="afda7-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="afda7-277">nazwy Hello hello maszyn wirtualnych, które stają się hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="afda7-278">Nazwa klastra trybu failover hello</span><span class="sxs-lookup"><span data-stu-id="afda7-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="afda7-279">Adres IP dla klastra trybu failover hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="afda7-280">Adres IP, który nie jest używany na powitania można użyć tej samej sieci wirtualnej platformy Azure i podsieć, jak hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="afda7-281">Witaj następującego środowiska PowerShell tworzy klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="afda7-282">Aktualizacja hello skryptu z nazwami hello hello węzłów (hello nazwy maszyny wirtualnej) i dostępny adres IP z hello sieci Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="afda7-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="afda7-283">Tworzenie monitora chmury</span><span class="sxs-lookup"><span data-stu-id="afda7-283">Create a cloud witness</span></span>

<span data-ttu-id="afda7-284">Monitor chmury jest nowy typ monitora kworum klastra przechowywane w obiekcie Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="afda7-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="afda7-285">To eliminuje potrzebę hello oddzielne hosting udziału monitora maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="afda7-286">[Tworzenie chmury monitora dla klastra trybu failover hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="afda7-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="afda7-287">Tworzenie kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="afda7-287">Create a blob container.</span></span>

1. <span data-ttu-id="afda7-288">Zapisz hello klucze dostępu i hello adresu URL kontenera.</span><span class="sxs-lookup"><span data-stu-id="afda7-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="afda7-289">Skonfiguruj Monitor kworum klastra klastra pracy awaryjnej hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="afda7-290">Zobacz [Konfiguruj hello monitora kworum w interfejsie użytkownika hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) w hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afda7-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="afda7-291">Dodawanie magazynu</span><span class="sxs-lookup"><span data-stu-id="afda7-291">Add storage</span></span>

<span data-ttu-id="afda7-292">dyski Hello S2D muszą toobe pusty i bez partycji lub innych danych.</span><span class="sxs-lookup"><span data-stu-id="afda7-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="afda7-293">Wykonaj dysków tooclean [hello kroków w tym przewodniku](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="afda7-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="afda7-294">[Włącz sklepu odstępów bezpośrednio \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="afda7-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="afda7-295">Witaj następującego środowiska PowerShell umożliwia bezpośrednie miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="afda7-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="afda7-296">W **Menedżera klastra trybu Failover**, możesz teraz przeglądać hello puli magazynu.</span><span class="sxs-lookup"><span data-stu-id="afda7-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="afda7-297">[Tworzenie woluminu](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="afda7-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="afda7-298">Jedną z funkcji hello S2D jest on automatycznie tworzona jest pula magazynu po jej włączeniu.</span><span class="sxs-lookup"><span data-stu-id="afda7-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="afda7-299">Wszystko jest teraz gotowy toocreate woluminu.</span><span class="sxs-lookup"><span data-stu-id="afda7-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="afda7-300">Witaj polecenia programu PowerShell `New-Volume` automatyzuje proces tworzenia woluminu hello oraz formatowanie, dodawanie toohello klastra i utworzenie udostępnionego woluminu klastra (CSV).</span><span class="sxs-lookup"><span data-stu-id="afda7-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="afda7-301">Witaj poniższy przykład tworzy 800 gigabajt (GB) CSV.</span><span class="sxs-lookup"><span data-stu-id="afda7-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="afda7-302">Po wykonaniu tego polecenia, jako zasób klastra został zainstalowany wolumin 800 GB.</span><span class="sxs-lookup"><span data-stu-id="afda7-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="afda7-303">wolumin Hello jest na `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="afda7-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="afda7-304">powitania po diagram przedstawia udostępniony wolumin klastra z S2D:</span><span class="sxs-lookup"><span data-stu-id="afda7-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="afda7-306">Krok 3: Testowanie trybu failover klastra trybu failover</span><span class="sxs-lookup"><span data-stu-id="afda7-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="afda7-307">W Menedżerze klastra trybu Failover Sprawdź, czy można przenieść toohello zasobów magazynu hello innym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="afda7-308">Jeśli można połączyć toohello trybu failover klaster z **Menedżera klastra trybu Failover** i przeniesienie magazynu hello z jednego węzła toohello innych, są gotowe tooconfigure hello infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="afda7-309">Krok 4: Tworzenie programu SQL Server infrastruktury klasyfikacji plików</span><span class="sxs-lookup"><span data-stu-id="afda7-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="afda7-310">Po skonfigurowaniu klastra trybu failover hello i wszystkie składniki klastra, łącznie z magazynem, można utworzyć hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="afda7-311">Połącz toohello pierwszej maszyny wirtualnej z protokołem RDP.</span><span class="sxs-lookup"><span data-stu-id="afda7-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="afda7-312">W **Menedżera klastra trybu Failover**, upewnij się, że wszystkie zasoby podstawowe klastra znajdują się na pierwszej maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="afda7-313">Jeśli to konieczne, Przenieś wszystkie maszyny wirtualnej toothis zasobów.</span><span class="sxs-lookup"><span data-stu-id="afda7-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="afda7-314">Zlokalizuj hello nośnika instalacyjnego.</span><span class="sxs-lookup"><span data-stu-id="afda7-314">Locate hello installation media.</span></span> <span data-ttu-id="afda7-315">Jeśli maszyna wirtualna hello używa jednego z obrazów Azure Marketplace hello, hello nośnika znajduje się pod adresem `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="afda7-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="afda7-316">Kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="afda7-316">Click **Setup**.</span></span>

1. <span data-ttu-id="afda7-317">W hello **Centrum instalacji programu SQL Server**, kliknij przycisk **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="afda7-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="afda7-318">Kliknij przycisk **instalacji klastra pracy awaryjnej nowy serwer SQL**.</span><span class="sxs-lookup"><span data-stu-id="afda7-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="afda7-319">Wykonaj instrukcje hello hello kreatora tooinstall hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="afda7-320">katalogi danych FCI Hello muszą toobe w magazynie klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="afda7-321">Z S2D nie jest udostępniony dysk, ale tooa punktu instalacji woluminu na każdym serwerze.</span><span class="sxs-lookup"><span data-stu-id="afda7-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="afda7-322">S2D synchronizuje woluminu hello między obu węzłów.</span><span class="sxs-lookup"><span data-stu-id="afda7-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="afda7-323">wolumin Hello są prezentowane toohello klastra jako udostępniony wolumin klastra.</span><span class="sxs-lookup"><span data-stu-id="afda7-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="afda7-324">Użyj punktu instalacji woluminu CSV hello hello danych katalogów.</span><span class="sxs-lookup"><span data-stu-id="afda7-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="afda7-326">Po zakończeniu pracy Kreatora hello Instalator zainstaluje na pierwszym węźle hello FCI serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="afda7-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="afda7-327">Po zainstalowaniu Instalator pomyślnie hello infrastruktury klasyfikacji plików na pierwszym węźle hello Uzyskuj dostęp do drugiego węzła toohello RDP.</span><span class="sxs-lookup"><span data-stu-id="afda7-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="afda7-328">Otwórz hello **Centrum instalacji programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="afda7-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="afda7-329">Kliknij przycisk **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="afda7-329">Click **Installation**.</span></span>

1. <span data-ttu-id="afda7-330">Kliknij przycisk **klastra pracy awaryjnej programu SQL Server Dodaj węzeł tooa**.</span><span class="sxs-lookup"><span data-stu-id="afda7-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="afda7-331">Wykonaj te instrukcje hello hello kreatora tooinstall programu SQL server, a następnie dodaj ten toohello serwera infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="afda7-332">Jeśli używasz obrazu galerii Azure Marketplace z programem SQL Server, narzędzia programu SQL Server zostały zawarte w hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="afda7-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="afda7-333">Jeśli nie używasz tego obrazu, hello narzędzia SQL Server należy zainstalować oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="afda7-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="afda7-334">Zobacz [pobierania programu SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="afda7-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="afda7-335">Krok 5: Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="afda7-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="afda7-336">Na maszynach wirtualnych Azure klastrom toohold usługi równoważenia obciążenia adres IP, który wymaga toobe na jednym węźle klastra w czasie.</span><span class="sxs-lookup"><span data-stu-id="afda7-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="afda7-337">W tym rozwiązaniu usługi równoważenia obciążenia hello zawiera adres IP hello hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="afda7-338">[Tworzenie i konfigurowanie usługi równoważenia obciążenia Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="afda7-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="afda7-339">Tworzenie usługi równoważenia obciążenia hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="afda7-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="afda7-340">Moduł równoważenia obciążenia hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="afda7-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="afda7-341">W hello portalu Azure Przejdź toohello grupy zasobów z maszynami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="afda7-342">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="afda7-342">Click **+ Add**.</span></span> <span data-ttu-id="afda7-343">Wyszukiwanie hello Marketplace dla **modułu równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="afda7-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="afda7-344">Kliknij przycisk **modułu równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="afda7-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="afda7-345">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afda7-345">Click **Create**.</span></span>

1. <span data-ttu-id="afda7-346">Skonfiguruj hello modułu równoważenia obciążenia z:</span><span class="sxs-lookup"><span data-stu-id="afda7-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="afda7-347">**Nazwa**: nazwę identyfikującą hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="afda7-348">**Typ**: hello modułu równoważenia obciążenia mogą być publicznych lub prywatnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="afda7-349">Moduł równoważenia obciążenia prywatnej jest możliwy za pomocą hello tej samej sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="afda7-350">Najbardziej Azure aplikacje mogą używać modułu równoważenia obciążenia prywatnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="afda7-351">Jeśli aplikacja wymaga dostępu tooSQL serwera bezpośrednio przez hello Internet, użyj publiczny moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="afda7-352">**Sieć wirtualna**: hello sam sieci jako hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="afda7-353">**Podsieci**: hello tej samej podsieci co hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="afda7-354">**Prywatny adres IP**: hello przypisania zasobu sieciowego klastra programu SQL Server FCI toohello tego samego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="afda7-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="afda7-355">**Subskrypcja**: Azure Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="afda7-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="afda7-356">**Grupa zasobów**: Użyj hello sam grupie zasobów co maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="afda7-357">**Lokalizacja**: Użyj hello sam lokalizacji platformy Azure jako maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afda7-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="afda7-358">Zobacz hello poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="afda7-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="afda7-360">Konfigurowanie puli zaplecza modułu równoważenia obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="afda7-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="afda7-361">Zwraca toohello grupy zasobów platformy Azure z maszynami wirtualnymi hello i Znajdź hello nowego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="afda7-362">Mogą mieć widok hello toorefresh na powitania grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="afda7-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="afda7-363">Kliknij przycisk hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="afda7-364">W bloku modułu równoważenia obciążenia hello, kliknij **pul zaplecza**.</span><span class="sxs-lookup"><span data-stu-id="afda7-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="afda7-365">Kliknij przycisk **+ Dodaj** tooadd puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="afda7-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="afda7-366">Wpisz nazwę hello puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="afda7-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="afda7-367">Kliknij przycisk **Dodaj maszynę wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="afda7-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="afda7-368">Na powitania **wybierz maszyny wirtualne** bloku, kliknij przycisk **wybierz zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="afda7-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="afda7-369">Wybieranie zestawu dostępności hello umieszczanie maszyn wirtualnych programu SQL Server hello w.</span><span class="sxs-lookup"><span data-stu-id="afda7-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="afda7-370">Na powitania **wybierz maszyny wirtualne** bloku, kliknij przycisk **wybierz maszyny wirtualne hello**.</span><span class="sxs-lookup"><span data-stu-id="afda7-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="afda7-371">Portalem Azure powinna wyglądać hello poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="afda7-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="afda7-373">Kliknij przycisk **wybierz** na powitania **wybierz maszyny wirtualne** bloku.</span><span class="sxs-lookup"><span data-stu-id="afda7-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="afda7-374">Kliknij przycisk **OK** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="afda7-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="afda7-375">Skonfiguruj kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afda7-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="afda7-376">W bloku modułu równoważenia obciążenia hello, kliknij **sondy kondycji**.</span><span class="sxs-lookup"><span data-stu-id="afda7-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="afda7-377">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="afda7-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="afda7-378">Na powitania **sondy kondycji Dodaj** bloku <a name="probe"> </a>Ustaw parametry sondy kondycji hello:</span><span class="sxs-lookup"><span data-stu-id="afda7-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="afda7-379">**Nazwa**: Nazwa sondy kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="afda7-380">**Protokół**: TCP.</span><span class="sxs-lookup"><span data-stu-id="afda7-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="afda7-381">**Port**: Ustaw tooan dostępny port TCP.</span><span class="sxs-lookup"><span data-stu-id="afda7-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="afda7-382">Ten port wymaga port zapory otwarte.</span><span class="sxs-lookup"><span data-stu-id="afda7-382">This port requires an open firewall port.</span></span> <span data-ttu-id="afda7-383">Użyj hello [tego samego portu](#ports) ustawiony dla sondy kondycji hello na zaporze hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="afda7-384">**Interwał**: 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="afda7-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="afda7-385">**Próg złej kondycji**: 2 kolejnych błędów.</span><span class="sxs-lookup"><span data-stu-id="afda7-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="afda7-386">Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="afda7-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="afda7-387">Ustaw reguły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afda7-387">Set load balancing rules</span></span>

1. <span data-ttu-id="afda7-388">W bloku modułu równoważenia obciążenia hello, kliknij **reguły równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="afda7-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="afda7-389">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="afda7-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="afda7-390">Ustaw parametry reguły równoważenia obciążenia hello:</span><span class="sxs-lookup"><span data-stu-id="afda7-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="afda7-391">**Nazwa**: nazwę reguły równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="afda7-392">**Adres IP frontonu**: Użyj hello adresu IP dla hello zasobu sieciowego klastra programu SQL Server infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="afda7-393">**Port**: Ustaw dla hello port TCP programu SQL Server infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="afda7-394">Witaj domyślnego wystąpienia portu to 1433.</span><span class="sxs-lookup"><span data-stu-id="afda7-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="afda7-395">**Port zaplecza**: Ta wartość używa hello sam portu jako hello **portu** wartość po włączeniu **pływającego adresu IP (bezpośredni zwrot serwera)**.</span><span class="sxs-lookup"><span data-stu-id="afda7-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="afda7-396">**Puli zaplecza**: Nazwa puli zaplecza hello Użyj, wcześniej skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="afda7-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="afda7-397">**Sondy kondycji**: badanie kondycji hello użycia, które skonfigurowane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="afda7-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="afda7-398">**Trwałość sesji**: Brak.</span><span class="sxs-lookup"><span data-stu-id="afda7-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="afda7-399">**Czas bezczynności (w minutach)**: 4.</span><span class="sxs-lookup"><span data-stu-id="afda7-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="afda7-400">**Zmienny adres IP (bezpośredni zwrot serwera)**: włączone</span><span class="sxs-lookup"><span data-stu-id="afda7-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="afda7-401">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="afda7-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="afda7-402">Krok 6: Konfigurowanie klastra dla sondy</span><span class="sxs-lookup"><span data-stu-id="afda7-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="afda7-403">Wartość parametru port sondy klastra hello w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afda7-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="afda7-404">tooset hello parametru port sondy klastra, zaktualizuj zmienne w hello następującego skryptu ze środowiska.</span><span class="sxs-lookup"><span data-stu-id="afda7-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="afda7-405">Krok 7: Testowanie trybu failover z infrastruktury klasyfikacji plików</span><span class="sxs-lookup"><span data-stu-id="afda7-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="afda7-406">Testowanie pracy awaryjnej hello funkcje klastra toovalidate infrastruktury klasyfikacji plików.</span><span class="sxs-lookup"><span data-stu-id="afda7-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="afda7-407">Witaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="afda7-407">Do hello following steps:</span></span>

1. <span data-ttu-id="afda7-408">Połącz tooone węzłów klastra programu SQL Server FCI hello z protokołem RDP.</span><span class="sxs-lookup"><span data-stu-id="afda7-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="afda7-409">Otwórz **Menedżera klastra trybu Failover**.</span><span class="sxs-lookup"><span data-stu-id="afda7-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="afda7-410">Kliknij przycisk **ról**.</span><span class="sxs-lookup"><span data-stu-id="afda7-410">Click **Roles**.</span></span> <span data-ttu-id="afda7-411">Powiadomienia, który węzeł jest właścicielem roli SQL Server FCI hello.</span><span class="sxs-lookup"><span data-stu-id="afda7-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="afda7-412">Kliknij prawym przyciskiem myszy hello roli SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="afda7-413">Kliknij przycisk **Przenieś** i kliknij przycisk **najlepszego możliwego węzła**.</span><span class="sxs-lookup"><span data-stu-id="afda7-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="afda7-414">**Menedżer klastra trybu failover** pokazuje hello roli i jej zasobach przejścia do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="afda7-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="afda7-415">Witaj zasobów następnie przenieś i przejdzie w tryb online hello na inny węzeł.</span><span class="sxs-lookup"><span data-stu-id="afda7-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="afda7-416">Testowanie łączności</span><span class="sxs-lookup"><span data-stu-id="afda7-416">Test connectivity</span></span>

<span data-ttu-id="afda7-417">połączenie tootest, logowanie tooanother maszyny wirtualnej w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afda7-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="afda7-418">Otwórz **programu SQL Server Management Studio** i połącz toohello Nazwa SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="afda7-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="afda7-419">Jeśli to konieczne, możesz [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="afda7-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="afda7-420">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="afda7-420">Limitations</span></span>
<span data-ttu-id="afda7-421">Na maszynach wirtualnych Azure Microsoft Distributed Transaction Coordinator (DTC) nie jest obsługiwana na wystąpienia ponieważ hello portu RPC nie jest obsługiwana przez hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afda7-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="afda7-422">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="afda7-422">See Also</span></span>

[<span data-ttu-id="afda7-423">Instalacja S2D przy użyciu pulpitu zdalnego (Azure)</span><span class="sxs-lookup"><span data-stu-id="afda7-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="afda7-424">[Zbieżność Hyper rozwiązania z bezpośrednie miejsca do magazynowania](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="afda7-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="afda7-425">Omówienie bezpośrednie miejsca magazynu</span><span class="sxs-lookup"><span data-stu-id="afda7-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="afda7-426">Obsługa programu SQL Server dla S2D</span><span class="sxs-lookup"><span data-stu-id="afda7-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
