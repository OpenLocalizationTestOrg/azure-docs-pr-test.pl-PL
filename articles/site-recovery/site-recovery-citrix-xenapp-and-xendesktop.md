---
title: "aaaReplicate wdrażania Citrix XenDesktop i program XenApp wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooprotect Odzyskaj Citrix XenDesktop i program XenApp wdrożenia i przy użyciu usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="21892-103">Replikowanie wdrażania program Citrix XenApp i XenDesktop wielowarstwową przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="21892-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="21892-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="21892-104">Overview</span></span>

<span data-ttu-id="21892-105">Citrix XenDesktop to rozwiązanie wirtualizacji pulpitu, polegającego na dostarczaniu pulpitów i aplikacji na żądanie usługi tooany użytkownik dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="21892-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="21892-106">Dzięki technologii dostarczania FlexCast XenDesktop szybko i bezpiecznie zapewnia aplikacji i toousers komputerów stacjonarnych.</span><span class="sxs-lookup"><span data-stu-id="21892-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="21892-107">Obecnie program Citrix XenApp nie zapewnia żadnych po awarii możliwości odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="21892-108">Dobre rozwiązanie odzyskiwania po awarii, należy zezwala modelowania planów odzyskiwania wokół hello powyżej architekturach aplikacji złożonych i również mieć hello możliwości tooadd dostosowane kroki toohandle aplikacji mapowań między różnych warstw, dlatego zapewnienie jednym kliknięciem się, że zrzut rozwiązanie w przypadku awarii wiodące tooa hello obniżyć RTO.</span><span class="sxs-lookup"><span data-stu-id="21892-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="21892-109">Ten dokument zawiera wskazówki krok po kroku budowania rozwiązanie odzyskiwania po awarii dla lokalnej program Citrix XenApp wdrożeniach funkcji Hyper-V i oprogramowania VMware vSphere platform.</span><span class="sxs-lookup"><span data-stu-id="21892-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="21892-110">Ten dokument zawiera również opis sposobu tooperform test trybu failover (wyszczególniania odzyskiwania po awarii) i tooAzure nieplanowanego trybu failover przy użyciu planów odzyskiwania, hello obsługiwane konfiguracje i wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="21892-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="21892-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="21892-111">Prerequisites</span></span>

