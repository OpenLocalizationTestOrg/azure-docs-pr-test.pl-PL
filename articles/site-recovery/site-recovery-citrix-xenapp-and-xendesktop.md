---
title: "Replikowanie wdrażania Citrix XenDesktop i program XenApp wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak chronić i odzyskiwać Citrix XenDesktop i program XenApp wdrożenia przy użyciu usługi Azure Site Recovery."
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
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="57680-103">Replikowanie wdrażania program Citrix XenApp i XenDesktop wielowarstwową przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="57680-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="57680-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="57680-104">Overview</span></span>

<span data-ttu-id="57680-105">Citrix XenDesktop to rozwiązanie wirtualizacji pulpitu, polegającego na dostarczaniu pulpity i aplikacje jako usługa na żądanie do dowolnego miejsca i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57680-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="57680-106">Dzięki technologii dostarczania FlexCast XenDesktop można szybko i bezpiecznie dostarczania aplikacji i pulpitów do użytkowników.</span><span class="sxs-lookup"><span data-stu-id="57680-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="57680-107">Obecnie program Citrix XenApp nie zapewnia żadnych po awarii możliwości odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="57680-108">Dobre rozwiązanie odzyskiwania po awarii, powinno umożliwić modelowania planów odzyskiwania wokół powyższych architekturach aplikacji złożonych, a także mieć możliwość dodawania kroków dostosowane do obsługi aplikacji mapowań między różnych warstw, dlatego zapewnienie pojedynczym kliknięciem czy zrzut rozwiązanie w przypadku awarii, co może prowadzić do dolnej RTO.</span><span class="sxs-lookup"><span data-stu-id="57680-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="57680-109">Ten dokument zawiera wskazówki krok po kroku budowania rozwiązanie odzyskiwania po awarii dla lokalnej program Citrix XenApp wdrożeniach funkcji Hyper-V i oprogramowania VMware vSphere platform.</span><span class="sxs-lookup"><span data-stu-id="57680-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="57680-110">Ten dokument opisuje również sposób wykonywania testowy tryb failover (wyszczególniania odzyskiwania po awarii) i nieplanowany tryb failover na platformie Azure przy użyciu planów odzyskiwania, obsługiwane konfiguracje i wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="57680-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="57680-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="57680-111">Prerequisites</span></span>

