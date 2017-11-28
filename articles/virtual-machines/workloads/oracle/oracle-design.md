---
title: "aaaDesign i wdrożenie Oracle bazy danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Projektowania i implementacji bazy danych programu Oracle w środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="eaa16-103">Projektowania i implementacji bazy danych programu Oracle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eaa16-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="eaa16-104">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="eaa16-104">Assumptions</span></span>

- <span data-ttu-id="eaa16-105">Planowane jest toomigrate z tooAzure lokalnej bazy danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="eaa16-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="eaa16-106">Masz zrozumienia hello różnych metryk w raportach Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="eaa16-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="eaa16-107">Możesz wiedzę na temat linii bazowej wydajności aplikacji oraz wykorzystania platformy.</span><span class="sxs-lookup"><span data-stu-id="eaa16-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="eaa16-108">Cele</span><span class="sxs-lookup"><span data-stu-id="eaa16-108">Goals</span></span>

- <span data-ttu-id="eaa16-109">Zrozumienie sposobu toooptimize wdrożenia programu Oracle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa16-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="eaa16-110">Poznaj opcje dla bazy danych Oracle w środowisku Azure dostrajania wydajności.</span><span class="sxs-lookup"><span data-stu-id="eaa16-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="eaa16-111">Witaj różnice między lokalnymi i Azure implementacji</span><span class="sxs-lookup"><span data-stu-id="eaa16-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="eaa16-112">Poniżej przedstawiono niektóre istotne tookeep rzeczy pamiętać podczas migracji lokalnych tooAzure aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eaa16-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="eaa16-113">Jedną istotną różnicą jest to, że w implementacji platformy Azure, zasobów, takich jak maszyn wirtualnych, dysków i sieci wirtualne są współużytkowane przez innych klientów.</span><span class="sxs-lookup"><span data-stu-id="eaa16-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="eaa16-114">Ponadto zasobów może być ograniczony na podstawie wymagań hello.</span><span class="sxs-lookup"><span data-stu-id="eaa16-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="eaa16-115">Zamiast koncentrujących się na temat niepowodzenia (MTBF), Azure więcej koncentruje się na pozostałych hello awarii (MTTR).</span><span class="sxs-lookup"><span data-stu-id="eaa16-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="eaa16-116">Witaj poniższej tabeli przedstawiono niektóre hello różnic między implementacją lokalną i Azure implementacji bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="eaa16-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="eaa16-117">**Implementacja lokalna**</span><span class="sxs-lookup"><span data-stu-id="eaa16-117">**On-premises implementation**</span></span> | <span data-ttu-id="eaa16-118">**Implementacja Azure**</span><span class="sxs-lookup"><span data-stu-id="eaa16-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="eaa16-119">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="eaa16-119">**Networking**</span></span> |<span data-ttu-id="eaa16-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="eaa16-120">LAN/WAN</span></span>  |<span data-ttu-id="eaa16-121">SDN (technologia Sdn)</span><span class="sxs-lookup"><span data-stu-id="eaa16-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="eaa16-122">**Grupy zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="eaa16-122">**Security group**</span></span> |<span data-ttu-id="eaa16-123">Ograniczenia adresu IP i portu narzędzi</span><span class="sxs-lookup"><span data-stu-id="eaa16-123">IP/port restriction tools</span></span> |[<span data-ttu-id="eaa16-124">Grupy zabezpieczeń sieci (NSG)</span><span class="sxs-lookup"><span data-stu-id="eaa16-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="eaa16-125">**Odporność**</span><span class="sxs-lookup"><span data-stu-id="eaa16-125">**Resilience**</span></span> |<span data-ttu-id="eaa16-126">MTBF (Średni czas między awariami)</span><span class="sxs-lookup"><span data-stu-id="eaa16-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="eaa16-127">MTTR (toorecovery średniego czasu)</span><span class="sxs-lookup"><span data-stu-id="eaa16-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="eaa16-128">**Planowana konserwacja**</span><span class="sxs-lookup"><span data-stu-id="eaa16-128">**Planned maintenance**</span></span> |<span data-ttu-id="eaa16-129">Stosowanie poprawek do uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="eaa16-129">Patching/upgrades</span></span>|<span data-ttu-id="eaa16-130">[Zestawy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (poprawki/uaktualniania zarządzane przez usługę Azure)</span><span class="sxs-lookup"><span data-stu-id="eaa16-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="eaa16-131">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="eaa16-131">**Resource**</span></span> |<span data-ttu-id="eaa16-132">Dedykowany</span><span class="sxs-lookup"><span data-stu-id="eaa16-132">Dedicated</span></span>  |<span data-ttu-id="eaa16-133">Współużytkowane z innymi klientami</span><span class="sxs-lookup"><span data-stu-id="eaa16-133">Shared with other clients</span></span>|
> | <span data-ttu-id="eaa16-134">**Regiony**</span><span class="sxs-lookup"><span data-stu-id="eaa16-134">**Regions**</span></span> |<span data-ttu-id="eaa16-135">Centra danych</span><span class="sxs-lookup"><span data-stu-id="eaa16-135">Datacenters</span></span> |[<span data-ttu-id="eaa16-136">Pary regionu</span><span class="sxs-lookup"><span data-stu-id="eaa16-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="eaa16-137">**Storage**</span><span class="sxs-lookup"><span data-stu-id="eaa16-137">**Storage**</span></span> |<span data-ttu-id="eaa16-138">Dyski fizyczne/w sieci SAN</span><span class="sxs-lookup"><span data-stu-id="eaa16-138">SAN/physical disks</span></span> |[<span data-ttu-id="eaa16-139">Zarządzane Azure magazynu</span><span class="sxs-lookup"><span data-stu-id="eaa16-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="eaa16-140">**Skalowanie**</span><span class="sxs-lookup"><span data-stu-id="eaa16-140">**Scale**</span></span> |<span data-ttu-id="eaa16-141">Skalowanie w pionie</span><span class="sxs-lookup"><span data-stu-id="eaa16-141">Vertical scale</span></span> |<span data-ttu-id="eaa16-142">Skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="eaa16-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="eaa16-143">Wymagania</span><span class="sxs-lookup"><span data-stu-id="eaa16-143">Requirements</span></span>

- <span data-ttu-id="eaa16-144">Określenie hello stopy rozmiaru i wzrostu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="eaa16-145">Ustal wymagania dotyczące IOPS hello, które można oszacować na podstawie raportów Oracle AWR lub innych narzędzi do monitorowania sieci.</span><span class="sxs-lookup"><span data-stu-id="eaa16-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="eaa16-146">Opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="eaa16-146">Configuration options</span></span>

<span data-ttu-id="eaa16-147">Istnieją cztery potencjalnych obszarów dostroić tooimprove wydajności w środowisku platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="eaa16-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="eaa16-148">Rozmiar maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eaa16-148">Virtual machine size</span></span>
- <span data-ttu-id="eaa16-149">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="eaa16-149">Network throughput</span></span>
- <span data-ttu-id="eaa16-150">Typy dysków i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="eaa16-150">Disk types and configurations</span></span>
- <span data-ttu-id="eaa16-151">Ustawienia pamięci podręcznej dysku</span><span class="sxs-lookup"><span data-stu-id="eaa16-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="eaa16-152">Generowanie raportu AWR</span><span class="sxs-lookup"><span data-stu-id="eaa16-152">Generate an AWR report</span></span>

<span data-ttu-id="eaa16-153">Jeśli korzystasz z istniejącej bazy danych programu Oracle i planowania toomigrate tooAzure, masz kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="eaa16-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="eaa16-154">Możesz uruchomić hello Oracle AWR raport tooget hello metryki (IOPS, MB/s, GiBs i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="eaa16-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="eaa16-155">Następnie wybierz powitalne maszyny Wirtualnej w oparciu metryki hello zebranych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="eaa16-156">Lub możesz skontaktować się infrastruktury zespołu tooget podobne informacje.</span><span class="sxs-lookup"><span data-stu-id="eaa16-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="eaa16-157">Należy rozważyć działania raportu AWR podczas obciążeń zarówno regularne i szczytu, więc możesz porównać.</span><span class="sxs-lookup"><span data-stu-id="eaa16-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="eaa16-158">Na podstawie tych raportów, można rozmiar powitalne maszyn wirtualnych na podstawie obciążenia średni hello lub hello maksymalne obciążenie.</span><span class="sxs-lookup"><span data-stu-id="eaa16-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="eaa16-159">Poniżej przedstawiono przykładowy sposób toogenerate AWR raportu:</span><span class="sxs-lookup"><span data-stu-id="eaa16-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="eaa16-160">Kluczowych metryk</span><span class="sxs-lookup"><span data-stu-id="eaa16-160">Key metrics</span></span>

<span data-ttu-id="eaa16-161">Poniżej przedstawiono metryki hello można uzyskać z hello AWR raportu:</span><span class="sxs-lookup"><span data-stu-id="eaa16-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="eaa16-162">Całkowita liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="eaa16-162">Total number of cores</span></span>
- <span data-ttu-id="eaa16-163">Szybkość zegara Procesora</span><span class="sxs-lookup"><span data-stu-id="eaa16-163">CPU clock speed</span></span>
- <span data-ttu-id="eaa16-164">Całkowitej ilości pamięci w GB</span><span class="sxs-lookup"><span data-stu-id="eaa16-164">Total memory in GB</span></span>
- <span data-ttu-id="eaa16-165">Użycie procesora CPU</span><span class="sxs-lookup"><span data-stu-id="eaa16-165">CPU utilization</span></span>
- <span data-ttu-id="eaa16-166">Szczytowa szybkość transferu danych</span><span class="sxs-lookup"><span data-stu-id="eaa16-166">Peak data transfer rate</span></span>
- <span data-ttu-id="eaa16-167">Liczba operacji We/Wy zmiany (odczyt/zapis)</span><span class="sxs-lookup"><span data-stu-id="eaa16-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="eaa16-168">Wykonaj ponownie szybkość dziennika (MB/s)</span><span class="sxs-lookup"><span data-stu-id="eaa16-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="eaa16-169">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="eaa16-169">Network throughput</span></span>
- <span data-ttu-id="eaa16-170">Szybkość opóźnienia sieci (niski/wysoka)</span><span class="sxs-lookup"><span data-stu-id="eaa16-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="eaa16-171">Rozmiar bazy danych w GB</span><span class="sxs-lookup"><span data-stu-id="eaa16-171">Database size in GB</span></span>
- <span data-ttu-id="eaa16-172">Bajty odebrane za pomocą programu SQL * Net z / tooclient</span><span class="sxs-lookup"><span data-stu-id="eaa16-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="eaa16-173">Rozmiar maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eaa16-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="eaa16-174">1. Szacowanie rozmiaru maszyny Wirtualnej, na podstawie użycia Procesora, pamięci i operacji We/Wy z hello AWR raportu</span><span class="sxs-lookup"><span data-stu-id="eaa16-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="eaa16-175">Jedyną operacją, której może wyglądać na jest hello najwyższego pięć czasu pierwszego planu zdarzenia wskazujące, gdzie są hello wąskich gardeł systemu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="eaa16-176">Na przykład w hello po diagramu, synchronizacji plików dziennika hello jest u góry hello.</span><span class="sxs-lookup"><span data-stu-id="eaa16-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="eaa16-177">Wskazuje liczbę hello czeka przed hello LGWR zapisuje plik dziennika Powtórz toohello hello dziennika buforu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="eaa16-178">Te wyniki wskazują, że lepiej wykonuje magazynu lub dyski są wymagane.</span><span class="sxs-lookup"><span data-stu-id="eaa16-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="eaa16-179">Ponadto hello diagram przedstawia również, hello liczba procesora CPU (rdzenie) oraz hello ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="eaa16-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="eaa16-181">Witaj Poniższy diagram przedstawia hello całkowita liczba operacji We/Wy odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="eaa16-182">Znaleziono 59 GB do odczytu i 247.3 zapisane w czasie hello hello raportu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="eaa16-184">2. Wybierz Maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="eaa16-184">2. Choose a VM</span></span>

<span data-ttu-id="eaa16-185">Na podstawie hello informacji zebranych od hello AWR raportu, hello następnym krokiem jest toochoose maszyny Wirtualnej o rozmiarze podobne, który spełnia wymagania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="eaa16-186">Listę dostępnych maszyn wirtualnych można znaleźć w artykule hello [zoptymalizowanych pod kątem pamięci](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="eaa16-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="eaa16-187">3. Dostosowywanie rozmiaru maszyny Wirtualnej hello oparte na powitania ACU podobne serią maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eaa16-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="eaa16-188">Po wybraniu hello maszyny Wirtualnej, należy zwrócić uwagę toohello ACU dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="eaa16-189">Można wybrać innej maszyny Wirtualnej, oparte na powitania wartość ACU, dostosowany do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="eaa16-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="eaa16-190">Aby uzyskać więcej informacji, zobacz [jednostki rozwiązań usługi obliczenia Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="eaa16-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Zrzut ekranu przedstawiający stronę jednostki ACU hello](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="eaa16-192">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="eaa16-192">Network throughput</span></span>

<span data-ttu-id="eaa16-193">powitania po diagram przedstawia hello relację między przepływności i IOPS:</span><span class="sxs-lookup"><span data-stu-id="eaa16-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![Zrzut ekranu przedstawiający przepływność](./media/oracle-design/throughput.png)

<span data-ttu-id="eaa16-195">przepustowość sieci Całkowita Hello jest szacowana oparte na powitania następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="eaa16-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="eaa16-196">SQL * Net ruchu</span><span class="sxs-lookup"><span data-stu-id="eaa16-196">SQL*Net traffic</span></span>
- <span data-ttu-id="eaa16-197">MB/s x wielu serwerów (strumienia wychodzącego takich jak Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="eaa16-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="eaa16-198">Innych czynników, takich jak replikacja aplikacji</span><span class="sxs-lookup"><span data-stu-id="eaa16-198">Other factors, such as application replication</span></span>

![Zrzut ekranu przedstawiający hello SQL * przepustowość sieci](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="eaa16-200">Zgodnie z wymaganiami przepustowości sieci, istnieją różne typy bramy dla toochoose z.</span><span class="sxs-lookup"><span data-stu-id="eaa16-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="eaa16-201">Obejmują one basic, VpnGw i usługa Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eaa16-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="eaa16-202">Aby uzyskać więcej informacji, zobacz hello [bramy sieci VPN, na stronie dotyczącej cen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="eaa16-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="eaa16-203">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="eaa16-203">**Recommendations**</span></span>

- <span data-ttu-id="eaa16-204">Opóźnienie sieci jest wyższy porównaniu tooan lokalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eaa16-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="eaa16-205">Zmniejszenie sieci round rund może znacznie poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="eaa16-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="eaa16-206">aplikacje, które mają wysokie transakcji lub "chatty" aplikacji na powitania skonsolidować przechodzenia tooreduce tej samej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="eaa16-207">Typy dysków i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="eaa16-207">Disk types and configurations</span></span>

- <span data-ttu-id="eaa16-208">*Domyślna dysków systemu operacyjnego*: tych typów dysków oferują trwałych danych i buforowania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="eaa16-209">Są zoptymalizowane pod kątem dostępu do systemu operacyjnego podczas uruchamiania, a nie są przeznaczone dla jednej transakcyjnej lub magazynu danych obciążenia (analitycznych).</span><span class="sxs-lookup"><span data-stu-id="eaa16-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="eaa16-210">*Niezarządzane dysków*: Z tych typów dysku zarządzasz kont magazynu hello, w których są przechowywane pliki wirtualnego dysku twardego (VHD) hello, które odpowiadają tooyour dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="eaa16-211">Pliki VHD są przechowywane jako stronicowe obiekty BLOB na kontach magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa16-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="eaa16-212">*Dyski zarządzane*: Azure zarządza kontami magazynu hello, których używasz dla dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="eaa16-213">Należy określić typ dysku hello (standardowy lub premium) i hello rozmiar dysku hello, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="eaa16-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="eaa16-214">Azure tworzy i którymi zarządza hello dysku dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="eaa16-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="eaa16-215">*Dyski magazynu Premium*: tych typów dysków są najbardziej odpowiednie dla obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="eaa16-216">Dyski maszyny Wirtualnej obsługuje magazynu Premium, które można dołączyć toospecific rozmiar serii maszyn wirtualnych, takie jak seria DS, DSv2 i GS oraz F maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="eaa16-217">dysku premium Hello jest dostarczany z różnych rozmiarach i można wybrać dyski od too4 32 GB, 096 GB.</span><span class="sxs-lookup"><span data-stu-id="eaa16-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="eaa16-218">Rozmiar każdego dysku ma specyfikacjami wydajności.</span><span class="sxs-lookup"><span data-stu-id="eaa16-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="eaa16-219">W zależności od wymagań aplikacji można dołączyć co najmniej jeden tooyour dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="eaa16-220">Po utworzeniu nowego dysku zarządzanego z hello portalu można wybrać hello **typ konta** dla typu hello dysku ma toouse.</span><span class="sxs-lookup"><span data-stu-id="eaa16-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="eaa16-221">Należy pamiętać, że nie wszystkie dostępne dyski są wyświetlane w menu rozwijanym hello.</span><span class="sxs-lookup"><span data-stu-id="eaa16-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="eaa16-222">Po wybraniu określonego rozmiaru maszyny Wirtualnej hello menu pokazuje tylko hello magazynu premium dostępne jednostki SKU, które są oparte na rozmiar tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Zrzut ekranu przedstawiający stronę dysków zarządzanych w hello](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="eaa16-224">Aby uzyskać więcej informacji, zobacz [zarządzanych dysków dla maszyny wirtualne i Magazyn w warstwie Premium wysokiej wydajności](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="eaa16-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="eaa16-225">Po skonfigurowaniu magazynu na maszynie Wirtualnej można tooload testu hello dysków przed utworzeniem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="eaa16-226">Znajomość szybkości operacji We/Wy hello pod względem zarówno opóźnienia i przepływności pozwalają określić, czy maszyny wirtualne hello obsługuje hello oczekiwano przepływności z obiektami docelowymi opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="eaa16-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="eaa16-227">Istnieje wiele narzędzi dla aplikacji testów obciążenia, takich jak Oracle Orion, Sysbench i Fio.</span><span class="sxs-lookup"><span data-stu-id="eaa16-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="eaa16-228">Ponownie uruchom test obciążenia powitania po wdrożeniu bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="eaa16-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="eaa16-229">Uruchom regularne i szczytowa obciążeń i hello Pokaż wyniki hello linii bazowej środowiska.</span><span class="sxs-lookup"><span data-stu-id="eaa16-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="eaa16-230">Może być większe znaczenie toosize hello magazynu na podstawie współczynnika IOPS hello zamiast hello rozmiar magazynu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="eaa16-231">Na przykład w razie potrzeby hello IOPS jest 5000, ale wymagane jest tylko 200 GB można nadal otrzymać hello P30 klasy premium dysku nawet, jeśli zawiera więcej niż 200 GB pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="eaa16-232">szybkość IOPS Hello można uzyskać z hello AWR raportu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="eaa16-233">Określono hello Powtórz dziennika, fizyczne odczyty i zapisy szybkości.</span><span class="sxs-lookup"><span data-stu-id="eaa16-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/awr_report.png)

<span data-ttu-id="eaa16-235">Na przykład rozmiar Powtórz hello jest 12,200,000 bajtów na sekundę, która jest równa too11.63 MB/s.</span><span class="sxs-lookup"><span data-stu-id="eaa16-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="eaa16-236">Witaj IOPS jest 12,200,000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="eaa16-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="eaa16-237">Po umieszczeniu jasny obraz powitania wymagań operacji We/Wy, można wybrać kombinację dysków, które są najlepiej nadaje się toomeet tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="eaa16-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="eaa16-238">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="eaa16-238">**Recommendations**</span></span>

- <span data-ttu-id="eaa16-239">Dla tabel danych rozmieszczenie obciążenia We/Wy hello liczba dysków za pomocą funkcji ASM Oracle lub zarządzanego magazynu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="eaa16-240">Jak zwiększa rozmiar bloku hello we/wy dla operacji intensywnego odczytu i zapisu intensywnie, Dodaj więcej dysków danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="eaa16-241">Zwiększenie rozmiaru bloku hello dużych sekwencyjnych procesów.</span><span class="sxs-lookup"><span data-stu-id="eaa16-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="eaa16-242">Użyj danych kompresji tooreduce we/wy (dla danych i indeksów).</span><span class="sxs-lookup"><span data-stu-id="eaa16-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="eaa16-243">Oddzielne Powtórz dzienniki systemu i temps, a cofnąć usług terminalowych na dyskach danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="eaa16-244">Nie należy umieszczać plików aplikacji na domyślne dysków systemu operacyjnego (/ dev/sda).</span><span class="sxs-lookup"><span data-stu-id="eaa16-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="eaa16-245">Te dyski nie są zoptymalizowane dla maszyny Wirtualnej szybkiego czas uruchamiania i nie może zawierać dobrą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eaa16-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="eaa16-246">Ustawienia pamięci podręcznej dysku</span><span class="sxs-lookup"><span data-stu-id="eaa16-246">Disk cache settings</span></span>

<span data-ttu-id="eaa16-247">Istnieją trzy opcje buforowania na hoście:</span><span class="sxs-lookup"><span data-stu-id="eaa16-247">There are three options for host caching:</span></span>

- <span data-ttu-id="eaa16-248">*Tylko do odczytu*: wszystkie żądania są buforowane dla przyszłych operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="eaa16-249">Zapisuje wszystkie są zachowywane bezpośrednio tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="eaa16-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="eaa16-250">*Odczyt i zapis*: jest to "odczytu z wyprzedzeniem" algorytmu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="eaa16-251">Witaj odczytuje i zapisuje są buforowane dla przyszłych operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="eaa16-252">Zapisy non-write-through są najpierw utrwalone toohello lokalnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="eaa16-253">Dla programu SQL Server zapisy są tooAzure utrwalonego magazynu, ponieważ używa go do zapisu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="eaa16-254">Zapewnia także hello można uzyskać najmniejsze opóźnienia dysku światła obciążeń.</span><span class="sxs-lookup"><span data-stu-id="eaa16-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="eaa16-255">*Brak* (wyłączone): za pomocą tej opcji, można pominąć hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="eaa16-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="eaa16-256">Wszystkie dane hello jest przeniesione toodisk i utrwalone tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="eaa16-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="eaa16-257">Dzięki temu metody hello najwyższej szybkości operacji We/Wy dla intensywnych obciążeń we/wy.</span><span class="sxs-lookup"><span data-stu-id="eaa16-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="eaa16-258">Należy również tootake "kosztów transakcji" pod uwagę.</span><span class="sxs-lookup"><span data-stu-id="eaa16-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="eaa16-259">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="eaa16-259">**Recommendations**</span></span>

<span data-ttu-id="eaa16-260">toomaximize hello przepływności, zalecamy rozpocząć od **Brak** dla buforowania na hoście.</span><span class="sxs-lookup"><span data-stu-id="eaa16-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="eaa16-261">Dla usługi Premium Storage należy pamiętać o tym, należy wyłączyć bariery"hello" w przypadku zainstalowania systemu plików hello za pomocą hello **tylko do odczytu** lub **Brak** opcje.</span><span class="sxs-lookup"><span data-stu-id="eaa16-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="eaa16-262">Zaktualizuj plik /etc/fstab hello hello UUID toohello dysków.</span><span class="sxs-lookup"><span data-stu-id="eaa16-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="eaa16-263">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium dla maszyn wirtualnych systemu Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="eaa16-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Zrzut ekranu przedstawiający stronę dysków zarządzanych w hello](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="eaa16-265">W przypadku dysków systemu operacyjnego, użyj domyślnej **odczytu/zapisu** buforowania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="eaa16-266">Dla systemu, TEMP i cofania użyj **Brak** do buforowania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="eaa16-267">W przypadku danych, użyj **Brak** do buforowania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="eaa16-268">Ale jeśli bazy danych jest tylko do odczytu lub intensywnego odczytu, użyj **tylko do odczytu** buforowania.</span><span class="sxs-lookup"><span data-stu-id="eaa16-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="eaa16-269">Po zapisaniu ustawień dysku danych, chyba że Odinstaluj dysku hello na powitania poziomu systemu operacyjnego i ponownie zainstaluj po dokonaniu zmiany hello nie można zmienić ustawienia pamięci podręcznej hello hosta.</span><span class="sxs-lookup"><span data-stu-id="eaa16-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="eaa16-270">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="eaa16-270">Security</span></span>

<span data-ttu-id="eaa16-271">Po Konfigurowanie i skonfigurowania środowiska Azure hello następnym krokiem jest toosecure sieci.</span><span class="sxs-lookup"><span data-stu-id="eaa16-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="eaa16-272">Poniżej przedstawiono kilka zaleceń:</span><span class="sxs-lookup"><span data-stu-id="eaa16-272">Here are some recommendations:</span></span>

- <span data-ttu-id="eaa16-273">*Zasady grupy NSG*: grupy NSG można zdefiniować przy podsieci lub kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="eaa16-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="eaa16-274">Jest prostsze toocontrol dostęp na poziomie podsieci hello zabezpieczeń i Wymuś routingu dla elementów, jak zapór aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eaa16-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="eaa16-275">*Jumpbox*: bezpieczniejszego dostępu administratorów nie należy bezpośrednio łączyć toohello aplikacji usługi lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="eaa16-276">Jumpbox jest używane jako nośniki między hello administratora komputera i zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa16-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="eaa16-277">![Zrzut ekranu przedstawiający stronę topologii Jumpbox hello](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="eaa16-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="eaa16-278">Witaj administratora maszyny powinno oferować tylko jumpbox toohello dostęp ograniczony IP.</span><span class="sxs-lookup"><span data-stu-id="eaa16-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="eaa16-279">Witaj jumpbox powinien mieć dostęp toohello aplikacji i baz danych.</span><span class="sxs-lookup"><span data-stu-id="eaa16-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="eaa16-280">*Sieć prywatna* (podsieci): zaleca się, czy masz usługi aplikacji hello i bazy danych w różnych podsieciach, lepszą kontrolę można ustawić przez zasady grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="eaa16-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="eaa16-281">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="eaa16-281">Additional reading</span></span>

- [<span data-ttu-id="eaa16-282">Configure Oracle ASM (Konfigurowanie programu Oracle ASM)</span><span class="sxs-lookup"><span data-stu-id="eaa16-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="eaa16-283">Skonfiguruj Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="eaa16-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="eaa16-284">Konfigurowanie bramy Golden Oracle</span><span class="sxs-lookup"><span data-stu-id="eaa16-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="eaa16-285">Oracle kopii zapasowych i odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="eaa16-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="eaa16-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eaa16-286">Next steps</span></span>

- [<span data-ttu-id="eaa16-287">Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="eaa16-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="eaa16-288">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eaa16-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