<span data-ttu-id="21892-112">Przed rozpoczęciem upewnij się, że rozumiesz hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="21892-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="21892-113">Replikowanie tooAzure maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="21892-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="21892-114">Jak zbyt[projektowania sieci odzyskiwania](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="21892-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="21892-115">Ten test trybu failover tooAzure</span><span class="sxs-lookup"><span data-stu-id="21892-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="21892-116">Sposób tooAzure trybu failover</span><span class="sxs-lookup"><span data-stu-id="21892-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="21892-117">Jak zbyt[replikacji kontrolera domeny](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="21892-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="21892-118">Jak zbyt[replikacji programu SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="21892-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="21892-119">Wzorce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="21892-119">Deployment patterns</span></span>

<span data-ttu-id="21892-120">Farma program Citrix XenApp i XenDesktop ma zazwyczaj hello następującego wzorca wdrażania:</span><span class="sxs-lookup"><span data-stu-id="21892-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="21892-121">**Wzorzec wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="21892-121">**Deployment pattern**</span></span>

<span data-ttu-id="21892-122">Program Citrix XenApp i XenDesktop wdrożenia z serwerem AD, DNS, SQL bazy danych serwera, Citrix dostarczania kontrolera sklepu server, program XenApp głównego (VDA), serwer licencji na program XenApp Citrix</span><span class="sxs-lookup"><span data-stu-id="21892-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Wzorzec wdrożenia 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="21892-124">Obsługa odzyskiwania lokacji</span><span class="sxs-lookup"><span data-stu-id="21892-124">Site Recovery support</span></span>

<span data-ttu-id="21892-125">W celu hello w tym artykule Citrix wdrożeń na maszynach wirtualnych VMware zarządza vSphere w wersji 6.0 / System Center VMM 2012 R2 były używane toosetup odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="21892-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="21892-126">Źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="21892-126">Source and target</span></span>

<span data-ttu-id="21892-127">**Scenariusz**</span><span class="sxs-lookup"><span data-stu-id="21892-127">**Scenario**</span></span> | <span data-ttu-id="21892-128">**tooa lokacji dodatkowej**</span><span class="sxs-lookup"><span data-stu-id="21892-128">**tooa secondary site**</span></span> | <span data-ttu-id="21892-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="21892-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="21892-130">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="21892-130">**Hyper-V**</span></span> | <span data-ttu-id="21892-131">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="21892-131">Not in scope</span></span> | <span data-ttu-id="21892-132">Tak</span><span class="sxs-lookup"><span data-stu-id="21892-132">Yes</span></span>
<span data-ttu-id="21892-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="21892-133">**VMware**</span></span> | <span data-ttu-id="21892-134">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="21892-134">Not in scope</span></span> | <span data-ttu-id="21892-135">Tak</span><span class="sxs-lookup"><span data-stu-id="21892-135">Yes</span></span>
<span data-ttu-id="21892-136">**Serwer fizyczny**</span><span class="sxs-lookup"><span data-stu-id="21892-136">**Physical server**</span></span> | <span data-ttu-id="21892-137">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="21892-137">Not in scope</span></span> | <span data-ttu-id="21892-138">Tak</span><span class="sxs-lookup"><span data-stu-id="21892-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="21892-139">Wersje</span><span class="sxs-lookup"><span data-stu-id="21892-139">Versions</span></span>
<span data-ttu-id="21892-140">Klienci mogą wdrożyć program XenApp składniki jako maszynami wirtualnymi funkcji Hyper-V lub programu VMware lub serwerach fizycznych.</span><span class="sxs-lookup"><span data-stu-id="21892-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="21892-141">Usługa Azure Site Recovery może chronić tooAzure obu wdrożeń fizycznych i wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="21892-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="21892-142">Ponieważ program XenApp 7,7 lub nowszej jest obsługiwana na platformie Azure, można nie tylko wdrożenia z tych wersji za pośrednictwem tooAzure dla odzyskiwania po awarii lub migracji.</span><span class="sxs-lookup"><span data-stu-id="21892-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="21892-143">Tookeep rzeczy pamiętać</span><span class="sxs-lookup"><span data-stu-id="21892-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="21892-144">Ochrona i odzyskiwanie z lokalnego wdrożenia przy użyciu serwerowy system operacyjny maszyny toodeliver program XenApp opublikowane aplikacje i program XenApp publikowane komputerów stacjonarnych jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="21892-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="21892-145">Ochrona i odzyskiwanie wdrożenia lokalnego przy użyciu pulpitu systemu operacyjnego maszyny toodeliver Pulpitów dla pulpitów wirtualnych klienta, w tym Windows 10 nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="21892-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="21892-146">Jest tak, ponieważ funkcja automatycznego odzyskiwania systemu nie obsługuje odzyskiwania hello maszyn z pulpitem OS'es.</span><span class="sxs-lookup"><span data-stu-id="21892-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="21892-147">Ponadto niektóre klienta pulpitu wirtualnego smaki (np.)</span><span class="sxs-lookup"><span data-stu-id="21892-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="21892-148">Windows 7) nie są jeszcze obsługiwane w przypadku licencjonowania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="21892-149">[Dowiedz się więcej](https://azure.microsoft.com/pricing/licensing-faq/) na temat licencjonowania dla komputerów stacjonarnych klienta/serwera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="21892-150">Usługa Azure Site Recovery nie może replikować i ochronę istniejących klony MCS lub Odwiedziny lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="21892-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="21892-151">Należy toorecreate tych fragmentach operacje przy użyciu Menedżera zasobów Azure inicjowania obsługi administracyjnej z kontrolera dostarczania.</span><span class="sxs-lookup"><span data-stu-id="21892-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="21892-152">NetScaler nie mogą być chronione przy użyciu usługi Azure Site Recovery NetScaler jest oparta na FreeBSD i usługi Azure Site Recovery nie obsługuje ochrony FreeBSD systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="21892-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="21892-153">Będzie konieczne toodeploy i skonfiguruj nowe urządzenie NetScaler z rynku Azure po tooAzure pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="21892-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="21892-154">Replikowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="21892-154">Replicating virtual machines</span></span>

<span data-ttu-id="21892-155">następujące składniki hello wdrożenia program Citrix XenApp Hello muszą toobe chronione tooenable replikacji i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="21892-156">Ochrona serwera AD DNS</span><span class="sxs-lookup"><span data-stu-id="21892-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="21892-157">Ochrona serwera bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="21892-157">Protection of SQL database server</span></span>
* <span data-ttu-id="21892-158">Ochrona kontrolera dostarczania Citrix</span><span class="sxs-lookup"><span data-stu-id="21892-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="21892-159">Ochrona serwera sklepu.</span><span class="sxs-lookup"><span data-stu-id="21892-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="21892-160">Ochrona program XenApp wzorca (VDA)</span><span class="sxs-lookup"><span data-stu-id="21892-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="21892-161">Ochrona program Citrix XenApp serwera licencji</span><span class="sxs-lookup"><span data-stu-id="21892-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="21892-162">**Replikacja serwer AD DNS**</span><span class="sxs-lookup"><span data-stu-id="21892-162">**AD DNS server replication**</span></span>

<span data-ttu-id="21892-163">Zobacz zbyt[ochrony usługi Active Directory i DNS z usługą Azure Site Recovery](site-recovery-active-directory.md) na wskazówki dotyczące replikacji i konfigurowania kontrolera domeny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="21892-164">**Replikacja serwer bazy danych SQL**</span><span class="sxs-lookup"><span data-stu-id="21892-164">**SQL database Server replication**</span></span>

<span data-ttu-id="21892-165">Zobacz zbyt[ochrony programu SQL Server z odzyskiwania po awarii programu SQL Server i usługi Azure Site Recovery](site-recovery-sql.md) techniczne wskazówki dotyczące hello zalecane opcje ochrony serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="21892-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="21892-166">Postępuj zgodnie z [w tych wskazówkach](site-recovery-vmware-to-azure.md) replikowanie toostart hello tooAzure maszyn wirtualnych innych składników.</span><span class="sxs-lookup"><span data-stu-id="21892-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Ochrona program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="21892-168">**Ustawienia sieci i obliczeń**</span><span class="sxs-lookup"><span data-stu-id="21892-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="21892-169">Po hello maszyn objętych ochroną (pokazuje stan jako "Protected" w obszarze elementy replikowane), hello obliczeń i toobe skonfigurowane wymagane ustawienia sieciowe.</span><span class="sxs-lookup"><span data-stu-id="21892-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="21892-170">W obliczenia i sieć > obliczeniowe właściwości, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="21892-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="21892-171">Zmodyfikować hello toocomply nazwy z wymagania dotyczące usługi Azure, jeśli potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="21892-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="21892-172">Można również wyświetlić i dodać informacje dotyczące sieci docelowej hello, podsieci i adres IP, który zostanie przypisany toohello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="21892-173">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="21892-173">Note hello following:</span></span>

* <span data-ttu-id="21892-174">Można ustawić hello docelowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="21892-174">You can set hello target IP address.</span></span> <span data-ttu-id="21892-175">Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="21892-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="21892-176">Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover nie będzie działać.</span><span class="sxs-lookup"><span data-stu-id="21892-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="21892-177">Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.</span><span class="sxs-lookup"><span data-stu-id="21892-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="21892-178">Dla serwera AD DNS hello zachowując hello lokalnymi pozwala adres określić hello sama adresu jako powitania serwera DNS dla sieci wirtualnej Azure hello.</span><span class="sxs-lookup"><span data-stu-id="21892-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="21892-179">Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="21892-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="21892-180">Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.</span><span class="sxs-lookup"><span data-stu-id="21892-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="21892-181">Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.</span><span class="sxs-lookup"><span data-stu-id="21892-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="21892-182">Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="21892-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="21892-183">Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.</span><span class="sxs-lookup"><span data-stu-id="21892-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="21892-184">Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.</span><span class="sxs-lookup"><span data-stu-id="21892-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="21892-185">Jeśli maszyna wirtualna hello ma wiele kart sieciowych, hello pierwszego wyświetlane na liście hello staje się hello domyślnej karty sieciowej hello maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="21892-186">Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="21892-186">Creating a recovery plan</span></span>

<span data-ttu-id="21892-187">Po włączeniu replikacji dla hello maszyn wirtualnych składnika program XenApp hello następnym krokiem jest toocreate planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="21892-188">Odzyskiwanie Planowanie grup razem maszyny wirtualne mają podobne wymagania dotyczące trybu failover i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="21892-189">**Kroki toocreate planu odzyskiwania**</span><span class="sxs-lookup"><span data-stu-id="21892-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="21892-190">Dodaj maszyny wirtualne składnika program XenApp hello w hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="21892-191">Kliknij przycisk planów odzyskiwania -> + planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="21892-192">Podaj nazwę intuicyjne hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="21892-193">W przypadku maszyn wirtualnych VMware: Wybierz źródło jako serwer przetwarzania VMware, element docelowy jako Microsoft Azure i modelu wdrażania usługi Resource Manager i wybierz elementy, kliknij polecenie.</span><span class="sxs-lookup"><span data-stu-id="21892-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="21892-194">W przypadku maszyn wirtualnych funkcji Hyper-V: Wybierz źródło jako serwer programu VMM, docelowy jako Microsoft Azure i modelu wdrażania jak Menedżer zasobów i kliknij pozycję Wybierz elementy, a następnie wybierz hello program XenApp wdrażania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="21892-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="21892-195">Dodawanie grup toofailover maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="21892-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="21892-196">Plany odzyskiwania może być dostosowane tooadd trybu failover grupy działań zamówienia, skrypty lub ręcznego uruchamiania określonego.</span><span class="sxs-lookup"><span data-stu-id="21892-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="21892-197">Witaj następujące grupy muszą planu odzyskiwania dodano toohello toobe.</span><span class="sxs-lookup"><span data-stu-id="21892-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="21892-198">Grupa1 trybu failover: DNS AD</span><span class="sxs-lookup"><span data-stu-id="21892-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="21892-199">Grupa2 trybu failover: Maszyny wirtualne SQL Server</span><span class="sxs-lookup"><span data-stu-id="21892-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="21892-200">Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA</span><span class="sxs-lookup"><span data-stu-id="21892-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="21892-201">Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu</span><span class="sxs-lookup"><span data-stu-id="21892-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="21892-202">Dodawanie skryptów toohello planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="21892-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="21892-203">Można uruchamiać skrypty przed lub po określonej grupy w planie odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="21892-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="21892-204">Ręczne akcje mogą być również być uwzględnione i wykonywane w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="21892-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="21892-205">plan odzyskiwania dostosowane Hello wygląda hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="21892-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="21892-206">Grupa1 trybu failover: DNS AD</span><span class="sxs-lookup"><span data-stu-id="21892-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="21892-207">Grupa2 trybu failover: Maszyny wirtualne SQL Server</span><span class="sxs-lookup"><span data-stu-id="21892-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="21892-208">Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA</span><span class="sxs-lookup"><span data-stu-id="21892-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="21892-209">Kroki 4, 6 i 7 zawierający akcje ręczne lub skryptu są stosowane tooonly program XenApp lokalnymi > środowisko z katalogami MCS/Odwiedziny.</span><span class="sxs-lookup"><span data-stu-id="21892-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="21892-210">Akcja ręczna lub skryptu grupa 3: zamknięcie wzorca hello VDA maszyny Wirtualnej VM VDA wzorca podczas przejścia w tryb failover tooAzure będzie w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="21892-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="21892-211">toocreate nowego serwera MCS katalogów przy użyciu hostingu Azure ARM, wzorzec hello VDA maszyny Wirtualnej jest wymagana toobe w zatrzymane (de przydzielone) stanu.</span><span class="sxs-lookup"><span data-stu-id="21892-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="21892-212">Witaj zamykania maszyny Wirtualnej z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="21892-213">Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu</span><span class="sxs-lookup"><span data-stu-id="21892-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="21892-214">Grupa 3 ręczny lub skryptu akcji 1:</span><span class="sxs-lookup"><span data-stu-id="21892-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="21892-215">***Dodaj połączenie hostów protokołu RM Azure***</span><span class="sxs-lookup"><span data-stu-id="21892-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="21892-216">Utwórz połączenia hosta Azure ARM tooprovision maszyny kontrolera dostarczania nowych katalogów serwera MCS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="21892-217">Wykonaj kroki hello, zgodnie z objaśnieniem w tym [artykułu](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="21892-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="21892-218">Grupa 3 ręczny lub skryptu akcji 2:</span><span class="sxs-lookup"><span data-stu-id="21892-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="21892-219">***Utwórz ponownie MCS katalogi na platformie Azure***</span><span class="sxs-lookup"><span data-stu-id="21892-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="21892-220">Hello istniejącego serwera MCS lub Odwiedziny klony w lokacji głównej hello nie będą replikowane tooAzure.</span><span class="sxs-lookup"><span data-stu-id="21892-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="21892-221">Należy toorecreate tych fragmentach operacje przy użyciu hello replikowane VDA wzorca i Azure ARM inicjowania obsługi administracyjnej z kontrolera dostarczania. Wykonaj kroki hello, zgodnie z objaśnieniem w tym [artykułu](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS kataloguje na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21892-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Plan odzyskiwania program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="21892-223">Możesz używać skryptów w [lokalizacji](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS z hello nowe adresy IP z hello przejścia w tryb failover > maszyn wirtualnych lub tooattach modułu równoważenia obciążenia na powitania przejścia w tryb failover maszyny wirtualnej, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="21892-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="21892-224">Ten test trybu failover</span><span class="sxs-lookup"><span data-stu-id="21892-224">Doing a test failover</span></span>

<span data-ttu-id="21892-225">Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="21892-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Plan odzyskiwania](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="21892-227">Podczas pracy w trybie failover</span><span class="sxs-lookup"><span data-stu-id="21892-227">Doing a failover</span></span>

<span data-ttu-id="21892-228">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="21892-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21892-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21892-229">Next steps</span></span>

<span data-ttu-id="21892-230">Możesz [więcej](https://aka.ms/citrix-xenapp-xendesktop-with-asr) o replikowanie wdrożenia program Citrix XenApp i XenDesktop w oficjalnym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="21892-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="21892-231">Obejrzyj wskazówki hello zbyt[replikacji z innych aplikacji](site-recovery-workload.md) przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="21892-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
