---
title: "Planowanie wydajności i skalowania replikacji maszyny Wirtualnej funkcji Hyper-V (bez VMM) na platformie Azure za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Użyj w tym artykule Planowanie wydajności i skalowania podczas replikowania maszyn wirtualnych funkcji Hyper-V do platformy Azure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="b15ca-103">Krok 3: Planowanie wydajności i skalowania dla funkcji Hyper-V do platformy Azure replikacji</span><span class="sxs-lookup"><span data-stu-id="b15ca-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="b15ca-104">Niniejszy artykuł służy zorientować się planowanie pojemności i skalowania, podczas replikacji (bez programu System Center VMM), maszynach wirtualnych funkcji Hyper-V lokalnego do platformy Azure z [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b15ca-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="b15ca-105">Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu i zadawaj pytania techniczne na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b15ca-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="b15ca-106">Jak rozpocząć planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="b15ca-106">How do I start capacity planning?</span></span>


<span data-ttu-id="b15ca-107">Zbieranie informacji o środowisku replikacji, a następnie planowania pojemności, korzystając z tych informacji, wraz z uwagi wyróżniane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b15ca-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="b15ca-108">Zbieranie informacji</span><span class="sxs-lookup"><span data-stu-id="b15ca-108">Gather information</span></span>

1. <span data-ttu-id="b15ca-109">Zebrać informacje o środowisku replikacji, w tym o maszynach wirtualnych, liczbie dysków na maszynę wirtualną oraz pojemności dysków.</span><span class="sxs-lookup"><span data-stu-id="b15ca-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="b15ca-110">Określ częstotliwość codziennych zmian (przenoszenia) dla replikowanych danych.</span><span class="sxs-lookup"><span data-stu-id="b15ca-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="b15ca-111">Pobierz [narzędzia do planowania pojemności funkcji Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) uzyskać szybkość zmian.</span><span class="sxs-lookup"><span data-stu-id="b15ca-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="b15ca-112">Zaleca się uruchomić to narzędzie dłużej niż przez tydzień do przechwytywania średnie.</span><span class="sxs-lookup"><span data-stu-id="b15ca-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="b15ca-113">Ustalenia pojemności</span><span class="sxs-lookup"><span data-stu-id="b15ca-113">Figure out capacity</span></span>

<span data-ttu-id="b15ca-114">Na podstawie informacji, które zostały zbieranie, uruchom [Planisty wydajności odzyskiwania lokacji](http://aka.ms/asr-capacity-planner-excel) aby przeanalizować środowiska źródłowego i obciążeń, oszacować wymagania dotyczące przepustowości i zasobów serwera do lokalizacji źródłowej i zasobów (maszyn wirtualnych i magazynu itp.), wymagających w lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="b15ca-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="b15ca-115">Narzędzie można uruchomić na kilka metod:</span><span class="sxs-lookup"><span data-stu-id="b15ca-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="b15ca-116">Planowanie szybkie: Uruchom narzędzie w tym trybie można pobrać projekcje sieci i serwera oparte na średnich liczbach maszyn wirtualnych, dysków, magazynu i szybkość zmian.</span><span class="sxs-lookup"><span data-stu-id="b15ca-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="b15ca-117">Szczegółowe planowanie: Uruchom narzędzie w tym trybie i podaj szczegóły poszczególnych obciążeń na poziomie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b15ca-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="b15ca-118">Analizowanie zgodności maszyny Wirtualnej i uzyskać projekcje sieci i serwera.</span><span class="sxs-lookup"><span data-stu-id="b15ca-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="b15ca-119">Teraz uruchom narzędzie:</span><span class="sxs-lookup"><span data-stu-id="b15ca-119">Now run the tool:</span></span>

1. <span data-ttu-id="b15ca-120">Pobierz [narzędzia](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="b15ca-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="b15ca-121">Aby uruchomić szybkie planowania, wykonaj [tych instrukcji](site-recovery-capacity-planner.md#run-the-quick-planner)i wybrać scenariusz **funkcji Hyper-V w systemie Azure**.</span><span class="sxs-lookup"><span data-stu-id="b15ca-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="b15ca-122">Aby uruchomić szczegółowe planowania, wykonaj [tych instrukcji](site-recovery-capacity-planner.md#run-the-detailed-planner)i wybrać scenariusz **funkcji Hyper-V w systemie Azure**.</span><span class="sxs-lookup"><span data-stu-id="b15ca-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="b15ca-123">Sterowania przepustowością sieci</span><span class="sxs-lookup"><span data-stu-id="b15ca-123">Control network bandwidth</span></span>

<span data-ttu-id="b15ca-124">Po został obliczony przepustowości, które są potrzebne, masz kilka opcji kontrolowania ilość przepustowości używanej w ramach replikacji:</span><span class="sxs-lookup"><span data-stu-id="b15ca-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="b15ca-125">**Ograniczanie przepustowości**: ruch funkcji Hyper-V, który replikuje Azure przechodzi przez konkretnego hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b15ca-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="b15ca-126">Możesz ograniczyć przepustowość na serwerze hosta.</span><span class="sxs-lookup"><span data-stu-id="b15ca-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="b15ca-127">**Wpływ przepustowości**: może mieć wpływ na przepustowość wykorzystywaną podczas replikacji przy użyciu kilku kluczy rejestru.</span><span class="sxs-lookup"><span data-stu-id="b15ca-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="b15ca-128">Ograniczanie przepustowości</span><span class="sxs-lookup"><span data-stu-id="b15ca-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="b15ca-129">Otwórz przystawkę MMC usługi Microsoft Azure Backup na serwerze hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b15ca-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="b15ca-130">Domyślnie skrót do usługi Microsoft Azure Backup jest dostępny na pulpicie lub w folderze C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="b15ca-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="b15ca-131">W przystawce kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b15ca-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="b15ca-132">Na karcie **Ograniczanie przepływności** wybierz opcję **Włącz ograniczanie użycia przepustowości internetowej dla operacji kopii zapasowych** i ustaw limity dla godzin roboczych i godzin innych niż godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="b15ca-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="b15ca-133">Prawidłowy zakres: od 512 Kb/s do 102 Mb/s na sekundę.</span><span class="sxs-lookup"><span data-stu-id="b15ca-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Ograniczanie przepustowości](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="b15ca-135">Możesz też użyć polecenia cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx), aby ustawić ograniczanie przepływności.</span><span class="sxs-lookup"><span data-stu-id="b15ca-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="b15ca-136">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="b15ca-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="b15ca-137">**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="b15ca-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="b15ca-138">Wywieranie wpływu na przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="b15ca-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="b15ca-139">W rejestrze przejdź do pozycji **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="b15ca-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="b15ca-140">Wpływ na przepustowość ruchu replikacji dysku, zmodyfikuj wartość **UploadThreadsPerVM**, lub Utwórz klucz, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="b15ca-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="b15ca-141">Wpływ przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="b15ca-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="b15ca-142">Wartość domyślna to 4.</span><span class="sxs-lookup"><span data-stu-id="b15ca-142">The default value is 4.</span></span> <span data-ttu-id="b15ca-143">W sieci „o nadmiarowych zasobach” należy zmienić wartości domyślne tych kluczy rejestru.</span><span class="sxs-lookup"><span data-stu-id="b15ca-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="b15ca-144">Wartość maksymalna to 32.</span><span class="sxs-lookup"><span data-stu-id="b15ca-144">The maximum is 32.</span></span> <span data-ttu-id="b15ca-145">Monitoruj ruch, aby zoptymalizować tę wartość.</span><span class="sxs-lookup"><span data-stu-id="b15ca-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b15ca-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b15ca-146">Next steps</span></span>

<span data-ttu-id="b15ca-147">Przejdź do [krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="b15ca-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
