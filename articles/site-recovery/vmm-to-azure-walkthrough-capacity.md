---
title: "aaaPlan wydajności i skalowania dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (w programie VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Użyj tego artykułu tooplan pojemności i skali, podczas replikacji maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="cea1b-103">Krok 3: Planowanie wydajności i skalowania dla replikacji tooAzure funkcji Hyper-V (w programie VMM)</span><span class="sxs-lookup"><span data-stu-id="cea1b-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="cea1b-104">Po przejrzeniu hello [wymagania wstępne dotyczące wdrażania](vmm-to-azure-walkthrough-prerequisites.md), użyj tego artykułu toofigure limit planowania pojemności, jak i skalowanie podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu System Center Virtual Machine Manager (VMM), z [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cea1b-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="cea1b-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cea1b-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="cea1b-106">Jak rozpocząć planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="cea1b-106">How do I start capacity planning?</span></span>


<span data-ttu-id="cea1b-107">Możesz zbierać informacje o środowisku replikacji i następnie pojemności planu przy użyciu hello dane, wraz z uwagi hello wyróżniane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="cea1b-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="cea1b-108">Zbieranie informacji</span><span class="sxs-lookup"><span data-stu-id="cea1b-108">Gather information</span></span>

1. <span data-ttu-id="cea1b-109">Zebrać informacje o środowisku replikacji, w tym o maszynach wirtualnych, liczbie dysków na maszynę wirtualną oraz pojemności dysków.</span><span class="sxs-lookup"><span data-stu-id="cea1b-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="cea1b-110">Określ częstotliwość codziennych zmian (przenoszenia) dla replikowanych danych.</span><span class="sxs-lookup"><span data-stu-id="cea1b-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="cea1b-111">Pobierz hello [narzędzia do planowania pojemności funkcji Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) szybkość zmian hello tooget.</span><span class="sxs-lookup"><span data-stu-id="cea1b-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="cea1b-112">Firma Microsoft zaleca się, że możesz uruchomić to narzędzie za pośrednictwem toocapture tygodnia średnie.</span><span class="sxs-lookup"><span data-stu-id="cea1b-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="cea1b-113">Ustalenia pojemności</span><span class="sxs-lookup"><span data-stu-id="cea1b-113">Figure out capacity</span></span>

<span data-ttu-id="cea1b-114">Na podstawie informacji hello znasz zbieranie, uruchom hello [Planisty wydajności odzyskiwania lokacji](http://aka.ms/asr-capacity-planner-excel) tooanalyze Twojego środowiska źródłowego i obciążeń, oszacować wymagania dotyczące przepustowości i zasobów serwera dla lokalizacji źródła hello i hello zasoby (maszyn wirtualnych i magazynu itp.), które należy w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="cea1b-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="cea1b-115">Można uruchomić narzędzie hello w kilka metod:</span><span class="sxs-lookup"><span data-stu-id="cea1b-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="cea1b-116">Planowanie szybkie: Uruchom narzędzie hello w tym trybie tooget sieci i serwera prognozy oparte na średnich liczbach maszyn wirtualnych, dysków, magazynu i szybkość zmian.</span><span class="sxs-lookup"><span data-stu-id="cea1b-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="cea1b-117">Szczegółowe planowanie: Uruchom narzędzie hello w tym trybie i podaj szczegóły poszczególnych obciążeń na poziomie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cea1b-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="cea1b-118">Analizowanie zgodności maszyny Wirtualnej i uzyskać projekcje sieci i serwera.</span><span class="sxs-lookup"><span data-stu-id="cea1b-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="cea1b-119">Teraz uruchom narzędzie hello:</span><span class="sxs-lookup"><span data-stu-id="cea1b-119">Now run hello tool:</span></span>

1. <span data-ttu-id="cea1b-120">Pobierz hello [narzędzia](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="cea1b-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="cea1b-121">Szybkie planner hello toorun wykonaj [tych instrukcji](site-recovery-capacity-planner.md#run-the-quick-planner)oraz scenariusz hello wybierz **tooAzure funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cea1b-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="cea1b-122">toorun hello planner szczegółowe, należy wykonać [tych instrukcji](site-recovery-capacity-planner.md#run-the-detailed-planner)oraz scenariusz wybierz hello **tooAzure funkcji Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cea1b-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="cea1b-123">Sterowania przepustowością sieci</span><span class="sxs-lookup"><span data-stu-id="cea1b-123">Control network bandwidth</span></span>

<span data-ttu-id="cea1b-124">Po znasz obliczeniowej hello wymaganą przepustowość, masz kilka opcji kontrolowanie hello ilość przepustowości używanej w ramach replikacji:</span><span class="sxs-lookup"><span data-stu-id="cea1b-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="cea1b-125">**Ograniczanie przepustowości**: ruch funkcji Hyper-V, który replikuje tooAzure przechodzi przez konkretnego hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cea1b-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="cea1b-126">Można ograniczyć przepustowość na powitania serwera hosta.</span><span class="sxs-lookup"><span data-stu-id="cea1b-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="cea1b-127">**Wpływ przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru.</span><span class="sxs-lookup"><span data-stu-id="cea1b-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="cea1b-128">Ograniczanie przepustowości</span><span class="sxs-lookup"><span data-stu-id="cea1b-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="cea1b-129">Otwórz hello Microsoft Azure Backup przystawka programu MMC na serwerze hosta funkcji Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="cea1b-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="cea1b-130">Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="cea1b-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="cea1b-131">W przystawce powitania kliknij **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="cea1b-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="cea1b-132">Na powitania **ograniczania** wybierz pozycję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**i Ustaw limity hello do pracy oraz innych niż godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="cea1b-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="cea1b-133">Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.</span><span class="sxs-lookup"><span data-stu-id="cea1b-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Ograniczanie przepustowości](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="cea1b-135">Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cea1b-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="cea1b-136">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="cea1b-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="cea1b-137">**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="cea1b-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="cea1b-138">Wywieranie wpływu na przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="cea1b-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="cea1b-139">W rejestrze hello Przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="cea1b-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="cea1b-140">tooinfluence hello przepustowości ruchu replikacji dysku, zmodyfikuj hello wartość hello **UploadThreadsPerVM**, lub Utwórz klucz hello, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="cea1b-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="cea1b-141">tooinfluence hello przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość hello **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="cea1b-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="cea1b-142">Witaj, wartość domyślna to 4.</span><span class="sxs-lookup"><span data-stu-id="cea1b-142">hello default value is 4.</span></span> <span data-ttu-id="cea1b-143">W sieci "o nadmiarowych zasobach" należy zmienić te klucze rejestru hello wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="cea1b-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="cea1b-144">Witaj maksymalna to 32.</span><span class="sxs-lookup"><span data-stu-id="cea1b-144">hello maximum is 32.</span></span> <span data-ttu-id="cea1b-145">Monitorowanie ruchu toooptimize hello wartość.</span><span class="sxs-lookup"><span data-stu-id="cea1b-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea1b-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cea1b-146">Next steps</span></span>

<span data-ttu-id="cea1b-147">Przejdź za[krok 4: Planowanie sieci](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="cea1b-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