<span data-ttu-id="57680-112">Przed rozpoczęciem upewnij się, że należy zrozumieć następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="57680-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="57680-113">Replikacja maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="57680-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="57680-114">Jak [projektowania sieci odzyskiwania](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="57680-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="57680-115">Ten test trybu failover na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="57680-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="57680-116">Podczas pracy w trybie failover na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="57680-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="57680-117">Jak [replikacji kontrolera domeny](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="57680-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="57680-118">Jak [replikacji programu SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="57680-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="57680-119">Wzorce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="57680-119">Deployment patterns</span></span>

<span data-ttu-id="57680-120">Farma program Citrix XenApp i XenDesktop ma zazwyczaj następującego wzorca wdrażania:</span><span class="sxs-lookup"><span data-stu-id="57680-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="57680-121">**Wzorzec wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="57680-121">**Deployment pattern**</span></span>

<span data-ttu-id="57680-122">Program Citrix XenApp i XenDesktop wdrożenia z serwerem AD, DNS, SQL bazy danych serwera, Citrix dostarczania kontrolera sklepu server, program XenApp głównego (VDA), serwer licencji na program XenApp Citrix</span><span class="sxs-lookup"><span data-stu-id="57680-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Wzorzec wdrożenia 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="57680-124">Obsługa odzyskiwania lokacji</span><span class="sxs-lookup"><span data-stu-id="57680-124">Site Recovery support</span></span>

<span data-ttu-id="57680-125">Na potrzeby tego artykułu Citrix wdrożeń na maszynach wirtualnych VMware zarządza vSphere w wersji 6.0 / System Center VMM 2012 R2 użyto w celu ustawienia odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="57680-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="57680-126">Źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="57680-126">Source and target</span></span>

<span data-ttu-id="57680-127">**Scenariusz**</span><span class="sxs-lookup"><span data-stu-id="57680-127">**Scenario**</span></span> | <span data-ttu-id="57680-128">**Do lokacji dodatkowej**</span><span class="sxs-lookup"><span data-stu-id="57680-128">**To a secondary site**</span></span> | <span data-ttu-id="57680-129">**Na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="57680-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="57680-130">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="57680-130">**Hyper-V**</span></span> | <span data-ttu-id="57680-131">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="57680-131">Not in scope</span></span> | <span data-ttu-id="57680-132">Tak</span><span class="sxs-lookup"><span data-stu-id="57680-132">Yes</span></span>
<span data-ttu-id="57680-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="57680-133">**VMware**</span></span> | <span data-ttu-id="57680-134">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="57680-134">Not in scope</span></span> | <span data-ttu-id="57680-135">Tak</span><span class="sxs-lookup"><span data-stu-id="57680-135">Yes</span></span>
<span data-ttu-id="57680-136">**Serwer fizyczny**</span><span class="sxs-lookup"><span data-stu-id="57680-136">**Physical server**</span></span> | <span data-ttu-id="57680-137">Nie znajduje się w zakresie</span><span class="sxs-lookup"><span data-stu-id="57680-137">Not in scope</span></span> | <span data-ttu-id="57680-138">Tak</span><span class="sxs-lookup"><span data-stu-id="57680-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="57680-139">Wersje</span><span class="sxs-lookup"><span data-stu-id="57680-139">Versions</span></span>
<span data-ttu-id="57680-140">Klienci mogą wdrożyć program XenApp składniki jako maszynami wirtualnymi funkcji Hyper-V lub programu VMware lub serwerach fizycznych.</span><span class="sxs-lookup"><span data-stu-id="57680-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="57680-141">Usługa Azure Site Recovery może chronić wdrożeń fizycznych i wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="57680-142">Ponieważ program XenApp 7,7 lub nowszej jest obsługiwana na platformie Azure, tylko wdrożenia z tymi wersjami mogą można przełączyć do platformy Azure dla odzyskiwania po awarii lub migracji.</span><span class="sxs-lookup"><span data-stu-id="57680-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="57680-143">Warto pamiętać o</span><span class="sxs-lookup"><span data-stu-id="57680-143">Things to keep in mind</span></span>

1. <span data-ttu-id="57680-144">Ochrona i odzyskiwanie z lokalnego wdrożenia przy użyciu serwerowy system operacyjny maszyny w celu dostarczenia program XenApp opublikowane aplikacje i program XenApp publikowane komputerów stacjonarnych jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="57680-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="57680-145">Ochrona i odzyskiwanie wdrożeń lokalnych przy użyciu pulpitu systemu operacyjnego maszyny do dostarczania Pulpitów dla klienta pulpitów wirtualnych, w tym Windows 10 nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="57680-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="57680-146">Jest tak, ponieważ funkcja automatycznego odzyskiwania systemu nie obsługuje odzyskiwania maszyn z pulpitem OS'es.</span><span class="sxs-lookup"><span data-stu-id="57680-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="57680-147">Ponadto niektóre klienta pulpitu wirtualnego smaki (np.)</span><span class="sxs-lookup"><span data-stu-id="57680-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="57680-148">Windows 7) nie są jeszcze obsługiwane w przypadku licencjonowania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="57680-149">[Dowiedz się więcej](https://azure.microsoft.com/pricing/licensing-faq/) na temat licencjonowania dla komputerów stacjonarnych klienta/serwera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="57680-150">Usługa Azure Site Recovery nie może replikować i ochronę istniejących klony MCS lub Odwiedziny lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="57680-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="57680-151">Należy ponownie utworzyć te klony za pomocą Menedżera zasobów Azure inicjowania obsługi administracyjnej z kontrolera dostarczania.</span><span class="sxs-lookup"><span data-stu-id="57680-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="57680-152">NetScaler nie mogą być chronione przy użyciu usługi Azure Site Recovery NetScaler jest oparta na FreeBSD i usługi Azure Site Recovery nie obsługuje ochrony FreeBSD systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="57680-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="57680-153">Będzie potrzebny do wdrożenia i skonfigurowania nowego urządzenia NetScaler z rynku Azure po przejściu w tryb failover Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="57680-154">Replikowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="57680-154">Replicating virtual machines</span></span>

<span data-ttu-id="57680-155">Następujące składniki wdrożenia program Citrix XenApp muszą być chronione, aby włączyć replikację i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="57680-156">Ochrona serwera AD DNS</span><span class="sxs-lookup"><span data-stu-id="57680-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="57680-157">Ochrona serwera bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="57680-157">Protection of SQL database server</span></span>
* <span data-ttu-id="57680-158">Ochrona kontrolera dostarczania Citrix</span><span class="sxs-lookup"><span data-stu-id="57680-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="57680-159">Ochrona serwera sklepu.</span><span class="sxs-lookup"><span data-stu-id="57680-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="57680-160">Ochrona program XenApp wzorca (VDA)</span><span class="sxs-lookup"><span data-stu-id="57680-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="57680-161">Ochrona program Citrix XenApp serwera licencji</span><span class="sxs-lookup"><span data-stu-id="57680-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="57680-162">**Replikacja serwer AD DNS**</span><span class="sxs-lookup"><span data-stu-id="57680-162">**AD DNS server replication**</span></span>

<span data-ttu-id="57680-163">Zapoznaj się z [ochrony usługi Active Directory i DNS z usługą Azure Site Recovery](site-recovery-active-directory.md) na wskazówki dotyczące replikacji i konfigurowania kontrolera domeny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="57680-164">**Replikacja serwer bazy danych SQL**</span><span class="sxs-lookup"><span data-stu-id="57680-164">**SQL database Server replication**</span></span>

<span data-ttu-id="57680-165">Zapoznaj się z [ochrony programu SQL Server z odzyskiwania po awarii programu SQL Server i usługi Azure Site Recovery](site-recovery-sql.md) szczegółowe wskazówki techniczne na temat zalecanych opcji ochrony serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="57680-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="57680-166">Postępuj zgodnie z [w tych wskazówkach](site-recovery-vmware-to-azure.md) do rozpoczęcia replikacji z innych składników maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![Ochrona program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="57680-168">**Ustawienia sieci i obliczeń**</span><span class="sxs-lookup"><span data-stu-id="57680-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="57680-169">Po maszyn objętych ochroną (stan to "Protected" w obszarze elementy replikowane), należy skonfigurować ustawienia obliczeń i sieci.</span><span class="sxs-lookup"><span data-stu-id="57680-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="57680-170">W obliczenia i sieć > obliczeniowe właściwości, można określić nazwę i docelowy rozmiar maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="57680-171">Zmodyfikuj nazwę, aby spełniać wymagania dotyczące usługi Azure, jeśli potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="57680-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="57680-172">Można również wyświetlić i dodać informacje dotyczące sieci docelowej, podsieci i adres IP, który zostanie przypisany do maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="57680-173">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="57680-173">Note the following:</span></span>

* <span data-ttu-id="57680-174">Możesz ustawić docelowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="57680-174">You can set the target IP address.</span></span> <span data-ttu-id="57680-175">Jeśli nie podasz adresu, maszyna w trybie failover będzie używać protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="57680-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="57680-176">Jeśli ustawisz adres, który nie jest dostępna w trybie failover, przejście w tryb failover nie będzie działać.</span><span class="sxs-lookup"><span data-stu-id="57680-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="57680-177">Ten sam docelowy adres IP może być użyty do testowania trybu failover, jeśli adres jest dostępny w testowej sieci trybu failover.</span><span class="sxs-lookup"><span data-stu-id="57680-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="57680-178">Dla serwera AD DNS zachowując adresu lokalnego pozwala określić ten sam adres jako serwer DNS w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="57680-179">Liczba kart sieciowych zależy od rozmiaru określonego dla docelowej maszyny wirtualnej, zgodnie z poniższym:</span><span class="sxs-lookup"><span data-stu-id="57680-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="57680-180">Jeśli liczba kart sieciowych w maszynie źródłowej jest mniejsza lub równa liczbie kart sieciowych dozwolonych dla rozmiaru maszyny docelowej, maszyna docelowa będzie mieć taką samą liczbę kart sieciowych jak maszyna źródłowa.</span><span class="sxs-lookup"><span data-stu-id="57680-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="57680-181">Jeśli liczba kart sieciowych dla źródłowej maszyny wirtualnej przekracza liczbę dozwolonych kart sieciowych dla rozmiaru maszyny docelowej, zostanie użyta maksymalna liczba kart dla rozmiaru maszyny docelowej.</span><span class="sxs-lookup"><span data-stu-id="57680-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="57680-182">Na przykład, jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej obsługuje cztery karty, maszyna docelowa będzie mieć dwie karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="57680-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="57680-183">Jeśli maszyna źródłowa ma dwie karty sieciowe, ale rozmiar maszyny docelowej obsługuje tylko jedną kartę, maszyna docelowa będzie mieć tylko jedną kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="57680-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="57680-184">Jeśli maszyna wirtualna ma wiele kart sieciowych, wszystkie będą łączyć z tą samą siecią.</span><span class="sxs-lookup"><span data-stu-id="57680-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="57680-185">Jeśli maszyna wirtualna ma wiele kart sieciowych, pierwsza z nich wyświetlane na liście staje się domyślnej karty sieciowej na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="57680-186">Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="57680-186">Creating a recovery plan</span></span>

<span data-ttu-id="57680-187">Po włączeniu replikacji dla maszyn wirtualnych program XenApp składnika następnym krokiem jest utworzenie planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="57680-188">Odzyskiwanie Planowanie grup razem maszyny wirtualne mają podobne wymagania dotyczące trybu failover i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="57680-189">**Kroki umożliwiające utworzenie planu odzyskiwania**</span><span class="sxs-lookup"><span data-stu-id="57680-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="57680-190">Dodawanie maszyn wirtualnych składnika program XenApp w planie odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="57680-191">Kliknij przycisk planów odzyskiwania -> + planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="57680-192">Podaj nazwę intuicyjne planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="57680-193">W przypadku maszyn wirtualnych VMware: Wybierz źródło jako serwer przetwarzania VMware, element docelowy jako Microsoft Azure i modelu wdrażania usługi Resource Manager i wybierz elementy, kliknij polecenie.</span><span class="sxs-lookup"><span data-stu-id="57680-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="57680-194">W przypadku maszyn wirtualnych funkcji Hyper-V: Wybierz źródło jako serwer programu VMM, docelowy jako Microsoft Azure i modelu wdrażania jak Menedżer zasobów i kliknij pozycję Wybierz elementy, a następnie wybierz program XenApp wdrażania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57680-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="57680-195">Dodawanie maszyn wirtualnych do trybu failover grupy</span><span class="sxs-lookup"><span data-stu-id="57680-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="57680-196">Plany odzyskiwania można dostosować, aby dodać grupy pracy awaryjnej dla kolejności uruchamiania określonego, skrypty i działań ręcznych.</span><span class="sxs-lookup"><span data-stu-id="57680-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="57680-197">Następujące grupy muszą być dodane do planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="57680-198">Grupa1 trybu failover: DNS AD</span><span class="sxs-lookup"><span data-stu-id="57680-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="57680-199">Grupa2 trybu failover: Maszyny wirtualne SQL Server</span><span class="sxs-lookup"><span data-stu-id="57680-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="57680-200">Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA</span><span class="sxs-lookup"><span data-stu-id="57680-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="57680-201">Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu</span><span class="sxs-lookup"><span data-stu-id="57680-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="57680-202">Dodawanie skryptów do planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="57680-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="57680-203">Można uruchamiać skrypty przed lub po określonej grupy w planie odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="57680-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="57680-204">Ręczne akcje mogą być również być uwzględnione i wykonywane w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="57680-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="57680-205">Plan odzyskiwania dostosowane wygląda jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="57680-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="57680-206">Grupa1 trybu failover: DNS AD</span><span class="sxs-lookup"><span data-stu-id="57680-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="57680-207">Grupa2 trybu failover: Maszyny wirtualne SQL Server</span><span class="sxs-lookup"><span data-stu-id="57680-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="57680-208">Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA</span><span class="sxs-lookup"><span data-stu-id="57680-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="57680-209">Kroki 4, 6 i 7 zawierający akcje ręczne lub skryptu dotyczą tylko program XenApp lokalnymi > środowisko z katalogami MCS/Odwiedziny.</span><span class="sxs-lookup"><span data-stu-id="57680-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="57680-210">Akcja ręczna lub skryptu grupa 3: zamknięcie wzorca VDA maszyny Wirtualnej wzorca VDA maszyny Wirtualnej po awarii Azure będzie w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="57680-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="57680-211">Aby utworzyć nowe katalogi MCS przy użyciu hostingu Azure ARM, głównego maszyna wirtualna VDA jest wymagane będzie zatrzymane (de przydzielone) stanu.</span><span class="sxs-lookup"><span data-stu-id="57680-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="57680-212">Zamknij maszynę Wirtualną z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="57680-213">Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu</span><span class="sxs-lookup"><span data-stu-id="57680-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="57680-214">Grupa 3 ręczny lub skryptu akcji 1:</span><span class="sxs-lookup"><span data-stu-id="57680-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="57680-215">***Dodaj połączenie hostów protokołu RM Azure***</span><span class="sxs-lookup"><span data-stu-id="57680-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="57680-216">Utwórz połączenie hosta Azure ARM na maszynie kontrolera dostawy do udostępnienia nowego serwera MCS katalogi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="57680-217">Wykonaj kroki opisane w tym [artykułu](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="57680-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="57680-218">Grupa 3 ręczny lub skryptu akcji 2:</span><span class="sxs-lookup"><span data-stu-id="57680-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="57680-219">***Utwórz ponownie MCS katalogi na platformie Azure***</span><span class="sxs-lookup"><span data-stu-id="57680-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="57680-220">Istniejące klony MCS lub Odwiedziny w lokacji głównej nie będą replikowane do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="57680-221">Należy ponownie utworzyć te klony przy użyciu zreplikowanych VDA wzorca i Azure ARM inicjowania obsługi administracyjnej z kontrolera dostarczania. Wykonaj kroki opisane w tym [artykułu](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) do tworzenia katalogów serwera MCS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57680-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![Plan odzyskiwania program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="57680-223">Możesz używać skryptów w [lokalizacji](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) zaktualizować DNS o nowe adresy IP z nieudane za pośrednictwem > maszyn wirtualnych lub dołączyć modułu równoważenia obciążenia na nieudane przez maszynę wirtualną, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="57680-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="57680-224">Ten test trybu failover</span><span class="sxs-lookup"><span data-stu-id="57680-224">Doing a test failover</span></span>

<span data-ttu-id="57680-225">Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) przeprowadzić test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="57680-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![Plan odzyskiwania](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="57680-227">Podczas pracy w trybie failover</span><span class="sxs-lookup"><span data-stu-id="57680-227">Doing a failover</span></span>

<span data-ttu-id="57680-228">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="57680-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57680-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57680-229">Next steps</span></span>

<span data-ttu-id="57680-230">Możesz [więcej](https://aka.ms/citrix-xenapp-xendesktop-with-asr) o replikowanie wdrożenia program Citrix XenApp i XenDesktop w oficjalnym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="57680-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="57680-231">Przyjrzyj się wskazówki dotyczące [replikacji z innych aplikacji](site-recovery-workload.md) przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="57680-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
